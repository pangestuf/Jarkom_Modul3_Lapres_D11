# Jarkom_Modul3_Lapres_D11
Lapres Jarkom Kelompok D11

Anggota Kelompok:
- M. Farras Pangestu - 05111840000134
- Rasyid Ridlo W. - 05111840000135

## Nomor 1 : Membuat topologi jaringan.

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/topo.PNG" >

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

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/7a.PNG" >

Restart squid service squid restart, dan berikutnya ubah proxy pada web browser ataupun OS

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/proxyip.PNG" >

Selanjutnya dapat mencoba untuk mengakses situs tertentu seperti monta.if.its.ac.id

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/7b.PNG" >

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/7c.PNG" >

## Nomor 8 : Setiap hari Selasa-Rabu pukul 13.00-18.00. Bu Meguri membatasi penggunaan internet Anri hanya pada jadwal yang telah ditentukan itu saja. Maka diluar jam tersebut, Anri tidak dapat mengakses jaringan internet dengan proxy tersebut.

Pada UML MOJOKERTO buat file konfigurasi dengan mengetikkan

    nano /etc/squid/acl.conf

dan tambahkan

    acl SATU time TW 13:00-18:00
    
<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/aclconf.PNG" >

Buka kembali file squid.conf dengan mengetikkan

    include /etc/squid/acl.conf

    http_port 8080
    http_access allow USERS SATU
    http_access deny all
    visible_hostname mojokerto
    

Simpan file tersebut. Kemudian **service squid restart** . Lalu conba akses situs apapun, contoh monta.if.its.ac.id, jika sesuai dengan jam yang ditentukan, maka situs monta.if.its.ac.id akan terbuka, jika tidak sesuai dengan jam yang telah ditentukan, maka situs tersebut tidak dapat diakses.

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/bukti8.PNG" >


## Nomor 9 : Jadwal bimbingan dengan Bu Meguri adalah setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00).

Sama halnya dengan nomor 8. Pada UML MOJOKERTO buat file konfigurasi dengan mengetikkan

    nano /etc/squid/acl.conf

dan tambahkan

    acl DUA time TWH 21:00-23:59
    acl TIGA time WHF 00:00-09:00

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/aclconf.PNG" >

Buka kembali file squid.conf dengan mengetikkan

    include /etc/squid/acl.conf

    http_port 8080
    http_access allow USERS DUA
    http_access allow USERS TIGA
    http_access deny all
    visible_hostname mojokerto

Simpan file tersebut. Kemudian **service squid restart**. Lalu coba akses situs apapun, contoh monta.if.its.ac.id, jika sesuai dengan jam yang ditentukan, maka situs monta.if.its.ac.id akan terbuka, jika tidak sesuai dengan jam yang telah ditentukan, maka situs tersebut tidak dapat diakses.

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/bukti9.PNG" >

## Nomor 10 : Setiap mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id.

Buka file ban.acl dengan mengetikkan

    nano /etc/squid/ban.acl

Lalu tambahkan pada file tersebut google.com. hal ini dimaksudkan dengan soal yaitu jika user mengetikkan google.com maka akan me-redirect ke monta.if.its.ac.id.

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/banacl.PNG">

Buka file squid.conf dengan mengetikkan nano /etc/squid/squid.conf, dan tambahkan script berikut:

    acl awas url_regex "/etc/squid/ban.acl"
    deny_info http://monta.if.its.ac.id/ awas
    http_access deny awas
    
<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/squidconf.PNG" >

Restart squid service squid restart, lalu masukkan google.com pada search bar, maka akan teralihkan ke monta.if.its.ac.id. (Berlaku jika sesuai dengan jam yang telah ditetapkan).

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/monta.PNG" >

## Nomor 11 : Mengubah error page default squid 

Buka folder cd /usr/share/squid/errors/en dan download error page dengan cara wget 10.151.36.202/ERR_ACCESS_DENIED. Lalu tampilannya akan sebagai berikut dengan ls

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/11.PNG" >

Remove ERR_ACCESSS_DENIED dan download error page dengan cara wget 10.151.36.202/ERR_ACCESS_DENIED

    rm ERR_ACCESSS_DENIED

Buka kembali konfigurasi squid.conf dengan mengetikkan nano /etc/squid/squid.conf. Ubah file konfigurasi squid menjadi seperti berikut ini.

    http_port 8080
    visible_hostname mojokerto

    acl BLACKLISTS dstdomain "/etc/squid/restrict-sites.acl"
    http_access deny BLACKLISTS
    http_access allow all
    
<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/squidconf.PNG">

Restart squid **service squid restart** dan jalankan alamat URL monta.if.its.ac.id

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/errorpage.PNG" >


## Nomor 12 : Menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080.

Buka MALANG dan update package lists dengan menjalankan command:

    apt-get update

Setelah melakukan update silahkan install aplikasi bind9 pada MALANG dengan perintah:

    apt-get install bind9 -y

Lakukan perintah pada MALANG. Isikan seperti berikut:

    nano /etc/bind/named.conf.local

Isikan konfigurasi domain janganlupa-ta.c12.pw sesuai dengan syntax berikut:

    zone "janganlupa-ta.c12.pw" {
 	type master;
	file "/etc/bind/jarkom/janganlupa-ta.c12.pw";
    };

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/12a.PNG" >

Buat folder jarkom di dalam /etc/bind

    mkdir /etc/bind/jarkom

Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi janganlupa-ta.d11.pw

    cp /etc/bind/db.local /etc/bind/jarkom/janganlupa-ta.d11.pw

Kemudian buka file janganlupa-ta.d11.pw dan edit seperti gambar berikut dengan IP MOJOKERTO masing-masing kelompok:

    nano /etc/bind/jarkom/janganlupa-ta.d11.pw
    
<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/12b.PNG" >

Restart bind9 dengan perintah

    service bind9 restart

Ganti proxy pada web browser atau OS yang sebelumnya 10.151.79.99 menjadi janganlupa-ta.d11.pw, dengan port yaitu 8080.

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/12c.PNG" >

Lalu coba periksa proxy yang telah diubah tersebut, contohnya dengan mengakses website apapun, seperti monta.if.its.ac.id

<img src="https://github.com/pangestuf/Jarkom_Modul3_Lapres_D11/blob/main/Foto/monta.PNG" >


