# A2osX (0.92) Multi-Tasking OS for Apple II  

## Disk images :  

+ **A2OSX.BOOT.po**   :  **(0.92)**  140k BOOT disk image with all binaries  
+ **A2OSX.DEV.po**    :  **(0.92)**  140k disk image with ASM binaries, Debug Tools & INClude files  
+ **A2OSX.BUILD.po**  :  **(0.92)**  800k BOOT disk image with S-C MASM 3.0 and all binaries (BOOT+DEV)  
+ **A2OSX.SRC.po**    :  **(0.92)**  800k disk image with all sources  

## Latest News 2018-11-10

My loneliness has been cured, new resources have signed onto the project.  I welcome Patrick Kloepfer
who is helping with product management, recruitment, testing and feedback. 

## News 2018-09-06

0.92 stable enough to resume playing with.
Many 0.9.1 bugs already corrected in this version, please check & close opened issues.

## News 2018-07-20

Kernel & some BINs/SBINs migrated to 0.92.

## News 2018-06-17

Ok, as i'm still the lone developer here, i decided to break the kernel, HAHAHAHAHAHA!!!!
I updated the Calling Convention (see projects), i now setup the header in each KERNEL.S.* file accordingly to generate doc, then i change the code...

So ....nothing works anymore on the A2OSX.BUILD media...

## News 2018-06-13

Previous (relatively!) stable version 0.9.1 has been archived, see link above.  

Roadmap for 0.9.2:
 + Organize this roadmap in projects (anybody interested in a PM job ?)
 + Organize Testing (Testers wellcome)
 + NET : TCPIP Network services, AppleTalk (Coders wellcome)
 + GUI : Window Manager (Coders wellcome)
 + DEV : ASM, CSH, C compiler, someone suggested PLASMA (Coders wellcome)
 + release Version 1.0.0
 
Sub projects:
 + Finalize enhanced STDIO (Buffered IO)
 + Link UDP/TCP sockets to new STDIO
 + Rewrite Driver interface (SmartPort Protocol) and link to STDIO
 + establish parameter passing convention (C-like Stack frame)
 + Move all LIBs to this new convention to allow preemtive mode for LIBs
 + AT commands (Appletalk)
 + TELNETD/HTTPD/NFSD (STDIO)
 + GUI : Window Manager, Controls...
 + Assembler (AUX mem manager) will allow A2osX to build entirely itself every night!
 + Shell CSH (MATH API, AUX mem manager)
 + C compiler (Stack Frame, MATH API, AUX mem manager)
 + Disk II format (LIBBLKDEV)
 + Simple compression API (LIBPAK)
 + CSH+LIBPACK -> A2osX Installer
 + TCPIP+SSC DRV+LIBBLKDEV -> ADT Client
 + /etc/passwd (LIBCRYPT)

I need :
 + someone able to handle project management so i can focus on code writing
 + developers interested in one of these subjects above
 + someone able to build a test plan
 + ....ideas...help....support....beer, or something stronger! 

## News 2018-05-29

Time to work on STDIO : 

 + Buffered IO to link TCP/IP stream sockets properly to STDIN,STDOUT,STDERR (TELNETD)
 + Implement missing STDIO functions (Puts, FPuts...)
 + Faster Console output
 + Better 'C-Like' API

Scope : KERNEL.STDIO, All drivers, CDEV, FIFO,...

Goal : TELNETD & HTTPD working.

Wanna play ? 

## News 2018-04-29

Kernel 0.9.1 is now preemptive. 

It defaults to cooperative mode ('P'olling mode). For this, no particular hardware needed (except 65c02 and 128k, of course!)

If you want to enable preemptive mode, all you need is a "tick" source to get 'V'BL or 'C'lock Mode.
(see below for supported hardware)

Then you must explicitly ENABLE it using KCONFIG utility. (see screenshot below)

You can monitor the kernel state on the 'SYS' screen (OA-1, or SHIFT-OA-1 on french keyboards) and look at the upper right corner, you should see a blincking 'P', 'V' or 'C', showing you the current kernel state..

If you enabled preemptive mode, you should see an additional blinking 'S', each time the kernel switch from one PS to another.

Reminder : 
 + (SHIFT)-OA-1 : Kernel SYS Screen
 + (SHIFT)-OA-2 : Console Screen (Shell...)
 + (SHIFT)-OA-3 : DHGR Screen (if loaded)

For now, only SBIN/BIN executables are "switcheable". 

Roadmap is as follow: 

 + Check all BIN/SBIN sources to make them preemptive compliant, most of them are NOT. 
 + Add a way to make LIB also interruptible and reentrant.
 + Add more supported hardware for system clock.
 + ...and  still hoping finding few contributors.... :-(

## News 2017-11-08

Kernel 0.9.1 stable enough to resume building.

 + KM.APPLETALK module not crashing anymore  
   (Undocummented AtInit function, had to go further in official ATINIT disassembly) 

 + Improved Command Line editing and history. 
   (SUPPR key is emulated with Ctrl-X using //e keyboard)

 + New DevMgr enumeration strategy, now including /RAM and other virtual Block Devices 
 
 + Math API (Hacked from APPLESOFT ROM ;-)

 + CSH Script engine within Shell (In progress)
 
## News 2017-09-22

(once Kernel 0.9.1 stable enough, BOOT & DEV will be updated) __(done!)__

**0.9 has been archived, next Kernel Version is 0.9.1**  
   
 + More Standard C API compliance __(done!)__
 + API Cleanup, many functions still use shared space __(done!)__
 + Per process Stack Segment __(done!)__
 + Larger S.PS structure __(done!)__
 + ...
 + to allow...Preemptive!


**"System Tick" sources for preemptive mode :**

| Hardware                 | Resolution | Status      | Comment |
| -------------------------| ---------- | ----------- | ------- |
| //c,//c+,IIgs Mouse port | 50/60 Hz   | Working     | Supported at Kernel level, no conflict with GUI's Mouse.DRV (not required to be loaded), requires setting "Machine Timing" properly in KConfig Utility |
| IIe Mouse Card           | 50/60 Hz   | Working     | (same as above) |
| ThunderClock Plus        | 64 Hz      | Working     | gave up fixing this faulty H/W, thanx to JACE emulator! |
| Super Serial Card |      ?      | Idea, from EtchedPixels | #31 |
| MockingBoard     |      ?      | Idea, from Michael |  |
| GOES Irq Card  |      ?      | Idea, from Oliver | #34 |
| ... Any Other suggestion ?     |            |             |  |

## !!!HELP NEEDED!!!

Thanx a lot for all positive comments i read here and there, but i definitively need contributors & testers.

Anybody wants to join this project ?

If you're interested on contributing, please send a message with your skills and in which area you are interested to work on (Network, Kernel, device drivers for additional hardware support, GUI, graphical resourses, command line tools....)

This is some sort of "last hope call", some of you were right, this project is really huge!!! 
Anyway, i'm convinced that a small team of developers could reach "version 1.0" with GUI & network support in few months....i'm working on it for...4 years now, spending the most of my free time fixing hardware to test this code instead of...writing it! 

Well, let me know if you can bring "fresh blood" to this stuff... 

## Requires :
Enhanced IIe (65c02 cpu) with 128k, //c, IIgs

## Introduction...
A2osX is a cooperative, event-driven multitasking kernel (meaning it is applications that are responsible to give back control to kernel)
Its principal goal is to collect all "genius" 65c02 pieces of code ever written here and there, concentrated in the same environment.
(including IP Stack & HTTPD/TELNETD..., GUI & graphical tools...)
"Complete working place", no needing any more to reboot to switch between tons of diskettes!!!

A2osX is designed to work on any "stock" 128k Apple //e, with no additional hardware. As VBL signal is NOT available as an IRQ on //e (it is on //c & IIgs)
it makes preemptive multitasking impossible.

__A new attempt using Mouse card VBL IRQ is targeted in 0.9.1.__

Kernel, loading in Aux LC on top of ProDOS provide API inspired from Linux/Unix World to allow writing applications & command line tools on top of it.
This kernel provides an advanced "Memory Manager" able to relocate 65c02 code.
"Event Manager" makes TCPIP stack able to listen on several ports, manage ARP,DNS...cache expiration and any background processes.
"Task Manager" is responsible to "distribute" CPU time to several loaded processes.
"Device Manager" handles event collected from builtin devices as well as devices added by loadable drivers.

If you're 65c02 or Z80 code writer, how to contribute ?

Several subprojects are now indentified :

+ Hardware Support : adding drivers to support more & more hardware (RAM cards, storage....)
+ Z80 support : Kernel could pass control to any Z80 detected on the system.
+ TCP/IP stack
+ AppleTalk Support
+ GUI & Printing
+ Archive, Disk Image transfer tools (ADT client!)...
+ Question : Pascal or C Compiler? 
+ --> Answer : C compiler....Next version of Kernel API will be closer to STDLIBC, Genralize the use of C-Strings
+ ...sure there is some more!

## Screenshots

UNIX-Like Shell...

![](./.screen-shots/ScreenShot.LS.png)

TCP/IP Stack...

![](./.screen-shots/ScreenShot.IP1.png)

![](./.screen-shots/ScreenShot.IP2.png)

Full screen editor ...

![](./.screen-shots/ScreenShot.EDIT.png)

Kernel Configuration Utility...

![](./.screen-shots/ScreenShot.KCONFIG.png)

Color ANSI/VT100 Support...

![](./.screen-shots/PuTTY.png)

DHGR Mixed-Mode Graphic primitives....

![](./.screen-shots/ScreenShot.GFX.png)

## General Information:

Kernel API is confined in Aux LC Bank 1 & 2 to leave enough room at $EOOO for Drivers.
Network drivers, Mouse, DHGR.DRV can load and fit in Aux LC.
Now it's time to make all external BINs use new API, then GUI development will resume.

OApple+1,OApple+2,OApple+3 to switch between screens : Kernel Log, text, DHGR.
(OApple+shift+1,OApple+shift+2,OApple+shift+3 on FR keyboard)

## SYS/KM* Supported Hardware At Kernel Level (ProDOS):

| KM.Name      | Status  | Comment |
| -------      | ------  | ------- |
| KM.NSC       | Working | No-Slot-Clock/DS1216E |
| KM.RAMWORKS  | Working | AE-Ramworks I,II,III  |
| KM.VSDRIVE   | Working | ADTPro Virtual Drive for SSC |
| KM.APPLETALK | Working | AppleTalk Support for ProDOS |

## SBIN,Daemons/Commands:

| Name    | Status      | Comment | K.Ver |
| ----    | ------      | ------- | ------|
| INSDRV  | Working     |         | 0.92 |
| GETTY   | Working     | -E : Exit on remote close | 0.92 |
| LOGIN   | In Progress | no auth using /etc/passwd yet | 0.92 |
| SHELL   | Working     | (See Internal Shell commands) | 0.92 |
| KCONFIG | Working     | Kernel Configuration Utility | 0.92 |
| ----    | ------      | ------- | ----- |
| TCPIPD  | Working     | ARP,IP,ICMP,UDP & TCP ok | 0.92 |
| DHCPCLNT| Working     | rewritten to use new Socket API | 0.92 |
| TELNETD | Working  |  | 0.92 |
| HTTPD   | In Progress |  | 0.9 |

## Internal Shell commands:

| Name      | Status  | Comment |
| ----      | ------  | ------- |
| CD        | Working | Improved syntax : now, 'CD ../BIN' works |
| REN       | Working | Rename a file, directory or volume |
| MD        | Working | Create a directory |
| RD        | Working | Delete an empty directory |
| PWD       | Working | Print Working Directory |
| DATE      | Working | |
| ECHO      | Working | \b,\e,\f,\n,\\\ and \\% supported |
|           |         | -N : Suppress \r\n |
| EXIT      | Working | exit shell |
| PAUSE     | Working | Wait until CR |
| PUSHD     | Working | Save actual working directory |
|           |         | PUSHD <dir> do aslo a CD to <dir> |
| POPD      | Working | Restore previously saved working directory |
| READ      | Working | -S : no echo (password) |
|           |         | -P : "prompt message"   |
| TIME      | Working | |
| SET       | Working | -X toggle debug mode |
| SLEEP     | Working | Wait <count> 10th sec |
| STARTPROC | Working | Used in A2osX.startup |
| SHIFT     | Working | Remove $1 from cmd line |
| ----      | ------  | ------- |
| IF .. ELSE .. FI | Working | [ -d direxists ] |
|           |         | [ -e fileordirexists ] |
|           |         | [ -f fileexists ] |
|           |         | [ string1 = string2 ] |
|           |         | [ string1 != string2 ] |
|           |         | [ int32 -eq int32 ] |
|           |         | [ int32 -ne int32 ] |
|           |         | [ int32 -lt int32 ] |
|           |         | [ int32 -le int32 ] |
|           |         | [ int32 -gt int32 ] |
|           |         | [ int32 -ge int32 ] |
| WHILE .. LOOP | Working | [ same tests as IF ] |
| BREAK      |  | |
| CONTINUE   |  | |

## Shell variables:

| Name  | Status  | Comment |
| ----  | ------  | ------- |
| $0    | Working | Command Full Path |
| $1-$9 | Working | Arg[n] |
| $*    | Working | All Args |
| $#    | Working | Arg Count |
| $?    | Working | Return Code |
| $@    | Working | Parent PID |
| $$    | Working | PID |
| $!    | Working | Child PID |
| $UID  | Working | PS Owner UID |
| $PWD  | Working | Working Directory |

note : '$VAR' does NOT expand Variable

## Shell I/O control/redirection:

| Token  | Status  | Comment |
| ----  | ------  | ------- |
| . | Working | use same env |
| & | Working | start proc |
| \| |  | pipe |
| <    | Working | StdIn redirection |
| >>    | Working | StdOut redirection |
| >    | Working |  |
| 1>>    | Working |  |
| 1>   | Working |  |
| 2>>    | Working | StdErr redirection |
| 2>     | Working |  |

## DRV,Drivers:

| Name | Status | Comment | K.Ver |
| ---- | ------ | ------- | ----- |
| Console.DRV | Working | ANSI support in Progress. | 0.92 |
| SSC.DRV     | Working | Apple "Super Serial Card" Driver | 0.92 |
| SSC.I.DRV   | Working | Apple "Super Serial Card" Driver (IRQ enabled) | 0.92 |
| PIC.DRV | In Progress | Apple "Parallel Interface Card" Driver, renamed from PPIC.DRV | 0.9 |
| Mouse.DRV | Working | Apple Mouse Card,//c Mouse Port | 0.9.1 |
| DHGR.DRV | Working | 560x192 Mono/16 colors Mixed-Mode support | 0.9.1 |
| ---- | ------ | ------- | ----- |
| LanCeGS.DRV | Working | | 0.92 |
| Uthernet.DRV  | Working | | 0.92 |
| Uthernet2.DRV | Working | | 0.92 |
| Uther2.AI.DRV | In Progress | With ARP/IP Offloading | 0.92 |

## BIN,External Shell commands:
| Name | Status | Comment | K.Ver |
| ---- | ------ | ------- | ----- |
| MEM | Working | Old dump behavior is now MEMDUMP.  New MEM command displays MEMSTAT (Main, Aux & Kernel Memory) | 0.92 |
| LSDEV | Working | Dump device Drivers | 0.92 |
| LSOF | Working | List Open Files | 0.92 |
| PS | Working | List Processes| 0.92 |
| MKDIR | Working | Make Directory| 0.92 |
| LS | Working | -A : Do Not Print . & .. | 0.92 |
| | | -L : long listing with size/date... | |
| | | -R : Recurse subdirectories | |
| RM | Working | -C : Continue On Error | 0.92 |
| | | -Q : Quiet | |
| | | -R : Recurse subdirectories | |
| CP | Working | -C : Continue On Error | 0.92 |
| | | -Q : Quiet | |
| | | -R : Recurse subdirectories | |
| | | -Y : Dont't Prompt For Override | |
| MV | Working | -C : Continue On Error | 0.92 |
| | | -Q : Quiet | |
| | | -R : Recurse subdirectories | |
| | | -Y : Dont't Prompt For Override | |
| CAT | Working | -A : Show All non printable caracters | 0.92 |
| | | -N : Number all output lines | |
| | | -S : Suppress repeated empty output lines | |
| EDIT | Working | still missing : find/replace | 0.92 |
| KILL | Working | KILL <signal> PID | 0.92 |
| FORMAT | In Progress | -L : Low-Level Format | 0.92 |
| | | -1..9 : Catalog Size (block count) | |
| CHTYP | Working | -C : Continue On Error | 0.92 |
| | | -R : Recurse subdirectories | |
| MD5 | Working | -D : String Input | 0.92 |
| CHMOD | In Progress | -C : Continue On Error | 0.9 |
| | | -R : Recurse subdirectories | |
| CHOWN | In Progress | -C : Continue On Error | 0.9 |
| | | -R : Recurse subdirectories | |
| CHGRP | In Progress | -C : Continue On Error | 0.9 |
| | | -R : Recurse subdirectories | |
| NSCUTIL | Working | Tool for setting time in NSC/DL1216E | 0.92 |

## Network (TCPIP) tools:
| Name | Status | Comment | K.Ver |
| ---- | ------ | ------- | ----- |
| IPCONFIG | Working | renamed from NETINFO | 0.92 |
| NETSTAT | Working | | 0.92 |
| ARP | Working | dump ARP cache, setup a static ARP entry | 0.92 |
| DNSINFO | Working | dump DNS cache, setup a static DNS entry | 0.92 |
| PING | Working | -1..9 : Ping Count | 0.92 |
| TELNET | Working | | 0.92 |

## DEV tools:
| Name | Status | Comment | K.Ver |
| ---- | ------ | ------- | ----- |
| MEMDUMP | Working | Tool to track memory leak| 0.92 |
| ASM | In Progress | S-C MASM based multi CPU assembler | 0.9.1 |
| ---- | ------ | ------- | ----- |
| RPCDUMP | In Progress | tool based on UDP socket API, renamed from RPCINFO | 0.92 |

## Misc

### S-C MASM color scheme for Notepad++
...drop _Tools/userDefineLang.xml in %APPDATA%\Notepad++
;-)

