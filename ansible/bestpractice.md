Use a project structure as below
site.yml - playbook
hosts - list of hosts
roles
  group
  - tasks -> list of tasks to perform in a group
  - handlers -> start services
  - templates -> jinja2 files
  - files -> files to copy
  - meta -> dependencies on other roles
group_vars - 
