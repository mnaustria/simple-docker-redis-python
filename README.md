# simple docker redis python application

---

## Build Application

Build the docker image manually by cloning the git repository

> \$ git clone https://github.com/mnaustria/simple-docker-redis-python.git

> \$ docker build -t mnaustria/myapp:v0.1 .

## Create Redis Container

> \$ docker run -d --name redis redis:latest

## Run the application linking to redis container

Create a container from the image.

> \$ docker run -d -p 5000:5000 --link redis --name myapp mnaustria/myapp:v0.1

Notes:

'-d' to allow the container from the background

'-p' to expose the port

Now Visit http://localhost:5000

## Verify the container mapping by checking the /etc/hosts

> \$ docker exec -it myapp more /etc/hosts

    127.0.0.1       localhost
    ::1     localhost ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters
    172.17.0.4      redis 4692dd04e9d6
    172.17.0.3      b972aacbf008

## Check the container IP

> \$ docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' redis

    172.17.0.4

## Check the container hostname

> \$ docker inspect -f '{{ .Config.Hostname }}' redis

    4692dd04e9d6
