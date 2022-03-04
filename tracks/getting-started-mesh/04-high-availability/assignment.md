---
slug: high-availability
id: kcl8kjem907q
type: challenge
title: Resilient automation with mesh
teaser: Automation mesh offers flexible design options and native resilience across
  worker nodes
notes:
- type: text
  contents: "# Challenge summary\n<br>\n\n<p align=\"center\">\n  <img width=\"400px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_map_dbn.png\">\n</p>\n<br>\n\nACME
    Corp successfully executed automation content across multiple regions using automation
    mesh. A new network outage between **Raleigh** and **Johannesburg**, however,
    is stopping the team from running automation in the South African region.\n\nAutomation
    mesh provides the capability to build native fault tolerance and redundancy into
    your platform installation. In this challenge, we’ll use a [**hop node**](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html/red_hat_ansible_automation_platform_automation_mesh_guide/con-automation-mesh-node-types#execution_plane)
    to reach Johannesburg via a secondary network link.\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
- type: text
  contents: "# Automation mesh hop nodes\n<br>\n\n<p align=\"center\">\n  <img height=\"500px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_node_distr_hop.png\">\n</p>\n<br>\n\n[**Hop
    nodes**](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html/red_hat_ansible_automation_platform_automation_mesh_guide/con-automation-mesh-node-types#execution_plane)
    \ also provide a mechanism to natively build redundancy into your platform topology
    across existing networks.\n\n**Hop nodes** route traffic to other execution nodes
    across constrained networks, such as DMZs and VPCs and don’t run automation jobs.
    Hop nodes enable you to reach devices that aren't directly connected to  controller
    and effectively replace the need for SSH proxies and jump hosts.\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
tabs:
- title: Controller
  type: service
  hostname: automation-controller21
  port: 443
difficulty: basic
timelimit: 600
---
# Your assignment
### *Estimated time: 10 minutes*

**Controller login credentials:**<p>
*User*: admin <p>
*Password*: ansible123!

> **Note**<p>
>
> All tasks are performed in the automation controller UI.<p>
> Log into automation controller dashboard using the credentials above.

## Perform a health check on the execution node

The Johannesburg data center is currently unreachable from the ACME Corp Raleigh head office. A secondary network link exists via the **Dublin data center** located in Ireland. We'll confirm the status of `mesh-exec1` and configure a **hop node** in the **Dublin data center** to reach Johannesburg.

## Confirm the status of ```mesh-exec1``` in the Johannesburg data center

Automation mesh performs periodic health checks on worker nodes and uses this information to determine optimal routing and job assignment. Health checks can be triggered in the automation controller WebUI or API.

* On the side navigation under the **Administration** section, click on **Instance Groups**
* Click on the ```Johannesburg data center``` instance group
* Click on **Instances** located in the top menu
* Note that ```mesh-exec1``` is showing an *Error* status.

![mesh_exec1_error](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_exec1_error.png)
<br>

* Select ```mesh-exec1``` by clicking on the checkbox next to it
* Click on the **Health Check** button to confirm the *Error* status. This takes a few seconds to complete.

**Run the ```Mesh route info``` job template**

The ```Mesh route info``` job template displays the route mesh uses to run automation jobs in Johannesburg. Let's confirm there's currently no route to ```mesh-exec1```

* On the side navigation under the **Resources** section, click on **Templates**
* Click on the *rocket* icon next to the ```Mesh route info``` job template to launch it.
* A new window will prompt to choose an inventory. Keep the default selection of ```Raleigh DC```
* Click **Next**
* Click **Launch**
* Note the job template output

> *Error no connection to next hop from automation-controller21*<p>
>
<br>

![mesh_exec1_route](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_exec1_no_route.png)
<br>

## Configure ```mesh-hop1``` as a hop node in the ```Dublin DC```

**Hop nodes** route traffic to other execution nodes across constrained networks, such as DMZs and VPCs and don’t run automation jobs. Hop nodes enable you to reach devices that aren't directly connected to **controller**.

ACME Corp can reach the Johannesburg location via Dublin, Ireland using a backup network connection. Configuring a **hop node** in Dublin would resolve the outage by creating an indirect link back to the **Raleigh data center**.

Your automation controller instance is configured with a new ```Dublin DC``` inventory and ```Setup Dublin hop node``` job template.

>**Note**<p>
>The ```Setup Dublin hop node``` job template is used as a demo example in this lab. Mesh worker nodes are configured and installed using the Ansible Automation Platform installer.<p>
> Please visit the [official installation guide](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html/red_hat_ansible_automation_platform_installation_guide/index) for more information on the supported method.
<br>

The ```Setup Dublin hop node``` job template configures ```mesh-hop1.dublin.example.com``` as a **hop node**.

**Run the ```Setup Dublin hop node``` job template**

* On the side navigation under the **Resources** section, click on **Templates**
* Click on the *rocket* icon next to the ```Setup Dublin hop node``` job template to launch it.
* A new window will prompt to choose an inventory. Keep the default selection of ```Dublin DC```
* Click **Next**
* Click **Launch**
* Note that automation mesh dynamically added ```mesh-hop1``` to the routing table.

>**Note**<p>
> **Hop nodes** don't run automation jobs and therefore cannot be assigned to instance groups within automation controller.

![mesh_exec1_route](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_route_hop1.png)
<br>

**Confirm the updated route to ```mesh-exec1```**

Automation mesh is aware of ```mesh-hop1``` and its connections to other worker nodes. The ```mesh-exec1``` is also peered with the hop node. Let's confirm the new route to the Johannesburg data center.

* On the side navigation under the **Resources** section, click on **Templates**
* Click on the `rocket` icon next to the ```Mesh route info``` job template to launch it.
* A new window will prompt to choose an inventory. Keep the default selection of ```Raleigh DC```
* Click **Next**
* Click **Launch**
* Note that ```mesh-hop1``` is used to reach ```Johannesburg DC```.

![mesh_exec1_new_route](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_route_new_exec1.png)
<br>

## Review the status of ```mesh-exec1``` in the ```Johannesburg data center```

Now that automation mesh has created a new route to ```mesh-exec1```, we should see it restored to a *healthy* state

* On the side navigation under the **Administration** section, click on **Instance Groups**
* Click on the ```Johannesburg data center``` instance group
* Click on **Instances** located in the top menu
* Select ```mesh-exec1``` by clicking on the checkbox next to it
* Click on the **Health Check** button. This takes a few seconds to complete.
* Note that ```mesh-exec1``` is now showing a healthy status

![mesh_exec1_error](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_health_check_mesh-exec1.png)
<br>

**Run the ```Debug info``` job template using the ```Johannesburg DC``` inventory**

ACME Corp can now run automation jobs using the new route to Johannesburg. Execute the ```Debug info``` job template to confirm this.

* On the side navigation under the **Resources** section, click on **Templates**
* Click on the ```Debug info``` job template
* Click on the *rocket* icon under the **Actions** column to launch the job template.
* Select the ```Johannesburg inventory```
* Click **Next**
* Click **Launch**
* The ```Debug info``` job template executed successfully!

![mesh_exec1_error](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jt_debug_jhb_output.png)
<br>

# Building resilient platforms with automation mesh

Automation mesh offers native capabilities to create redundant platform topologies and reach endpoint devices over constrained networks such as DMZs and VPCs. ACME Corp used a **hop node** to reach Johannesburg via a backup network link and dynamic mesh peering capabilities.

When you're done with all the steps, click on the `Check` button move to the next challenge.