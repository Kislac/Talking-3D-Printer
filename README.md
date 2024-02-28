# Talking-3D-Printer
Description how to make a talking 3D Printer for key main states, like: Start/End Print, Filament Switch/Motion sensor alert, M600 command for filament change, for power failure detection, etc... \
Printer need to be run Klipper on Raspberry PI3/4/5, and Shell-Gcode-Command extension need to be installed.




## Needed HW: 
- Printer with Klipper and Raspberry PI3/4/5 (with 3,5mm aux)
- Any Speaker with Jack cable, which can be attached to RPI.
- I have using the one of the cheapest speaker: [GENIUS SP-HF180](https://genius-me.com/product/?i=sp-hf180): 
### Key features:
- Its USB powered, can be powered directly from RPI.
- 6W, which is loud enough to hear it in a normal house even with some background noise.
- It has a manual voulume control, so can be change to volume phisically and virtually as well. 

## Wiring
![image](https://github.com/Kislac/Talking-3D-Printer/assets/34631881/cc2c26cd-0c3b-46d0-8994-e2fc9a0a26f0)


## Preconfigs:
### Install Shell-Gcode-Command from Kiauh
- [Kiauh docu](https://github.com/dw-0/kiauh/)
- [Shell-Gcode-Command docu](https://github.com/dw-0/kiauh/blob/095823bf288029a2d8e147c275b0c3b8549edd57/docs/gcode_shell_command.md#L1)

Connect to the printer via SSH (like with putty)
### Install Kiauh and some dependencies (if its not installed yet):
```
sudo apt-get update && apt-get upgrade
sudo apt install pigpio
sudo apt-get install python-pigpio python3-pigpio
cd ~ && git clone https://github.com/dw-0/kiauh.git
```
### Start Kiauh:
```
./kiauh/kiauh.sh 
```
### Install Shell-Gcode-Command
In the Kiauh menu --> 4 (advance) --> 8 (extras) \
![2024-02-23_15h51_29](https://github.com/Kislac/Talking-3D-Printer/assets/34631881/ba7590a8-5b2b-4948-9d19-acbb400573de)
![2024-02-23_15h51_47](https://github.com/Kislac/Talking-3D-Printer/assets/34631881/2662b8c4-b932-40c8-8fbf-b7821986af62)

### Install VLC
- [Official VLC docu]([https://github.com/dw-0/kiauh/](https://raspberry-projects.com/pi/software_utilities/media-players/vlc-player))
- [Guide which i followed](https://pimylifeup.com/raspberry-pi-vlc/)
```
sudo apt install -y vlc
```

## Copy Audio files and shell_command.cfg to the printer config file
Drag & drop the audi files and from this repo.
![image](https://github.com/Kislac/Talking-3D-Printer/assets/34631881/9c49e31f-09a7-41f1-b4f8-1b64374b0033)

## Play Audio files
Now you can play the audio files from printer or call the shell command from klipper console: \
Try to play audio file from putty:
```
cvlc --play-and-exit /home/pi/printer_data/config/Music/hu_PrintStart.mp3
```
Or play the audio file from klipper console:
```
RUN_SHELL_COMMAND CMD=Play_PrintStart
```
Once audio file has played some error messages will be there, which i don't know how to remove it, but neverteless it not cause any problem at all.
![image](https://github.com/Kislac/Talking-3D-Printer/assets/34631881/5c19b5a7-ae26-4427-83b6-1c001651d96e)



## Volue control
You can get volume system voulme level with following command
```
amixer -M sget PCM
```
You can control the system volume level with following command. (% represent the volume level from 0-100%)
```
amixer -q -M sset PCM 30%
```
Or call the shell command from Klipper console as well:
```
RUN_SHELL_COMMAND CMD=Get_Volume
RUN_SHELL_COMMAND CMD=Set_Volume_80
```

### Shell command structure
More information in [Shell-Gcode-Command docu](https://github.com/dw-0/kiauh/blob/095823bf288029a2d8e147c275b0c3b8549edd57/docs/gcode_shell_command.md#L1)
- command: Command to be executed like in SSH
- timeout: Time in seconds after terminate the command. If the audio file is longer than this value, than the audio fule will be stopped.
- verbose: True--> Show the terminal messages within the klipper console. False --> Do not show the terminal messages within the klipper console

### Audio files
7 audio files has creted in english and hungarian language. \
I have used the https://ondoku3.com site for text to speach \
English Nanrator: English-David \
Hungarian Nanrator: Tamas

## Use cases:
- Error_FilamentMotion --> When filament motion sensor activated, beacuse of clogging. I have using the [Biqu SFS](https://biqu.equipment/products/btt-sfs-v1-0-smart-filament-sensor-detection-stuck-blocking-filament-module)
- Error_FilamentSwitch --> When filament switch sensor activated, beacuse out of filament
- Error_General --> Some general error message, which i am not using anywhere currently
- Error_PowerFailure --> Planned to be used with [Biqu UPS 24V](https://biqu.equipment/products/btt-ups-24v-v1-0-resume-printing-while-power-off-module) to resume the printing. Not used yet.
- FilamentChange --> For M600 g code command to pause the printing for filament change
- PrintEnd --> For Print end notification
- PrintStart --> For Print strat notification

## Change language.
Simply comment out the hungraian line and comment back the english line within shell_command.cfg
```
[gcode_shell_command Play_Error_FilamentMotion]
#command: cvlc --play-and-exit /home/pi/printer_data/config/Music/en_Error_FilamentMotion.mp3
command: cvlc --play-and-exit /home/pi/printer_data/config/Music/hu_Error_FilamentMotion.mp3
timeout: 10
verbose: False
```
