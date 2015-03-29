# SecurityTests
Tests made to secure my linux box and learn about logs, tool and information about preventing bruceforcing


## BruteForceSSH.js
Normally a SSH bruteforce attack can be seen in /var/log/auth.log, unless a attack was succesful and the attacker have removed or partially sanitized the auth.log. 

A attacker trying to bruteforce into ssh:

        Mar 29 17:57:52 YourMachineName sshd[2563]: PAM 2 more authentication failures; logname= uid=0 euid=0 tty=ssh ruser= rhost=221.229.166.245  user=root
        Mar 29 17:57:53 YourMachineName sshd[2575]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=43.255.191.169  user=root
        Mar 29 17:57:54 YourMachineName sshd[2577]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=103.41.124.165  user=root
        Mar 29 17:57:55 YourMachineName sshd[2575]: Failed password for root from 43.255.191.169 port 53154 ssh2
        Mar 29 17:57:56 YourMachineName sshd[2577]: Failed password for root from 103.41.124.165 port 56158 ssh2
        Mar 29 17:57:58 YourMachineName sshd[2575]: message repeated 2 times: [ Failed password for root from 43.255.191.169 port 53154 ssh2]
        Mar 29 17:57:58 YourMachineName sshd[2575]: Received disconnect from 43.255.191.169: 11:  [preauth]
        Mar 29 17:57:58 YourMachineName sshd[2575]: PAM 2 more authentication failures; logname= uid=0 euid=0 tty=ssh ruser= rhost=43.255.191.169  user=root
        << Above message repeats for a million times >>
  


