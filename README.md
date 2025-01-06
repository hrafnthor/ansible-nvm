# ansible-nvm
An opinionated Ansible role for installing Node Version Manager (nvm) 


Requirements
------------

This role requires two separate tools be installed.

First it requires the 'ansible.utils' collection be installed from Ansible-Galaxy via:

```shell
ansible-galaxy collection install ansible.utils
```

Secondly it requires the `jsonschema` Python package be installed via:

```shell
pip3 install jsonschema
```



Role Variables
--------------

`nvm` : [mapping] (required) contains the following fields:

* `source_url`: [string] (optional) The http url to the nvm source repository to use. Defaults to `https://github.com/nvm-sh/nvm`

* `users` : [array of objects]

    A list of mappings containing the following fields:

    * `name` [string] (required)

        The user name for which to install the requested version of nvm for 

    * `version` [string] (required)

        The version number of nvm to install for the user.
    
    * `path` [string] (optional)

        The user home directory relative path where nvm will be installed at.

    * `remove` [boolean] (optional)

        Indicates if NVM should be removed for this user. If set, then `version` can not be present as well.


Example:

```yaml
nvm:
  source_url: https://myprivatecms.com/nvm
  users: 
  - name: Joe
    remove: true    # Remove a previous installation for user before installing a different one in a custom location
  - name: Joe
    version: v0.39.0
    path: ".local/development/nvm"
  - name: Sally
    version: v0.34.2

 ```

Dependencies
------------

None, other then previously stated requirements.

Setup
-----

Before the role can be used it needs to be added to the machine running the playbook, and as of writing this, this role is not hosted on Ansible-Galaxy only on Github.

1. Create a `requirements.yml` file in the root directory of the playbook being worked on.

2. Add the following definition inside the `requirements.yml` file:

```yml
- name: hth-nvm
  src: https://github.com/hrafnthor/ansible-nvm.git
  scm: git
```

3. Install the requirements by executing

```shell
ansible-galaxy install -r .requirements.yml
```

This will allow any playbook run from this machine to use the role `hth-nvm`


Example Playbook
----------------


```yaml
- hosts: all
    vars:
    - nvm:
        - users: 
            - name: Joe
              version: v0.39.0
              path: ".local/nvm"
            - name: Sally
              version: v0.34.2
  roles:
     - hth-nvm
```


License
-------

MIT license. See attached license file.

Author Information
------------------

Hrafn Thorvaldsson
Find me at https://www.hth.is
