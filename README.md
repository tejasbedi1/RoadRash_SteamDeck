# Road Rash 1994 on the SteamDeck (WIP)
[//]: # (Insert Image you posed on Reddit)
How to run Road Rash's Windows version on the Steam Deck With Videos &amp; Music.

### Game Version
Road Rash 1994, (1996 Windows Release)
https://en.wikipedia.org/wiki/Road_Rash_(1994_video_game)

## Precursor
This one took a while to get running and it was a frustrating process.
Anyhow I;m doing this write up so that you don't have bash your head agaist the wall
to get this running.

Note: Its possible to Run Road Rash on emulators for some consoles (3DO, Sega CD, PlayStation, Saturn). But these versions 
lack a dashboard. Which to my knowledge was only present in the windows version of the game.

## 1. Get the Game
This game today comes under the abondonware category. Thankfully EA is not as aggresive as Nintendo when 
it comes to DMCA's.
For our case we need 2 Major things. 
- An iso of the game. (For the videos) Archive.org worked for me 
https://archive.org/details/roadrash_201910
You can get the ISO from anywhere basically. It will be approximately 519 MB large

- Next we need a version of the game with a No CD fix
Orginally the CD had to be put in. In today windows PC we will have to Mount an iso to get it to run
This funfortunately is difficult to do on a steam deck, (Not impossible, just distasteful)

Although you can find it in websites like https://www.myabandonware.com/
It can be a hit or miss in some cases. So In order to save you people some headache. 
I attached a file in the repo with the fixes. They work on my steam deck and 
there are almost no reasons it doesent work on yours.

## 2. Prepare the files
Although you can do this step on the deck itself its easier on a PC. 
- Mount the iso file. On windows (10 and up, itll be funny if youre doing this while windows 12 is out cause theres not even a rumor of it atm).  
- anyhow right click and mount. 
- copy all files and paste it in a fresh directory. We need to send these to the deck.
- next unizip the files in the repo and paste them to the root directory of the game. Overrite any conflicts.

## 3. Send folder to the deck
Now send this folder to the deck, (You will have to switch to deskop mode if thats still unclear.) 
Easiest way I've found to share is to use KDE connect. Just open it on your PC/mac and
on the deck. Make sure both are connected to the same Wifi, pair and then select send file from the pc/mac . 
Google this if you get stuck. 
Or you can just zip the file and send it to a cloud service and pull. Or use a usb stick

## 4. Place Files
Now after you have them on your deck. Place them in a neat place. My location was the SD Card. In a folder i had named windows.
As it represented windows games.

## 5. How to Run
Now how do we run this. We will use wine!! (Wine 7 to be exact) Open the discover app on the deck and install wine.
I did spend a lot of time around with lutris and tured multiple proton versions to run the exe. But to no awail.
It always game me an error, stating the game hasnt been properly installed or that there was no CD detected. 
At some point it just wasnt worth spending more time on it.

## 6. Wine Settings
Now we change a few configuration settings  on wine so that things run correctly with needed.
Without this Wine will run in potrait mode. And it just looks so damn ugly.

open knsole app on the deck and type. "org.winehq.Wine winecfg" press enter 
It will open a window with wine. (Trackpad might not work in the mode. To move the mouse hold the steam button while moving the mouse)
Head on to the Graphics tab and change 
- desktop size to 1280 * 800
- Check emulate a virtal desktop

## 7. Music Tuning
With these settings wine will be able to run the game. And we should be able to see videos since we included that folder.
But there is still a problem. The in race music. Apparently the in-race music is MIDI music. And the steam deck, most linux machines 
do not have a sythsizer for this kind of music. (I aplogize if I over simiplied the explanation). 
Which will result with us not hearing the iconic music. So to make it work.
We need to install a MIDI synthezier. 

## 8. Qsynth Setup 
The process which I will explain as well is taken from here (https://steamcommunity.com/sharedfiles/filedetails/?id=2809933598)
So head over to the dicover store again and install Qsynth.

Next we need a sound front to tell the Midi engine, what to play. I like Scc1t2.sf2 (http://www.vogonsdrivers.com/getfile.php?fileid=500)
Download and unzip the soundfront

## 9. Flatseal
Now if you are installing the game on the SD card, do this. Before sompleting Qsynth setup make we need to make sure Qsynth and Wine can 
access our SD card. So head on to the discover store one last time and install an application called Flatseal. Once installed open it.

## 10. Config Flatseal
Fine both Wine and Qsynth in it. Scroll down to Filesystem and under "Other files" add, /run/media. This will allow these apps to access the 
SD card properly. Be sure to save these changes, even though these is no save button and close flatseal.

## 11. Qsynth Config
Now Open Qsynth. (You can find it in the start menu, under all applications). Turn down the gain volume to somewhere bettween 20~60. The 
default is too high. Press 'Setup', Select 'SoundFronts', Click on 'Open' and navigate to the .sf2 file and open it. Press Ok to confirm the soundfront.

 Next, we must set up Qsynth to start minimized, so that it will not get in the way of the game.
Go back to the Qsynth main window, and press the 'options' button in the top right.
Tick the 'Enable system tray icon' checkbox.
Tick the 'Start minimized to system tray' checkbox.
Thats it for Qsynth. 

## 12. Road Rash executable
Now the last step. Create an empty file and name it 'road.sh'. Or any name you want.
This will have the startup instructions for steam. On how to launch the game.

I have placed this file next to the game folder. under sdcard/windows/road.sh
Its contents are like So. 

`#!/bin/bash

flatpak run org.rncbc.qsynth &
cd "run/media/mmcblk0p1/windows/Road Rash A1/Road Rash"
flatpak run org.winehq.Wine "ROADRASH.EXE" > log.txt 2>&1

killall -9 qsynth`

This script will make sure. Qsynth is run befroe the game starts and is closed after the game is stopped.
It will also ofcouse instrict wine to Run the game.

## 13. Finalize
Close the editor of the file. And right click and open properties. Nake sure the sh file "is_executable".
At this point you can double click the file and check if the game runs. If it does, you won. If it did not then I'm 
sorry something went wrong somewhere. Please recheck all steps.

## 14. Go to steam 
Now lets add it to steam. Head over to steam in . Click on Add a game and "Add a non Steam Game". Find and select the sh file.
Once added, you can exit dessktop mode. I believe you;ll be able to do the rest. Chaning the game name to something proper and adding artwork to it.

## DONE
and there you go. Thanks!!
For any queries feel free to check out at tejas.bedi1@gmail.com
I havnt been able to try this out on a vanilla deck. So if it dosent work on one, please let me know. :)








