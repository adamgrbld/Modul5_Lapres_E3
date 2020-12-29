# Jarkom_Modul5_Lapres_E3

## A

**Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan**

- UML
	- nano topologi.sh
		
		```
		# Switch
		uml_switch -unix switch1 > /dev/null < /dev/null &
		uml_switch -unix switch2 > /dev/null < /dev/null &
		uml_switch -unix switch3 > /dev/null < /dev/null &
		uml_switch -unix switch4 > /dev/null < /dev/null &
		uml_switch -unix switch5 > /dev/null < /dev/null &
		uml_switch -unix switch6 > /dev/null < /dev/null &

		# Router
		xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.70.17 eth1=daemon,,,switch4 eth2=daemon,,,switch3 mem=96M &
		xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch2 eth1=daemon,,,switch6 eth2=daemon,,,switch4 mem=96M &
		xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch3 eth1=daemon,,,switch5 eth2=daemon,,,switch1 mem=96M &

		# Server
		xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
		xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
		xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch1 mem=128M &
		xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch1 mem=128M &

		# Klien
		xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch6 mem=96M &
		xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch5 mem=96M &

		```

## B

**Membuat topologi tersebut menggunakan teknik CIDR atau VLSM**

Kami menggunakan teknik **VLSM** seperti berikut:

- Menentukan subnet

	![soal](https://github.com/adamgrbld/Modul5_Lapres_E3/blob/main/image/soal.png)

- Menghitung jumlah IP

	![subnet](https://github.com/adamgrbld/Modul5_Lapres_E3/blob/main/image/subnet.png)

- Membagi NID

	![nid](https://github.com/adamgrbld/Modul5_Lapres_E3/blob/main/image/nid.jpg)

- Menentukan IP untuk setiap device

	![ip](https://github.com/adamgrbld/Modul5_Lapres_E3/blob/main/image/ip.png)

	![server](https://github.com/adamgrbld/Modul5_Lapres_E3/blob/main/image/server.png)

- Setting UML sesuai pembagian IP, netmask dan gateway diatas

  **surabaya**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 10.151.70.18
  netmask 255.255.255.252
  gateway 10.151.70.17

  auto eth1
  iface eth1 inet static
  address 192.168.0.1
  netmask 255.255.255.252

  auto eth2
  iface eth2 inet static
  address 192.168.0.5
  netmask 255.255.255.252
  ```

  **sidoarjo**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.2.2
  netmask 255.255.255.0
  gateway 192.168.2.1
  ```
  **gresik**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1

  ```
  **malang**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 10.151.71.35
  netmask 255.255.255.248
  gateway 10.151.71.34
  ```
  **mojokerto**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 10.151.71.34
  netmask 255.255.255.248
  gateway 10.151.71.33
  ```
  **batu**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.0.6
  netmask 255.255.255.252
  gateway 192.168.0.5

  auto eth1
  iface eth1 inet static
  address 10.151.71.33
  netmask 255.255.255.248

  auto eth2
  iface eth2 inet static
  address 192.168.2.1
  netmask 255.255.255.0
  ```
  **kediri**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.0.2
  netmask 255.255.255.252
  gateway 192.168.0.1

  auto eth1
  iface eth1 inet static
  address 192.168.0.9
  netmask 255.255.255.248

  auto eth2
  iface eth2 inet static
  address 192.168.1.1
  netmask 255.255.255.0
  ```
  **madiun**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.0.10
  netmask 255.255.255.248
  gateway 192.168.0.9
  ```
  **probolinggo**
  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.0.11
  netmask 255.255.255.248
  gateway 192.168.0.9
  ```

## C

**Melakukan routing agar setiap perangkat pada jaringan tersebut dapat terhubung**

![route](https://github.com/adamgrbld/Modul5_Lapres_E3/blob/main/image/route.png)

```Add route pada UML sesuai dengan pembagian NID, netmask dan gateway diatas```


## 1

**Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi SURABAYA menggunakan iptables, namun Bibah tidak ingin kalian menggunakan MASQUERADE**

- SURABAYA

	```
	iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.71.18
	```

	Dengan menggunakan chain POSTROUTING, maka source semua paket yang menuju keluar akan diubah menjadi 10.151.71.18

## 2

**Kalian diminta untuk mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER) pada SURABAYA demi menjaga keamanan**

- SURABAYA

	```
	iptables -A FORWARD -d 10.151.71.32/29 -i eth0 -p tcp --dport 22 -j DROP
	```

	Dengan menggunakan chain FORWARD, sehingga setiap paket dengan protokol TCP, interface eth0 yang datang dari luar dan port tujuan 22 serta subnet tujuan 10.151.71.32/29 akan didrop
	
## 3

**Karena tim kalian maksimal terdiri dari 3 orang, Bibah meminta kalian untuk membatasi DHCP dan DNS server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana saja menggunakan iptables pada masing masing server, selebihnya akan di DROP**

- SURABAYA

	```
	iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 -j DROP
	```

	Dengan menggunakan chain INPUT setiap paket dengan protokol ICMP akan dibatasi untuk membuat koneksi sebanyak 3 dan selebihnya akan didrop

## 4

**Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat**

- SURABAYA

	```
	iptables -A INPUT -s 192.168.2.0/24 -m time --timestart 07:00 --timestop 17:00 --days Mon,Tue,Wed,Thu,Fri -j ACCEPT
	iptables -A INPUT -s 192.168.2.0/24 -j REJECT
	```
	Dengan menggunakan chain INPUT, mengizinkan akses pada pukul 07.00-17.00 dan selain itu akan direject

## 5

**Akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 hingga pukul 07.00 setiap harinya**

- SURABAYA

	```
	iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:00 --timestop 17:00 -j REJECT
	```

	Dengan menggunakan chain INPUT, mengizinkan akses pada pukul 17.00-07.00 dengan mereject waktu antara 07.00-17.00

## 6

**Bibah ingin SURABAYA disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80**

- SURABAYA

	```
	iptables -t nat -A PREROUTING -p tcp -d 10.151.71.90 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.168.1.3:80
	iptables -t nat -A PREROUTING -p tcp -d 10.151.71.90 -j DNAT --to-destination 192.168.1.2:80
	```
	
	Setiap paket yang menuju DNS Server dengan protocol TCP dan port tujuan 80 akan didistribusikan masing masing ke 192.168.1.3:80 dan 192.168.1.2:80

## 7

**Bibah ingin agar semua paket didrop oleh firewall (dalam topologi) tercatat dalam log pada setiap UML yang memiliki aturan drop**

- SURABAYA

	```
	iptables -N LOGGING
  iptables -A FORWARD -j LOGGING
  iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IP Tables Packet Dropped: " --log-level 4
  iptables -A LOGGING -j DROP
	```

- MALANG dan MOJOKERTO

	```
	iptables -N LOGGING
  iptables -A INPUT -j LOGGING
  iptables -A OUTPUT -j LOGGING
  iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
  iptables -A LOGGING -j DROP
	```
	
Membuat sebuah variabel LOGGING. Variabel LOGGING ini bertujuan untuk menambahkan LOG “IPTables Packet Dropped” ketika suatu action dilakukan. Action untuk LOG ini adalah DROP, jadi setiap terjadi droppacket, maka akan ditambahkan LOG tersebut
