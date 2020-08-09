# Toolbox

>My mission is to create a list of "goto's" for myself when I do CTF's, Incident Response, or other CyberSecurity based activities.

[Ports](#ports)

[Port Scanners](#port-scanners)

[SMB Stuff](#smb-stuff)

[Linux Goodies](#linux-goodies)

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

### enumerate target Windows system with rpcclient
`rpcclient 172.30.0.22 -U <username>`

### rpcclient prompt once logged in
`rpcclient $>`

> All commands after this line will be from the `rpcclient $>` prompt, if you don't see that prompt don't progress

### rpcclient help, type at rpcclient prompt, you will hit tab twice
`enum<tabtab>`

### enumerating users on domain
`enumdomusers`

### help also prints off a bunch of commands you can use
`help`

### enumerate service info
`srvinfo`

### enumerate information about password policies
`getdompwinfo`

#### enumerate information about user password policies
`getusrdompwinfo <RID>`


___

## Linux Goodies! 

### create a copy of /bin/sh shell to the tmp directory and call it backdoor

`cp /bin/sh /tmp/backdoor`

### want this file to execute as root so chmod it

`chmod 4111 /tmp/backdoor`

### file should be red and look at the permissions they will have the SUID bit set

`ls -l backdoor`

### /bin/sh binary attempts to stop people from gaining root access from a SETUID binary; override this setting by adding a -p option

`./backdoor -p`

### find look for SUID root files on the system in the tmp directory by running this

`find /tmp -uid 0 -perm -4000 -print`

### find other SUID root files on the system 

`find /bin -uid 0 -perm -4000 -print`

### create a newwork listening process and unlink the executable associated with it

`cp /bin/nc /tmp/nc`

### delete a user account

`userdel -rf <UserAccountName>`

### check to see if you deleted said account (UID 0 because if we are adding accounts they are root, baby ;) )

`grep :0: /etc/passwd`

#### Make Linux's network card go into promiscuous mode (on/off switch)

`ip link seet eth0 promisc on`

#### Check log entries that indicates that the interface went into promiscuous mode

`dmesg | grep promisc`
