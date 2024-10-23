# Touch Host Controller (THC) Linxu Drivers

Intel Touch Host Controller (THC) is a new high performance input IP which can benefit HID device's data transaction, such as touch screen, touch pad, stylus.

THC IP now evoluates to V4, it can support 3 different modes: IPTS, HIDSPI and HIDI2C. Here are upgrade history:
- THC v1, for TGL/LKF, supports intel private IPTS (Intel Precise Touch and Stylus) protocol ( IPTS mode)
- THC v2, for ADL, add industrial standard HID over SPI protocol support (HIDSPI mode)
- THC v3, for MTL, enhance HID over SPI mode
- THC v4, for LNL, add inudstrial standard HID over I2C protocol support (HIDI2C mode) 

Linux Surface community (https://github.com/linux-surface) already implemented IPTS mode. These patch series provides THC HIDSPI mode and THC HIDI2C mode support on Linux.

These patch series includes:
- Document for THC hardware and software introduction.
- Intel THC Hardware layer driver which provides control interfaces for protocol layer.
- Intel QuickSPI (R) driver working as a HIDSPI device driver which implements HID over SPI protocol and flow.
- Intel QuickI2C (R) driver working as a HIDI2C device driver which implements HID over I2C protocol and flow.

## Content of this repository:
- driver_source_code: THC drivers source code
- pathes: patches
- Documents: documents for THC IP and THC drivers

## Dependencies:
- BIOS: THC must be enabled in BIOS, and ACPI parameters are correctly configured.
- Touch Device: TouchScreen/TouchPad must be compatible with HIDSPI or HIDI2C protocol and connected correctly.
- Linux Kernel: version >= 6.8

## Test Environment:
- Board: Intel LNL Reference & Validation Platform Board.
- Touch Device:
    - Elan HIDI2C TouchScreen with Stylus
    - Elan HIDSPI TouchScreen with Stylus
    - Wacom HIDSPI TouchScreen with Stylus
    - THAT TouchPad in multi-touch mode
    - ALPS TouchPad in mouse mode
- Linxu Kernel: V6.10 and V6.11

# How to Build

## 1. Build with kernel source tree
- Clone and checkout Linux kernel source tree
- Copy driver_source_code/include/linux/* to $(kernel_tree)/include/linux/*
- Copy driver_source_code/intel-thc-hid folder to &(kernel_tree)/drivers/hid/
- Include intel-thc-hid/Makefile into &(kernel_tree)/drivers/hid/Makefile
- Include intel-thc-hid/Kconfig into &(kernel_tree)/drivers/hid/Kconfig
- Add follow lines to kernel configure file:
    ```sh
        CONFIG_INTEL_THC_HID=m
        CONFIG_INTEL_QUICKSPI=m
        CONFIG_INTEL_QUICKI2C=m
    ```
- Build kernel
