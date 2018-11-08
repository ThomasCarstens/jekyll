---
title: "Deployment for cheapskates"
excerpt: "... using Dokku to deploy web apps and machine learning models on your own PaaS system"
header:
  teaser: assets/images/clouds.jpg
  overlay_image: /assets/images/clouds.jpg
categories:
  - tech
tags:
  - devops
  - cloud
toc: true
toc_sticky: true
date: 2018-11-08
---

Ok, so [Heroku](https://www.heroku.com) is kind of expensive for hobby projects using PaaS ($7/month per dyno) and free instances are deployed on-demand and thus have a nasty start-up delay and autosleep after 30min. As an alternative, let's use [Dokku](http://dokku.viewdocs.io/dokku/) the "Docker powered mini-Heroku". They also have a another nice slogan: "Own Your PaaS. Infrastructure at a fraction of the cost". Sounds good to me. In essence, Dokku gives you your own Heroku. After isntallation you can push Heroku-compatible applications via git. They autobuild using Heroku buildpacks and then run in isolated containers.  

{%
include figure 
image_path="/assets/images/posts/dokku.png" 
alt="Meet dokku" 
caption="Meet dokku: The smallest PaaS implementation you've ever seen"
%}

To host Dokku, there are multiple options and people seem to like [Digital Ocean](https://www.digitalocean.com) who provide a Dokku droplet so you start deploying pretty much right away. But we want to go even cheaper (cheapskate, you know)!  So, as an alternative, I will present a solution that'll cost you about 3 bucks a month and you can potentially host multiple apps with this (depending on your RAM and disk requirement).  

# Start a Virtual Private Cloud instance
So we need a virtual server/ Virtual Private Cloud (VPC) instance to install Dokku. I chose a German hosting company called [Hetzner](https://www.hetzner.de). I use the [base-level CX11 vCPU instance](https://www.hetzner.de/cloud) that features 1 vCPU, 2GB of RAM and 20GB NVMe SSD and plenty of traffic. Then I choose the images' linux system (I opted for [Ubuntu 18.04 LTS](http://releases.ubuntu.com/18.04/)). Next I create a passwordless ssh key and add the public key to the instance.

# Install Dokku
Now we ssh into the instance and first set the hostname (replace the IP and hostname with your info).
```bash
echo "100.100.100.100 dokku.mydomain.net dokku" >> /etc/hosts
```
We also add the dokku repository to the system package control (incl. GPG keys).
```bash
wget -nv -O - https://packagecloud.io/gpg.key | apt-key add
echo "deb https://packagecloud.io/dokku/dokku/ubuntu/ bionic main" \
    > /etc/apt/sources.list.d/dokku.list
```

Then we proceed to update the packages and install docker dependencies.
```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates \
	curl software-properties-common
```

Now we add another repository (this time for docker):  
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable"
```

Finally we install docker-ce and dokku to the system.
```bash
# When asked, select YES to enable web setup
sudo apt-get update
sudo apt-get upgrade

sudo apt-get install docker-ce
sudo apt-get install dokku
```

You now also should have a new user and group *Dokku* in the system
```bash
id dokku
# uid=1000(dokku) gid=1000(dokku) groups=1000(dokku),4(adm),999(docker)
```

If all went well the service should be running by default after the installation (service name: *dokku-installer.service*). To check type this into your terminal:  

```bash
systemctl status dokku-installer.service
systemctl is-enabled dokku-installer.service
```

Finish the installation by adding core dependencies:
```bash
dokku plugin:install-dependencies --core
```

On the machine use the *dokku* command to start and stop apps, see logs and configure things. See the [help pages](http://dokku.viewdocs.io/dokku~v0.12.13/getting-started/installation) here for details.

# Deploy an app
Dokku relies on git for deployment. First, make sure you have a local repository setup on your local machine (i.e. *get init, ...*). Then you need to add a deployment remote where the app will be pushed to (this is your dokku server you just set up). In the command below, *my-app* will also be used by dokku to create your app subdomain when deployed. Thus, the command will host your app at *my-app.mydomain.net* . With git push you simply deploy and trigger a rebuild if the app already exists. **Done.** 

```
git remote add dokku dokku@mydomain.net:my-app
git push dokku master
```

**Note:** For deploying multiple apps you also want a domain hoster that allows you to set [wildcard DNS records](https://en.wikipedia.org/wiki/Wildcard_DNS_record). I started using [Porkbun](https://porkbun.com) for hosting my apps at [http://cwerner.ai](http://cwerner.ai) (note that this address redirects, to see a live app go [here](http://guitars.cwerner.ai)). They are cheap, offer good features (wildcard DNS entires included), and people seem to like them.

A wildcard DNS record looks like this (replace the ip-address with your IP from your VPC instance):  
```
A   *.mydomain.net  100.100.100.100  
```

# Pitfalls
There are some things that you should watch out for.

If you are ever stuck with this error message  
```
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'dokku@mydomain.net:my-app'
```

There a a couple of things you should check:  

## Insufficient memory
Check that your servers' disk and memory are sufficient. I discovered that the Ubuntu 18.04 image has only a small swapfile allocated so I manually increased that to 4GB just to be sure.

```bash
# increase swapfile to 4G
sudo swapoff -a
sudo dd if=/dev/zero of=/swapfile bs=4G count=102
sudo mkswap /swapfile
sudo swapon /swapfile
```

## Insufficient disk space

Docker can really fill up your hard drive. So if you experiment a lot it might also be a good idea to clean up old stuff like so:

Delete volumes:
```bash
# https://github.com/chadoe/docker-cleanup-volumes
docker volume rm $(docker volume ls -qf dangling=true)
docker volume ls -qf dangling=true | xargs -r docker volume rm
```

Delete images:
```bash
# http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images
docker images
docker rmi $(docker images --filter "dangling=true" -q --no-trunc)

docker images | grep "none"
docker rmi $(docker images | grep "none" | awk '/ / { print $3 }')
```

Delete containers:
```bash
# http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images
docker ps
docker ps -a
docker rm $(docker ps -qa --no-trunc --filter "status=exited")
```

If this stuff does not help you might need to upgrade your machine or attach a [volume](https://www.hetzner.de/cloud) to your instance to offload stuff.

# Conclusion
I think this a neat possibility to bring apps to live for cheap and you also learn a bit about PaaS and devops along the way. I will illustrate how to actually build a python based webapp in another post soon.
