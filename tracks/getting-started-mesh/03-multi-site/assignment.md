---
slug: multi-site
id: a2ix1emgbupt
type: challenge
title: Multi-site automation using mesh
teaser: Run automation jobs across multiple sites using automation mesh
notes:
- type: text
  contents: "# Challenge summary\n<br>\n\n<p align=\"center\">\n  <img width=\"500px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_map_nodes.png\">\n</p>\n<br>\n\nOur
    previous challenge logically grouped automation capacity by associating mesh worker
    nodes with the **Raleigh data center** and **Johannesburg data center** instance
    groups. Our next step is to assign these instance groups to ACME Corp [**inventories**](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html)
    and run localized automation jobs.\n\n<style type=\"text/css\" rel=\"stylesheet\">\nh1
    {\n\ttext-align: center\n\t}\n</style>"
- type: text
  contents: "# Start locally, scale globally\n<br>\n\n<p align=\"center\">\n  <img
    width=\"500px\" src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_node_distributed.png\">\n</p>\n<br>\n\nDelivering
    and running automation closer the endpoints reduces execution interruptions, inconsistent
    states, and IT service downtime. Distributing and managing automation across multiple
    sites, however, is complex.\n\nAutomation mesh distributes automation content
    and runs execution environments across dynamically peered workers nodes which
    are co-located with the target endpoints. Localizing execution overcomes multi-region
    challenges, such as high latency and connection disruptions.\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1 {\n\ttext-align: center\n\t}\n</style>"
tabs:
- title: Controller UI
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
> Log into automation controller dashboard, using the credentials above.

## Assign instance groups to inventories
Instance groups and the associated mesh worker nodes are assigned to Organizations, Inventories, and Job Templates within automation controller.

The ACME Corp IT department needs to run automation in the Raleigh and Johannesburg locations. We'll assign the instance groups we created in the previous exercise to pre-created inventories.

**Associate the ```Raleigh data center``` instance group with the ```Raleigh DC``` inventory**

* On the side navigation under the **Resources** section, click on **Inventories**
* Click on the ```Raleigh DC``` inventory
* Click on Edit
* Click on the magnifying glass button under **Instance Groups**
* Check the box next to ```Raleigh data center```
* Click on **Select**
* Click on **Save** in the **Edit Details** window

![raleigh_inv](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_us_inv_ig_select.png)
<br>

**Associate the ```Johannesburg data center``` instance group with the ```Johannesburg DC``` inventory**

* On the side navigation under the **Resources** section, click on **Inventories**
* Click on the ```Johannesburg DC``` inventory
* Click on Edit
* Click on the magnifying glass button under **Instance Groups**
* Check the box next to ```Johannesburg data center```
* Click on **Select**
* Click on **Save** in the **Edit Details** window

![jhb_inv](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jhb_inv_ig_select.png)
<br>

## Execute job templates using ACME Corp inventories

A **job template** is a definition and set of parameters for running Ansible automation. Job templates are useful to execute the same job many times. Job templates also encourage the reuse of Ansible playbook content and collaboration between teams.

The ```Debug info``` job template returns current load information from systems.
<br>

**Run the ```Debug info``` job template using the ```Raleigh``` DC inventory**

* On the side navigation under the **Resources** section, click on **Templates**
* Click on the *rocket icon* under the **Actions** column on the ```Debug info``` job template row. This will open a new window

![inv_choose_raleigh](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_inv_choose_raleigh.png)
<br>

The ```Debug info``` job template is configured to ask which inventory to use prior to launching. Job templates provide the ability to prompt for user input for certain parameters before execution. This is useful as we need to run the automation on multiple ACME Corp inventories.

* Keep the ```Raleigh DC``` inventory as the selection
* Click on **Next** and then click on **Launch**

![jt_debug_info_output](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jt_debug_raleigh_output.png)
<br>

* Click on the **Details** tab on the top of the window and note that it used the ```Raleigh data center``` instance group and ```automation-controller21``` worker node to run the job.

![jt_debug_info_details](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jt_debug_raleigh_details.png)
<br>

**Run the ```Debug info``` job template using the ```Johannesburg DC``` inventory**

* On the side navigation under the **Resources** section, click on **Templates**
* Click on the *rocket icon* under the **Actions** column on the ```Debug info``` job template row. This will open a new window
* Select the ```Johannesburg inventory```

![inv_choose_jhb](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_inv_choose_jhb.png)
<br>

* Click on **Next** and then click on **Launch**

![jt_debug_info_output](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jt_debug_jhb_output.png)

* As we did in the previous steps, click on the **Details** tab on the top of the window and note that it used the ```Johannesburg data center``` instance group and ```mesh-exec1``` worker node to run the job.

![jt_debug_info_details](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jt_debug_jhb_details.png)
<br>

## Automation mesh worker node remote execution

Automation mesh localizes automation execution using worker nodes co-located with the target endpoint devices. This design overcomes scaling challenges that includes high latency networks and connection disruptions.

We consistently ran the ```Debug info``` job template in the Johannesburg and Raleigh data centers using automation mesh. Let's have a closer look at the localized execution and route automation mesh used to accomplish this.

```Mesh route info``` uses the automation mesh ```receptorctl``` command line tool to return the status of the ```mesh-exec1``` worker node located in the Johannesburg data center. The job template also displays the path the automation job took to gather the information.
<br>

**Run the ```Mesh route info``` job template using the ```Raleigh DC``` inventory**

* On the side navigation under the **Resources** section, click on **Templates**
* Click on the *rocket icon* under the **Actions** column in the ```Mesh route info``` job template row. This will open a new window
* Keep the ```Raleigh DC``` inventory as the selection
* Click on **Launch**
* Verify in the `Output` window that all the tasks succeeded.

![jt_path_raleigh_output](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jt_path_raleigh_output.png)
<br>

* The job template returned the state of ```automation-controller21```, which is associated with the ```Raleigh DC``` inventory.

* Under the **Print path to mesh node** task, note that the first hop in the path is ```automation-controller21``` before reaching ```mesh-exec1```.

This indicates the job was executed using ```automation-controller21``` which associated with the **Raleigh DC** inventory.
<br>

**Run the ```Mesh route info``` job template using the ```Johannesburg DC``` inventory**
* Follow the steps above used to run the  ```Mesh route info``` job template.
* This time, select the ``Johannesburg DC``` inventory
* Click on **Next** and then click on **Launch**

![jt_path_jhb_output](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_jt_path_jhb_output.png)
<br>

* The job output displays current state of ```mesh-exec1```.
* Under the **Print path to mesh node** task, note that no extra hops were required to reach ```mesh-exec1```

This demonstrates that the execution occurred **locally** in the Johannesburg data center using `mesh-exec1` and not on ```automation-controller21```.
<br>

When you're done with all the steps, click on the `Check` button move to the next challenge.

