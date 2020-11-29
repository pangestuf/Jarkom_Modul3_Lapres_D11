# Jarkom_Modul3_Lapres_D11
Lapres Jarkom Kelompok D11

Anggota Kelompok:
- M. Farras Pangestu - 05111840000134
- Rasyid Ridlo W. - 05111840000135

## Nomor 1 : Membuat topologi jaringan.

Setting interfaces pada setiap UML seperti berikut:
- SURABAYA (Router)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1a.PNG" >

- MALANG (DNS Server)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1b.PNG" >

- MOJOKERTO (Proxy Server)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1c.PNG" >

- TUBAN (DHCP Server)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1d.PNG" >

- MADIUN (Client)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1e.PNG" >

- GRESIK (Client)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1f.PNG" >

- SIDOARJO (Client)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1g.PNG" >

- BANYUWANGI (Client)

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/1h.PNG" >

## Nomor 2 : SURABAYA ditunjuk sebagai perantara (DHCP Relay) antara DHCP Server dan client.

Pertama, lakukan **apt-get install isc-dhcp-relay** pada UML SURABAYA, lalu setting dhcp relay tersebut dengan settingan sebagai berikut:

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/2b.PNG" >

Lalu pada DHCP Server yaitu UML TUBAN, setting dhcp server yang telah diinstall dengan settingan berikut:

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/2a.PNG" >

## Nomor 3 : Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.

Pada UML TUBAN, lakukan **nano /etc/dhcp/dhcpd.conf** dan masukkan settingan seperti berikut:

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/356.PNG" >

## Nomor 4 : Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.

Pada UML TUBAN, lakukan **nano /etc/dhcp/dhcpd.conf** dan masukkan settingan seperti berikut:

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/46.PNG" >

## Nomor 5 : Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP.

Pada UML TUBAN, lakukan **nano /etc/dhcp/dhcpd.conf** pada settingan yang telah dibuat tambahkan settingan seperti berikut (bagian yang ditandai **#Nomer5**):

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/356.PNG" >

## Nomor 6 : Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.

Pada UML TUBAN, lakukan **nano /etc/dhcp/dhcpd.conf** pada settingan yang telah dibuat tambahkan settingan seperti berikut (bagian yang ditandai **#Nomer6**):

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/356.PNG" >

## Nomor 7 : User autentikasi.
Meng-install squid di MOJOKERTO dengan cara apt-get update lalu

    apt-get install isc-dhcp-server

dan meng-install apache2-utils

    apt-get install apache2-utils

Backup terlebih dahulu file konfigurasi default yang disediakan Squid.

    mv /etc/squid/squid.conf /etc/squid/squid.conf.bak

Buat konfigurasi baru dengan mengetikkan

    nano /etc/squid/squid.conf

Kemudian, pada file config yang baru, ketikkan script:

    http_port 8080
    visible_hostname mojokerto

Setelah itu buat user dengan nama userta_c12 dan password pada MOJOKERTO dengan mengetikkan:

    htpasswd -c /etc/squid/passwd userta_c12

Edit konfigurasi squid menjadi:

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/7a.PNG"

Restart squid service squid restart, dan berikutnya ubah proxy pada web browser ataupun OS

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/proxyip.PNG"

Selanjutnya dapat mencoba untuk mengakses situs tertentu seperti monta.if.its.ac.id

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/7b.PNG"

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/7c.PNG"

## Nomor 8 : Setiap hari Selasa-Rabu pukul 13.00-18.00. Bu Meguri membatasi penggunaan internet Anri hanya pada jadwal yang telah ditentukan itu saja. Maka diluar jam tersebut, Anri tidak dapat mengakses jaringan internet dengan proxy tersebut.

Pada UML MOJOKERTO buat file konfigurasi dengan mengetikkan

    nano /etc/squid/acl.conf

dan tambahkan

    acl SATU time TW 13:00-18:00
    
<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/aclconf.PNG"

Buka kembali file squid.conf dengan mengetikkan

    include /etc/squid/acl.conf

    http_port 8080
    http_access allow USERS SATU
    http_access deny all
    visible_hostname mojokerto
    

Simpan file tersebut. Kemudian **service squid restart** . Lalu conba akses situs apapun, contoh monta.if.its.ac.id, jika sesuai dengan jam yang ditentukan, maka situs monta.if.its.ac.id akan terbuka, jika tidak sesuai dengan jam yang telah ditentukan, maka situs tersebut tidak dapat diakses.

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/bukti8.PNG"


## Nomor 9 : Jadwal bimbingan dengan Bu Meguri adalah setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00).
## Nomor 10 : Setiap mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id.
## Nomor 11 : Mengubah error page default squid 
## Nomor 12 : Menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080.
