# Cara Memprediksi dan Menampilkan 10 Karyawan Teratas yang Berpotensi Attrition (Menggunakan Model Random Forest)

Berkas ini menjelaskan cara menggunakan skrip Python `prediction.py` untuk memprediksi 10 karyawan yang paling mungkin mengalami attrition dari berkas `cleaned_employees.csv` (di mana nilai attrition saat ini adalah 0 atau karyawan aktif) dan menampilkan kolom `EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, dan `Gender` dari karyawan-karyawan tersebut langsung ke konsol. Skrip ini menggunakan model Random Forest yang telah dilatih sebelumnya, scaler, dan daftar nama kolom fitur yang telah disimpan menggunakan `joblib`.

## Prasyarat

1.  **Python 3 terinstal** di sistem Anda.
2.  **Pustaka `pandas` dan `joblib` terinstal.** Anda dapat menginstalnya menggunakan pip:
    ```bash
    pip install pandas joblib scikit-learn
    ```

3.  **Berkas Model (`rf_model.pkl`) Tersedia:** Letakkan berkas model Random Forest yang telah disimpan di direktori yang sama dengan skrip.
4.  **Berkas Scaler (`scaler.pkl`) Tersedia:** Letakkan berkas scaler yang telah disimpan di direktori yang sama dengan skrip. Pastikan nama berkasnya sesuai.
5.  **Berkas Nama Kolom Fitur (`x_columns.pkl`) Tersedia:** Letakkan berkas yang berisi daftar nama kolom fitur di direktori yang sama dengan skrip. Pastikan nama berkasnya sesuai.
6.  **Berkas Data Karyawan (`cleaned_employees.csv`) Tersedia:** Pastikan berkas CSV ini berada di direktori yang sama dengan skrip. Berkas ini harus memiliki kolom 'Attrition' dan kolom-kolom yang ingin ditampilkan (`EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, `Gender`).

## Langkah-langkah Penggunaan

1.  **Pastikan Semua Berkas Tersedia:** Letakkan skrip `prediction.py`, berkas model Random Forest (`rf_model.pkl`), berkas scaler (`scaler.pkl`), berkas nama kolom fitur (`x_columns.pkl`), dan berkas data karyawan (`cleaned_employees.csv`) di direktori yang sama. **Pastikan Anda mengganti nama berkas model Anda sesuai dengan apa yang sebenarnya Anda simpan.**

2.  **Jalankan Skrip Prediksi:** Buka terminal atau command prompt, navigasi ke direktori tempat Anda menyimpan berkas-berkas tersebut, dan jalankan perintah berikut:
    ```bash
    python prediction.py
    ```

3.  **Lihat Hasil Prediksi di Konsol:** Setelah skrip selesai dijalankan, output yang berisi kolom `EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, dan `Gender` dari 10 karyawan teratas yang diprediksi akan attrition akan ditampilkan langsung di konsol. Karyawan akan diurutkan berdasarkan hasil prediksi kelas attrition (nilai 1).

## Penjelasan Skrip

Skrip `prediction.py` melakukan langkah-langkah berikut:

1.  **Memuat Model, Scaler, dan Nama Kolom:** Memuat berkas-berkas yang telah disimpan sebelumnya menggunakan `joblib`.
2.  **Memuat Data Karyawan:** Memuat data dari `cleaned_employees.csv`.
3.  **Memfilter Karyawan dengan Attrition = 0:** Hanya karyawan yang saat ini tidak attrition yang akan diprediksi.
4.  **Memastikan Urutan Kolom:** Memilih kolom dari data karyawan sesuai dengan urutan fitur yang digunakan saat model dilatih.
5.  **Melakukan Scaling:** Menerapkan scaling yang sama seperti saat pelatihan model menggunakan scaler yang telah disimpan.
6.  **Memprediksi Attrition:** Menggunakan model Random Forest untuk memprediksi kelas attrition (0 atau 1).
7.  **Menampilkan 10 Prediksi Teratas:** Mengambil 10 karyawan dengan prediksi kelas attrition tertinggi (nilai 1) dan menampilkan kolom `EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, dan `Gender` mereka di konsol.

Pastikan nama berkas model, scaler, dan daftar kolom sesuai dengan apa yang Anda gunakan saat menyimpan objek-objek tersebut. Juga, pastikan nama kolom yang ingin ditampilkan (`EmployeeId`, `Department`, `JobRole`, `OverTime`, `MaritalStatus`, `Gender`) sesuai dengan nama kolom di berkas `cleaned_employees.csv` Anda. Hasil akan diurutkan berdasarkan prediksi kelas attrition (karyawan dengan prediksi '1' akan berada di bagian atas).
