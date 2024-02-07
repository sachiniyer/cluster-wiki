# Hardware

## Overview

There are four thinkpads and a framework motherboard in my five node k3s cluster. I also have an ec2 instance that acts as my "entrance node" and also headscale control server. I don't include this in the cluster, because it has very little resources.

## Compute

I have a very powerful 40 virtualized cores in this cluster. It may not seem like much, but I paid ~$600 in total (a lot of this comes from the framework motherboard).

#### Thinkpads

The cheapest way to get cores is to buy used thinkpads (to which I am preferential anyway). The four secondary nodes are a thinkpad T410, thinkpad T420 thinkpad T440, and thinkpad x220T. These thinkpads have been semi-reliable for the last year during the formation of this cluster. You can also look into removing the Intel ME as well as installing coreboot if you have a computer that is old enough (the T410s are). The computer will also boot if you short two of the pins in the eDP ribbon connector (which means you can remove the display).

#### Framework Motherboard

The master node used to be a cheap fanless computer. I decided to go with a new fanless computer for the master node to increase reliability a bit more, but this completely backfired. **Don't buy the AWOW Mini PC - AK41. It is super unreliable and sucks**. 

I switched the master node to a [framework](https://frame.work/) and it has been super awesome. It is quite powerful and really made me worry less about my cluster. I don't deal with shutdowns anymore.

#### Why no raspberry pi

I did not use raspberry pis because a lot of my applications do not play nice with arm, and they are extremely expensive right now. In the previous iteration of this cluster I ran a multiarch setup with x86 and arm, and I ran into a lot of weird problems. I decided to avoid the headache and just stick to x86.

## Storage

I don't want to deal with hdds - I removed all of them. Spinning disks are really quite annoying. Each node has an internal ssd boot drive (128 or 256 gb) and three have an external 256gb ssd. In total I have ~1tb of storage available.

## Physical Networking

#### TP Link Access Point

I use a TP Link Router (in AP mode) to both extend my wifi network in my apartment and also connect the nodes. I don't worry too much about networking speeds, but everything is theoretically around gig-speed.

#### TP Link Switch

I also have a small switch that I use for the rest of the machines and some raspberry pis that I have.
