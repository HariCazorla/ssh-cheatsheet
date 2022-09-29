# ssh-cheatsheet
Repository to maitain coomonly used ssh commands

## Local Port Forwarding: Make remote resources accessible on your local machine
For example, let’s say you want to access a database server at your office/university which sits behind a firewall. For security reasons, that database server is only configured to accept connections from the local network. But if you can ssh into the server from local machine, then it is possible to access the same service from local machine by port-forwarding.

```
ssh -L local_port:remote_address:remote_port username@server.com
```

### Usecase: 
We have K8s cluster behind a fire wall, and we have RabbitMQ on the K8s. We want to access the RabbitMQ Management dashboard from local machine.
1. First ssh into the K8s node, run 
```
kubectl port-forward svc/rabbitmq-cluster 15672:15672
```

2. Now create a ssh tunnel between local machine and K8s node
```
ssh -L 15672:localhost:15672 shree@ssh.uni.com
```

3. That's it, now you can access the RabbitMQ dashboard at http://localhost:15672


