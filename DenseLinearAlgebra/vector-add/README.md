﻿# `vector-add` Sample

Vector Add is the equivalent of a ‘Hello, World!’ sample for data parallel
programs. Building and running the code sample verifies that your development
environment is set up correctly and demonstrates the use of the core features of
SYCL*.

For comprehensive instructions, see the [Intel&reg; oneAPI Programming
Guide](https://software.intel.com/en-us/oneapi-programming-guide) and search
based on relevant terms noted in the comments.


| Optimized for                     | Description
|:---                               |:---
| OS                                | Linux* Ubuntu* 18.04 <br>Windows* 10
| Hardware                          | Skylake with GEN9 or newer <br>Intel&reg; Programmable Acceleration Card with Intel&reg; Arria&reg; 10 GX FPGA
| Software                          | Intel&reg; oneAPI DPC++/C++ Compiler

## Purpose

The `vector-add` is a simple program that adds two large vectors of integers and
verifies the results. This program is implemented using C++ and SYCL* for
Intel&reg; CPU and accelerators.

In this sample, you can learn how to use the most basic code in C++ language
that offloads computations to a GPU. This includes using Unified Shared Memory
(USM) and buffers. USM requires an explicit wait for the asynchronous kernel's
computation to complete. Buffers, at the time they go out of scope, bring main
memory in sync with device memory implicitly; the explicit wait on the event is
not required as a result. This sample provides examples of both implementations
for simple side-by-side reviews (the Windows sample only supports USM).

The code attempts to execute on an available GPU and fallback to the system CPU
if a compatible GPU is not detected. If successful, the name of the offload
device and a success message is displayed, which indicates your development
environment is set up correctly.

In addition, you can target an FPGA device using the build scripts described
below. If you do not have FPGA hardware, the sample will run in emulation mode,
which includes static optimization reports for design analysis.

A detailed code walkthrough can be found in the [Explore SYCL* with Samples from
Intel](https://software.intel.com/content/www/us/en/develop/documentation/explore-dpcpp-samples-from-intel/top.html#top_STEP1_VECTOR_ADD)
guide.

## Key Implementation Details

The basic SYCL* implementation explained in the code includes device selector,
USM, buffer, accessor, kernel, and command groups.

## License
Code samples are licensed under the MIT license. See
[License.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/License.txt)
for details.

Third party program Licenses can be found here:
[third-party-programs.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/third-party-programs.txt).

## Known Issues
With oneAPI 2021.4 the argument for accessors was changed from `noinit` to
`no_init`. The change was derived from a change between the SYCL 2020
provisional spec and that of the 2020Rev3 spec

If running this sample and it fails, do one of the following
- Update the Intel® oneAPI Base Toolkit to 2021.4
- Change the 'no_init' argument  to 'noinit'

> **Note**: If you have not already done so, set up your CLI environment by
> sourcing  the `setvars` script located in the root of your oneAPI
> installation.
>
> Linux:
> - For system wide installations: `. /opt/intel/oneapi/setvars.sh`
> - For private installations: `. ~/intel/oneapi/setvars.sh`
>
> Windows:
> - `C:\Program Files(x86)\Intel\oneAPI\setvars.bat`
>
>For more information on environment variables, see Use the setvars Script for
>[Linux or
>macOS](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-programming-guide/top/oneapi-development-environment-setup/use-the-setvars-script-with-linux-or-macos.html),
>or
>[Windows](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-programming-guide/top/oneapi-development-environment-setup/use-the-setvars-script-with-windows.html).

### Running Samples in DevCloud

If running a sample in the Intel DevCloud, you must specify the compute node
(CPU, GPU, FPGA) and whether to run in batch or interactive mode. For more
information, see the Intel&reg; oneAPI Base Toolkit [Get Started
Guide](https://devcloud.intel.com/oneapi/get_started/).

### Using Visual Studio Code*  (Optional)

You can use Visual Studio Code (VS Code) extensions to set your environment,
create launch configurations, and browse and download samples.

The basic steps to build and run a sample using VS Code include:
 - Download a sample using the extension **Code Sample Browser for Intel oneAPI
   Toolkits**.
 - Configure the oneAPI environment with the extension **Environment
   Configurator for Intel oneAPI Toolkits**.
 - Open a Terminal in VS Code (**Terminal>New Terminal**).
 - Run the sample in the VS Code terminal using the instructions below.

To learn more about the extensions and how to configure the oneAPI environment,
see the [Using Visual Studio Code with Intel&reg; oneAPI Toolkits User
Guide](https://software.intel.com/content/www/us/en/develop/documentation/using-vs-code-with-intel-oneapi/top.html).

After learning how to use the extensions for Intel&reg; oneAPI Toolkits, return
to this readme for instructions on how to build and run a sample.


### On Linux* using the Command Line
Perform the following steps:

1. Build the program using the following `make` commands (default uses buffers):
    ```
    make all
    ```
> **Note**: For USM use `make build_usm`

2. Run the program using:
    ```
    make run
    ```
> **Note**: For USM use `make run_usm`

3. Clean the program using:
    ```
    make clean
    ```

### On Windows* Using a Command Line Interface

1. Select **Programs** > **Intel oneAPI 2021** > **Intel oneAPI Command Prompt**
   to launch a command window.
2. Build the program using the following `nmake` commands:
    ```
    nmake -f Makefile.win
    ```
> **Note**: For USM use `nmake -f Makefile.win build_usm`

3. Run the program using:
    ```
    nmake -f Makefile.win run
    ```
> **Note**: For USM use `nmake -f Makefile.win run_usm`

4. Clean the program using:
    ```
    nmake -f Makefile.win clean
    ```

### On a Windows* System Using Visual Studio* Version 2017 or Newer
Perform the following steps:
1. Launch the Visual Studio* 2017.
2. Select the menu sequence **File** > **Open** > **Project/Solution**.
3. Locate the `vector-add` folder.
4. Select the `vector-add.sln` file.
5. Select the configuration 'Debug' or 'Release'
6. Select **Project** > **Build** menu option to build the selected
   configuration.
7. Select **Debug** > **Start Without Debugging** menu option to run the
   program.

## Building the `vector-add` Program for Intel&reg; FPGA

### Linux*

Perform the following steps:

1. Clean the `vector-add` program using:
    ```
    make clean -f Makefile.fpga
    ```
2. Based on your requirements, you can perform the following:
   * Build and run for FPGA emulation using the following commands:
    ```
    make fpga_emu -f Makefile.fpga
    make run_emu -f Makefile.fpga
    ```
    * Build and run for FPGA hardware. (The hardware compilation can take a long
      time to complete.)
    ```
    make hw -f Makefile.fpga
    make run_hw -f Makefile.fpga
    ```
    * Generate static optimization reports for design analysis. Path to the
      reports is `vector-add_report.prj/reports/report.html`
    ```
    make report -f Makefile.fpga
    ```

### On Windows Using a Command Line Interface
Perform the following steps:

> **Note** On a Windows* system, you can only compile and run on the FPGA
emulator. Generating an HTML optimization report and compiling and running on
the FPGA hardware is not currently supported.

1. Select **Programs** > **Intel oneAPI 2021** > **Intel oneAPI Command Prompt**
   to launch a command window.
2. Build the program using the following `nmake` commands:
   ```
   nmake -f Makefile.win.fpga clean
   nmake -f Makefile.win.fpga
   nmake -f Makefile.win.fpga run
   ```

### On Windows Using Visual Studio* Version 2017 or Newer
Perform the following steps:
1. Launch the Visual Studio* 2017.
2. Select the menu sequence **File** > **Open** > **Project/Solution**.
3. Locate the `vector-add` folder.
4. Select the `vector-add.sln` file.
5. Select the configuration 'Debug-fpga' that have the necessary project
   settings already below:

        Under the 'Project Property' dialog:

     a. Select the **DPC++** tab. <br>b. In the **General** subtab, the
     **Perform ahead of time compilation for the FPGA** setting is set to
     **Yes**. <br>c. In the **Preprocessor** subtab, the **Preprocessor
     Definitions" setting has **FPGA_EMULATOR=1** added. <br>d. Close the
     dialog.

6. Select **Project** > **Build** menu option to build the selected
   configuration.
7. Select **Debug** > **Start Without Debugging** menu option to run the
   program.

## Running the Sample
### Application Parameters
There is an optional parameter which determines the size of vector. Default
value is 10000.

### Example of Output
```
Running on device:        Intel(R) Gen(R) HD Graphics NEO
Vector size: 10000
[0]: 0 + 0 = 0
[1]: 1 + 1 = 2
[2]: 2 + 2 = 4
...
[9999]: 9999 + 9999 = 19998
Vector add successfully completed on device.
```

## Troubleshooting
If you receive an error message, troubleshoot the problem using the Diagnostics
Utility for Intel&reg; oneAPI Toolkits, which provides system checks to find
missing dependencies and permissions errors. See [Diagnostics Utility for
Intel&reg; oneAPI Toolkits User
Guide](https://www.intel.com/content/www/us/en/develop/documentation/diagnostic-utility-user-guide/top.html).