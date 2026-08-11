---
layout: default
title: "Design patterns"
---

Signals - Observer pattern
Nodes their tree like relationships favor composition over inheritance
Singletons - auto-loaded nodes
Command pattern - turn a function call into an object and pass it around
flyweight pattern - resources in godot
Entity component pattern

### Optimization patterns

data locality
spacial partitioning
object pooling

### Architectural patterns

Entity-component system (ECS)
	1. favoring composition over inheritance gives you a lot of flexibility in the way you design entities
	2. related components are generally grouped in memory and arranged in a CPU-friendly way, offering better performance.
	This does not affect rendering performance. If the bottleneck is the number of polygons, textures and shaders a ECS wont benefit you.
	The other benefit, flexibility, means using ECS in godot replaces godots node system with a different architecture. Godot already favors composition. To replace that with ECS, you would replace godots node system and create a parallel one.


### When or not to use patterns

more flexibility or performance at the cost of complexity and extra maintenance work. They add extra code and abstractions

Always go with the simplest code possible. A chest that only has an open and closed state, a boolean is enough. A menu with sub menus an array will suffice. Both can be handled with FSMs, but the previous mentioned methods are more simple and work too.

When to use a FSM:
1. Have more than three or four different states for a given object
2. Update, add or remove behaviors many times as you create the game



