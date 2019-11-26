# Bastian host = 요새
https://en.wikipedia.org/wiki/Bastion_host

Instances in VPC are not accessible from outside of the network via ssh. But the admin anyway need to access to servers for the purpose of management. Bastian host enables the admin to access to instances.
Bastian host is a kinda proxy server to acess to private network. To access to instances in VPC, the admin should always be connected to bastian host and run ssh command in it.

## Why is it good?
- This has more security since we can keep other instances as private not allowing ssh from outside of the network.
- We can get all the logs from private subnet in the bastian host.

## Is it always secure?
- No. If a bastian host is attacked, all the things inside of the private network can be in a danger.

## How to access to private instance via Bastian host?
- There are multiple ways to do it. One thing you can do is **SSH Tunneling**
