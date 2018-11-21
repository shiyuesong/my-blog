title: CentOS7 安装 docker
tags: []
categories: []
date: 2018-11-20 07:11:00
---
## Introduction
Docker is an application that makes it simple and easy to run application processes in a container, which are like virtual machines, only more portable, more resource-friendly, and more dependent on the host operating system. For a detailed introduction to the different components of a Docker container, check out [The Docker Ecosystem: An Introduction to Common Components.](https://www.digitalocean.com/community/tutorials/the-docker-ecosystem-an-introduction-to-common-components)

## Prerequisites
* 64-bit CentOS 7 Droplet
* Non-root user with sudo privileges. A CentOS 7 server set up using [Initial Setup Guide for CentOS 7](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7) explains how to set this up.


Note: Docker requires a 64-bit version of CentOS 7 as well as a kernel version equal to or greater than 3.10. The default 64-bit CentOS 7 Droplet meets these requirements.


#### Step 1 — Installing Docker

The Docker installation package available in the official CentOS 7 repository may not be the latest version. To get the latest and greatest version, install Docker from the official Docker repository. This section shows you how to do just that.

But first, let's update the package database:

```
$ sudo yum check-update
```

Now run this command. It will add the official Docker repository, download the latest version of Docker, and install it:

```
$ curl -fsSL https://get.docker.com/ | sh
```

After installation has completed, start the Docker daemon:

```
$ sudo systemctl start docker
```

Verify that it's running:

```
$ sudo systemctl status docker
```

The output should be similar to the following, showing that the service is active and running:

```
docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2016-05-01 06:53:52 CDT; 1 weeks 3 days ago
     Docs: https://docs.docker.com
 Main PID: 749 (docker)
```

Lastly, make sure it starts at every server reboot:

```
$ sudo systemctl enable docker
```

Installing Docker now gives you not just the Docker service (daemon) but also the docker command line utility, or the Docker client. We'll explore how to use the docker command later in this tutorial.

#### Step 2 — Executing Docker Command Without Sudo (Optional)

By default, running the docker command requires root privileges — that is, you have to prefix the command with sudo. It can also be run by a user in the docker group, which is automatically created during the installation of Docker. If you attempt to run the docker command without prefixing it with sudo or without being in the docker group, you'll get an output like this:

```
docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See 'docker run --help'.
```

If you want to avoid typing sudo whenever you run the docker command, add your username to the docker group:

```
$ sudo usermod -aG docker $(whoami)
```

You will need to log out of the Droplet and back in as the same user to enable this change.

If you need to add a user to the docker group that you're not logged in as, declare that username explicitly using:

```
$ sudo usermod -aG docker [username]
```

The rest of this article assumes you are running the docker command as a user in the docker user group. If you choose not to, please prepend the commands with sudo.

