```
# lxc - linux container 
# install 
apt-get update && apt-get install lxc -y

# overview page
man lxc

# create a ubuntu environment
sudo lxc-create -t Ubuntu  -n bashy
or sudo lxc-create -t download -n u1 -- -d ubuntu -r bionic -a amd64


# list all the containers 
sudo lxc-ls --fancy

#start a container in daemon mode 
sudo lxc-start -n bashy -d

# do an ls to get the machine name 
# can just ssh into the machine
# default user and pass is ubuntu
https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart

# you can attach to a container shell 
lxc-attach -n bashy
passwd ubuntu
apt install openssh-server -y
apt-get install python-minimal --no-install-recommends -y
apt-get install sudo python-minimal python-setuptools

# create new user 
adduser username
usermod -aG sudo username

sudo lxc-ls --fancy
sudo lxc-start --name u1 --daemon
sudo lxc-info --name u1
sudo lxc-stop --name u1
sudo lxc-destroy --name u1

```
check what version of package is in the cache
```
apt-cache policy ansible
```
Install 
```
apt-get update
apt-get install software-properties-common -y
apt-add-repository ppa:ansible/ansible -y
apt-get update
apt-get install ansible -y
cp -r /etc/ansible ansible_workspace
```
### uncomment gather_timeout = 100 # if there are timeouts when logging in

make sure you add the ssh public id's to the root user (makes it easy for rest )

Use the playbook method to run as sudo
```
- hosts: all
  gather_facts: False # required for installing python 2
  remote_user: ubuntu
  become: yes # esclates the permission, become user will not do this
  become_user: root
  become_method: sudo

  tasks:
    - name: Install python 2
      raw: test -e /usr/bin/Python || (apt-get update && apt-get install -y python)

    - name: Copy authorized keys
      authorized_key: user=root
                       exclusive=no
                       key="{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
```
ansible-playbook prepare_ansible_server.yaml -i hosts1 -K -u ubuntu --ask-sudo-pass

NGINX
```
- hosts: all
  vars:
    site_name: "var1value"
    site_title: "var2value"
    site_url: "var3value"

  tasks:
    - name: Install nginx
      package: name=nginx state=latest

    - name: Create Website directory
      file: path="/var/www/{{ site_name }}" state=directory mode=0755

    - name: Create nginx config file
      template:
        src: "templates/nginx.conf"
        dest: "/etc/nginx/nginx.conf"
      notify:
      - restart nginx
    - name: Create vhost file
      template:
        src: "templates/website.conf"
        dest: "/etc/nginx/conf.d/ {{ site_name }}.conf"
      notify:
      - restart nginx
      - wait for sometime # wait handler 
  handlers:
    - name: restart nginx
      service:
        name: nginx
        state: restarted
   - name: wait for sometime
     wait_for: timeout=10
---
# templates website.conf
server {
        listen  80;
        server_name {{ site_url }}

        root  /var/www/{{ site_name }}

        location / {
            try_files /index.html
        }
}
---
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
        worker_connections 768;
}

http {

        sendfile on;
        tcp_nopush off;
        tcp_nodelay on;
        keepalive_timeout 65;
        types_hash_max_size 2048;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
        ssl_prefer_server_ciphers on;

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;
        gzip on;
        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}

```

run scripts locally, loop through items and check value of previous task
```
- hosts: 127.0.0.1 # run on the local host, still need to pass --connection=local
   become: no
   # USAGE: ansible-playbook create_playbook.yml --connection=local
   vars:
     playbook_name: ansibleskeleton
     location: /tmp/{{ playbook_name }}
     roles: ["web", "database", "common"]

   tasks:
     - name: Check if playbook already exists
       stat: path={{ location }}
       register: playbook_directory

     - name: Create playbook directory
       file: path={{ item }} state=directory
       when: playbook_directory.stat.exists == False
       with_items:
         - "{{ location }}"
         - "{{ location }}/group_vars"
         - "{{ location }}/roles"

     - name: Create playbook files
       file: path={{ item }} state=touch
       with_items:
         - "{{ location }}/group_vars/all"
         - "{{ location }}/{{ playbook_name }}.yml"
```
loop through dictionary, the value 
```
- name: copy tomcat config files
  template: src="{{ item.src }}" dest="{{ item.dest }}"
  with_items:
    - { src: 'context.xml.j2', dest: '/opt/tomcat/conf/context.xml'}
```
lineinfile - to replace a line in a file
refer to examples here
https://docs.ansible.com/ansible/latest/modules/lineinfile_module.html

lineinblock is to replace a blovk

get_url is to download the content to a file path


