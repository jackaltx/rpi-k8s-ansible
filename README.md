# rpi-k8s-ansible
Raspberry PI's running Kubernetes deployed with Ansible

## Preparing an SD card
```
# Write the image to the SD card
sudo dd if=YYYY-MM-DD-raspbian-stretch-lite.img of=/dev/sdX bs=16M status=progress

# Provision wifi settings
cp wpa_supplicant.conf /mnt/boot/

# Enable SSH on first boot
touch /mnt/boot/ssh

# Disable the Wifi country rfkill script (source: https://www.raspberrypi.org/forums/viewtopic.php?t=209226)
sudo mv /mnt/rootfs/usr/lib/raspberrypi-sys-mods/wifi-country /mnt/rootfs/usr/lib/raspberrypi-sys-mods/wifi-country+
```

# Examples
## apt-get upgrade
```
ansible-playbook -i cluster.yml playbooks/upgrade.yml
```

## rpi3b & rpi3bp overclocks
```
ansible-playbook -i cluster.yml playbooks/overclock-rpi3p.yml -l node00
ansible-playbook -i cluster.yml playbooks/overclock-rpi3.yml -l node01
ansible-playbook -i cluster.yml playbooks/overclock-rpi3.yml -l node02
ansible-playbook -i cluster.yml playbooks/overclock-rpi3.yml -l node03
ansible-playbook -i cluster.yml playbooks/overclock-rpi3.yml -l node04
```

## Bootstrap k8s master
```
ansible-playbook -i cluster.yml site.yml -l node00
```
