# Networking

## Overview

This is the heart of this project. The main motivation for remaking this cluster was to create something that I could move from place to place with me very easily, and my networking configuration enables that. Overally, each node connects through a P2P wireguard connection.

```
                        |--> Devocion
                        |--> Sey
Tunnel --> Herkimer --> +
                        |--> Milstead
                        |--> CoffeeProject
```

## Tailscale

### Reasoning for Tailscale

#### What is Tailscale

Wireguard is a way to establish quick p2p encrypted tunnels at a kernel level. Tailscale handles the key orchestration for wireguard. The end result of this is a p2p connection with every other machine in the "Tailnet". Using some fancy port opening stuff, you can also expand your wireguard tunnel through NATs and essentially communicate with every other machine no matter where you are. Each machine gets a Tailscale IP as well as a MagicDNS (an entry in resolv.conf basically).

#### Why Tailscale

When all the nodes of the cluster and machines used for controlling the cluster are in a "Tailnet" together, you essentially have a private network where not only can you access internal service (one of the advertised uses for tailscale), but also machines can talk to each other without worrying about where they are. You can also manage individual nodes without needing to be in the same network. There is no more tricky, finicky, insecure port forwarding.

#### What's Headscale

[Headscale](https://github.com/juanfont/headscale) is an awesome open source project that allows you to self deploy a server with many of the same capabilities as the proprietary Tailscale server. This means that I don't have to worry about a device limit and can keep all keys on my own machines. Since the Tailscale clients are open source, I actually can just use the Tailscale clients to connect to [my headscale instance](https://tunnel.sachiniyer.com) (including the android app).

Another cool thing about Tailscale is that I can still use their DERP and relay servers without issues. Although headscale can be deployed with a DERP server, I found this to be very finicky.

### How do packets move

#### Entrance Nodes

This is the term that I started using for traffic that comes into the cluster. These nodes need a public IP and basically do an nginx `proxy_pass`. I use an ec2 instance for this purpose. I may switch back to a machine with port-forwarding if I find a place that I can get a public IP with.

Another way to do this would be to just configure IP tables to pass the packets from the public IP to the tailscale IP. I don't do this however, because I want to validate it as an HTTP request first. I also prefer to configure nginx and route based on domain name instead of blindly forwarding packets.

You can actually visit a couple of non-cluster machines that are connected to the network through this entrance node, such as my [laptop](https://computer.sachiniyer.com) (if it is up), [Raspberry Pi 1](https://coffeesociety.sachiniyer.com), and [Raspberry Pi 2](https://playground.sachiniyer.com) (both raspberry pis died, so just the laptop is the only thing visible now).

#### Exit Nodes

This is the tailscale term for machines that advertise themselves as being able to forward your traffic through them. I actually use [a rapsberry pi](https://playground.sachiniyer.com) for this purpose (this is not available anymore, cause the pi died). I am working on a good way to integrate Mullvad VPN with Headscale.

#### TLS

Handling TLS is a bit tricky. I prefer to do ssl termination on the cluster or end machine instead of the entrance node itself, This way, I can keep the traffic encrypted while traveling to machine as well as take advantage of cool tools like [cert-manager](https://cert-manager.io/). On nginx, you use a combination of `proxy_pass` and SNI (Server Name Indication) to get your packets going to the right place. You can also configure Traefik (my ingress of choice) and Nginx (my other ingress of choice) to accept `proxy_passed` packets. Also depending on the Load Balancer that you are using, you may have to configure that to accept `proxy_passed` packets as well.

#### Domain Names

Another requirement for this project was to be able to separate internal and external tools. I do this through whitelisting domains at the entrance nodes. Instead of blindly forwarding all the traffic from \*.sachiniyer.com, I instead just forward the tools I want available to the world. Traffic that reaches the entrance nodes with those domains will be allowed into the tailnet. This is handled by a script that reads my dns configuration from AWS Route53.

All traffic with other domains will have to be generated from inside the tailnet. You can make this easier with a quick change to resolv.conf to point traffic from your domain to the magicDNS of the cluster. This results in a clear separation of internal and external tools. You could also configure your dns record to only have the whitelisted domains as well.

### Tips and tricks

As a couple of tips, it can be hard to keep the nginx config consistent among all of your entrance nodes, so what I recommend doing is keeping git as a source of truth, and do a cronjob that pulls from a git repo and automatically updates at whatever frequency that you would like. There may be a better way to do this with webhooks. I would also avoid keeping your nodes in restrictive networks, as this means that they use the relay servers as little as possible and you have faster speeds.

## MetalLB

All my load balancing communication happens through Tailscale MagicDNS. You need to be wary about configuring MetalLB for `proxy_passed` packets. I am considering a switch to cilium because it has a much more interesting design pattern (eBPF-based load balancing).

## Traefik Ingress

I made a similar switch from Nginx to Traefik for the same `proxy_protocol` reasoning. the Nginx ingress was not respecting my `proxy_protocol` packets, and somehow the Traefik ingress was really easy to configure and get working. I also started to like Traefik a lot more because it seems to play better with the more modern versions of kubernetes (> 1.25).

## Cert Manager

Cert Manager is great, and my main reason for doing TLS termination on the cluster instead of the entrance nodes (and also that wildcard certificates are a bit insecure). I integrated cert-manager with Traefik and it works quite well. I love being able to spin up a cert easily and have ssl easily enabled. You can also use dns validation and keep your domains pointed to the Tailscale IPs.


