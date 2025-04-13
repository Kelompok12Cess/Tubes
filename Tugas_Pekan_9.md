**Dokumen Perencanaan Proyek: Perancangan Topologi Jaringan Enterprise PT. Nusantara Network**

**Disusun oleh Kelompok [12]:**

1.  **Risky Nur Fatimah Bahar** - Network Architect
2.  **Anjas Geofany Diamare** - Network Engineer
3.  **Ahmad Daffa Alfattah** - Network Services Specialist
4.  **Dzakwan Fatih Fadhilah** - Security & Documentation Specialist

**Tanggal Pengumpulan:** Minggu, [Pekan 9], [2025]

---
**Daftar Isi**

1.  Pendahuluan<br>
    1.1. Latar Belakang<br>
    1.2. Tujuan Proyek<br>
    1.3. Ruang Lingkup Proyek<br>

2.  Pembagian Kelompok dan Peran<br>

3.  Analisis Kebutuhan Jaringan PT. Nusantara Network<br>
    3.1. Struktur Organisasi & Lokasi<br>
    3.2. Kebutuhan Segmentasi dan Keamanan (VLAN & ACL)<br>
    3.3. Kebutuhan Konektivitas (Inter-VLAN, WAN, Internet)<br>
    3.4. Kebutuhan Layanan Jaringan (DHCP, DNS, NAT)<br>
    3.5. Kebutuhan Manajemen & Skalabilitas<br>

4.  Timeline Rencana Kerja Proyek (Pekan 9-15)<br>

5.  Sketsa Awal Desain Jaringan<br>
    5.1. Pendekatan Desain<br>
    5.2. Deskripsi Tekstual Sketsa Awal<br>

6.  Kendala dan Solusi<br>

7.  Kesimpulan<br>

8.  Lampiran<br>
---

**1. Pendahuluan**<br>
**1.1. Latar Belakang**<br>
PT. Nusantara Network merupakan perusahaan yang bergerak di bidang teknologi informasi dengan perkembangan yang cukup pesat. Perusahaan ini memiliki dua lokasi operasional, yaitu Kantor Pusat di Gedung A dan Kantor Cabang di Gedung B, dengan total enam departemen yang mencakup IT, Keuangan, SDM, Server Farm, Marketing, dan Operasional. Seiring meningkatnya kebutuhan komunikasi antar departemen dan lokasi, diperlukan perancangan infrastruktur jaringan yang lebih aman, efisien, dan mudah dikelola. Rencana jaringan ini mencakup pemisahan setiap departemen ke dalam VLAN tersendiri untuk keamanan dan pengaturan lalu lintas data, koneksi WAN antar gedung dengan bandwidth yang terbatas, serta implementasi NAT untuk akses internet. Selain itu, layanan DHCP dan DNS akan diterapkan untuk mempermudah pengelolaan alamat IP dan resolusi nama, sementara penggunaan Access Control List (ACL) akan membantu membatasi akses antar departemen sesuai dengan kebijakan keamanan yang berlaku. Untuk mendukung keandalan jaringan, routing dinamis berbasis OSPF juga akan digunakan, dilengkapi dengan sistem monitoring dan manajemen jaringan terpusat agar performa dan keamanan jaringan tetap terjaga secara menyeluruh.

**1.2. Tujuan Proyek**<br>
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

**1.3. Ruang Lingkup Proyek**<br>
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
- Pembagian tugas dala tim untuk melatih kerja sama, manajemen waktu, serta meningkatkan kemampuan teknis setiap anggota dalam proyek ini.

**2. Pembagian Kelompok dan Peran**

Dalam pelaksanaan proyek ini, pembagian peran dilakukan secara terstruktur untuk memastikan setiap aspek dari perancangan hingga implementasi jaringan berjalan dengan optimal. Setiap anggota kelompok bertanggung jawab sesuai dengan bidang keahlian masing-masing. Berikut rincian pembagian perannya :

* **Network Architect – Risky**  
  Sebagai perancang utama, Network Architect bertugas menyusun desain topologi jaringan secara menyeluruh. Selain itu, peran ini mencakup perencanaan detail skema pengalamatan IP dan pembagian subnet yang efisien, serta menyusun dokumentasi desain baik dalam bentuk visual seperti diagram maupun dalam bentuk penjelasan tertulis untuk memudahkan implementasi.

* **Network Engineer – Anjas**  
  Network Engineer bertanggung jawab dalam menerapkan konfigurasi routing, baik itu routing statis maupun dinamis, agar komunikasi antar jaringan dapat berjalan lancar. Selain itu, ia juga mengatur pengaturan VLAN beserta trunking untuk memisahkan dan mengelola lalu lintas jaringan antar departemen, serta memastikan koneksi WAN antar gedung terhubung dengan baik.

* **Network Services Specialist – Daffa**  
  Tugas Network Services Specialist mencakup penerapan layanan jaringan seperti DHCP untuk distribusi IP secara otomatis, DNS untuk penerjemahan nama domain, dan NAT untuk memungkinkan perangkat internal terhubung ke internet. Peran ini juga mencakup pengaturan layanan server tambahan apabila diperlukan, sekaligus memastikan semua layanan jaringan dapat terhubung secara end-to-end tanpa hambatan.

* **Security & Documentation Specialist – Dzakwan**  
  Peran ini berfokus pada aspek keamanan jaringan dengan cara menerapkan kebijakan keamanan melalui Access Control List (ACL) dan melakukan pengujian keamanan untuk memastikan konfigurasi yang diterapkan sesuai dan aman. Serta, bertanggung jawab meliputi penyusunan dokumentasi proyek secara menyeluruh dan mempersiapkan materi untuk presentasi project.

**3. Analisis Kebutuhan Jaringan PT. Nusantara Network**<br>
**3.1. Struktur Organisasi & Lokasi**<br>
PT. Nusantara Network memiliki dua lokasi operasional utama, yaitu Gedung A sebagai pusat kegiatan utama dan Gedung B sebagai kantor cabang. Masing-masing lokasi tersebut dilengkapi dengan perangkat jaringan dalam jumlah yang cukup banyak. Rincian kebutuhan perangkat di tiap lokasi dapat dilihat berikut ini:

* **Gedung A – Kantor Pusat:**
  - **Departemen IT:** Terdiri dari 40 unit komputer yang dikelola melalui satu unit switch. Departemen ini bertanggung jawab atas pengelolaan infrastruktur jaringan, pemeliharaan sistem, dan dukungan teknis bagi seluruh cabang dan pusat.
  - **Departemen Keuangan:** Memiliki 25 unit komputer yang terhubung dengan dedicated switch. Departemen ini fokus pada pengelolaan keuangan, akuntansi, dan pengawasan anggaran perusahaan.
  - **Departemen SDM (HR):** Terdapat 20 komputer yang mendukung aktivitas pengelolaan karyawan, rekrutmen, serta administrasi personalia.
  - **Server Farm:** Dilengkapi dengan 10 unit server yang terhubung melalui switch khusus. Fungsi utama server farm ini adalah menyimpan data penting perusahaan, mengelola aplikasi internal, dan mendukung kebutuhan layanan cloud untuk seluruh organisasi.

* **Gedung B – Kantor Cabang:**
  - **Departemen Marketing:** Dengan 40 komputer yang terkoneksi melalui switch, departemen ini bertanggung jawab atas promosi, pengembangan pasar, dan interaksi dengan pelanggan.
  - **Departemen Operasional:** Sebanyak 40 komputer digunakan oleh tim operasional untuk mendukung kelancaran proses bisnis harian, logistik, dan layanan pelanggan.

Setiap kantor dilengkapi dengan router yang menghubungkan seluruh perangkat di masing-masing gedung ke jaringan perusahaan, sekaligus menjadi penghubung antara kantor pusat dan kantor cabang melalui jalur WAN.

**3.2. Kebutuhan Segmentasi dan Keamanan (VLAN & ACL)**

**3.3. Kebutuhan Konektivitas (Inter-VLAN, WAN, Internet)**

**3.4. Kebutuhan Manajemen & Skalabilitas**




**4. Timeline Rencana Kerja Proyek (Pekan 9-15)**
| Pekan | Tanggal Deadline (Jumat, 23:59 WIB) | Tugas Utama Kelompok                                                                 | Deliverable                                    | Penanggung Jawab Utama Koordinasi |
| :---- | :---------------------------------- | :----------------------------------------------------------------------------------- | :--------------------------------------------- | :-------------------------------- |
| **9** | [Tanggal Pekan 9]                   | Identifikasi kebutuhan, pembagian tugas tim, diskusi ide awal, dan rancangan desain | Dokumen Perencanaan Proyek                     | Risky (Architect)           |
| **10**| [Tanggal Pekan 10]                  | Finalisasi topologi jaringan, alokasi IP, rencana VLAN, dan pemilihan perangkat      | Dokumen Desain Jaringan (Diagram, Tabel IP)   | Risky (Architect)                |
| **11**| [Tanggal Pekan 11]                  | Penerapan topologi dasar, konfigurasi VLAN & trunking, serta routing antar VLAN     | Laporan Implementasi Tahap 1 + File Simulasi  | Anjas (Engineer)                  |
| **12**| [Tanggal Pekan 12]                  | Konfigurasi routing statis (opsional), implementasi OSPF antar gedung, simulasi WAN | Laporan Implementasi Tahap 2 + File Simulasi  | Anjas (Engineer)                  |
| **13**| [Tanggal Pekan 13]                  | Pengaturan layanan DHCP, DNS internal/eksternal, dan NAT untuk akses internet       | Laporan Implementasi Tahap 3 + File Simulasi  | Daffa (Services)                  |
| **14**| [Tanggal Pekan 14]                  | Implementasi ACL antar departemen, uji jaringan menyeluruh, dan troubleshooting      | Laporan Implementasi Tahap 4 + File Simulasi  | Dzakwan (Security)                |
| **15**| **Rabu**, [Tanggal Pekan 15], 23:59 WIB | Penyusunan dokumentasi akhir, persiapan presentasi, serta pembuatan video demo     | Laporan Akhir, Video Demo, Slide Presentasi   | Dzakwan (Documentation)           |

**5.  Sketsa Awal Desain Jaringan**<br>
Sketsa awal ini bertujuan untuk menggambarkan rancangan dasar jaringan PT. Nusantara Network, mencakup koneksi antar perangkat di Kantor Pusat dan Kantor Cabang sebagai panduan dalam implementasi. Berikut rancangan sketsa awal :<br>

<img src=SketsaAwal.png>

- **Gedung A – Kantor Pusat:**
Pada Kantor Pusat (Gedung A) terdapat 4 lokasi yaitu Departemen IT, Departemen Keuangan, Departemen SDM, dan Server Farm. <br>
Setiap departemen dalam menyambungkan komputer ke switch menggunakan topologi bus agar digunakan untuk instalasi kabel yang lebih hemat dan mudah dalam ruang terbatas, serta cocok untuk konfigurasi yang tidak memerlukan bandwidth besar antar perangkat dalam satu departemen.
Sedangkan dalam menyambungkan setiap switch ke main switch menggunakan topologi star agar setiap departemen terhubung langsung dan independen ke main switch, sehingga jika satu link putus, jaringan lainnya tetap aktif (tidak bergantung satu sama lain).

  **Rincian Perangkat Jaringan - Gedung A:**
  | Lokasi             | Perangkat     | VLAN              | Keterangan                                                             |
  |--------------------|---------------|-------------------|------------------------------------------------------------------------|
  | Departemen IT      | 1 Switch      | VLAN 10 (IT)      | Terhubung ke 40 komputer dan main switch Gedung A                      |
  | Departemen Keuangan| 1 Switch      | VLAN 20 (Finance) | Terhubung ke 25 komputer dan main switch Gedung A                      |
  | Departemen SDM     | 1 Switch      | VLAN 30 (SDM)     | Terhubung ke 20 komputer dan main switch Gedung A                      |
  | Server Farm        | 1 Main Switch | VLAN 99 (Server)  | Terhubung ke 10 server dan router Gedung A                             |
  |                    | 1 Router      | -                 | Terhubung ke Router Gedung B                                           |

  ---
<br>

- **Gedung B – Kantor Cabang:**
Pada Kantor Cabang (Gedung B) terdapat 2 lokasi yaitu Departemen Marketing dan Departemen Operasional.<br>
Setiap departemen dalam menyambungkan komputer ke switch menggunakan topologi bus, sedangkan menyambungkan switch ke main switch menggunakan topologi star.

  **Rincian Perangkat Jaringan - Gedung B:**
  | Lokasi                | Perangkat     | VLAN                    | Keterangan                                                      |
  |-----------------------|---------------|-------------------------|-----------------------------------------------------------------|
  | Departemen Marketing  | 1 Main Switch | VLAN 40 (Marketing)     | Terhubung ke 30 komputer ke router Gedung B                     |
  | Departemen Operasional| 1 Switch      | VLAN 50 (Operasional)   | Terhubung ke 35 komputer ke main switch Gedung B                |
  |                       | 1 Router      | -                       | Terhubung ke Router Gedung A                                    |

  ---
<br>
Setiap gedung memiliki main switch sebagai pusat koneksi lokal. Switch per departemen menghubungkan komputer dengan topologi bus, lalu disambung ke main switch dengan topologi star. Router per gedung bertugas untuk interkoneksi antar gedung dan ke internet.

**6. Kendala dan Solusi**

**7. Kesimpulan**

**8. Lampiran**
