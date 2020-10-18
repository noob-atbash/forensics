---
layout: default
---

## Resources
- [Tools](https://ericzimmerman.github.io/#!index.md)
- [windows-forensic-analysis](http://what-when-how.com/windows-forensic-analysis/)

## TOOLS 

>Don't forget to checkout the ```strings``` 

### 1. Volatility 
>The Volatility Framework is a completely open collection of tools,
implemented in Python under the GNU General Public License, for the
extraction of digital artifacts from volatile memory (RAM) samples.
The extraction techniques are performed completely independent of the
system being investigated but offer visibilty into the runtime state
of the system. The framework is intended to introduce people to the
techniques and complexities associated with extracting digital artifacts
from volatile memory samples and provide a platform for further work into
this exciting area of research
- [Github](https://github.com/volatilityfoundation/volatility) 

```bash
apt-get install volatility

```

- [command-refrence](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference)

**Detecting the OS:**

```
$ volatility -f filename  imageinfo 

```

```bash
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x64 , WinXPSP3x86 (Instantiated with Win7SP1x64 )
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/panardin/Challs/cridex.vmem)
                      PAE type : PAE
                           DTB : 0x2fe000L
                          KDBG : 0x80545ae0L
          Number of Processors : 1
     Image Type (Service Pack) : 3
                KPCR for CPU 0 : 0xffdff000L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2012-07-22 02:45:08 UTC+0000
     Image local date and time : 2012-07-21 22:45:08 -0400

```
>Once we have the computer OS from which this memory dump comes from (Win7SP1x64). The investigation can now begin, we can specify to volatility the OS profile (--profile=Win7SP1x64)


**CHEATSHEETS**

```bash
$ volatility -f filename --profile=Win7SP1x64 pslist #see running processes using the pslist plugin
$ volatility -f filename --profile=Win7SP1x64 pstree  # to display the processes and their parent processes
$ volatility -f foren.raw --profile=WinXPSP2x86 psxview # psxview will list processes that are trying to hide themselves while running on the computer, this plugin can be really useful

```

```bash
$ volatility -f foren.raw  --profile=Win7SP0x64  hivelist  #to see the available hivelist
$ volatility -f foren.raw --profile=Win7SP1x64 hashdump #all poosible pass hashes 
$ volatility -f cridex.vmem --profile=WinXPSP2x86 cmdline #to look at the last commands ran, by using cmdscan, consoles and cmdline 
$ volatility -f mem.raw --profile=Win10x64_15063 procdump -D . -p 5448 #dump files using pid 
$ volatility -f foren.raw  --profile=Win7SP0x64  memdump -p 1044 --dump-dir=dirname #dump files using pid 
$ $ volatility -f cridex.vmem --profile=WinXPSP2x86 connscan # to check  running sockets and open connections on the computer

```
>Don't forget to use the combination of **strings** and **grep**.  

> One way we can analyze .exe file is by runing them in [Virustotal](https://www.virustotal.com/gui/home/upload).

### WRITEUPS TO START WITH 

- [LOGarithm](https://github.com/5h3r10ck/CTF_Writeups/tree/master/InCTF)
- [Investigation](https://blog.bi0s.in/2020/08/04/Forensics/Investigation-InCTFi2020/)
- [sh*tty ransomware](https://aresx.carrd.co/#ransom)



### 2.RegRipper 

> RegRipper is an open source tool, written in Perl, for extracting/parsing information (keys, values, data) from the Registry and presenting it for analysis.

[Installation](https://raw.githubusercontent.com/siftgrab/siftgrab/master/regripper.conf/RegRipper30-apt-git-Install.sh)


### 3.Prefetch.py / PECmd


>Prefetch files are great artifacts for forensic investigators trying to analyze applications that have been run on a system. Windows creates a prefetch file when an application is run from a particular location for the very first time. This is used to help speed up the loading of applications. For investigators, these files contain some valuable data on a user’s application history on a computer.

[PECmd](https://github.com/EricZimmerman/PECmd)

```bash
PECmd.exe -d "C:\location\to\prefetch" --csv .

```
[Prefetch.py](https://github.com/PoorBillionaire/Windows-Prefetch-Parser/blob/master/windowsprefetch/prefetch.py)


```py
python3 prefetch.py -f filename.EXE filename.pf
```

### WRITEUPS TO START WITH 

[Prefetch Perfection](https://ctftime.org/task/13433)
[Prefetch Perfection 2](https://ctftime.org/task/13434)