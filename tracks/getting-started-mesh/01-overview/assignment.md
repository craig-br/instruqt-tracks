---
slug: overview
id: 2y22esvrwfyd
type: challenge
title: Automation mesh overview
teaser: Explore automation mesh concepts
notes:
- type: text
  contents: "# Challenge summary\n<br>\n\n<p align=\"center\">\n  <img width=\"500px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_high_level.png\">\n</p>\n<br>\n\nIn
    this challenge, we'll cover the different automation mesh node types and instance
    groups created during the Ansible Automation Platform installation.\n\n<style
    type=\"text/css\" rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
- type: text
  contents: "# Automation mesh\n<br>\n<p align=\"center\">\n  <img width=\"700px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_instances_view.png\">\n</p>\n<br>\n\n**Automation
    mesh** is an overlay network intended to ease the distribution of work across
    a large and dispersed collection of workers. Mesh nodes establish peer-to-peer
    connections with each other across your existing networks.\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
- type: text
  contents: "# Automation mesh worker node types\n<br>\n<p align=\"center\">\n  <img
    width=\"700px\" src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_default_igs.png\">\n</p>\n<br>\n\n**Automation
    mesh** enables independent scaling of *control plane* and *execution plane* capacity
    and is configured during the Ansible Automation Platform installation. It allows
    you to create worker node types and allocate the capacity to control tasks (e.g.
    RBAC, auditing ), and execution tasks ( running your playbooks ).\n\n\n**Automation
    mesh** worker nodes are logically grouped using automation controller [*instance
    groups*](https://docs.ansible.com/automation-controller/latest/html/userguide/instance_groups.html).\n\n\n<style
    type=\"text/css\" rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
tabs:
- title: Controller UI
  type: service
  hostname: automation-controller21
  port: 443
difficulty: basic
timelimit: 300
---
## Your assignment.
### *Estimated time: 5 minutes*

*Login credentials:*<p>
User: admin <p>
Password: ansible123!

> **Note**
> All tasks are performed in the automation controller UI.
>

* Log into the Controller UI using the provided credentials
* On the side navigation under the **Administration** section, click on **Instance Groups**
* Click on the `default`instance group
* Click on the `Instances` tab on the top

![default_ig](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_default_ig_instances.png)


* The **`default` instance group** is the default location for all mesh worker nodes and is always present in automation controller. It's used to execute *Job Templates* if no instance group is specified in their configuration.

* Click on the `mesh-exec1` instance and have a look at the `Node Type`. `mesh-exec1` is configured as an **execution node**.
  * **Execution nodes** replace isolated nodes used in Ansible Tower and fulfills the same functions. This node is dedicated to run **Job Templates** and does not execute any controller runtime functions.

![mesh-exec1](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_mesh-exec1.png)

* Click on **Instance Groups** under the **Administration** section to return to the main instance group window
* Click on the `controlplane` instance group.
* Click on the `Instances` tab on the top

![controlplane](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_controlplane_ig_instances.png)

* The **`controlplane` instance group** is the preselected instance group for all mesh worker nodes that run control plane tasks.

* Click on the `automation-controller21` instance and have a look at the `Node Type`. `automation-controller21` is configured as a **hybrid** node.
  * **Hybrid nodes** can run automation controller runtime functions, like project updates and management jobs, and run automation jobs.

* The `controlplane` instance group also contains another node type, called **Control nodes**. **Control nodes** are dedicated to running control plane tasks and does not execute any automation jobs. This lab does not use **Control nodes** and will use the `automation-controller21` **execution** node for automation jobs.

![automation-controller21](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_automation-controller21.png)

* When you are done, press the `Next` button below to go to the next challenge.