# visual-studio-ftdi-libMPSSE-I2C

Ftdi MPSSE-I2C ou MPSSE-SPI lib with Visual Studio 2017 x86_64. Isn't a project, this is just a "HOW TO" to compile the libMPSSE-I2C from FTDI to use with Visual Studio x84_64.

## Content
Due the mingw incompatibility with visual studio toolchain, is necessary a new compilation to provide useful libs for visual studio. The pre-compiled x86  libs are provided with the MPSSE lib, with version for visual studio x86 and mingw, but  not the x86_64 version for visual studio. This tutorial demonstrate the use of lib.exe, a Visual Studio tool and dlltool.exe from mingw, to generate a compatible lib from the .def file generated by lib compilation with mingw64.



## Compilling libMPSSE-I2C

1. Download the source code from ftdi site: [LibMPSSE-I2C_source.zip](https://www.ftdichip.cn/Support/SoftwareExamples/MPSSE/LibMPSSE-I2C/LibMPSSE-I2C_source.zip)

2. Download and Install [*mingw64*](http://www.mingw.org) compiller and *make*.

3. Follow the instructions in file "...\LibMPSSE-I2C\Documents\BuildProcedure_LibMPSSE.txt". The ompiler will generate the *.obj, .a* and *.def* files inside the folder "...\LibMPSSE-I2C\LibMPSSE\Build\Windows\\" 



## Generate .lib with lib.exe from Visual Studio

In Visual Studio command prompt go to libMPSSE folder and type:

   ```powershell
   lib.exe /MACHINE:X64 /DEF:libMPSSE.def
   ```



## Generate .lib with dlltool.exe from mingw

Go to the  to libMPSSE folder and type:

   ```
   dlltool.exe -d libMPSSE.def -D libMPSSE.dll -l libMPSSE.lib
   ```



## To use the files in Visual Studio

1. Copy the important project files, **libMPSSE.dll, libMPSSE.lib** from local folder, and the  **libMPSSE_i2c.h, WinTypes.h, ftd2xx.h** from "...\LibMPSSE-I2C\Release\samples\I2C" folder to your Visual Studio's project folder.

9. The last step is change the line inside WinTypes.h:

  ```c
  #include <sys/time.h>
  ```
  to 
  ```c
  #include <time.h>
  ```



## Considerations

- Some times lib.exe tool ignores some functions and do not exports to the .lib file, in this case use the dlltool.

- You can generate a complete lib I2C + SPI, fot this you need do add the SPI source folder in the Topllayer folder from libMPSSE and modify the makefile as this [makefile](makefile). 
