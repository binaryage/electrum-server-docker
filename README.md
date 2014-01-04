# Docker-ized Electrum server

[Electrum](http://electrum.org) is a great light-weight Bitcoin client. It connects to dozen servers provided by enthustiasts.

This is an easy way how to run your own Electrum server and help to diversify Bitcoin infrastructure.

# Installation

#### Prerequisities

* grab some VPS (tested Digital Ocean with Ubuntu 13.10) - min 30GB disk, 2GB mem
* [install Docker](https://www.docker.io/gettingstarted/#h_installation)
* don't worry about losing containers, all esential data will be persistent in main host filesystem
  * technically essential data folders will be mapped via docker volumes to `/var/lib/electrum-server-docker/*`
    * bitcoind's database, electrum's data, leveldb and cerificates

#### Installation

Following script will build and add two new containers in your docker:

1. electrum-bitcoind ([bitcoind](https://github.com/bitcoin/bitcoin) with mapped database to host's `/var/lib/electrum-server-docker/bitcoind`)
2. electrum-server ([electrum-server](https://github.com/spesmilo/electrum-server) with mapped database to host's `/var/lib/electrum-server-docker/electrum/*`)

Steps:

    git clone git@github.com:binaryage/electrum-server-docker.git
    cd electrum-server-docker
    touch .env
    echo "export BITCOIND_RPC_USER=some_user" >> .env
    echo "export BITCOIND_RPC_PASSWORD=some_password" >> .env
    ./do setup
    ./do build
    ./do run

Note: Inspect etc/env and see more overrides you can add to your custom .env

##### Stop

    ./do stop

##### Start

    ./do start

##### Upgrade

    ./do stop
    git pull
    ./do build
    ./do rm
    ./do run

## Credits

* Docker is awesome!
* Electrum guys rock
* Inspiration from [srid's discourse-docker](https://github.com/srid/discourse-docker)

[Licensed under MIT](LICENSE)