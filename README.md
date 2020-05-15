# Azure RTOS FileX

This is a high-performance, file allocation table (FAT)-compatible file system that’s fully integrated with Azure RTOS ThreadX and available for all supported processors. Like Azure RTOS ThreadX, Azure RTOS FileX is designed to have a small footprint and high performance, making it ideal for today’s deeply embedded applications that require file management operations. FileX supports most physical media, including RAM, Azure RTOS USBX, SD CARD, and NAND/NOR flash memories via Azure RTOS LevelX.

## Documentation

Documentation for this library can be found here: http://docs.microsoft.com/azure/rtos/filex

## exFAT Licensing

FileX supports the Microsoft exFAT file system format using the FX_ENABLE_EXFAT define. See [common/inc/fx_user_sample.h](common/inc/fx_user_sample.h) for more information about configuration of FileX.

Your use of exFAT technology in your products requires a separate license from Microsoft. Please see the following link for further details on exFAT licensing: https://www.microsoft.com/en-us/legal/intellectualproperty/mtl/exfat-licensing.aspx

# Understanding inter-component dependencies

The main components of Azure RTOS are each provided in their own repository, but there are dependencies between them--shown in the following graph--that are important to understand when setting up your builds.

![dependency graph](docs/deps.png)

# Building and using the library

## Prerequisites

Install the following tools:

* [CMake](https://cmake.org/download/) version 3.0 or later
* [GCC compilers for arm-none-eabi](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)
* [Ninja](https://ninja-build.org/)

## Cloning the repo

```bash
$ git clone https://github.com/azure-rtos/filex.git
```

## Building as a static library

Each component of Azure RTOS comes with a composible CMake-based build system that supports many different MCUs and host systems. Integrating any of these components into your device app code is as simple as adding a git submodule and then including it in your build using the CMake command `add_subdirectory()`.

While the typical usage pattern is to include threadx into your device code source tree to be built & linked with your code, you can compile this project as a standalone static library to confirm your build is set up correctly.

```bash
$ cmake -Bbuild -DCMAKE_TOOLCHAIN_FILE=cmake/cortex_m4.cmake -GNinja .

$ cmake --build ./build
```

NOTE: You will have to take the dependency graph above into account when building anything other than threadx itself.

# Repository Structure and Usage

## Branches & Releases

The master branch has the most recent code with all new features and bug fixes. It does not represent the latest General Availability (GA) release of the library.

## Releases

Each official release (preview or GA) will be tagged to mark the commit and push it into the Github releases tab, e.g. `v6.0-rel`.

## Directory layout

```
- cmake
- common
  - inc
  - src
- ports
  - cortex_m0/gnu
    - inc
    - src
  - cortex_m3/gnu
    - inc
    - src
  - cortex_m4/gnu
    - inc
    - src
  - cortex_m7/gnu
    - inc
    - src
- samples
```

# Contribution, feedback and issues

If you encounter any bugs, have suggestions for new features or if you would like to become an active contributor to this project please follow the instructions provided in the contribution guideline for the corresponding repo.

For general support, please post a question to [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-rtos+threadx) using the `threadx` and `azure-rtos` tags.