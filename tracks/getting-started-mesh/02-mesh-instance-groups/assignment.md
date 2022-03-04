---
slug: mesh-instance-groups
id: j5xbmsjakj6r
type: challenge
title: Automation mesh and instance groups
teaser: Create new instance groups and allocate mesh worker nodes for local and remote
  execution
notes:
- type: text
  contents: "# Challenge summary\n<br>\n\n<p align=\"center\">\n  <img width=\"500px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_map_jhb.png\">\n</p>\n<br>\n\nACME
    Corp is a global company based in Raleigh, United States, with remote locations
    across the globe. One of these remote locations is Johannesburg, South Africa.\n\nIn
    this challenge, we'll create **instance groups** for the Raleigh and Johannesburg
    data centers and allocate automation mesh worker nodes to them.\n\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
- type: text
  contents: "# Automation mesh and instance groups\n<br>\n<p align=\"center\">\n  <img
    width=\"600px\" src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jhb_ig.png\">\n</p>\n<br>\n\n[**Instance
    groups**](https://docs.ansible.com/automation-controller/latest/html/administration/containers_instance_groups.html)
    logically arrange execution capacity and provide control on where an automation
    job runs.\n\nAutomation mesh worker nodes are assigned to **instance groups**
    during installation or via automation controller.\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
- type: text
  contents: "# Mesh node health checks\n<br>\n<p align=\"center\">\n  <img width=\"600px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_node_health_check.png\">\n</p>\n<br>\n\nAutomation
    mesh performs capacity health checks on worker nodes based on CPU, memory and
    other metrics.\n\nMesh uses these metrics to dynamically calculate the optimal
    route and node to execute automation jobs, based on your configuration.\n\n<style
    type=\"text/css\" rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
tabs:
- title: Controller UI
  type: service
  hostname: automation-controller21
  port: 443
difficulty: basic
timelimit: 600
---
**Controller login credentials:**<p>
*User*: admin <p>
*Password*: ansible123!

> **Note**<p>
>
> All tasks are performed in the automation controller UI.<p>
> All the fields are **case-sensitive** and the check will fail! Please ensure you use the same capitalization as used in the assignments.

## Your assignment
### *Estimated time: 10 minutes*

[**Instance groups**](https://docs.ansible.com/automation-controller/latest/html/administration/containers_instance_groups.html) logically arrange execution capacity and provide control on where an automation job runs. Instance groups are then assigned with **automation controller** objects, such as Inventories, Organizations and Job Templates.

Automation mesh worker nodes are associated with **instance groups** enabling you to allocate the desired execution capacity and location for your platform.

**Create a new instance group for Raleigh data center**
<br>

Automation controller is deployed in the Raleigh data center and we want to run our automation jobs locally using the **automation-controller21 hybrid node**.
<br>

* On the side navigation under the **Administration** section, click on **Instance Groups**
* Click on the **Add** and select **Add instance group**
* Create a new instance group and name it `Raleigh data center`.
* Click on **Save**

![raleigh_ig](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_raleigh_ig_create.png)
<br>

**Associate the `automation-controller21` instance with the **Raleigh data center** instance group**
* Click on **Instances** on the top menu.
* Click on **Associate**
* Select the `automation-controller21` instance and click on **Save**

![raleigh_associate](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_raleigh_associate_instance.png)
<br>

**Create a new instance group for Johannesburg data center**
<br>

We also need to run automation jobs in Johannesburg, South Africa. To do this, we'll create a new instance group and associate the **mesh-exec1 execution node** which is deployed in the data center.
<br>

* On the side navigation under the **Administration** section, click on **Instance Groups**
* Click on the **Add** and select **Add instance group**
* Create a new instance group and name it `Johannesburg data center`.
* Click on **Save**

![raleigh_ig](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jhb_ig_create.png)
<br>

**Associate the `mesh-exec1` instance with the **Johannesburg data center** instance group**
* Click on **Instances** on the top menu.
* Click on **Associate**
* Select the `mesh-exec1` instance and click on **Save**

![jhb_associate](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jhb_associate_instance.png)
<br>

**Worker node health checks**
<br>

Automation mesh performs health checks on worker nodes to determine the optimal route and automation job allocation. Let's run a health check on `mesh-exec1` in Johannesburg.
<br>

* On the side navigation under the **Administration** section, click on **Instance Groups**
* Click on the `Johannesburg data center` instance group
* Click on **Instances** on the top menu.
* Select `mesh-exec1` by clicking on the checkbox next it
* Click on **Health Check**
* Hover your mouse over the `Healthy` under the **Status** column and note the day/time.”

![mesh-exec1_health](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_health_check_mesh-exec1.png)
<br>

* When you are done, press the `Check` button below to go to the next challenge.
