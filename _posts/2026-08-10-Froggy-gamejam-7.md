---
layout: default
title: "Froggy gamejam 7"
---

## Recap

The summer frog jam deadline approaches and I am not at the status I want to be. Now the questions for the future are, did I do too little or do I need longer gamejams as I do stuff regularly but not enough to finish a game it seems. Or I focus at the wrong things, 

The menu took me like 2 days because I used the second day to refine it, and one day was almost entirely invested into getting the pipeline (git to itch) running.

Now the deadline is on August 13th, this thursday at 7 pm. I would like to upload the finished and tested game one day before that. That means I have today, tomorrow and the day after tomorrow to finish things up.

As I stated yesterday, these are the next essential steps:

- The first level with its mechanics
	- The Timer
	- The cost mechanic (for jumps) and or disappearing tiles
	- Enemies
- The scoreboard (I dont know if I have to scrap this feature...)

## Water shader

I added a water shader because the still blue image in the background was irritating to me. I used this as a reference.
[https://godotshaders.com/shader/pond-water-shader-2d-top-down/](https://godotshaders.com/shader/pond-water-shader-2d-top-down/)

![](/assets/blog/2026-08-10-Froggy-gamejam-7/godot.windows.opt.tools.64_ls4Zfx81y5.gif)

## Pixel font issues

Also, I added a custom pixel font because it fits the game. But it was blurry when the game was running. Of course the first thing one would check if the rendering is set to "nearest" which is the best setting for 2D pixel art games. Unfortunately that did not fix the setting.

![](/assets/blog/2026-08-10-Froggy-gamejam-7/Pasted image 20260810211453.png)

The culprit was the setting in the pixelfont.ttf itself, which overrides the global setting. After anti aliasing was disabled and the font reimported the issue fixed itself.

![](/assets/blog/2026-08-10-Froggy-gamejam-7/Pasted image 20260810211958.png)

There is another issue, when the game runs on a smaller screen than the expected 1920x1080, but this is a gamejam and it is not gamebreaking so I will ignore this for now.

## Jumping mechanic

Before, the player needed to press WASD and JUMP all the time to move. As I implemented a "jump to distant tile"-mechanic I changed that feature. As jumping is the frogs normal walk, normal movement is done with WASD, and "real" jumping with WASD and JUMP.

![](/assets/blog/2026-08-10-Froggy-gamejam-7/godot.windows.opt.tools.64_nVAWXcYyYQ.gif)

## Flag mechanic

Added a flag, this is the creator:
[https://ankousse26.itch.io/free-flag-with-animation](https://ankousse26.itch.io/free-flag-with-animation)

In code, I added a gamemanager autoload that receives a signal when the frog has reached its target. It looks like godot 4 needs a callable parameter count to match what the signal emits and just drops a debugger error if it does not.

Wrong code:
```gdscript
func _flag_reached():
	Gamemanager.load_next_level()
```
![](/assets/blog/2026-08-10-Froggy-gamejam-7/Pasted image 20260810221422.png)

Correct code:
```gdscript
func _flag_reached(_body: Node2D) -> void:
	Gamemanager.load_next_level()
```

## Todos

- Check how scoreboards work.
- Menu needs to be opened when I press escape in the game itself
- Add keybind mapping?
- Add small shadow below frog? Which gets smaller when he jumps?
- Make the first level. If its not fun, trash the idea.
- add starting island mechanic
- add jump for bigger distances, add cost for that
- add spider
- add butterfly
- add nono sound when jump is not possible
- Disappearing tiles mechanic?
- change jumping sfx, or add a couple and decide on the best ones
- follower camera or fixed? zoom out but can only move when zoomed in?
- Smooth camera transition?
- fix loop for background music - mp3 to ogg
- add tutorial level
