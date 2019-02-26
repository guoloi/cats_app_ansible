# cats_app_ansible

On Ubuntu only! Do not work on CentOS.

Using this ansible script you will be able to implement Cats_app on any number of slave Virtual Mashines.

I suppose that:

1) Every VM have Python 2.7 installed (apt install python)
2) There is user "user" on every Slave VM, which is able to escalate privileges using "sudo" command
3) Management VM has ssh access to every Slave VM by key (ssh-copy-id user@Slave_VM_IP)
4) On Management VM ansible is installed (apt install ansible)
5) In case of reboot you have to run script again, or start cats_app manualy 

This script DO NOT install virtual mashines!


# Management VM:
ubuntu-18.04.2

# Slave VM(s)
ubuntu-18.04.2

# Command to run script:
ansible-playbook main.yaml -K
