---
layout: default
title: "Froggy gamejam 2"
---

## Gamedev

Todays plan is to check adjacent cells and let the player only move if it is walkable. The goal is to finish the basic game loop, therefore this mechanic has to work.

We start of by using another invisible tilemaplayer and we add a custom data layer to the tilemaplayer node and assign "walkable" to the tiles we use in the scene. This way we can separate the art from the logic.

Also we had scaling issues in all possible areas so I changed back the root nodes scaling to 1 and turned up the resolution to 640x360.

![](/assets/blog/2026-07-31-Froggy-gamejam-2/Pasted image 20260731232903.png)
![](/assets/blog/2026-07-31-Froggy-gamejam-2/Pasted image 20260731233444.png)
![](/assets/blog/2026-07-31-Froggy-gamejam-2/godot.windows.opt.tools.64_1RFndq5ld7.gif)

This was very bothersome to make because the godot tileset editor and its design are somewhat bad.

I wish I could have done more today, this simple mechanic took me more time than expected.

## Technical stuff

Additionally, because I do not want to manually export and upload the game every time to itch, I looked up on how to get the github workflow running. This then generates a web export and pushes it to itch.

For this, you need two config files and an itch api key you need to add to github as a secret. Both files need to be in the root directory of your game. Also, as I manually exported the game in the past, I only needed to add some changes to the 'exports_preset.cfg' file.

To bypass malicious updates to the repos I access I added the checksum of the specific commits.

deploy.yml
```yml
name: Export and Deploy to itch.io
on:
  push:
    branches: [main]
jobs:
  export:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          lfs: true
      - name: Export Web build
        uses: firebelley/godot-export@29965918cc35b77c465839035775e0e12dc87029 # v6.0.0
        with:
          godot_executable_download_url: [https://github.com/godotengine/godot/releases/download/4.7.1-stable/Godot_v4.7.1-stable_linux.x86_64.zip](https://github.com/godotengine/godot/releases/download/4.7.1-stable/Godot_v4.7.1-stable_linux.x86_64.zip)
          godot_export_templates_download_url: [https://github.com/godotengine/godot/releases/download/4.7.1-stable/Godot_v4.7.1-stable_export_templates.tpz](https://github.com/godotengine/godot/releases/download/4.7.1-stable/Godot_v4.7.1-stable_export_templates.tpz)
          relative_project_path: ./
          use_preset_export_path: true
          archive_export_output: false
          export_debug: false
          cache: true
      - name: Debug list export output
        run: |
          echo "== build/web contents =="
          find build/web -maxdepth 3
      - name: Upload to itch.io
        uses: yeslayla/butler-publish-itchio-action@483157ebeeeb440e2fdc9f162f3fcfc27028c0ef # v1.2.0
        env:
          BUTLER_CREDENTIALS: ${{ secrets.BUTLER_API_KEY }}
          CHANNEL: html5
          ITCH_GAME: frogjam
          ITCH_USER: alpiv4
          PACKAGE: build/web/Frogjam(working title)
```

exports_preset.cfg
```yml
[runnable_presets]

Web="Frogjam(working title)"

[preset.0]

name="Frogjam(working title)"
platform="Web"
dedicated_server=false
custom_features=""
export_filter="all_resources"
include_filter=""
exclude_filter=""
export_path="build/web/index.html"
patches=PackedStringArray()
patch_delta_encoding=false
patch_delta_compression_level_zstd=19
patch_delta_min_reduction=0.1
patch_delta_include_filters="*"
patch_delta_exclude_filters=""
encryption_include_filters=""
encryption_exclude_filters=""
seed=0
encrypt_pck=false
encrypt_directory=false
script_export_mode=2

[preset.0.options]

custom_template/debug=""
custom_template/release=""
variant/extensions_support=false
variant/thread_support=false
vram_texture_compression/for_desktop=true
vram_texture_compression/for_mobile=false
html/export_icon=true
html/custom_html_shell=""
html/head_include=""
html/canvas_resize_policy=2
html/focus_canvas_on_start=true
html/experimental_virtual_keyboard=false
progressive_web_app/enabled=false
progressive_web_app/ensure_cross_origin_isolation_headers=true
progressive_web_app/offline_page=""
progressive_web_app/display=1
progressive_web_app/orientation=0
progressive_web_app/icon_144x144=""
progressive_web_app/icon_180x180=""
progressive_web_app/icon_512x512=""
progressive_web_app/background_color=Color(0, 0, 0, 1)
threads/emscripten_pool_size=8
threads/godot_pool_size=4

```
