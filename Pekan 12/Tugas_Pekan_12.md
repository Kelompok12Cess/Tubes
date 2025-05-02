**Dokumen Perencanaan Proyek: Perancangan Topologi Jaringan Enterprise PT. Nusantara Network**

**Disusun oleh Kelompok [12]:**

1.  **Risky Nur Fatimah Bahar** - Network Architect
2.  **Anjas Geofany Diamare** - Network Engineer
3.  **Ahmad Daffa Alfattah** - Network Services Specialist
4.  **Dzakwan Fatih Fadhilah** - Security & Documentation Specialist

**Tanggal Pengumpulan:** Jumat, [Pekan 12], [2025]

---
**Daftar Isi**

1. Implementasi Routing Statis<br>
    1.1 Link File Simulasi<br>
    1.2 Konfigurasi Routing Statis<br>
    1.3 Dokumentasi CLI<br>

2. Implementasi Routing Dinamis<br>
    2.1 Konfigurasi OSPF di Setiap Router<br>
    2.2 Dokumentasi CLI<br>

3. Simulasi Koneksi WAN Antar-Gedung<br>
    3.1 Tabel Routing & Penjelasan<br>
    3.2 Screenshot Hasil Uji Konektivitas<br>

4. Analisis & Evaluasi<br>
    4.1 Perbandingan Routing Statis vs OSPF<br>
    4.2 Kesimpulan Performa<br>

---
**1. Implementasi Routing Statis**<br>
**1.1 Link File Simulasi**<br>
[Link PKT](https://github.com/Kelompok12Cess/Tubes/tree/main/Pekan%2012)

**1.2 Konfigurasi Routing Statis**<br>
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

**1.3 Dokumentasi CLI**<br>
<img src="./Dokumentasi/Konfigurasi Routing Statis - router pusat.png">
<img src="./Dokumentasi/Konfigurasi Routing Statis - router cabang.png">

**2. Implementasi Routing Dinamis**<br>
**2.1 Konfigurasi OSPF di Setiap Router**<br>
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

**2.2 Dokumentasi CLI**
<img src="./Dokumentasi/konfigurasi Routing Dinamis - router pusat.png">
<img src="./Dokumentasi/konfigurasi Routing Dinamis - router cabang.png">

**3. Simulasi Koneksi WAN Antar_Gedung**<br>
**3.1 Tabel Routing & Penjelasan**
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

**3.2 Screenshot Hasil Uji Konektivitas**
<img src="./Dokumentasi/test ping pc dep it ged kan pusat ke pc dep marketing ged kan cabang.png">
<img src="./Dokumentasi/test ping pc dep sdm ged kantor pusat ke pc dep operasional ged kan cabang.png">

**4. Analisis & Evaluasi**<br>
**4.1 Perbandingan Routing Statis vs OSPF**
| Aspek                     | Routing Statis                                 | Routing Dinamis (OSPF)                      |
| ------------------------- | ---------------------------------------------- | ------------------------------------------- |
| Skalabilitas              | Kurang baik untuk banyak jaringan              | Sangat baik dan otomatis                    |
| Manajemen Perubahan       | Manual dan rawan kesalahan                     | Otomatis mendeteksi perubahan topologi      |
| Kemudahan Konfigurasi     | Sulit jika banyak subnet                       | Cukup mudah dan cepat                       |
| Jalur Backup | Harus dikonfigurasi manual                     | Didukung secara otomatis oleh OSPF          |
| Efisiensi Bandwidth       | Tidak menggunakan bandwidth untuk routing info | Gunakan sedikit bandwidth untuk OSPF packet |


**4.2 Kesimpulan Performa**
Berdasarkan hasil simulasi dan pengamatan routing table, OSPF mampu mengelola rute antar gedung secara efisien, dinamis, dan andal.
Dengan hanya menambahkan satu entri VLAN 99 sebagai link antar-router, seluruh jaringan dapat saling terhubung tanpa konfigurasi rute statis satu per satu.<br>
OSPF menjadi solusi ideal untuk jaringan menengah hingga besar yang memiliki struktur bertingkat dan subnet yang banyak. Dengan fitur seperti auto route discovery dan topologi adaptif, performa dan pemeliharaan jaringan menjadi jauh lebih mudah dibanding metode statis.

**Kendala**<br>
Untuk menyambungkan dari router antar gedung memiliki step yang harus di taati tanpa terlewat jika terlewat maka akan terjadi error dalam ping antar gedung.

**Kesimpulan**<br>
Pada minggu ini dapat disimpulkan bahwa setiap router dapat terhubung dengan vlan yang berada di switch, dengan ospf routing dinamis dapat ditentukan jalan terbaik nya serta wan berfungsi sebagai penentu lokasi geografis.