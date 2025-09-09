# Customer Churn Analysis
by Rahadian Yaumal Etantyo

Project ini dibuat sebagai **Final Project** untuk memprediksi kemungkinan pelanggan melakukan churn dengan menggunakan model machine learning. Dataset yang digunakan berisi informasi pelanggan seperti tenure, status complain, jarak pengiriman, dan variabel lainnya.

## **Konteks**
<p align="justify">
Sebuah Perusahaan E-Commerce tidak mengetahui pelanggan mana yang akan churn atau tidak churn dengan platform mereka untuk berbelanja. Churn berarti pelanggan sudah menguninstall atau sudah tidak memakai aplikasinya lagi. Perusahaan yang tidak mengetahui mana pelanggan churn dan mana yang tidak akan menyebabkan perusahaan merugi karena biaya iklan yang membengkak karena tidak mengetahui mana pelanggan yang loyal dan mana yang tidak loyal. Upaya pemasaran yang tidak tepat sasaran ini tidak hanya meningkatkan biaya operasional, tetapi juga mengurangi potensi pendapatan berulang dari pelanggan yang sebenarnya dapat dipertahankan. Dengan memanfaatkan analisis machine learning untuk menghasilkan prediksi churn yang akurat, perusahaan dapat mengidentifikasi pelanggan yang berisiko tinggi untuk churn dan mengarahkan kampanye iklan secara spesifik hanya kepada mereka. Pendekatan ini memungkinkan alokasi anggaran pemasaran yang lebih efisien, mengurangi pemborosan biaya iklan, dan meningkatkan efektivitas strategi retensi untuk mempertahankan pelanggan serta mendukung keberlanjutan bisnis

**Target :**
- 0 : Tetap berlangganan (Loyal) atau tidak churn
- 1 : Tidak berlangganan (Tidak Loyal) atau churn


</p>

## **Problem Statement**

<p align="justify">
Perusahaan belum memiliki kemampuan untuk mengidentifikasi pelanggan yang berpotensi churn dan yang tidak. Kondisi ini menyebabkan strategi pemasaran dan retensi kurang efektif. Diasumsikan bahwa perilaku churn dapat diprediksi dengan menganalisis faktor-faktor tertentu, seperti waktu terakhir pelanggan mengakses platform, Complain,SatisfactionScore, dan lama pelanggan bergabung dengan platform(tenure). Dengan membangun model machine learning berbasis data tersebut, perusahaan dapat melakukan prediksi churn secara lebih akurat, sehingga strategi retensi pelanggan dapat dijalankan dengan tepat sasaran.
</p>

## **Goals**
<p align="Justify">
Perusahaan mampu memprediksi pelanggan mana yang churn dan pelanggan mana yang tidak churn  menggunakan machine learning dan analisis data berdasarkan factor – factor lain yang dapat mempengaruhi tingkat churn pelanggan seperti waktu terakhir kali akses platform, Complain, SatisfactionScore, dan lama pelanggan bergabung dengan platform(tenure).
</p>

## **Stakeholder**

Hasil analisis data dan machine learning akan digunakan untuk tim marketing dan customer relationship management menyusun strategi pemasaran yang lebih efektif dan efisien. Selain itu hasil dari analisis data dan machine learning juga akan digunakan oleh tim finance untuk forecasting revenue dan tim product development untuk evaluasi terkait product yang mereka ciptakan.

## **Analytic Approach**

<p align="Justify">
Dari problem statement tersebut  akan dilakukan analisis data perilaku pelanggan untuk meprediksi apakah pelanggan tersebut loyal/tidak churn (0) atau tidak loyal/churn (1). Dari hasil prediksi tersebut akan dibuat model klasifikasi untuk memperoleh probabilitas pelanggan tersebut akan loyal atau tidak loyal.
</p>

## **Metric Evaluation**
| ACTUAL \ PREDICTED | Not Churn (0) | Churn (1) |
| ------------------ | ------------- | --------- |
| Not Churn (0)      | TN            | FP        |
| Churn (1)          | FN            | TP        |

Keterangan:<br>
- TN (True Negatif) = Aktualnya Not Churn dan machine learning memprediksi not churn
- FP (False Positif) = Aktualnya Not Churn dan machine learning memprediksi churn
- FN (False Negatif) = Aktualnya Churn dan machine learning memprediksi not churn
- TP (True Positif) = Aktualnya Churn dan machine learning memprediksi churn <br>

Type Eror:<br>
- Type Error 1 (FP) False Positif = Biaya marketing yang dikeluarkan membengkak dan sia sia (3 juta/orang).
- Type Error 2 (FN) False Negatif = Potensi kehilangan pendapatan (6 juta/orang)

<p align="justify"> 
Tujuan utama analisis perilaku pelanggan adalah mengidentifikasi secara akurat mana pelanggan yang berisiko churn dan mana yang tidak, sehingga perusahaan dapat mengoptimalkan strategi retensi dengan biaya yang efisien. Fokus dalam machine learning ini adalah meminimalkan nilai False Negatif, karena kegagalan mendeteksi pelanggan yang benar-benar churn akan menyebabkan hilangnya potensi pendapatan akibat kehilangan pelanggan serta biaya yang dikeluarkan untuk menarik pelanggan kembali lebih besar daripada biaya untuk mempertahankan pelanggan loyal. Dalam konteks ini, metric evaluasi utama yang digunakan adalah F2 Score. Pemakaian F2 Score dipilih karena dalam kasus prediksi churn, kesalahan false negative (pelanggan yang sebenarnya churn tetapi diprediksi tidak churn) lebih merugikan perusahaan dibanding false positive. F2 memberikan bobot lebih besar pada recall, sehingga model lebih fokus menangkap sebanyak mungkin pelanggan berisiko churn untuk meminimalkan potensi kehilangan biaya yang lebih besar baik pendapatan maupun biaya untuk menarik kembali pelanggan yang churn.
</p>


## **Rumus F2 Score**
Rumus umum Fscore: <br>
$$F_{\beta} = \frac{(1 + \beta^{2}) \cdot (Precision \cdot Recall)}{(\beta^{2} \cdot Precision) + Recall}
$$

Rumus F2 Score : <br>
$$
F_{2} = \frac{5 \cdot Precision \cdot Recall}{(4 \cdot Precision) + Recall}
$$

## **Data Understanding**

| Nama Kolom                 | Jenis Data    | Deskripsi                                                                 |
|-----------------------------|---------------|---------------------------------------------------------------------------|
| CustomerID                  | Integer| ID unik setiap pelanggan.                                                 |
| Churn                       | Integer  | Status churn pelanggan (0 = loyal / tidak churn, 1 = churn).              |
| Tenure                      | Integer       | Lama waktu (misal bulan) pelanggan sudah bergabung dengan platform.       |
| PreferredLoginDevice        | Categorical   | Perangkat utama pelanggan untuk login (misal: Mobile, Computer).          |
| CityTier                    | Integer | Kategori tier kota tempat pelanggan berada.                              |
| WarehouseToHome             | Integer       | Jarak gudang ke rumah pelanggan (dalam km).                              |
| PreferredPaymentMode        | Categorical   | Metode pembayaran utama (Debit Card, Credit Card, UPI, dll).             |
| Gender                      | Categorical   | Jenis kelamin pelanggan (Male/Female).                                   |
| HourSpendOnApp              | Float         | Rata-rata jam yang dihabiskan pelanggan di aplikasi per hari.             |
| NumberOfDeviceRegistered    | Integer       | Jumlah perangkat yang terdaftar untuk akun pelanggan.                     |
| PreferedOrderCat            | Categorical   | Kategori produk yang paling sering dipesan pelanggan.                     |
| SatisfactionScore           | Integer  | Skor kepuasan pelanggan terhadap layanan (skala 1–5).                     |
| MaritalStatus               | Categorical   | Status pernikahan pelanggan (Single, Married, dll).                       |
| NumberOfAddress             | Integer       | Jumlah alamat yang disimpan di akun pelanggan.                            |
| Complain                    | Integer  | Apakah pelanggan pernah mengajukan komplain (0 = tidak, 1 = ya).          |
| OrderAmountHikeFromlastYear | Float         | Persentase kenaikan jumlah belanja dibanding tahun sebelumnya.            |
| CouponUsed                  | Integer       | Jumlah kupon yang pernah digunakan pelanggan.                             |
| OrderCount                  | Integer       | Jumlah total pesanan pelanggan.                                           |
| DaySinceLastOrder           | Integer       | Jumlah hari sejak terakhir kali pelanggan melakukan pembelian.            |
| CashbackAmount              | Float         | Total jumlah cashback yang pernah diterima pelanggan.                     |


source data: https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction<br>
Notes : <br>
- Sebagian besar data berjenis integer
- Dataset ini memiliki baris sebanyak 5630 dan kolom berjumlah 20 kolom
- Dataset ini berjenis file csv

## **Exploratorary Data Analysis**

