# Hardware

There are two thinkpads and ~~one fanless computer~~ a framework in my 3 node k3s cluster. I also have an ec2 instance that acts as my "entrance node" and also [headscale control server](#sec:Headscale). I don't include this in the cluster, because I want an odd number of nodes. In addition, it does not have much capacity.

## Compute

I have a very powerful 16 virtualized cores in this cluster. It may not seem like much, but I paid \$600 in total (a lot of this comes from the framework).

#### Thinkpads

The cheapest way to get cores is to buy used thinkpads (to which I am preferential anyway). The four secondary nodes are a thinkpad T410, thinkpad T420 thinkpad T440, and thinkpad x220T. These thinkpads have been semi-reliable for the last year during the formation of this cluster. You can also look into removing the Intel ME as well as installing coreboot if you have a computer that is old enough (the T410s are). The computer will also boot if you short two of the pins in the eDP ribbon connector (which means you can remove the display).

#### ~~Fanless Computer from China~~ Framework

~~The master node is a cheap fanless computer. I decided to go with a new fanless computer for the master node to increase reliability a bit more. It is also because there were no T410s on new york craigslist when I was expanding to my last node.~~**Don't buy the AWOW Mini PC - AK41. It is super unreliable and sucks**. I switched the master node to a [framework](https://frame.work/) and it has been super awesome. It is quite powerful and really made me worry less about my cluster. I don't deal with shutdowns anymore.

#### Why no raspberry pi

I did not use raspberry pis because a lot of my applications do not play nice with arm, and they are extremely expensive right now. In the previous iteration of this cluster I ran a multiarch setup with x86 and arm, and I ended up running into a lot of weird problems. I decided to avoid the headache and just stick to x86.

## Storage

I don't want to deal with hdds - I removed all of them. Spinning disks are really quite annoying. Each node has an internal boot drive (128 or 256 gb) and then an external 256gb ssd. In total I have 768gb of storage available.

## Physical Networking

#### TP Link Access Point

I use a TP Link Router (in AP mode) to both extend my wifi network in my apartment and also connect the nodes. I don't worry too much about networking speeds, but everything is theoretically around gig-speed.

#### TP Link Switch

I also have a small switch that I use for the rest of the machines and some raspberry pis that I have.
