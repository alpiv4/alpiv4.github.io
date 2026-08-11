---
layout: default
title: "Froggy gamejam 8"
---

## Gamemanager

I want to finish the level switch and the first 3 levels today. For this, I created a gamemanager (autoload script) that manages which scenes are loaded.

At first I tried to check what scene is loaded in the current scene tree and compare it to existing level scenes I have. In the end the gamemanager itself started tracking the current level index and just counts up when a level is loaded. As the menu is level 0 and the rest of the levels just 1,2,3 loading them is pretty basic but functional.

## Grid math impacted by scaling

Also for the future, as I had issues when the menu was 1920x1080 and the levels 640x320 I needed to scale up the levels. But then the grid calculation did not work any more. Thats because we use `local_to_map` when calculating the frogs position. For this to understand one has to understand two things:
`global position` = This is the position measured from the worlds absolute origin `0,0`.
`local position` = This is the position relative to its parent node, measured from its parent origin.
If nothing is scaled, these two are the same, therefore no issues arise. But if scaling is used, this does not work anymore as `local_to_map` needs a position relative to the tile grid itself, not global space. But the code I used was using global positioning. By converting the frogs position into a position relative tot he tile grid first, the grid math worked again.

before:
```gdscript
var own_cell = fences.local_to_map(self.global_position)
```

after:
```gdscript
var own_cell = fences.local_to_map(fences.to_local(self.global_position))
```

## Current look

So we now have the first tutorial level with its base mechanic. A menu scene and switching up between levels. An options menu that can be opened any time and where sound can be changed. The game can be closed (except on browser builds).

![](/assets/blog/2026-08-11-Froggy-gamejam-8/godot.windows.opt.tools.64_eGhOx7jW0r.gif)

## Next steps

Doing for tomorrow (the final day for my own deadline) is to create the timer and a visual cost indicator for jumps. I wanted to have enemies that can be consumed to give the frog the power to jump. I guess I will do that in the second level.

Also, I think I invested to little time into the actual level mechanics and more into surrounding mechanics and perfecting the game feel. There is not much time left and I do not now if that is even enough time to think of puzzle level ideas and to create them. Especially when these levels need new mechanics like enemies or specific fields that allow different movement or unlock paths (randomized minigame when trying to solve a shortcut? Another idea, but think of among us?).

I just thought of that, but the player should be able to save its progress? Not manually, but maybe I need some kind of "maximum points" counter that is saved?

But that is something for tomorrow. At least I am having fun, and that is the important part.

## prio 1 todos

- ~~open menu when pressing escape during the game, pausing the game too~~
- The first level with its mechanics
	- The Timer
	- The cost mechanic (for jumps) and or disappearing tiles
	- Enemies
- The scoreboard (I dont know if I have to scrap this feature...)
- add looping music or playlist that loops
- add frog sound when flag is reached

## prio 2 todos

- maximum points counter? like a save?
- edit walkable sprite so that is more visible for debugging
- edit the font for 5 in FontForge? it looks like another symbol...
- Check how scoreboards work.
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
