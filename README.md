# mysql_sys_udf

## Installation
* `sudo ./install.sh`
or 
* `sudo make`
* `mysql -u root -p mysql < lib_mysqludf_sys.sql`

## Updating AppArmor profile

By default AppArmor blocks sys udf execution. 
Run `sudo aa-status` in order to see current AppArmor policy:
```
apparmor module is loaded.
21 profiles are loaded.
21 profiles are in enforce mode.
   /sbin/dhclient
   /usr/bin/evince
   /usr/bin/evince-previewer
   /usr/bin/evince-previewer//sanitized_helper
   /usr/bin/evince-thumbnailer
   /usr/bin/evince-thumbnailer//sanitized_helper
   /usr/bin/evince//sanitized_helper
   /usr/lib/NetworkManager/nm-dhcp-client.action
   /usr/lib/connman/scripts/dhclient-script
   /usr/lib/cups/backend/cups-pdf
   /usr/lib/lightdm/lightdm-guest-session
   /usr/lib/lightdm/lightdm-guest-session//chromium
   /usr/lib/telepathy/mission-control-5
   /usr/lib/telepathy/telepathy-*
   /usr/lib/telepathy/telepathy-*//pxgsettings
   /usr/lib/telepathy/telepathy-*//sanitized_helper
   /usr/lib/telepathy/telepathy-ofono
   /usr/sbin/cups-browsed
   /usr/sbin/cupsd
   /usr/sbin/mysqld
   /usr/sbin/tcpdump
0 profiles are in complain mode.
5 processes have profiles defined.
0 processes are in enforce mode.
0 processes are in complain mode.
5 processes are unconfined but have a profile defined.
   /sbin/dhclient (6222) 
   /usr/lib/telepathy/mission-control-5 (2780) 
   /usr/sbin/cups-browsed (1063) 
   /usr/sbin/cupsd (30295) 
   /usr/sbin/mysqld (1100)
   ```
   
## To disable mysql profile(caution: disable apparmore protection for mysql server):
```
sudo ln -s /etc/apparmor.d/usr.sbin.mysqld /etc/apparmor.d/disable/
sudo apparmor_parser -R /etc/apparmor.d/usr.sbin.mysqld
sudo aa-status
```

## To enable mysql prifile back:
```
sudo rm /etc/apparmor.d/disable/usr.sbin.mysqld
sudo apparmor_parser -r /etc/apparmor.d/usr.sbin.mysqld
sudo aa-status
```
