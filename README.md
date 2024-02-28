# consul-work

A brief consul PoC

# 1.How to build the servers?

## 1.1 Build Docker

Open a terminal and type the command below to build docker:

```
docker_compose up -d
```

Then, in another terminal, type the command below to build server_01:

```
docker exec -it consul_server_01 sh
```

Now, you should verify your docker ip address with the command:

```
ifconfig
```

## 1.2 Build Consul Server

Perform the Bind and build the consul server (In this example, my docker IP was 172.20.0.2):

```
mkdir /var/lib/consul
mkdir /etc/consul.d
```

```
consul agent -server --bootstrap-expect=3 -node=consul_server_01 -bind=172.20.0.2 -data-dir=/var/lib/consul -config-dir=/etc/consul.d
```

Do the same with consul_server_02 and consul_server_03:

```
docker exec -it consul_server_02 sh
```

```
mkdir /var/lib/consul
mkdir /etc/consul.d
```

```
consul agent -server --bootstrap-expect=3 -node=consul_server_02 -bind=172.20.0.3 -data-dir=/var/lib/consul -config-dir=/etc/consul.d
```

## 1.3 Bind Consul Servers in cluster

On one server, perform the bind using the IP of the other server.
E.g: At server with ip 172.20.0.2, you should type:

```
consul join 172.20.0.3
```

Therefore, on the third server, just link it to any of the other two.
