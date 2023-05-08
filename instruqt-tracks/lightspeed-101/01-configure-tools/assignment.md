---
slug: configure-tools
id: trgtkqisymwa
type: challenge
title: Configuring Ansible Lightspeed in Visual Studio Code.
teaser: We'll enable Ansible Lightspeed and Ansible Lint in the Ansible Visual Studio
  Code extension, and authenticate with the Ansible Lightspeed  service.
notes:
- type: text
  contents: WIP
tabs:
- title: RHEL
  type: service
  hostname: vnc-proxy
  path: /#/client/c/srv01?username=student&password=learn_ansible
  port: 8080
  new_window: true
- title: controller-cmd
  type: terminal
  hostname: lightspeed-101-controller
  cmd: /bin/bash
- title: quac
  type: terminal
  hostname: vnc-proxy
  cmd: /bin/bash
- title: controller
  type: service
  hostname: lightspeed-101-controller
  path: /
  port: 443
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
VSCode extension
How to enable
How to log in and accept Tc & Cs