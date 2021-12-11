# Jarkom-Modul-5-A05-2021

Kelompok A5 :
<li>05111840000138 - Gema Adi Perwira
<li>05111940000024 - Hanifa Fauziah
<li>05111940000111 - Evelyn Sierra

## Soal Shift Modul 5 Jaringan Komputer
<a href="https://docs.google.com/document/d/1Sc2jTlqmyM149yi4QzOGijyjPmSeEoy14Ajg9MnmkuY/edit">Soal Shift Modul 5 Jarkom 2021</a></br>
Setelah kalian mempelajari semua modul yang telah diberikan, Luffy ingin meminta bantuan untuk terakhir kalinya kepada kalian. Dan kalian dengan senang hati mau membantu Luffy.      
1. Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Luffy</br>
   Keterangan : 	      
        Doriki adalah DNS Server        
		Jipangu adalah DHCP Server       
		Maingate dan Jorge adalah Web Server      
		Jumlah Host pada Blueno adalah 100 host      
		Jumlah Host pada Cipher adalah 700 host      
		Jumlah Host pada Elena adalah 300 host       
		Jumlah Host pada Fukurou adalah 200 host  

2.	Karena kalian telah belajar subnetting dan routing, Luffy ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM. setelah melakukan subnetting
3.	Kalian juga diharuskan melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.
4.	Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

5.	Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.
6.	Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.
7.	Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.
Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut
8.	Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.
9.	Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.
Selain itu di reject
10.	Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate
Luffy berterima kasih pada kalian karena telah membantunya. Luffy juga mengingatkan agar semua aturan iptables harus disimpan pada sistem atau paling tidak kalian menyediakan script sebagai backup.

  
  
## Membuat Topologi
  
  <img width="731" alt="image" src="https://user-images.githubusercontent.com/80946219/145578526-b8bc9c78-7a3c-4dd4-8de2-60ad3db60e51.png">

## Melakukan Subnetting dan Routing
### Perhitungan VLSM
Topologi dan Pembagian **Subnet**
![image](https://user-images.githubusercontent.com/80946219/145581406-56c71eaf-7844-4e2d-9ca5-6f0bd1e92a3c.png)

**VLSM** Tree
![modul5](https://user-images.githubusercontent.com/80946219/145582207-c6838d20-ccb1-4b59-ad82-5879f257e187.jpg)

Hasil Pembagian **Subnet**
![image](https://user-images.githubusercontent.com/80946219/145581703-1f41d202-3c42-4b37-a682-431ffbe9c8b2.png)

### Melakukan Konfigurasi Interfaces pada GNS3
Pada **Foosha**
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
        address 192.171.0.1
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
         address 192.171.0.5
         netmask 255.255.255.252
```

Pada **Water7**
```
auto eth0
iface eth0 inet static
        address 192.171.0.2
        netmask 255.255.255.252
	gateway 192.171.0.1

auto eth1
iface eth1 inet static
        address 192.171.0.129
        netmask 255.255.255.128

auto eth2
iface eth2 inet static
         address 192.171.0.17
         netmask 255.255.255.248

auto eth3
iface eth3 inet static
         address 192.171.4.1
         netmask 255.255.252.0
```

Pada **Guanhao**
```
auto eth0
iface eth0 inet static
         address 192.171.0.6
         netmask 255.255.255.252
	 gateway 192.171.0.5

auto eth1
iface eth1 inet static
        address 192.171.2.1
        netmask 255.255.254.0

auto eth2
iface eth2 inet static
         address 192.171.1.1
         netmask 255.255.255.0

auto eth3
iface eth3 inet static
         address 192.171.0.25
         netmask 255.255.255.248
```

Pada **Doriki**
```
auto eth0
iface eth0 inet static
         address 192.171.0.18
         netmask 255.255.255.248
	 			 gateway 192.171.0.17
```

Pada **Jipangu**
```
auto eth0
iface eth0 inet static
         address 192.171.0.19
         netmask 255.255.255.248
	 			 gateway 192.171.0.17
```

Pada **Jorge**
```
auto eth0
iface eth0 inet static
         address 192.171.0.27
         netmask 255.255.255.248
	 			 gateway 192.171.0.25
```

Pada **Maingate**
```
auto eth0
iface eth0 inet static
         address 192.171.0.26
         netmask 255.255.255.248
	 			 gateway 192.171.0.25
```

Pada **Blueno**
```
auto eth0
iface eth0 inet static
        address 192.171.0.130
        netmask 255.255.255.128
        gateway 192.171.0.129
```

Pada **Cipher**
```
auto eth0
iface eth0 inet static
         address 192.171.4.2
         netmask 255.255.252.0
	 			 gateway 192.171.4.1
```

Pada **Elena**
```
auto eth0
iface eth0 inet static
        address 192.171.2.2
        netmask 255.255.254.0
				gateway 192.171.2.1
```

Pada **Fukorou**
```
auto eth0
iface eth0 inet static
         address 192.171.1.2
         netmask 255.255.255.0
				 gateway 192.171.1.1
```

### Melakukan Routing
Pada **Foosha**
```
route add -net 192.171.0.16 netmask 255.255.255.248 gw 192.171.0.2

route add -net 192.171.0.128 netmask 255.255.255.128 gw 192.171.0.2

route add -net 192.171.4.0 netmask 255.255.252.0 gw 192.171.0.2 

route add -net 192.171.0.24 netmask 255.255.255.248 gw 192.171.0.6

route add -net 192.171.2.0 netmask 255.255.254.0 gw 192.171.0.6   

route add -net 192.171.1.0 netmask 255.255.255.0 gw 192.171.0.6 
```

Melakukan cek dengan perintah `route -n`
![image](https://user-images.githubusercontent.com/80946219/145591741-db4cef33-2cfc-4c9e-ae1b-8d5772181684.png)

### Melakukan iptables
Pada **Foosha**, hal ini dilakukan agar bisa melakukan setting pada DNS Server, DHCP Server, DHCP Relay dan Client
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.171.0.0/21
```

## Mengatur interfaces pada semua Client 
Agar **Blueno**, **Cipher**, **Elena**, dan **Fukurou** bisa mendapatkan ip dinamis dari DHCP Server, ubah interfacesnya menjadi berikut ini.
```
auto eth0
iface eth0 inet dhcp
```

## Mengatur DNS Server
Pada **Doriki**

Melakukan **instalasi** `bind9`
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
                           
apt-get update

apt-get install bind9 -y
```

Melakukan **start** pada `bind9`
```
service bind9 start
```

## Mengatur DHCP Server
Pada **Jipangu**

Melakukan **instalasi**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update -y

apt-get install isc-dhcp-server -y
```

Cek apakah berhasil **diinstall**
```
dhcpd --version
```

Mengatur **interfaces** pada **DHCP Server**
```
echo "
INTERFACES=\"eth0\"
" > /etc/default/isc-dhcp-server
```

Mengatur subnet dan netmask pada file `/etc/dhcp/dhcpd.conf`
```
echo "
subnet 192.171.0.16 netmask 255.255.255.248 {
}

#Akses Blueno
subnet 192.171.0.128 netmask 255.255.255.128 {
    range 192.171.0.130 192.171.0.254;
    option routers 192.171.0.129;
    option broadcast-address 192.171.0.255;
    option domain-name-servers 192.171.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}

#Akses Cipher
subnet 192.171.4.0 netmask 255.255.252.0 {
    range 192.171.4.2 192.171.7.254;
    option routers 192.171.4.1;
    option broadcast-address 192.171.7.255; 
    option domain-name-servers 192.171.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}

#Akses Elena
subnet 192.171.2.0 netmask 255.255.254.0 {
    range 192.171.2.2 192.171.3.254;
    option routers 192.171.2.1;
    option broadcast-address 192.171.3.255; 
    option domain-name-servers 192.171.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}

#Akses Fukurou
subnet 192.171.1.0 netmask 255.255.255.0 {
    range 192.171.1.2 192.171.1.254;
    option routers 192.171.1.1;
    option broadcast-address 192.171.1.255; 
    option domain-name-servers 192.171.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
" > /etc/dhcp/dhcpd.conf
```

Melakukan restart pada **DHCP Server**
```                                
service isc-dhcp-server restart
```

## Mengatur DHCP Relay
### Pada Water7, Foosha, dan Guanhao
Melakukan instalasi **DHCP Relay**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update -y

apt-get install isc-dhcp-relay -y
```

Melakukan setting pada `/etc/default/isc-dhcp-relay`

Untuk **Water7** dan **Guanhao**
```
# What servers should the DHCP relay forward requests to?
SERVERS="192.171.0.19"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2 eth3"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

Untuk **Foosha**
```
# What servers should the DHCP relay forward requests to?
SERVERS="192.171.0.19"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

Cek apakah berhasil **diinstall**
```
dhcrelay --version
```

Melakukan restart pada **DHCP Relay**
```                                
service isc-dhcp-relay restart
```

## Melakukan DNS Forwarder 
Pada **Doriki** (**DNS Server**)

Mengatur isi file `/etc/bind/named.conf.options` menjadi
```
echo "
options {
        directory \"/var/cache/bind\";

         forwarders {
                192.168.122.1;
         };

        allow-query{any;};
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
```

## Konfigurasi iptables pada Foosha tanpa MASQUERADE
Menjalankan perintah **iptables** berikut ini. (tanpa tanda petik)
```
iptables -t nat -A POSTROUTING -s 192.171.0.0/16 -o eth0 -j SNAT --to-source "ip eth0"
```
Note: `ip eth0` yang digunakan bisa dicek dulu dengan menggunakan `ip a` pada **Foosha**. Karena ketika distart dan dimatikan lalu dihidupkan kembali maka `ip eth0` nya akan berubah

**Cek** pada client apakah settingan sudah berhasil dan client sudah bisa terhubung ke internet.
![image](https://user-images.githubusercontent.com/80946219/145590840-81b0d014-c54a-49ec-b948-ddec8d154555.png)
![image](https://user-images.githubusercontent.com/80946219/145591017-51c4ecb8-3cfa-4b4e-98e2-6103c70e5ce4.png)
![image](https://user-images.githubusercontent.com/80946219/145591052-56c6bef2-175f-4cd6-a3c6-5632f65c82c0.png)
![image](https://user-images.githubusercontent.com/80946219/145591110-1bf736b8-591e-402d-a8ea-4e5efb32ab62.png)

## Drop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan
Pada **Foosha**

Menjalankan perintah berikut ini.
```
iptables -A FORWARD -p tcp --dport 80 -d 192.171.0.16/29 -i eth0 -j DROP
```

Mengecek apakah sudah masuk perintahnya dengan perintah `iptables -L`
![image](https://user-images.githubusercontent.com/80946219/145592209-e82763f2-1c2a-4c2d-9b43-fc2441771279.png)

Pada **Doriki(DNS Server)** & **Jipangu(DHCP Server)**

Melakukan instalasi **netcat** 
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update -y

apt-get install netcat -y
```

Melakukan **testing** 

Pada **Doriki(DNS Server)** & **Jipangu(DHCP Server)**

```nc -l -p 80```

Pada **Foosha**

![image](https://user-images.githubusercontent.com/80946219/145593937-c325a2c7-0eaa-4cfd-8eb9-86ef65b01844.png)
![image](https://user-images.githubusercontent.com/80946219/145594009-103c8950-f8c3-45be-b969-89a052827939.png)

## Membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.
Pada **Doriki(DNS Server)** & **Jipangu(DHCP Server)**
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

Cek dengan perintah `iptables -L`
![image](https://user-images.githubusercontent.com/80946219/145594477-81b6e8ec-8757-42e7-9b11-93314f20b58f.png)
![image](https://user-images.githubusercontent.com/80946219/145594549-8c6b5e06-f0d8-4f3c-b345-2d25d4edcd6e.png)

Melakukan **testing** pada 4 Client
![image](https://user-images.githubusercontent.com/80946219/145594726-fa5cead8-91ce-4102-9223-9ff26378ea80.png)
![image](https://user-images.githubusercontent.com/80946219/145594768-c9194740-6f3b-4cf1-b269-63ac5713ace6.png)
![image](https://user-images.githubusercontent.com/80946219/145594814-35963abd-8271-4125-85eb-726976cbf9cf.png)
![image](https://user-images.githubusercontent.com/80946219/145594845-ae2c06eb-e919-4275-8303-12b661bb386b.png)

## Membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro
### Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis
Pada **Doriki (DNS Server)**
```
#tutup akses blueno
iptables -A INPUT -s 192.171.0.128/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.171.0.128/25 -j REJECT

#tutup akses cipher
iptables -A INPUT -s 192.171.4.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.171.4.0/22 -j REJECT
```

### Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya
Pada **Doriki (DNS Server)**
```
#tutup akses elena
iptables -A INPUT -s 192.171.2.0/23 -m time --timestart 07:00 --timestop 15:00 -j REJECT

#tutup akses FUKUROU
iptables -A INPUT -s 192.171.1.0/24 -m time --timestart 07:00 --timestop 15:00 -j REJECT
```

### Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya
Testing pada Client
![image](https://user-images.githubusercontent.com/80946219/145598254-bdbc3ddc-8e0e-4361-824f-caaf6af22244.png)
![image](https://user-images.githubusercontent.com/80946219/145598407-c5a25d49-9588-48df-90b2-070adfdcd245.png)
![image](https://user-images.githubusercontent.com/80946219/145598686-e82635b3-bb29-4d9f-b538-a82a141177c9.png)
![image](https://user-images.githubusercontent.com/80946219/145598707-a9d2b82a-b06b-4363-ab56-e46f65ac463b.png)

## Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate
Pada **Guanhao**
```
iptables -t nat -A PREROUTING -p tcp -d 192.171.0.18 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.171.0.26:80
iptables -t nat -A PREROUTING -p tcp -d 192.171.0.18 --dport 80 -j DNAT --to-destination 192.171.0.27:80
iptables -t nat -A POSTROUTING -p tcp -d 192.171.0.26 --dport 80 -j SNAT --to-source 192.171.0.18:80
iptables -t nat -A POSTROUTING -p tcp -d 192.171.0.27 --dport 80 -j SNAT --to-source 192.171.0.18:80
```
Pada **Maingate, Jorge dan Client**
Instalasi netcat
```
apt-get update -y
apt-get install netcat -y
```

Pada **Maingate & Jorge** 

```nc -l -p 80```

Pada **Client** yang ingin di testing 

```nc 192.171.0.18 80```

Tuliskan pesan pada **client**, maka pesan tersebut akan ditampilkan pada **maingate** dan **jorge** secara bergantian.

![image](https://user-images.githubusercontent.com/80946219/145601580-78a083ed-76ff-41bf-8900-34511e82fe85.png)

![image](https://user-images.githubusercontent.com/80946219/145601668-ecf6c075-8644-4abc-8c37-44b5838b3d9e.png)

![image](https://user-images.githubusercontent.com/80946219/145674233-233860aa-91f0-42af-b3b3-1b121e90a0ce.png)

![image](https://user-images.githubusercontent.com/80946219/145674212-81550e48-c8b8-4ba9-9636-f80e7ca46309.png)

# Kendala
Nomor 2 Output port 80 udah dilakukan filtered tapi ketika dilakukan nmap outputnya masih open

Bingung cara melakukan testing nya


