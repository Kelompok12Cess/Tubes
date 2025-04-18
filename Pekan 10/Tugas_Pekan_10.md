**Dokumen Perencanaan Proyek: Perancangan Topologi Jaringan Enterprise PT. Nusantara Network**

**Disusun oleh Kelompok [12]:**

1.  **Risky Nur Fatimah Bahar** - Network Architect
2.  **Anjas Geofany Diamare** - Network Engineer
3.  **Ahmad Daffa Alfattah** - Network Services Specialist
4.  **Dzakwan Fatih Fadhilah** - Security & Documentation Specialist

**Tanggal Pengumpulan:** Jumat, [Pekan 10], [2025]

---
**Daftar Isi**

4.  Desain Topologi & Skema Pengalamatan<br>
    4.1. Diagram Topologi Fisik dan Logis<br>
    4.2. Tabel Pengalamatan IP<br>
    4.3. Daftar Perangkat yang Dibutuhkan<br>
    4.4. Rencana Penerapan VLAN<br>
    4.5. Awal Implementasi Dalam Packet Tracer Dengan Screenshot Topologi Dasar<br>
---

**4. Desain Topologi & Skema Pengalamatan**<br>
**4.1. Diagram Topologi Fisik dan Logis**<br>
**4.1.1 Diagram Topologi**<br>
<img src=Cisco.jpg>

**4.1.2 Topologi Fisik**<br>
Topologi fisik menggambarkan bagaiaman perangkat keras(hardware) jaringan dihubungkan secara nyata menggunaakn kabel dan perangkat jaringan seperti switch, router, dan komputer. Pada PT Nusantara Network, jaringan terbagi menjadi dua lokasi yaitu Kantor Pusat dan Kantor Cabang.<br>

A. Kantor Pusat
Pada Kantor Pusat menggunakan topologi tree (pohon) yang merupakan gabungan dari topologi bus dan topologi star yang saling terhubung. Main switch pada ruang server menjadi pusat penghubung untuk semua switch pada departemen. Adapun rincian struktur detailnya sebagai berikut.
- Router Pusat terhubung pada Main Switch yang berfungsi sebagai gerbang (gateway) untuk semua jaringan di Kantor Pusat, penghubung ke kantor cabang, dan mengatur routing ke jaringan luar.
- Main Switch pada ruang server berfungsi sebagai titik penghubung dengan switch lainnya (central distribution switch) dengan menyebar koneksi dari Router ke lainnya. Main Switch menerima koneksi dari Router Pusat, Switch tiap departemen, dan server.
- Departemen IT memiliki 2 Switch yang terbagi menjadi 20 Komputer dalam 1 Switch. 2 Switch tersebut langsung terhubung pada Main Switch di Ruang Server.
- Departemen Keuangan memiliki 2 switch yang terbagi menjadi 13 Komputer dan 12 Komputer untuk setiap Switchnya. 2 Switch tersebut langsung terhubung pada Main Switch di Ruang Server.
- Departemen SDM memiliki 1 switch yang terhubung pada 20 Komputer dan langsung terhubung pada Main Switch di Ruang Server.

Sehingga alur koneksinya adalah Komputer Departemen -> Switch Departemen 1 atau 2 -> Main Switch Ruang Server -> Router Pusat.<br>

B. Kantor Cabang
Pada Kantor Cabang juga memiliki topologi tree (pohon) tetapi dalam skala kecil karena hanya memiliki 2 departemen. Adapun rinciannya sebagai berikut.

- Router Cabang terhubung ke Main Switch Kantor Cabang yang sebagai gerbang (gateway) untuk semua jaringan di Kantor Cabang dan mengatur routing ke jaringan luar.
- Main Switch Kantor Cabang terhubung ke seluruh switch di departemen kantor cabang. Berfungsi sebagai titik pengumpulan jaringan dari kedua departemen.
- Departemen Marketing memiliki 2 switch yang terbagi menajadi 15 Komputer dalam 1 switch. 2 Switch tersebut terhubung ke Main Switch Kantor Cabang.
- Departemen Operasional memiliki 2 Switch yang terbagi menjadi 20 Komputer dan 15 Komputer untuk setiap Switchnya. 2 Switch tersebut terhubung ke Main Switch Kantor Cabang.

Sehingga alur koneksinya adalah Komputer Departemen -> Switch Departemen 1 atau 2 -> Main Switch Kantor Cabang -> Router Cabang.

**4.1.3 Topologi Logis**<br>
Topologi logis menggambarkan bagaimana jaringan diatur secara virtual. Baik pengelompokan perangkat ke dalam VLAN, alokasi alamat IP, subnetting, dan interaksi antar jaringan yang diatur pada router dan switch.

A. Penggunaan VLAN
- Setiap departemen dikelompokkan ke dalam VLAN yang berbeda untuk meningkatkan efisiensi, keamanan, dan pengelolaan jaringan. 
- VLAN memungkinkan pemisahan trafik antar departemen meskipun perangkat mereka terhubung ke switch yang sama secara fisik.

B. Alokasi IP dan Subnetting
- Setiap VLAN diberikan subnet IP berbeda agar setiap jaringan tetap tertata rapi dan mudah untuk dikontrol
- Subnet disesuaikan dengan jumlah perangkat (host) pada tiap departemennya.
- Menggunakan IP kelas C yang disubnetting untuk efisiensi.
- Setiap subnet memiliki gateway IP untuk akses luar jaringan VLAN.

C. Inter-VLAN Routing <br>
Semua komunikasi antar departemen atau antara cabang dan pusat harus melalui router. Router Pusat dan Cabang memiliki interface trunk yang bisa membaca VLAN tag.

D. Keamanan dan Manajemen <br>
VLAN Manajemen (VLAN 100) memungkinkan untuk pemantauan seluruh jaringan ke semua Switch/Router.

**4.2. Tabel Pengalamatan IP**<br>
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

**4.3. Daftar Perangkat yang Dibutuhkan**<br>
Perangkat yang diperlukan terdiri dari 5 perangkat, yaitu:
1. Cisco Router seri 1840. Perangkat jaringan layer 3 yang berfungsi untuk mengatur lalu lintas antar jaringan.
2. Cisco Switch Catalyst 2960. Switch layer 2 yang berfungsi untuk menghubungkan perangkat dalam 1 VLAN secara fisik.
3. Server yang berfungsi untuk menyediakan layanan untuk komputer lain dalam jaringan seprtti DHCP, DNS, dan lainnya.
4. Kabel Copper Straight-Throught yang digunakan untuk menghubungkan perangkat berbeda jenis. Contohnya seperti komputer ke swtich atau router ke switch.
5. Kabel Cross-Over yang digunakan utnuk menghubungkan perangkat sejenis. Contohnya seperti switch ke switch atua router ke router.

**4.4. Rencana Penerapan VLAN**<br>
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

**4.5. Awal Implementasi Dalam Packet Tracer Dengan Screenshot Topologi Dasar**<br>
<img src=TOPOLOGI.png>
Kantor Pusat terdiri dari beberapa perangkat utama, yaitu:
1. Departemen IT : 
    - 1 Switch ke 20 Komputer
    - 1 Switch ke 20 Komputer <br>
    TOTAL : 2 Switch 40 Komputer

2. Departemen Keuangan :
    - 1 Switch ke 13 Komputer
    - 1 Switch ke 12 Komputer <br>
    TOTAL : 2 Switch 25 Komputer

3. Departemen SDM :
    - 1 Switch ke 20 Komputer
    TOTAL : 1 Switch 20 Komputer

4. Server Farm :
    - 1 Main Switch ke 10 Server
    TOTAL : 1 Main Switch 10 Server

5. Router Pusat

TOTAL perangkat :
- 1 Router
- 5 Switch
- 1 Main Switch
- 10 Server
- 85 Komputer

Detail Koneksi :
- Semua switch dari setiap departemen terhubung langsung ke main switch di ruang server.
- Main switch pusat dihubungkan ke Router Kantor Pusat menggunakan kabel straight-through.
- Dari router pusat terdapat koneksi WAN ke router cabang.
- Server diletakkan dalam satu jaaringan fisik dan terhubung ke main switch.

Kantor Cabang terdiri dari beberapa perangkat utama, yaitu:
1. Departemen Marketing :
    - 1 Switch ke 15 Komputer
    - 1 Switch ke 15 Komputer
    TOTAL : 2 Switch 30 Komputer

2. Departemen Operasional :
    - 1 Switch ke 20 Komputer
    - 1 Switch ke 15 Komputer
    TOTAL : 2 Switch 35 Komputer

3. Main Switch Kantor Cabang

4. Router Kantor Cabang

TOTAL perangkat :
- 1 Router
- 4 Switch
- 1 Main Switch
- 65 Komputer

Detail Koneksi :
- Setiap departemen memiliki 2 switch yang terhubung ke 1 main switch.
- Main switch terhubung ke router cabang dan mengarahkan data ke router pusat.

TOTAL PERANGKAT PT. NUSANTARA NETWORK :
- 2 Router
- 2 Main Switch
- 9 Switch
- 10 Server
- 150 Komputer

**Kendala dan Solusi**<br>
Selama pengerjaan terdapat 2 kendala Utama yang dihadapi, yaitu :
- Terjadi kesalahpahaman terhadap format laporan yang telah ditentukan untuk laporan, akibatnya format dan pembuatan laporan 1 tidak sesuai dengan ketentuan yang ada. <br>
Format dan laporan 2 sudah diperbaiki sesuai dengan yang seharusnya.

- Setelah melakukan implementasi di Packet Tracer, diketahui bahwa switch yang digunakan hanya mendukung maksimal 24 port Fast Ethernet, akibatnya terjadi perubahan pada sketsa desain awal yang hanya menggunakan 1 switch per departemen menjadi 2 switch setiap departemen.

**Kesimpulan**<br>
1. Hasil yang dicapai : <br>
Berhasil membagi struktur jaringan menjadi 2 lokasi utama, yaitu Kantor Pusat dan Kantor Cabang, dengan masing-masing menggunakan topologi _tree_ (pohon) fisik yang disesuaikan dengan kebutuhannya masing-masing. Merancang topologis jaringan secara efisien dengan memanfaatkan VLAN untuk setiap departemen. Dan terakhir, berhasil memvisualisasikan implementasi awal jaringan ke dalam Cisco Packet Tracer, menunjukkan koneksi antarperangkat yang terorganisir baik secara fisik maupun logis.

2. Pembelajaran yang didapat : <br>
- Pentingnya perencanaan topologi fisik dan logis dalam membangun infrastruktur jaringan yang efisien dan terstruktur.
- Penerapan VLAN memberikan efisiensi dan keamanan yang lebih baik di dalam organisasi dengan banyak divisi yang berbeda fungsi.
- Penggunaan subnetting memudahkan dalam pengalokasian IP agar tetap terkontrol dalam satu jaringan besar.
- Simulasi menggunakan Cisco Packet Tracer memberikan pembelajaran praktis mengenai interkoneksi perangkat, konfigurasi jaringan, dan potensi kendala yang bisa diantisipasi sejak awal sebelum jaringan bener-bener diterapkan.

**Lampiran**<br>
[Kelompok 12](https://github.com/Kelompok12Cess/Tubes/tree/main)
