# Jarkom-Modul-4-C11-2021

## Anggota Kelompok C11 : <br>
- 05111940000001 Christopher Baptista
- 05111940000093 Riki Mi’roj Achmad
- 05111940000219 M Rizqi Fiqih Thalib

## VLSM (Variable Length Subnet Masking) 

Perhitungan Subnet : 
| Subnet  | Jumlah IP | Netmask |
| :----:| :-----: | :---: |
| A1 | 1001 | 22 |
| A2 | 13  | 28 |
| A3 | 502 | 23 |
| A4 | 2 | 30 |
| A5 | 2 | 30 |
| A6 | 2 | 30 |
| A7 | 101 | 25 |
| A8 | 701 | 22 |
| A9 | 2021 | 21 |
| A10 | 521 | 22 |
| A11 | 2 | 30 |
| A12 | 721 | 22 |
| A13 | 252 | 24 |
| Total | 5841 | 19 |

Pohon VLSM : 
![Pohon VLSM](https://user-images.githubusercontent.com/62735317/143675589-caf40479-816a-478c-93b2-49287cd4a052.jpg)

![image](https://user-images.githubusercontent.com/62735317/143676342-5d84420b-118e-4a08-b7fc-b63d66e72b05.png) 
![image](https://user-images.githubusercontent.com/62735317/143676846-7f99ca58-6d07-45aa-8644-6a9559398921.png)


Lingkaran VLSM : 
![Lingkaran VLSM](https://user-images.githubusercontent.com/62735317/143675573-74c2a358-046e-4c3a-80c1-bb5f042c3c72.jpg)



## CIDR (Classless Inter Domain Routing)

Perhitungan Subnet : 
![1](https://user-images.githubusercontent.com/62735317/143675712-4471e8ed-5971-4423-8ba8-b681ba5c5e35.jpg)
![2](https://user-images.githubusercontent.com/62735317/143675713-e7afa238-0aee-4413-bdcd-e6d6ab7484ee.jpg)
![3](https://user-images.githubusercontent.com/62735317/143675715-fae9871f-e94f-48d0-9216-35fa531d2c33.jpg)
![4](https://user-images.githubusercontent.com/62735317/143675717-0e70fd63-a7d0-4443-84ec-a3bb05b95064.jpg)
![5](https://user-images.githubusercontent.com/62735317/143675719-9738aa92-cc70-4b3e-abad-20fa79d52971.jpg)
![6](https://user-images.githubusercontent.com/62735317/143675720-a0015369-c97b-41a7-b0b7-09b9ca3cda08.jpg)
![7](https://user-images.githubusercontent.com/62735317/143675723-1d85b19a-1d7e-4e59-a97b-2e13d14fc54d.jpg)


Pohon CIDR : 
![Pohon CIDR](https://user-images.githubusercontent.com/62735317/143675730-17a8db4b-e150-4bc8-a4c9-450c91b81b1e.jpg)

![image](https://user-images.githubusercontent.com/62735317/143676935-c304a16a-3ae0-4a26-a2da-ed9d703ab8e8.png)
![image](https://user-images.githubusercontent.com/62735317/143676966-2dd6efc6-96ce-4c89-8f8a-553d4cb24ba0.png)

### Config pada GNS3
semua node selain router foosha command
```echo nameserver 192.168.122.1 > /etc/resolv.conf```

### Router
semua router command ```nano /etc/sysctl.conf``` kemudian ```net.ipv4.ip_forward=1```

##### -FOOSHA
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
address 192.189.64.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.189.192.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.189.32.1
netmask 255.255.255.252
```
Lakukan command berikut pada router FOOSHA : ```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.189.0.0/16```  

menjalankan route.sh yang berisi:
```
route add -net 192.189.64.0 netmask 255.255.252.0 gw 192.189.64.2

route add -net 192.189.128.0 netmask 255.255.128.0 gw 192.189.192.2

route add -net 192.189.0.0 netmask 255.255.192.0 gw 192.189.32.2  
```  
  
##### WATER7
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.189.192.2
netmask 255.255.255.252
gateway 192.189.192.1

auto eth1
iface eth1 inet static
address 192.189.160.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.189.144.1
netmask 255.255.255.252
```
  
menjalankan route.sh yang berisi:
```
route add -net 192.189.160.0 netmask 255.255.252.0 gw 192.189.160.2

route add -net 192.189.128.0 netmask 255.255.224.0 gw 192.189.144.2
```  
  ##### GUANHAO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.189.32.2
netmask 255.255.255.252
gateway 192.189.32.1

auto eth1
iface eth1 inet static
address 192.189.20.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.189.8.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.189.16.1
netmask 255.255.254.0
```  
  
menjalankan route.sh yang berisi :
```
route add -net 192.189.16.0 netmask 255.255.252.0 gw 192.189.16.3

route add -net 192.189.16.0 netmask 255.255.252.0 gw 192.189.16.2

route add -net 192.189.20.0 netmask 255.255.252.0 gw 192.189.20.2

route add -net 192.189.0.0 netmask 255.255.240.0 gw 192.189.8.2
```  

##### OIMO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.189.8.2
netmask 255.255.255.252
gateway 10.4.8.1

auto eth1
iface eth1 inet static
address 192.189.4.1
netmask 255.255.255.0
```  
  
menjalankan route.sh yang berisi :
```
route add -net 192.189.0.0 netmask 255.255.248.0 gw 192.189.4.3

route add -net 192.189.0.0 netmask 255.255.248.0 gw 192.189.4.2
```  
  
##### PUCCI
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.189.144.2
netmask 255.255.255.252
gateway 192.189.144.1

auto eth1
iface eth1 inet static
address 192.189.136.1
netmask 255.255.255.128

auto eth2
iface eth2 inet static
address 192.189.128.1
netmask 255.255.248.0
```  
    
##### SEASTONE
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.189.4.2
netmask 255.255.255.0
gateway 192.189.4.1

auto eth1
iface eth1 inet static
address 192.189.0.1
netmask 255.255.252.0
```  
  
##### ALABASTA
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.189.16.2
netmask 255.255.254.0
gateway 192.189.16.1

auto eth1
iface eth1 inet static
address 192.189.18.1
netmask 255.255.255.240
```  
### Klien

##### BLUENO
```
auto eth0
iface eth0 inet static
address 192.189.64.2
netmask 255.255.252.0
gateway 192.189.64.1
```

##### CIPHER
```
auto eth0
iface eth0 inet static
address 192.189.160.2
netmask 255.255.252.0
gateway 192.189.160.1
```

##### JIPANGU
```
auto eth0
iface eth0 inet static
address 192.189.136.2
netmask 255.255.255.128
gateway 192.189.136.1
```

##### CALMBELT
```
auto eth0
iface eth0 inet static
address 192.189.128.2
netmask 255.255.248.0
gateway 192.189.128.1
```

##### COURTYARD
```
auto eth0
iface eth0 inet static
address 192.189.128.3
netmask 255.255.248.0
gateway 192.189.128.1
```

##### JABRA
```
auto eth0
iface eth0 inet static
address 192.189.20.2
netmask 255.255.252.0
gateway 192.189.20.1
```

##### ENIESLOBBY
```
auto eth0
iface eth0 inet static
address 192.189.4.3
netmask 255.255.255.0
gateway 192.189.4.1
```

##### ELENA
```
auto eth0
iface eth0 inet static
address 192.189.0.2
netmask 255.255.252.0
gateway 192.189.0.1
```

##### MAINGATE
```
auto eth0
iface eth0 inet static
address 192.189.16.3
netmask 255.255.254.0
gateway 192.189.16.1
```

##### JORGE
```
auto eth0
iface eth0 inet static
address 192.189.18.2
netmask 255.255.255.240
gateway 192.189.18.1
```
