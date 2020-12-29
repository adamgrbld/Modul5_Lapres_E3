# Modul5_Lapres_E3

# setting uml

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
