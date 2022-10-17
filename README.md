## Ansible Installation and Setup <br />
- Sudo apt update <br />
- Sudo apt ansible <br />

Once the installation is done check version to verify the installation <br />
- ansible --version <br />

Create a new folder with name ansible in /etc directory
And then create file named “hosts” this is where ansible automatically detects the host inventory file. We can also create our inventory file at any custom path and mention the path while running 

Like below
```python
[Web]
server1 ansible_host=ip-172-31-34-141.ap-south-1.compute.internal
server2 ansible_host=ip-172-31-47-223.ap-south-1.compute.internal

[App]
app1 ansible_host=ip-172-31-38-250.ap-south-1.compute.internal ansible_ssh_private_key_file=~/ansible/key.pem #given private key path in the inventory itself
app2 ansible_host=ip-172-31-33-53.ap-south-1.compute.internal ansible_ssh_private_key_file=~/ansible/key.pem #given private key path in the inventory itself
```
Or
```python
[Web]
web1 ansible_host=ip-172-31-34-141.ap-south-1.compute.internal
web2 ansible_host=ip-172-31-47-223.ap-south-1.compute.internal

[App]
app1 ansible_host=ip-172-31-38-250.ap-south-1.compute.internal
app2 ansible_host=ip-172-31-33-53.ap-south-1.compute.internal

#We are giving all the common variables under all:vars group to avoid rework all the time
[all:vars]
ansible_ssh_private_key_file=~/ansible/key.pem
```

Playbook to Push the SSH key generated in the master server

[SSHkeypush.yml](playbooks/SSHkeypush.yml)
