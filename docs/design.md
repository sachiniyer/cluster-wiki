# Design Goals

## Overview

Thisa k3s cluster with tailscale and old thinkpads. I believe that the architecture is somewhat unique, and fits the use case of a cheap, portable, and extensible self hosting infrastructure.

## Cheap

This cluster can be cheap for two reasons. First, I don't have any SLA requirements, nor do I really care too much about performance. As such, it is better for me to try and create something that optimizes for price.

## Portable

I tend to move around quite a bit, and it is an absolute pain to set up port forwarding everywhere that I go. I also am not guaranteed access to a public IP wherever I am going. Therefore it is necessary that I am able to move my cluster with ease.

## Secure

The previous version of this cluster used to be accessible by ssh with a 5 letter alpha password. This is just not smart. I wanted to make this cluster slightly more secure and tightly control the traffic that hits the cluster.

## Based in Open Source

I wanted to try to use open source software for pretty much everything (down to the bios). This was because I wanted to not only support open source projects, but see if I could really run this without having to rely on any proprietary software.

## Resiliency

Ideally I want to design something that had non-resilient cheap hardware with a very resilient architecture. I want to make sure that the cluster would have a much higher uptime than would be expected of any individual components.
