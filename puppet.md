Install puppet master
https://medium.com/@Alibaba_Cloud/how-to-install-puppet-master-and-client-on-ubuntu-16-04-9f8c241125df
https://help.ubuntu.com/lts/serverguide/puppet.html.en - worked for puppet master
change hostname
```
# edit /etc/hostname
add the name and reboot machine
# can be done on all the machines
```

setup a fake dns
```
# edit the file /etc/hosts
# go to the end line and type in the following
# ifconfig to find the ipaddress
#ipaddress hostname.local hostname
ex - 192.168.1.23 puppet-master.local puppet-master
# do this on all the machines
```

Install puppet server
```
# requires atleast 2 core 3gi ram
curl -O https://apt.puppetlabs.com/puppetlabs-release-pc1-xenial.deb
dpkg -i puppetlabs-release-pc1-xenial.deb
apt-get update -y
apt-get install puppetserver -y
```
Configure memory allocation 
```
vi /etc/default/puppetserver
# change JAVA_ARGS="-Xms3g -Xmx 3g ... 3g = 3 gigs
```
Make sure the unconfigured firewall allows puppet
```
ufw allow 8140
```
start puppet server and enable at boot time
```
systemctl start puppetserver
systemctl enable puppetserver
```



### client setup
```
# same fake dns setup
curl -O https://apt.puppetlabs.com/puppetlabs-release-pc1-xenial.deb
dpkg -i puppetlabs-release-pc1-xenial.deb
apt-get update -y
apt-get install puppet-agent -y
systemctl start puppet
systemctl enable puppet
```
copy the fake dns on both the machines

Certificate signing request
```
cd /opt/puppetlabs/puppet/bin
./puppet agent -t --server=puppet-master.local
# go to the server and check the certificate to be signed
/opt/puppetlabs/bin/puppet cert list --all 
# the cert without the + sign is not signed
# sign the request
puppet cert sign <name of the cert request > # ex - puppet-client.local
# if you run puppet agent again on the client it should pull in the catalog
```
