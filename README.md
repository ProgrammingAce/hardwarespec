# hardwarespec
Hardwarespec is an easy way to describe server hardware in yaml and test that your specs match.

##Required Software
Hardwarespec requires Ansible to be installed, and uses standard Ansible conventions to describe your servers and run the tests.

##Describing a server
Servers can be described either individually or in groups. Settings for individual servers override the settings from any group they're in.

##Automatic generation
You can automatically generate a hardware spec of an existing server by running the command below. Assuming your hosts are in your inventory file and you have SSH keys setup, run the checks with this command:
> ansible-playbook -i inventory generate_spec.yml

This generates a yaml configuration file for each server and automatically puts it in the 'host_vars' folder.

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
> ansible-playbook -i inventory check_hardware.yml

If you only want to check a specific group (like 'dev') you can add the -l flag
> ansible-playbook -i inventory check_hardware.yml -l dev
