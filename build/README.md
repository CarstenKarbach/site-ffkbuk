# Build gluon with this configuration

## Motivation
Deploy freifunk node in Cologne on Archer C7 v5.
Official support only available for Archer C7 v2.
Solution: site config from Cologne, but use some config from Bonn from https://github.com/ff-kbu/site-ffkbu-bonn-v2/releases/tag/v2018.2.x-fastd

see https://kbu.freifunk.net/wiki/index.php?title=KBU_Gluon_Firmware for inspiration

## Get gluon and site configuration
```
git clone https://github.com/freifunk-gluon/gluon.git
cd gluon
git checkout v2018.2.x
rm -r site || true
git clone git@github.com:CarstenKarbach/site-ffkbuk.git site
cd site
git checkout v2018.2
```

## Prepare build environment based on Ubuntu
```
cd build
docker-compose build 
docker exec -it build_deb_1 bash
```

## Within container, build gluon
```
cd /etc/gluon
make clean GLUON_TARGET=ar71xx-generic || true
make update
make clean GLUON_TARGET=ar71xx-generic || true
make update
make -j8 GLUON_TARGET=ar71xx-generic GLUON_BRANCH=stable BROKEN=1
make manifest GLUON_BRANCH=stable GLUON_PRIORITY=0

exit # Leave container
```

## Save output images
```
mkdir images
docker cp build_deb_1:/etc/gluon/output/images images/

docker-compose down
```

## Example images
see images/factory
- Archer C7 v4 and v5

## Deploy on your system
Archer example:
Use these steps: https://forum.ffrn.de/t/archer-c7-v5-mit-tftp-flashen/3243