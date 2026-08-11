---
layout: default
title: "Froggy gamejam 5"
---

I am not sure how to track todos, if I should remove finished ones or not. I think I will keep the list and move finished ones to the bottom.

I am very interested in implementing a scoreboard. So that is todays topic. For this to work I need another server where I can host user data. We keep it as simple as possible, the game needs to work, the scoreboard is just a part of it. Therefore, we will use a godot plugin called Silentwolf (no placement, I found that site by change when I googled a solution).

Also, players need to be able to use nicknames. Therefore, when players start a game, the initial nickname should be a random string, which they can change when posting on the scoreboard.

What is the content of the scoreboard? Basic draft:

![](/assets/blog/2026-08-07-Froggy-gamejam-5/Pasted image 20260807150439.png)

An hour later I changed up some stuff, added a splash screen, added a menu and configured the plugin to test.

![](/assets/blog/2026-08-07-Froggy-gamejam-5/godot.windows.opt.tools.64_MuAJVkVlLQ.gif)

Additionally, just because I wanted to, I added multiple sliders for the volume. I want them to be visible on the starting screen because if the sound is too loud, people should be able to change it asap.
For this, you need to define multiple audio-bus streams and put the audiostream nodes in the corresponding bus. Then, by connecting to the signal of the HSlider every time the slider is dragged a change gets propagated to the volume value.

![](/assets/blog/2026-08-07-Froggy-gamejam-5/Pasted image 20260807191529.png)

Finally, we now can now credit people who made the assets. To make changes easier, I can edit them in a simple txt file which gets read by godot. Also this loops!

![](/assets/blog/2026-08-07-Froggy-gamejam-5/godot.windows.opt.tools.64_1zkk6UcsPQ.gif)

## Todos

- ~~Add Menu~~
- Change frog name art and name in menu?
- ~~add menu art~~
- Add credits
- Check how scoreboards work.
- add custom logo for bootup

- change volume naming from master to main
- add 10 increment steps for volume, and show value
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
- ~~Jump only with space~~
- ~~Jump direction indicator~~
- ~~add background music~~
- ~~add jumping/damage/"nonono" sound~~
- ~~Fix first jump visual bug~~
- ~~Continuous jumping~~
