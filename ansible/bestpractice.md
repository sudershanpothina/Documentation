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


Place arguments in multiple lines, the next segment is more prefered
```
- name: Add user details
  user: >
    name={{ user_name }}
    password={{ user_pass }}
    shell=/bin/bash
    groups=sudo
    append=yes # group would be added instead of replacing current groups
    generate_ssh_keys=yes
    ssh_key_bits=2048
    state=present
```

Copy contents of a file
```
- name: Copy contents of a cert
  authorized_key:
    user: {{ user_name }}
    key: {{ lookup('file', 'file path from relative to the project') }}
    state: present
```
