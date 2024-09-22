# pegasus-frontend-tutorial
A description for how to get Pegasus-Frontend working with Retroarch games when on either Aurora (a version of Fedora), or Windows.

Aurora Linux
======

## 1. Organizing your File System
To get Pegasus working in conjunction with Skyscraper, we need our file system to be organized in a certain way.

1. To start, we need a place for our ROMS. The specific location does not matter, but in this tutorial, Ill just assume you’re using "home/Games"
2. Create a separate folder for each console you emulate. 
   1. Skyscraper, the metadata scraper, supports the following consoles. If you are, for example, emulating a DS, name the folder "nds" - keep it exactly the same as the names listed here: '3do', '3ds', 'amiga', 'amigacd32', 'amstradcpc', 'apple2', 'arcade', 'arcadia', 'astrocde', 'atari800', 'atari2600', 'atari5200', 'atari7800', 'atarijaguar','atarijaguarcd', 'atarilynx', 'atarist','atomiswave', 'c16', 'c64', 'c128', 'channelf','coco', 'coleco', 'daphne', 'dragon32','dreamcast', 'easyrpg', 'fba', 'fds','gameandwatch', 'gamegear', 'gb', 'gba', 'gbc','gc', 'genesis', 'intellivision', 'mame-advmame','mame-libretro', 'mame-mame4all', 'mastersystem','megacd', 'megadrive', 'moto', 'msx', 'msx2','n64', 'naomi', 'nds', 'neogeo', 'neogeocd','nes', 'ngp', 'ngpc', 'openbor', 'oric', 'pc','pc88', 'pc98', 'pcfx', 'pcengine', 'pcenginecd','pico8', 'pokemini', 'ports', 'ps2', 'psp','psx', 'saturn', 'scummvm', 'sega32x', 'segacd','sg-1000', 'snes', 'steam', 'switch', 'ti99','trs-80', 'vectrex', 'vic20', 'videopac','virtualboy', 'wii', 'wiiu', 'wonderswan','wonderswancolor', 'x68000', 'x1', 'zmachine','zx81', 'zxspectrum'
3. Inside these folders, place the relevant ROMs. For example, a GBA ROM goes in the “gba” folder.

## 2. Setting up Pegasus
Pegasus cannot run games itself (it will connect with Steam, Retroarch, etc. for that), nor can it get data on games (we use Skyscraper for that). All it does is look pretty, and connect to other software. 

1. Download from [Flathub](https://flathub.org/apps/org.pegasus_frontend.Pegasus)
2. You can skip the rest of this section if you want, but the default theme is kinda lame in my opinion at least. Luckily, we can change it! Ive tried all the big ones, I recommend one called BartopOS
⋅⋅1. Go [here](https://pegasus-frontend.org/tools/themes/), click on "bartopOS" (should be the second theme) and click download
⋅⋅2. Extract the archive
⋅⋅3. Move the resulting folder to "/home/<YOUR-USERNAME>/.var/app/org.pegasus_frontend.Pegasus/config/pegasus-frontend/themes" 
⋅⋅⋅⋅1. You will likely need to make a themes folder. 
⋅⋅4. Close and reopen Pegasus. Click Esc, or the menu key on an xbox controller, click Settings. Then, click Theme, and change it to bartopOS
⋅⋅5. While here, I recommend maybe changing fullscreen mode off if you want to
⋅⋅6. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. Youll probably see games already, from steam. Hopefully at least
3. At the top right of the screen is a cog wheel – thats the BartopOS settings. Go there
⋅⋅1. Maybe try enabling “Allow video thumbnails” in the General section. Very cool, but I found it to be laggy. Worth trying out anyway. 
⋅⋅2. Enable “Animate highlight” in the General section if it isn’t already
⋅⋅3. Enable “Full details view” in the Game Details section if it isn’t already

## 3. Setting up Skyscraper
Pegasus has no information about what ROMs are – that information is provided by a scraper. For that, we will be using Skyscraper

1. Skyscraper has weird dependencies that I found personally hard to install on Fedora. As such, I recommend running it through Distrobox.
⋅⋅1. Distrobox comes by default on Aurora Kionite, but if you are running, for example, base Fedora, a simple “sudo dnf install distrobox” in your terminal should work.
⋅⋅2. To make distrobox easier to use, we will also be using BoxBuddy – a GUI for it. I recommend downloading it from [Flathub](https://flathub.org/apps/io.github.dvlv.boxbuddyrs)
⋅⋅3. Open Boxbuddy, click the + at the top left, fill in the name as being “Debian,” and select “debian – quay.io/toolbx-images/debian-toolbox:latest” as your Image. Then, click Create, and let it do its thing.
⋅⋅4. When its done, there should be an open terminal window. If not, click on “Open Terminal” inside Boxbuddy. Do all commands in this section inside this terminal window, if you are using Distrobox. 
2. In your terminal, run “sudo apt install build-essential qtbase5-dev qt5-qmake qtbase5-dev-tools”
3. In your terminal, run the following commands to install Skyscraper
⋅⋅1. mkdir skysource
⋅⋅2. cd skysource
⋅⋅3. wget -q -O - https://raw.githubusercontent.com/muldjord/skyscraper/master/update_skyscraper.sh | bash
4. Go to home/.skyscraper. If you can’t find this folder, enble “Show Hidden Files”. In Dolphin, you can do this by pressing Ctrl+H
⋅⋅1. Delete “config.ini” and “artwork.xml”
⋅⋅2. Replace it with the “config.ini” and “artwork.xml” files from this github
5. Each console folder you have in home/Games will need you to run two commands for them. For this example, we will assume you are doing it for the DS (nds). Every console is exactly the same, but replace “nds” with the name of the folder you made earlier for each console.
⋅⋅1. Close Pegasus if its open. 
⋅⋅2. “Skyscraper -f pegasus -s screenscraper -p nds”
⋅⋅3. Wait until it says its done
⋅⋅4. “Skyscraper -f pegasus -p nds”
6. Go to home/Games/nds and check if theres a couple new files and a “Media” folder. If so, it worked!
7. While here, inside the folder named after the console open “metadata.pegasus.txt” in Notepad. 
⋅⋅1. Delete command: /opt/retropie/supplementary/runcommand/runcommand.sh 0 _SYS_ snes "{file.path}" near the top
⋅⋅2. Replace it with launch: flatpak run org.libretro.RetroArch -L "/home/rkabelitz/.var/app/org.libretro.RetroArch/config/retroarch/cores/mgba_libretro.so" {file.path}
⋅⋅⋅⋅1. (replace the mgba_libretro.so with whatever retroarch core you want to use for the given console)
⋅⋅⋅⋅2. Where it says “{file.path}”, that isnt me asking you to fill in a file path – literally just leave it as “{file.path}”
## 4. Finishing Touches
Now we just need to update Pegasus super fast, so it can see your games and their assets that you now obtained through Skyscraper

1. Open Pegasus
2. Click Esc, or the menu key on an xbox controller, click Settings.
3. Scroll down and click “Set game directories…”
4. Click the plus
5. Navigate to home/Games/[CONSOLE NAME HERE] and click on the “metadata.pegasus.txt” file
6. Click off to the side
7. It should ask if you want to reload – click OK
8. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. You should see all your games from the console you selected, with awesome artwork and shit!
9. Repeat steps 2-8 for each console folder you have

Windows
======

## 1. Organizing your File System
To get Pegasus working, as well as Skyscraper (we'll get to that later), we need our file system to be organized in a certain way.

1. On linux at least, I have a "Games" folder automatically created in my Home directory. No idea if you have that on windows too. For me it was empty, so I used it for this. If you have junk in there, either clean it out, or make a folder inside Games called "Pegasus" or something like that. If you don’t have a Games folder at all, maybe make one. It’s not a big deal – we just need a place for our ROMs. In this tutorial, Ill just assume youre using "home/Games"
2. Create a seperate folder for each console you emulate. 
⋅⋅1. Skyscraper, the metadata scraper, supports the following consoles. If you are, for example, emulating a DS, name the folder "nds" - keep it exactly the same as the names listed here: '3do', '3ds', 'amiga', 'amigacd32', 'amstradcpc', 'apple2', 'arcade', 'arcadia', 'astrocde', 'atari800', 'atari2600', 'atari5200', 'atari7800', 'atarijaguar','atarijaguarcd', 'atarilynx', 'atarist','atomiswave', 'c16', 'c64', 'c128', 'channelf','coco', 'coleco', 'daphne', 'dragon32','dreamcast', 'easyrpg', 'fba', 'fds','gameandwatch', 'gamegear', 'gb', 'gba', 'gbc','gc', 'genesis', 'intellivision', 'mame-advmame','mame-libretro', 'mame-mame4all', 'mastersystem','megacd', 'megadrive', 'moto', 'msx', 'msx2','n64', 'naomi', 'nds', 'neogeo', 'neogeocd','nes', 'ngp', 'ngpc', 'openbor', 'oric', 'pc','pc88', 'pc98', 'pcfx', 'pcengine', 'pcenginecd','pico8', 'pokemini', 'ports', 'ps2', 'psp','psx', 'saturn', 'scummvm', 'sega32x', 'segacd','sg-1000', 'snes', 'steam', 'switch', 'ti99','trs-80', 'vectrex', 'vic20', 'videopac','virtualboy', 'wii', 'wiiu', 'wonderswan','wonderswancolor', 'x68000', 'x1', 'zmachine','zx81', 'zxspectrum'
3. Inside these folders, place the relevant ROMs. For example, a GBA ROM goes in the “gba” folder.

## 2. Setting up Pegasus
Pegasus cannot run games itself (it will connect with Steam, Retroarch, etc. for that), nor can it get data on games (we use Skyscraper for that). All it does is look pretty, and connect to other software. All the screenshots I sent are of Pegasus.

1. Download from [here](https://pegasus-frontend.org/#downloads)
2. Should be a simple open and it works, but the default theme is kinda lame in my opinion at least. Luckily, we can change it! Ive tried all the big ones, I recommend one called BartopOS
⋅⋅1. Go [here](https://pegasus-frontend.org/tools/themes/), click on "bartopOS" (should be the second theme) and click download
⋅⋅2. extract the archive
⋅⋅3. move the resulting folder to "C:\Users\[username]\AppData\Local\pegasus-frontend\themes\" 
⋅⋅4. close and reopen Pegasus. Click Esc, or the menu key on an xbox controller, click Settings. Then, click Theme, and change it to bartopOS
⋅⋅5. While here, I recommend maybe changing fullscreen mode off if you want to
⋅⋅6. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. Youll probably see games already, from steam. Hopefully at least
3. At the top right of the screen is a cog wheel – thats the BartopOS settings. Go there
⋅⋅1. Maybe try enabling “Allow video thumbnails” in the General section. Very cool, but I found it to be laggy. Could be a linux problem, who knows. Worth trying out. 
⋅⋅2. Enable “Animate highlight” in the General section if it isn’t already
⋅⋅3. Enable “Full details view” in the Game Details section if it isn’t already
4. BartopOS says it needs Windows users, if they want to have videos for their games, to download a “K-lite Codec Pack” from here. It works without this on Linux so I havent done it… no idea how to do it, good luck.

## 3. Setting up Skyscraper
Pegasus has no information about what ROMs are – that information is provided by a scraper. I use skyscraper, which has only unofficial windows support. If it doesn’t work, try [Skraper.net](https://www.skraper.net/), but I havent used it so you’re on your own when it comes to making it work.

1. Download from [here](https://github.com/muldjord/skyscraper).
⋅⋅1. Go down under the “Windows” heading and download from there
2. Extract the archive
3. According to the very limited Windows documentation, you need to copy all folders from within the "deploy" folder to the C:\Users\<YOURUSER>\ folder
⋅⋅1. This means you should have a C:\Users\<YOURUSER>\.skyscraper and a C\Users\<YOURUSER>\RetroPie
4. Go to  C:\Users\<YOURUSER>\.skyscraper
⋅⋅1. Delete “config.ini” and “artwork.xml”
⋅⋅2. Replace it with the “config.ini” and “artwork.xml” files I sent you
5. The Windows documentation recommends that you run Skyscraper within [Cygwin terminal](https://cygwin.com/). This is not necessary, but simply makes the coloring work better, which could possibly make the program visually easier to use.
⋅⋅1. If you do want to do this, download “Setup-x86_64.exe” from under the Installing Cygwin header. 
6. Open Skyscraper.exe using either Cygwin (I imagine you can do this by right clicking then Open With) or just the Windows Terminal (Command Prompt? Whats it called in Windows again?)
7. Each console folder you have in home/Games will need you to run two commands for them. For this example, we will assume you are doing it for the DS (nds). Every console is exactly the same, but replace “nds” with the name of the folder you made earlier for each console.
⋅⋅1. Close Pegasus if its open. 
⋅⋅2. “Skyscraper -f pegasus -s screenscraper -p nds”
⋅⋅3. Wait until it says its done
⋅⋅4. “Skyscraper -f pegasus -p nds”
8. Go to home/Games/nds and check if theres a couple new files and a “Media” folder. If so, it worked!
9. While here, inside the folder named after the console open “metadata.pegasus.txt” in Notepad. 
⋅⋅1. Delete command: /opt/retropie/supplementary/runcommand/runcommand.sh 0 _SYS_ snes "{file.path}" near the top
⋅⋅2. Replace it with launch: C:\RetroArch\retroarch.exe  -L C\RetroArch\cores\bsnes2014_accuracy_libretro.so  {file.path}
⋅⋅⋅⋅1. (replace the bsnes2014_accuracy_libretro.so with whatever retroarch core you want to use for the given console)
⋅⋅⋅⋅2. Where it says “{file.path}”, that isnt me asking you to fill in a file path – literally just leave it as “{file.path}”
## 4. Finishing Touches
Now we just need to update Pegasus super fast, so it can see your games and their assets that you now obtained through Skyscraper

1. Open Pegasus
2. Click Esc, or the menu key on an xbox controller, click Settings.
3. Scroll down and click “Set game directories…”
4. Click the plus
5. Navigate to home/Games/[CONSOLE NAME HERE] and click on the “metadata.pegasus.txt” file
6. Click off to the side
7. It should ask if you want to reload – click OK
8. Esc, Esc (keyboard) or B, B (xbox controller) to get back to the main screen. You should see all your games from the console you selected, with awesome artwork and shit!
9. Repeat steps 2-8 for each console folder you have
