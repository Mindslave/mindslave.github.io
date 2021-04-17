---
title: Managing my system configurations with Ansible
author: Marius Kimmina
date: 2021-06-21 14:10:00 +0800
categories: [DevOps, Ansible]
published: false
tags: [Ansible, dotfiles]
---


## 1. Introduction
A common problem for a lot of Developers, Sysadmins and the like is that they have a lot of custom configurations
on they're system. These configurations can be a lot of different things, aliases for commands or shortcuts for example. 
People grow used to they're configurations and they develop an efficent workflow with them. The problem with this is, 
that it becomes harder to work with off the shelf systems. Especially for people that do a lot of they're work in
VMs or otherwise virtualized environments, they find themselves missing they're cosy configurations quite often. 
They are then faced with 2 options:

* Install all they're custom software and configurations on the system
* Work with the system as is

The first of these solutions takes a lot of time upfront, the second one might be fine for short tasks but if they are 
supposed to work with the given system for long, this becomes inefficient. This is were Ansible comes in, it can be used 
to reduce the setup time of a new system dramatically. In fact, once all the ansible playbook is ready, new systems can be 
configured with one single command, leaving the developer/admin free to do other things while his system is getting ready.

## 2. What is Ansible?

Well, from the Ansible website itself: "Ansible is a universal language, unraveling the mystery of how work gets done. 
Turn tough tasks into repeatable playbooks. Roll out enterprise-wide protocols with the push of a button." 
With ansible we define a job that needs to get done with YAML files, these so called `playbooks` can then be used over over again.

### 2.1 Playbooks
Playbooks are on the highest level of the ansible hierarchy, a `playbook` defines a tasks that is in itself complete and does not depend
on any other tasks. A `playbook` can be made up of one big .yml file or it can broken up into multiple `roles`. 

### 2.2 Roles

### 2.3 Tasks

## Example Role: Neovim

## Why I think that Ansible is the right tool for the job
I saw many people using bash scripts for this that kinda got the job done as well, but Ansible makes it easier to define
playbooks that work accross different linux distributions as well as on MacOS by simly importing tasks based on the 
ansible\_os\_family bultin variable.
For every piece of software that should be installed and configured there is a seperate `role`. The structure for one of these roles
looks like this:

```
├── files
│   └── .tmux.conf
└── tasks
    ├── darwin.yml
    ├── debian.yml
    ├── main.yml
    └── redhat.yml
```
Inside the `tasks` directory create a file called `main.yml` and then a seperate file for every os/distro you want to support.
Inside the `main.yml` file we import all os/distro specific tasks according to the `ansible_os_family`

```
- import_tasks: redhat.yml
  when: ansible_os_family == "RedHat"
- import_tasks: debian.yml
  when: ansible_os_family == "Debian"
- import_tasks: darwin.yml
  when: ansible_os_family == "Darwin"
```

The `files` directory contains all the configuration files associated with the software, tmux in this case.
