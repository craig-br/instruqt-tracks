---
slug: playground
id: dt3d6hbcq5ol
type: challenge
title: Automation mesh playground
teaser: Test your mesh skills in this challenge!
notes:
- type: text
  contents: "# Automation mesh playground\n<br>\n\n<p align=\"center\">\n  <img width=\"400px\"
    src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_map_dbn.png\">\n</p>\n<br>\n\nThe
    last challenge is to recap what we've covered in this lab. You will configure
    the ACME Corp automation mesh using what we've learnt in the previous exercises.\n\nACME
    Corp need to run the ```Debug info``` job template in the Johannesburg data center.
    However, Johannesburg is unreachable from the Raleigh data center due to a network
    outage.\n\n\n<style type=\"text/css\" rel=\"stylesheet\">\nh1 {\n\ttext-align:
    center\n\t}\n</style>"
- type: text
  contents: "# Key takeaways and next steps\n<br>\n\n<p align=\"center\">\n  <img
    width=\"400px\" src=\"https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_logical.png\">\n</p>\n<br>\nAutomation
    mesh provides a simple and robust framework to scale automation from single-site
    deployments to installations spanning the globe with a security-first approach.\n\nWith
    its flexible, multi-directional communication layer and native peering capabilities,
    you can reach further with improved reliability and less sensitivity to latency
    and connection disruptions.\n\n## Where to go next\n* Reach out to your [local
    Red Hat team](https://www.redhat.com/en/contact) to find out more about Ansible
    Automation Platform\n* Find out more about the [Ansible Automation Platform 2.1
    release](https://www.ansible.com/blog/introducing-red-hat-ansible-automation-platform-2.1)\n*
    Sign up for an [Ansible Automation Platform trial](https://www.redhat.com/en/technologies/management/ansible/try-it?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW)\n*
    Visit the Automation mesh [official documentation](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html/red_hat_ansible_automation_platform_automation_mesh_guide/index)
    for more technical details\n\n\n\n<style type=\"text/css\" rel=\"stylesheet\">\nh1
    {\n\ttext-align: center\n\t}\n</style>"
tabs:
- title: Controller UI
  type: service
  hostname: automation-controller21
  port: 443
difficulty: basic
timelimit: 900
---
# Your assignment
### *Estimated time: 15 minutes*

**Controller login credentials:**<p>
*User*: admin <p>
*Password*: ansible123!

> **Note**<p>
>
> All tasks are performed in the automation controller UI.<p>
> Log into automation controller dashboard using the credentials above.


## Automation mesh playground

In this last exercise, you'll configure the ACME Corp automation mesh! This exercise provides less guidance on how to perform the necessary configuration.

Alternatively, please feel free to use the time to explore automation controller and automation mesh.

> **Note**<p>
>
> There are no checks for this exercise. You can click on the **Next** button at the bottom right of the screen to complete the lab at any time.


## Lab scenario

![playground_scenario](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/mesh/mesh_map_dbn.png)
<br>

The ```mesh-exec1``` worker node, located in the Johannesburg data center is currently unreachable from the ACME Corp Raleigh head office. A secondary network link exists via the **Dublin data center** located in Ireland.

The ACME Corp IT team needs to run the ```Debug info``` job template on ```1.johannesburg.example.com``` located in the Johannesburg data center.

## Lab environment

**Preconfigured inventories and associated hosts:**
* ```Johannesburg DC``` inventory contains the  ```1.johannesburg.example.com``` host
* ```Raleigh DC``` inventory contains the ```1.raleigh.example.com``` host
* ```Dublin DC``` inventory contains the ```	mesh-hop1.dublin.example.com``` host

**Automation mesh worker nodes**
* ```automation-controller21``` is configured as a **hybrid node** in the Raleigh data center
* ```mesh-exec1``` is configured as an **execution node** in the Johannesburg data center.
* ```mesh-hop1``` is configured as a **hop node** in the Dublin data center.
<br>

## Your tasks

**Create instance groups and associate with inventories**
* Create the ```Raleigh data center``` instance group and associate the ```automation-controller21``` instance with the instance group
* Configure the ```Raleigh DC``` inventory to use the ```Raleigh data center``` instance group.
* Create the ```Johannesburg data center``` instance group and associate the ```mesh-exec1``` instance with the instance group
* Configure the ```Johannesburg DC``` inventory to use the ```Johannesburg data center``` instance group.

**Configure ```mesh-hop1``` in the Dublin data center**
> **Note**<p>
>
> Feel free to run the ```Mesh route info``` job template during the exercises to see how automation mesh creates new peer connections.
>
* Execute the ```Setup Dublin hop node``` job template to configure ```mesh-hop1``` as a hop node.

**Run the ```Debug info``` job template**
* Run the ```Debug info``` job template using the ```Johannesburg DC``` inventory and associated ```mesh-exec1``` execution node.

**Congratulations on completing the lab!**
<br>

# Key takeaways
**Automation mesh** provides a simple and robust framework to scale automation from single-site deployments to installations spanning the globe with a security-first approach.

With its flexible, multi-directional communication layer and native peering capabilities, you can reach further with improved reliability and less sensitivity to latency and connection disruptions.
<br>

# Where to go next
* Reach out to your [local Red Hat team](https://www.redhat.com/en/contact) to find out more about Ansible Automation Platform
* Find out more about the [Ansible Automation Platform 2.1 release](https://www.ansible.com/blog/introducing-red-hat-ansible-automation-platform-2.1)
* Sign up for an [Ansible Automation Platform trial](https://www.redhat.com/en/technologies/management/ansible/try-it?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW)
* Visit the Automation mesh [official documentation](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html/red_hat_ansible_automation_platform_automation_mesh_guide/index) for more technical details
<br>

When you're done with all the steps, click on the `Next` button move to the next challenge.

