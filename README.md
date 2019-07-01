# AnsibleForWindows
Practice with using ansible to provisioning Windows Server machine

- [x] setup control node for ansible.
- [x] use virtualbox or vagrant to spin Windows Server 2016 Standart (https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016?filetype=ISO)
- [x] Prepare Windows vm by using bootstrap scripts for WinRM
- [x] Create skeleton for Webserver role which install IIS and extra features (using ansible-galaxy init)
- [x] Setup IIS with extra features on the vm using ansible (dont forget to add VM to hosts:) )
Aditional tasks:
- [] Ansible vault is  need to be used.
- [] Configure extra features IIS 

## setup control node for ansible.
Install pip for python 2.7
```$ yum install python2-pip.noarch -y```
Using pip install pywinrm
```$ pip2 install pywinrm```
Install ansible
```$ yum install ansible -y```
## use virtualbox or vagrant to spin ...
Create and install new VM in VirtualBox
## Prepare Windows vm by using bootstrap scripts for WinRM
Enable RDP using PowerShell.
```$ Set-ItemProperty ‘HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\‘ -Name “fDenyTSConnections” -Value 0```
Enable Network Level Authentication
```$ Set-ItemProperty ‘HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\‘ -Name “UserAuthentication” -Value 1```
Allow RDP connections
```$ Enable-NetFirewallRule -DisplayGroup “Remote Desktop”```
Bootstrap Windows machine for ansible access.
Using PowerShell download bootstrap script
```$ wget https://raw.githubusercontent.com/SMILE009/AnsibleForWindows/master/ConfigureRemotingForAnsible.ps1 -OutFile ConfigureRemotingForAnsible.ps1```
Start boostraper script
```$ ./ConfigureRemotingForAnsible.ps1```
Expected output
> Self-signed SSL certificate generated; thumbprint: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
>
>
> wxf                 : http://schemas.xmlsoap.org/ws/2004/09/transfer
> a                   : http://schemas.xmlsoap.org/ws/2004/08/addressing
> w                   : http://schemas.dmtf.org/wbem/wsman/1/wsman.xsd
> lang                : en-US
> Address             : http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous
> ReferenceParameters : ReferenceParameters
>
> Ok.
Now you can check winrm listeners
```$ winrm enumerate winrm/config/Listener```
And WinRM config
```$ winrm get winrm/config/Service```
## Setup IIS with extra...
Edit inventory file
Run ansible to provision Windows Server with IIS and additional page =)
```ansible-playbook main.yml```

