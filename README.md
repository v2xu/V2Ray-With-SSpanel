# V2Ray With SSpanel File

Thanks a lot to @Anankke 、 V2ray Team、 @rico93

## For NODE
```
bash <(curl -L -s  https://raw.githubusercontent.com/NS-Sp4ce/V2Ray-Node-Need-File/master/install-release.sh) --panelurl https://xxxx --panelkey xxxx --nodeid NODEID

# restart v2ray node services

service v2ray restart

# checkout v2ray status

service v2ray status
```

## For PANEL 
1. Install BaoTa and config LNMP with PHP7.2 (more steps see here https://github.com/NS-Sp4ce/ShadowSocksPanelFiles#%E5%AE%89%E8%A3%85%E5%AE%9D%E5%A1%94%E9%9D%A2%E6%9D%BF TO https://github.com/NS-Sp4ce/ShadowSocksPanelFiles#%E5%AE%89%E8%A3%85%E5%AE%9D%E5%A1%94%E9%9D%A2%E6%9D%BF )
2. Install panel (thanks a lot to ss-panel-uim team)
```
cd /www/wwwroot/sspanel
yum update -y && yum install git -y
git clone -b master https://github.com/Anankke/ss-panel-v3-mod_Uim.git tmp && mv tmp/.git . && rm -rf tmp && git reset --hard
cp config/.config.example.php config/.config.php
chown -R root:root *
chmod -R 755 *
chown -R www:www storage
php composer.phar install
```

> NOTE: if output errors like `Could not open input file: composer.phar`, recheck `putenv()` function has **not** been disabled and try 

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer install
```
if composer output like that
```
Loading composer repositories with package information
Updating dependencies (including require-dev)
Killed
```
try to divide the swap partition for 2G 
```
free -m
mkdir -p /var/_swap_
cd /var/_swap_
dd if=/dev/zero of=swapfile bs=1M count=2000
mkswap swapfile
swapon swapfile
echo “/var/_swap_/swapfile none swap sw 0 0” >> /etc/fstab
free -m
```
and run `composer install` again.

3. Config Database
Download sql file(`glzjin_all.sql`) from `/www/wwwroot/sspanel/sql/` then import to mysql database

4. Final things
```
php xcat createAdmin
php xcat syncusers
php xcat initQQWry
php xcat resetTraffic
php xcat initdownload
```
