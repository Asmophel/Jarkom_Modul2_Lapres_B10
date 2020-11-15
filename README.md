# Jarkom_Modul2_Lapres_B10

### Jordan Gilbert - 0511184000084
### Fandi Wahyu R - 05111840000108

### Soal 1
Pada MALANG,
```nano /etc/bind/named.conf.local```

lalu ubah konfigurasi menjadi

![](.//img/1_1.PNG)

Buat folder semeru di dalam /etc/bind
```mkdir /etc/bind/semeru```

Copykan file db.local pada path /etc/bind ke dalam folder semeru
```cp /etc/bind/db.local /etc/bind/semeru/semerub10.pw```

kemudian buka file semerub10.pw
```nano /etc/bind/semeru/semerub10.pw```

edit menjadi file seperti ini
![](.//img/1_.PNG)

lalu restart Apache
```service bind9 restart```

lihat hasilnya dengan
```ping semerub10.pw```
![](.//img/1_3.PNG)

### Soal 2
untuk membuat alias,
```nano /etc/bind/semeru/semerub10.pw```

lalu edit seperti berikut,

![](.//img/2.PNG)

lalu lihat hasilnya dengan
```ping www.semerub10.pw```
pada client

![](.//img/2_1.PNG)

### Soal 3
![](.//img/malang.semerub10.pw.JPG)

Pada malang dibuka semeru.pw
```nano /etc/bind/semeru/semeru.pw```
ditambahan
```penanjakan  IN  A   10.151.83.92```
### Soal 4
![](.//img/Malang.named.conf.local.jpg)

pada Malang dibuka named.conf.local
```nano /etc/bind/named.conf.local```
ditambahkan
```
zone "83.151.10.in-addr.arpa" {
    type master;
    file "/etc/bind/semeru/83.151.10.in-addr.arpa";
};
```
![](.//img/Malang.83.151.10.JPG)

pada Malang buat 83.151.10.in-addr.arpa dari db.local
```cp /etc/bind/db.local /etc/bind/semeru/83.151.10.in-addr.arpa```
ditambahkan
```
83.151.10.in-addr.arpa. IN  NS semerub10.pw.
92                      IN  PTR semerub10.pw.
```
### Soal 5
![](.//img/Malang.named.conf.local.jpg)

pada Malang membuka named.conf.local
```nano /etc/bind/named.conf.local```
ditambahkan
```
zone "semerub10.pw" {
    type master;
    ditambahkan ini{
        notify yes;
        also-notify { 10.151.83.91; };
        allow-transfer { 10.151.83.91; }; 
    }
    file "/etc/bind/semeru/semerub10.pw";
};
```
![](.//img/Mojokerto.named.conf.local.jpg)

pada Mojokerto membuka named.conf.local
```/etc/bind/named.conf.local```
ditambahkan
```
zone "semerub10.pw" {
    type slave;
    masters { 10.151.83.92; }; 
    file "/var/lib/bind/semerub10.pw";
};
```
### Soal 6
![](.//img/malang.semerub10.pw.JPG)

pada Malang membuka semerub10.pw
```nano /etc/bind/semeru/semerub10.pw```
ditambahkan
```
ns1     IN  A   10.151.83.91
gunung  IN  NS  ns1

```
![](.//img/Malang.named.conf.options.JPG)

pada Malang membuka named.conf.option
```nano /etc/bind/named.conf.options```
ditambahkan
```allow-query{any;};```
![](.//img/Mojokerto.named.conf.options.jpg)

pada MojoKerto membuka named.conf.option
```nano /etc/bind/named.conf.options```
ditambahkan
```allow-query { any; };```
![](.//img/Mojokerto.named.conf.local.jpg)

pada MojoKerto membuka named.conf.local
```nano /etc/bind/named.conf.local```
ditambahkan
```
zone "gunung.semerub10.pw" {
    type master;
    file "/etc/bind/delegasi/gunung.semerub10.pw";
    allow-transfer { any; };
};
```
### Soal 7
membuat pada Mojokerto membuat file delegasi
```mkdir /etc/bind/delegasi```
![](.//img/Mojokerto.delegasi.gunung,.semerub10.pw.jpg)

membuka file delegasi
```cp /etc/bind/db.local /etc/bind/delegasi/gunung.semerub10.pw```
ditambahkan
```
gunung.semerub10.pw.
@       IN  NS  gunung.semerub10.pw.
@       IN  A   10.151.83.92
naik    IN  A   10.151.83.92
```
### Soal 8
Pada PROBOLINGGO
```nano /etc/apache2/sites-available/semerub10.pw```

lalu edit file menjadi seperti ini,
ubah ServerName dan DocumentRoot menjadi
```/var/www/semerub10.pw```
![](.//img/8.PNG)

lalu lihat hasilnya dengan membuka melalui browser

![](.//img/8_1.PNG)

### Soal 9
aktifkan
```a2enmod rewrite```
lalu restart apache
```service apache2 restart```

lalu pada
```nano /etc/apache2/sites-available/semerub10.pw```
edit menjadi seperti

![](.//img/9.PNG)

lalu pada
```nano /var/www/semerub10.pw/.htaccess```
edit menjadi

![](.//img/9_1.PNG)

lalu coba pada browser

![](.//img/9_2.PNG)

### Soal 10
Ekstrak file penanjakan, isinya adalah
![](.//img/10.PNG)

Tambahkan ServerName dan DocumentRoot pada
```nano /etc/apache2/sites-available/penanjakan.semerub10.pw```
menjadi

![](.//img/10_1.PNG)

lalu aktifkan a2ensite

![](.//img/10_2.PNG)

coba pada browser

![](.//img/10_3.PNG)

### Soal 11
Pada
```nano /etc/apache2/sites-available/penanjakan.semerub10.pw```

Tambahkan Option +Indexes untuk directory yang dapat diakses

Dan tambahkan Option -Indexes untuk directory yang private

![](.//img/11.PNG)

Pada browser, jika buka /public

![](.//img/11_1.PNG)

jika buka isi public

![](.//img/11_2.PNG)

### Soal 12

membuka file Penanjakan.semerub10
```/etc/apache2/site-available/Penanjakan.semerub10.pw```

ditambahkan
```ErrorDocument 404 /var/www/penanjakan.semerub10.pw/error/404.html```

![](.//img/Probolinggo.penanjakan.semerub10.pw.1.jpg)

### Soal 13
Pada
```nano /etc/apache2/sites-available/penanjakan.semerub10.pw```

Tambahkan
```Alias "/js" "/var/www/penanjakan.semerub10.pw/public/javasripts"```

![](.//img/13.PNG)

lalu restart apache
```service apache2 restart```

Pada browser

![](.//img/13_1.PNG)

### Soal 14
Pada
```nano /etc/apache2/sites-available/naik.gunung.semerub10.pw```
Setting virtual host di port 8888, tambahkan ServerName dan DocumentRoot untuk naik.gunung.semerub10.pw

![](.//img/14.PNG)

lalu pada
```nano /etc/apache2/ports.conf```
tambahkan
```Listen 8888```

![](.//img/14_1.PNG)

lalu restart apache
```service apache2 restart```

lalu hasilnya saat mengakses naik.gunung.semerub10.pw:888

![](.//img/15_3.PNG)

### Soal 15
Pada PROBOLINGGO
```htpasswd -c /etc/apache2/.htpasswd semeru```

lalu set username dan password

![](.//img/15_1.PNG)

lalu pada
```nano /etc/apache2/sites-available/naik.gunung.semerub10.pw```
tambahkan

```
<Directory "/var/www/naik.gunung.semerub10.pw">
    AuthType Basic
    AuthName "Restricted Content"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```

![](.//img/15_2.PNG)

lalu restart apache
```service apache2 restart```

pada browser akan menjadi

![](.//img/15.PNG)

setelah memasukkan uname dan pass

![](.//img/15_3.PNG)

### Soal 16
Pada 
```nano /etc/apache2/sites-available/default```

tambahkan
```Redirect permanent / http://semerub10.pw/```

![](.//img/16.PNG)

lalu restart apache
```service apache2 restart```

Saat mengakses 10.151.83.92 (IP PROBOLINGGO)

![](.//img/16_2.PNG)

### Soal 17
pada
```nano /var/www/penanjakan.semerub10.pw/.htaccess```
Tambahkan

![](.//img/17.PNG)

Tambahkan
```AllowOverride All```
pada
```nano /etc/apache2/sites-available/penanjakan.semerub10.pw```
![](.//img/17_1.PNG)

Hasilnya jika mengkases
```http://penanjakan.semerub10.pw/public/images/semeru123.jpg```

akan otomatis menuju
```http://penanjakan.semerub10.pw/public/images/semeru.jpg```