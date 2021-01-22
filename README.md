# docker-example
A simple example showing how to run Husarnet Client inside a Docker container.

Tested on host system:
```
  Operating System: Ubuntu 20.04.1 LTS
            Kernel: Linux 5.4.0-62-generic
      Architecture: x86-64
    Docker version: 19.03.8, build afacb8b7f0
```


## build

Make sure `init-container.sh` is executable. If not:
```bash
sudo chmod +x init-container.sh
```

```bash
sudo docker build -t docker-example .
```

## run

create `.env` file in the project main folder with your Husarnet credentials, eg.:
```
JOINCODE=fc94:b01d:1803:8dd8:2222:3333:1234:1234/xxxxxxxxxxxxxxxxxxxxx
HOSTNAME=mydevice1
```

and run:

```bash
sudo docker run --rm -it \
--env HOSTNAME='my-container-1' \
--env JOINCODE='fc94:b01d:1803:8dd8:3333:2222:1234:1111/xxxxxxxxxxxxxxxxx' \
-v my-container-1-v:/var/lib/husarnet \
-v /dev/net/tun:/dev/net/tun \
--cap-add NET_ADMIN \
--sysctl net.ipv6.conf.all.disable_ipv6=0 \
docker-example
```

After running a container you should see a log like this:

```bash
docker-example$ sudo docker run --rm -it --env HOSTNAME='my-container-1' --env JOINCODE='fc94:b01d:1803:8dd8:b293:5c7d:7639:1111/xxxxxxxxxxxxxxxxx' -v my-container-1-v:/var/lib/husarnet -v /dev/net/tun:/dev/net/tun --cap-add NET_ADMIN --sysctl net.ipv6.conf.all.disable_ipv6=0 docker-example

⏳ [1/2] Initializing Husarnet Client:
waiting...
waiting...
waiting...
waiting...
success

🔥 [2/2] Connecting to Husarnet network as "my-container-1":
[693849] joining...
[695852] joining...
done

*******************************************
💡 Tip
To SSH your container execute in a new terminal session:

ssh johny@fc94:2106:8423:68d7:695e:f6cf:8130:c059

(default password is "johny" as well)
*******************************************
```

This simple container runs SSH server and you can access it from a level of other devices in the same Husarnet network. You don't even have to install Husarnet Client on your host machine!
