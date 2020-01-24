# Dockerized Wetty for CoreOS CLIs
[![](https://badge.imagelayers.io/centurylink/coreos-cli-wetty.svg)](https://imagelayers.io/?images=centurylink/coreos-cli-wetty:latest 'Get your own badge on imagelayers.io')

This image provides a [Wetty](https://github.com/krishnasrinivas/wetty) terminal
with access to the following CoreOS command-line tools:

* `docker`
* `fleetctl`
* `etcdctl`

## NOTE

This repo is no longer being maintained. Users are welcome to fork it, but we make no warranty of its functionality.

## docker
The Docker CLI requires access to the `docker.sock` in the host OS in order to communicate with the Docker daemon.
To provide access to the `docker.sock` you need to mount it into the container using the `-v` flag:

    docker run -p 3000:3000 \
      -v /var/run/docker.sock:/var/run/docker.sock \
      centurylink/coreos-cli-wetty

## fleetctl
The Fleet CLI communicates with the Etcd API over HTTP. The Etcd endpoint is specified by setting the
`FLEETCTL_ENDPOINT` environment variable. The default value is http://10.1.42.1:4001 (10.1.42.1 is
typically the IP address of the `docker0` interface in CoreOS) but can be overriden with
the `-e` flag on the `docker run` command if necessary.

    docker run -p 3000:3000 \
      -v /var/run/docker.sock:/var/run/docker.sock \
      -e FLEETCTL_ENDPOINT=http://17.1.0.10:4001 \
      centurylink/coreos-cli-wetty

## Wetty
Once the container is running, the Wetty terminal can be accessed by browsing to [http://localhost:3000]
(assuming 3000 was the port mapping you chose when starting the container) with your Chrome browser. Login
with username `term` and password `term`.
