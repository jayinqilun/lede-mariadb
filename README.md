# LEDE-MARIADB 5.5.57

Your built package:
  
* Linksys WRT ARM 
  * https://cdn.corifeus.com/lede/17.01.3/packages/arm_cortex-a9_vfpv3/mariadb/  

* Like D-Link DIR 860L B1 RAMIPS 
  * https://cdn.corifeus.com/lede/17.01.3/packages/mipsel_24kc/mariadb/


## The router service

Please, where you can find it in  [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia), of course it includes ```init.d``` service as well.


This is if you have ext-root or enough NAND. :)

```bash
mkdir -p /var/lib/mysql
mysql_install_db --force --basedir=/usr
/etc/init.d/mariadb stop|start
```

## Bulding

This is based on:
https://github.com/openwrt/packages/pull/4221 .

It will be in all of my [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia).

### CPU type
Right now, I only test on ARM (Linksys WRT1200ACS, Linksys 3200ACM) and D-Link DIR 860l B1 RAMIPS since it is 5.5.

# The location:  
  
```text
packages/feeds/mariadb/mariadb
```
# To use it


# Build

Clone from GitHub ```patrixk3/lede-insomnia``` repo.

```bash

# either
./run-d-link-dir-860l-b1
# or
./run-linksys-wrt

# then
echo 'src-git mariadb https://github.com/patrikx3/lede-mariadb.git' >> feeds.conf

./scripts/feeds update -a
./scripts/feeds install -a
./scripts/feeds update -a -p mariadb
./scripts/feeds install mariadb

make package/feeds/mariadb/mariadb/{clean,prepare,compile} package/index V=s

```


[//]: #@corifeus-footer

---

[**P3X-LEDE-MARIADB**](https://pages.corifeus.com/lede-mariadb) Build v5.5.35-3 

[![Like Corifeus @ Facebook](https://img.shields.io/badge/LIKE-Corifeus-3b5998.svg)](https://www.facebook.com/corifeus.software) 
 

[//]: #@corifeus-footer:end