# Proyek Akhir: Menyelesaikan Permasalahan Perusahaan Edutech

## Business Understanding

Jaya Jaya Maju adalah perusahaan multinasional yang telah beroperasi sejak tahun 2000 dan memiliki lebih dari 1.000 karyawan yang tersebar di seluruh Indonesia. Seiring berkembangnya skala bisnis, tantangan dalam pengelolaan sumber daya manusia menjadi semakin kompleks. Salah satu permasalahan utama yang dihadapi adalah tingginya attrition rate (tingkat keluar-masuk karyawan), yang telah melampaui angka 10%.

Attrition rate yang tinggi mengindikasikan adanya masalah dalam kepuasan kerja, manajemen karier, kompensasi, atau kondisi kerja secara umum. Hal ini dapat menyebabkan kerugian besar bagi perusahaan, baik dari sisi finansial (biaya rekrutmen dan pelatihan ulang), produktivitas, maupun stabilitas organisasi.

Untuk mendukung pengambilan keputusan yang tepat, departemen HR membutuhkan dashboard berbasis data yang dapat membantu memantau dan menganalisis faktor-faktor yang mempengaruhi tingginya attrition rate. Visualisasi yang tepat akan memudahkan HR dalam memahami kondisi terkini dan mengambil tindakan preventif atau korektif secara lebih cepat dan akurat. Selain itu, dibutuhkan juga model machine learning untuk memprediksi karyawan - karyawan yang mungkin akan mengundurkan diri / mengalami attrition.

### Permasalahan Bisnis

Berikut adalah permasalahan bisnis utama yang ingin diselesaikan:
- Tingginya angka attrition rate yang melebihi 10%.
- Tidak adanya alat bantu visual atau analitik yang memadai untuk memantau faktor-faktor penyebab attrition.
- Kurangnya pemahaman tentang bagaimana atribut-atribut seperti usia, pendapatan, jenis pekerjaan, kepuasan kerja, lembur, dan jarak tempat tinggal mempengaruhi keputusan karyawan untuk keluar.
- Sulitnya mendeteksi lebih awal pola atau tren yang menunjukkan risiko tinggi karyawan akan keluar dari perusahaan.
- Tidak adanya sistem berbasis data untuk memprediksi retensi karyawan.

### Cakupan Proyek

1. Pembuatan business dashboard interaktif menggunakan Metabase, yang menampilkan:
   - Statistik dasar attrition rate secara umum (departemen, role, level pekerjaan, dan usia)
   - Analisis faktor demografis (jenis kelamin, status pernikahan, dan jarak rumah ke kantor)
   - Analisis faktor pekerjaan (lembur, level kepuasan pekerjaan, level work life balance, level keterlibatan dalam pekerjaan serta level kepuasan lingkungan kerja)
   - Analisis kompensasi dan pengambangan karir (gaji bulanan, kenaikan gaji, total training tahun lalu, dan lama bekerja di perusahaan dalam tahun)
2. Pembuatan model machine learning untuk memprediksi karyawan yang akan mengalami retensi.

### Persiapan

Sumber data: [JayaJayaMaju Dataset - Dicoding](https://github.com/dicodingacademy/dicoding_dataset/tree/main/employee)

### 📦 Setup Environment

**Opsi 1: Menggunakan anaconda**
```
conda create --name attrition-analysis python=3.9
conda activate attrition-analysis
pip install -r requirements.txt
```
**Opsi 2: Menggunakan Shell/Terminal**
```
pip install pipenv
pipenv install
pipenv shell
pip install -r requirements.txt
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

   Gunakan akun login berikut:
   - Email: root@mail.com
   - Password: root123

5. Menghubungkan Metabase ke Supabase (PostgreSQL Cloud)
   Setelah login, pilih opsi untuk menambahkan database dan isi form koneksi berikut:

   - Database Type: PostgreSQL
   - Name: Supabase Attrition DB
   - Host: aws-0-ap-southeast-1.pooler.supabase.com
   - Port: 6543
   - Database Name: postgres
   - Username: postgres.mfklfwdpjxepgrxdhhnb
   - Password: V1NOgjcNCmz90J52

   Klik Next dan tunggu hingga koneksi berhasil.

6. Lihat Dashboard 'Employee Dashboard'.


⚙️ Setup File Model Prediksi (Random Forest)
1.  Pastikan Python 3 sudah terinstal.
2.  Instal pustaka tambahan (jika belum):
    ```bash
    pip install pandas joblib scikit-learn
    ```

3.  Letakkan file berikut di direktori kerja Anda:
   - rediction.py
   - rf_model.pkl
   - scaler.pkl
   - x_columns.pkl
   - cleaned_employees.csv
4.  Jalankan prediksi:
   ```
   python prediction.py
   ```
   Output prediksi akan muncul di terminal berupa daftar 10 karyawan teratas yang diprediksi mengalami attrition, dilengkapi kolom-kolom  `EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, dan `Gender`.

## Business Dashboard

Dashboard ini dirancang untuk menganalisis attrition (tingkat keluar masuk karyawan) dalam perusahaan, menggunakan data karyawan yang telah diklasifikasikan berdasarkan beberapa faktor penting. Komponen utama dari dashboard ini meliputi:

1. Attrition Rate secara umum: Memberikan wawasan mendalam mengenai tingkat attrition per departemen, tugas, level tugas dan umur.
<img width="1074" alt="Screenshot 2025-05-12 at 22 00 16" src="https://github.com/user-attachments/assets/03906eae-4237-4203-903b-9bd84f9272aa" />
<img width="1137" alt="Screenshot 2025-05-12 at 21 57 36" src="https://github.com/user-attachments/assets/0d9bc5ab-70dd-4ff1-aa94-cfe12010c0c3" />
<img width="1073" alt="Screenshot 2025-05-12 at 22 00 35" src="https://github.com/user-attachments/assets/30cea524-433a-49f1-99b8-c70105c625c7" />

2. Attrition Rate berdasarkan faktor demografi: Memberikan wawasan mendalam mengenai tingkat attrition berdasarkan gender, status pernikahan, dan jarak kantor ke rumah.
<img width="1238" alt="Screenshot 2025-05-12 at 12 12 46" src="https://github.com/user-attachments/assets/17394fa5-8a73-4a81-b937-f0d7be4b27cc" />

3. Attrition Rate terkait pekerjaan: Memberikan wawasan mendalam mengenai tingkat attrition berdasarkan lembur atau tidak, level kepuasan pekerjaan, level work life balance, level keterlibatan dalam pekerjaan serta level kepuasan lingkungan kerja.
<img width="1182" alt="Screenshot 2025-05-12 at 12 12 58" src="https://github.com/user-attachments/assets/9c9086bd-4341-40e2-a984-68f2c7495109" />
<img width="1057" alt="Screenshot 2025-05-12 at 22 01 06" src="https://github.com/user-attachments/assets/a5b303c1-7a54-4312-b9c4-0de19ef06fde" />

4. Attrition Rate terkait kompensasi dan pengembangan karir: Memberikan wawasan mendalam mengenai tingkat attrition berdasarkan gaji per bulan, persentase kenaikan gaji dari bulan sebelumnya, total training di tahun lalu, dan lama bekerja di perusahaan dalam tahun.
<img width="1183" alt="Screenshot 2025-05-12 at 12 13 17" src="https://github.com/user-attachments/assets/2322c139-0f05-42ce-b3fc-7a90ed829707" />

## Conclusion

Dari hasil visualisasi, terdapat beberapa poin penting yang dapat disimpulkan:

1. Departemen dengan tingkat attrition tertinggi adalah Sales (14.8%) dan Research & Development(11.13%). Sedangkan untuk tugas (JobRole) dengan attrition rate tertinggi ada di sales representative (30.12%) dan laboratory technician (18.92%). Berdasarkan level pekerjaan, level pekerjaan 1 (paling rendah) justru memiliki attrition rate terbesar yaitu 19.89%. Berdasarkan usia, attrition rate terbesar ada di usia 15-20 tahun yaitu di angka 52.94%
2. Berdasarkan faktor demografi, attrition rate paling tinggi dipengaruhi oleh status pernikahan karyawan, yaitu attrition rate untuk status single sebesar 20%, untuk married sebesar 9.21%, dan untuk divorce sebesar 7.03%
3. Faktor yang berhubungan dengan pekerjaan menunjukkan peran yang besar untuk attrition. Attrition rate untuk karyawan yang bekerja lembur sebesar 23.56% sedangkan karyawan yang tidak lembur hanya 7.69%. Selain itu, attrition rate terbesar ada di level kepuasan pekerjaan terendah, level work life balance terendah, level keterlibatan dalam pekerjaan yang rendah, serta level kepuasan lingkungan kerja terendah.
4. Faktor yang berhubungan dengan kompensasi dan pengembangan karir menunjukkan attrition rate tertinggi  ada pada gaji bulanan di angka terendah yaitu $0 - $2,500 (23.66%) dan berdasarkan jumlah training di tahun lalu menunjukkan bahwa karyawan yang tidak mendapatkan training di tahun sebelumnya memiliki attrition rate sebesar 24.07%.
5. Meskipun sebagian besar karyawan masih aktif (non-attrition), persentase attrition yang signifikan menunjukkan adanya masalah yang perlu diatasi.
6. Distribusi attrition yang tidak merata antar departemen mengindikasikan bahwa beberapa area mengalami tantangan organisasi atau beban kerja yang lebih berat.

### Rekomendasi Action Items

Berdasarkan analisis tersebut, berikut beberapa rekomendasi yang dapat diambil oleh perusahaan:

1. Lakukan exit interview terstruktur di departemen dengan attrition tinggi (Sales dan Research and Development) untuk memahami alasan spesifik karyawan keluar.
2. Tinjau ulang kebijakan kompensasi, beban kerja, dan jenjang karier di departemen yang terdampak.
3. Implementasikan program retensi karyawan seperti pelatihan pengembangan karier, mentoring, atau fleksibilitas kerja.
4. Lakukan survei keterlibatan karyawan secara berkala untuk mendeteksi gejala ketidakpuasan sebelum berujung pada pengunduran diri.
5. Pantau metrik ini secara berkala di dashboard Metabase untuk melihat dampak dari kebijakan yang diimplementasikan dan mendeteksi tren baru lebih awal.
