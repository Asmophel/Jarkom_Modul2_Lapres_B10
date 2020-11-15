# Jarkom_Modul2_Lapres_B10
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
### Soal 12
![](.//img/Probolinggo.penanjakan.semerub10.pw.1.jpg)

membuka file Penanjakan.semerub10
```/etc/apache2/site-available/Penanjakan.semerub10.pw```
ditambahkan
```ErrorDocument 404 /var/www/penanjakan.semerub10.pw/error/404.html```

