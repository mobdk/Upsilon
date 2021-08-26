# Upsilon
Upsilon execute shellcode with syscalls - no API like NtProtectVirtualMemory is used

NtProtectVirtualMemory is used in many PoC to change allocated memory with RWX, this PoC do not use any API calls but create a MemoryMappedFile
to execute our shellcode with syscalls.

Resolver function is just a "sinkhole" for the Mimikatz payload, Mimikatz is converted to shellcode and then converted to 3 digits numeric format, 
the final code is pasted in the compiled Upsilon.exe with a hex editor, this technique breaks the string logic in C# string and makes it hard for
AV/EDR to analyse the contex both before execution and at execution.

Two syscalls is used: NtCreateSection/0x004A and NtMapViewOfSection/0x0028

This is tested on Windows 10 build 20H2 64 bit only.

Compile: csc.exe /platform:x64 /target:exe /unsafe Upsilon.cs

Upsilon.exe is compiled version with Mimikatz embedded and ready to test
