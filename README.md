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

The STM32 IDE uses OpenOCD to communicate with STM debuggers, so the STM32 generates an ```openocd.exe``` executable that can be used for PlatformIO.

Navigate to the STM32 generated OpenOCD file.

``` 
C:\ST\STM32CubeIDE_1.13.2\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.openocd.win32_2.3.0.202305091550\tools\bin\openocd.exe
```

If you cannot locate the openocd executable, search for ```openocd.exe``` on your local machine.

You will need to create a symbolic link between the STM32 executable and your ```~\.platformio\packages\tool-openocd\bin```.

Navigate to the location of your ```tool-openocd``` installation.

```
cd C:\Users\user\.platformio\packages\tool-openocd\bin
```

Create a symbolic link between your openocd.exe and your bin folder.

```
mklink "openocd.exe" "C:\ST\STM32CubeIDE_1.13.2\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.openocd.win32_2.3.0.202305091550\tools\bin\openocd.exe"
```

You should see a linked copy of your OpenOCD executable in C:\Users\user\.platformio\packages\tool-openocd\bin.

You will now need to add both ```"C:\ST\STM32CubeIDE_1.13.2\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.openocd.win32_2.3.0.202305091550\tools\bin``` and ```C:\Users\user\.platformio\packages\tool-openocd\bin``` to your system's PATH. Make sure to add the folders and not just the executables, just adding the executables will result in dependency errors. 
