# pico-sdk-devcontainer

(WIP) A dead simple Dev Container skeleton of the newbie, by the newbie for the newbie.

Based on [Getting started with Raspberry Pi Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) (Release: 2.2, Date: 14 Jun 2023)

## Usage

Copy `.devcontainer`, `.vscode` and `pico_sdk_import.cmake` (optionally `CMakeLists.txt` and `test.c` as a project skeleton) to your Pico SDK project.

## Windows

1. Install WinUSB driver for Picoprobe with [Zadig](https://zadig.akeo.ie/).
2. Copy [60-openocd.rules](https://github.com/raspberrypi/openocd/blob/rp2040/contrib/60-openocd.rules) to `/etc/udev/rules.d` on WSL2 then [restart udev](https://github.com/dorssel/usbipd-win/wiki/WSL-support#udev).
3. Connect Picoprobe to WSL2 with [usbipd-win](https://github.com/dorssel/usbipd-win), may need to rebuild the kernel if the version is older than 5.10.60.1.
