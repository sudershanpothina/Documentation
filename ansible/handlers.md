create a handler
```
- name: nginx restart
  service: name=nginx state=restarted
  ```

create a notify in the task
```
- name: update nginx
  template: src=nginx.conf.jinja2, dest=/etc/nginx/nginx.conf 
  # no need to give the full path to the source, it can find templates in the template folder
  notify: nginx restart
```  
