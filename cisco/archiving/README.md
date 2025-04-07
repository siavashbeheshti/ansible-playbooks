# Schedule Cisco config backups with archive
This simple Ansible Playbook configure archiving on Cisco IOS. Cisco IOS routers and switches are able to create **snapshots** of their configuration using the archive feature. Cisco calls these snapshots **configuration archives** and they are very useful as it allows you to store multiple versions of your configuration. Using this Ansible Playbook you can store your **configuration archives** in a FTP server.

## FTP Information
You can change FTP informations such as credentials and path in archiving-playbook.yaml file. In **vars** section you can enter your desired configurations for your FTP server.

**Note**: The FTP path that you enter should be already created on FTP server. 

```
# FTP Server information
  vars:
    ftp_information:
      username: ftpusername
      password: ftppassword
      path: ftp://10.10.10.10/Backup/$h/$t
```

## Ansible SSH Authentication
You can change ssh authentication information in group_vars directory. 
```
ansible_network_os: ios
ansible_user: cisco
ansible_password: cisco123
ansible_connection: network_cli
ansible_become: true
ansible_become_method: enable
```
Ansible uses the ansible-connection setting to determine how to connect to a remote device. When working with Ansible Networking, set this to an appropriate network connection option, such as network_cli, so Ansible treats the remote node as a network device with a limited execution environment. Without this setting, Ansible would attempt to use ssh to connect to the remote and execute the Python script on the network device, which would fail because Python generally isn’t available on network devices.

**Note**: Having plain text passwords in the configuration file is **NOT** recommended. I recommend you to encrypt the password using Ansible Vault.
