+++
title = 'SSH Setup'
date = 2023-11-26T23:48:12+05:45
draft = false
url = "/ssh-setup"
+++

#### Copy the public and private key to the .ssh directory

```bash
cp ~/[filePath]/id_rsa* ~/.ssh/
```

#### Setup config file

```bash
sudo nano ~/.ssh/config
```

#### Config file configuration

```bash
Host acme-server
    HostName 34.231.213.345
    User pratik
    IdentityFile ~/.ssh/id_rsa
```

#### SSH to the server

```bash
ssh acme-server
```
