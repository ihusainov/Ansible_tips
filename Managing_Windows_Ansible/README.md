
**Step 1 – Prerequisites:**

**Ansible Control Machine :- On Ansible control machine we need to have python winrm module to be installed.**

```
root@devopstechie$ pip install "pywinrm>=0.2.2"
```
**Windows Machine :- In order for Ansible to manage your windows machines, you will have to enable and configure PowerShell remoting. 
To automate the setup of WinRM, Ansible Team(RedHat) provides examples/scripts/ConfigureRemotingForAnsible.ps1 script. 
We need to run above script on the remote machine in a PowerShell console as an administrator.**

```
powershell.exe -File ConfigureRemotingForAnsible.ps1
```

**Step 2 – Configure / Setup:**

**Once completed the prerequisites setup, you have to do following things to test Ansible Windows machine connection. 
Create /etc/ansible/hosts inventory file, you can add the Windows machines into this file you want to manage./etc/ansible/hosts**

```
[windows]
dc01.devopstechie.local

[windows:vars]
 ansible_user=administrator@DEVOPSTECHIE.LOCAL
 ansible_pass=SecretPasswordGoesHere
 ansible_port=5986
 ansible_connection=winrm
 ansible_winrm_server_cert_validation=ignore
```
**Now by using Ansible win_ping module you can test connection/setup is working**

```
[root@ansible ansible]# ansible windows -m win_ping
dc01.devopstechie.local | success >> {
    "changed": false,
    "ping": "pong"
}
```
