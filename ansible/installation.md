Install ansible simple 
```bash
apt-get install ansible
```

To install it from a repo
```bash
apt-add-repository ppa:ansible/ansible
apt-get update #update the repository cache
echo y | apt-get install ansible
```
Copy /etc/ansible to a local directory
```
cp -R /etc/ansible myfolder
```
edit the ansible.conf and make sure the inventory is pointing to the local folder
```
vi ansible.cfg
```
inventory      = hosts

Clear everything from the hosts file - there are only comments on these
```
> hosts
```
Write down the names of the servers in the hosts file - Can also specify the ip addresses
```
ansible1
ansible2
spnginx
```
make sure you run the following command on all the machines
```
sudo apt install python-minimal python-simplejson
```
run the following command to check if everything works fine
```
ansible -m ping all
```