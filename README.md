# clustering-rabbitmq

You'll need [this configuration file](https://github.com/rabbitmq/rabbitmq-server/blob/v3.7.x/docs/rabbitmq.conf.example).
 It has to be at `/etc/rabbitmq/rabbitmq.conf`. This is the sysctl newer configuration file format compared to the old style `rabbit.config` file
 
Uncomment out the following section (`lines 400-403`) and replace hostname with lists of RabbitMQ servers.
 
 ```
# cluster_formation.classic_config.nodes.1 = rabbit1@hostname
# cluster_formation.classic_config.nodes.2 = rabbit2@hostname
# cluster_formation.classic_config.nodes.3 = rabbit3@hostname
 ```

**Start all your nodes at the same time**. If you do not start all your RabbitMQ nodes at the same time, they will start in standalone mode and you won't get a cluster.

If you've started Rabbit before configuring clustering, you'll have to stop rabbit and reset it with:

```
rabbitmqctl stop_app; rabbitmqctl reset; rabbitmqctl start_app
```

You can do this for each vagrant box with

```
for node in web haproxy01 repository ; do vagrant ssh ${node} -- "sudo rabbitmqctl stop_app; sudo rabbitmqctl reset; sudo rabbitmqctl start_app" ; done
```
