# Jarkom-Modul-3-B13-2022

### Kelompok B13
| **No** | **Nama** | **NRP** | 
| ------------- | ------------- | --------- |
| 1 | Amsal Herbert  | 5025201182 | 
| 2 | Elbert Dicky Aristyo | 5025201231 |
| 3 | Nathanael Roviery | 5025201258 |

## Network Configuration
### **Ostania**
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.179.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.179.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.179.3.1
	netmask 255.255.255.0
```
### **SSS**
```
#auto eth0
#iface eth0 inet static
#       address 192.179.1.2
#       netmask 255.255.255.0
#       gateway 192.179.1.1

auto eth0
iface eth0 inet dhcp

```
### **Garden**
```
#auto eth0
#iface eth0 inet static
#	address 192.179.1.3
#	netmask 255.255.255.0
#	gateway 192.179.1.1

auto eth0
iface eth0 inet dhcp

```
### **WISE**
```
auto eth0
iface eth0 inet static
	address 192.179.2.2
	netmask 255.255.255.0
	gateway 192.179.2.1
```
### **Berlint**
```
auto eth0
iface eth0 inet static
	address 192.179.2.3
	netmask 255.255.255.0
	gateway 192.179.2.1
```
### **Westalis**
```
auto eth0
iface eth0 inet static
	address 192.179.2.4
	netmask 255.255.255.0
	gateway 192.179.2.1
```
### **Eden**
```
auto eth0
iface eth0 inet static
	address 192.179.3.13
	netmask 255.255.255.0
	gateway 192.179.3.1


```
### **NewstonCastle**
```
#auto eth0
#iface eth0 inet static
#	address 192.179.3.3
#	netmask 255.255.255.0
#	gateway 192.179.3.1

auto eth0
iface eth0 inet dhcp

```
### **KemonoPark**
```
#auto eth0
#iface eth0 inet static
#	address 192.179.3.4
#	netmask 255.255.255.0
#	gateway 192.179.3.1

auto eth0
iface eth0 inet dhcp

```
## Package Installation
### **Ostania**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.179.0.0/16
apt-get update
apt-get install isc-dhcp-relay -y
```
### **SSS** & **GARDEN**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install lynx -y
apt install speedtest-cli -y
```
### **WISE**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
```
### **Berlint**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install squid -y
```
### **Westalis**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y
dhcpd --version
```
### **Eden**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install apache2 -y
apt-get install php -y
apt-get install libapache2-mod-php7.0
apt-get install lynx -y
apt install speedtest-cli
```
## Soal
Loid bersama Franky berencana membuat peta tersebut dengan kriteria WISE sebagai DNS Server, Westalis sebagai DHCP Server, Berlint sebagai Proxy Server (1), dan Ostania sebagai DHCP Relay (2). Loid dan Franky menyusun peta tersebut dengan hati-hati dan teliti.

### No.1




