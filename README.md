# ansible-testing

ansible-testing is designed to be a set of modules for Ansible to allow 
infrastructure testing. 

Hopefully these modules will be absorbed into [Ansible](http://github.com/ansible/ansible)
if the concept proves itself

## Installation

```
git clone http://github.com/willthames/ansible-testing
```

## Usage
```
ansible -M path/to/ansible-testing testing-playbook.yml
```

## Implemented

```
name: python is running app.py
test_process:
  state: present
  name: python
  args:
  - app.py

name: port 80 appears open from playbook machine
local_action: test_tcp state=open port=80

name: check HTTP response has 200 status and contains Hello
local_action: test_http url=http://example.com/helloworld status=200 regex='.*Hello.*'

```

# See also

* [assert module](http://docs.ansible.com/assert_module.html)
* [stat module](http://docs.ansible.com/stat_module.html)
* [Testing Strategies](http://docs.ansible.com/test_strategies.html)

## Example

```
name: run hello command
action: command echo -n hello
register: hello_cmd

name: check results of hello command
assert:
  that:
    - "hello_cmd.stdout == 'hello'"
    - "hello_cmd.rc == 0"
```


