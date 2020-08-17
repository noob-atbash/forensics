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
**Listing all the running process:**
```
$ volatility -f filename --profile=Win7SP1x64 pstree
```
> One way we can analyze .exe file is by runing them in [Virustotal](https://www.virustotal.com/gui/home/upload).

### WRITEUPS

- [LOGarithm](https://github.com/5h3r10ck/CTF_Writeups/tree/master/InCTF)
- [Investigation](https://blog.bi0s.in/2020/08/04/Forensics/Investigation-InCTFi2020/)
- [sh*tty ransomware](https://aresx.carrd.co/#ransom)