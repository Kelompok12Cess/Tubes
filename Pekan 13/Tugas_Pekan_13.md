**Dokumen Perencanaan Proyek: Perancangan Topologi Jaringan Enterprise PT. Nusantara Network**

**Disusun oleh Kelompok [12]:**

1.  **Risky Nur Fatimah Bahar** - Network Architect
2.  **Anjas Geofany Diamare** - Network Engineer
3.  **Ahmad Daffa Alfattah** - Network Services Specialist
4.  **Dzakwan Fatih Fadhilah** - Security & Documentation Specialist

**Tanggal Pengumpulan:** Jumat, [Pekan 13], [2025]

---
**Daftar Isi**

1. Konfigurasi DHCP Server untuk Setiap Departemen<br>
    1.1 Topologi Jaringan & Pembagian IP<br>
    1.2 Konfigurasi DHCP di Router/Server<br>
    1.3 Screenshot Hasil Uji DHCP<br>

2. Implementasi DNS Server untuk Resolusi Nama Internal<br>
    2.1 Konfigurasi DNS Server<br>

3. Konfigurasi NAT untuk Akses Jaringan<br>
    3.1 Konfigurasi NAT di Router<br>
    3.2 Screenshot Hasil Uji Konektivitas<br>

---
**1. Konfigurasi DHCP Server untuk Setiap Departemen**<br>
**1.1 Topologi Jaringan & Pembagian IP**<br>
Perancangan dan konfigurasi DHCP Server membagi alamat IP secara otomatis kepada perangkat-perangkat yang terhubung di jaringan, khususnya untuk setiap departemen yang telah dibagi berdasarkan VLAN. Setiap VLAN mewakili satu departemen dan masing-masing VLAN memiliki network address, default gateway, serta DNS Server yang sama agar dapat melakukan resolusi nama ke domain lokal.<br>
| Departemen  | VLAN | Network         | Default Gateway | DNS Server    |
| ----------- | ---- | --------------- | --------------- | ------------- |
| IT          | 10   | 192.168.10.0/24 | 192.168.10.1    | 192.168.40.10 |
| Keuangan    | 20   | 192.168.20.0/24 | 192.168.20.1    | 192.168.40.10 |
| SDM         | 30   | 192.168.30.0/24 | 192.168.30.1    | 192.168.40.10 |
| Marketing   | 50   | 192.168.50.0/24 | 192.168.50.1    | 192.168.40.10 |
| Operasional | 60   | 192.168.60.0/24 | 192.168.60.1    | 192.168.40.10 |

**1.2 Konfigurasi DHCP di Router/Server**<br>
Untuk di Router Pusat, terdapat 3 VLAN yang di konfigurasi DHCP nya, yaitu VLAN10-IT, VLAN20-Keuangan, dan VLAN30-SDM.<br>
Config **Router Pusat**
<img src="./Dokumentasi/router pusat .png">

Konfigurasi di **Router Pusat** pada VLAN10-IT membuat pool DHCP untuk departemen IT dengan network *192.168.10.0/24* dan default gateway *192.168.10.1*.<br>
Config VLAN10-IT :
```
! Konfigurasi DHCP untuk VLAN10 - IT
ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp pool VLAN10-IT
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 192.168.40.10
 domain-name perusahaan.lokal
```

Konfigurasi di **Router Pusat** pada VLAN20-Keuangan membuat pool DHCP untuk departemen Keuangan dengan network *192.168.20.0/24* dan default gateway *192.168.20.1*.<br>
Config VLAN20-Keuangan :
```
! Konfigurasi DHCP untuk VLAN20 - KEUANGAN
ip dhcp excluded-address 192.168.20.1 192.168.20.10
ip dhcp pool VLAN20-KEUANGAN
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 192.168.40.10
 domain-name perusahaan.lokal
```

Konfigurasi di **Router Pusat** pada VLAN30-SDM membuat pool DHCP untuk departemen SDM dengan network *192.168.30.0/24* dan default gateway *192.168.30.1*.<br>
Config VLAN30-SDM :
```
! Konfigurasi DHCP untuk VLAN30 - SDM
ip dhcp excluded-address 192.168.30.1 192.168.30.10
ip dhcp pool VLAN30-SDM
 network 192.168.30.0 255.255.255.0
 default-router 192.168.30.1
 dns-server 192.168.40.10
 domain-name perusahaan.lokal
```

Config **Router Cabang**
<img src="./Dokumentasi/router cabang.png">

Konfigurasi di **Router Cabang** pada VLAN50-Marketing membuat pool DHCP untuk departemen Marketing dengan network *192.168.50.0/24* dan default gateway *192.168.50.1*.<br>
Config VLAN50-Marketing :
```
! Konfigurasi DHCP untuk VLAN50 - MARKETING
ip dhcp excluded-address 192.168.50.1 192.168.50.10
ip dhcp pool VLAN50-MARKETING
 network 192.168.50.0 255.255.255.0
 default-router 192.168.50.1
 dns-server 192.168.40.10
 domain-name perusahaan.lokal
```

Konfigurasi di **Router Cabang** pada VLAN60-Operasional membuat pool DHCP untuk departemen Operasional dengan network *192.168.60.0/24* dan default gateway *192.168.60.1*.<br>
Config VLAN60-Operasional :
```
! Konfigurasi DHCP untuk VLAN60 - OPERASIONAL
ip dhcp excluded-address 192.168.60.1 192.168.60.10
ip dhcp pool VLAN60-OPERASIONAL
 network 192.168.60.0 255.255.255.0
 default-router 192.168.60.1
 dns-server 192.168.40.10
 domain-name perusahaan.lokal
```

**1.3 Screenshot Hasil Uji DHCP**<br>
<img src="./Dokumentasi/uji dhcp 1.jpg">
<img src="./Dokumentasi/uji dhcp 2.jpg">

**2. Implementasi DNS Server untuk Resolusi Nama Internal**<br>
**2.1 Konfigurasi DNS Server**<br>
Selain alamat IP dan Gateway, konfigurasi DHCP juga menyertakan **DNS Server internal (192.168.40.10)** dan nama domain **perusahaan.lokal** yang digunakan untuk resolusi nama internal.<br>
Dengan pengaturan ini, setiap perangkat yang menerima IP dari DHCP akan langsung bisa menggunakan layanan DNS untuk mengakses resource jaringan internal menggunakan nama, bukan IP. Untuk konfigurasi DNS ini dikonfig langsung di dalam pengaturan DHCP, seperti ini :
```
dns-server 192.168.40.10
domain-name perusahaan.lokal
```

**3. Konfigurasi NAT untuk Akses Jaringan**<br>
**3.1 Konfigurasi NAT di Router**<br>
- Implementasi pada Router Pusat<br>
Router Pusat dikonfigurasi dengan sub-interface untuk VLAN manajemen **(FastEthernet0/0.100)** yang menggunakan IP **192.168.100.1/24**. Namun, terjadi konflik IP karena alamat tersebut tumpang tindih dengan konfigurasi sebelumnya di interface fisik **FastEthernet0/0**. Ini mengindikasikan perlunya perencanaan IP yang lebih teliti agar tidak terjadi overlapping.<br>
Selanjutnya, interface **FastEthernet0/1** digunakan sebagai penghubung ke RouterCabang dengan IP **10.0.0.1/30**, konfigurasi umum untuk point-to-point link. Interface ini ditandai sebagai ip nat inside, menandakan bahwa ia berada di sisi jaringan internal. Sebaliknya, **FastEthernet0/0** yang terhubung ke jaringan luar ditetapkan sebagai ip nat outside.<br>
Untuk menentukan subnet mana yang akan dikenai NAT, dibuat sebuah access list standar bernama **NAT_ACL_PUSAT**. ACL ini mengizinkan beberapa subnet lokal **(192.168.10.0, 20.0, 30.0, 40.0, 100.0)** serta alamat tambahan **(0.0.0.0 0.0.0.3)**. Access list ini kemudian digunakan dalam perintah NAT overload yang menerapkan translasi sumber alamat berdasarkan daftar tersebut melalui interface **FastEthernet0/0**.

- Implementasi pada Router Cabang<br>
RouterCabang juga memiliki konfigurasi NAT yang hampir serupa namun disesuaikan dengan topologinya. Interface **FastEthernet0/0** dikonfigurasi dengan IP **10.0.0.2/30** sebagai penghubung ke RouterPusat, sementara FastEthernet0/1 sebagai jalur ke ISP dengan IP publik **203.0.113.2/29**.<br>
Pada router ini, interface yang mengarah ke LAN **(FastEthernet0/0)** ditetapkan sebagai ip nat inside, dan interface yang mengarah ke luar **(FastEthernet0/1)** sebagai ip nat outside. Sama seperti di RouterPusat, dibuat access list **NAT_ACL** untuk menentukan subnet yang dikenai NAT, yaitu **192.168.50.0/24** dan **192.168.60.0/24**.<br>
NAT overload kemudian diaktifkan menggunakan ACL tersebut agar kedua subnet lokal dapat berbagi satu alamat IP publik. Untuk memastikan lalu lintas dari jaringan internal bisa mencapai jaringan pusat, dibuat rute statis ke subnet **192.168.50.0** dan **192.168.60.0** melalui alamat **10.0.0.1**, yaitu interface milik RouterPusat.

**3.2 Screenshot Hasil Uji Konektivitas**<br>
<img src="./Dokumentasi/uji konek.jpg">

**Kendala**<br>
- konfig dns server masih sering miss
- konfig nat agak susah
- vlan 50 dan 60 agak susah nyambung 
- request time out dari gedung A dan Gedung B
- konfigurasi server tidak bisa dipakai di server fisik 
- ip dhcp untuk vlan 50 dan 60 sering miss/ tidak dapat ip 
- tidak ada panduan mengerjakan yang tepat pada konfigurasi dhcp dan dns server

**Kesimpulan**<br>
Untuk minggu ini terdapat konfigurasi dhcp yang dimana ip didapatkan secara otomatis sehingga tidak perlu melakukan konfigurasi satu per satu tetapi semua tergantung vlan yang telah di konfigurasi sebelum nya, selanjutnya dns adalah domain yang digunakan untuk mencangkup lingkup dari internet tiap gedung dengan domain yang telah diberi nama serta nat buat menerjemahkan ip private jadi ip global sebelum mengirim data ke internet.