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

#auto eth0
#iface eth0 inet dhcp

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

## Soal 1
Loid bersama Franky berencana membuat peta tersebut dengan kriteria WISE sebagai DNS Server, Westalis sebagai DHCP Server, Berlint sebagai Proxy Server

**WISE**  
Membuat domain website **loid-work.com** dan **franky-work.com**

- /etc/bind/named.conf.local

	```
	zone "loid-work.com" {
					type master;
					file "/etc/bind/b13/loid-work.com";
	};

	zone "franky-work.com" {
					type master;
					file "/etc/bind/b13/franky-work.com";
	};
	```
- /etc/bind/b13/loid-work.com
	```
	;
	; BIND data file for local loopback interface
	;
	$TTL    604800
	@       IN      SOA     loid-work.com. root.loid-work.com. (
											2022110701         ; Serial
												604800         ; Refresh
												 86400         ; Retry
											   2419200         ; Expire
												604800 )       ; Negative Cache TTL
	;
	@       IN      NS      loid-work.com.
	@       IN      A       192.179.3.13    ; IP Eden
	www     IN      CNAME   loid-work.com.
	@       IN      AAAA    ::1
	```
- /etc/bind/b13/franky-work.com
	```
	;
	; BIND data file for local loopback interface
	;
	$TTL    604800
	@       IN      SOA     franky-work.com. root.franky-work.com. (
											2022110701    ; Serial
											604800        ; Refresh
											86400         ; Retry
											2419200		  ; Expire
											604800 )      ; Negative Cache TTL
	;
	@       IN      NS      franky-work.com.
	@       IN      A       192.179.3.13    ; IP Eden
	www     IN      CNAME   franky-work.com.
	@       IN      AAAA    ::1
	```

**Westalis**
- /etc/default/isc-dhcp-server 

	menambahkan eth0 pada interfaces
	```
	INTERFACES="eth0"
	```
- /etc/dhcp/dhcpd.conf

	```
	subnet 192.179.2.0 netmask 255.255.255.0 {

	}

	subnet 192.179.1.0 netmask 255.255.255.0 {
			range 192.179.1.50 192.179.1.88;
			range 192.179.1.120 192.179.1.155;
			option routers 192.179.1.1;
			option broadcast-address 192.179.1.255;
			option domain-name-servers 192.179.2.2;
			default-lease-time 300;
			max-lease-time 6900;
	}

	subnet 192.179.3.0 netmask 255.255.255.0 {
			range 192.179.3.10 192.179.3.30;
			range 192.179.3.60 192.179.3.95;
			option routers 192.179.3.1;
			option broadcast-address 192.179.3.255;
			option domain-name-servers 192.179.2.2;
			default-lease-time 600;
			max-lease-time 6900;
	}
	```

**Berlint**
- /etc/squid/squid.conf
	```
	http_port 8080
	visible_hostname Berlint
	```

## Soal 2
Ostania sebagai DHCP Relay

**Ostania**
- /etc/default/isc-dhcp-relay
	```
	# Defaults for isc-dhcp-relay initscript
	# sourced by /etc/init.d/isc-dhcp-relay
	# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

	#
	# This is a POSIX shell fragment
	#

	# What servers should the DHCP relay forward requests to?
	SERVERS="192.179.2.4"

	# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
	INTERFACES="eth1 eth2 eth3"

	# Additional options that are passed to the DHCP relay daemon?
	OPTIONS=""
	```

## Soal 3
Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.50 - [prefix IP].1.88 dan [prefix IP].1.120 - [prefix IP].1.155

Penyelesaian:

**Westalis**

- Menambahkan range pada dhcpd.conf di Switch1
	```
	subnet 192.179.1.0 netmask 255.255.255.0 {
			range 192.179.1.50 192.179.1.88;
			range 192.179.1.120 192.179.1.155;
			option routers 192.179.1.1;
			option broadcast-address 192.179.1.255;
			option domain-name-servers 192.179.2.2;
			default-lease-time 300;
			max-lease-time 6900;
	}
	```

## Soal 4
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.10 - [prefix IP].3.30 dan [prefix IP].3.60 - [prefix IP].3.85

Penyelesaian:

**Westalis**

- Menambahkan range pada dhcpd.conf di Switch3
	```
	subnet 192.179.3.0 netmask 255.255.255.0 {
			range 192.179.3.10 192.179.3.30;
			range 192.179.3.60 192.179.3.95;
			option routers 192.179.3.1;
			option broadcast-address 192.179.3.255;
			option domain-name-servers 192.179.2.2;
			default-lease-time 600;
			max-lease-time 6900;
	}
	```

## Soal 5
Client mendapatkan DNS dari WISE dan client dapat terhubung dengan internet melalui DNS tersebut

Penyelesaian:

**WISE**

- Mengatur forwarders dan allow-query{any;} pada **/etc/bind/named.conf.options**
	```
	options {
			directory "/var/cache/bind";

			// If there is a firewall between you and nameservers you want
			// to talk to, you may need to fix the firewall to allow multiple
			// ports to talk.  See http://www.kb.cert.org/vuls/id/800113

			// If your ISP provided one or more IP addresses for stable
			// nameservers, you probably want to use them as forwarders.
			// Uncomment the following block, and insert the addresses replacing
			// the all-0's placeholder.

			forwarders {
							192.168.122.1;
			};

			//========================================================================
			// If BIND logs error messages about the root key being expired,
			// you will need to update your keys.  See https://www.isc.org/bind-keys
			//========================================================================
			//dnssec-validation auto;
			allow-query{any;};
			auth-nxdomain no;    # conform to RFC1035
			listen-on-v6 { any; };
	};
	```


