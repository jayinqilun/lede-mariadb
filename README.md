[//]: #@corifeus-header

  [![Build Status](https://travis-ci.org/patrikx3/lede-mariadb.svg?branch=master)](https://travis-ci.org/patrikx3/lede-mariadb)  [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/patrikx3/lede-mariadb/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-mariadb/?branch=master)  [![Code Coverage](https://scrutinizer-ci.com/g/patrikx3/lede-mariadb/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-mariadb/?branch=master) 

# The LEDE Stable MariaDB 5.5 package

 
                        
[//]: #@corifeus-header:end

It is important that you use ```ext-root```, before you install, since MariaDB is space hungry. If you want to move the defaults, it requires you to program with it. The info is at the bottom. 

## The feed

http://cdn.corifeus.com/lede/17.01.4/packages/arm_cortex-a9_vfpv3/mariadb
```text
src/gz reboot_mariadb http://cdn.corifeus.com/lede/17.01.4/packages/arm_cortex-a9_vfpv3/mariadb
```

http://cdn.corifeus.com/lede/17.01.4/packages/mipsel_24kc/mariadb
```text
src/gz reboot_mariadb http://cdn.corifeus.com/lede/17.01.4/packages/mipsel_24kc/mariadb
```

## Built packages
  
* Linksys WRT ARM 
  * https://cdn.corifeus.com/lede/17.01.4/packages/arm_cortex-a9_vfpv3/mariadb/  

* Like D-Link DIR 860L B1 RAMIPS 
  * https://cdn.corifeus.com/lede/17.01.4/packages/mipsel_24kc/mariadb/


## The router service

Please, where you can find it in  [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia), of course it includes ```init.d``` service as well.


This is if you have ext-root or enough NAND. :)

```bash
# it is important that you might have a conflict if you use 
# some client like php, python or any other mysql client
# libmysqlclient or libmysqlclient-r , so
# opkg remove libmysqlclient 
# opkg remove libmysqlclient-r
opkg install mariadb-server libmariadb mariadb-client-extra 
mysql_install_db --force --basedir=/usr
/etc/init.d/mariadb stop|start
```


## Your own build

```bash
cp feeds.conf.default feeds.conf
echo 'src-git mariadb https://github.com/patrikx3/lede-mariadb.git' >> feeds.conf
./scripts/feeds update -a
./scripts/feeds install -a
./scripts/feeds update mariadb
./scripts/feeds install -a -p  mariadb


# create a .config
# the default is LITE
make menuconfig

# might need as well
make kernel_menuconfig

# either
make package/feeds/mariadb/mariadb/{clean,prepare,compile} package/index V=s

# or
make V=s
```


## Bulding info

This is based on:
https://github.com/openwrt/packages/pull/4221 .

It will be in all of my [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia).

### CPU type
Right now, I only test on ARM (Linksys WRT1200ACS, Linksys 3200ACM) and D-Link DIR 860l B1 RAMIPS since it is 5.5.


# Change the data location

The defaults are ```/opt/var/lib/mysql``` and ```/opt/var/lib/mysql-tmp``` (auto created), but you can configure at ```/etc/mysql/my.cnf``` and ```/etc/init.d/mariadb```. So, if you move the DB location, then you must change ```/etc/init.d/mariadb``` as well as ```my.cnf``` together, since right now it is a symlink. The built-in is ```/var/lib/mysql```, that, you can't change right now, but ```LEDE``` puts it into the ```ROM```, so I created a symlink for ```/var/lib/mysql``` to ```/opt/var/lib/mysql```. That's all.

Given that lots of small devices expect ```/var/lib/mysql``` in the ```ROM``` and you have a different setup, please do not use ```/var/lib/mysql```, otherwise you have to work on it more, but of course if you change the ```my.cnf``` and ```/etc/init.d/mariadb``` any setup can be configured at will. 

[//]: #@corifeus-footer

---

[**P3X-LEDE-MARIADB**](https://pages.corifeus.com/lede-mariadb) Build v5.5.64-89 

[![Like Corifeus @ Facebook](https://img.shields.io/badge/LIKE-Corifeus-3b5998.svg)](https://www.facebook.com/corifeus.software) [![Donate for Corifeus / P3X](https://img.shields.io/badge/Donate-Corifeus-003087.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=LFRV89WPRMMVE&lc=HU&item_name=Patrik%20Laszlo&item_number=patrikx3&currency_code=HUF&bn=PP%2dDonationsBF%3abtn_donate_SM%2egif%3aNonHosted) 


 

[//]: #@corifeus-footer:end