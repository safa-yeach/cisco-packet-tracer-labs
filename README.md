# Cisco Packet Tracer Labs: Routing & Switching

Repositori ini berisi kumpulan dokumentasi praktik dan simulasi jaringan komputer menggunakan Cisco Packet Tracer. Semua lab di sini dibangun untuk melatih cara kerja jaringan di balik layar—mulai dari menghubungkan jaringan lokal yang berbeda segmen, membagi jalur menggunakan VLAN, hingga memastikan koneksi tetap aman lewat jalur cadangan (*failover*).

---

## Daftar Topologi & Pembahasan Lab

### 1. Inter-VLAN & Multilayer Switching
![Inter-VLAN](<Inter-VLAN.jpeg>)

* **Gambaran Sistem:** Terdiri dari 2 Router (`Router0`, `Router1`), 2 Multilayer Switch (`3560-24PS`), dan 4 PC yang dibagi menjadi dua segmen jaringan berbeda (`192.168.1.0` dan `192.168.2.0`).
* **Cara Kerja & Tujuan:** Di lab ini, switch tidak cuma dipakai buat colok-colok kabel saja (Layer 2), tapi difungsikan juga untuk mengatur lalu lintas IP (Layer 3) menggunakan *Switch Virtual Interface* (SVI). Tujuannya agar komunikasi antar-segmen di jaringan lokal bisa berjalan cepat langsung di level switch sebelum diteruskan ke router untuk keluar jaringan.

---

### 2. Static Routing Dasar (Point-to-Point)
![Static Route](<Static route.jpeg>)

* **Gambaran Sistem:** Menghubungkan 2 jaringan lokal (LAN) terpisah melalui 2 buah Router yang disambungkan langsung menggunakan kabel *cross-over*.
* **Cara Kerja & Tujuan:** Secara bawaan, router hanya kenal dengan jaringan yang menempel langsung di port-nya. Di sini saya melatih konfigurasi **Static Route** dan **Default Route** untuk memberitahu router ke mana harus melempar paket data jika tujuannya berada di jaringan seberang. Ini adalah fondasi paling wajib sebelum masuk ke arsitektur jaringan yang lebih rumit.

---

### 3. Routing Dinamis & Jalur Cadangan (WAN Redundancy)
![Routing Dinamis](<Routing dinamis.jpeg>)

* **Gambaran Sistem:** Tiga buah Router dihubungkan membentuk segitiga (*full-mesh*) memakai antarmuka Serial DCE/DTE, lengkap dengan 3 jaringan lokal di masing-masing sisi.
* **Cara Kerja & Tujuan:** Jika menggunakan *static route* pada topologi segitiga seperti ini, admin bakal kewalahan mengatur jalur satu per satu. Karena itu, di lab ini diterapkan protokol routing dinamis (seperti OSPF / RIPv2) agar router bisa menghitung jalur tercepat secara otomatis. Selain itu, topologi ini dipakai untuk menguji **failover**—memastikan kalau satu kabel terputus, koneksi langsung pindah ke jalur memutar tanpa membuat jaringan mati total.

---

### 4. Router-on-a-Stick (Single-Switch Inter-VLAN)
![Router-on-a-Stick](<Router-on-a-Stick.jpeg>)

* **Gambaran Sistem:** Menggunakan 1 Router dan 1 Multilayer Switch untuk memisahkan 4 PC ke dalam dua kelompok logis yang berbeda, yaitu **VLAN 10** dan **VLAN 20**.
* **Cara Kerja & Tujuan:** Dalam satu perangkat switch fisik yang sama, lalu lintas data dipisah agar lebih aman dan tidak saling mengganggu (*broadcast domain* terpisah). Karena beda VLAN artinya beda jaringan, saya mengonfigurasi metode **Router-on-a-Stick** dengan membuat *sub-interface* pada router supaya perangkat di VLAN 10 tetap bisa bertukar data dengan VLAN 20 secara terkontrol.

---

### 5. VLAN Trunking Antar-Switch (IEEE 802.1Q)
![VLAN Trunking](<VLAN Trunking.jpeg>)

* **Gambaran Sistem:** Pengembangan dari lab sebelumnya dengan menggunakan 2 Multilayer Switch dan 1 Router, di mana anggota **VLAN 10** dan **VLAN 20** tersebar di kedua switch tersebut.
* **Cara Kerja & Tujuan:** Di lapangan nyata, anggota satu divisi atau satu VLAN sering kali berada di ruangan atau lantai yang berbeda (switch yang berbeda). Agar PC di VLAN 10 pada Switch bawah bisa terhubung dengan sesama VLAN 10 di Switch atas tanpa harus menarik banyak kabel, jalur penghubung antar-switch dikonfigurasi menggunakan mode **Trunk (802.1Q)**. Jalur ini bertugas membawa banyak trafik VLAN sekaligus dalam satu kabel fisik.

---

## Konsep & Protokol yang Diterapkan
* **Switching:** VLAN Segmentation, Access Port, Trunking (802.1Q), Multilayer Switching (SVI).
* **Routing:** Static Routing, Default Route, Router-on-a-Stick, Dynamic Routing (RIPv2 / OSPF).
* **Pengalamatan & Layanan:** IPv4 Subnetting, DHCP Server / Pool Configuration.
