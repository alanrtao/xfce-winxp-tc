# OpenSUSE XFCE XP Look

The following steps detail how to start from a box standard OpenSUSE (Tumbleweed) image with Mate desktop installed, and get to at least a look-alike of box standard XP. The upstream repo supports way more than what's outlined below run (`find . -name "CMakeLists.txt"` to list all features)

- Install build prereqs as listed [here](./packaging/README.MD#tldr-on-building), as well as `sassc`, `xcursorgen`, `rpm-build`, `python3-virtualenv`
- `export BUILD_DIR='xptc'`
- `mkdir -p $BUILD_DIR && ./packaging/buildall.sh -c basic.txt -o $BUILD_DIR` (you can swap out xptc for any directory name, this saves your build outputs there)
  > Make sure `basic.txt` is terminated with a new line, or else the last entry won't be read...
- `sudo rpm -i $BUILD_DIR/*` if you just want one time install
  - If you built again and want to replace, use `sudo rpm -Uvh --replacepkgs $BUILD_DIR/*`

  > For dev, do `gsettings set org.gtk.Settings.Debug enable-inspector-keybinding true` and then ctrl + shift + I to vieww

- The installation should only add themes without actually switching them on. Use the following to actually use them:
  > https://github.com/rozniak/xfce-winxp-tc/wiki/Manual-configuration-following-install

  - For the task bar, instead of using this project's implementation [here](./shell/taskband/), just use [a texture reskin](./hack/) instead in the panel setting and start menu settings. Do set the task bar height to 26px (28px - 1px on each end for the item border)

- While regular GTK and XFWM themes have been installed, "certain other" applications may still not be adopting them
  - Firefox: open Firefox, on the top area right click and "customize toolbar", on the bottom left of the page there should be an option to turn on the title bar (and also a separate menu bar)
    - [this theme](https://addons.mozilla.org/en-US/firefox/addon/xp-classic-theme/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search) looks pretty nice in combination with the default bar
  
  - Neofetch (why of course, the most important application of them all)
    - `alias neofetch='/usr/bin/neofetch --ascii_distro windows'

  - Terminal (ref: https://www.allidylls.com/poetry/o/spectra.html)
    - Background: 象牙 HEX: #FFFBF0
    - ANSI replacements:
      1. 乌黑 HEX: #392F41
      2. 赫赤 HEX: #C91F37
      3. 松绿 HEX: #057748
      4. 昏黄 HEX: #C89B40
      5. 靛蓝 HEX: #065279
      6. 黛螺 HEX: #4A4266
      7. 蓝色 HEX: #44CEF6
      8. 花白 HEX: #C2CCD0
      9. 墨色 HEX: #50616D
      10. 嫣红 HEX: #EF7A82
      11. 柏绿 HEX: #21A675
      12. 鹅黄 HEX: #FFF143
      13. 靛青 HEX: #177CB0
      14. 丁香 HEX: #CCA4E3
      15. 蔚蓝 HEX: #70F3FF
      16. 雪白 HEX: #F0FCFF
    
  - VSCode:
    ```json
    {
      "window.titleBarStyle": "native",
      "editor.fontFamily": "'PT Mono', 'Droid Sans Mono', 'monospace', monospace",
      "workbench.colorCustomizations": {
          "terminal.foreground": "#392F41",
          "terminal.background": "#FFFBF0",
          "terminal.ansiBlack": "#392F41",
          "terminal.ansiRed": "#C91F37",
          "terminal.ansiGreen": "#057748",
          "terminal.ansiYellow": "#C89B40",
          "terminal.ansiBlue": "#065279",
          "terminal.ansiPurple": "#4A4266",
          "terminal.ansiCyan": "#44CEF6",
          "terminal.ansiWhite": "#C2CCD0",
          "terminal.ansiBrightBlack": "#50616D",
          "terminal.ansiBrightRed": "#EF7A82",
          "terminal.ansiBrightGreen": "#21A675",
          "terminal.ansiBrightYellow": "#FFF143",
          "terminal.ansiBrightBlue": "#177CB0",
          "terminal.ansiBrightPurple": "#CCA4E3",
          "terminal.ansiBrightCyan": "#70F3FF",
          "terminal.ansiBrightWhite": "#F0FCFF",
      }
    }
    ```

- Other stuff:
  - Desktop & Panel shortcuts:
    - In "preferred applications", change system/file manager to thunar, and in Mate Tweaks add the "home" and "trash" desktop icons
    - VSCode (icon under `luna/blue/apps/preferences-desktop-keyboard.png`)
    - Mail (icon under `luna/blue/apps/thunderbird.png`): `firefox --new-tab "<link to your email>"`
    - Discord (icon under `luna/blue/actions/windows-messenger.png`)
    - Mate terminal & Mate System Monitor

  - Set Super + Shift + S to `xfce4-screenshooter -r -c` (select region and save to clipboard)

> BELOW IS THE ORIGINAL README

# xfce-winxp-tc
This is my little chipping-away spot for a Windows XP Total Conversion for XFCE.

![luna-blue-promo](https://github.com/user-attachments/assets/53ce3a26-9d51-47f5-9c6e-8104b654b019)
![luna-metallic-promo](https://github.com/user-attachments/assets/a113ca1b-4047-4519-95dc-3d1feb479426)
![professional-promo](https://github.com/user-attachments/assets/33c063ea-9456-42d0-b969-c131d1b72d96)
![classic-promo](https://github.com/user-attachments/assets/09cb558e-900e-4dd1-b1c0-994680969504)

## What?
Essentially this repo is a 'project' to replicate the XP experience on XFCE / Linux in general. This includes everything from desktop themes, icons, cursors, all the way to programs and the shell itself.

**Please be aware of the following:**
- This project is **NOT** for installing on your parents/grandparents/whoever's computer to 'ease them into Linux' or something, I share this project for the interest of Windows/Linux enthusiasts
- There is no attempt to pretend the system is not Linux - consider this as 'Windows XP on the Linux kernel' (ie. you cannot expect there to be a `C:` drive under *My Computer*)
- Everything is massively under construction, and I am one person, so please don't whinge to me about how x/y/z doesn't look 100% like Windows XP, or that I haven't made program a/b/c

## Why?
I used to use Luna theme ports on Windows 7, which has now lost support, and customisability is non-existent/blown away by WU on Windows 10 - switching to Linux seemed like the best choice.

There are themes that aim to replicate the Windows XP visual styles already, however as anyone who has tried this stuff knows, themes are either lacking or only go so far. This project differs in that I aim for as close to pixel-perfect as possible, and write programs to recreate the complete Windows XP environment (themes alone cannot reproduce the Start menu in the screenshots above).

## Building / Installation
Please see the *Installation* section of the Wiki here: https://github.com/rozniak/xfce-winxp-tc/wiki/Installation 😁

## The theme(s) are buggy!
Themes in GTK3 are not supported by upstream and this project is still under development, so they can potentially look broken in certain programs. If you're using themes from this repository and programs look broken, you should file issues here rather than pestering the developers of said program.

I hope to cover theming for standard GTK widgets across the board, but there will always be potential bugs with subclassed widgets and the like - they'll have to be handled on a case-by-case basis.

The theme is now based directly from Adwaita to hopefully maximise compatibility and make it easier to fix theme bugs. A refactored form of Adwaita from the upstream GTK 3 sources exists in this repo to make it easier to base themes from/fix problems.

## Licence
The source code in this repository, essentially any *text* files, such as SASS, C, Bash script source code, are licensed under GPL 2.0.

This licence obviously does not cover the assets from Windows/Office (images, sounds, fonts etc.) - those are still Microsoft's copyright (packaging will mark components using these as `non-free`). They're in this repo because I am lazy. 😛

## Roadmap?
I don't have a fancy looking roadmap document for this repo - there's too much to list really. Essentially, if something was in Windows XP, it's on my mind.

As part of that, user-friendliness is always a target - besides themes and programs, I aim to one day have a nice setup application/process akin to XP's. And perhaps an OOBE if I can figure that out (mostly for the nostalgic music).

If you're interested in the current completion state of the project, see this Wiki page: https://github.com/rozniak/xfce-winxp-tc/wiki/Project-progress-and-status
