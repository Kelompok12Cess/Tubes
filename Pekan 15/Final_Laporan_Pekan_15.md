**Dokumen Perencanaan Proyek: Perancangan Topologi Jaringan Enterprise PT. Nusantara Network - Pekan 15**

**Disusun oleh Kelompok [12]:**

1.  **Risky Nur Fatimah Bahar** - Network Architect
2.  **Anjas Geofany Diamare** - Network Engineer
3.  **Ahmad Daffa Alfattah** - Network Services Specialist
4.  **Dzakwan Fatih Fadhilah** - Security & Documentation Specialist

---
**Daftar Isi**

1. Pendahuluan<br>
    1.1 Latar Belakang<br>
    1.2 Tujuan Proyek<br>
    1.3 Ruang Lingkup Proyek<br>

2. Isi<br>
    2.1 Desain Topologi dan Desain Pengalamatan<br>
        2.1.1 Diagram Topologi Fisik dan Logis<br>
        2.1.2 Tabel Pengalamatan IP<br>
        2.1.3 Daftar Perangkat yang Dibutuhkan<br>
        2.1.4 Rencana Penerapan VLAN<br>

    2.2 Konfigurasi VLAN dan Trunking<br>
        2.2.1 Konfigurasi VLAN pada Switch dan Konfigurasi Trunk<br>

    2.3 Implementasi Routing antar-VLAN<br>
        2.3.1 Konfigurasi Router untuk Inter-VLAN Routing<br>
        2.3.2 Penjelasan Skema Routing<br>
        
    2.4 Implementasi Routing Statis dan Dinamis<br>
        2.4.1 Konfigurasi Routing Statis<br>
        2.4.2 Konfigurasi OSPF di Setiap Router<br>
        2.4.3 Konfigurasi WAN antar-Gedung

    2.5 Konfigurasi DHCP dan DNS Server<br>
        2.5.1 Topologi Jaringan dan Pembagian IP<br>
        2.5.2 Konfigurasi DHCP di Router/Server<br>
        2.5.3 Konfigurasi DNS Server untuk Resolusi Nama Internal<br>
    
    2.6 Konfigurasi NAT<br>
        2.6.1 Konfigurasi NAT di Router<br>
    
    2.7 Implementasi Access Control List (ACL)<br>
        2.7.1 Kebijakan Keamanan Jaringan<br>
        2.7.2 Konfigurasi ACL<br>
        2.7.3 Penjelasan Rule ACL<br>

3. Dokumentasi Laporan<br>
    3.1 Pengujian Hasil<br>
        3.1.1 Pengujian Hasil Konfigurasi dan Implementasi antar-VLAN<br>
        3.1.2 Pengujian Hasil Konektivitas Routing Statis dan Dinamis<br>
        3.1.3 Pengujian Hasil DHCP dan Konektivitas NAT<br>
        3.1.4 Pengujian Hasil Fitur ACL<br>
    
    3.2 Laporan Presentasi dan Video Simulasi<br>

4. Penutup<br>
    4.1 Kendala<br>
    4.2 Kesimpulan<br>
---

**1. Pendahuluan**<br>
--
**1.1 Latar Belakang**<br>
PT. Nusantara Network merupakan perusahaan yang bergerak di bidang teknologi informasi dengan perkembangan yang cukup pesat. Perusahaan ini memiliki dua lokasi operasional, yaitu Kantor Pusat di Gedung A dan Kantor Cabang di Gedung B, dengan total enam departemen yang mencakup IT, Keuangan, SDM, Server Farm, Marketing, dan Operasional. Seiring meningkatnya kebutuhan komunikasi antar departemen dan lokasi, diperlukan perancangan infrastruktur jaringan yang lebih aman, efisien, dan mudah dikelola. Rencana jaringan ini mencakup pemisahan setiap departemen ke dalam VLAN tersendiri untuk keamanan dan pengaturan lalu lintas data, koneksi WAN antar gedung dengan bandwidth yang terbatas, serta implementasi NAT untuk akses internet. Selain itu, layanan DHCP dan DNS akan diterapkan untuk mempermudah pengelolaan alamat IP dan resolusi nama, sementara penggunaan Access Control List (ACL) akan membantu membatasi akses antar departemen sesuai dengan kebijakan keamanan yang berlaku. Untuk mendukung keandalan jaringan, routing dinamis berbasis OSPF juga akan digunakan, dilengkapi dengan sistem monitoring dan manajemen jaringan terpusat agar performa dan keamanan jaringan tetap terjaga secara menyeluruh.<br>

**1.2 Tujuan Proyek**<br>
Tujuan utama dari proyek ini adalah :
- Merancang infrastruktur jaringan yang fleksibel dan aman digunakan untuk memenuhi kebutuhan operasional PT. Nusantara Network, serta mendukung struktur organisasi perusahaan secara menyeluruh.<br>
- Membangun segmentasi jaringan dengan menggunakan VLAN untuk setiap departemen, seperti TI, Keuangan, SDM, Server Farm, Marketing, dan Operasional, sehingga keamanan dan pengelolaan lalu lintas data lebih terkontrol.<br>
- Mensimulasikan implementasi desain jaringan melalui Cisco Packet Tracer untuk memastikan fungsionalitas dan performa jaringan berjalan optimal sesuai dengan rancangan.<br>
- Menerapkan konfigurasi routing inter-VLAN serta dynamic routing OSPF untuk memastikan konektivitas antar gedung melalui jaringan WAN, dengan memperhitungkan keterbatasan bandwith agar koneksi tetap stabil.<br>
- Mengimplementasikan layanan DHCP untuk mempermudah distribusi IP secara otomatis ke seluruh perangkat dalam jaringan, serta layanan DNS untuk memudahkan proses resolusi nama domain baik internal maupun eksternal.<br>
- Menggunakan Network Address Translation (NAT) agar perangkat di dalam jaringan lokal dapat mengakses internet melalui koneksi ISP yang tersedia secara efisien.<br>
- Menerapkan Access Control List (ACL) untuk membatasi dan mengatur akses antar departemen berdasarkan kebijakan keamanan perusahaan, untuk menjaga integritas dan kerahasiaan data.
- Mendokumentasikan seluruh tahapan mulai dari perancangan, konfigurasi, implementasi, hingga pengujian jaringan secara terstruktur sebagai referensi dan bukti kerja proyek.<br>
- Meningkatkan keterampilan anggota tim dalam kerja sama, manajemen proyek, serta kemampuan menyusun dan menyampaikan presentasi dengan baik.<br>

**1.3 Ruang Lingkup Proyek**<br>
Proyek ini mencakup berbagai aktivitas teknis dan penyusunan dokumentasi yang bertujuan untuk merancang infrastruktur jaringan tingkat enterprise, berdasarkan studi kasus di PT. Nusantara Network. Fokus utama dalam proyek ini melibatkan sejumlah kegiatan berikut :
- Perancangan topologi jaringan untuk seluruh departemen di PT. Nusantara Network, mencakup gedung kantor pusat dan gedung tambahan yang terhubung melalui jaringan WAN.<br>
- Penggunaan aplikasi Cisco Packet Tracer sebagai media simulasi dan implementasi virtual untuk memastikan konfigurasi berjalan sesuai rencana.<br>
- Penerapan segmentasi jaringan menggunakan VLAN untuk memisahkan trafik data antar departemen untuk meningkatkan keamanan dan efisiensi.<br>
- Konfigurasi routing inter-VLAN dan routing dinamis OSPF untuk menjamin komunikasi yang stabil dan optimal antar jaringan VLAN serta antar gedung.<br>
- Implementasi layanan DHCP untuk memudahkan pengalokasian IP secara otomatis dan layanan DNS untuk mendukung sistem penamaan domain internal maupun eksternal.<br>
- Penggunaan Network Address Translation (NAT) agar jaringan internal dapat terhubung dengan internet menggunakan koneksi ISP yang tersedia.<br>
- Penerapan Access Control List (ACL) untuk mengatur hak akses antar departemen sesuai dengan kebijakan keamanan yang diterapkan.<br>
- Pengujian hasil konfigurasi jaringan untuk memastikan setiap layanan berjalan dengan baik dan sesuai dengan kebutuhan perusahaan.<br>
- Penyusunan dokumentasi lengkap yang mencakup desain, konfigurasi, hasil simulasi, serta evaluasi terhadap performa jaringan.<br>
- Pembagian tugas dala tim untuk melatih kerja sama, manajemen waktu, serta meningkatkan kemampuan teknis setiap anggota dalam proyek ini.<br>

**2. Isi**<br>
--
**2.1 Desain Topologi dan Jaringan**<br>
**2.1.1 Diagram Topologi Fisik dan Logis**<br>
<img src="./Dokumentasi/Pekan 10/Cisco.jpg">
<br>
**Topologi Fisik**<br>
Topologi fisik menggambarkan bagaimana perangkat keras jaringan seperti router, switch, dan komputer terhubung secara nyata menggunakan kabel. Jaringan PT Nusantara Network terbagi menjadi dua lokasi utama: Kantor Pusat dan Kantor Cabang, keduanya menggunakan topologi tree (gabungan bus dan star).<br>

A. Kantor Pusat
- Router Pusat terhubung ke Main Switch di ruang server sebagai gateway jaringan internal, ke Kantor Cabang, dan ke luar jaringan.

- Main Switch mendistribusikan koneksi ke semua switch departemen dan menerima koneksi dari router serta server.

- Departemen IT: 2 switch, masing-masing menangani 20 komputer, langsung ke Main Switch.

- Departemen Keuangan: 2 switch, masing-masing 13 dan 12 komputer, terhubung ke Main Switch.

- Departemen SDM: 1 switch untuk 20 komputer, langsung ke Main Switch.<br>

Alur koneksi: Komputer → Switch Departemen → Main Switch → Router Pusat.<br>

B. Kantor Cabang
- Router Cabang terhubung ke Main Switch sebagai gateway lokal dan ke jaringan eksternal.

- Main Switch Cabang mendistribusikan koneksi ke switch di dua departemen.

- Departemen Marketing: 2 switch, masing-masing menangani 15 komputer.

- Departemen Operasional: 2 switch, masing-masing 20 dan 15 komputer.<br>

Alur koneksi: Komputer → Switch Departemen → Main Switch → Router Cabang.
<br>

**Topologi Logis**<br>
Topologi logis menunjukkan bagaimana jaringan diatur secara virtual, termasuk penggunaan VLAN, alokasi IP, subnetting, serta interaksi antar jaringan melalui perangkat aktif seperti router dan switch.

A. Penggunaan VLAN
- Tiap departemen dimasukkan ke VLAN berbeda untuk meningkatkan efisiensi, keamanan, dan pengelolaan.

- VLAN memisahkan lalu lintas jaringan antar departemen meskipun perangkat berada di switch fisik yang sama.

B. Alokasi IP dan Subnetting
- Setiap VLAN memiliki subnet IP sendiri, disesuaikan dengan jumlah perangkat pada masing-masing departemen.

- Menggunakan IP kelas C yang disubnet untuk efisiensi dan kemudahan pengelolaan.

- Tiap subnet dilengkapi gateway sebagai akses keluar VLAN.

C. Inter-VLAN Routing
- Komunikasi antar VLAN dilakukan melalui router, baik di kantor pusat maupun cabang.

- Router menggunakan interface trunk untuk membaca VLAN tag.

D. Keamanan dan Manajemen
- VLAN 100 digunakan sebagai VLAN manajemen, memungkinkan pemantauan seluruh switch dan router dari satu titik pusat.

**2.1.2 Tabel Pengalamatan IP**<br>
Adapun tabel pengalamatan IP pada PT. Nusantara Network adalah sebagai berikut.

| VLAN ID | Nama VLAN        | Subnet (Kelas C)      | Subnet Mask       | Gateway                  | Host Maks |
|---------|------------------|------------------------|--------------------|---------------------------|-----------|
| 10      | VLAN_IT          | 192.168.10.0/26        | 255.255.255.192    | 192.168.10.1              | 62        |
| 20      | VLAN_Keuangan    | 192.168.20.0/27        | 255.255.255.224    | 192.168.20.1              | 30        |
| 30      | VLAN_SDM         | 192.168.30.0/27        | 255.255.255.224    | 192.168.30.1              | 30        |
| 40      | VLAN_Server      | 192.168.40.0/28        | 255.255.255.240    | 192.168.40.1              | 14        |
| 50      | VLAN_Marketing   | 192.168.50.0/27        | 255.255.255.224    | 192.168.50.1              | 30        |
| 60      | VLAN_Operasional | 192.168.60.0/26        | 255.255.255.192    | 192.168.60.1              | 62        |
| 99      | VLAN_WAN_Link    | 192.168.99.0/30        | 255.255.255.252    | 192.168.99.1 (Gedung A) /<br>192.168.99.2 (Gedung B) | 2 |
| 100     | VLAN_Manajemen   | 192.168.100.0/28       | 255.255.255.240    | 192.168.100.1             | 14        |

**2.1.3 Daftar Perangkat yang Dibutuhkan**<br>
Perangkat yang diperlukan terdiri dari 5 perangkat, yaitu:
1. Cisco Router seri 1840. Perangkat jaringan layer 3 yang berfungsi untuk mengatur lalu lintas antar jaringan.
2. Cisco Switch Catalyst 2960. Switch layer 2 yang berfungsi untuk menghubungkan perangkat dalam 1 VLAN secara fisik.
3. Server yang berfungsi untuk menyediakan layanan untuk komputer lain dalam jaringan seprtti DHCP, DNS, dan lainnya.
4. Kabel Copper Straight-Throught yang digunakan untuk menghubungkan perangkat berbeda jenis. Contohnya seperti komputer ke swtich atau router ke switch.
5. Kabel Cross-Over yang digunakan utnuk menghubungkan perangkat sejenis. Contohnya seperti switch ke switch atua router ke router.

**2.1.4 Rencana Penerapan VLAN**<br>
Adapun rencana penerapan VLAN pada PT. Nusantara Network adalah sebagai berikut.
| VLAN ID | Nama VLAN        | Tujuan / Fungsi                                                                 |
|---------|------------------|----------------------------------------------------------------------------------|
| 10      | VLAN_IT          | Digunakan untuk perangkat dan user di Departemen IT (pengelolaan jaringan & sistem). |
| 20      | VLAN_Keuangan    | Mengelompokkan perangkat milik staf keuangan untuk keamanan data transaksi dan akuntansi. |
| 30      | VLAN_SDM         | Menyediakan segmentasi khusus bagi perangkat SDM (data karyawan, payroll, absensi). |
| 40      | VLAN_Server      | Khusus untuk server internal seperti DHCP, DNS, File Server, dan layanan web aplikasi. |
| 50      | VLAN_Marketing   | Memisahkan koneksi jaringan perangkat user Marketing agar tidak tercampur dengan divisi lain. |
| 60      | VLAN_Operasional | Didedikasikan untuk perangkat operasional yang menjalankan aktivitas logistik dan operasional lapangan. |
| 99      | VLAN_WAN_Link    | VLAN khusus untuk koneksi antar router pusat dan cabang (trunk WAN / routing antar gedung). |
| 100     | VLAN_Manajemen   | VLAN tertutup untuk akses admin dan monitoring jaringan (SSH, SNMP, dan manajemen switch/router). |
        
**2.2 Konfigurasi VLAN dan Trunking**<br>
**2.2.1 Konfigurasi VLAN pada Switch dan Konfigurasi Trunk**<br>
- Departemen IT<br>
VLAN 10 = VLAN_Manajemen
Interface range fa0/1-20
Interface fa0/24
<img src="./Dokumentasi/Pekan 11/konf dep it.jpg">
<img src="./Dokumentasi/Pekan 11/konf switch dep it (2).jpg">

- Departemen Keuangan<br>
VLAN 20 = VLAN_Keuangan
Interface range fa0/1-12
Interface fa0/24
<img src="./Dokumentasi/Pekan 11/konf swirc dep keuangan.jpg">
<img src="./Dokumentasi/Pekan 11/konf departemen keuangan.jpg">

- Departemen SDM<br>
VLAN 30 = VLAN_SDM
Interface range fa0/1-20
Interface fa0/24
<img src="./Dokumentasi/Pekan 11/konf switch dep sdm.jpg">

- Departemen Operasional<br>
VLAN 50 = VLAN_Marketing
Interface range fa0/1-15
VLAN 100 = VLAN_Manajemen
Interface fa0/24<br>
VLAN 50 = VLAN_Marketing
Interface range fa0/1-20
VLAN 100 = VLAN_Manajemen
Interface fa0/24
<img src="./Dokumentasi/Pekan 11/konf switch dep operasional.jpg">
<img src="./Dokumentasi/Pekan 11/switch dep operasionall.jpg">

- Departemen Marketing
VLAN 50 = VLAN_Marketing
Interface range fa0/1-15
VLAN 100 = VLAN_Manajemen
Interface fa0/24
<img src="./Dokumentasi/Pekan 11/konf switch dep marketing.jpg">

- Switch Farm
VLAN 40 = VLAN_Server
Interface range fa0/1-10
<img src="./Dokumentasi/Pekan 11/konf switch farm.jpg">
<img src="./Dokumentasi/Pekan 11/konf switch farm (2).jpg">
<img src="./Dokumentasi/Pekan 11/konf switch farm (3).jpg">
<img src="./Dokumentasi/Pekan 11/konf switch farm  .2.jpg">

**2.3 Implementasi Routing antar-VLAN**<br>
**2.3.1 Konfigurasi Router untuk Inter-VLAN Routing**<br>
<img src="./Dokumentasi/Pekan 11/konf rout utama.jpg">
<img src="./Dokumentasi/Pekan 11/konf router utama.jpg">
<img src="./Dokumentasi/Pekan 11/konf router utama (2).jpg">
<img src="./Dokumentasi/Pekan 11/router utama konf.jpg">

**2.3.2 Penjelasan Skema Routing**<br>
Konfigurasi yang dilakukan yaitu Konfigurasi Inter-VLAN routing menggunakan metode Router-on-a-Stick, di mana suatu interface fisik fa0/0 di router dibagi menjadi beberapa subinterface seperti fa0/0.10, fa0/0.20, hingga fa0/0.100. Masing-masing subinterface dikonfigurasi dengan encapsulation dot1Q untuk VLAN tertentu dan diberikan IP address sebagai gateway VLAN tersebut. Interface utama fa0/0 diaktifkan *no shutdown* agar semua subinterface bisa aktif dan siap digunakan untuk routing antar VLAN di jaringan.

**2.4 Implementasi Routing Statis dan Dinamis**<br>
**2.4.1 Konfigurasi Routing Statis**<br>
Menghubungkan beberapa VLAN atau subnet di Router Pusat dan Router Cabang melalui sub-interface dengan menggunakan encapsulation dot1Q, serta menghubungkan antar-router dengan routing statis agar semua jaringan bisa saling berkomunikasi.<br>
Router Pusat menggunakan FastEthernet0/0 untuk membuat beberapa sub-interface. Tiap sub-interface menangani 1 VLAN :
| Sub-interface       | VLAN ID | IP Address    | Subnet Mask   |
| ------------------- | ------- | ------------- | ------------- |
| FastEthernet0/0.10  | 10      | 192.168.10.1  | 255.255.255.0 |
| FastEthernet0/0.20  | 20      | 192.168.20.1  | 255.255.255.0 |
| FastEthernet0/0.30  | 30      | 192.168.30.1  | 255.255.255.0 |
| FastEthernet0/0.40  | 40      | 192.168.40.1  | 255.255.255.0 |
| FastEthernet0/0.100 | 100     | 192.168.100.1 | 255.255.255.0 |

Dan untuk konfigurasi di Router Cabang, seperti ini :
| Sub-interface       | VLAN ID | IP Address    | Subnet Mask   |
| ------------------- | ------- | ------------- | ------------- |
| FastEthernet0/0.10  | 10      | 192.168.11.1  | 255.255.255.0 |
| FastEthernet0/0.20  | 20      | 192.168.21.1  | 255.255.255.0 |
| FastEthernet0/0.30  | 30      | 192.168.31.1  | 255.255.255.0 |
| FastEthernet0/0.40  | 40      | 192.168.41.1  | 255.255.255.0 |
| FastEthernet0/0.100 | 100     | 192.168.101.1 | 255.255.255.0 |

Routing Statis memungkinkan kedua router mengetahui jalur ke semua subnet di sisi lainnya. Encapsulation Dot1Q digunakan agar router bisa mengenali VLAN.

**2.4.2 Konfigurasi OSPF di Setiap Router**<br>
Routing dinamis menggunakan protokol OSPF diimplementasikan untuk menghubungkan jaringan antar gedung melalui VLAN 99 sebagai jalur WAN. Setiap Router dikonfigurasi agar dapat saling bertukar informasi jaringan secara otomatis.<br>
Untuk konfigurasi seperti ini :
```
RouterPusat(config)# router ospf 1
RouterPusat(config-router)# network 192.168.10.0 0.0.0.255 area 0
RouterPusat(config-router)# network 192.168.20.0 0.0.0.255 area 0
RouterPusat(config-router)# network 192.168.30.0 0.0.0.255 area 0
RouterPusat(config-router)# network 192.168.40.0 0.0.0.255 area 0
RouterPusat(config-router)# network 192.168.100.0 0.0.0.255 area 0
RouterPusat(config-router)# network 192.168.99.0 0.0.0.255 area 0
```

```
RouterCabang(config)# router ospf 1
RouterCabang(config-router)# network 192.168.50.0 0.0.0.255 area 0
RouterCabang(config-router)# network 192.168.60.0 0.0.0.255 area 0
RouterCabang(config-router)# network 192.168.99.0 0.0.0.255 area 0
```
- VLAN 99 digunakan sebagai WAN link untuk pertukaran routing antar router.
- Semua jaringan lokal dari kedua router diumumkan ke OSPF melalui perintah.

**2.4.3 Koneksi WAN antar-Gedung**<br>
Setelah konfigurasi OSPF selesai, kedua router akan secara otomatis membuat entri di routing table masing-masing.<br>
Tabel di Router Pusat :
| Network Tujuan  | Next Hop         | Interface          | Jenis Route |
| --------------- | ---------------- | ------------------ | ----------- |
| 192.168.50.0/24 | via 192.168.99.2 | FastEthernet0/1.99 | OSPF        |
| 192.168.60.0/24 | via 192.168.99.2 | FastEthernet0/1.99 | OSPF        |

Tabel di Router Cabang :
| Network Tujuan   | Next Hop         | Interface          | Jenis Route |
| ---------------- | ---------------- | ------------------ | ----------- |
| 192.168.10.0/24  | via 192.168.99.1 | FastEthernet0/1.99 | OSPF        |
| 192.168.20.0/24  | via 192.168.99.1 | FastEthernet0/1.99 | OSPF        |
| 192.168.100.0/24 | via 192.168.99.1 | FastEthernet0/1.99 | OSPF        |

**2.5 Konfigurasi DHCP dan DNS Server**<br>
**2.5.1 Topologi Jaringan dan Pembagian IP**<br>
Perancangan dan konfigurasi DHCP Server membagi alamat IP secara otomatis kepada perangkat-perangkat yang terhubung di jaringan, khususnya untuk setiap departemen yang telah dibagi berdasarkan VLAN. Setiap VLAN mewakili satu departemen dan masing-masing VLAN memiliki network address, default gateway, serta DNS Server yang sama agar dapat melakukan resolusi nama ke domain lokal.<br>
| Departemen  | VLAN | Network         | Default Gateway | DNS Server    |
| ----------- | ---- | --------------- | --------------- | ------------- |
| IT          | 10   | 192.168.10.0/24 | 192.168.10.1    | 192.168.40.10 |
| Keuangan    | 20   | 192.168.20.0/24 | 192.168.20.1    | 192.168.40.10 |
| SDM         | 30   | 192.168.30.0/24 | 192.168.30.1    | 192.168.40.10 |
| Marketing   | 50   | 192.168.50.0/24 | 192.168.50.1    | 192.168.40.10 |
| Operasional | 60   | 192.168.60.0/24 | 192.168.60.1    | 192.168.40.10 |

**2.5.2 Konfigurasi DHCP di Router/Server**<br>
Untuk di Router Pusat, terdapat 3 VLAN yang di konfigurasi DHCP nya, yaitu VLAN10-IT, VLAN20-Keuangan, dan VLAN30-SDM.<br>
Config **Router Pusat**
<img src="./Dokumentasi/Pekan 13/router pusat .png">

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
<img src="./Dokumentasi/Pekan 13/router cabang.png">

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

**2.5.3 Konfigurasi DNS Server untuk Resolusi Nama Internal**<br>
Selain alamat IP dan Gateway, konfigurasi DHCP juga menyertakan **DNS Server internal (192.168.40.10)** dan nama domain **perusahaan.lokal** yang digunakan untuk resolusi nama internal.<br>
Dengan pengaturan ini, setiap perangkat yang menerima IP dari DHCP akan langsung bisa menggunakan layanan DNS untuk mengakses resource jaringan internal menggunakan nama, bukan IP. Untuk konfigurasi DNS ini dikonfig langsung di dalam pengaturan DHCP, seperti ini :
```
dns-server 192.168.40.10
domain-name perusahaan.lokal
```

**2.6 Konfigurasi NAT**<br>
**2.6.1 Konfigurasi NAT di Router**<br>
- Implementasi pada Router Pusat<br>
Router Pusat dikonfigurasi dengan sub-interface untuk VLAN manajemen **(FastEthernet0/0.100)** yang menggunakan IP **192.168.100.1/24**. Namun, terjadi konflik IP karena alamat tersebut tumpang tindih dengan konfigurasi sebelumnya di interface fisik **FastEthernet0/0**. Ini mengindikasikan perlunya perencanaan IP yang lebih teliti agar tidak terjadi overlapping.<br>
Selanjutnya, interface **FastEthernet0/1** digunakan sebagai penghubung ke RouterCabang dengan IP **10.0.0.1/30**, konfigurasi umum untuk point-to-point link. Interface ini ditandai sebagai ip nat inside, menandakan bahwa ia berada di sisi jaringan internal. Sebaliknya, **FastEthernet0/0** yang terhubung ke jaringan luar ditetapkan sebagai ip nat outside.<br>
Untuk menentukan subnet mana yang akan dikenai NAT, dibuat sebuah access list standar bernama **NAT_ACL_PUSAT**. ACL ini mengizinkan beberapa subnet lokal **(192.168.10.0, 20.0, 30.0, 40.0, 100.0)** serta alamat tambahan **(0.0.0.0 0.0.0.3)**. Access list ini kemudian digunakan dalam perintah NAT overload yang menerapkan translasi sumber alamat berdasarkan daftar tersebut melalui interface **FastEthernet0/0**.

- Implementasi pada Router Cabang<br>
RouterCabang juga memiliki konfigurasi NAT yang hampir serupa namun disesuaikan dengan topologinya. Interface **FastEthernet0/0** dikonfigurasi dengan IP **10.0.0.2/30** sebagai penghubung ke RouterPusat, sementara FastEthernet0/1 sebagai jalur ke ISP dengan IP publik **203.0.113.2/29**.<br>
Pada router ini, interface yang mengarah ke LAN **(FastEthernet0/0)** ditetapkan sebagai ip nat inside, dan interface yang mengarah ke luar **(FastEthernet0/1)** sebagai ip nat outside. Sama seperti di RouterPusat, dibuat access list **NAT_ACL** untuk menentukan subnet yang dikenai NAT, yaitu **192.168.50.0/24** dan **192.168.60.0/24**.<br>
NAT overload kemudian diaktifkan menggunakan ACL tersebut agar kedua subnet lokal dapat berbagi satu alamat IP publik. Untuk memastikan lalu lintas dari jaringan internal bisa mencapai jaringan pusat, dibuat rute statis ke subnet **192.168.50.0** dan **192.168.60.0** melalui alamat **10.0.0.1**, yaitu interface milik RouterPusat.<br>

**2.7 Implementasi Access Control List (ACL)**<br>
**2.7.1 Kebijakan Keamanan Jaringan**<br>
Kebijakan keamanan jaringan dirancang untuk membatasi akses antar VLAN sesuai dengan peran dan kebutuhan masing-masing departemen, guna meningkatkan kontrol, menjaga kerahasiaan data, dan mencegah potensi akses tidak sah.<br>

Adapun kebijakan keamanan yang diterapkan adalah sebagai berikut:

- VLAN IT(10) dan VLAN Keuangan(20) diperbolehkan mengakses Server(40):<br>
IT membutuhkan akses untuk manajemen teknis dan pemeliharaan server, sedangkan Keuangan memerlukan akses untuk sistem keuangan yang disimpan di server. Oleh karena itu, akses dari kedua VLAN ini diizinkan.<br>

- VLAN SDM(30) diblokir dari akses ke Server(40):<br>
Departemen SDM tidak memiliki keperluan langsung terhadap server utama, sehingga untuk menjaga keamanan data server, akses dari VLAN SDM dibatasi sepenuhnya.<br>

- VLAN Marketing(50) diblokir dari akses ke VLAN IT(10):<br>
Untuk menghindari potensi gangguan atau penyalahgunaan jaringan teknis, VLAN Marketing tidak diperbolehkan berkomunikasi dengan VLAN IT.<br>

- VLAN 40 hingga 60 diblokir dari akses ke VLAN 100 (Manajemen):<br>
Rentang VLAN 40–60 kemungkinan digunakan untuk pengguna umum atau tamu. Untuk mencegah intervensi atau potensi kebocoran data penting, akses ke VLAN 100 yang berisi departemen manajemen diblokir sepenuhnya.<br>

Alasan ACL:<br>
ACL digunakan untuk menerapkan kebijakan-kebijakan tersebut secara eksplisit di perangkat jaringan (biasanya router atau multilayer switch). Tanpa ACL, semua VLAN dapat saling berkomunikasi secara default, yang berpotensi menimbulkan risiko keamanan internal seperti penyalahgunaan data, pencurian informasi, atau kerusakan layanan.<br>

**2.7.2 Konfigurasi ACL**<br>
Berikut konfigurasi yang dilakukan dari Router Pusat :<br>
```
conf t
no ip access-list extended ACL_Tubes_Network
ip access-list extended ACL_Tubes_Network
 remark Izinkan VLAN IT (10) ke Server (40)
 permit ip 192.168.10.0 0.0.0.63 192.168.40.0 0.0.0.15

 remark Izinkan VLAN Keuangan (20) ke Server (40)
 permit ip 192.168.20.0 0.0.0.31 192.168.40.0 0.0.0.15

 remark Blok VLAN SDM (30) ke Server (40)
 deny ip 192.168.30.0 0.0.0.31 192.168.40.0 0.0.0.15

 remark Blok VLAN Marketing (50) ke VLAN IT (10)
 deny ip 192.168.50.0 0.0.0.31 192.168.10.0 0.0.0.63

 remark Blok semua VLAN ke VLAN Manajemen (100)
 deny ip 192.168.10.0 0.0.0.63 192.168.100.0 0.0.0.15
 deny ip 192.168.20.0 0.0.0.31 192.168.100.0 0.0.0.15
 deny ip 192.168.30.0 0.0.0.31 192.168.100.0 0.0.0.15
 deny ip 192.168.40.0 0.0.0.15 192.168.100.0 0.0.0.15
 deny ip 192.168.50.0 0.0.0.31 192.168.100.0 0.0.0.15
 deny ip 192.168.60.0 0.0.0.63 192.168.100.0 0.0.0.15

 remark Izinkan semua lalu lintas lain
 permit ip any any
exit
```

Penerapan ACL ke Interface :<br>
```
interface FastEthernet0/0.10
 ip access-group ACL_Tubes_Network out
exit

interface FastEthernet0/0.20
 ip access-group ACL_Tubes_Network out
exit

interface FastEthernet0/0.30
 ip access-group ACL_Tubes_Network out
exit

interface FastEthernet0/0.40
 ip access-group ACL_Tubes_Network out
exit

interface FastEthernet0/0.50
 ip access-group ACL_Tubes_Network out
exit

interface FastEthernet0/0.60
 ip access-group ACL_Tubes_Network out
exit
```

**2.7.3 Penjelasan Rule ACL**<br>
Berikut adalah penjabaran aturan-aturan ACL yang diterapkan untuk mendukung kebijakan keamanan:<br>
1. Mengizinkan VLAN IT dan Keuangan ke Server
```
access-list 110 permit ip 192.168.10.0 0.0.0.255 192.168.200.0 0.0.0.255
access-list 110 permit ip 192.168.20.0 0.0.0.255 192.168.200.0 0.0.0.255
```
Penjelasan: VLAN 10 (IT) dan VLAN 20 (Keuangan) diperbolehkan mengakses seluruh subnet server.<br>

2. Memblokir VLAN SDM ke Server
```
access-list 110 deny ip 192.168.30.0 0.0.0.255 192.168.200.0 0.0.0.255
```
Penjelasan: VLAN 30 (SDM) tidak diperbolehkan mengakses subnet server..<br>

3. Memblokir VLAN Marketing ke VLAN IT
```
access-list 110 deny ip 192.168.40.0 0.0.0.255 192.168.10.0 0.0.0.255
```
Penjelasan: VLAN 40 (Marketing) tidak dapat berkomunikasi dengan VLAN 10 (IT), mencegah gangguan atau akses ke sistem internal teknis.<br>

4. Memblokir VLAN 40–60 ke VLAN 100 (Manajemen)
```
access-list 110 deny ip 192.168.40.0 0.0.3.255 192.168.100.0 0.0.0.255
```
Penjelasan: Rentang subnet dari VLAN 40–60 diblokir dari mengakses VLAN 100 yang digunakan oleh manajemen, demi keamanan dan kerahasiaan.<br>
Berikut hasil dari ACL yang diterapkan :
| Sumber VLAN          | Tujuan Akses         | Hasil Pengujian                     | Status      |
| -------------------- | -------------------- | ----------------------------------- | ----------- |
| VLAN 10 (IT)         | Server (VLAN 40)    | Ping berhasil, akses layanan OK     | ✅ Diizinkan |
| VLAN 20 (Keuangan)   | Server (VLAN 40)    | Ping berhasil, akses layanan OK     | ✅ Diizinkan |
| VLAN 30 (SDM)        | Server (VLAN 40)    | Host Unreachable, akses ditolak         | ❌ Diblokir  |
| VLAN 50 (Marketing)  | VLAN 10 (IT)         | Ping timeout, tidak bisa komunikasi | ❌ Diblokir  |
| VLAN 40 (Server) | VLAN 100 (Manajemen) | Ping timeout, tidak bisa komunikasi | ❌ Diblokir  |
| VLAN 60 (Operasional)       | VLAN 100 (Manajemen) | Ping timeout, tidak bisa komunikasi | ❌ Diblokir  |

**3. Dokuementasi Laporan**<br>
--
**3.1 Pengujian Hasil**<br>
**3.1.1 Pengujian Hasil Konfigurasi dan Implementasi antar-VLAN**<br>
- Departemen Marketing
<img src="./Dokumentasi//Pekan 11/sw0-dmp.jpg">
<img src="./Dokumentasi/Pekan 11/dm.jpg">

- Departemen Operasional
<img src="./Dokumentasi/Pekan 11/sw0 do.jpg">
<img src="./Dokumentasi/Pekan 11/do.jpg">

- Departemen IT
<img src="./Dokumentasi/Pekan 11/sw0 di.jpg">
<img src="./Dokumentasi/Pekan 11/di.jpg">

- Departemen Keuangan
<img src="./Dokumentasi/Pekan 11/sw0 dk.jpg">
<img src="./Dokumentasi/Pekan 11/dk.jpg">

- Departemen SDM
<img src="./Dokumentasi/Pekan 11/dsdm.jpg">

- Server Farm
<img src="./Dokumentasi/Pekan 11/sw0 sf.jpg">

**3.1.2 Pengujian Hasil Konektivitas Routing Statis dan Dinamis**<br>
<img src="./Dokumentasi/Pekan 12/test ping pc dep it ged kan pusat ke pc dep marketing ged kan cabang.png">
<img src="./Dokumentasi/Pekan 12/test ping pc dep sdm ged kantor pusat ke pc dep operasional ged kan cabang.png">

**3.1.3 Pengujian Hasil DHCP dan Konektivitas NAT**<br>
- DHCP
<img src="./Dokumentasi/Pekan 13/uji dhcp 1.jpg">
<img src="./Dokumentasi/Pekan 13/uji dhcp 2.jpg">

- NAT
<img src="./Dokumentasi/Pekan 13/uji konek.jpg">

**3.1.4 Pengujian Hasil Fitur ACL**<br>
- VLAN IT
<img src="./Dokumentasi/Pekan 14/VLAN IT.png"><br>

- VLAN Keuangan
<img src="./Dokumentasi/Pekan 14/VLAN KEUANGAN.png"><br>

- VLAN SDM
<img src="./Dokumentasi/Pekan 14/VLAN SDM.png"><br>

- VLAN Marketing
<img src="./Dokumentasi/Pekan 14/VLAN MARKETING.png"><br>
<img src="./Dokumentasi/Pekan 14/VLAN MARKETING 2.png"><br>

- VLAN Operasional
<img src="./Dokumentasi/Pekan 14/VLAN OPERASIONAL.png"><br>

**3.2 Laporan Presentasi dan Video Simulasi**<br>
[Link PKT](https://www.canva.com/design/DAGoFWLbkhA/Mcfkwa37j-Og2t6XZBrvng/edit?utm_content=DAGoFWLbkhA&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)<br>
[Link Presentasi](https://www.canva.com/design/DAGoFWLbkhA/Mcfkwa37j-Og2t6XZBrvng/edit?utm_content=DAGoFWLbkhA&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)<br>
[Link Video Simulasi](https://drive.google.com/drive/folders/1mWnuGMo4lTgBATSEfp8jMBsz1ELMxt_z)<br>
[Link Github](https://github.com/Kelompok12Cess/Tubes)

**4. Penutup**<br>
--
**4.1 Kendala**<br>
- Selama menjalankan tugas besar saya memiliki tim yang sangat baik tetapi tim baik tidak hanya cukup jika tidak didampingi modul yang sangat bagus, dari kami terkadang bingung jika terjadi error atau bahkan bug dari cisco karena modul yang kurang sehingga kelompok kami mengalami kesusahan dalam menjalankan tugas besar dan bahkan kami tidak mengerti apa yang kurang dari konfigurasi yang kami buat untuk topologi tersebut.
- Dalam proses penyusunan laporan dokumentasi dari awal pengerjaan pekan 9 hingga sekarang pekan 15, pengerjaannya dilakukan dalam deadline waktu yang mepet di hari H pengumpulan. Sehingga laporan dikerjakan dengan sedikit terburu-buru dan hasilnya ada beberapa penjelasan yang kurang lengkap dan tidak menyertakan file simulasi di github pada pekan sebelumnya.

**4.2 Kesimpulan**<br>
Melalui rangkaian praktikum pada pertemuan 9 hingga 15, kami berhasil merancang dan mengimplementasikan sebuah jaringan enterprise yang kompleks dan terintegrasi sesuai dengan kebutuhan bisnis PT. Nusantara Network. Proyek ini menjadi wadah nyata untuk mengaplikasikan berbagai konsep jaringan yang telah dipelajari sebelumnya, mulai dari topologi jaringan, subnetting, VLAN, routing statis dan dinamis, hingga layanan jaringan seperti DHCP, DNS, dan NAT.

Setiap anggota kelompok menjalankan peran dengan tanggung jawab yang jelas dan saling melengkapi. Kolaborasi yang solid menjadi kunci keberhasilan dalam menyelesaikan seluruh tahapan proyek, mulai dari perencanaan awal, implementasi teknis, pengujian, hingga dokumentasi akhir.