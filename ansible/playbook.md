To create a new roles cd into the roles directory and make a directory and inside that create a directory called tasks
and cd into directory make a file called main.yml
```
cd roles  
mkdir simple
cd simple
mkdir tasks
cd tasks
cat <<EOF>main.yml
- name: "Install vim" # discriptive name useful for debuggin
  apt: pkg=vim state=present # name of the package to be installed and the state
EOF
```

Create a playbook
```
cat << EOF > site.yml
- hosts: all
  become: true #become another user
  roles: 
  - basic
EOF
```
create a playbook and run as root user
```
cat << EOF > site.yml
- name: playbook for group1
  hosts: group1
  user: root
  sudo: true
  roles: 
  - basic
EOF
```
Run ansible playbook
```
ansible-playbook -K site.yml

# if the ansible.conf has not been updated to point the inventry to the hosts file use the following command
ansible-playbook -i hosts -K site.yml
# -K is for the sudo password
```

Install multiple packages in the same task
```
- name: "Install vim" # discriptive name useful for debuggin
  apt: pkg=vim state=present # name of the package to be installed and the state
- name: "Installting DNS utils"
  apt: pkg=dnsutils state=present
- name: "Installing git"
  apt: pkg=git state=present
```
Or
```
- name: Install a list of packages
  apt:
    name: "{{ packages }}"
  vars:
    packages:
    - dnsutils
    - git
    - vim
```

Copying files, make sure that the files directory is created at the same task level
```
- name: "Adding files"
  copy: src=../files/test.txt dest=/tmp/text.txt owner=spothi group=root mode=0644
```
a better way to copy file is to use a jinja2 template. this allows variable substitution
```
- name: "Update nginx config"
  template: src=../files/nginx.conf.j2 dest=/etc/nginx/nginx.conf
```
Run shell command
creates will make sure that the command wont run if the file exists
```
- name: "move files by runnig shell commands"
  shell: creates=/home/spothi/test1.txt mv /home/spothi/test.txt /home/spothi/test1.txt
```
apt get update
```
- name: Only run "update_cache=yes" if the last one is more than 3600 seconds ago
  apt:
    update_cache: yes
    cache_valid_time: 3600
```

Using variables
```
- hosts: group1
  vars: 
    test_var: Test value
  template: src=../files/{{ test_var }} dest=/tmp/{{ test_var }}
```

using dependencies
create a meta/main.yml in the roles folders and define the dependencies of the roles there
```
dependencies:
  - basic
  - nginx
```
This reduces the playbook to only have a specific role like say webserver and all the dependencies are installed automatically
