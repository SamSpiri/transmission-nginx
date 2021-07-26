```
sudo apt-get install -y davfs2
cd /mnt
sudo mkdir -p /mnt/transmission
sudo tee transmission_davfs2.conf >/dev/null <<EOF
secrets           /mnt/transmission_davfs2_secrets
ignore_dav_header 1
EOF
sudo tee mount_transmission.sh >/dev/null <<EOF
URL=http://env-1070879.mircloud.ru/
echo \$URL user password | sudo tee /mnt/transmission_davfs2_secrets > /dev/null
sudo chmod 600 /mnt/transmission_davfs2_secrets
sudo mount -t davfs -o noexec -o conf=/mnt/transmission_davfs2.conf \$URL /mnt/transmission
EOF

```