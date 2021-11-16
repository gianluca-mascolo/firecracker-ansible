# Firecracker VM management with Ansible

## About

This project is a personal research about Firecracker and Microvms.  
It contains an Ansible playbook used to start one or more virtual machines described by a configuration file.

## Requirements


* [Firecracker](https://github.com/firecracker-microvm/firecracker) engine
* Ansible
* A Linux host with:
  -  libvirt and a bridge configured
  -  systemd
  -  screen
  -  sudo rights
* A [kernel and a root filesystem](https://github.com/firecracker-microvm/firecracker/blob/main/docs/getting-started.md#running-firecracker) for your vm. 

Additionally you will need Ansible galaxy collection `ansible.netcommon` installed locally:

`ansible-galaxy collection install  -p ./collections -r requirements.yml`

## Demo

[![asciicast](https://asciinema.org/a/449532.svg)](https://asciinema.org/a/449532)

## How it works

The playbook will install systemd user services in your `~/.config/systemd/user/` to start a firecracker process for every vm you need to manage.  
It will then create the configured tap interfaces and attach them to a libvirt network bridge.  
Finally, using firecracker REST api it will start the configured vms and you can attach to the console process using screen.
The configuration file for virtual machines is placed in [group_vars/firecracker.yml](group_vars/firecracker.yml)
To ask for sudo password (if needed) run the playbook with  
`ansible-playbook -K playbook`

## Disclaimer
At this stage all I can say is: "it works on my machine(tm)".
