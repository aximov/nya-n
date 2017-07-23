---
title: "SSH to lab machines with keypairs"
date: 2017-04-07T18:57:39+09:00
draft: false
tags: [ssh, rsa, lab]
---

For my colleagues.
<!--more-->

## SSH to lab machines using RSA keys

### Make a keypair
First, check if you have any keypair.

```sh
$ ls -a ~/.ssh
```

If you don't see any keypair like `id_rsa` and `id_rsa.pub`, make a new one.

```sh
$ ssh-keygen -t rsa -b 2048
```

### Get inside the firewall
Now connect to a machine. You can do this step either through VPN or from inside the school firewall (indeed they're same in this situation). VPN server name is like `kaguvpn.ed.tus.ac.jp`.

Once gotten inside the firewall, open the [machine list](http://10.33.24.6/analysis/pc_spec/pc_spec.html). Choose one with its location UG. 

### Copy the public key to a server
In this step, stay in the firewall.

Copy your **public** key to `authorized_keys`.

```sh
$ cat ~/.ssh/id_rsa.pub | ssh ${username}@${server_IP_address} "cat >> ~/.ssh/authorized_keys"
```

Replace `${username}` as your name, `${server_IP_address}` as the lab machine's IP address in the list.

Debian asks for your password, so respond to the request.

### Connect with SSH keys
Now you can connect to lab machines using ssh with the keypair (from inside the firewall).

```sh
$ ssh ${username}@${server_IP_address}
```

Well done!