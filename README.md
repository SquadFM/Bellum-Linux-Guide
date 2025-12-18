# Install Bellum on Arch-like Linux Distros
- Note: This guide is based on Joepaji's excellent Fedora Linux instructions. All credit goes to Joe. I only adopted it for Arch. Most lines are copy-pasted from Joe's guide.
- Joe's Fedora guide: https://discord.com/channels/1252319655289159680/1254497950080565288/1441475646118297712

## My system
- EndevourOS
- AMD 9070 XT

## Install required software
```
yay -S protonplus
yay -S wine-staging
yay -S winetricks
yay -S lutris
yay -S gamemode #optional
```

## protonplus config
- start protonplus (should be in your start menu)
- Switch it to Lutris mode from the top-left corner.
- Scroll to Wine-Proton (Kron4ek) and download version 10.0-3.
- Note: This Proton build lacks DXVK and VKD3D; we'll add these via Winetricks later.

- verify that folder is not empty:
```
ls -l /home/$USER/.local/share/lutris/runners/wine/wine-proton-10.0-3-amd64/bin/
```
- set install directory (folder must not exist - replace /home/x with your home folder):
```
export WINEPREFIX=/home/x/Games/Bellum
```
- go to directory below and run wineboot (replace /home/x with your home folder):

/home/x/.local/share/lutris/runners/wine/wine-proton-10.0-3-amd64/bin/wineboot -u
- it may offer to install .NET, do so by clicking OK

## Lutris - config
- Open Lutris and remove any existing Bellum entry from the library.
- On left panel, go to Runners → Wine → Settings (gear icon)
- Under Runner Options => Wine Version => select System (10.19 (Staging))
- Ensure DXVK and VK3D are enabled (skip dgvoodoo2).
- Under System Options, enable (I am not entirely sure if or how these affect stuff):
  - Disable Lutris Runtime (toggle on)
  - Prefer system libraries (toggle on)
- Save

## Lutris - set game options
- On top left corner, press + to add game → Add locally installed game (its not installed yet but we will get there)
- Set the name to "Bellum", choose Wine as the runner.
- Under Game Options, set the wine prefix to your earlier WINEPREFIX that we set in Step 8 (/home/x/Games/Bellum)
- Leave Executable path empty for now.
- Ensure System (10.19 (Staging)) is selected.
- Ensure Gamescope is NOT enabled. It doesn't exit properly with that and leaves dangling processes.
- Save.

## Lutris - check that correct Wine version is used
- Select the game > click the Wine up-arrow (at the bottom, next to "Play" button) > Wine Configuration.
- The Applications tab in the new window should show many entries (not only “Default Settings”). This confirms Proton-Wine is the underlying base. Close the window. If that's not the case, start over.

# Lutris - install DXVK + VK3D via Winetricks
- Select the game > click the Wine up-arrow (at the bottom, next to "Play" button) > Winetricks
- Choose "Select the default wineprefix" > "OK" > "Install a Windows DLL or Component" > Install all of the following (multi-select allowed):
  - dxvk
  - dxvk2053
  - dxvk_nvapi0061
  - vk3d
- If you are running Nvidia GPU, its very possible that these steps will be different for you (also possible it'll work). I am on AMD 9070XT with mesa vulkan drivers.
- After installation completes, the winetricks window will come back. Close the Winetricks window after that.

## Lutris - install Bellum
- Select the game > click the Wine up-arrow (at the bottom, next to "Play" button) > "Run EXE inside wine prefix"
- Select the Bellum launcher installer (AstarteLauncher-amd64-installer.exe) that was provided to us from devs.
- Complete the installer normally.
- NOTE: If installation goes through really quickly in a handful of seconds, then it probably did not work.

## Lutris - Post Install - Set Executable in Lutris
- In Lutris, right-click the Bellum entry > Configure.
- Under Game Options, set the launcher executable. Example path:

/home/x/Games/Bellum/drive_c/users/steamuser/AppData/Local/Astarte Industries/Astarte Launcher/AstarteLauncher.exe
- And that's it! You should now be able to launch the game from Lutris.

## Issues
- Mouse cursor not visible in launcher. You can kind of track where the mouse cursor is at if you press ALT and the click (which moves the window, but also shows the location of the cursor).




