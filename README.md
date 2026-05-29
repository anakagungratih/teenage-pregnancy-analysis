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
# 1. Tahap 1 — mengecek dataset .
a) Struktur data berhasil dibentuk
Dari glimpse(data_clean) terlihat:
Dari glimpse(data_clean) terlihat:
Rows: 14.656, Columns: 3
country bertipe chr — sudah benar sebagai teks
year bertipe dbl — terbaca sebagai numerik, nanti perlu dikonversi ke integer dengan as.integer(year) agar lebih rapi
afr bertipe dbl — sudah benar sebagai numerik
# b) Tidak ada missing values
Hasil summarise(across(everything(), ~sum(is.na(.)))):
country   year   afr
      0      0     0
Ketiga variabel bebas dari nilai kosong. Ini berarti data siap dianalisis tanpa perlu proses imputasi atau pembersihan tambahan. Untuk konteks presentasi, ini poin kredibilitas — datamu murni dari sumber tanpa rekayasa.
# c) Data Indonesia lengkap
   nrow(idn) menghasilkan 64, persis sesuai jumlah tahun dari 1960 sampai 2023. Tidak ada satu tahun pun yang hilang untuk Indonesia.
# d) Statistik deskriptif AFR Indonesia

#  - MEAN MEDIAN DAN MAX ANGKA KELAHIRAN DARI REMAJA
  Data tidak berbohong dalam 64 tahun, Indonesia berhasil memangkas angka kelahiran remaja dari 152 menjadi 26 per 1.000 remaja perempuan, penurunan sebesar 82%, dan ini bukan kebetulan melainkan hasil nyata dari program berencana yang konsisten."
  
Min: 26.42   1st Qu: 47.32   Median: 70.37
Mean: 82.39  3rd Qu: 121.14  Max: 151.70

Rentang data sangat lebar — perjalanan 64 tahun yang dramatis
Selisih antara nilai minimum (26,42) dan maksimum (151,70) adalah 125,28 poin. Ini bukan sekadar angka — ini mencerminkan transformasi besar kondisi kesehatan reproduksi remaja Indonesia dari era pra-KB hingga era GenRe saat ini.

Minimum 26,42 — pencapaian terbaik Indonesia
Artinya di tahun 2023, hanya sekitar 26 dari 1.000 perempuan remaja usia 15–19 tahun yang melahirkan dalam setahun. Ini angka terendah sepanjang sejarah pencatatan dan bukti nyata bahwa program berencana di Indonesia berhasil.

Maximum 151,70 — kondisi sebelum ada program KB
Di sekitar tahun 1965, hampir 152 dari 1.000 remaja perempuan melahirkan dalam setahun. Hampir 1 dari 7 remaja perempuan. Angka ini menggambarkan betapa rentannya remaja Indonesia sebelum ada intervensi kebijakan yang sistematis.

Median (70,37) lebih kecil dari Mean (82,39) — distribusi menceng kanan
Ini temuan statistik yang penting. Karena median lebih kecil dari mean, artinya lebih dari separuh tahun pengamatan sudah berada di AFR di bawah 70 — sebagian besar periode Indonesia sudah relatif baik. Tapi nilai-nilai tinggi di era 1960–1970-an masih menarik rata-rata ke atas hingga 82,39.
Dalam bahasa sederhana untuk presentasi: "Indonesia sudah lebih lama berada di kondisi baik daripada kondisi buruk."

Kuartil — kesenjangan antar era sangat besar
1st Quartile 47,32 artinya 25% data terbaik berada di bawah angka ini — ini era 2000-an hingga sekarang. Sedangkan 3rd Quartile 121,14 artinya 75% data berada di bawah 121 — yang berarti hanya sekitar 25% data (era 1960-an awal) yang pernah mencapai AFR setinggi itu. Jarak antara kuartil 1 dan kuartil 3 sebesar 73,82 poin menunjukkan betapa besarnya variasi kondisi lintas dekade.
   

Artinya proses select untuk memilih 3 kolom dari 39 kolom berjalan sempurna.
Artinya proses select untuk memilih 3 kolom dari 39 kolom berjalan sempurna.
3. Tahap 2 — Analisis deskriptif Indonesia.
   Dilakukan eksplorasi statistik dasar menggunakan summary() untuk melihat nilai minimum, maksimum, median, dan rata-rata AFR Indonesia sepanjang waktu. Ditemukan bahwa AFR Indonesia bergerak dari titik tertinggi 151,70 (sekitar 1965) turun ke titik terendah 26,42 (2023), dengan penurunan total sekitar 82%.
4. Tahap 3 — Analisis tren per era kebijakan.
  Data Indonesia dibagi ke dalam 5 era berdasarkan kebijakan nasional: Pra-KB (1960–1965), BKKBN awal (1966–1984), KB intensif (1985–1999), Transisi (2000–2011),  dan Era GenRe (2012–2023). Setiap era dihitung AFR awal, AFR akhir, dan persentase penurunannya.
5. Tahap 4 — Perbandingan regional ASEAN (tahap berikutnya).
    Indonesia akan dibandingkan dengan negara-negara Asia Tenggara untuk melihat posisi relatif Indonesia di kawasan.
6. 
