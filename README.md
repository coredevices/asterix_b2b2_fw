# Debugprobe

Firmware source for the Raspberry Pi Debug Probe SWD/UART accessory,
modified to run on `asterix_b2b2v2`.

[Raspberry Pi Debug Probe product page](https://www.raspberrypi.com/products/debug-probe/)

[Raspberry Pi Pico product page](https://www.raspberrypi.com/products/raspberry-pi-pico/)


# Documentation

Debug Probe documentation can be found at the [Raspberry Pi Microcontroller Documentation portal](https://www.raspberrypi.com/documentation/microcontrollers/debug-probe.html#about-the-debug-probe).

# Hacking

For the purpose of making changes or studying of the code, you may want to compile the code yourself.

First, clone the repository:
```
git clone https://github.com/raspberrypi/debugprobe
cd debugprobe
```
Initialize and update the submodules:
```
GIT_LFS_SKIP_SMUDGE=1 git submodule update --init --recursive --progress
```

(Note that the `GIT_LFS_SKIP_SMUDGE` is required to successfully check out the obsolete `CMSIS_5`; see [ARM-software/CMSIS_5#1201](https://github.com/ARM-software/CMSIS_5/issues/1201).)

Then create and switch to the build directory:
```
 mkdir build
```
If your environment doesn't contain `PICO_SDK_PATH`, then either add it to your environment variables with `export PICO_SDK_PATH=/path/to/sdk` or add `PICO_SDK_PATH=/path/to/sdk` to the arguments to CMake below. 
Or, have CMake download it yourself, as shown below as well.

Run cmake and build the code:
```
 cmake -B build -DPICO_SDK_FETCH_FROM_GIT=on -DPICOTOOL_FORCE_FETCH_FROM_GIT=1
 make -C build
```
Done! You should now have a `asterix_b2b2v2.uf2` that you can upload to your Debug Probe via the UF2 bootloader.

# TODO
- AutoBaud selection, as PIO is a capable frequency counter
- Possibly include RTT support
