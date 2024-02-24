```
#!/bin/bash
apt update
DEBIAN_FRONTEND=noninteractive apt install zip unzip qbittorrent-nox -y

mkdir -p /root/seedbox/
wget -O /root/seedbox/seedbox.zip https://github.com/tnan/seedbox/raw/main/lastest/seedbox.zip
unzip /root/seedbox/seedbox.zip -d /

adduser --system --group torrent-downloader
gpasswd -a torrent-downloader www-data
gpasswd -a www-data torrent-downloader
chown -R torrent-downloader:torrent-downloader /home/torrent-downloader/
chmod 777 /home/torrent-downloader/qbittorrent-nox

systemctl daemon-reload
systemctl enable torrent-downloader
systemctl start torrent-downloader

adduser --system --group file-manager
gpasswd -a file-manager www-data
gpasswd -a www-data file-manager
chown -R file-manager:file-manager /home/file-manager/
chmod 777 /home/file-manager/file-manager-start.sh
chmod 777 /home/file-manager/filebrowser

systemctl daemon-reload
systemctl enable file-manager
systemctl start file-manager

chown -R www-data:www-data /var/www/html/
chmod -R 777 /var/www/html/
```
