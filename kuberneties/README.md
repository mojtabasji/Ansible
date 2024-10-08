
# Config and install Containerd as container runtime with Ansible


### Step one:

Add the following line to the /etc/apt/sources.list file on the master system

* Note: the following line is for the Kali Linux rolling repository, you can replace it with the repository of your choice

``
deb http://kali.cs.nctu.edu.tw/kali kali-rolling main non-free contrib
``

### step two:

create keys for passwords on ansible vault containing the following keys:
ansible_become_pass: ###     // client sudo password
gateway_ip: ###     // gateway ip

``
ansible-vault create group_vars/all/vault.yml
``

### step 3:

create hosts.ini with following structure:

``
[clients]
client1 ansible_host= <client1_ip>
client2 ansible_host= <client2_ip>
``

### step 4:

Add master public key to the client system authorized_keys file in the following path:

``
~/.ssh/authorized_keys
``

### Finally:

then run the following command to install containerd on the client system

``
ansible-playbook -i hosts.ini config_clients.yml --ask-vault-pass
``
