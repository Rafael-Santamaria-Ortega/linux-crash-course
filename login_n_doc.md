# Notes on Login and System Documentation in Linux

There are various ways to login in Linux: 
1. Local text-mode console
2. Remote text-mode console
3. Local graphical-mode console
4. Remote graphical-mode console

**Important concepts:**
- Console: Screen where OS displys text and user can input commands
- Terminal Emulator: graphical app that runs in a window and does a similar thing.
- Virtual Terminal: ctrl+alt+F2

This concepts come from the old days of computing, as computers were expensive, companies only bought a single one for everyone. Nevertheless, multiple people could connect to it through different devices and use it, even at the same time.Those devices were *consoles* and *terminals*. Nowadays, they are software, instead of software. 

In CLI you open a virtual terminal; whereas in GUI, you open a terminal emulator to login and type commands. In practice, it's very usual to login in to remote Linux systems, instead of local ones (*Local GUI systems:* something you can physically acces, like a computer in my desk). A server running on Google Cloud is remote, usally when Linux is installed in such servers it doesn't have a GUI but a CLI. However, sometimes you would get GUI's. This makes it very easy to login (don't forget to log out!). If there is a server oriented Linux OS in the device with no GUI, login is also easy too as you can simply type username and password. When done, type exit to log out. 

Most of the time Linux will have no GUI's on servers, however, when remote OS have GUI, login is trickier as there is no standard. It could be VNC (virtual network computing), which will imply downloading the proper client to access. RDP (remote desktop protocol) is another possibility, where you click start in windows, type "remote desktop connection" and open that, enter username and password. It all boils down to having the correct app and credentials.

**Initiating a text based remote connection:** pretty standard, because almost every Linux system uses same tool for remote logins: Open SSH (Secure Shell) daemon, that runs in the background all the time with encryption. Replaced unencrypted insecure Telnet connections. SSH client connects to SSH server. To use ssh, type ssh user@xxx.xxx.xxx.xx and then it will ask for password. 

## Read and use commands in Linux

Linux has many commands, if you need to read documentation on it use "command --help" for shorter, simple commands. 

**Useful commands:** 
- ls: display dir
- ls -l: diplay many facts of files and dirs such as permissions
- --help
- joournalctl: queries a journal
- q: leave long documents
- man: Gives full manual description of commands
- man man: you can use the categories to distinguish between equally named commands and functions, etc.
- apropos: search for commands without using names (sections 1-8 commands) -> apropos -s 1,8 director
- mkdir: create directories 
