# Ansible role: labocbz.install_ssh

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Cbz-blue)

## Description

![Tag: Ssh](https://img.shields.io/badge/Tech-Ssh-orange)
![Tag: Cron](https://img.shields.io/badge/Tech-Cron-orange)

An Ansible role to install SSH and import your configuration.

The Ansible role for SSH configuration automates the setup and management of SSH access to your system. This role utilizes several variables to customize the SSH configuration.

The variable "ssh_allowed_groups" specifies the groups that are allowed SSH access. In this example, the "root" group is allowed SSH access. You can modify this list to include other groups as needed.

The variable "ssh_port" defines the SSH port number. By default, it is set to port 22, which is the standard SSH port. You can change this value if you have configured SSH to use a different port.

To ensure SSH service starts at boot, the variable "ssh_create_cron_start_at_boot" is set to true. This will create a cron job that starts the SSH service automatically when the system boots.

The "ssh_restart_after_boot_time" variable determines the delay, in seconds, before the SSH service is restarted after the system boots. In this example, it is set to 10 seconds. Adjust this value according to your specific requirements.

Lastly, the "ssh_administration_name" variable allows you to specify the name of your company or organization for administrative purposes. In this example, it is set to "your company".

Using this Ansible role for SSH configuration, you can easily manage SSH access, define the SSH port, ensure SSH service starts at boot, configure the restart delay, and specify your company name for administrative purposes.

## Folder structure

By default Ansible will look in each directory within a role for a main.yml file for relevant content (also man.yml and main):

```PYTHON
.
├── README.md  # Contains an overview of the role and its purpose.
├── defaults
│   ├── main.yml  # Contains default variables for the role that can be overridden by users.
│   └── README.md  # Contains documentation for the default variables.
├── files
│   └── README.md  # Contains documentation for the files in the directory.
├── handlers
│   ├── main.yml  # Contains handlers that can be called by tasks within the role.
│   └── README.md  # Contains documentation for the handlers.
├── meta
│   ├── main.yml  # Contains metadata about the role, including dependencies and supported platforms.
│   └── README.md  # Contains documentation for the role metadata.
├── tasks
│   ├── main.yml  # Contains tasks to be executed by the role on the managed nodes.
│   └── README.md  # Contains documentation for the tasks.
├── templates
│   └── README.md  # Contains documentation for the templates.
└── vars
    ├── main.yml  # Contains variables that are specific to the role and are not meant to be overridden.
    └── README.md  # Contains documentation for the role variables.
```

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the role) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This role contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your role
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this role, just copy/import this role or raw file into your fresh playbook repository or call it with the "include_role/import_role" module.

## Usage

### Vars

Some vars a required to run this role:

```YAML
---
ssh_allowed_groups:
  - "root"

ssh_port: 22

ssh_create_cron_start_at_boot: true
ssh_restart_after_boot_time: 10
ssh_administration_name: "your company"

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---
inv_ssh_administration_name: "My Compagny"

inv_ssh_port: 23

```

```YAML
# From AWX / Tower
---

```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
- name: "Include labocbz.install_ssh"
    tags:
    - "labocbz.install_ssh"
    vars:
    ssh_port: "{{ inv_ssh_port }}"
    ssh_administration_name: "{{ inv_ssh_administration_name }}"
    ansible.builtin.include_role:
    name: "labocbz.install_ssh"
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-04-27: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
