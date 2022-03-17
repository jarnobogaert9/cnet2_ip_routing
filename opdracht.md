# Computernetwerken II - cnet2

# Lab 4: IP routing

> (base 20220338) - complete your personal information below

date: 10/03/2022

name: Jarno Bogaert

year: 2022

## Design

### IP addresses

> These are the assigned IP address for the different hosts in your network.

| Host                         | IP address                           |
| ---------------------------- | ------------------------------------ |
| workstation1                 | 10.20.100.14                         |
| workstation2                 | 10.20.100.37                         |
| webserver                    | 10.20.100.199                        |
| ftpserver                    | 10.20.100.215                        |
| Host in 12-host network      | 10.20.100.179                        |
| Uplink address on ISP router | 10.20.100.254/<Smallest SN possible> |

### Subnetworks calculated

> Fill in the resulting network information in the table below; use the format as in the theoretical exercises (Linux differs on some points in itâ€™s display).

| Network       | Netmask | Interface |
| ------------- | ------- | --------- |
| 10.20.100.0   | /26     | rout-eth2 |
| 10.20.100.176 | /28     | rout-eth4 |
| 10.20.100.192 | /27     | rout-eth3 |
| 10.20.100.252 | /30     | rout-eth1 |

## Configure the network

### ... the router

> screenshot of the router pinging external node

![Router pinging external node](https://raw.githubusercontent.com/jarnobogaert9/cnet2_ip_routing/main/router_pinging_external_node.png)

### ... the hosts

> What do you need to add on the host to make this work?

You need to add a default gateway on the hosts to be able to ping the router. You also need to configure the interfaces on the router with the correct IP address.

> screenshot of the workstation pinging the webserver

![Workstation pinging webserver](https://raw.githubusercontent.com/jarnobogaert9/cnet2_ip_routing/main/ws_pinging_web.png)

> Your built-up routing table of the company router (ip route output):

![Router routing table](https://raw.githubusercontent.com/jarnobogaert9/cnet2_ip_routing/main/router_routing_table.png)

### ... the ISP router

> Which networks are we missing?

We miss a network which aggregates all our subnets into one network.

In our case we miss the network 10.20.100.0/24

> screenshot of the workstation pinging external node

![Workstation pinging external node](https://raw.githubusercontent.com/jarnobogaert9/cnet2_ip_routing/main/ws_pinging_external_node.png)

> Explain what general rule make the entry match.

It will match with this rule because all the IP addresses from all the hosts in the subnets fall under this big network. What we are doing here is supernetting.

```
10.20.100.0/24 via 10.20.100.253 dev rISP-eth0
```
