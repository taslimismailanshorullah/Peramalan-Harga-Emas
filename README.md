# Analisis Peramalan Harga Emas dengan Pendekatan ARIMA-GARCH di Indonesia

Repositori ini memuat analisis deret waktu (*time series forecasting*) untuk memprediksi harga emas di Indonesia menggunakan pendekatan pemodelan *hybrid*[cite: 3]. 

## Latar Belakang & Objektif
Harga emas rentan terhadap fluktuasi dan volatilitas tinggi yang sulit dijelaskan menggunakan model linier tradisional[cite: 3]. Proyek ini bertujuan untuk membangun model peramalan *hybrid* menggunakan model ARIMA untuk menangkap pola linier data dan model GARCH untuk menangkap dinamika volatilitas secara simultan[cite: 3].

## 🛠️ Data & Pra-pemrosesan
- **Sumber Data:** Data historis nilai tukar mata uang (harga emas) selama tiga tahun terakhir (838 entri) yang diperoleh dari situs investing.com[cite: 3].
- **Pra-pemrosesan (Data Preprocessing):** 
  - Penyesuaian tipe data dan penanganan nilai kosong[cite: 3].
  - *Upsampling* deret waktu dari mingguan (*weekly*) ke harian (*daily*) untuk memastikan interval waktu yang konsisten[cite: 3].
  - Imputasi *missing values* menggunakan kombinasi *rolling mean* (7 hari dan 30 hari), interpolasi linear, dan *shifting*[cite: 3].
  - Transformasi logaritma natural untuk menstabilkan varians dan menghindari nilai kovarians yang mendekati singular[cite: 3].

## Metodologi Pemodelan
- **Uji Stasioneritas:** Augmented Dickey-Fuller (ADF) dan KPSS Test[cite: 3].
- **Pemodelan Mean:** Identifikasi orde menggunakan plot ACF/PACF dan iterasi penaksiran parameter untuk mendapatkan model ARIMA terbaik[cite: 3].
- **Uji Volatilitas:** Uji Lagrange Multiplier (ARCH-LM Test) untuk mendeteksi *volatility clustering* (efek ARCH) pada residual model ARIMA[cite: 3].
- **Pemodelan Varians:** Spesifikasi dan penyesuaian model GARCH untuk mengakomodasi heteroskedastisitas bersyarat[cite: 3].
- **Uji Diagnostik:** Uji Ljung-Box untuk memastikan residual akhir bersifat *white noise*[cite: 3].

## Temuan Utama
1. **Pemodelan Mean (ARIMA):** Berdasarkan uji iteratif dan metrik evaluasi yang mementingkan aspek parsimoni, model ARIMA(0,1,3) terpilih sebagai model terbaik untuk menangkap struktur dependensi nilai tengah (mean)[cite: 3].
2. **Eksistensi Volatilitas:** Uji ARCH-LM menolak hipotesis nol secara signifikan (p-value < 0.05), membuktikan adanya efek *volatility clustering* yang membutuhkan penanganan lebih lanjut[cite: 3].
3. **Model Hybrid Final:** Model GARCH(1,1) dengan penyesuaian *mean* (AR) terbukti efektif dalam memodelkan varians[cite: 3]. Kombinasi **ARIMA(0,1,3)-GARCH(1,1)** secara valid menangkap karakteristik data secara menyeluruh, di mana uji diagnostik Ljung-Box mengonfirmasi tidak ada lagi autokorelasi tersisa pada residual maupun *squared residual*[cite: 3].

## Struktur Repositori
- `notebooks/` : *Source code* lengkap (Python/Jupyter Notebook) yang mendemonstrasikan proses transformasi, fitting model ARIMA-GARCH, dan evaluasi pengujian statistik.
- `ANALISIS PERAMALAN HARGA EMAS DENGAN PENDEKATAN ARIMA-GARCH DI INDONESIA.pdf` : Dokumen laporan hasil penelitian secara komprehensif[cite: 3].
