# tool-openocd

PlatformIO meta tool for using custom versions of OpenOCD. The repo was created to solve uploading to a stm32 target via SWD with a ST-Link V3. The binary of the desired OpenOCD version is placed in `bin`. We have the STLINK-V3PWR which has different usb vendor and device ids as shown below. These have been added to `interfaces/stlink.cfg`.

```bash
$ lsusb
...
Bus 001 Device 033: ID 0483:3757 STMicroelectronics STLINK-V3PWR
...
```

## Usage

1. First uninstall `tool-openocd` using

```
pio pkg uninstall -g -t tool-openocd
```

2. Then install this git repo using

```
pio pkg install -g -t "https://github.com/jlab-sensing/tool-openocd.git"
```

3. Copy or link your openocd binary to `bin/openocd`

4. Configure your `platformio.ini`

```ini
[env:...]
platform_packages =
    ...
    https://github.com/jlab-sensing/tool-openocd.git
    ...
```

## Where to get binaries

### Unix

The STM32 fork of OpenOCD is compatible with our configuration of ST-Link V3 and *stm32wl55*. Downloading and compilation directions are found at: (https://github.com/STMicroelectronics/OpenOCD)[https://github.com/STMicroelectronics/OpenOCD]. After compilation you can link the binary using

```bash
ln -s [path to openocd] bin/openocd
```

### Windows

[TODO] Add direction on path to copy from the STM32CubeIDE
