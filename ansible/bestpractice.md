Use a project structure as below
```
site.yml - playbook
hosts - list of hosts
roles
  group
  - tasks -> list of tasks to perform in a group
  - handlers -> very simple tasks, like starting a service
    ex -
    - name: Restart nginx
      service: name=nginx state=restarted
  - templates -> jinja2 files
  - files -> files to copy
  - meta -> dependencies on other roles
group_vars -> all.yml (file with list of variables) 
ex - 
port: 2030
hostname: test
```


Place arguments in multiple lines
```
- name: Add user details
  user: >
    name={{ user_name }}
    password={{ user_pass }}
    shell=/bin/bash
    groups=sudo
    append=yes
    generate_ssh_keys=yes
    ssh_key_bits=2048
    state=present
```
