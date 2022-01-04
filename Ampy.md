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
## run
Then run it with the --no-output option and notice it immediately returns:
```
ampy --port /serial/port run --no-output test.py
```