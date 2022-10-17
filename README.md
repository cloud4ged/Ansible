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


# Some Ansible Adhoc commands

```python
ansible -m ping all
```

```python
ansible-inventory --list all    #Command to show the inventory file in json format with metadata on how ansible is reading your host file
```

```python
ansible all --list-hosts        # Command lists all the hosts names given in inventory irrespective of their group
```

```python
ansible -m ping Web     # To ping the servers listed only in Web group
```

```python
ansible -m ping App     # To ping the servers listed only in App group
```

```python
ansible -m shell -a "apt update" all –become   		# --become is used to run the command as sudo user and module shell to run shell commands
```
```python
ansible-playbook SSHkeyPush.yaml --private-key=~/ansible/key.pem    	#This command can be used to run a playbook using private key authorization>
```

git commands
Intial
```git
git init -b main  ## to initiate a repository in current directory in main branch
git add . ## to add all the files to queue
git commit -m “<message you want to enter for commit>”
git pusht
```