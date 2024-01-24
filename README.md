# Guide for a dedicated Palworld Server running on Ubuntu

Big thanks to A1RM4X for the basic instructions to setup a dedicated Palworld server on Debian:

- Github: <https://github.com/A1RM4X/HowTo-Palworld>
- Youtube Video Part 1: <https://www.youtube.com/watch?v=0TjFLk_lP6c>
- Youtube Video Part 2: <https://www.youtube.com/watch?v=bjC081ERYcQ>

## Requirements

- fresh and clean Ubuntu Server installation (tested with version 22.04)
- SSH access

## Setup

1. Go to your `root` user
2. Update and upgrade your packages:

   ```bash
   apt update && apt dist-upgrade
   ```

3. Install SteamCMD using the following commands:

   ```bash
   apt install software-properties-common
   apt-add-repository non-free
   dpkg --add-architecture i386
   apt update
   apt install steamcmd
   ```

4. Install `sudo` and create a new user (here the username `steam` will be used):

   ```bash
   apt install sudo
   sudo adduser steam
   sudo passwd steam
   usermod -aG sudo steam
   ```

## Downloading the files by using SteamCMD

1. Login as user `steam`:

   ```bash
   su steam
   ```

2. Run SteamCMD to download all the files of the server:

   ```bash
   /usr/games/steamcmd +login anonymous +app_update 2394010 validate +quit
   ```

   All the files will now be downloaded into the folder `Steam` in the home directory.

## Creating symlinks to get the server running

1. Create new directories:

   ```bash
   mkdir ~/.steam
   mkdir ~/Steam/sdk32
   mkdir ~/Steam/sdk64
   ```

2. Create the necessary symlinks:

   ```bash
   ln -s /home/steam/.local/share/Steam/steamcmd/linux32/steamclient.so /home/steam/.steam/sdk32/
   ln -s /home/steam/.local/share/Steam/steamcmd/linux64/steamclient.so /home/steam/.steam/sdk64/
   ```

## Running the server

1. Go to the Palworld server directory:

   ```bash
   cd ~/Steam/steamapps/common/PalServer
   ```

2. Copy the default server settings to the configuration folder

   ```bash
   cp DefaultPalWorldSettings.ini Pal/Saved/Config/LinuxServer/PalWorldSettings.ini
   ```

   You can now use a text editor of your choice to change all the possible settings for the server by editing this file.

3. Run the server starting script:

   ```bash
   ./PalServer.sh -useperfthreads -NoAsyncLoadingThread -UseMultithreadForDS
   ```
