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
create a playbook at the root level of the ansible folder
```
cat << EOF > playbook.yml
- hosts: all
  become: true #become another user
  roles: 
  - basic
EOF
```

Run ansible playbook
```
ansible-playbook -K playbook.yml
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
Run shell command
creates will make sure that the command wont run if the file exists
```
- name: "move files by runnig shell commands"
  shell: creates=/home/spothi/test1.txt mv /home/spothi/test.txt /home/spothi/test1.txt
```
