# Pegasus Frontend Tutorial
A description for how to get Pegasus-Frontend working with Steam, Retroarch, Epic Games, GOG, and other executable games when on either Aurora (a version of Fedora) or Windows.

The explanation for Aurora is likely extremely applicable to other distributions, Aurora is just what I personally use and can verify that as of writing this these steps work on. I do not use Windows myself, so that section I am less sure about.

I made this simply because I was frustrated by the lack of easy to use information for Fedora-based distrubutions, as I myself am very much an end-user and I can struggle sometimes to follow more vague documentation. I thought I would share my experience as this setup works amazingly, and I thought maybe someone else would appreciate this explanation. If you find something wrong with it, feel free to open an Issue - I won't necessarily fix it, but it could help other future users.

Aurora Linux
======

## 1. Organizing your File System
To get Pegasus working in conjunction with Skyscraper, we need our file system to be organized in a certain way.

1. To start, we need a place for our ROMS. The specific location does not matter, but in this tutorial, Ill just assume you’re using `$HOME/Games`
2. Create a separate folder for each console you emulate. 
   1. Skyscraper, the metadata scraper, supports the following consoles. If you are, for example, emulating a DS, name the folder "nds" - keep it exactly the same as the names listed here: '3do', '3ds', 'amiga', 'amigacd32', 'amstradcpc', 'apple2', 'arcade', 'arcadia', 'astrocde', 'atari800', 'atari2600', 'atari5200', 'atari7800', 'atarijaguar','atarijaguarcd', 'atarilynx', 'atarist','atomiswave', 'c16', 'c64', 'c128', 'channelf','coco', 'coleco', 'daphne', 'dragon32','dreamcast', 'easyrpg', 'fba', 'fds','gameandwatch', 'gamegear', 'gb', 'gba', 'gbc','gc', 'genesis', 'intellivision', 'mame-advmame','mame-libretro', 'mame-mame4all', 'mastersystem','megacd', 'megadrive', 'moto', 'msx', 'msx2','n64', 'naomi', 'nds', 'neogeo', 'neogeocd','nes', 'ngp', 'ngpc', 'openbor', 'oric', 'pc','pc88', 'pc98', 'pcfx', 'pcengine', 'pcenginecd','pico8', 'pokemini', 'ports', 'ps2', 'psp','psx', 'saturn', 'scummvm', 'sega32x', 'segacd','sg-1000', 'snes', 'steam', 'switch', 'ti99','trs-80', 'vectrex', 'vic20', 'videopac','virtualboy', 'wii', 'wiiu', 'wonderswan','wonderswancolor', 'x68000', 'x1', 'zmachine','zx81', 'zxspectrum'
2. The above list is most likely outdated. Always check the `Skyscraper --help` output to get a up-to-date list of supported consoles/systems. The list of consoles and systems is not limited to that and can be [extended or renamed to your liking](https://gemba.github.io/skyscraper/PLATFORMS/#how-to-add-platforms-for-scraping).
3. Inside these folders, place the relevant ROMs. For example, a GBA ROM goes in the “gba” folder.

## 2. Setting up Pegasus
Pegasus cannot run games itself (it will connect with Steam, Retroarch, etc. for that), nor can it get data on games (we use Skyscraper for that). All it does is look pretty, and connect to other software. 

1. Download from [Flathub](https://flathub.org/apps/org.pegasus_frontend.Pegasus)
2. You can skip the rest of this section if you want, but the default theme is kinda lame in my opinion at least. Luckily, we can change it! Ive tried all the big ones, I recommend one called BartopOS
   1. Go [here](https://pegasus-frontend.org/tools/themes/), click on "bartopOS" (should be the second theme) and click download
   2. Extract the archive
   3. Move the resulting folder to `$HOME/.var/app/org.pegasus_frontend.Pegasus/config/pegasus-frontend/themes`
      1. You will likely need to make a themes folder. 
   4. Close and reopen Pegasus. Click Esc, or the menu key on an xbox controller, click Settings. Then, click Theme, and change it to bartopOS
   5. While here, I recommend maybe changing fullscreen mode off if you want to
   6. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. Youll probably see games already, from steam. Hopefully at least
3. At the top right of the screen is a cog wheel – thats the BartopOS settings. Go there
   1. Maybe try enabling “Allow video thumbnails” in the General section. Very cool, but I found it to be laggy. Worth trying out anyway. 
   2. Enable “Animate highlight” in the General section if it isn’t already
   3. Enable “Full details view” in the Game Details section if it isn’t already

## 3. Setting up Skyscraper
Pegasus has no information about what ROMs are – that information is provided by a scraper. For that, we will be using Skyscraper

1. Skyscraper has [dependencies](https://github.com/Gemba/Skyscraper/#-how-to-install-skyscraper) (basically Qt6, make, g++, git and python3) that I found personally hard to install on Fedora. As such, I recommend running it through Distrobox.
   1. Distrobox comes by default on Aurora Kionite, but if you are running, for example, base Fedora, a simple `sudo dnf install distrobox` in your terminal should work.
   2. To make distrobox easier to use, we will also be using BoxBuddy – a GUI for it. I recommend downloading it from [Flathub](https://flathub.org/apps/io.github.dvlv.boxbuddyrs)
   3. Open Boxbuddy, click the + at the top left, fill in the name as being “Debian,” and select “debian – quay.io/toolbx-images/debian-toolbox:latest” as your Image. Then, click Create, and let it do its thing.
   4. When its done, there should be an open terminal window. If not, click on “Open Terminal” inside Boxbuddy. Do all commands in this section inside this terminal window, if you are using Distrobox. 
2. In your terminal, run `sudo apt install qt6-base-dev qmake6 qt6-base-dev-tools libqt6sql6-sqlite p7zip-full python3`
3. In your terminal, run the following commands to build and install Skyscraper
   1. `mkdir skysource`
   2. `cd skysource`
   3. `wget -q -O - https://raw.githubusercontent.com/gemba/skyscraper/master/update_skyscraper.sh | bash -s --`
4. Go to `$HOME/.skyscraper`. If you can’t find this folder, enble “Show Hidden Files”. In Dolphin, you can do this by pressing Ctrl+H
   1. Delete `config.ini` and `artwork.xml`
   2. Replace it with the `config.ini` and `artwork.xml` files from this github. You can adjust a variety of things, if you want to change the input folder from `$HOME/Games` to something else, do it in the `config.ini`.
5. Do this once: Review the `config.ini`, notice the sections `[<console>]` and the launch command option `launch=`. Copy this section for each console you want to create pegasus output for. Then adjust the value to `flatpak run org.libretro.RetroArch -L "/home/<YOURUSER>/.var/app/org.libretro.RetroArch/config/retroarch/cores/mgba_libretro.so" {file.path}` per each console. You will need different RetroArch core emulators (the `*.so` file) for each console. That way you can save you the tedious manual editing noted a few steps below, as Skyscraper will fill in that information to the pegasus output.
5. Each console folder you have in `$HOME/Games` will need you to run two commands for them. For this example, we will assume you are doing it for the DS (nds). Every console is exactly the same, but replace “nds” with the name of the folder you made earlier for each console.
   1. Close Pegasus if its open. 
   2. `Skyscraper -s screenscraper -p nds`
   3. Wait until it says its done
   4. `Skyscraper -p nds`
6. Go to `$HOME/Games/nds` and check if theres a couple new files and a `media/` subfolder. If so, it worked!
7. You can skip the next step if you entered the launch information in the `config.ini` on each console's `launch=` option (see `config.ini` for an example)
7. Only if you did not confgured Skyscraper to do this: While here, inside the folder named after the console open `metadata.pegasus.txt` (or whatever you have set in the `config.ini` as `gameListFilename=`) in Notepad.
   1. Delete `command: /opt/retropie/supplementary/runcommand/runcommand.sh 0 _SYS_ snes "{file.path}"` near the top
   2. Replace it with `launch: flatpak run org.libretro.RetroArch -L "/home/<YOURUSER>/.var/app/org.libretro.RetroArch/config/retroarch/cores/mgba_libretro.so" {file.path}`
      1. (replace the `mgba_libretro.so` with whatever retroarch core you want to use for the given console)
      2. Where it says `“{file.path}”`, that isnt me asking you to fill in a file path – literally just leave it as `“{file.path}”` as placeholder for Pegasus

## 4. Finishing Touches
Now we just need to update Pegasus super fast, so it can see your games and their assets that you now obtained through Skyscraper

1. Open Pegasus
2. Click Esc, or the menu key on an xbox controller, click Settings.
3. Scroll down and click “Set game directories…”
4. Click the plus
5. Navigate to `$HOME/Games/[CONSOLE NAME HERE]` and click on the `metadata.pegasus.txt` file
6. Click off to the side
7. It should ask if you want to reload – click OK
8. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. You should see all your games from the console you selected, with awesome artwork and shit!
9. Repeat steps 2-8 for each console folder you have

Windows
======

## 1. Organizing your File System
To get Pegasus working, as well as Skyscraper (we'll get to that later), we need our file system to be organized in a certain way.

1. To start, we need a place for our ROMS. The specific location does not matter, but in this tutorial, Ill just assume you’re using `C\Users\<YOURUSER>\Games`
2. See note in the Linux part for supported consoles/systems and respective foldernames of Skyscraper.
3. Inside these folders, place the relevant ROMs. For example, a GBA ROM goes in the “gba” folder.

## 2. Setting up Pegasus
Pegasus cannot run games itself (it will connect with Steam, Retroarch, etc. for that), nor can it get data on games (we use Skyscraper for that). All it does is look pretty, and connect to other software. All the screenshots I sent are of Pegasus.

1. Download from [here](https://pegasus-frontend.org/#downloads)
2. Should be a simple open and it works, but the default theme is kinda lame in my opinion at least. Luckily, we can change it! Ive tried all the big ones, I recommend one called BartopOS
   1. Go [here](https://pegasus-frontend.org/tools/themes/), click on "bartopOS" (should be the second theme) and click download
   2. extract the archive
   3. move the resulting folder to `C:\Users\[username]\AppData\Local\pegasus-frontend\themes\`
   4. close and reopen Pegasus. Click Esc, or the menu key on an xbox controller, click Settings. Then, click Theme, and change it to bartopOS
   5. While here, I recommend maybe changing fullscreen mode off if you want to
   6. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. Youll probably see games already, from steam. Hopefully at least
3. At the top right of the screen is a cog wheel – thats the BartopOS settings. Go there
   1. Maybe try enabling “Allow video thumbnails” in the General section. Very cool, but I found it to be laggy. Could be a linux problem, who knows. Worth trying out. 
   2. Enable “Animate highlight” in the General section if it isn’t already
   3. Enable “Full details view” in the Game Details section if it isn’t already
4. BartopOS says it needs Windows users, if they want to have videos for their games, to download a “K-lite Codec Pack” from here. It works without this on Linux so I havent done it… no idea how to do it, good luck.

## 3. Setting up Skyscraper
Pegasus has no information about what ROMs are – that information is provided by a scraper. I use skyscraper, which has only unofficial windows support. If it doesn’t work, try [Skraper.net](https://www.skraper.net/), but I havent used it so you’re on your own when it comes to making it work.

1. Go down at the [README](https://github.com/Gemba/skyscraper/blob/master/win32/README.md) and follow the instructions. Continue after you have a running Skyscraper instance.
2. Go to  `C:\Users\<YOURUSER>\.skyscraper`
   1. Delete `config.ini` and `artwork.xml`
   2. Replace it with the `config.ini` and `artwork.xml` files from this github. You may have to adjust the `inputFolder` to the respective folder with games, without the console/system name, e.g. `"C:\Users\<YOURUSER>\Games` but not `"C:\Users\<YOURUSER>\Games\nds"`
6. Run `Skyscraper.exe` from a command prompt (see README of Skyscraper).
7. Each console folder you have in `C\Users\<YOURUSER>\Games` will need you to run two commands for them. For this example, we will assume you are doing it for the DS (nds). Every console is exactly the same, but replace “nds” with the name of the folder you made earlier for each console.
   1. Close Pegasus if its open. 
   2. `path\to\Skyscraper.exe -s screenscraper -p nds`
   3. Wait until it says its done
   4. `path\to\Skyscraper.exe -p nds`
8. Go to `C:\Users\<YOURUSER>\Games\nds` and check if theres a couple new files and a `media` folder. If so, it worked!
9. While here, inside the folder named after the console open “metadata.pegasus.txt” in Notepad. **Note**: See Linux install for an alternative to this.
   1. Delete `command: /opt/retropie/supplementary/runcommand/runcommand.sh 0 _SYS_ snes "{file.path}"` near the top
   2. Replace it with `launch: C:\RetroArch\retroarch.exe  -L C\RetroArch\cores\bsnes2014_accuracy_libretro.so  {file.path}`
      1. (replace the bsnes2014_accuracy_libretro.so with whatever retroarch core you want to use for the given console)
      2. Where it says `“{file.path}”`, that isnt me asking you to fill in a file path – literally just leave it as `“{file.path}”`

## 4. Finishing Touches
Now we just need to update Pegasus super fast, so it can see your games and their assets that you now obtained through Skyscraper

1. Open Pegasus
2. Click Esc, or the menu key on an xbox controller, click Settings.
3. Scroll down and click “Set game directories…”
4. Click the plus
5. Navigate to `C\Users\<YOURUSER>\Games\[CONSOLE NAME HERE]` and click on the “metadata.pegasus.txt” file
6. Click off to the side
7. It should ask if you want to reload – click OK
8. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. You should see all your games from the console you selected, with awesome artwork and shit!
9. Repeat steps 2-8 for each console folder you have
