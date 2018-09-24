# Docker Swarm with Caddy router

Our target run multiple stacks on one or more nodes

In this example we have 3 stacks: 
- router
- s1
- s2

Upload all this on node in ```/var/www/```

Run on node1 

```
docker swarm init
docker network create -d overlay routing
docker stack deploy -c /var/www/s1/docker-compose.yml s1
docker stack deploy -c /var/www/s2/docker-compose.yml s2
docker stack deploy -c /var/www/router/docker-compose.yml router
```

Now you able access any service on any stack from router by name [STACK]_[SERVICE].  
Example: ```s1_whoami```
If you have multiply instance of service you get round robin access.


If you want add more nodes, get token on main node by command:
```
docker swarm join-token worker
```

You will get something like this
```
docker swarm join --token SWMTKN-1-1ebjoptn25tnkehnqxipyv2y1mrw0j2qw5rk6tzdlfw79cieho-auppuzfnzokv2l7hgls7udl48 192.168.1.26:2377
```

Run this on other nodes