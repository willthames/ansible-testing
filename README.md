ansible-testing
===============

ansible-testing is designed to be a set of modules for Ansible to allow 
infrastructure testing. 

Hopefully these modules will be absorbed into [Ansible](http://github.com/ansible/ansible)
if the concept proves itself

## Installation

```
cd ~/src/ansible
git submodule add http://github.com/willthames/ansible-testing library/testing
```

## Usage
```
- hosts: testinstance

  roles:
  - base
  - webserver
```

# Implemented
```
name: python is running app.py
check_process:
  state: present
  name: python
  args: 
  - app.py

name: port 80 appears open from playbook machine
local_action: check_tcp state=open port=80

name: number of cpus is 2
action: check_equals left={{ansible_processor_count}} right=2
```

# To be implemented
```
name: http is installed
action: check_rpm state=present name=http

name: connecting to http://example.com/healthcheck returns 'Healthy' and status 200
local_action: check_http url=http://example.com/healthcheck status=200 message='.*Healthy.*'

name: /usr/local/etc/example exists
action: check_file state=file name=/usr/local/etc/example

name: /usr/local/bin/bobbins outputs 'hello' and exits with status 0
action: check_command name=/usr/local/bin/bobbins status=0 stdout='hello'
```
