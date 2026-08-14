# SSH server & host configuration

* For defining ssh access to machines, use the config file (use as a template).
* For define hosts (as a private and local DNS), use the hosts file (as a template).

## HOST
### Generate ssh key
1. Windows
* Open Putty Key Generator (PuTTYgen)
* Create and save the public and private key
* To use it, browse the private key file PuTTY > SSH > Auth
2. Ubuntu

````bash
ssh-keygen -t rsa
#interactive process
````

## SERVER
To see the current configuration of the server, use `sshd -T`
### Add authorized key
Add the public key (id_rsa.pub) yo the /.ssh/authorized_keys.
In windows, the PuTTYgen provides the required text to append to the server authorized_keys file.

````bash
mkdir -p /home/user_name/.ssh && touch /home/user_name/.ssh/authorized_keys

#Then add the public key with the editor:
nano ~/.ssh/authorized_keys
#Or use this:
cat id_rsa.pub or txt >> ~/.ssh/authorized_keys

#Set the appropriate permission to the file:
chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys
chown -R username:username /home/username/.ssh
````
### Disable password authentication
Is very usefull to disable the password authentication, only allowing key access.
````bash
sudo nano /etc/ssh/sshd_config
#Find for PasswordAuthentication, set to no
#Then restart the ssh service:
sudo service ssh restart
````

## Logs
The file `/var/log/auth.log` contains all the ssh environment log messages.(`tail -f /var/log/auth.log`)
