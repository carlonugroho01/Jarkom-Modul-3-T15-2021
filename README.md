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


<img width="500" alt="mkdir" src="https://lh5.googleusercontent.com/Hl7_dviBiIBJxETgG2mKbvsnXSgcK9OONqYadnerHplUbneNORuGd_dguW4wXIb_wHqhqPt_1lgy3ACL4AZkm21YKOkKo5J-rPwnSASfXkGGve4aXGuUWqD7VxrDhGLCIQt3YNbm”>

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

<img width="500" alt="mkdir" src="https://lh4.googleusercontent.com/P8VFFIy2AcR53eT2mWhydQOa4ELDifI-_PWTzJ28OD8p6K1MWikKnBoslff0YtngrqGj113evTFRqJoAMuvh945WKvxhHWm65SEBpfvQ5pV4qjLCU_vS2wGd5COGWsBiohLrbWGO”> 

---
## Soal 2

### Deskripsi Soal
Menjadikan Foosha sebagai DHCP Relay

### Jawaban
### Pada Foosha
Install dhcp relay dengan memasukkan perintah ‘apt-get install isc-dhcp-relay -y’
Kemudian melakukan edit file ‘/etc/default/isc-dhcp-relay’ sehingga seperti pada gambar



<img width="500" alt="mkdir" src="https://lh3.googleusercontent.com/I3XN6Uclm9O87oOfF7Fm5plRJ0b9ossZwxg5xLYnZDR2sJ7V3zcUHJ8jIMhnuCmutdxm0Z7Qi51bTdHcXguSxqbFflt9TcxDvfzV_2zmLO8vKfF74Vji9jDrKPXOTdu3tBhjkeBB”>

Kemudian melakukan restart dhcp relay dengan menjalankan perintah ‘service isc-dhcp-relay restart’

---
## Soal 3

### Deskripsi Soal
Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.20 - [prefix IP].1.99 dan [prefix IP].1.150 - [prefix IP].1.169.

### Jawaban
### Pada Jipangu
Melakukan instalasi dhcp server dengan menjalankan perintah ‘apt-get install isc-dhcp-server -y’
Selanjutnya melakukan edit file ‘/etc/default/isc-dhcp-server’ sehingga seperti pada gambar


<img width="500" alt="mkdir" src="https://lh4.googleusercontent.com/nGQM8NWpVgq3DZe8u9rr2ATGHDZAAq4-0rChn_TCmict9E2HnTGdl4htBveV7ufIqekyiUxuldUDqPowZLaS9hbaWXiHRZVwNxW3zpcdrJWl7TMZJajboXsmateIwP8vw8sDoi5l”>

Kemudian melakukan edit file ‘/etc/dhcp/dhcpd.conf’ sebagai berikut



<img width="500" alt="mkdir" src=”https://lh6.googleusercontent.com/YVZjlWucl6EM-zMzWPeIl6KPPpB3qEcSzHnf8BMqZZeTEEHF2zLU86OcEMS7J4LUjkJnfNTLVv8YMcwM8ABPLS5EOoPT7-vZGe7kjDDYeZXXmCxG-hWIWa3qdaoWrMqC7flBslqW”>

Selanjutnya melakukan konfigurasi pada Loguetown dengan mengedit file ‘/etc/network/interfaces’ seperti pada gambar berikut

<img width="500" alt="mkdir" src=”https://lh5.googleusercontent.com/8oyTDm1cAzKrxklSufQNgH9um5ITNYz9mLWnQZq1obHqyVzjjq8FbE39t2U4H699BVNAQuKLrhcxWLV7PWVHgFVCJpkui88XCdKBwNut1jTA9dxdak7BDk-mhbcjlcH1y1MkSMwu”>

Lakukan restart dengan klik tombol stop dan start pada Loguetown
Lakukan uji IP dan nameserver, muncul sebagai berikut

<img width="500" alt="mkdir" src=”https://lh4.googleusercontent.com/LGuzcBq-I0xu41rK3LKWQKF3gPLZHG9kU2QWk-PZ1F610WGbxdG6VloBmmC9-uNLydAputJ3Qrd6ZGBhcSPFiNEP8jHuew9rpUIPwMPn0ujWmdwWZPwJIuOHP-VC3bEwiD2bbEkr”>

###Pada Alabasta
Selanjutnya pada Alabasta juga dilakukan langkah yang sama, mengedit file ‘/etc/network/interfaces’ seperti pada gambar

<img width="500" alt="mkdir" src=”https://lh4.googleusercontent.com/B7n5Vckk6yU1rAJgF_qVbpfbkgM8kNsZ4pNNW43wf6EXyH3oMqupCG1LbFLNkYFFzLaoup91_NDwYFx55hKHMq1z0wAxHQi2U3DXHCwhN5ZYuxdhLO_KHOFPHkkBfPAOuYWovHVF”>

Selanjutnya melakukan restart pada alabasta dengan klik tombol stop dan start lagi.
Melakukan uji testing pada IP dan nameserver. Akan muncul sebagai berikut

<img width="500" alt="mkdir" src=”https://lh3.googleusercontent.com/q3p196mlF5i3aO_xD6VTfQtbBeKFisG8-ib-YMIUiTmJSD-YLlS7BrYgaUF4kJwlxoY4JL1g0EVihaaXTKbRuIKaIcjrdHxImY_tol0VR78_x58lZe489yPNipIoh_8Xr7ZVJ6Wl”>

---
## Soal 4

### Deskripsi Soal
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.30 - [prefix IP].3.50.

### Jawaban
### Pada Jipangu
Edit file ‘/etc/dhcp/dhcpd.conf’ sebagai berikut

<img width="500" alt="mkdir" src=”https://lh5.googleusercontent.com/4IU0WsteRJm7xEt5NaJP888TVMp8ogHD9ja9yqFcURSdhvl9U9bka7UzhbxU2AvzvkORVu5V_lgtoWK8OdWIMTSosUdNuQZGwQweAnhp4Yl-N6siBNOZN_bmVnZ3sncvtSMkSFw0”> 

Kemudian melakukan restart dhcp dengan perintah ‘service isc-dhcp-server restart’

###Pada TottoLand
Selanjutnya pada Tottoland dilakukan mengedit file ‘/etc/network/interfaces’ seperti pada gambar

<img width="500" alt="mkdir" src=”https://lh4.googleusercontent.com/MdCSRBzBBwI_wTkpGCbXBALKA09PbnPpNYs8Ua8Q7T9Tamxp8BoDyYjA2KbjNpR25sNQvMZuxuRBbqj-1MZGKx1_TcusT4HAiMJNgifYjs53yp4FRvJ-0TcGC01vu5AByyTzrKCR”> 

Selanjutnya melakukan restart pada alabasta dengan klik tombol stop dan start lagi.
Melakukan uji testing pada IP dan nameserver. Akan muncul sebagai berikut

<img width="500" alt="mkdir" src=”https://lh6.googleusercontent.com/drgAJ1tOrcZtwZiQeFi1FWtmCdahNtLvvkwFSFQMmLr4FcgAex1ScgQC-l92z4oKt4CDYNq7gytBZLqhIp8s73Na2EhFmhXG9uoTWe5xDQShMPkX8NYRIWyL6alHFLfzg1ZEP7hZ”> 

---
## Soal 5

### Deskripsi Soal
Client mendapatkan DNS dari EniesLobby dan client dapat terhubung dengan internet melalui DNS tersebut.

### Jawaban 
### Pada EniesLobby
Melakukan instalasi DNS dengan perintah ‘apt-get install bind9 -y’
Kemudian melakukan edit pada file 

<img width="500" alt="mkdir" src=”https://lh3.googleusercontent.com/BLB5f8BlbuGByMCUGYZh69d5ffz3GDw7D9yRe9VQIudGsEM5PSTOMe2SO6WIaWfC-La5Ob5L9PDbt7GiRystiA958cDxwAE5Hw-t2e8CAFwimlilCgo1a_D2ind8fauYUypZIhTX”> 

Kemudian melakukan restart bind dengan perintah ‘service bind9 restart’

### Pada EniesLobby melakukan
Instalasi bind dengan perintah ‘apt-get install bind9 -y’
Kemudian melakukan edit file ‘/etc/bind/named.conf.options’ seperti pada gambar:


<img width="500" alt="mkdir" src=”https://lh3.googleusercontent.com/Nj6g9BY1sdnMg6X2Y0WSoEHXlCZXjGgD2qTpYXUkV_lpvm08qG7ek_jxCwd2Gpu-IT8Q_eGNFpKrU0aUsGL1JsuSeCp2jCiuFEas4_d9Wux3eCldttMkekeZzhMOAY3A_GCKTSLZ”> 

Kemudian melakukan restart bind dengan perintah ‘service bind9 restart’

###Pada Loguetown
Melakukan ping ke ‘google.com’ 

<img width="500" alt="mkdir" src=”https://lh3.googleusercontent.com/6R3-QgnGFRmwipn0IzSqA-oeSiFBdmeoVuwRIRwTg3jFUZs3ZYgNrV7DeJg5jvn_k-c2c61cDjbRowDtTeoSSIUoPOZHsoZgc6ANP_yDUkrqGnharL0eievsMDmzVbMeL26_lqew”> 

###Pada Alabasta
Melakukan ping ke ‘google.com’ 

<img width="500" alt="mkdir" src=”https://lh3.googleusercontent.com/7lbQ7zYqbCugE5gClT2SvP_xG2SvgaLle1_UYY2kiGAmMrFcOQMN3AR3nvn5i4623Ngi7_yNCKjOEdV3Aqbk2DiOVrB538paNUqJ0lrPqrIWK7ogftm_mC_KvqR6YqC3hJvetnnb”> 

###Pada Skypie
Melakukan ping ke ‘google.com’

<img width="500" alt="mkdir" src=”https://lh6.googleusercontent.com/-gOwRIPqDYTVaEyNzglz1TuNmfKOIxTzo3GFScaFobvlw236XEDZ_uMizOi2IiXRQNCnN_KjSxagn6G-itwNOW2j-KRJAlTEFjtRXyrrm3uoEU6TOAsxuibecSF9jyTw4ovLCn_H”> 

###Pada TottoLand
Melakukan ping ke ‘google.com’

<img width="500" alt="mkdir" src=”https://lh4.googleusercontent.com/gyo750kZakYgyT9hzXtmiJFN-UMIhRZrdYRpVgCKXDsUOQxXXx2KPQoHLAenUI46-agkrbJZ2R2hzL-a6zCj3LjaeVSN2kr1XPcegZNhWhdWVnwQX2liAVYpruJEKtyZ-7TSVxbI”> 

---
## Soal 6
### Deskripsi Soal
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit.

### Jawaban
### Pada Jipangu
Melakukan edit file /etc/dhcp/dchpd.conf seperti pada gambar berikut:

<img width="500" alt="mkdir" src=”https://lh3.googleusercontent.com/f5bXtbA0cIQgfNFytucM_VgkFpGhzWU5vO-zi6LgAU0NXs0pVLC6U0WPV1HgAeHpJEB79hTFO9knprb9wpz9NgRZz7HhxEpDElmhFQmzMZtw7_sxgznzrZcJ8BgaEVFQj9IdTliy”> 

<img width="500" alt="mkdir" src=”https://lh5.googleusercontent.com/oO08p8Z3cqckACR6WPxp4NkTDUOi0LwVpXJZcn4xwx02fko-nU9UxATb8mxV3yw2T6G9a840Cv5hfm2qf5YLZ7kpHZj6dcfpTDB6S9xuDJmMScpIe_1_oGovVZnS32TuwYcjgdGA”>

Kemudian melakukan restart bind dengan perintah ‘service bind9 restart’

## Kendala
- Soal 1 : Belum berhasil membuat log khusus untuk enkripsi-dekripsi AtoZ
- Soal 2 : Belum berhasil membuat fungsi vigenere ketika dilakukan rename serta membagi file ke dalam file-file kecil berukuran 1024mb
- Soal 3 : Belum dapat memahamai soal
- Soal 4 : -
