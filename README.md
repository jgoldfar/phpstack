# PHPStack - Swiper

PHPStack gives you everything you need for developing PHP/Hack applications locally. The idea came from the need of having an OS-agnostic and virtualized alternative to the great [MNPP](http://getmnpp.org/) stack as regular LAMP stacks quite simply can't keep up with the Nginx + PHP-FPM/HHVM combo in terms of performance. I hope you'll find it as useful an addition to your dev-arsenal as I've found it!

This version of PHPStack has been stripped down a bit to just run the hack FastCGI interpreter and include the Swiper application, for easier deployment.

See also https://github.com/nikolaplejic/docker.hhvm, from where some of the configuration was borrowed.

## What's inside

* [Shipyard](http://shipyard-project.com/) (optional)
* [Nginx](http://nginx.org/)
* [MySQL](http://www.mysql.com/)
* [HHVM](http://www.hhvm.com/)
* [Memcached](http://memcached.org/)

### Requirements

* [Docker](https://docker.com/)
* [Docker Compose](http://docs.docker.com/compose/)

### Instructions

```sh
# Clone the repository, then:
# boot up the Docker containers
$ docker-compose up

# To start shipyard (workaround for container name bug, apparently)
$ docker run --rm -v /var/run/docker.sock:/var/run/docker.sock shipyard/deploy start
```

Once everything is up and running, you can access Shipyard at `http://<IP>:8080`. The default user credentials are `admin:shipyard`. Once logged in, you will need to [add an engine](http://shipyard-project.com/docs/engines/) with an address of `http://<IP>:2375` to see the local containers.

The IP is `127.0.0.1`

---
Copyright &copy; 2014-2015 [Kasper Kronborg Isager](http://github.com/kasperisager). Licensed under the terms of the [MIT License](LICENSE.md).
