---
slug: generate-tasks
id: oqasvizywai0
type: challenge
title: Generating Ansible Playbook tasks with Ansible Lightspeed.
teaser: We'll explore Ansible Lightspeed features, generate Ansible Playbook tasks,
  and learn more about Ansible Visual Studio Code extension features.
tabs:
- title: cmd
  type: terminal
  hostname: lightspeed-101-controller
  cmd: /bin/bash
- title: controller
  type: service
  hostname: lightspeed-101-controller
  path: /
  port: 443
  new_window: true
- title: RHEL
  type: service
  hostname: vnc-proxy
  path: /#/client/c/srv01?username=student&password=learn_ansible
  port: 8080
  new_window: true
- title: code
  type: service
  hostname: lightspeed-101-controller
  path: /editor/
  port: 443
  new_window: true
difficulty: basic
timelimit: 600
---
WIP