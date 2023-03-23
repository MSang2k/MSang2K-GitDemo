#!/bin/bash
device_name1=$(lsblk -o NAME,SIZE,TYPE,MOUNTPOINT | grep 'disk\|part' | grep 'sd[a-z][1]' | awk '{print $1}')
device_name2=$(lsblk -o NAME,SIZE,TYPE,MOUNTPOINT | grep 'disk\|part' | grep 'sd[a-z][1]' | awk '{print $1}' | sed 's/├─//g')
#device_name=$(lsblk -o NAME,SIZE,TYPE,MOUNTPOINT | grep 'disk\|part' | grep 'sd[b-z]' | grep -v '[1]$' | sed 's/^ *//g' | sed -n '1p' | xargs lsblk -no NAME)
device_name=$(lsblk -o NAME,SIZE,TYPE,MOUNTPOINT | grep 'disk\|part' | grep 'sd[b-z]' | grep -v '[1]$' | xargs lsblk -no NAME)
echo "$device_name2"

echo $(cat /dev/$device_name2)

sda1
