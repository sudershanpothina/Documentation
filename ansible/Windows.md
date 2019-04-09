Need powershell 3.0 and asp.net 4.5.2

To verify powershell
```powershell
$PSVersionTable.PSVersion
```
Follow this repo
https://github.com/vipin-k/Ansible-Windows

to install powershell and asp.net run the following powershell script
https://github.com/vipin-k/Ansible-Windows/blob/master/Upgrading%20PowerShell%20and%20.NET%20Framework.ps1

# IF THE SOFTWARES ARE PRESENT YOU CAN NO ACTION REQUIRED MESSAGE
open powershellISE
goto view-> select show script pane
paste the script over there and click on run
make sure to change the username and password

next run the following powershell script
https://github.com/vipin-k/Ansible-Windows/blob/master/ConfigureRemotingForAnsible.ps1
this will enable winrm service
and setup certifacte
and open and configure the port and the firewall settings

run the command below in powershell to verify winrm
```powershell
winrm enumerate winrm/config/Listener
```

create hosts on ansible machine
```
[windows-server]
WINTEST # may have to add the ip in the hosts file

[windows-server:vars]
user=username
password=password
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore
```
run the following command to test it
```
ansible windows-server -i hosts -m win_ping
```
