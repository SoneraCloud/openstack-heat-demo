# openstack-heat-demo
<B> *** This instruction is under construction *** </B>

<H3>Overview</H3>
This repository contains examples of how to use Heat templates in OpenStack. With Heat you can easily deploy a group of resources with one operation, and later remove all the related resources. In Heat terminology such group of resources is called a "stack". And example of a multi-instance stack could be for example deployment of a web-server and database server instance along with the required network connections.

<H3>Deploying stack</H3>
Stacks can be deployed via Horizon GUI, OpenStack CLI or Ansible, giving the yaml-format Heat template as input. The templates typically have variables that are used to define for example name and flavor of instances. Input for the variables can be given via a separate "environment file", as command line parameters or interactively via Horizon GUI.

The stacks are managed in Horizon GUI via <I>Project->Orchestration->Stacks</I> page. Clich the <I>Launch Stack</I> button to open a dialogue where you can give the template file and optionally the environment file. The files can be given using any of the following methods:
- Template Source = "File": Upload the file via browser.
- Template Source = "Direct input": Type or copy&paste the template content on the dialogue.
- Template Source = "URL": Let OpenStack controller fetch the file from an external HTTP server in the internet using URL given by the user. When the templates are stored in GitHub, they should be accessed with raw URL like https://raw.githubusercontent.com/SoneraCloud/openstack-heat-demo/master/heat_create_instance_linux.yml

Deploying via CLI is done with "heat stack-create" command. Note that the required parameters depend on the used template and this is just an example command:
<PRE>heat stack-create myStack -u https://raw.githubusercontent.com/SoneraCloud/openstack-heat-demo/master/heat_create_instance_linux.yml -P instance_name=testVM1 -P flavor_name=sonera.linux.tiny -P image_name=centos-7 -P keypair_name=my_heat_key -P security_group=my_sec_group -P network_name=my_net</PRE>


<H3>References</H3>
- <A HREF='http://docs.openstack.org/developer/heat/template_guide/' target="_blank">Heat template guide</A>
- <A HREF='http://docs.openstack.org/cli-reference/heat.html' target='_blank'>Heat CLI reference</A>
- <A HREF='http://docs.ansible.com/ansible/os_stack_module.html' target='_blank'>Ansible module for using Heat</A>




