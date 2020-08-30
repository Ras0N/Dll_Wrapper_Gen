DLL Wrapper Generator
=====================

Automatic generation of Dll wrapper for both 32 bit and 64 bit Dll.

This code parses a windows DLL and generates a wrapper that exports the same symbol. 
By default, the wrapper function points to the original function by a jump instruction.
You can modify and insert code for some of the function if you know its signature.



Forked from mavenlin/Dll_Wrapper_Gen

usage:

1. put your dll file into the same folder where Generate_Wrapper.py exists.

2. open a console and run the following command and you'll get what you want.

   ```bash
   python Generate_Wrapper.py <yourdllname>.dll
   ```

## A simple guide about editing your own proxy-dll

for x64 dlls:

1. open the generated .asm assembly file, find the function you want to wrap:

   ```assembly
   <function name> proc
       jmp mProcs[INDEX*8]
   <function name> endp
   ```

   select them and delete.

2. find the function declaration in the .cpp file, re-declare it and write you own logics. The original function can be obtained by the following method:

   ```c++
   returnType (*functionPointerName)(param list) = (returnType (*)(param list))mProcs[INDEX]
   ```

   and been called by:

   ```c++
   returnType res = (*functionPointerName)(params);
   ```



for x86 dlls:

​	just delect *__declipec(naked)* and do your tricks.

