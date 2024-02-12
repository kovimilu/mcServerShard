# Minecraft multi-server - server/dimension

<br>

What I would like to achive is to have 3 seperate servers, each running just one dimension (overworld, nether, end), where you can seemlessly go between them with nether and end porals.

The nether-overworld 1:8 ratio (for travel) and nether portal creation is very very importnt to me. I don't want to use commans ingame like you would in a MultiVerse server.

<br>
<br>

## Why do this?

-  __Performance__

<br>

## Why not just have a better server or increase the resources of the hosting server?


#### Simple explination: 
Big server = loud. Pi cluster = not loud.

<br>

#### More detailed explanation:
I want to run this on a Raspberry Pi 4 cluster, in k3s. My nodes have 4 CPUs and 8GBs or RAM. Giving more then 

    resources:
        limits:
            memory: "7.5Gi"
            cpu: "7000m"

resources to deployment is pointless, since one pod can only run on one node. (I left 1GB of RAM and 0.5 CPU for the cluster overhead)

My first thought was to increase the replicas, but that wouldn't work either since minecraft server in not staless, so the servers would not be in sync.

My second thoughs was to use *stateful sets* with mounting then to the same volume. I have not tried this yet.

Then when i was searching for i found something that pequed my interest.
https://www.spigotmc.org/threads/nether-and-overworld-on-seperate-servers.405573/

so i thought that since you don't really interact with others from different dimension, a possible performance increasing solution could be to have the 3 dimensions in 3 different servers, disabling the other 2 realms that are not in use in each server. 
