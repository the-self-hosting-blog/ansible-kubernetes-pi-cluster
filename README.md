[![The Self Hosting BLog](https://dcbadge.vercel.app/api/server/fc5qMhkE)](https://discord.gg/fc5qMhkE)
[![TheSelfHostingBlog](https://forthebadge.com/images/badges/built-with-love.svg)](https://theselfhostingblog.com/)

# Introduction

This playbook will install and set up a kubernetes cluster on raspberry pi's using k3s. It will then enable and install Portainer onto the machine.

# Set-up

This playbook is designed to work with the following:

- A cluster of Raspberry Pi 4's (minimum 2)
- Pi's running Ubuntu 20.04
- You have ansible set up and communicating with your cluster

# Steps

The steps this playbook takes are as follows:

K3s cluster only:

1. Update and upgrade the hosts
2. Update hostname
3. Enable c-groups
4. Reboot
5. Curl & execute k3s install script for master node
6. Extract node-token from the master node
7. Run the worker node install on the other hosts
8. Add portainer to the master node
9. Reboot

# Prerequisites

Please ensure you have a inventory file with a collection that looks like so:

```yml
[picluster]
server_ip new_hostname=pi-one
server_ip new_hostname=pi-two
server_ip new_hostname=pi-three
server_ip new_hostname=pi-four
```

pi-one will be used as the main node and should be placed at the top of the group list as shown above

# Issues & Feedback

If you have any issues running the playbook or any feedback (good or bad!), please dont hesitate to reach out to us on our discord where one of us will be more than happy to help you!

When I was building this playbook I ran into some issues where my router wouldn't return the new hostname for the pi's. If you do get issues it's worth double checking that you can ping using the hostname. K3s seems to fail silently if it can't reach the master node so I had to change step 007 to use an IP address like so:

```diff
- ...K3S_URL=https://pi-one:6443...
+ ...K3S_URL=https://10.1.1.1:6443...
```

But as long as your router isn't weird like mine you should be fine!
