# Overview

This is the description of how I created my k3s cluster with tailscale and old thinkpads. I believe that the architecture is somewhat unique, and fits the use case of cheap college kid trying to deal with no public ips and moving all the time. These docs are currently a work in progress, and contain a lot of my musings on the trials and tribulations taken when building this cluster.

## Cheap

I needed this cluster to be somewhat cheap for two reasons. First, I don't have any super high SLA requirements, nor do I really care too much about performance. As such, it is better for me to try and create something that optimizes for price.

## Portable

I tend to move around quite a bit, and it is an absolute pain to set up port forwarding everywhere that I go. I also am not guaranteed access to a public IP wherever I am going. Therefore it is necessary that I am able to move my cluster with ease.

## Secure

The previous version of this cluster used to be accessible by ssh with a 5 letter alpha password. This is just not smart. I wanted to make this cluster slightly more secure and control the traffic that hits the cluster better.

## Based in Open Source

I wanted to try to use open source software for pretty much everything (down to the bios). This was because I wanted to not only support open source projects, but see if I could really run this without having to rely on any proprietary software.

## Resiliency

Ideally I wanted to design something that had non-resilient cheap hardware and a very resilient architecture. I wanted to make sure that the cluster would have a much higher uptime than would be expected of it.

## k3s

I really wanted to make a kubernetes cluster not just to learn, but because it allows me to deploy all of my apps with ease. I also get to keep my data on my machines and overall just have a testing ground for all of my stuff that I do. If I want something to go up, I am not at the mercy of a cloud service.
