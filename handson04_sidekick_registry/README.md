#"Sidekick" units 

Runs a separate discovery agent next to the main container that is being run.

To keep service registration logic outside of your main codebase, "sidekick" units can be run next to the main systemd unit. Sidekicks will be scheduled by fleet onto the same machine as the main unit and will stop if the main unit stops for any reason. 

Examples of common sidekick containers are for service discovery and controlling external services such as cloud load balancers.

#Handson on "sidekick" units for service discovery

    $fleetctl start *.service
    $fleetctl list-units
    $fleetctl journal -f lb-config-from-container.service

###NOTES 

In vagrant, docker0's ip is 10.1.42.1, while in EC2 and GCE it is 172.17.42.1 

The docker0 IP will be the default gateway inside your container. So it is probably easier to lookup the IP in the container. So do something like the following in your CMD script:
 
    export ETCD=$(ip route get 8.8.8.8 | grep via | awk '{print $3}'):4001


In this handson, lb use `pull` every 5 seconds to detect workers status. But it is better to use etcd's event-handler to do it because push is better than pull.
