# Esp-idf Cheatsheet
## Installation
---------------
```bash
mkdir -p ~/esp
cd ~/esp
git clone --recursive https://github.com/espressif/esp-idf.git
```
Run installation script
```bash
cd ~/esp/esp-idf
./install.sh esp32
```
## Setup environment variables
------------------------------
one time
```bash
. $HOME/esp/esp-idf/export.sh
```
Since i use it regularly setup an alias for executing the export
1. Copy and paste the following to shell profile(`.bashrc`)
```bash
alias get_idf='. $HOME/esp/esp-idf/export.sh'
```
2. Refresh the configuration by restarting the terminal session or by running
```bash
source ~/.bashrc
```
## Start a project
```bash
mkdir <project name>
cd <project name>
cp -r ~/esp $IDF_PATH/examples/get-started/hello_world .
```
## Configure
### Setup/refresh esp-idf environment in terminal session
```bash
$ get_idf
```
### gotchas
```bash
$ get_idf
Adding ESP-IDF tools to PATH...
WARNING: tool cmake found in path, but failed to run
Not using an unsupported version of tool openocd-esp32 found in PATH: 0.10.0.
Checking if Python packages are up to date...
The following Python requirements are not satisfied:
click>=5.0
future>=0.15.2
pyelftools>=0.22
Please follow the instructions found in the "Set up the tools" section of ESP-IDF Getting Started Guide
```
solution
```bash
python -m pip install click>=5.0 future>=0.15.2 pyelftools>=0.22
```
### Set the target 
This should be done once after opening a new project
```bash
idf.py set-target esp32
```
### Configure project specific variables
e.g. Wi-Fi network name and password, the processor speed, etc.
```bash
idf.py menuconfig
```
## Build
```
idf.py build
```
This command will compile the application and all ESP-IDF components, then it will generate the bootloader, partition table, and application binaries.

## Flash ontu the device
Flash the binaries that you just built (bootloader.bin, partition-table.bin and hello_world.bin) onto your ESP32 board by running:
```bash
idf.py -p PORT [-b BAUD] flash
```

## Monitor
```
idf.py -p PORT monitor
```
