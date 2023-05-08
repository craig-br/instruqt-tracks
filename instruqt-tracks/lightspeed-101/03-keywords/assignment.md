---
slug: keywords
id: xjiacv6lk0nq
type: challenge
title: Ansible Lightspeed  and Ansible Playbook keyword content.
teaser: We'll use Ansible Lightspeed to generate tasks based on existing Ansible Playbook
  keywords.
tabs:
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
- title: cmd
  type: terminal
  hostname: lightspeed-101-controller
  cmd: su - rhel -c "/bin/bash"
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