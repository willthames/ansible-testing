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
test_process:
  state: present
  name: python
  args: 
  - app.py

name: port 80 appears open from playbook machine
local_action: test_tcp state=open port=80

name: number of cpus is 2
action: assert condition="{{ansible_processor_count}} == 2" failure_msg="Expecting 2 CPUs, found {{ansible_processor_count}}"

name: /usr/local/etc/example exists
action: test_file state=file path=/usr/local/etc/example mode=0755 owner=testuser group=testgroup

name: capture results of /usr/local/bin/run_stuff
action: command /usr/local/bin/run_stuff
register: run_stuff_results

name: run_stuff exited with status 0
action: assert condition="{{run_stuff_results.rc}} == 0" failure_msg="run_stuff did not exit with status 0"

# Note that the expansion of run_stuff_results.stdout is quoted here
name: run_stuff printed Hello
action: assert condition="'Hello' in '{{run_stuff_results.stdout}}'" failure_msg="run_stuff did not print Hello"

```

# To be implemented
```
name: http is installed
action: test_rpm state=present name=http

name: connecting to http://example.com/healthcheck returns 'Healthy' and status 200
local_action: test_http url=http://example.com/healthcheck status=200 message='.*Healthy.*'

name: /usr/local/bin/bobbins outputs 'hello' and exits with status 0
action: test_command name=/usr/local/bin/bobbins status=0 stdout='hello'
```
