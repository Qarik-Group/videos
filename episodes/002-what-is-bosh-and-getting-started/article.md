>BOSH is an open source tool for release engineering, deployment, lifecycle management, and monitoring of distributed systems. - http://bosh.io/

In this tutorial we get started with a local version of BOSH called [bosh-lite](https://github.com/cloudfoundry/bosh-lite) and start to introduce some of the concepts, terminology and commands.

<iframe src="https://player.vimeo.com/video/167593972? quality=720p" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
But first, why BOSH?

We're being asked to operate an increasing number of increasingly complex systems. We have to make changes with increasing frequency, across an increasing number of data centres/cloud regions. All the while we have increasing user base with increasingly critical business objectives.

BOSH is a project that unifies release engineering, deployment, and lifecycle management of small and large-scale cloud software. BOSH can provision and deploy software over hundreds of VMs. It also performs monitoring, failure recovery, and software updates with zero-to-minimal downtime.

## Getting started

Thanks to [Maria Shaldibina](https://github.com/mariash) for writing a great [Learn BOSH](http://mariash.github.io/learn-bosh/) guide. In this episode we start Maria's tutorial.

It all begins with running a local-only version of BOSH on your computer, called [bosh-lite](https://github.com/cloudfoundry/bosh-lite)...

```
vagrant init cloudfoundry/bosh-lite
vagrant up
```

That's right. You will need Vagrant, Virtualbox, and also a relatively new version of Ruby installed (try https://rvm.io).

Install the BOSH CLI and target our local bosh-lite:

```
gem install bosh_cli
bosh target 192.168.50.4
```

Now that we have a running BOSH (our local bosh-lite) and our CLI is targeting it, we can run BOSH deployments.

## What is a BOSH deployment?

Each BOSH deployment is one or more running servers with interesting processes running, that combine together to make an interesting system.

There are three main components to a BOSH deployment:

* BOSH stemcell - used when creating server VMs/containers
* BOSH releases - bespoke software and dependencies
* BOSH manifest - how to combine the above to provision and configure running servers
