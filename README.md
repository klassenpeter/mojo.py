# mojo.py
This tiny script loads a given `firmware.bin` file
to your [Mojo V3](https://alchitry.com/products/mojo-v3) board.
In the following the led demo firmware
[led_wave.bin](http://cdn.embeddedmicro.com/mojo/led_wave.bin)
is loaded.


## setup steps
To use this script, execute the following preparation steps.
See the [usage](#usage) section on how
to load a firmware to to your Mojo V3 board.


### clone this repo

```shell
git clone https://github.com/klassenpeter/mojo.py.git
```


### create a virtual environment
Enter the repo and use the venv python module (`-m venv`) to create a virtual environment
with the same name `venv`:
```shell
cd mojo.py
python -m venv venv
```


### activate the virtual environment
In your linux shell use the venv `activate` script to
enter your created virtual environment:
```shell
source ./venv/bin/activate
```

### install the dependencies
Unfortunately there is neither a pypi package (yet), nor a requrements.txt, thus
you need to install the `pyserial` package yourself:
```shell
pip install pyserial
```

### done
You are done with the setup. Do not forget to deactivate the virtual 
environment, if you keep the terminal open:
```shell
deactivate
```
To load a firmware proceed with the [usage](#usage) section.


## usage

### venv
first you need to activate your python virtual environment,
which you created in the [setup](#setup-steps) section:
```shell
source ./venv/bin/activate
```

Now you should be able to use the script, try:
```shell
./mojo.py -h
```
you should see:
```shell
usage: mojo.py [-h] [-i BITSTREAM] [-r] [-v] [-V] [-n] [-e] [-d MOJO_TTY] [-p] [BITSTREAM]

Mojo bitstream loader v2

positional arguments:
  BITSTREAM             Bitstream file to upload to the Mojo.

optional arguments:
  -h, --help            show this help message and exit
  -i BITSTREAM, --install BITSTREAM
                        Bitstream file to upload to the Mojo
  -r, --ram             Install bitstream file only to ram
  -v, --verbose         Enable verbose output to cli.
  -V, --version         Display version number of mojo.
  -n, --no-verify       Do not verify the operation to the Mojo.
  -e, --erase           Erase flash on Mojo.
  -d MOJO_TTY, --device MOJO_TTY
                        Address of the serial port for the mojo [Default: /dev/mojo]
  -p, --progress        Display progress bar while uploading.
(venv) ➜  mojo.py git:(further_rework)
```

### get your firmware
To test the upload procedure, you could use a firmware that is provided by the manufacturer:
```shell
wget http://cdn.embeddedmicro.com/mojo/led_wave.bin -O ../led_wave.bin
```

### serial port
To check which port name your Mojo V3 board is assigned to,
you could do something like:
```shell
journalctl -f
```
Now connect your Mojo and search the log output
for something like `/dev/ttyUSB0` or `/dev/ttyACM0`.
Alternatively see which `/dev/tty*` gets created after
the insertion.


### flash
Finally upload the bin file to your Mojo board:
```shell
./mojo.py -i ../led_wave.bin  -d /dev/ttyACM1 -v
```

### have fun
