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

> ![image](assets/1.PNG)

-   Buat folder jarkom di dalam /etc/bind

-   Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi semerua14.pw

-   Kemudian buka file semerua14.pw dan edit seperti gambar berikut

> ![image](assets/2.PNG)
>
> Setelah di restart bind9 nya dan dicoba hasilnya,
>
> ![image](assets/pingsemeru.PNG)

#

### Soal2
2.  **Buat  alias menggunakan CNAME untuk http://www.semerua14.pw sebagai berikut**

> ![image](assets/2.PNG)
>
> Lalu hasilnya setelah di coba ping,
>
> ![image](assets/4.PNG)
#

### Soal3
3.  **Lalu untuk membuat subdomain http://penanjakan.semeruyyy.pw**

> ![image](assets/2.PNG)
>
> Hasilnya test dengan ping, sebagai berikut
>
> ![image](assets/5.PNG)
#

### Soal4
4.  **Membuat reverse domain http://semerua14.pw**

-   Edit file /etc/bind/named.conf.local pada *MALANG*

-   Lalu tambahkan konfigurasi berikut ke dalam file named.conf.local

> ![image](assets/6.PNG)

-   Copykan file db.local pada path /etc/bind ke dalam folder jarkom
    > yang baru saja dibuat dan ubah namanya menjadi
    > 73.151.10.in-addr.arpa

-   Edit file 73.151.10.in-addr.arpa menjadi seperti gambar di bawah ini

> ![image](assets/7.PNG)
>
> Setelah itu restart Malang dan jika dicoba pada Gresik hasilnya,
>
> ![image](assets/ptrrecord.PNG)

### Soal5
5.  **Membuat DNS Server Slave pada MOJOKERTO**

Edit file /etc/bind/named.conf.local dan sesuaikan dengan syntax berikut

> ![image](assets/conf.localMalang.PNG)
>
> Kemudian buka file /etc/bind/named.conf.local pada MOJOKERTO dan
> tambahkan syntax berikut:
>
> ![image](assets/conf.localMojo.PNG)

Lalu untuk testing, pertama kita matikan MALANG

> ![image](assets/stopMalang.PNG)
>
> Lalu setelah MALANG di matikan kita test dan hasilnya seperti berikut,
>
> ![image](assets/testDNSslave.PNG)

#

### Soal6
6.  **Membuat subdomain http://gunung.semerua14.pw di delagasikan ke MOJOKERTO dan mengarah ke PROBOLINGGO**

> Ubah pada MALANG dengan menambahkan subdomain baru,
>
> ![image](assets/2.PNG)

-   Kemudian edit file /etc/bind/named.conf.options pada *MALANG*.

-   Kemudian comment dnssec-validation auto; dan tambahkan baris berikut
    > allow-query{any;};

-   Pada *MOJOKERTO* edit file /etc/bind/named.conf.options


-   Kemudian comment dnssec-validation auto; dan tambahkan baris berikut
    > allow-query{any;};

-   Lalu edit file /etc/bind/named.conf.local menjadi seperti gambar di bawah:
    > ![image](assets/conf.localMalang.PNG)


-   Kemudian buat direktori dengan nama delegasi lalu copy db.local ke
    > direktori pucang dan edit namanya menjadi gunung.semerua14.pw

-   Kemudian edit file gunung.semerua14.pw menjadi seperti dibawah ini

> ![image](assets/delegasi.PNG)
>
> Lalu saat dicoba pada GRESIK hasilnya,
>
> ![image](assets/testdelegasi.PNG)
#

### Soal7
7.  **Membuat subdomain naik.gunung.semerua14.pw diarahkan ke IP Server PROBOLINGGO**

> Pada MOJOKERTO ditambahkan subdomain sebagai berikut,
>
> ![image](assets/delegasi.PNG)
>
> Lalu jika kita coba di GRESIK hasilnya,
>
> ![image](assets/testsubnaik.PNG)
#

### Soal8
8.  **Mengatur webserver untuk Domain semerua14.pw yang memiliki DocumentRoot pada /var/www/semerua14.pw**

> Dengan menambahkan ServerName dan DocumentRoot
>
> ![image](assets/8.3.PNG)

Lalu untuk melihat hasilnya dapat diakses dengan browser semerua14.pw

> ![image](assets/8.4.PNG)
#

### Soal9
9.  **Mempersingkat alamat web http://semerua14.pw/index.php/home menjadi  http://semerua14.pw/home dengan mengaktifkan mod rewrite**

> Aktifkan a2enmod rewrite pada PROBOLINGGO

Lalu untuk semerua14.pw, AllowOverride None diganti AllowOverride All

> ![image](assets/9.1.PNG)
>
> Lalu edit file .htaccess dan isikan seperti berikut
>
> ![image](assets/9.2.PNG)

Lalu untuk melihat hasilnya tinggal di coba untuk semerua14.pw/home

> ![image](assets/9.3.PNG)
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

> ![image](assets/10.1.PNG)
>
> Lalu aktifkan a2ensite penanjakan
>
> Hasilnya jika dibuka penanjakan.semerua14.pw
>
> ![image](assets/10.2.PNG)
#

### Soal11
11. **Listing pada /public tanpa folder didalamnya**

> Tambahkan Option +Indexes untuk directory
> penanjakan.semerua14.pw/public
>
> Dan tambahkan Option -Indexes untuk directory
> penanjakan.semerua14.pw/public/\*
>
> ![image](assets/11.1.PNG)

Hasilnya saat mengakses penanjakan.semerua14.pw/public/css/

> ![image](assets/11.2.PNG)
#

### Soal12
12. **Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache**

> Dengan menambahkan ErrorDocument 404 /errors/404.html
>
> ![image](assets/12.1.PNG)
>
> Lalu apache di restart
>
> Hasilnya saat mengakses link yang tidak ada
>
> ![image](assets/12.2.PNG)
#

### Soal13
13. **Membuat konfigurasi virtual host agar dapat mengakses http://penanjakan.semerua14.pw/public/javascripts dengan http://penanjakan.semerua14.pw/js**

> Dengan menambahkan Alias dengan memberinya alias "/js"
>
> ![image](assets/13.1.PNG)
>
> Lalu restart apache
>
> Hasilnya saat mengakses penanjakan.semerua14.pw/js\
> *\*tidak lagi not found, karena folder javascript memang tidak bisa
> diakses*
>
> ![image](assets/13.2.PNG)
#

### Soal14
14. **Membuat naik.gunung.semerua14.pw di port 8888**

> Setting virtual host di port 8888, tambahkan server name dan document
> root untuk naik.gunung.semerua14.pw
>
> ![image](assets/14.3.PNG)
>
> Lalu pada ports.conf Listen untuk port 8888
>
> ![image](assets/14.2.PNG)

Lalu restart apache
>
> Lalu hasilnya jika mengakses naik.gunung.semerua14.pw:8888
>
> ![image](assets/14.4.PNG)
#

### Soal15
15. **Memberikan Auth pada naik.gunung.semerua14.pw dengan username `semeru` dan password `kuynaikgunung`. Sehingga h mengunjungi IP PROBOLINGGO, yang muncul bukan web utama http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”.**

> Membuat user "semeru" dan password "kuynaikgunung" dengan perintah
> ``htpasswd -c /etc/apche2/.htpasswd semeru``
>
> ![image](assets/15.1.PNG)
>
> Lalu tambahkan Auth untuk directory naik.gunung.semerua14.pw
>
> ![image](assets/15.2.PNG)
>
> Lalu restart apache
>
> Hasilnya saat mengakses naik.gunung.semerua14.pw:8888
>
> ![image](assets/15.3.PNG)
>
> Setelah memsukkan username dan password yang sesuai
>
> ![image](assets/15.4.PNG)
#

### Soal16
16. **Mengarahkan IP PROBOLINGGO 10.151.73.124 no 15 ke semerua14.pw**

> Test ip 10.151.73.124, masih menampilkan "it Works!"
>
> Edit .htaccess default pada PROBOLINGGO untuk meredirect ip
> PROBOLINGGO ke semerua14.pw
>
> ![image](assets/16.2.PNG)
>
> Ganti allowoverride none jadi all untuk directory /var/www/
>
> ![image](assets/16.1.PNG)
>
> Lalu restart apache
>
> Hasilnya saat mengakses 10.151.73.124
>
> ![image](assets/16.3.PNG)
#

### Soal17
17. **Mengubah semua gambar yang mengadung "semeru" ke "semeru.jpg"**

>
> Edit file .htaccess sesuai berikut
>
> ![image](assets/17.2.PNG)
>
> Tambahkan AllowOverride All untuk directory penanjakan.semerua14.pw

> ![image](assets/17.1.PNG)

> Hasilnya semua akses file gambar yang mengandung "semeru" akan
> diarahkan ke semeru.jpg
>
> ![image](assets/17.3.PNG)
#

##  Hambatan Selama Pengerjaan
-   apt-get install dan ping ke jaingan luar tiba-tiba baru bisa dilakukan ketika hari terakhir praktikum
-   sering nge lag, misalnya terkadang ketika pada putty di bash bye.sh seharusnya menutup semua UML secara otomatis, namun tidak terjadi apa-apa, sehingga harus di halt satu persatu
