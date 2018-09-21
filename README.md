# visual-studio-ftdi-libMPSSE-I2C
Ftdi MPSSE-I2C lib with Visual Studio 2017 x86_64. Isn't a project, this is just a "HOW TO" to compile the libMPSSE-I2C from FTDI to use with Visual Studio x84_64.

## Compilling libMPSSE-I2C

1. Download the source code from ftdi site: [LibMPSSE-I2C_source.zip](https://www.ftdichip.cn/Support/SoftwareExamples/MPSSE/LibMPSSE-I2C/LibMPSSE-I2C_source.zip)

2. Download and Install [*mingw64*](http://www.mingw.org) compiller and *make*.

3. Follow the instructions in file "...\LibMPSSE-I2C\Documents\BuildProcedure_LibMPSSE.txt". The ompiler will generate the *.obj, .a* and *.def* files inside the folder "...\LibMPSSE-I2C\LibMPSSE\Build\Windows\\"

4. To use the mingw lib with the Visual Studio compiller is neccessary a compatible .lib file. Use the *.def* file with visual studio tool called lib.exe. Run the Visual Studio command prompt, you could find it in Start->Visual Studio (2017)->Command Prompt.

5. In Visual Studio command prompt go to libMPSSE folder and type:

   ```powershell
   lib.exe /MACHINE:X64 /DEF:libMPSSE.def
   ```

6. The libMPSSE.lib file will be generated.

7. Copy the important project files, **libMPSSE.dll, libMPSSE.lib** from local folder, and the  **libMPSSE_i2c.h, WinTypes.h, ftd2xx.h** from "...\LibMPSSE-I2C\Release\samples\I2C" folder to your Visual Studio's project folder.

8. The last step is change the line inside WinTypes.h:

	```c
   #include <sys/time.h>
	```
   to 
   ```c
   #include <time.h>
   ```
