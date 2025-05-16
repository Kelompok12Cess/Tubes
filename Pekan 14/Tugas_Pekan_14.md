**Dokumen Perencanaan Proyek: Perancangan Topologi Jaringan Enterprise PT. Nusantara Network**

**Disusun oleh Kelompok [12]:**

1.  **Risky Nur Fatimah Bahar** - Network Architect
2.  **Anjas Geofany Diamare** - Network Engineer
3.  **Ahmad Daffa Alfattah** - Network Services Specialist
4.  **Dzakwan Fatih Fadhilah** - Security & Documentation Specialist

**Tanggal Pengumpulan:** Jumat, [Pekan 14], [2025]

---
**Daftar Isi**

1. Implementasi Access Control List (ACL)<br>
    1.1 Kebijakan Keamanan Jaringan<br>
    1.2 Konfigurasi ACL<br>
    1.3 Penjelasan Rule ACL<br>

2. Pengujian Fitur Jaringan<br>
    2.1 Hasil Pengujian<br>
    2.2 Analisis Pengujian<br>

3. Troubleshooting dan Perbaikan<br>
    3.1 Identifikasi Masalah<br>

---
**1. Implementasi Access Control List (ACL)**<br>
**1.1 Kebijakan Keamanan Jaringan**<br>
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

**1.2 Konfigurasi ACL**<br>
<img src="./Dokumentasi/conft cli 1.png">
<img src="./Dokumentasi/conft cli 2.png">
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

**1.3 Penjelasan Rule ACL**<br>
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

**2. Pengujian Fitur Jaringan**<br>
**2.1 Hasil Pengujian**<br>
**VLAN IT**
<img src="./Dokumentasi/VLAN IT.png"><br>
**VLAN Keuangan**
<img src="./Dokumentasi/VLAN KEUANGAN.png"><br>
**VLAN SDM**
<img src="./Dokumentasi/VLAN SDM.png"><br>
**VLAN Marketing**
<img src="./Dokumentasi/VLAN MARKETING.png"><br>
**VLAN Operasional**
<img src="./Dokumentasi/VLAN OPERASIONAL.png"><br>
**VLAN Marketing**
<img src="./Dokumentasi/VLAN MARKETING 2.png"><br>

Pengujian dilakukan untuk memastikan bahwa Access Control List (ACL) telah berfungsi sesuai dengan kebijakan keamanan yang diterapkan. Pengujian dilakukan dengan cara mengirimkan ping dan mencoba akses ke server atau VLAN tertentu dari masing-masing VLAN sumber. Berikut hasilnya:
| Sumber VLAN          | Tujuan Akses         | Hasil Pengujian                     | Status      |
| -------------------- | -------------------- | ----------------------------------- | ----------- |
| VLAN 10 (IT)         | Server (VLAN 40)    | Ping berhasil, akses layanan OK     | ✅ Diizinkan |
| VLAN 20 (Keuangan)   | Server (VLAN 40)    | Ping berhasil, akses layanan OK     | ✅ Diizinkan |
| VLAN 30 (SDM)        | Server (VLAN 40)    | Host Unreachable, akses ditolak         | ❌ Diblokir  |
| VLAN 50 (Marketing)  | VLAN 10 (IT)         | Ping timeout, tidak bisa komunikasi | ❌ Diblokir  |
| VLAN 40 (Server) | VLAN 100 (Manajemen) | Ping timeout, tidak bisa komunikasi | ❌ Diblokir  |
| VLAN 60 (Operasional)       | VLAN 100 (Manajemen) | Ping timeout, tidak bisa komunikasi | ❌ Diblokir  |

**2.2 Analisis Pengujian**<br>
Berdasarkan hasil di atas, dapat disimpulkan bahwa konfigurasi ACL telah berjalan sesuai dengan kebijakan keamanan yang telah dirancang:<br>

Akses yang Diizinkan: VLAN IT dan Keuangan berhasil melakukan komunikasi dengan server yang ada di VLAN Server, membuktikan bahwa rule permit ACL untuk subnet tersebut bekerja sebagaimana mestinya.<br>

Akses yang Diblokir: VLAN SDM, Marketing, dan rentang VLAN 40–60 terbukti tidak dapat mengakses tujuan yang telah dibatasi. Hal ini menunjukkan bahwa rule deny ACL diterapkan secara efektif dan tepat sasaran.<br>

**3. Troubleshooting**<br>
**3.1 Identifikasi Masalah**<br>
Selama proses pengujian komunikasi antar VLAN setelah penerapan ACL, ditemukan sebuah masalah sebagai berikut:<br>
- Pada VLAN 30 (SDM) dapat mengakses Server pada VLAN (40), padahal berdasarkan kebijakan, akses harusnya tidak diizinkan.<br>
- Pada VLAN 40-60 dapat mengakses VLAN Manajemen (100), padahal berdasarkan kebijakan, akses harusnya tidak diijinkan.<br>

**Kendala**<br>
Pada penerapan awal dalam kebijakan keamanan jaringan untuk akses ke VLAN Manajemen (100), tidak mengizinkan atau memblokir VLAN 10-60. Tetapi dikarenakan VLAN 10-30 dapat mengakses VLAN 100, jadi melakukan perubahan dan hanya dapat memblokir VLAN 40-60

**Kesimpulan**<br>
Untuk minggu ini implementasi Access Control List (ACL) berhasil membatasi akses antar VLAN sesuai dengan kebijakan keamanan jaringan yang telah ditentukan. Pengujian menunjukkan bahwa rule ACL berfungsi dengan baik dalam mengizinkan atau memblokir komunikasi antar departemen sesuai kebutuhan. Meskipun sempat ditemukan kendala pada akses VLAN tertentu, masalah tersebut berhasil diidentifikasi dan diperbaiki melalui proses troubleshooting. Secara keseluruhan, penerapan ACL meningkatkan keamanan dan segmentasi jaringan secara signifikan.