# openstack-heat-demo
<B> *** This instruction is under construction *** </B>

<H3>Overview</H3>
This repository contains examples of how to use Heat templates in OpenStack. With Heat you can easily deploy a group of resources with one operation, and later remove all the related resources. In Heat terminology such group of resources is called a "stack". And example of a multi-instance stack could be for example deployment of a web-server and database server instance along with the required network connections.

It is up to the creator of Heat templates to decide what resources are considered as baseline already existing in the cloud, and what resources will be created by the Heat template.

<H3>Writing templates</H3>

Documentation for Heat templates is found in <A HREF='http://docs.openstack.org/developer/heat/template_guide/' target="_blank">Heat template guide</A>

One thing to keep in mind when writing the templates is that the Heat template specifications are continuously developed and older versions don't have all the features that newer versions support. The version of the template is written in the first line, for example "heat_template_version: 2014-10-16", but you cannot use newer version than the used OpenStack platform supports.

Tip for usability via GUI: By default the template variables are shown in alphabetical order in the GUI dialogue. However with parameter <I>parameter_groups</I> you can explicitly define the order.

<H3>Deploying stack</H3>
Stacks can be deployed via Horizon GUI, OpenStack CLI or Ansible, giving the yaml-format Heat template as input. The templates typically have variables that are used to define for example name and flavor of instances. Input for the variables can be given via a separate "environment file", as command line parameters or interactively via Horizon GUI.

<H4>Deploying stack with Horizon GUI</H4>
The stacks are managed in Horizon GUI via <I>Project->Orchestration->Stacks</I> page. Clich the <I>Launch Stack</I> button to open a dialogue where you can give the template file and optionally the environment file. The files can be given using any of the following methods:
- Template Source = "File": Upload the file via browser.
- Template Source = "Direct input": Type or copy&paste the template content on the dialogue.
- Template Source = "URL": Let OpenStack controller fetch the file from an external HTTP server in the internet using URL given by the user. When the templates are stored in GitHub, they should be accessed with raw URL like https://raw.githubusercontent.com/SoneraCloud/openstack-heat-demo/master/heat_create_instance_linux.yml

The launch dialogue may have dropdown menus for some items if <I>custom_constraint</I> has been defined for a variable in the template. However all the resource types do not support constraints and then the only possibility is for the user to manually type the resource name.

<H4>Deploying stack with CLI</H4>
Deploying via CLI is done with "heat stack-create" command. Note that the required parameters depend on the used template and this is just an example command:
<PRE>heat stack-create myStack -u https://raw.githubusercontent.com/SoneraCloud/openstack-heat-demo/master/heat_create_instance_linux.yml -P instance_name=testVM1 -P flavor_name=sonera.linux.tiny -P image_name=centos-7 -P keypair_name=my_heat_key -P security_group=my_sec_group -P network_name=my_net</PRE>

Another example using newer OpenStack CLI client:
<PRE>openstack stack create -t https://raw.githubusercontent.com/SoneraCloud/openstack-heat-demo/master/heat_create_instance_linux.yml --parameter instance_name=testVM1 --parameter flavor_name=sonera.linux.tiny --parameter image_name=centos-7 --parameter keypair_name=my_heat_key --parameter security_group=my_sec_group --parameter network_name=my_net myStack</PRE>

You can list existing stacks using "heat stack-list" (or "openstack stack list") and show details of a stack using "heat stack-show |ID|" (or "openstack stack show |ID|").

Delete stack with "heat stack-delete |ID|" or "openstack stack delete |ID|".

<H4>Deploying stack with Ansible</H4>

Refer to <A HREF='http://docs.ansible.com/ansible/os_stack_module.html' target='_blank'>Ansible module for using Heat</A>
Note: Ansible os_stack module requires Ansible version 2.2 or later.

<H3>Troubleshooting</H3>

Stack deployment can fail if for example non-existing resources are referred by the template. Then the stack may end up in semiconfigured state so that only part of the requested resources exist. To troubleshoot what is wrong, you can inspect the error messages found by clicking the resources in <I>GUI->Project->Orchestration->Stacks</I> or CLI command "openstack heat stack show |ID|".
After you find the root cause, delete the stack and try deployment again.


<H3>References</H3>
- <A HREF='http://docs.openstack.org/developer/heat/template_guide/' target="_blank">Heat template guide</A>
- <A HREF='http://docs.openstack.org/cli-reference/heat.html' target='_blank'>Heat CLI reference</A>
- <A HREF='http://docs.ansible.com/ansible/os_stack_module.html' target='_blank'>Ansible module for using Heat</A>




