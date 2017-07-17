# Simple local Docker Cluster Orchestrated by Swarm
Create the Swarm
```bash
$ docker-machine create --driver virtualbox manager
$ docker-machine create --driver virtualbox worker
```

Init the swarm and assigne the  worker to the manager
```bash
$ docker-machine ssh manager "docker swarm init"
$ docker-machine ssh worker "docker swarm join --token <TOKEN> --ip <MANAGER_ID>"
```

Copy compose file into the manager
```bash
$ docker-machine scp docker-compose.yml manager:~
```

Start the stack
```bash
$ docker-machine ssh manager "docker stack deploy -c docker-compose.yml letsdistribute"
```

Check the stack's status
```bash
$ docker-machine ssh manager "docker stack ps letsdistribute"
```

Go to visualizer website
http://managegerIP:8080

You should see running containers

Finally check the website. 
http://managerip

Every time you refresh you should see different host ip address. 