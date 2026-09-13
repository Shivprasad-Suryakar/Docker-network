# Docker-network 
Docker Bridge Network Command 
      **Bridge**  The default network driver.
        
    docker network create -d bridge my-net 
When creating a network, IPv4 address allocation is enabled by default, it can be disabled using --ipv4=false. IPv6 address allocation can be enabled using --ipv6.

    docker network create --ipv6 --ipv4=false v6net 

**host**  Remove network isolation between the container and the Docker host.
        
        docker run -d --network host nginx

**none**  Completely isolate a container from the host and other containers.
                        
        docker run -it --network none alpine
        
**overlay**  Swarm Overlay networks connect multiple Docker daemons together.
Overlay networks are generally used with Docker Swarm:

        docker network create -d overlay overlay-net

Common use
Docker Swarm
Multi-host container communication
Distributed applications
Microservices across multiple Docker servers
**ipvlan ** Connect containers to external VLANs.

**ipvlan **  Containers appear as devices on the host's network.
                        
      docker network create -d ipvlan  --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 my-ipvlan

      | Driver      | Main purpose                             |      Multi-host? | Typical IP     |
| ----------- | ---------------------------------------- | ---------------: | -------------- |
| **bridge**  | Normal container networking              |                ❌ | `172.17.x.x`   |
| **host**    | Share host network                       |                ❌ | Host's IP      |
| **none**    | No networking                            |                ❌ | None           |
| **overlay** | Docker hosts communicate                 |                ✅ | Overlay subnet |
| **ipvlan**  | Containers directly use physical network | Depends on setup | LAN IP         |
| **macvlan** | Containers appear as physical devices    | Depends on setup | LAN IP         |


Subnet Allocation 
                
                docker network create --ipv6 --subnet 192.0.2.0/24 --subnet 2001:db8::/64 mynet

