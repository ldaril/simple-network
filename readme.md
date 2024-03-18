# Build simple network

[Instructions](https://github.com/becodeorg/BXL-k4MK4r-2/blob/8fe4db3fedb80874d4be9d9cd27282aadcdf4f71/content/01.Network/00-Network_basics_(Pretraining)/projects/Build_simple_network.md)

## Material 

- 1 switch (Cisco 2960 with Cisco IOS version 15.0(2) image lanbasek9 or similar)
- 3 PCs (Windows 10)
- Three Ethernet cables

## IP addressing table

We are given the IP addressing scheme for the PCs ,we add the router IP address.

| Devices | LAN | IP | Mask |
|---------|-----|----|------|
| PC-Robert | Eth | 192.168.1.10 | 255.255.255.0 | 
| PC-Camille | Eth | 192.168.1.11 | 255.255.255.0 |
| PC-Renaud | Eth | 192.168.1.12 | 255.255.255.0 |
| Router0 | Eth | 192.168.1.1 | 255.255.255.0 |


### Switch connections

Switch is connected to PCs and routers with copper straight cables.

| Interface | Connecté à |
|--------|----------|
| f0/1 | PC-Robert |
| f0/2 | PC-Camille |
| f0/3 | PC-Renaud |
| g0/1 | Router0 |


### Router configuration

In the CLI of the router:

```
Router>enable
Router#
Router#configure terminal.
Router(config)#interface GigabitEthernet0/0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#no shutdown
```

### Connecting to internet

To connect to the internet, we add another router connected to the first router with serial cable and a server connected to the router with crossover cables.

We assign an IP address to the router and server: 

| Devices | Interfaces | IP | Mask |
| --- | --- | --- | --- |
| PC-Robert | f0 | 192.168.1.10 | 255.255.255.0 | 
| PC-Camille | f0 | 192.168.1.11 | 255.255.255.0 |
| PC-Renaud | f0 | 192.168.1.12 | 255.255.255.0 |
| Router0 | g0/0/0 | 192.168.1.1 | 255.255.255.0 |
| Router0 | g0/0/1 | 192.168.2.1 | 255.255.255.0 |
| Router1 | g0/0/0 | 192.168.2.2 | 255.255.255.0 |
| Router1 | g0/0/1 | 192.168.3.1 | 255.255.255.0 |
| Server1 | f0 | 192.168.3.2 | 255.255.255.0 |

We add default gateway 192.168.2.1 to server1 and static routes on router0 and router1.
+ Router0 192.168.3.0/24 via 192.168.2.2	
+ Router1 192.168.1.0/24 via 192.168.2.1

