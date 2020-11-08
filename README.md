# Install_OpenSSH_on_Windows

## 1. On server side 

Got to next link and download the latest version

```
https://www.mls-software.com/opensshd.html
```

Install the application in C:\Program Files\OpenSSH changing the generated password with your one.

Go to C:\Program Files\OpenSSH\etc, Open the file 'sshd_config' with notepad and edit and uncomment next line:

```
StrictModes no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

If the service sshd did not started automaticaly reboot the windows machine or go to C:\Program Files\OpenSSH\usr\sbin\ and execute 'sshd.exe' file

If you have connection problems, in windows cmd exectue following command to open the firewall for sshd.exe to allow inbound SSH connections

```
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

```
Note: New-NetFirewallRule is for Windows 2012 and above servers only. If you're on a client desktop machine (like Windows 10) or Windows 2008 R2 and below, try:

```
netsh advfirewall firewall add rule name=sshd dir=in action=allow protocol=TCP localport=22
```

## 2. On client side

Copy your ssh key from .ssh/

ssh to the windows machine using password

Generate a ssh-key on the server

```
  ssh-keygen
```
  
Go to .ssh/ and create a file called authorized_keys with your key inside

```
  echo 'your-ssh-key' > authorized_keys
```

### If you want to ssh from here to other machines you need to set your **private** key permissions to 600 using:

```
chmod 600 .ssh/id_rsa
```
