---
slug: overview
id: wsknw3xi3kvw
type: challenge
title: Automation mesh overview
teaser: Explore automation mesh concepts
notes:
- type: text
  contents: "# \U0001F50E ACME Corp environment overview\n\n![node_overview](../assets/img/mesh_nodes.png)\n\nIn
    this challenge, we'll look at the ACME Corp environment and configuration.\n\n<style
    type=\"text/css\" rel=\"stylesheet\">\nh1,h2{\n  text-align: center;\n}\np {\n
    \ text-align: center;\n}\nimg {\n  display: block;\n  margin-left: auto;\n  margin-right:
    auto;\n  height: 60%;\n\n}\n</style>"
tabs:
- title: Controller
  type: service
  hostname: raleigh-controller
  port: 443
difficulty: basic
timelimit: 600
---

🔐 Login credentials
===
All the logins use the same credentials.

>**Username**:
> ```yaml
>student
>```
>**Password**:
>```yaml
>learn_ansible
>```

👋 Introduction
===

##### ⏰ Estimated time to complete: *5 minutes*

ACME Corp uses Ansible Automation Platform extensively to manage their IT ecosystem across multiple regions.  In this challenge, we’ll review their installation, learn more about mesh worker node types and explore controller instances and instance groups.

>**❗️ Note**
>
>* Perform all tasks in the _Controller_ tab located at the top-left of your browser.
>* If required, log into the automation controller using the provided credentials.
>* You can expand the images by clicking on them for a closer look.

☑️ Task - ACME Corp mesh overview
===

<a href="#mesh_nodes">
  <img alt="Controller login" src="../assets/img/mesh_nodes.png" />
</a>

<a href="#" class="lightbox" id="mesh_nodes">
  <img alt="Amesh_nodes" src="../assets/img/mesh_nodes.png" />
</a>

>ℹ️ Automation mesh provides different worker node types you can use for [control plane](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#control_plane) and [execution plane](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#execution_plane) tasks.
>* **Hybrid nodes** run control plane tasks, such as management jobs, and can execute automation.
>* **Execution nodes** only execute automation ( i.e.. running playbooks ) and don’t run automation controller runtime functions, such as project updates.
>* **Hop nodes**, like jump hosts, don’t run any execution or control plane tasks. They only route traffic to other execution nodes.

##### ACME Corp’s mesh configuration and automation mesh worker node types.

* `raleigh-controller` - Located in the Raleigh data center and configured as a **hybrid node**.

* `jhb-exec` - Located in the Johannesburg remote office and configured as an **execution node**.

* `dublin-hop` - Located in an Irish public cloud region and configured as a **hop node**. `dublin-hop` is *inactive* and is only enabled when a backup worker node is needed. We'll explore this in later tasks.

>**❗️ Note**\
>Automation mesh also provides a **control** node type which only runs controller runtime tasks. Automation execution is disabled. These nodes aren’t used in this lab.

☑️ Task - Controller instances and instance groups
===

>ℹ️ [Instance groups](https://docs.ansible.com/automation-controller/latest/html/userguide/instance_groups.html) let you logically group mesh worker nodes, or instances, together and apply policies to determine how they behave.

##### ✏️ Explore automation controller instance groups.

* Please log in to automation controller using the provided credentials.
* On the side navigation under the **Administration** section, click on **Instance Groups**.
* Click on the `default` instance group.
* Click on the **Instances** tab on the top.

<a href="#default_ig">
  <img alt="Default IG" src="../assets/img/default_ig.png" />
</a>

<a href="#" class="lightbox" id="default_ig">
  <img alt="Defaul IG" src="../assets/img/default_ig.png" />
</a>

The `default` instance group is the default location for all mesh worker nodes and is always present in automation controller. It's used to execute *Job Templates* if no instance group is specified in their configuration.

>**❗️ Note**\
>**Hop nodes** don't run automation jobs and aren’t assigned to instance groups.

* Click on the `jhb-exec` instance and look at the `Node Type`. `jhb-exec` is configured as an **execution node**.

<a href="#jhb-exec">
  <img alt="JHB Exec node" src="../assets/img/jhb_exec_node.png" />
</a>

<a href="#" class="lightbox" id="jhb-exec">
  <img alt="ACME mesh" src="../assets/img/jhb_exec_node.png" />
</a>

* Click on **Instance Groups** under the **Administration** section to return to the main instance group window.
* Click on the `controlplane` instance group.
* Click on the `Instances` tab on the top.

<a href="#control_ig">
  <img alt="Control IG" src="../assets/img/control_ig.png" />
</a>

<a href="#" class="lightbox" id="control_ig">
  <img alt="Control IG" src="../assets/img/control_ig.png" />
</a>

>ℹ️ The `controlplane` instance group is the preselected instance group for all mesh worker nodes that run [control plane](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#control_plane) tasks.

* Click on the `raleigh-controller` instance and look at the **Node Type**. `raleigh-controller` is configured as a **hybrid node**.

<a href="#hybrid_node">
  <img alt="Control IG" src="../assets/img/hybrid_node.png" />
</a>

<a href="#" class="lightbox" id="hybrid_node">
  <img alt="Control IG" src="../assets/img/hybrid_node.png" />
</a>

☑️ Task - Using topology viewer
===
>ℹ️ [Topology viewer](https://docs.ansible.com/automation-controller/latest/html/administration/topology_viewer.html) is a visual, interactive dashboard for automation mesh. It provides a view of node types, health,  and details in your mesh topology.

##### ✏️ Let’s view the ACME Corp mesh design in topology viewer.

* In the **Administration** menu on the left navigation bar, click **Topology View**.

<a href="#topology_viewer">
  <img alt="topology_viewer" src="../assets/img/topology_viewer.png" />
</a>

<a href="#" class="lightbox" id="topology_viewer">
  <img alt="topology_viewer" src="../assets/img/topology_viewer.png" />
</a>

>**❗️ Note**\
>The `dublin-hop` node is currently showing an error status.
>ACME Corp intentionally leaves `dublin-hop` *inactive* as it’s only used as a backup. We’ll explore this feature later in this lab.

* Click on the `jhb-exec` node in the diagram.

<a href="#jhb_exec_topology">
  <img alt="jhb_exec_topology" src="../assets/img/jhb_exec_topology.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_topology">
  <img alt="jhb_exec_topology" src="../assets/img/jhb_exec_topology.png" />
</a>

Topology viewer is an easy way to view the health status of your instances. You can view your instances' health and mesh node type in the top right-hand corner.

You can also drill down into the node configuration by clicking on the instance name.

✅ Next Challenge
===
Press the `Next` button below to go to the next challenge once you’ve completed the tasks.

🐛 Encountered an issue?
====
If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible/instruqt/issues/new?labels=getting-started-mesh&title=Getting+started+with+automation+mesh+issue&assignees=craig-br).

---
slug: multi-site
id: enp79ggq2g3m
type: challenge
title: Multi-site automation using mesh
teaser: Run automation jobs across multiple sites using automation mesh
notes:
- type: text
  contents: "# \U0001F44B Assigning instance groups to ACME Corp inventories\n\n![node_overview](../assets/img/instance_groups_main.png)\n\nIn
    this challenge, we'll assign the mesh execution nodes to different regions by
    associating instance groups to ACME Corp controller inventories.\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1,h2{\n  text-align: center;\n}\np {\n  text-align: center;\n}\nimg
    {\n  display: block;\n  margin-left: auto;\n  margin-right: auto;\n  height: 60%;\n\n}\n</style>"
tabs:
- title: Controller
  type: service
  hostname: raleigh-controller
  port: 443
- title: editor
  type: service
  hostname: raleigh-controller
  path: /editor/
  port: 443
  new_window: true
- title: api
  type: service
  hostname: raleigh-controller
  path: /api/v2
  port: 443
difficulty: basic
timelimit: 600
---
🔐 Login credentials
===
All the logins use the same credentials.

>**Username**:
> ```yaml
>student
>```
>**Password**:
>```yaml
>learn_ansible
>```

👋 Introduction
===

#### ⏰ Estimated time to complete: 10 minutes

Now that we’ve created instance groups for the Raleigh and Johannesburg regions and associated the corresponding instances, we can assign these instance groups to the appropriate ACME Corp controller [inventories](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html).

>**❗️ Note**
>* Perform all tasks in the _Controller_ tab located at the top-left of your browser.
>* If required, log into the automation controller using the provided credentials.
>* You can expand the images by clicking on them for a closer look.

☑️ Task - Assign instance groups to inventories
===

>ℹ️ Instance groups and the associated mesh worker nodes are assigned to automation controller objects, such as _organizations_, _inventories_, and _job templates_.

ACME Corp must assign the correct instance groups to the Johannesburg and Raleigh locations to ensure the closest mesh worker node executes the automation in the respective environments.

##### ✏️ Let’s associate the `Raleigh data center` instance group with the `Raleigh DC` inventory.

* On the side navigation under the **Resources** section, click on **Inventories**.
* Click on the `Raleigh DC inventory`.
* Click on **Edit**.
* Click on the magnifying glass button under **Instance Groups**.
* Check the box next to **Raleigh data center**.
* Click on **Select**.
* Click on **Save** in the **Edit Details** window.

<a href="#raleigh_inv_ig">
  <img alt="raleigh_inv_ig" src="../assets/img/raleigh_inv_ig.png" />
</a>

<a href="#" class="lightbox" id="raleigh_inv_ig">
  <img alt="raleigh_inv_ig" src="../assets/img/raleigh_inv_ig.png" />
</a>

##### ✏️ Let’s do the same for the `Johannesburg data center` instance group and `Johannesburg DC inventory`.

* On the side navigation under the **Resources** section, click on **Inventories**.
* Click on the `Johannesburg DC` inventory.
* Click on **Edit**.
* Click on the _magnifying glass button_ under **Instance Groups**.
* Check the box next to **Johannesburg data center**.
* Click on **Select**.
* Click on **Save** in the **Edit Details** window.

<a href="#jhb_inv_ig">
  <img alt="jhb_inv_ig" src="../assets/img/jhb_inv_ig.png" />
</a>

<a href="#" class="lightbox" id="jhb_inv_ig">
  <img alt="jhb_inv_ig" src="../assets/img/jhb_inv_ig.png" />
</a>

☑️ Task - Selecting where to run your automation
===

ACME Corp IT received reports of slow website response times. They must gather system information from Red Hat Enterprise Linux (RHEL) instances in the Johannesburg remote office and Raleigh data center.

They’ll use the pre-created `Debug info` [job template](https://docs.ansible.com/automation-controller/latest/html/userguide/job_templates.html) to gather information and fault find.

##### ✏️ Let’s execute the `Debug info` job template in the Raleigh data center.

* On the side navigation under the **Resources** section, click on **Templates**.
* Click on the <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> icon under the **Actions** column on the `Debug info` job template row. This will open a new window.

<a href="#debug_info_raleigh">
  <img alt="debug_info_raleigh" src="../assets/img/debug_info_raleigh.png" />
</a>

<a href="#" class="lightbox" id="debug_info_raleigh">
  <img alt="debug_info_raleigh" src="../assets/img/debug_info_raleigh.png" />
</a>

>**❗️ Note**
>
>The `Debug info` job template is configured to ask which inventory to use before launching. Job templates provide the ability to prompt user input for specific parameters before execution. This is useful as we need to run the automation on multiple ACME Corp inventories.

* Keep the `Raleigh DC` inventory as the selection.
* Click on **Next** and then click on **Launch**. This opens the *Job Output* window.

<a href="#debug_info_raleigh_details">
  <img alt="debug_info_raleigh_details" src="../assets/img/debug_info_raleigh_details.png" />
</a>

<a href="#" class="lightbox" id="debug_info_raleigh_details">
  <img alt="debug_info_raleigh_details" src="../assets/img/debug_info_raleigh_details.png" />
</a>

* Click on the **Details** tab on the top of the window

Note that it used the `Raleigh data center` instance group and `raleigh-controller` instance to run the job.

##### ✏️ Next, we’ll run the `Debug info` job template in the Johannesburg region.

* On the side navigation under the **Resources** section, click on **Templates**.
* Click on the <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> icon under the _Actions_ column on the `Debug info` job template row. This will open a new window.

<a href="#debug_info_jhb_inv">
  <img alt="debug_info_jhb_inv" src="../assets/img/debug_info_jhb_inv.png" />
</a>

<a href="#" class="lightbox" id="debug_info_jhb_inv">
  <img alt="debug_info_jhb_inv" src="../assets/img/debug_info_jhb_inv.png" />
</a>

* Select the `Johannesburg DC` inventory.
* Click on **Next** and then click on **Launch**. This will open the *Job Output* window.
* As we did in the previous steps, click on the **Details** tab at the top of the window.

<a href="#debug_info_jhb_details">
  <img alt="debug_info_jhb_details" src="../assets/img/debug_info_jhb_details.png" />
</a>

<a href="#" class="lightbox" id="debug_info_jhb_details">
  <img alt="debug_info_jhb_details" src="../assets/img/debug_info_jhb_details.png" />
</a>

Note that it used the `Johannesburg data center` instance group and the `jhb-exec` instance to run the job.

☑️ Task - Looking under the covers - mesh overlay network
===

Let's look at the route automation mesh used to reach the remote worker nodes and run the `Debug info` job template.

The `Mesh route info` job template uses the automation mesh `receptorctl` command line tool to return the status of the `jhb-exec` worker node in the Johannesburg remote office. The job template also displays the path the automation job took to gather the information.

##### ✏️ Let’s look at the route from the Raleigh data center to `jhb-exec` using the `Mesh route info` job template.

* On the side navigation under the **Resources section**, click on **Templates**.
* Click on the <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> icon under the _Actions_ column in the `Mesh route info` job template row.

<a href="#route_info_launch">
  <img alt="route_info_launch" src="../assets/img/route_info_launch.png" />
</a>

<a href="#" class="lightbox" id="route_info_launch">
  <img alt="route_info_launch" src="../assets/img/route_info_launch.png" />
</a>

* This will open a new window. Keep the `Raleigh DC` inventory as the selection.
* Click on **Next** and then click on **Launch**.

Verify in the `Output` window that all the tasks succeeded.

<a href="#mesh_route_raleigh_path">
  <img alt="mesh_route_raleigh_path" src="../assets/img/mesh_route_raleigh_path.png" />
</a>

<a href="#" class="lightbox" id="mesh_route_raleigh_path">
  <img alt="mesh_route_raleigh_path" src="../assets/img/mesh_route_raleigh_path.png" />
</a>

Under the _Print_ path to mesh node task, note that the first hop in the path is `raleigh-controller` before reaching `jhb-exec`. This indicates that the job was initiated in Raleigh and used the `raleigh-controller` hybrid node to contact the `jhb-exec` execution node.

##### ✏️ Next, run the `Mesh route info` job template using the `Johannesburg DC` inventory.

* Follow the above steps to run the `Mesh route info` job template.
* This time, select the `Johannesburg DC` inventory.
* Click on **Next** and then click on **Launch**.

<a href="#mesh_route_jhb_path">
  <img alt="mesh_route_jhb_path" src="../assets/img/mesh_route_jhb_path.png" />
</a>

<a href="#" class="lightbox" id="mesh_route_jhb_path">
  <img alt="mesh_route_jhb_path" src="../assets/img/mesh_route_jhb_path.png" />
</a>

Under the _Print_ path to mesh node task, note that no extra hops were required to reach `jhb-exec` as we initiated the automation in the Johannesburg remote office.

✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the tasks.

🐛 Encountered an issue?
====
If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible/instruqt/issues/new?labels=getting-started-mesh&title=Getting+started+with+automation+mesh+issue&assignees=craig-br).

<style type="text/css" rel="stylesheet">
  .lightbox {
    display: none;
    position: fixed;
    justify-content: center;
    align-items: center;
    z-index: 999;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 1rem;
    background: rgba(0, 0, 0, 0.8);
    margin-left: auto;
    margin-right: auto;
    margin-top: auto;
    margin-bottom: auto;
  }
  .lightbox:target {
    display: flex;
  }
  .lightbox img {
    max-width: 60%;
    max-height: 60%;
  }
  html {
    font-size: 14px;
  }
  img {
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 100%;
  }
  h1 {
    font-size: 18px;
  }
  h2 {
    font-size: 16px;
    font-weight: 600
  }
  h3 {
    font-size: 14px;
    font-weight: 600
  }
  p {
    font-size: 14px;
  }
  p span {
    font-size: 14px;
  }
  ul li span {
    font-size: 14px
  }
</style>
