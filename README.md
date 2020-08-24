# EPICS Archiver Appliance Configuration Environment for CentOS 7
Forked from Han Lee's repo which covers CentOS 8, Debian and Docker.
This fork is only supporting CentOS 7.

Configuration Environment for EPICS Archiver Appliance at <https://github.com/slacmshankar/epicsarchiverap>

## Download source code first

```bash
make init
```

## Install required packages

```bash
make install.pkgs
```

## Build

Generate all configuration files, prepare the storage space and build the archiver appliance

```bash
make build
```

which contains three rules such as `conf.archapplproperties`, `conf.storage`, and `build.ant`


### Tomcat 9
The user `tomcat` must already exist:
  
    sudo useradd -M tomcat


### MariaDB

* JDBC connector

It is inside the site specific building procedure, so don't need to do anything.

* Create the DB and itsuser : `archappl`

If the MariDB has already `admin` account, please use it with the modification in `configure/CONFIG_COMMOM`.
With the admin account, create `db` and `user` for the archiver appliance.

```bash
make db.create
```

If one cannot get results properly by `make db.show`, please run `make addAdmin`. Thus, from scratch, one should do

```bash
make db.secure
make db.addAdmin
make db.show
make db.create
make db.show
```

* Create and fill the tables

```bash
make sql.fill
make sql.show
```

Please see [docs/README.mariadb.md](docs/README.mariadb.md) for the further information.

### JAVA and Ant
Wget Java 11 jdk and install in /opt


```bash
make build
make install
make sd_start
make sd_status
```


### Systemd

```bash
make sd_start
make sd_status
```
