---
slug: env-overview
id: ywydmze3vfpu
type: challenge
title: Environment overview
teaser: In this challenge, we'll explore the lab environment
tabs:
- title: Controller
  type: service
  hostname: raleigh-controller
  port: 443
- title: code
  type: service
  hostname: raleigh-controller
  path: /editor/
  port: 443
  new_window: true
- title: jhb-exec
  type: terminal
  hostname: jhb-exec
- title: dublin-exec
  type: terminal
  hostname: dublin-exec
- title: jhb-kiosk
  type: terminal
  hostname: jhb-kiosk
- title: dublin-kiosk
  type: terminal
  hostname: dublin-kiosk
- title: jhb-app
  type: service
  hostname: jhb-kiosk
  port: 8088
  new_window: true
- title: dublin-app
  type: service
  hostname: dublin-kiosk
  port: 8088
  new_window: true
difficulty: basic
timelimit: 6000
---
WIP