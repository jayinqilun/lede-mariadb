[//]: #@corifeus-header

## The LEDE Stable MariaDB 5.5 package

---
                        
[//]: #@corifeus-header:end
# Create package

```bash
rm build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/mariadb* -rf
rm build_dir/target-mipsel_24kc_musl-1.1.16/mariadb* -rf
rm feeds/mariadb* -rf
./scripts/feeds update -a
./scripts/feeds install -a

# once you already updated the all
./scripts/feeds install mariadb
./scripts/feeds update -a -p mariadb

make package/feeds/mariadb/mariadb/{clean,prepare,compile} package/index V=s
```
[//]: #@corifeus-footer

---

[**P3X-LEDE-MARIADB**](https://pages.corifeus.com/lede-mariadb) Build v5.5.49-71 

[![Like Corifeus @ Facebook](https://img.shields.io/badge/LIKE-Corifeus-3b5998.svg)](https://www.facebook.com/corifeus.software) 
 

[//]: #@corifeus-footer:end