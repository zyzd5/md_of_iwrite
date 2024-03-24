```sh
hotspot_name=zyzds	#定义热点名称
bluetooth_address="6C:D3:EE:83:71:57"	#定义蓝牙地址

nmcli d wifi rescan
nmcli d wifi connect $hotspot_name	  #连接到热点

bluetoothctl << EOF
connect $bluetooth_address 
exit
EOF
```