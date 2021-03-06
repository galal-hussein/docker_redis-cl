Redis Cluster with Docker
=========================

This is a docker image of Redis node that starts in cluster mode and listen on port 7000 waiting to join the cluster, also there a simple fig.yml file to start 6 nodes.

## Building The Image
```
# git clone https://github.com/galal-hussein/docker_redis-cl.git
# docker build -t redis_node docker_redis-cl/
```
## Running Redis Nodes
```
# cd /docker_redis-cl
# fig up -d
```

## Starting The Cluster
To start the cluster you should specify the address of each redis node, to do that you should fetch the ip addresses of the created redis nodes using docker inspect:
```
# docker inpect <container-name> | grep "IPAdress"
```
Then to start the cluster:
```
# docker exec <any-node> ./src/redis-trib.rb create --replicas 1 \
<node1>:7000 <node2>:7000 \
<node3>:7000 <node4>:7000 \
<node5>:7000 <node6>:7000 
```

## Start Nodes with Different port
To start each node with different port change the value of the environment variable $REDIS_NODE_PORT during running the node or in the fig.yml file.
```
docker run -e"REDIS_NODE_PORT=6000" --name node1 -d redis_node 
```
