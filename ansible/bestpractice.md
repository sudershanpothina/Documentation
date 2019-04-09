Use a project structure as below
```
site.yml - playbook
hosts - list of hosts
roles
  group
  - tasks -> list of tasks to perform in a group
  - handlers -> very simple tasks, like starting a service
  - templates -> jinja2 files
  - files -> files to copy
  - meta -> dependencies on other roles
group_vars -> all.yml (file with list of variables) 
ex - 
port: 2030
hostname: test
```
