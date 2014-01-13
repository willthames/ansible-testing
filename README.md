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

Note that this is README-Driven development - some or all of the following may not be 
implemented (currently only check_tcp and check_process are implemented)

```
name: http is installed
action: check_rpm state=present name=http

name: http is running
action: check_process state=running name=http

name: port 80 appears open from playbook machine
local_action: check_tcp state=open port=80

name: connecting to http://example.com/healthcheck returns 'Healthy' and status 200
local_action: check_http url=http://example.com/healthcheck status=200 message='.*Healthy.*'
```
