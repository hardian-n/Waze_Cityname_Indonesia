<p align="center">
  <img src="waze_indonesia.png" alt="Waze Indonesia" width="120">
</p>

<h1 align="center">Waze Cityname Indonesia</h1>

<p align="center">
  Userscript overlay batas dan nama wilayah Indonesia untuk <strong>Waze Map Editor</strong>.
</p>

<p align="center">
  <a href="https://greasyfork.org/id/scripts/7628-wme-kecamatan-overlay">
    <img src="https://img.shields.io/badge/Install-Userscript-00bcd4?style=for-the-badge" alt="Install Userscript">
  </a>
  <img src="https://img.shields.io/badge/license-GPLv3-blue?style=for-the-badge" alt="GPLv3 License">
  <img src="https://img.shields.io/badge/Waze-Map%20Editor-33ccff?style=for-the-badge" alt="Waze Map Editor">
</p>

## Tentang proyek

**Waze Cityname Indonesia** menambahkan layer wilayah Indonesia ke dalam Waze Map Editor (WME). Layer mengambil data polygon berformat KML dari repository ini, kemudian menampilkan batas dan nama wilayah sesuai lokasi peta yang sedang dibuka.

Project ini ditujukan untuk membantu editor Waze Indonesia mengenali area kerja dan batas wilayah secara lebih mudah saat melakukan penyuntingan peta.

> Project komunitas ini bukan produk resmi dan tidak berafiliasi secara resmi dengan Waze atau Google.

## Fitur

- Menampilkan polygon batas wilayah pada Waze Map Editor.
- Menampilkan nama wilayah pada peta.
- Memuat data KML berdasarkan provinsi yang sedang dibuka.
- Menyorot wilayah yang sedang berada di tengah/fokus peta.
- Pilihan untuk menampilkan atau menyembunyikan isi polygon.
- Pilihan untuk menampilkan atau menyembunyikan label wilayah.
- Pembaruan database KML secara manual maupun otomatis.
- Penyimpanan data KML di IndexedDB browser agar tidak perlu selalu mengunduh ulang data yang sama.
- Mendukung halaman WME reguler dan WME beta.

## Persyaratan

Sebelum memasang script, siapkan:

1. Browser berbasis Chromium atau Firefox.
2. Extension pengelola userscript, seperti **Tampermonkey**.
3. Akun yang dapat mengakses [Waze Map Editor](https://www.waze.com/editor).

## Instalasi

1. Pasang Tampermonkey pada browser.
2. Klik tombol **Install Userscript** di bagian atas README ini, atau buka file berikut:

   [WME Kecamatan Overlay](https://greasyfork.org/id/scripts/7628-wme-kecamatan-overlay)

3. Pengelola userscript akan menampilkan halaman instalasi.
4. Klik **Install**.
5. Buka atau muat ulang Waze Map Editor.

Script menggunakan beberapa dependensi userscript, termasuk **WazeWrap** dan database pendukung WME Cities Overlay.

## Cara penggunaan

Setelah script aktif:

1. Buka Waze Map Editor.
2. Pindahkan peta ke wilayah Indonesia yang ingin diedit.
3. Aktifkan layer **Cities Overlay** dari menu layer WME apabila belum terlihat.
4. Buka tab **Cities** pada panel samping untuk mengatur tampilan overlay.

Pengaturan yang tersedia:

| Pengaturan | Fungsi |
|---|---|
| **Fill polygons** | Menampilkan atau menyembunyikan warna isi polygon. |
| **Show city labels** | Menampilkan atau menyembunyikan nama wilayah. |
| **Highlight focused city** | Menyorot wilayah yang sedang menjadi fokus peta. |
| **Update database** | Memeriksa dan mengambil pembaruan file KML. |
| **Automatically update database** | Memeriksa pembaruan database secara otomatis saat WME dibuka. |

## Struktur repository

```text
Waze_Cityname_Indonesia/
├── DESA/ID/                         # Data terkait wilayah desa Indonesia
├── KMLs/ID/                         # File KML wilayah per provinsi
├── css/                             # File pendukung tampilan
├── Sumut_Simalungun.kml             # Data KML khusus/contoh wilayah
├── WMEIndonesiaCitynameOverlay.js   # Userscript utama
├── waze_indonesia.png               # Logo project
└── README.md
```

File wilayah pada folder `KMLs/ID` menggunakan pola penamaan:

```text
<KODE_PROVINSI>_Cities.kml
```

Contoh:

```text
JATENG_Cities.kml
DIY_Cities.kml
JABAR_Cities.kml
```

Script menentukan provinsi aktif dari WME, kemudian mengambil file KML yang sesuai dari folder tersebut.

## Format data KML

Data polygon menggunakan format KML dengan koordinat geografis **EPSG:4326**. Setiap wilayah sebaiknya berada dalam elemen `Placemark` dan memiliki nama wilayah pada elemen `name`.

Contoh sederhana:

```xml
<?xml version="1.0" encoding="utf-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
  <Document>
    <Folder>
      <name>DIY</name>
      <Placemark>
        <name>Banguntapan</name>
        <Polygon>
          <outerBoundaryIs>
            <LinearRing>
              <coordinates>
                110.0000,-7.0000
                110.1000,-7.0000
                110.1000,-7.1000
                110.0000,-7.0000
              </coordinates>
            </LinearRing>
          </outerBoundaryIs>
        </Polygon>
      </Placemark>
    </Folder>
  </Document>
</kml>
```

## Menambahkan atau memperbarui data wilayah

1. Siapkan polygon wilayah dalam format KML.
2. Pastikan koordinat menggunakan longitude dan latitude atau EPSG:4326.
3. Pastikan setiap `Placemark` memiliki nama wilayah yang benar.
4. Simpan file ke folder `KMLs/ID` menggunakan pola nama yang sesuai.
5. Uji file pada Waze Map Editor.
6. Buat commit atau Pull Request dengan penjelasan sumber dan perubahan data.

Saat ukuran file KML di GitHub berubah, fitur pembaruan database pada script akan mendeteksi perubahan tersebut dan mengambil versi terbaru.

## Pengembangan

File utama project adalah:

```text
WMEIndonesiaCitynameOverlay.js
```

Metadata userscript saat ini mendefinisikan:

- Nama script: `WME Kecamatan Overlay`
- Namespace: `Komunitas Waze Indonesia`
- Versi: `2023.08.30.01`
- Lisensi: `GNU GPLv3`

Karena tampilan dan API internal Waze Map Editor dapat berubah, script mungkin perlu disesuaikan ketika WME melakukan pembaruan besar.

## Kontribusi

Kontribusi sangat terbuka, terutama untuk:

- Koreksi batas wilayah.
- Penambahan data wilayah yang belum tersedia.
- Koreksi nama wilayah.
- Optimasi ukuran file KML.
- Perbaikan kompatibilitas dengan Waze Map Editor terbaru.
- Perbaikan bug pada userscript.

Silakan buat **Issue** untuk melaporkan masalah atau kirim **Pull Request** untuk mengusulkan perubahan.

## Lisensi

Userscript ini menggunakan lisensi **GNU General Public License v3.0 (GPLv3)** sebagaimana tercantum pada metadata script.

## Author

Dikembangkan oleh [Hardian Nurhadi / Waze ID: hardian_n](https://www.waze.com/user/editor/hardian_n) untuk komunitas editor Waze Indonesia.
