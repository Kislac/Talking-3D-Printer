# Talking-3D-Printer
Description how to make a talking 3D Printer for key main states, like: Start/End Print, Filament Switch/Motion sensor alert, M600 command for filament change, for power failure detection, etc...
Printer need to be run Klipper on Raspberry PI3/4/5, and Shell-Gcode-Command extension need to be installed.




Needed HW: Any Speaker with Jack cable, which can be attached to RPI.
I have using the one of the cheapest speaker: GENIUS SP-HF180: https://genius-me.com/product/?i=sp-hf180
Its USB powered, can be powered directly from RPI.
6W, which is loud enough to hear it in a normal house even with some background noise.
It has a manual voulume control, so can be change to volume phisically and virtually as well. 




Steps need to be done. (Work in progress)

sudo apt-get update && apt-get upgrade
sudo apt install pigpio
sudo apt-get install python-pigpio python3-pigpio

then, if it hasn't been there yet, install the Shell-Gcode-Command add-on with Kiauh
https://github.com/dw-0/kiauh/blob/095823bf288029a2d8e147c275b0c3b8549edd57/docs/gcode_shell_command.md#L1

https://github.com/dw-0/kiauh/tree/master

In the Kiauh menu, 4 (advance) and then 8 (extras)





Step 1:
To download this script, it is necessary to have git installed. If you don't have git already installed, or if you are unsure, run the following command:
sudo apt-get update && sudo apt-get install git -y
Step 2:
Once git is installed, use the following command to download KIAUH into your home-directory:
cd ~ && git clone https://github.com/dw-0/kiauh.git
Step 3:
Finally, start KIAUH by running the next command:
./kiauh/kiauh.sh
