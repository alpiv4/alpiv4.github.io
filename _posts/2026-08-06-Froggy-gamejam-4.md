---
layout: default
title: "Froggy gamejam 4"
---

Have not done anything since the last post. We have a week left until the gamejam deadline, so let's push through. Also, something personal, I was not in the mood to start, but being angry and disappointed in procrastinating and myself pushed me?

Today were gonna fix a visual bug, on the first jump, no animation is played. I guess the order of the execution is wrong or there is some autostart setting just like with timers...

Also, we want to tackle at least one other step of my list. Also this list will grow, as I do not like to manage an additional google worksheet, thats just overkill for such a small project AND there is no collaboration. I am tracking everything in these notes, that should suffice, as I always take notes for the blog.

## Visual bug
It really just was the "autoplay on load" button in the AnimatedSprite2D node.

Buggy:
![](/assets/blog/2026-08-06-Froggy-gamejam-4/godot.windows.opt.tools.64_VU7CU8j3Rs.gif)

Fixed:
![](/assets/blog/2026-08-06-Froggy-gamejam-4/godot.windows.opt.tools.64_DAIuYSgwIQ.gif)

Setting to change:
![](/assets/blog/2026-08-06-Froggy-gamejam-4/Pasted image 20260806135301.png)

At least that is one fix. The other would be to do it properly and run the "idle" animation in the ready function. As this is proper, I decided to do that.

## Jump direction indicator
Sketched up an arrow indicator in aseprite and used a white border like the frog has. Additionaly, used the colorpalette of the frog for the arrow itself.
Nice thing is, if changes are needed just re-export the spritesheet into the godot folder with the same name and the changes are automatically added in the editor.

We now have a simple 2 frame animation. Which we assign to its own animatedsprite2d node and rotate it based on the direction value.

![](/assets/blog/2026-08-06-Froggy-gamejam-4/godot.windows.opt.tools.64_vDIbADC20F.gif)

I also thought about changing up the arrow indicator if a jump is not possible. It could disappear, or turn red or grey? Or blue, which then indicates that it is possible to jump further distances, which shortens the timerange people need for levels, which is the main goal of this game. To solve simple puzzles and to have a time record.

## Music and SFX
SFX for jumping
[https://pixabay.com/sound-effects/film-special-effects-jump-sound-531048/](https://pixabay.com/sound-effects/film-special-effects-jump-sound-531048/)
Menu theme
[https://pixabay.com/de/music/videospiele-game-music-puzzle-strategy-arcade-technology-301226/](https://pixabay.com/de/music/videospiele-game-music-puzzle-strategy-arcade-technology-301226/)
Background theme 1
[https://pixabay.com/de/music/hinterh%C3%A4ltig-kids-517854/](https://pixabay.com/de/music/hinterh%C3%A4ltig-kids-517854/)
Background theme 2
[https://pixabay.com/de/music/karikaturen-funny-kids-525160/](https://pixabay.com/de/music/karikaturen-funny-kids-525160/)

As for the repeating jumping sound, it is quite easy to make it easier for the eyes to just adjust the pitch with randf_range. But I will replace it in the future I guess.

## Final thoughts
As usual I procrastinated in starting the work, so I convinced myself to only do a couple of minutes and add a small feature on my list.
In the end I finished 5 tasks and invested like two hours. Interesting.

## Todos
- Add small shadow below frog? Which gets smaller when he jumps?
- Make the first level. If its not fun, trash the idea.
- Do not forget to add credits
- Add menu and keybind mapping?
- ~~Jump only with space~~
- ~~Jump direction indicator~~
- Add Menu
- ~~Fix first jump visual bug~~
- ~~Continuous jumping~~
- add starting island mechanic
- add jump for bigger distances, add cost for that
- add spider
- add butterfly
- add menu art
- ~~add background music~~
- ~~add jumping/damage/"nonono" sound~~
- add nono sound when jump is not possible
- Check how scoreboards work.
- Disappearing tiles mechanic?
- change jumping sfx, or add a couple and decide on the best ones
- follower camera or fixed? zoom out but can only move when zoomed in?
- Smooth camera transition?
- fix loop for background music - mp3 to ogg
- add custom logo for bootup
- add tutorial level
