# Welcome to the Qlico documentation

Qlico is an open-source project that makes it easier to run your (web) project
inside Docker, at the moment it’s just a set of configuration files.

It aims to accelerate development teams by using Docker in their development
workflow by using a hassle-free Docker stack.

## Why should I use Qlico instead of X?

* Easy configuration, just pick the parts you'll need
* Easy to use your own configuration files
* Easy to extend
* Close to the default `docker-compose` experience but everything is tested
* When using `qlico` in a team, you can use defaults in your project
  configurations, for example `postgres13` for PostgreSQL 13, `percona8` for
  Percona 8, etc.

## Prerequisites

* [Docker >= 26.0](https://docs.docker.com/get-docker/){:target="_blank"}
* [docker-compose >= 2.27.0](https://docs.docker.com/compose/install/){:target="_blank"}
* [dnsmasq (optional, but recommended)](dnsmasq.md)
* Basic knowledge of Docker and Docker Compose<br>
  If you don't have any experience with Docker (yet), 
  here are some starter resources, to get you up to speed:
    * [Docker Get Started](https://docs.docker.com/get-started/){:target="_blank"} (You can skip "Share the application part" you do not need a Docker Hub account)
    * [Docker for beginners](https://docker-curriculum.com/){:target="_blank"} (You do not need Amazon Web Services, just skip all the AWS Parts)

## Best Docker experience

* If you are using Windows, we would like to recommend
  using [Docker Desktop with WSL2](https://www.docker.com/products/docker-desktop/){:target="_blank"}.
* If you are using macOS, we would like to recommend
  using [OrbStack](https://orbstack.dev/){:target="_blank"}
* If you are
  running [Arch Linux, see this excellent wiki page](https://wiki.archlinux.org/title/docker){:target="_blank"}
* If you are running Linux, please use the see the Docker documentation for your
  distribution.
    * [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/){:target="_blank"}
    * [Debian](https://docs.docker.com/install/linux/docker-ce/debian/){:target="_blank"}
    * [CentOS](https://docs.docker.com/install/linux/docker-ce/centos/){:target="_blank"}
    * [Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/){:target="_blank"}

## Getting started

To start using Qlico please use the [Quick start](quick-start.md).

## History

Qlico started as a "side" project in 2017, we were using multiple Dockerfiles (for
PHP 5, PHP 7, etc.), and mounting all the projects inside one webserver (Apache).
This was really slow (on macOS), and it was not possible to change the PHP
version per project, all the projects were using php5, php7 or something else
depending on the url.

This has helped us to adopt Docker in our development workflow, but after a
while the old stack was not maintainable anymore, that's
when [Tom](https://github.com/TomKeur){:target="_blank"} decided to create a new
stack with a smaller footprint, and easier to update.

Qlico was born.

## The name Qlico?

In the Netherlands there are plastic trash cans, called Kliko's. Because these
are "containers", and we're using a lot of containers inside of
Docker/Kubernetes, the name Qlico was used. Since naming things is hard ;-).

> There are only two hard things in Computer Science: cache invalidation and
> naming things.

> -- Phil Karlton

[Picture of Kliko's](https://nl.wikipedia.org/wiki/Minicontainer#/media/Bestand:Kliko_op_Bonaire,_Nederlandse_Antillen_-_IMG_8372.JPG)

## Qlico in production?

Qlico can be used in development and in production. Just use the `prod` stage of
the `Dockerfile` inside your project.
Multiple companies are running Qlico in production (in a Kubernetes cluster)
without any problems!
If you need help, you can always contact [Tom](https://github.com/TomKeur){:target="_blank"} 
or [start a GitHub Discussion](https://github.com/qlico/qlico/discussions){:target="_blank"}

## Contributing

Qlico is open-source, you are more than welcome to contribute to this project!
Fork and make a Pull Request, or create an Issue if you see any problem (even
typos or spelling mistakes and grammer improvements are welcome).

## Stargazers

If you like using Qlico, please star
the [Qlico GitHub project](https://github.com/qlico/qlico).
