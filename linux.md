 
 proc
 - to check cpu info check /proc/cpuinfo
 - proc also has information about the processes running 
 
Pipe
- used to output the output to next command

Shell
- use chmod 755 to add executable permission to a shell file

Change the order of boot in multi boot
- change the order in /boot/grub/grub.cfg and run 
```
update-grub
```

always run the following to keep the system and the distribution of OS upto date
```
sudo apt-get update 
sudo apt-get dist-upgrade
```
remove package
```
sudo apt-get purge <packagename>
```
