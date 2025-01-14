[![Latest image layers and size](https://images.microbadger.com/badges/image/bgauduch/cod2server.svg)](https://microbadger.com/images/bgauduch/cod2server/) 
[![Current Docker image version](https://images.microbadger.com/badges/version/bgauduch/cod2server.svg)](https://hub.docker.com/r/bgauduch/cod2server/tags/)
[![Docker Build Status](https://img.shields.io/docker/cloud/build/bgauduch/cod2server.svg)](https://hub.docker.com/r/bgauduch/cod2server/builds/)
[![Docker Pulls](https://img.shields.io/docker/pulls/bgauduch/cod2server.svg)](https://hub.docker.com/r/bgauduch/cod2server/)

# Call of Duty 2 server meets docker
Launch a minimal & lightweight containarized [Call of Duty 2](https://en.wikipedia.org/wiki/Call_of_Duty_2) multiplayer game server.

## Supported tags and respective `Dockerfile` links
* `bgauduch/cod2server:latest` - [Dockerfile](https://github.com/bgauduch/call-of-duty-2-docker-server/blob/master/Dockerfile)
* `bgauduch/cod2server:1.0` - [Dockerfile](https://github.com/bgauduch/call-of-duty-2-docker-server/blob/v1.0/Dockerfile)

## What's inside
Currently it use:

* The `cod2_lnxded_1_3_nodelay_va_loc` server binary from [Killtube](https://killtube.org/showthread.php?1719-Latest-cod2-linux-binaries-(1-0-1-2-1-3)) by **Kung Foo Man**, **Mitch** and anyone that contributed;
* The [custom `libcod`](https://github.com/voron00/libcod) from **Voron00**, follow the repository forks for a complete list of creators and contributors.

Full credits goes to them for their awesome work !

## Prerequisites
You will need the following things:

1. The linux dedicated server binary, which can be found in this repository in the [`bin`](https://github.com/bgauduch/call-of-duty-2-docker-server/tree/master/bin) folder;
1. The orginal game, as it's contents are used by the dedicated server;
1. A host machine of your choice with x86_64 architecture;
1. [Docker](https://docs.docker.com/install/linux/docker-ce/debian/) and [Docker Compose](https://docs.docker.com/compose/install/) installed and configured on your host machine.

## Setup
Clone or download the repository and follow theses steps to get the server up and running:

1. Copy the required data from the game to the server:
    1. Go in the `main` folder of your original game (install directory or retail DVD);
    1. Copy all the `iw_XX.iwd` from 00 to 15 to the `cod2server/main` folder;
    1. Copy all the localizations `localized_english_iwXX.iwd` to the `cod2server/main` (it might be another language).
1. Edit the config file located in `cod2server/main/config.cfg` to suits your needs:
   * **[MANDATORY] Set the RCON password to something strong and private!**
   * Tweak the rest as you see fit, don't forget to updated the placeholders (server name, admin, etc).
1. From the project root, Launch the server:
    ``` bash
    docker-compose up -d
    ```
1. Depending on your setup, you might have some port-forwarding and firewalling to do in order to make your server publicly available.
1. And "voila" ! Availables server commands are listed in [/doc/readme.md](doc/readme.md).

## Server interaction
From the project root, you can:

* Restart the server (to pick up config change for instance):
  ```bash
  docker-compose restart
  ```
* Tail the server logs:
  ```bash
  # cod2_server refer to the name of the service in the compose file
  docker-compose logs -f cod2_server
  ```
* Completely stop the server:
  ```bash
  docker-compose down
  ```

## Troobleshooting
* For `docker-compose` to pick up potential changes in the Dockerfile, force the image build:

  ``` bash
  docker-compose up --build
  ```
* To choose another server binary, symply edit this file in the Dockerfile:
  ```docker
  COPY bin/BINARY_OF_YOUR_CHOICE /bin/cod2_lnxded
  ```

## Notes

* There is a similar repository on github proposing a Call of Duty 2 server based on CentOS: [hberntsen/docker-cod2](https://github.com/hberntsen/docker-cod2)
* A thread on setting up a cod2 server on ubuntu 14.04 is available [on killtube](https://killtube.org/showthread.php?2454-Work-in-progress-Setup-CoD2-on-your-ubuntu-14-04-server)
* This setup was tested on an ubuntu server 18.04.3 LTS x86_64 architecture and should work on any platform with the same architecture.
* You might want to use a separated user to launch your docker containers for security purpose. In this case do not forget to add him to the docker group. On Ubuntu for instance:
  ```bash
  # add user to docker group
  sudo gpasswd -a USER_NAME docker
  # restart docker dameon
  sudo service docker restart
  ```
* Original and cracked server binaries can be found in the [`bin`](https://github.com/bgauduch/call-of-duty-2-docker-server/tree/master/bin) folder, have a look at the `readme`
* The gcc3 library can be found in the [`lib`](https://github.com/bgauduch/call-of-duty-2-docker-server/tree/master/lib) folder, have a look at the `readme`
* If you need to use iptables in conjonction with Docker, please follow the [official documentation tips](https://docs.docker.com/network/iptables/)

## Docker
If you are not familiar with docker (docker engine, docker hub, dockerfiles, docker images and containers), I suggest you have a look at the [documentation](https://docs.docker.com/) (especially the [dockerfiles](https://docs.docker.com/reference/builder/) part).

I also strongly recommend reading the [best practices for writing dockerfiles](https://docs.docker.com/articles/dockerfile_best-practices/) for a better understanding and a cleaner writing of dockerfiles.

[Docker](https://www.docker.com/) is useful, give it a try ;-)

## Roadmap
Project roadmap & issues can be tracked on the [project page](https://github.com/bgauduch/call-of-duty-2-docker-server/projects/2).
