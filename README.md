# Jarkom-Modul-3-T15-2021

# PRAKTIKUM 3 JARINGAN KOMUNIKASI - T15

Penyelesaian Soal Shift 3 Jaringan Komunikasi 2021\
Kelompok T15
  * Muhammad Yasykur Rafii (05311940000017)
  * Stefanus Lionel Carlo Nugroho (05311940000027)

---

## Table of Contents

* [Soal 1](#soal-1)
* [Soal 2](#soal-2)
* [Soal 3](#soal-3)
* [Soal 4](#soal-4)
* [Soal 5](#soal-5)
* [Soal 6](#soal-6)
* [Soal 7](#soal-7)
* [Soal 8](#soal-8)
* [Soal 9](#soal-9)
* [Soal 10](#soal-10)
* [Soal 11](#soal-11)
* [Soal 12](#soal-12)
* [Soal 13](#soal-13)
* [Kendala](#kendala)

---
## Soal 1

### Deskripsi Soal
Membuat peta jaringan dengan kriteria EniesLobby sebagai DNS Server, Jipangu sebagai DHCP Server, Water7 sebagai Proxy Server.

### Jawaban
Membuat topologi sehingga menghasilkan sebagai berikut:

![pasted image 0 (1)](https://user-images.githubusercontent.com/63065991/141410269-2a995fbf-58da-4b31-8fb2-be81056cbf65.png)

Kemudian melakukan pengaturan konfigurasi network masing-masing node dengan fitur Edit network configuration sebagai berikut:
### Foosha (sebagai DHCP Relay)
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
      address 10.49.1.1
      netmask 255.255.255.0

auto eth2
iface eth2 inet static
      address 10.49.2.1
      netmask 255.255.255.0

auto eth3
iface eth3 inet static
      address 10.49.3.1
      netmask 255.255.255.0
```

### Loguetown (sebagai Client)
```
auto eth0
iface eth0 inet static
	address 10.49.1.2
	netmask 255.255.255.0
	gateway 10.49.1.1
```

### Alabasta (sebagai Client)
```
auto eth0
iface eth0 inet static
	address 10.49.1.3
	netmask 255.255.255.0
	gateway 10.49.1.1
```

### EniesLobby (sebagai DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.49.2.2
	netmask 255.255.255.0
	gateway 10.49.2.1
```

### Water7 (sebagai Proxy Server)
```
auto eth0
iface eth0 inet static
	address 10.49.2.3
	netmask 255.255.255.0
	gateway 10.49.2.1
```

### Jipangu (sebagai DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.49.2.4
	netmask 255.255.255.0
	gateway 10.49.2.1
```

### Skypie (sebagai Client)
```
auto eth0
iface eth0 inet static
	address 10.49.3.2
	netmask 255.255.255.0
	gateway 10.49.3.1
```

### TottoLand (Sebagai Client)
```
auto eth0
iface eth0 inet static
	address 10.49.3.3
	netmask 255.255.255.0
	gateway 10.49.3.1
```

Ketikkan ‘iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.49.0.0/16’ pada node Foosha.

Memasukkan perintah ‘echo nameserver 192.168.122.1 > /etc/resolv.conf’ pada node ubuntu yang lain.

Restart semua node dan coba ping ‘google.com’. Bukti ‘Loguetown’ dapat mengakses site google adalah sebagai berikut:

![pasted image 0 (2)](https://user-images.githubusercontent.com/63065991/141411386-6bf77f7f-b22c-4fa9-9333-1e88233514be.png)

---
## Soal 2

### Deskripsi Soal
Menjadikan Foosha sebagai DHCP Relay

### Jawaban
### Pada Foosha
Install dhcp relay dengan memasukkan perintah ‘apt-get install isc-dhcp-relay -y’
Kemudian melakukan edit file ‘/etc/default/isc-dhcp-relay’ sehingga seperti pada gambar

![pasted image 0 (3)](https://user-images.githubusercontent.com/63065991/141411591-a7f98529-fe3f-4ea5-81a6-0eed22e82800.png)

Kemudian melakukan restart dhcp relay dengan menjalankan perintah ‘service isc-dhcp-relay restart’

---
## Soal 3

### Deskripsi Soal
Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.20 - [prefix IP].1.99 dan [prefix IP].1.150 - [prefix IP].1.169.

### Jawaban
### Pada Jipangu
Melakukan instalasi dhcp server dengan menjalankan perintah ‘apt-get install isc-dhcp-server -y’
Selanjutnya melakukan edit file ‘/etc/default/isc-dhcp-server’ sehingga seperti pada gambar

![pasted image 0 (4)](https://user-images.githubusercontent.com/63065991/141411615-b1171693-5d9f-4445-acac-09053b5a8bfb.png)

Kemudian melakukan edit file ‘/etc/dhcp/dhcpd.conf’ sebagai berikut

![pasted image 0 (5)](https://user-images.githubusercontent.com/63065991/141411633-48418d59-7c07-4d26-b609-11df0e91d7d5.png)

Selanjutnya melakukan konfigurasi pada Loguetown dengan mengedit file ‘/etc/network/interfaces’ seperti pada gambar berikut

![pasted image 0 (6)](https://user-images.githubusercontent.com/63065991/141411646-9c90d740-dec3-46cb-8c23-781331f46338.png)

Lakukan restart dengan klik tombol stop dan start pada Loguetown
Lakukan uji IP dan nameserver, muncul sebagai berikut

![pasted image 0 (7)](https://user-images.githubusercontent.com/63065991/141411662-d577b660-cd22-47cd-8552-4cc314507438.png)

###Pada Alabasta
Selanjutnya pada Alabasta juga dilakukan langkah yang sama, mengedit file ‘/etc/network/interfaces’ seperti pada gambar

![pasted image 0 (8)](https://user-images.githubusercontent.com/63065991/141411673-21320134-bc8f-4101-bc34-9dfa087c211b.png)

Selanjutnya melakukan restart pada alabasta dengan klik tombol stop dan start lagi.
Melakukan uji testing pada IP dan nameserver. Akan muncul sebagai berikut

![pasted image 0 (9)](https://user-images.githubusercontent.com/63065991/141411686-e4e571c8-40ae-4e8d-932e-35f15441afe8.png)

---
## Soal 4

### Deskripsi Soal
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.30 - [prefix IP].3.50.

### Jawaban
### Pada Jipangu
Edit file ‘/etc/dhcp/dhcpd.conf’ sebagai berikut

![pasted image 0 (10)](https://user-images.githubusercontent.com/63065991/141411705-57f0bc43-c7b8-469e-9899-fd3ead7ff9ac.png)

Kemudian melakukan restart dhcp dengan perintah ‘service isc-dhcp-server restart’

###Pada TottoLand
Selanjutnya pada Tottoland dilakukan mengedit file ‘/etc/network/interfaces’ seperti pada gambar

![pasted image 0 (11)](https://user-images.githubusercontent.com/63065991/141411712-01b79da5-4532-4cec-9391-3a490d61f682.png)

Selanjutnya melakukan restart pada alabasta dengan klik tombol stop dan start lagi.
Melakukan uji testing pada IP dan nameserver. Akan muncul sebagai berikut

![pasted image 0 (12)](https://user-images.githubusercontent.com/63065991/141411724-7d636f0b-732e-4321-afdd-911aef53c853.png)

---
## Soal 5

### Deskripsi Soal
Client mendapatkan DNS dari EniesLobby dan client dapat terhubung dengan internet melalui DNS tersebut.

### Jawaban 
### Pada EniesLobby
Melakukan instalasi DNS dengan perintah ‘apt-get install bind9 -y’
Kemudian melakukan edit pada file 

![pasted image 0 (13)](https://user-images.githubusercontent.com/63065991/141411741-dee5aed0-04ce-48ee-8beb-7fe04a6c3b1b.png)

Kemudian melakukan restart bind dengan perintah ‘service bind9 restart’

### Pada EniesLobby melakukan
Instalasi bind dengan perintah ‘apt-get install bind9 -y’
Kemudian melakukan edit file ‘/etc/bind/named.conf.options’ seperti pada gambar:

![pasted image 0 (14)](https://user-images.githubusercontent.com/63065991/141411757-2cca4b8f-9976-4052-b390-27f3d4542e44.png)

Kemudian melakukan restart bind dengan perintah ‘service bind9 restart’

###Pada Loguetown
Melakukan ping ke ‘google.com’ 

![pasted image 0 (15)](https://user-images.githubusercontent.com/63065991/141411773-b0b0651b-3ba9-4bc5-874b-f730aaf5c28d.png)

###Pada Alabasta
Melakukan ping ke ‘google.com’ 

![pasted image 0 (16)](https://user-images.githubusercontent.com/63065991/141411785-846a7a84-8299-494b-9d54-e280510d4214.png)

###Pada Skypie
Melakukan ping ke ‘google.com’

![pasted image 0 (17)](https://user-images.githubusercontent.com/63065991/141411802-9c91b561-fe13-4172-8a76-fa0534218dc8.png)

###Pada TottoLand
Melakukan ping ke ‘google.com’

![pasted image 0 (18)](https://user-images.githubusercontent.com/63065991/141411808-78d8c4a4-3c5a-49e6-a0f3-8decd029c84c.png)

---
## Soal 6
### Deskripsi Soal
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit.

### Jawaban
### Pada Jipangu
Melakukan edit file /etc/dhcp/dchpd.conf seperti pada gambar berikut:
 
![pasted image 0 (19)](https://user-images.githubusercontent.com/63065991/141411829-7341910c-0cc3-4afb-a2d4-48372b64e6a8.png)
![pasted image 0 (20)](https://user-images.githubusercontent.com/63065991/141411851-2a696caa-a541-4a1d-a33c-44a865a64a1e.png)

Kemudian melakukan restart bind dengan perintah ‘service bind9 restart’

---
## Soal 7
### Deskripsi Soal
Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP [prefix IP].3.69.

### Jawaban
### Pada Jipangu
Melakukan edit file /etc/dhcp/dchpd.conf seperti pada gambar berikut:

![pasted image 0 (21)](https://user-images.githubusercontent.com/63065991/141413862-3f26e8f2-3a3b-4850-8c5b-e9a591f8c080.png)

Selanjutnya melakukan restart dhcp-server dengan perintah ‘service isc-dhcp-server restart’

### Pada Skypie
Melakukan konfigurasi dengan mengedit file ‘/etc/network/interfaces’ seperti pada gambar berikut

![pasted image 0 (22)](https://user-images.githubusercontent.com/63065991/141413891-ad147c62-ccb0-4e94-98fa-e0d3640554b1.png)

Selanjutnya melakukan restart Skypie dengan klik stop dan start pada node.
Melakukan uji ip dan nameserver dengan perintah ‘ip a’ maka akan menghasilkan seperti berikut

![pasted image 0 (23)](https://user-images.githubusercontent.com/63065991/141413908-a139066f-ce5d-4cbc-88b0-d6d03d653398.png)

## Kendala
- Soal 11 : 
- Soal 12 : 
- Soal 13 : 
