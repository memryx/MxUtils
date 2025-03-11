<picture>
  <source srcset="figures/mx_utils.png" media="(prefers-color-scheme: dark)">
  <source srcset="figures/mx_utils_light.png" media="(prefers-color-scheme: light)">
  <img src="figures/mx_utils_light.png" alt="MemryX Utilities">
</picture>


<!-- Badges for quick project insights -->
[![MemryX SDK](https://img.shields.io/badge/MemryX%20SDK-1.2-brightgreen)](https://developer.memryx.com)
[![MemryX SDK](https://img.shields.io/badge/MxAccl-1.2-brightgreen)](https://github.com/memryx/MxAccl)
[![C++](https://img.shields.io/badge/C++-17-blue)](https://en.cppreference.com)
[![OpenCV](https://img.shields.io/badge/OpenCV-gray)](...)
[![QT](https://img.shields.io/badge/QT-5-brightgreen)](...)

# MemryX Utilities

The MxUtils project provides **open-source code** for a variety of libraries, extensions, and utilities that enhance the functionality of the MemryX SDK. This repository offers transparency and flexibility for advanced development and customization. However, for a streamlined experience, the **default and recommended approach** is to use the [**MemryX SDK installation**](https://developer.memryx.com/get_started/install.html). The SDK delivers a fully integrated and optimized environment for efficient application development.

For guidance on setting up and using MemryX software, refer to the comprehensive resources available on the **[MemryX Developer Hub](https://developer.memryx.com)**.

### Full Documentation
For in-depth API details and technical references, visit the **[MemryX API Documentation](https://developer.memryx.com/api/index.html)**.

### Repository Overview

This repository includes the source code for two main components: `API_plugins` and `mxutils_gui`. These components are also available as pre-built packages, `memx-accl-plugins` and `memx-utils-gui`, bundled within the MemryX SDK for convenience.

| **Folder**         | **Description**                                                                                          |
|--------------------|----------------------------------------------------------------------------------------------------------|
| `API_plugins`      | MxAccl extensions that enable automatic inference for cropped Onnx, Tensorflow, and TFLite pre/post models |
| `mxutils_gui`      | A toolkit for creating and managing graphical user interfaces (GUI)                                      |

> **IMPORTANT**: We strongly encourage using the prebuilt `API_plugins` and `mxutils_gui` packages available through the [MemryX SDK](https://developer.memryx.com). This method simplifies the development process and ensures that all dependencies are correctly handled, providing a smoother and more reliable experience.

## Recommended Installation: MemryX SDK

The MemryX SDK provides all the necessary tools, drivers, and utilities for working with MemryX accelerators. Prebuilt packages for MxUtils components are `memx-accl-plugins` and `memx-utils-gui` and have [install instructions here](https://developer.memryx.com/tutorials/requirements/installation.html).

If you are simply developing applications that use MxUtils, not modifying MxUtils themselves, we recommend you use the prebuilt packages, and refer to the APIs here: [MxAccl (with pre/post plugins)](https://developer.memryx.com/api/accelerator/cpp.html) and [GUI Toolkit](https://developer.memryx.com/api/mxutils_gui.html).



## Advanced Installation: Building from Source

If you prefer building and installing MxUtils projects manually, clone this repo with:

### Step 1: Clone the repository

```
git clone https://github.com/memryx/MxUtils
```

Then, proceed with installing dependencies.

### Step 2: Build Dependencies

#### A. MxAccl Plugins

The MxAccl pre/post plugins require the following build dependencies.

##### 1. MxAccl core
The plugins require the core MxAccl runtime, which can be installed via the [memx-accl package](https://developer.memryx.com/get_started/install_driver.html) or built from [source](https://github.com/memryx/MxAccl).

##### 2. OnnxRuntime, TF, TFLite
We recommend using pre-built dependencies available [here](https://developer.memryx.com/example_files/mxutils_deps.tar.xz). Extract them so that `API_plugins/Deps/` contains the necessary libraries.

Alternatively, you can build/install these frameworks from source. Follow the 'Manual' steps outlined [here](https://developer.memryx.com/tutorials/requirements/installation.html) on the MemryX DevHub.

#### B. GUI Toolkit

`mxutils_gui` requires the following build dependencies.

##### 1. OpenCV

On Debian/Ubuntu and the like, you can install with `apt`:

```bash
sudo apt install libopencv-dev python3-opencv
```

Other Linux distros should use the equivalent packages from your package manager.


##### 2. Qt5

On **Ubuntu 20.04**, use:

```bash
sudo apt install qt5-default
```

On **Ubuntu 22.04 and later** and **Debian 11 and later**, use:

```bash
sudo apt install qtbase5-dev qt5-qmake
```

### Step 3: Build

After cloning the repo **and** building or downloading the dependencies,

```bash
mkdir build && cd build
cmake .. [-DBUILD_TYPE=[Debug | Release]]
make -j
```

If you omit the `-DBUILD_TYPE` flag, the type will default to *Release*.

### Step 4: Install

#### A. MxAccl Plugins

MxAccl expects pre/post plugins to be in specific directories:

- **Windows**: Same folder as `memx-accl.dll`
- **Linux**: Use one of the following paths:
    - `/opt/memryx/accl-plugins/`
    - `/usr/lib/`

Simply place the built files `lib*infer.so` (onnx, tf, tflite) into one of the valid paths.

If building MxAccl from source, you can instead modify these paths in `MxAccl/mx_accl/src/prepost.cpp`.

#### B. GUI Toolkit

To manually install `libmxutils_gui.so`:

```bash
sudo cp libmxutils_gui.so /usr/lib/
sudo cp gui_view.h /usr/include/memx/mxutils/
```

Then ensure your application is linked against these libraries and includes the appropriate headers.


## License

All MxUtils projects are open-source software under the permissive [MIT](LICENSE.md) license. But please note that external dependencies, Tensorflow and OnnxRuntime, have their own licenses as documented in the `API_plugins/debian*/copyright` file.


## See Also
Enhance your experience with MemryX solutions by exploring the following resources:

- **[Developer Hub](https://developer.memryx.com/index.html):** Access comprehensive documentation for MemryX hardware and software.
- **[MemryX SDK Installation Guide](https://developer.memryx.com/get_started/install.html):** Learn how to set up essential tools and drivers to start using MemryX accelerators.
- **[Tutorials](https://developer.memryx.com/tutorials/tutorials.html):** Follow detailed, step-by-step instructions for various use cases and applications.
- **[Model Explorer](https://developer.memryx.com/model_explorer/models.html):** Discover and explore models that have been compiled and optimized for MemryX accelerators.
- **[Examples](https://github.com/memryx/MemryX_eXamples):** Explore a collection of end-to-end AI applications powered by MemryX hardware and software.
