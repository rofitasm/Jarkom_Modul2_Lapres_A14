# Jarkom_Modul2_Lapres_A14
Laporan Resmi Modul 2 Praktikum Jaringan Komputer
#
- Rofita Siti Musdalifah    (05111840000034)
- Vachri Attala Putra       (05111840000043)
#

## Soal
1. [Soal1](#soal1)
2. [Soal2](#soal2)
3. [Soal3](#soal3)
4. [Soal4](#soal4)
5. [Soal5](#soal5)
6. [Soal6](#soal6)
7. [Soal7](#soal7)
8. [Soal8](#soal8)
9. [Soal9](#soal9)
10. [Soal10](#soal11)
11. [Soal11](#soal12)
12. [Soal12](#soal12)
13. [Soal13](#soal13)
14. [Soal14](#soal14)
15. [Soal15](#soal15)
16. [Soal16](#soal16)
17. [Soal17](#soal17)
#   

**Pada Praktikum 2 ini kami diminta untuk membuat sebuah website dengan Domain dan Konfigurasi yang telah ditentukan pada soal**

-   Terdapat 3 buah server yang berada di MALANG, MOJOKERTO dan PROBOLINGGO. Server MALANG akan digunakan sebagai DNS Server Master, MOJOKERTO akan digunakan sebagai DNS Server Slave dan PROBOLINGGO akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan untuk testing yaitu GRESIK dan SIDOARJO.

#
### Soal1
1.  **Buat domain semerua14.pw dengan mengisikan konfigurasi di MALANG sbg berikut**

!(assets/1.png)

-   Buat folder jarkom di dalam /etc/bind

-   Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi semerua14.pw

-   Kemudian buka file semerua14.pw dan edit seperti gambar berikut

!(assets/2.png)
>
> Setelah di restart bind9 nya dan dicoba hasilnya,
>
!(assets/pingsemeru.png)

#

### Soal2
2.  **Buat  alias menggunakan CNAME untuk http://www.semerua14.pw sebagai berikut**

!(assets/2.png)
>
> Lalu hasilnya setelah di coba ping,
>
!(assets/4.png)
#

### Soal3
3.  **Lalu untuk membuat subdomain http://penanjakan.semeruyyy.pw**

!(assets/2.png)
>
> Hasilnya test dengan ping, sebagai berikut
>
!(assets/5.png)
#

### Soal4
4.  **Membuat reverse domain http://semerua14.pw**

-   Edit file /etc/bind/named.conf.local pada *MALANG*

-   Lalu tambahkan konfigurasi berikut ke dalam file named.conf.local

!(assets/6.png)

-   Copykan file db.local pada path /etc/bind ke dalam folder jarkom
    > yang baru saja dibuat dan ubah namanya menjadi
    > 73.151.10.in-addr.arpa

-   Edit file 73.151.10.in-addr.arpa menjadi seperti gambar di bawah ini

!(assets/7.png)
>
> Setelah itu restart Malang dan jika dicoba pada Gresik hasilnya,
>
!(assets/ptrrecord.png)

### Soal5
5.  **Membuat DNS Server Slave pada MOJOKERTO**

Edit file /etc/bind/named.conf.local dan sesuaikan dengan syntax berikut

!(assets/conf.localMalang.png)
>
> Kemudian buka file /etc/bind/named.conf.local pada MOJOKERTO dan
> tambahkan syntax berikut:
>
!(assets/conf.localMojo.png)

Lalu untuk testing, pertama kita matikan MALANG

!(assets/stopMalang.png)
>
> Lalu setelah MALANG di matikan kita test dan hasilnya seperti berikut,
>
!(assets/testDNSslave.png)

#

### Soal6
6.  **Membuat subdomain http://gunung.semerua14.pw di delagasikan ke MOJOKERTO dan mengarah ke PROBOLINGGO**

> Ubah pada MALANG dengan menambahkan subdomain baru,
>
!(assets/2.png)

-   Kemudian edit file /etc/bind/named.conf.options pada *MALANG*.

-   Kemudian comment dnssec-validation auto; dan tambahkan baris berikut
    > allow-query{any;};

-   Pada *MOJOKERTO* edit file /etc/bind/named.conf.options


-   Kemudian comment dnssec-validation auto; dan tambahkan baris berikut
    > allow-query{any;};

-   Lalu edit file /etc/bind/named.conf.local menjadi seperti gambar di bawah:
    !(assets/conf.localMalang.png)


-   Kemudian buat direktori dengan nama delegasi lalu copy db.local ke
    > direktori pucang dan edit namanya menjadi gunung.semerua14.pw

-   Kemudian edit file gunung.semerua14.pw menjadi seperti dibawah ini

!(assets/delegasi.png)
>
> Lalu saat dicoba pada GRESIK hasilnya,
>
!(assets/testdelegasi.png)
#

### Soal7
7.  **Membuat subdomain naik.gunung.semerua14.pw diarahkan ke IP Server PROBOLINGGO**

> Pada MOJOKERTO ditambahkan subdomain sebagai berikut,
>
!(assets/delegasi.png)
>
> Lalu jika kita coba di GRESIK hasilnya,
>
!(assets/testsubnaik.png)
#

### Soal8
8.  **Mengatur webserver untuk Domain semerua14.pw yang memiliki DocumentRoot pada /var/www/semerua14.pw**

> Dengan menambahkan ServerName dan DocumentRoot
>
!(assets/8.3.png)

Lalu untuk melihat hasilnya dapat diakses dengan browser semerua14.pw

!(assets/8.4.png)
#

### Soal9
9.  **Mempersingkat alamat web http://semerua14.pw/index.php/home menjadi  http://semerua14.pw/home dengan mengaktifkan mod rewrite**

> Aktifkan a2enmod rewrite pada PROBOLINGGO

Lalu untuk semerua14.pw, AllowOverride None diganti AllowOverride All

!(assets/9.1.png)
>
> Lalu edit file .htaccess dan isikan seperti berikut
>
!(assets/9.2.png)

Lalu untuk melihat hasilnya tinggal di coba untuk semerua14.pw/home

!(assets/9.3.png)
#

### Soal10
10. **Mengatur configurasi `penanjakan.semerua14.pw` untuk menyimpan assets file yang memiliki DocumentRoot pada `/var/www penanjakan.semerua14.pw` dan memiliki struktur folder sebagai berikut:**

-   /var/www/penanjakan.semeruyyy.pw
>-  /public/javascripts
>-  /public/css
>-  /public/images
>-  /errors


> Ekstrak file asset ke folder penanjakan.semerua14.pw

Lalu tambahkan ServerName dan DocumentRoot dengan
penanjakan.semerua14.pw

!(assets/10.1.png)
>
> Lalu aktifkan a2ensite penanjakan
>
> Hasilnya jika dibuka penanjakan.semerua14.pw
>
!(assets/10.2.png)
#

### Soal11
11. **Listing pada /public tanpa folder didalamnya**

> Tambahkan Option +Indexes untuk directory
> penanjakan.semerua14.pw/public
>
> Dan tambahkan Option -Indexes untuk directory
> penanjakan.semerua14.pw/public/\*
>
!(assets/11.1.png)

Hasilnya saat mengakses penanjakan.semerua14.pw/public/

!(assets/8.4.png)

Hasilnya saat mengakses penanjakan.semerua14.pw/public/css/

!(assets/11.2.png)
#

### Soal12
12. **Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache**

> Dengan menambahkan ErrorDocument 404 /errors/404.html
>
!(assets/12.1.png)
>
> Lalu apache di restart
>
> Hasilnya saat mengakses link yang tidak ada
>
!(assets/12.2.png)
#

### Soal13
13. **Membuat konfigurasi virtual host agar dapat mengakses http://penanjakan.semerua14.pw/public/javascripts dengan http://penanjakan.semerua14.pw/js**

> Dengan menambahkan Alias dengan memberinya alias "/js"
>
!(assets/13.1.png)
>
> Lalu restart apache
>
> Hasilnya saat mengakses penanjakan.semerua14.pw/js\
> *\*tidak lagi not found, karena folder javascript memang tidak bisa
> diakses*
>
!(assets/13.2.png)
#

### Soal14
14. **Membuat naik.gunung.semerua14.pw di port 8888**

> Setting virtual host di port 8888, tambahkan server name dan document
> root untuk naik.gunung.semerua14.pw
>
!(assets/14.3.png)
>
> Lalu pada ports.conf Listen untuk port 8888
>
!(assets/14.2.png)

Lalu restart apache
>
> Lalu hasilnya jika mengakses naik.gunung.semerua14.pw:8888
>
!(assets/14.4.png)
#

### Soal15
15. **Memberikan Auth pada naik.gunung.semerua14.pw dengan username `semeru` dan password `kuynaikgunung`. Sehingga h mengunjungi IP PROBOLINGGO, yang muncul bukan web utama http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”.**

> Membuat user "semeru" dan password "kuynaikgunung" dengan perintah
> ``htpasswd -c /etc/apche2/.htpasswd semeru``
>
!(assets/15.1.png)
>
> Lalu tambahkan Auth untuk directory naik.gunung.semerua14.pw
>
!(assets/15.2.png)
>
> Lalu restart apache
>
> Hasilnya saat mengakses naik.gunung.semerua14.pw:8888
>
!(assets/15.3.png)
>
> Setelah memsukkan username dan password yang sesuai
>
!(assets/15.4.png)
#

### Soal16
16. **Mengarahkan IP PROBOLINGGO 10.151.73.124 no 15 ke semerua14.pw**

> Test ip 10.151.73.124, masih menampilkan "it Works!"
>
> Edit .htaccess default pada PROBOLINGGO untuk meredirect ip
> PROBOLINGGO ke semerua14.pw
>
!(assets/16.2.png)
>
> Ganti allowoverride none jadi all untuk directory /var/www/
>
!(assets/16.1.png)
>
> Lalu restart apache
>
> Hasilnya saat mengakses 10.151.73.124
>
!(assets/16.3.png)
#

### Soal17
17. **Mengubah semua gambar yang mengadung "semeru" ke "semeru.jpg"**

>
> Edit file .htaccess sesuai berikut
>
!(assets/17.2.png)
>
> Tambahkan AllowOverride All untuk directory penanjakan.semerua14.pw

!(assets/17.1.png)

> Hasilnya semua akses file gambar yang mengandung "semeru" akan
> diarahkan ke semeru.jpg
>
!(assets/17.3.png)
#

##  Hambatan Selama Pengerjaan
-   apt-get install dan ping keluar tiba-tiba baru bisa dilakukan ketika hari terakhir praktikum
-   sering nge lag, misalnya terkadang ketika pada putty di bash bye.sh seharusnya menutup semua UML secara otomatis, namun tidak terjadi apa-apa, sehingga harus di halt satu persatu
