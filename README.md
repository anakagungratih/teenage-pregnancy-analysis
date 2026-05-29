# teenage-pregnancy-analysis
Eksplorasi data AFR global (World Bank) untuk mendukung program Generasi Berencana (GenRe) BKKBN — visualisasi tren, perbandingan ASEAN, dan storytelling berbasis data
# DATASET 
Dataset yang digunakanDataset berasal dari World Bank Human Capital Project (WB_HCP), diakses secara publik melalui portal data resmi World Bank. Dataset ini berisi indikator Adolescent Fertility Rate (AFR) — yaitu angka kelahiran per 1.000 perempuan usia 15–19 tahun — yang mencakup 229 negara/wilayah di seluruh dunia dari tahun 1960 hingga 2023, dengan total 14.656 baris observasi.
# Variabel yang digunakan
Dari 39 kolom yang tersedia di dataset asli, hanya 3 variabel yang relevan untuk analisis:
country — nama negara atau wilayah, bersumber dari kolom REF_AREA_LABEL. Tipe data karakter.
year — tahun pencatatan data, bersumber dari kolom TIME_PERIOD. Rentang 1960–2023. Tipe data integer.
afr — nilai utama analisis, bersumber dari kolom OBS_VALUE. Satuan: jumlah kelahiran per 1.000 perempuan usia 15–19 tahun. Tipe data numerik. Semakin kecil nilainya, semakin baik kondisi kesehatan reproduksi remaja di negara tersebut.
Sisa 36 kolom lainnya merupakan metadata teknis World Bank yang nilainya seragam di seluruh baris (seperti kode frekuensi, satuan ukuran, status observasi) sehingga tidak diikutsertakan dalam analisis.
# Bagian-bagian yang dianalasis
1. Tahap 1 — mengecek dataset .
    a) Struktur data berhasil dibentuk
   Dari glimpse(data_clean) terlihat:
    Dari glimpse(data_clean) terlihat:
    Rows: 14.656, Columns: 3
    country bertipe chr — sudah benar sebagai teks
    year bertipe dbl — terbaca sebagai numerik, nanti perlu dikonversi ke integer dengan as.integer(year) agar lebih rapi
    afr bertipe dbl — sudah benar sebagai numerik
   b) Tidak ada missing values
   Hasil summarise(across(everything(), ~sum(is.na(.)))):
country   year   afr
      0      0     0
Ketiga variabel bebas dari nilai kosong. Ini berarti data siap dianalisis tanpa perlu proses imputasi atau pembersihan tambahan. Untuk konteks presentasi, ini poin kredibilitas — datamu murni dari sumber tanpa rekayasa.
    c) Data Indonesia lengkap
   nrow(idn) menghasilkan 64, persis sesuai jumlah tahun dari 1960 sampai 2023. Tidak ada satu tahun pun yang hilang untuk Indonesia.
    d) Statistik deskriptif AFR Indonesia
   

Artinya proses select untuk memilih 3 kolom dari 39 kolom berjalan sempurna.
Artinya proses select untuk memilih 3 kolom dari 39 kolom berjalan sempurna.
3. Tahap 2 — Analisis deskriptif Indonesia.
   Dilakukan eksplorasi statistik dasar menggunakan summary() untuk melihat nilai minimum, maksimum, median, dan rata-rata AFR Indonesia sepanjang waktu. Ditemukan bahwa AFR Indonesia bergerak dari titik tertinggi 151,70 (sekitar 1965) turun ke titik terendah 26,42 (2023), dengan penurunan total sekitar 82%.
4. Tahap 3 — Analisis tren per era kebijakan.
  Data Indonesia dibagi ke dalam 5 era berdasarkan kebijakan nasional: Pra-KB (1960–1965), BKKBN awal (1966–1984), KB intensif (1985–1999), Transisi (2000–2011),  dan Era GenRe (2012–2023). Setiap era dihitung AFR awal, AFR akhir, dan persentase penurunannya.
5. Tahap 4 — Perbandingan regional ASEAN (tahap berikutnya).
    Indonesia akan dibandingkan dengan negara-negara Asia Tenggara untuk melihat posisi relatif Indonesia di kawasan.
6. 
