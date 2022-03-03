# Ampy cheatsheet

## List files on the board
Example: list the root contents of a board run:
```bash
ampy --port /serial/port ls
```
## Read files from the board
Example: print the contents of /boot.py from a board run the following command:
```
ampy --port /serial/port get boot.py
```
## Remove file from the board
```
ampy --port /serial/port rm test.py
```
## Run
Then run it with the --no-output option and notice it immediately returns:
```
ampy --port /serial/port run --no-output test.py
```
## uploading a file
```bash
ampy --port /dev/ttyUSB0 put test.py
```
## Configuration
For convenience you can set an `AMPY_PORT` environment variable which will be used if the port parameter is not specified. For example on Linux:
```bash
export AMPY_PORT=/dev/ttyACM0
ampy ls
```
To set these variables automatically each time you run ampy, copy them into a file named `.ampy`:
```bash
# Example .ampy file
AMPY_PORT=/dev/ttyACM0
AMPY_BAUD=115200
```
