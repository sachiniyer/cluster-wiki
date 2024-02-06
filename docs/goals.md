# Future Goals

## DONE move master node

~~The machine that the master node is on right now became unstable, so I need to figure out a way to migrate that over to something more stable.~~

## TODO more reliable Headscale

Currently Headscale is deployed on bare metal which is okayish. However, I would much rather it be deployed in a docker container, or spun up with docker-compose or something with a bit more fault tolerance.

## TODO ec2 autoscaling

I want to integrate autoscaling with ec2 instances for when I am really out of compute on the cluster. This is going to take a lot of work however, because I will need to figure out a way to automate the addition of a node to the Tailnet, as well as figure out how to automate the addition of a node the k3s cluster. These are both very possible, but a little bit hard to do super securely.

## TODO Move entrance node

I want to move the entrance node off of the ec2 instance into another node that has a public IP. I think that this is a little better cost wise, and means I am fully not dependent on AWS. I will need a public IP for this to work however.

## DONE Add two more nodes

~~I quickly reach the maximum limits of this cluster, and I think that it would be prudent to start planning for the addition of two more nodes~~

## TODO Better Storage

~~I think it will be nice to add some better storage to this system. The current storage capabilities are alright, but~~ it would be nice to do intermittent backups to the cloud as well as potentially add even more capacity. ~~SSDs do not cost much these days.~~

## TODO Integrate Wireguard Key Management into k3s

~~Lastly, the by far most ambitious improvement would be to move the headscale control server functionality into k3s and handle it natively. This would require a lot more work and system design, but I think it could be interesting to actually make wireguard tunnels through k3s native system design. I will have to think a lot more about this though.~~ - *UPDATE* seems to be [done](https://www.netmaker.org/blog/deploy-distributed-kubernetes-clusters-with-wireguard-and-netmaker) by someone already.

