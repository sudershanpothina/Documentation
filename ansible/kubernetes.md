module - k8s_raw

Usage
```
- name: deploy persistent volume
  k8s_raw:
    state: present
    #Authentication use .kube/config file or use api key or use client certificate file
    # it automatically looks for $HOME/.kube/config file
    definition:
      kind: PersistentVolumeClaim
      apiVersion: v1
      namespace: blah
      ...
```
to run this playbook on localhost
```
ansible-playbook -i localhost, playbook.yaml
there is a docker module to help build docker images

```
https://docs.ansible.com/ansible/latest/modules/k8s_module.html

```
- name: Read definition file from the Ansible controller file system after Jinja templating
  k8s:
    state: present
    definition: "{{ lookup('template', '/testing/deployment.yml') }}"
```
