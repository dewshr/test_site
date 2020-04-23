---
title: "Automatically Upload Files to Remote Server Using Python"
date: 2020-04-18T14:21:45-05:00
description: Upload files daily at specific time to create backup
author: Dewan Shrestha
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: inner
tocLevels: ["h2", "h3", "h4"]
tags:
- paramiko
series:
-
categories:
- syntax
- python
image: images/feature3/code-file.png
---

<br/>

If you have your own server like Synology NAS or have access to other servers, you can write a sctipt in python to upload files to your remote server using python package called **Paramiko**.

I was trying to use function directly from Paramiko using SFTP (Secure File Transfer Protocol) client, but I getting error saying **Channel is closed**. So, I used the scp module from [SCP](https://github.com/jbardin/scp.py). The code given below is what I used to upload my files to the server using python.
```
#!/Users/user_name/opt/anaconda3/envs/py37/bin/python
import paramiko
from scp import SCPClient

#creating ssh client
ssh_client = paramiko.SSHClient()

#when you are logging to server, you can see a message to add key, and you have to select yes.
# this is what the following code is doing
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())

#logging into the server
ssh_client.connect(hostname = '192.168.0.1', port=22, username='user_name',password='password')


scp_client = SCPClient(ssh.get_transport(), socket_timeout=10)



# Uploading 'local_folder' directory and its content in the remote server to path /remote/path/

scp_client.put('local_folder', recursive=True, remote_path='/remote/path/local_folder')


scp_client.close()
ssh_client.close()
```
<br/>


##### Links
- [SCP](https://github.com/jbardin/scp.py)

