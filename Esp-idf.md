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
cd ~/esp $IDF_PATH/examples/get-started/hello_world .
```
## Configure
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