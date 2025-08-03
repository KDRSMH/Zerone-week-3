# Hardening Metasploitable-2 
Hello. In this article, we will perform a hardening process on Metasploitable 2, which contains many security vulnerabilities.

- You can see the security vulnerabilities I found in my Nmap scan below.
  <img src="imagess/vulner.png" width="500" />

## FTP(21)
Let's start with FTP. FTP is a file transfer protocol used to transfer files between remote hosts. Metasploitable 2 runs vsftpd version 2.3.4, which is vulnerable to backdoor code execution. To fix this vulnerability, anonymous uploads must be disabled by setting anon_upload_enable=NO in the /etc/vsftpd.conf file. Additionally, since the backdoor is located on port 6200, traffic to port 6200 should be blocked, which can be done using the following iptables rules.

 <img src="imagess/ftpc.png" width="500" />

## Telnet,Rexec,Rlogin (23,512,513)
Telnet, Rexec, and Rlogin are remote access services. They allow users to execute commands and interact with remote hosts. Unfortunately, data is sent in plain text, which is dangerous because sensitive information such as passwords can be transmitted. Therefore, these services should be disabled. More secure alternatives such as SSH should be used, as they provide a level of encryption. Telnet, Rexec, and Rlogin can be disabled by going to /etc/inetd.conf and commenting out the telnet, shell, and login entries, respectively. 

 <img src="imagess/telnet.png" width="500" />
