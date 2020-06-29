# ansible-vm-automation
VMware VM automation via ansible.


## Future Works

* VM-CREATE 
- After creating a VM, play can store the uuid value of the newly created VM for future plays such as vm-rename or vm-delete.

* VM-RENAME
- After renaming a VM, play should change the hostname (if necessary) and .vmdk name too.
