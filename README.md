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

Now you can call the shell command from klipper 
