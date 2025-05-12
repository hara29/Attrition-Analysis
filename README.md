# Proyek Akhir: Menyelesaikan Permasalahan Perusahaan Edutech

## Business Understanding

Jaya Jaya Maju adalah perusahaan multinasional yang telah beroperasi sejak tahun 2000 dan memiliki lebih dari 1.000 karyawan yang tersebar di seluruh Indonesia. Seiring berkembangnya skala bisnis, tantangan dalam pengelolaan sumber daya manusia menjadi semakin kompleks. Salah satu permasalahan utama yang dihadapi adalah tingginya attrition rate (tingkat keluar-masuk karyawan), yang telah melampaui angka 10%.

Attrition rate yang tinggi mengindikasikan adanya masalah dalam kepuasan kerja, manajemen karier, kompensasi, atau kondisi kerja secara umum. Hal ini dapat menyebabkan kerugian besar bagi perusahaan, baik dari sisi finansial (biaya rekrutmen dan pelatihan ulang), produktivitas, maupun stabilitas organisasi.

Untuk mendukung pengambilan keputusan yang tepat, departemen HR membutuhkan dashboard berbasis data yang dapat membantu memantau dan menganalisis faktor-faktor yang mempengaruhi tingginya attrition rate. Visualisasi yang tepat akan memudahkan HR dalam memahami kondisi terkini dan mengambil tindakan preventif atau korektif secara lebih cepat dan akurat. Selain itu, dibutuhkan juga model machine learning untuk memprediksi karyawan - karyawan yang mungkin akan mengundurkan diri / mengalami attrition.

### Permasalahan Bisnis

Berikut adalah permasalahan bisnis utama yang ingin diselesaikan:
- Tingginya angka attrition rate yang melebihi 10% setiap tahun.
- Tidak adanya alat bantu visual atau analitik yang memadai untuk memantau faktor-faktor penyebab attrition.
- Kurangnya pemahaman tentang bagaimana atribut-atribut seperti usia, pendapatan, jenis pekerjaan, kepuasan kerja, lembur, dan jarak tempat tinggal mempengaruhi keputusan karyawan untuk keluar.
- Sulitnya mendeteksi lebih awal pola atau tren yang menunjukkan risiko tinggi karyawan akan keluar dari perusahaan.
- Tidak adanya sistem berbasis data untuk memprediksi retensi karyawan.

### Cakupan Proyek

Pembuatan business dashboard interaktif menggunakan Metabase, yang menampilkan:
- Statistik dasar attrition rate secara keseluruhan dan per divisi
- Analisis faktor demografis (usia, jenis kelamin, status pernikahan)
- Analisis faktor pekerjaan (jabatan, departemen, jam kerja, lembur)
- Analisis kompensasi (gaji bulanan, kenaikan gaji, opsi saham)
- Analisis kepuasan kerja dan work-life balance
Pembuatan model machine learning untuk memprediksi karyawan yang akan mengalami retensi.

### Persiapan

Sumber data: [JayaJayaMaju Dataset - Dicoding](https://github.com/dicodingacademy/dicoding_dataset/tree/main/employee)

Untuk membangun dashboard analisis attrition menggunakan Metabase, terdapat dua bagian utama yang perlu dipersiapkan:

1. **Lingkungan Python** untuk eksplorasi dan pembersihan data (jika dibutuhkan).
2. **Environment Metabase** untuk membuat dashboard interaktif.

---

### 📦 Instalasi Library Python

Jika Anda ingin mengolah data terlebih dahulu sebelum digunakan di Metabase, pastikan Anda telah menginstal beberapa library Python berikut:
```
pip install pandas sqlalchemy
```

### 🐳 Menjalankan Metabase Menggunakan Docker
Untuk memudahkan proses setup, Metabase dapat dijalankan menggunakan Docker. Ikuti langkah-langkah berikut:

1. Install Docker
   Unduh dan instal Docker sesuai sistem operasi Anda dari: https://www.docker.com/products/docker-desktop
2. Unduh Image Metabase
   Gunakan perintah berikut untuk mengunduh image Metabase versi 0.46.4:
   ```
   docker pull metabase/metabase:v0.46.4
   ```
3. Jalankan Container Metabase
   Gunakan perintah berikut untuk menjalankan Metabase dan menyimpan file database internal di folder lokal metabase-data:
   ```
   docker run -d -p 3000:3000 --name metabase \
   -v $PWD/metabase-data:/metabase-data \
   -e "MB_DB_FILE=/metabase-data/metabase.db" \
   metabase/metabase:v0.46.4
   ```
   Penjelasan:

   -v $PWD/metabase-data:/metabase-data: Menyimpan file konfigurasi Metabase secara lokal.

    -e "MB_DB_FILE=/metabase-data/metabase.db": Memberitahu Metabase untuk menyimpan database internal di lokasi tersebut.

4. Akses Metabase
   Buka browser dan akses Metabase pada URL berikut [](http://localhost:3000/setup)

Untuk menjalankan model prediksi Random Forest terdapat dua bagian utama yang perlu dipersiapkan:
1. Prerequisite system and library
2. Langkah - langkah penggunaan

---
### Prerequisite
1.  **Python 3 terinstal** di sistem Anda.
2.  **Pustaka `pandas` dan `joblib` terinstal.** Anda dapat menginstalnya menggunakan pip:
    ```bash
    pip install pandas joblib scikit-learn
    ```

3.  **Berkas Model (`rf_model.pkl`) Tersedia:** Letakkan berkas model Random Forest yang telah disimpan di direktori yang sama dengan skrip.
4.  **Berkas Scaler (`scaler.pkl`) Tersedia:** Letakkan berkas scaler yang telah disimpan di direktori yang sama dengan skrip. Pastikan nama berkasnya sesuai.
5.  **Berkas Nama Kolom Fitur (`x_columns.pkl`) Tersedia:** Letakkan berkas yang berisi daftar nama kolom fitur di direktori yang sama dengan skrip. Pastikan nama berkasnya sesuai.
6.  **Berkas Data Karyawan (`cleaned_employees.csv`) Tersedia:** Pastikan berkas CSV ini berada di direktori yang sama dengan skrip. Berkas ini harus memiliki kolom 'Attrition' dan kolom-kolom yang ingin ditampilkan (`EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, `Gender`).

### Langkah - langkah penggunaan
1.  **Pastikan Semua Berkas Tersedia:** Letakkan skrip `prediction.py`, berkas model Random Forest (`rf_model.pkl`), berkas scaler (`scaler.pkl`), berkas nama kolom fitur (`x_columns.pkl`), dan berkas data karyawan (`cleaned_employees.csv`) di direktori yang sama. Pastikan Anda mengganti nama berkas model Anda sesuai dengan apa yang sebenarnya Anda simpan.

2.  **Jalankan Skrip Prediksi:** Buka terminal atau command prompt, navigasi ke direktori tempat Anda menyimpan berkas-berkas tersebut, dan jalankan perintah berikut:
    ```bash
    python prediction.py
    ```

3.  **Lihat Hasil Prediksi di Konsol:** Setelah skrip selesai dijalankan, output yang berisi kolom `EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, dan `Gender` dari 10 karyawan teratas yang diprediksi akan attrition akan ditampilkan langsung di konsol. Karyawan akan diurutkan berdasarkan hasil prediksi kelas attrition (nilai 1).

## Business Dashboard

Dashboard ini dirancang untuk menganalisis attrition (tingkat keluar masuk karyawan) dalam perusahaan, menggunakan data karyawan yang telah diklasifikasikan berdasarkan beberapa faktor penting. Komponen utama dari dashboard ini meliputi:

1. Attrition Rate secara umum: Memberikan wawasan mendalam mengenai tingkat attrition per departemen, tugas, level tugas dan umur.
![3C794044-0B57-47C7-BABF-5764BBADB653_1_201_a](https://github.com/user-attachments/assets/3f15720b-0baf-4c5e-89e0-ed28de654233)

2. Attrition Rate berdasarkan faktor demografi: Memberikan wawasan mendalam mengenai tingkat attrition berdasarkan gender, status pernikahan, dan jarak kantor ke rumah.


4. Attrition Rate terkait pekerjaan: Memberikan wawasan mendalam mengenai tingkat attrition berdasarkan lembur atau tidak, level kepuasan pekerjaan, level work life balance, level keterlibatan dalam pekerjaan serta level kepuasan lingkungan kerja.

5. Attrition Rate terkait kompensasi dan pengembangan karir: Memberikan wawasan mendalam mengenai tingkat attrition berdasarkan gaji per bulan, persentase kenaikan gaji dari bulan sebelumnya, total training di tahun lalu, dan lama bekerja di perusahaan dalam tahun.

## Conclusion

Jelaskan konklusi dari proyek yang dikerjakan.

### Rekomendasi Action Items (Optional)

Berikan beberapa rekomendasi action items yang harus dilakukan perusahaan guna menyelesaikan permasalahan atau mencapai target mereka.

- action item 1
- action item 2
