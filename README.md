# ansible-vm-automation
VMware VM automation via ansible.
This playbook can do the following:

- create
- rename
- delete
- poweroff
- poweron
- rebootguest
- shutdownguest
- suspend

The playbook has extra variables for user to set it later or to use it in AWX or some kind of user forms. (e.g ManageIQ)

# USAGE

- **VM-CREATE**

*If network_type=dhcp*

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_datacenter=<vm_datacenter> vm_name=<vm_name> vm_folder=<vm_folder> vm_template=<vm_template_name> vm_notes=<vm_notes> vm_cluster=<vm_cluster> hot_add_cpu=<true_or_false> hot_remove_cpu=<true_or_false> hot_add_memory=<true_or_false> cpu=<cpu_in_number> mem_mb=<memory_in_mb> disk_size=<disk_size_in_gb> vm_disk_type=<vm_disk_type> vm_datastore=<vm_datastore> vm_port_group=<vm_port_group> network_type=<network_type> task=create"`

*If network_type=static*

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_datacenter=<vm_datacenter> vm_name=<vm_name> vm_folder=<vm_folder> vm_template=<vm_template_name> vm_notes=<vm_notes> vm_cluster=<vm_cluster> hot_add_cpu=<true_or_false> hot_remove_cpu=<true_or_false> hot_add_memory=<true_or_false> cpu=<cpu_in_number> mem_mb=<memory_in_mb> disk_size=<disk_size_in_gb> vm_disk_type=<vm_disk_type> vm_datastore=<vm_datastore> vm_port_group=<vm_port_group> network_type=<network_type> vm_ip=<static_vm_ip> netmask=<netmask> dns_server1=<dns_server1> dns_server2=<dns_server2> network_gateway=<network_gateway> task=create"`

- **VM-RENAME**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> new_vm_name=<new_vm_name> task=rename"`

- **VM-DELETE**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> task=delete"`

- **VM-POWERON**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> task=poweron"`

- **VM-POWEROFF**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> task=poweroff"`

- **VM-RESTART**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> task=restart"`

- **VM-REBOOTGUEST**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> task=reboot"`

- **VM-SHUTDOWNGUEST**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> task=shutdown"`

- **VM-SUSPEND**

`ansible-playbook -i <inventory_name> automate.yml -e "vcenter_hostname=<vcenter_hostname> vcenter_username=<vcenter_username> vcenter_password=<vcenter_password> vm_uuid=<vm_uuid_in_vmware> task=suspend"`

## Usage Notes

* You can always set extra variables to a default value. In this case you can set your vcenter_hostname, vcenter_username and vcenter_password to default values. But I don't recommend using passwords in plain text. You should use a secret.
* There is a validate_certs in variables, this variable is set to 'False' by default. You can enable this variable either using in command line or editing through tasks.
* When deleting virtual machines, the VM should be poweredoff. You can force the delete operation but I didn't set a variable to force operation. Because you shouldn't force vCenter to delete a running VM.
## Future Works

**VM-CREATE** 
- After creating a VM, play can store the uuid value of the newly created VM for future plays such as vm-rename or vm-delete.

**VM-RENAME**
- After renaming a VM, play should change the hostname (if necessary) and .vmdk name too.
