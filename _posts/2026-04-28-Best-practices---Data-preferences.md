---
layout: default
title: "Best practices - Data preferences"
---

## Data preferences

[https://docs.godotengine.org/en/stable/tutorials/best_practices/data_preferences.html](https://docs.godotengine.org/en/stable/tutorials/best_practices/data_preferences.html)
There are different kinds of computational complexities for algorithms. These are three with short explanations and example workflows:

1. constant-time algorithm:
   Takes the same amount of time to finish regardless of how much data you have. A classic example is lookup up a value in a dictionary/hashmap by its key, you just go straight to it.
2. linear-time algorithm:
   This one takes proportionally longer as the data grows. If you double the data, the needed time doubles. An example is looping through every item in a list to find something.
3. logarithmic-time algorithm:
   This one sits right between the previous both, as it cuts the problem in half with each step. Binary search is a classic example. When searching a sorted list of 1 million examples, it takes about 20 steps, because each step elimitates halt the remaining possibilities.

Logarithmic time grows incredibly slow. Every time you multiply the data by 10, it needs only a few extra steps.

```
10 items:
- constant → 1 operation
- logarithmic → ~3 operations
- linear → 10 operations

1,000 items:
- constant → 1 operation
- logarithmic → ~10 operations
- linear → 1,000 operations

1,000,000 items:
- constant → 1 operation
- logarithmic → ~20 operations
- linear → 1,000,000 operations
```

There are also linearithmic time, quadratic time and exponential time (look them up on your own lol).

#### Array vs. Dictionary vs. Object
Godot stores all variables in the Variant class. These can store data structures such as Array and Dictionary as well as Objects.

##### Array
Godot implements Array as a `Vector<Variant>` (Do not switch it up with Vectors in godot, this Vector is a c++ specific term). The contents are then stored in memory adjacent to each other. This is different than for dictionaries, as arrays do not use hashing, no key-value paires and no slots.

Contiguous memory stores imply the following operation performance:
- **Iterate**: Fastest, great for loops
- **Insert, Erase, Move**: Position-dependant, generally slow.
- **Get, Set**: Fastest by position. But can not specify which record you want, which means if you know its position it can instantly grab its content, but it can not search for the content itself.
- **Find**: Slowest, Identifies the index/position of a value. This means it must iterate through the array and compare values until it finds a match.

##### Dictionaries
Godot implements Dictionaries as a `HashMap<Variant, Variant, VariantHasher, StringLikeVariantComparator>`. 

A Dictionary is a lookup table that trades memory for speed. You give it a key, it hashes that key into a number, and uses that number as an index to jump straight to the matching value in an internal array - no searching required. This works because hashing is deterministic: the same key always produces the same number, so it always lands on the same slot. Its like knowing which exactly which locker your stuff is in versus checking every locker in the hallway.

The array starts with 8 slots and doubles (16,32,64 etc) whenever it gets too full. This generous sizing matters because of how the spread works: the hash produces a big number, then the engine takes that number modulo the array size to get a slot index. Good hash functions make even slightly different inputs (like "hp" vs "hp2") produce wildly different numbers, so keys naturally scatter across the table rather than clumping.

So how is the slot index calculated? Say your array has 8 slots (indices 0-7) and you insert three keys.
"health": 4529 % 8 = 1 (slot 1)
"mana": 7214 % 8 = 6 (slot 6)
"armor": 3600 % 8 = 0 (slot 0)
Modulo just <mark>divides by the array size</mark> and takes the remainder, which guarantees the result always falls within the valid slot range (0-7). No matter how enormous the hash number is, the remainder can never exceed the array size minus one.
And if the array doubles to 16 slots, the engine rehashes everything - same keys, same hash numbers. But now it is 16 instead of 8, so they land on different slots. That is the "rebuilding" that happens on resize.

If two keys do land on the same slot (a collision), the engine uses the "robin hood strategy" to decide how to rearrange entries. It compares how far each entry is from its ideal (first slot it calculated) slot position. It tries to be "fair" by evening out the distance to its ideal position, for every entry. That means that filled slots can be taken by new entries and old entries need to move. Example:
Array of 8 slots. We have armor (3), gold (4) and mana (3). Armor gets his slot. Then gold arrives and takes its slot. Finally mana arrives, but his slot is taken. It could take slot 4, but gold is already occupying that slot. What about 5? It could take that slot, but the distance would be 2 to its ideal slot (3 -> 5). If that happens, robin hood decides to give gold slot slot 4, and bumbs gold also one slot higher (from 4 to 5).
We now have armor (3), mana (4 (3+1)) gold (5 (4+1)). Now the distance is evened out.

There is no performance reason to do this. It is about "when to give up". When using linear probing aka a linear strategy to find the next available spot, it would check every adjacent slot until a free one is found. With robin hood, because of the even distances, when probing at distance 5 and we encounter an entry that is only 1 distance away from its ideal, your key can not possibly be further, because robin hood would have swapped it earlier if it existed. That way, a continuation of the search is not needed. Also it helps that the table gets increased by powers of 2 when the table is filled 80%ish, that way hash collision chances are reduced too.

An overview of their operational details is as follows:
- **Iterate**: Fast.
- **Insert, Erase, Move**: Fastest.
- **Get, Set**: Fastest, same as Insert, erase, move.
- **Find**: Slowest, Identifies the key of a value.

When to use what?
If you're working with ordered, sequential data that you loop through or access by position (like a list of enemies, a queue of events, inventory slots), use an Array. If you need to look things up by name or ID (like stats, settings, item databases), use a Dictionary. Pick the one that matches how you're accessing the data, not which one sounds faster in general.
Regarding the slowest operation performance in Find, both engines need workarounds to deliver a performant result. Arrays can use binary search for example, where 10000 entries with its 10000 checks get cut down to about 13 checks. Dictionaries are instant when you lookup the key, but if you need values which you can not lookup for, you can define two dictionaries which are kept in sync but map each others entries:
(dict A: Tomato->Red | dict B: Red -> Tomato)

