to run shell commands on a machine
```
ansible -m shell -a 'hostname' all
```
hostname is the command here, all represents all the machines, -m is the module used, in this case it is shell

to know the disk space on all the machines
```
ansible -m shell -a 'df -h' all
```

Add a user with root permissions
```
ansible -b -K -m user -a 'name=testuser' all # -K makes it ask for the sudo password
#ansible will ask for the sudo password
# to check the user, ssh into the server and type the following command
getent passwd | grep testuser

```

You can also use ansible to do the same
```
ansible -m shell -a 'getent passwd | grep testuser' all
```

Remove user from all the machines
```
ansible -b -K -m user -a 'name=testuser state=absent' all
```
