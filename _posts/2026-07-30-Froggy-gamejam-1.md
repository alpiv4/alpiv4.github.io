---
layout: default
title: "Froggy gamejam 1"
---

Im not sure what to do today. I want to do something, but I have not decided on a small project I want to work on.
I guess as the webtest game on my site is unfinished this is the thing I will focus on.

Bahlgs game I tried yesterday was really fun. It was very simple, but I think the constant "number going up" and "dozens of effects per second" on screen hooked me.

A couple of hours later I was looking for a simple project to do. Vampire survivors clone does not interest me that much, and I need something very simple. Scrolling through itch gamejams I found this cute one:

[https://itch.io/jam/summer-frog-jam-2026](https://itch.io/jam/summer-frog-jam-2026)

![](/assets/blog/2026-07-30-Froggy-gamejam-1/Pasted image 20260730153955.png)

And it starts in 3 hours! Theme is not even out yet, but I want to do something basic and frog related. Look how cute it looks.

So I sketched up some VERY basic mechanics:

![](/assets/blog/2026-07-30-Froggy-gamejam-1/Pasted image 20260730154055.png)

This time I will focus on keeping it as basic as possible.

## Art

I found interesting sprites i want to use
[https://toadgirl.itch.io/mr-and-mrs-dudeS](https://toadgirl.itch.io/mr-and-mrs-dudeS)
![](/assets/blog/2026-07-30-Froggy-gamejam-1/Pasted image 20260730200803.png)

[https://melloinc.itch.io/cursor-frogs-32px](https://melloinc.itch.io/cursor-frogs-32px)
![](/assets/blog/2026-07-30-Froggy-gamejam-1/Pasted image 20260730200822.png)

[https://caz-bee.itch.io/froggy](https://caz-bee.itch.io/froggy)
![](/assets/blog/2026-07-30-Froggy-gamejam-1/froggy.gif)

I wanted to edit them already, because i need a back view when the frog is jumping upwards. BUT, this will not finish the game at all. So I will focus on making the jumping mechanic first.

## Prototype

What do we need:
Grid map, so that we can create a functional jumping system. The frog is only able to jump a specific distance. Movement is chess like. So it needs to be a grid.

![](/assets/blog/2026-07-30-Froggy-gamejam-1/Pasted image 20260730202202.png)

As I drew this two ideas:
- make the game crayon based? Frogs are cute, if the level is crayon made it could fit. I would need specific textures or a filter for that. Which isnt bad, there was a CRT filter i always liked, I want to test out shaders.
- forgot the other idea, SHIT it was not a bad one

Animation imported. Now i need the movement. For that the level needs to be scaled based on the Sprite of the character. As I move from grid to grid, pressing once means moving one cell (or jumping multiple). For that we need a jump distance based on pixels.

As most people use 16:9 displays, I will go with:
**320×180** or **640×360**
All divide evenly into 1080p, 1440p and 4k.

320x180 seems perfect

![](/assets/blog/2026-07-30-Froggy-gamejam-1/Pasted image 20260730202956.png)

So the creator of the frog defined the sprite as 32x32. I guess I will just go with that.
But i scaled down the frog by 50% as the levels would be too small otherwise.
There are other issues now though:

![](/assets/blog/2026-07-30-Froggy-gamejam-1/Pasted image 20260730204224.png)

I guess this will end up being a status bar or something. Also, there will be a skybox? So I should not worry about that for now.

Nice basic movement works!

![](/assets/blog/2026-07-30-Froggy-gamejam-1/godot.windows.opt.tools.64_BqgEb3vKt4.gif)

So as this is not a physics based movement (because i use the grid based system), I stripped myself of the ability to just use the jump animation and to let the jumping be done by the physics.
As I am moving 32 pixels and my jumping animation has 6 frames, i could use 1 frame per 4 seconds. This could imply jumping? Or maybe thats to "strict" movement? Lets try it out.

Tween did the trick.

![](/assets/blog/2026-07-30-Froggy-gamejam-1/godot.windows.opt.tools.64_LLOwJ1GUdD.gif)

Also added tween TRANS_QUAD and EASE_OUT for better feel.

```gdscript
	var tween = create_tween()
	tween.tween_property(self, "position", new_position, MOVE_DURATION).set_trans(Tween.TRANS_QUAD).set_ease(Tween.EASE_OUT)
	tween.finished.connect(_on_move_finished)
```

Then used the [https://pixelfrog-assets.itch.io/tiny-swords](https://pixelfrog-assets.itch.io/tiny-swords) free assetpack to generate some floor tiles.

Final look (for today):

![](/assets/blog/2026-07-30-Froggy-gamejam-1/godot.windows.opt.tools.64_3OQlP4du9c.gif)

Things to add/check:
- Add small shadow below frog? Which gets smaller when he jumps?
- Make the first level. If its not fun, trash the idea.
- Do not forget to add credits
- Add menu and keybind mapping?
- Jump only with space
- Jump direction indicator

I am happy about the progress today. Also, as I just started, I wanted to invest a couple of minutes. I did not track the time, but it was about 2,5 hours. Did NOT feel that way.
