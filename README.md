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


