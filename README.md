# SecurityTests
Tests made to secure my linux box and learn about logs, tool and information about preventing bruceforcing


## BruteforceSSH.js
Normally a SSH bruteforce attack can be seen in /var/log/auth.log, unless a attack was succesful and the attacker have removed or partially sanitized the auth.log. 

Update: There is several places SSH keeps logs about user/root logins. It is possible to see information about logins by using the command: last

A attacker trying to bruteforce into ssh (This is a real attack on a machine):

        Mar 29 17:57:52 YourMachineName sshd[2563]: PAM 2 more authentication failures; logname= uid=0 euid=0 tty=ssh ruser= rhost=221.229.166.245  user=root
        Mar 29 17:57:53 YourMachineName sshd[2575]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=43.255.191.169  user=root
        Mar 29 17:57:54 YourMachineName sshd[2577]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=103.41.124.165  user=root
        Mar 29 17:57:55 YourMachineName sshd[2575]: Failed password for root from 43.255.191.169 port 53154 ssh2
        Mar 29 17:57:56 YourMachineName sshd[2577]: Failed password for root from 103.41.124.165 port 56158 ssh2
        Mar 29 17:57:58 YourMachineName sshd[2575]: message repeated 2 times: [ Failed password for root from 43.255.191.169 port 53154 ssh2]
        Mar 29 17:57:58 YourMachineName sshd[2575]: Received disconnect from 43.255.191.169: 11:  [preauth]
        Mar 29 17:57:58 YourMachineName sshd[2575]: PAM 2 more authentication failures; logname= uid=0 euid=0 tty=ssh ruser= rhost=43.255.191.169  user=root
        << Above message repeats for a million times >>
  

How /var/log/auth.log shows how my script is trying to replicate a real attack:

        Mar 30 00:12:18 MyTestMachine sshd[2346]: Failed password for root from 85.10.169.109 port 38991 ssh2
        Mar 30 00:12:19 MyTestMachine sshd[2346]: Connection closed by 85.10.169.109 [preauth]
        Mar 30 00:12:19 MyTestMachine sshd[2356]: reverse mapping checking getaddrinfo for 85.10.169.109.sydfynsnet.dk [85.10.169.109] failed - POSSIBLE BREAK-IN ATTEMPT!
        Mar 30 00:12:19 MyTestMachine sshd[2356]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=85.10.169.109  user=root
        Mar 30 00:12:21 MyTestMachine sshd[2356]: Failed password for root from 85.10.169.109 port 34227 ssh2
        Mar 30 00:12:21 MyTestMachine sshd[2356]: Connection closed by 85.10.169.109 [preauth]
        Mar 30 00:12:22 MyTestMachine sshd[2377]: reverse mapping checking getaddrinfo for 85.10.169.109.sydfynsnet.dk [85.10.169.109] failed - POSSIBLE BREAK-IN ATTEMPT!
        Mar 30 00:12:22 MyTestMachine sshd[2377]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=85.10.169.109 user=root
