# hardwarespec
Hardwarespec is an easy way to describe server hardware in yaml and test that your specs match.

##Required Software
Hardwarespec requires Ansible to be installed, and uses standard Ansible conventions to describe your servers and run the tests.

##Describing a server
Servers can be described either individually or in groups. Settings for individual servers override the settings from any group they're in.

###Automatic spec generation
You can automatically generate a hardware spec of an existing server by running the command below. Assuming your hosts are in your inventory file and you have SSH keys setup, run the checks with this command:
```
ansible-playbook -i inventory generate_spec.yml -u <user>
```

This generates a yaml configuration file for each server and automatically puts it in the 'host_vars' folder.


###Collecting variable statistics
Using the generation script now collects the following variable information about your fleet. This information is not verified by the 'check' script:

```
cpu_performance
Ping
Download
Upload
cpu_utilization
security_patches
```

Some of this information requires additional tools to be installed. Hardwarespec provides an installer script to setup your hosts:

```
ansible-playbook -i inventory install_tools.yml -u <user>
```

####Describing groups of servers:
Add a new group to your inventory file with the following syntax:

```
[group_name]
host_fqdn.example.com
```

Then create a file in the group_vars directory called group_name.yml (the name of file must match the name of the group in the inventory file)

Using yaml syntax, you can describe any or all of the following values. All variables are optional.

```
cpu_model
cpu_count
cores_per_cpu
total_memory_mb
total_swap_mb
virtualization_type
ipv4_addresses
ipv6_addresses
system_architecture
linux_distribution
distribution_version
fqdn
selinux_status
```

##Running the tests
The tests are run through ansible using the check_hardware playbook. Assuming your hosts are in your inventory file and you have SSH keys setup, run the checks with this command:

```
ansible-playbook -i inventory check_hardware.yml -u <user>
```

If you only want to check a specific group (like 'dev') you can add the -l flag

```
ansible-playbook -i inventory check_hardware.yml -l dev -u <user>
```

The MIT License (MIT)
Copyright (c) 2016 Phil McDonough

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
