#
# Copyright (C) 2017 Lucian Cristian
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mariadb
PKG_VERSION:=10.2.9
PKG_RELEASE:=1

# might to remove the PKG_HASH
# ./scripts/feeds update mariadb
# make package/feeds/mariadb/mariadb/download V=s
# make package/feeds/mariadb/mariadb/check FIXUP=1 V=s
# cat package/feeds/mariadb/mariadb/Makefile | less
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=\
	http://ftp.hosteurope.de/mirror/archive.mariadb.org/$(PKG_NAME)-$(PKG_VERSION)/source/ \
	https://mirror.netcologne.de/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)/source/ \
	https://mirror.lstn.net/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)/source/ \
	http://lon1.mirrors.digitalocean.com/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)/source/ \
	http://ftp.kaist.ac.kr/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)/source/ \
	http://ftp.utexas.edu/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)/source/
#PKG_HASH:=12e0a01c52591ee77cf0f940fe65df024457fa16c70f08c6116048d576096124
PKG_MAINTAINER:=Lucian Cristian <lucian.cristian@gmail.com>, Patrik Laszlo <alabard@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_BUILD_DEPENDS:=mariadb/host libncurses libreadline
HOST_BUILD_DEPENDS += mariadb/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(INCLUDE_DIR)/host-build.mk

define Package/libmariadb
  SECTION:=libs
  CATEGORY:=Libraries
ifdef CONFIG_mariadb_LITE
  DEPENDS:=+libstdcpp +zlib +libpthread +libncurses +libreadline +libopenssl
else
  DEPENDS:=+libstdcpp +zlib +libpthread +libncurses +libreadline +libopenssl
endif
  TITLE:=MariaDB 10 client library
  URL:=http://mariadb.org/
  PROVIDES:=libmysqlclient libmysqlclient-r mariadb
  CONFLICTS:=libmysqlclient libmysqlclient-r
endef

define Package/mariadb/Default
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=mariadb
  TITLE:=MariaDB 10
  URL:=http://mariadb.org/
  SUBMENU:=database
endef

define Package/mariadb
  $(call Package/mariadb/Default)
  DEPENDS:=+libmariadb
  MENU:=1
endef

define Package/mariadb/description
 One of the most popular database servers. Made by the original developers of MySQL.
 Until mysql version is in tree, don't forget to link your applications against libmariadb, not libmysqlclient!
endef

define Package/mariadb-client
  $(call Package/mariadb/Default)
  TITLE+= client applications
  DEPENDS+=+libmariadb +coreutils
endef

define Package/mariadb-client-extra
  $(call Package/mariadb/Default)
  DEPENDS+=+mariadb-client
  TITLE+= additional client applications
endef

define Package/mariadb-server/config
	menu "Select additional options"
	depends on PACKAGE_mariadb-server
	config mariadb_LITE
		bool "Mariadb server lite, 10M vs 30M compressed"
		default y
		help
			Don't add plugins and other storage engines
	endmenu
endef

define Package/mariadb-server
  $(call Package/mariadb/Default)
  TITLE+= server
ifdef CONFIG_mariadb_LITE
  DEPENDS+=+libmariadb +libpcre +resolveip
else
  DEPENDS+=+libmariadb +libpcre +resolveip +libgnutls +liblzo +libbz2 +libxml2
endif
  PROVIDES:=mysql-server
  CONFLICTS:=mysql-server
endef


CMAKE_OPTIONS += -DSTACK_DIRECTION=+1
CMAKE_OPTIONS += -DPLUGIN_TOKUDB=NO
CMAKE_OPTIONS += -DWITHOUT_AUTH_PAM=1
ifdef CONFIG_mariadb_LITE
CMAKE_OPTIONS += -DCONC_WITH_SSL=OFF
CMAKE_OPTIONS += -DCONC_WITH_UNITTEST=OFF
CMAKE_OPTIONS += -DCONNECT_WITH_LIBXML2=OFF
CMAKE_OPTIONS += -DCONNECT_WITH_ODBC=OFF
CMAKE_OPTIONS += -DCONNECT_WITH_VCT=OFF
CMAKE_OPTIONS += -DCONNECT_WITH_XMAP=OFF
CMAKE_OPTIONS += -DCONNECT_WITH_ZIP=OFF
CMAKE_OPTIONS += -DENABLE_PROFILING=OFF
CMAKE_OPTIONS += -DPLUGIN_DAEMON_EXAMPLE=NO
CMAKE_OPTIONS += -DPLUGIN_DIALOG_EXAMPLES=NO
CMAKE_OPTIONS += -DPLUGIN_ROCKSDB=NO
CMAKE_OPTIONS += -DCONNECT_WITH_JDBC=OFF
CMAKE_OPTIONS += -DWITHOUT_PBXT_STORAGE_ENGINE=1
#CMAKE_OPTIONS += -DPLUGIN_ARIA=NO
#CMAKE_OPTIONS += -DUSE_ARIA_FOR_TMP_TABLES=OFF
CMAKE_OPTIONS += -DPLUGIN_ARCHIVE=NO
CMAKE_OPTIONS += -DPLUGIN_AUDIT_NULL=NO
CMAKE_OPTIONS += -DPLUGIN_AUTH_0X0100=NO
CMAKE_OPTIONS += -DPLUGIN_AUTH_ED25519=NO
CMAKE_OPTIONS += -DPLUGIN_BLACKHOLE=NO
CMAKE_OPTIONS += -DPLUGIN_CLIENT_ED25519=NO
CMAKE_OPTIONS += -DPLUGIN_CONNECT=NO
CMAKE_OPTIONS += -DPLUGIN_DEBUG_KEY_MANAGEMENT=NO
CMAKE_OPTIONS += -DPLUGIN_EXAMPLE=NO
CMAKE_OPTIONS += -DPLUGIN_EXAMPLE_KEY_MANAGEMENT=NO
CMAKE_OPTIONS += -DPLUGIN_FEDERATED=NO
CMAKE_OPTIONS += -DPLUGIN_FEDERATEDX=NO
CMAKE_OPTIONS += -DPLUGIN_FEEDBACK=NO
CMAKE_OPTIONS += -DPLUGIN_FILE_KEY_MANAGEMENT=NO
CMAKE_OPTIONS += -DPLUGIN_FTEXAMPLE=NO
CMAKE_OPTIONS += -DPLUGIN_HANDLERSOCKET=NO
CMAKE_OPTIONS += -DPLUGIN_LOCALES=NO
CMAKE_OPTIONS += -DPLUGIN_METADATA_LOCK_INFO=NO
CMAKE_OPTIONS += -DPLUGIN_MROONGA=NO
CMAKE_OPTIONS += -DPLUGIN_PARTITION=NO
CMAKE_OPTIONS += -DPLUGIN_PERFSCHEMA=NO
CMAKE_OPTIONS += -DPLUGIN_QA_AUTH_CLIENT=NO
CMAKE_OPTIONS += -DPLUGIN_QA_AUTH_INTERFACE=NO
CMAKE_OPTIONS += -DPLUGIN_QA_AUTH_SERVER=NO
CMAKE_OPTIONS += -DPLUGIN_QUERY_CACHE_INFO=NO
CMAKE_OPTIONS += -DPLUGIN_QUERY_RESPONSE_TIME=NO
CMAKE_OPTIONS += -DPLUGIN_SEMISYNC_MASTER=NO
CMAKE_OPTIONS += -DPLUGIN_SEMISYNC_SLAVE=NO
CMAKE_OPTIONS += -DPLUGIN_SEQUENCE=NO
CMAKE_OPTIONS += -DPLUGIN_SERVER_AUDIT=NO
CMAKE_OPTIONS += -DPLUGIN_SIMPLE_PASSWORD_CHECK=NO
CMAKE_OPTIONS += -DPLUGIN_SPHINX=NO
CMAKE_OPTIONS += -DPLUGIN_SPIDER=NO
CMAKE_OPTIONS += -DPLUGIN_TEST_SQL_DISCOVERY=NO
CMAKE_OPTIONS += -DWITH_INNODB_EXTRA_DEBUG=OFF
CMAKE_OPTIONS += -DWITH_INNODB_LZ4=OFF
CMAKE_OPTIONS += -DWITH_INNODB_BZIP2=OFF
CMAKE_OPTIONS += -DWITH_INNODB_LZMA=OFF
CMAKE_OPTIONS += -DWITH_INNODB_LZO=OFF
CMAKE_OPTIONS += -DWITH_INNODB_SNAPPY=OFF
CMAKE_OPTIONS += -DWITH_MARIABACKUP=OFF
CMAKE_OPTIONS += -DWITH_WSREP=OFF
CMAKE_OPTIONS += -DWITH_UNIT_TESTS=OFF
CMAKE_OPTIONS += -DWITHOUT_XTRADB=1
#CMAKE_OPTIONS += -DWITH_EXTRA_CHARSETS=none
CMAKE_OPTIONS += -DWITH_EXTRA_CHARSETS=complex
CMAKE_OPTIONS += -DWITH_SAFEMALLOC=OFF
CMAKE_OPTIONS += -DWITHOUT_AUTH_TEST_PLUGIN=1
endif
CMAKE_OPTIONS += -DIMPORT_EXECUTABLES=$(HOST_BUILD_DIR)/host/import_executables.cmake

define Host/Patch/Default
endef

define Host/Compile
	( mkdir $(HOST_BUILD_DIR)/host/ ; cd $(HOST_BUILD_DIR)/host ; cmake .. ; $(MAKE) -j import_executables )
endef

define Host/Install
endef

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(PKG_BUILD_DIR)" \
		SUBDIRS="include" \
		DESTDIR="$(PKG_INSTALL_DIR)"
	$(MAKE) -C "$(PKG_BUILD_DIR)" \
		SUBDIRS="include" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(2)/bin $(1)/usr/bin $(1)/usr/include $(1)/usr/lib $(1)/usr/lib/mysql $(1)/usr/share/aclocal
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mysql_config $(1)/usr/bin/
	ln -sf $(STAGING_DIR)/usr/bin/mysql_config $(2)/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/mysql $(1)/usr/include/
	# NOTE: needed for MySQL-Python
	$(CP) $(PKG_BUILD_DIR)/include/mysqld_error.h $(1)/usr/include/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.a $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.a $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/aclocal/mysql.m4 $(1)/usr/share/aclocal/
endef

define Package/libmariadb/install
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/lib/mysql
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmysqlclient*.so $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmariadb.so.* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmariadb.so $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/mysql_clear_password.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/dialog.so $(1)/usr/lib/mysql/
endef

define Package/mariadb-client/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqlcheck $(1)/usr/bin/
endef

define Package/mariadb-client-extra/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/innochecksum $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqlaccess $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqladmin $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqldump $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqldumpslow $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_find_rows $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_fix_extensions $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqlimport $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqlshow $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqlslap $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_waitpid $(1)/usr/bin/
endef

define Package/mariadb-server/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/share/mysql $(1)/usr/share/mysql/english $(1)/usr/lib/mysql $(1)/etc/mysql $(1)/etc/mysql/conf.d $(1)/etc/init.d
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqld $(1)/usr/bin/mysqld
	$(INSTALL_BIN) files/mariadb.init $(1)/etc/init.d/mariadb
	# these two need perl and should go into their own package which depends on perl + dbi + ?
	$(INSTALL_CONF) files/my.cnf $(1)/etc/mysql/
	$(INSTALL_CONF) files/conf.d/* $(1)/etc/mysql/conf.d/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/english/errmsg.sys $(1)/usr/share/mysql/english
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/fill_help_tables.sql $(1)/usr/share/mysql/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mysql_system_tables.sql $(1)/usr/share/mysql/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mysql_system_tables_data.sql $(1)/usr/share/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/auth_socket.so $(1)/usr/lib/mysql/
ifndef CONFIG_mariadb_LITE
	# $(INSTALL_BIN) files/mysqlreport $(1)/usr/bin/
	# $(INSTALL_BIN) files/innotop $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/auth_0x0100.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/auth_ed25519.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/auth_test_plugin.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/adt_null.so $(1)/usr/lib/mysql/
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/feedback.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/dialog.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/ha_*.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/handlersocket.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/mypluglib.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/metadata_lock_info.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/qa_auth_*.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/query_*.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/server_audit.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/semisync_master.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/semisync_slave.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/sha256_password.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/simple_password_check.so $(1)/usr/lib/mysql/
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/sphinx.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/msql2mysql $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/myisam_ftdump $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/myisamlog $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/myisampack $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/aria* $(1)/usr/bin/
#	$(CP) $(PKG_INSTALL_DIR)/usr/bin/aria_read_log $(1)/usr/bin/
#	$(CP) $(PKG_INSTALL_DIR)/usr/bin/aria_ftdump $(1)/usr/bin/
#	$(CP) $(PKG_INSTALL_DIR)/usr/bin/aria_chk $(1)/usr/bin/
#	$(CP) $(PKG_INSTALL_DIR)/usr/bin/aria_dump_log $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mariabackup $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mariadb_config $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_convert_table_format $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_tzinfo_to_sql $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqlbinlog $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqlhotcopy $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mytop $(1)/usr/bin/
endif
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/ha_innodb.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/plugin/sql_errlog.so $(1)/usr/lib/mysql/
	$(CP) $(PKG_INSTALL_DIR)/usr/scripts/mysql_install_db $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/my_print_defaults $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/myisamchk $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_plugin $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_secure_installation $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_setpermission $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysql_upgrade $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqld_multi $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqld_safe $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/mysqld_safe_helper $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/perror $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/replace $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/resolve_stack_dump $(1)/usr/bin/
endef

define Package/mariadb/conffiles
/etc/mysql/my.cnf
/etc/mysql/conf.d
endef

$(eval $(call HostBuild))

$(eval $(call BuildPackage,libmariadb))
$(eval $(call BuildPackage,mariadb))
$(eval $(call BuildPackage,mariadb-client))
$(eval $(call BuildPackage,mariadb-client-extra))
$(eval $(call BuildPackage,mariadb-server))
