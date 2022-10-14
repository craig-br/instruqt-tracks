---
slug: edge-playground
id: fkeryr2p6own
type: challenge
title: Playground
teaser: Use the remaining time to flex your new skills or explore the lab.
tabs:
- title: Controller
  type: service
  hostname: controller-edge-lab
  port: 443
- title: Jhb app
  type: service
  hostname: jhb-edge-lab
  path: /web/login
  port: 8088
  new_window: true
- title: Jhb mon
  type: service
  hostname: jhb-edge-lab
  path: /network
  port: 9090
  url: https://jhb-edge-lab:9090
  new_window: true
- title: Dublin app
  type: service
  hostname: dublin-edge-lab
  path: /web/login
  port: 8088
  new_window: true
- title: Dublin mon
  type: service
  hostname: dublin-edge-lab
  path: /network
  port: 9090
  url: https://dublin-edge-lab:9090
  new_window: true
difficulty: basic
timelimit: 600
---
WIP