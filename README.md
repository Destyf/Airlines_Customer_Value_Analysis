# Airline Customer Value Analysis Case with Clustering K-Means Based on LRFC Model

## Introduction
Semakin meningkatnya persaingan perusahaan Airline dapat menyebabkan penurunan pendapatan salah satunya dengan terjadinya kehilangan pelanggan. Perusahaan saat ini perlu melakukan strategi untuk dapat bersaing, salah satunya dengan pendekatan pelanggan. Pendekatan yang dilakukan perusahaan dapat dilakukan dengan melakukan clustering pelanggan untuk melihat karakteristik mana pelanggan yang memiliki nilai yang tinggi maupun rendah. Dengan hal ini, perusahaan dapat melakukan strategi pemasaran dan memberikan layanan yang berbeda sesuai dengan klasifikasi pelanggan tersebut sehingga Perusahaan dapat lebih optimal dalam meningkatkan penjualan dan pendapatan.

## Exploratory Data Analysis
-	Data memiliki 62988 rows & 23 columns (15 data numerikal, 8 data kategorikal).
-	Terdapat missing value pada feature GENDER, WORK_CITY, WORK_PROVINCE, WORK_COUNTRY,AGE, SUM_YR_1 & SUM_YR_2.
-	Tidak terdapat duplicated data.
-	Terdapat feature yang memiliki outliers data yaitu FFP_TIER, AGE, FLIGHT_COUNT, BP_SUM, SUM_YR_1, SUM_YR_2, SEG_KM_SUM, LAST_TO_END, AVG_INTERVAL, MAX_INTERVAL, EXCHANGE_COUNT, avg_discount, Points_Sum, & Point_NotFlight.
-	Pada feature kategorikal meyoritas memiliki data unik.
-	Distribusi data mayoritas berbentuk positively skew, kecuali MEMBER_NO & avg_discount mendekati normal.
-	Terdapat beberapa feature yang memiliki korelasi tinggi yaitu FLIGHT_COUNT, BP_SUM, SUM_YR_1, SUM_YR_2, SEG_KM_SUM, AVG_INTERVAL, MAX_INTERVAL & Points_Sum.

## Pre-Processing Data
-	Terdapat missing value sebesar 7.51%, maka diputuskan untuk dihapus karena tidak terlalu signifikan mempengaruhi hasil & beberapa feature memiliki banyak value yang unik yaitu GENDER, WORK_CITY, WORK_PROVINCE, WORK_COUNTRY, AGE, SUM_YR_1, & SUM_YR_2.
-	Merubah tanggal 2014/2/29 pada feature LAST_FLIGHT_DATE, karena pada tahun 2014 bukan tahun kabisat sehingga tidak ada tanggal 29 di bulan Februari.
-	Merubah data type menjadi datetime.
-	Menambah feature baru LOYALTY_TIME dihitung dari (LOAD_TIME - FFP_DATE) / 30 hari.
-	Melakukan feature selection berdasarkan LRFC model yang dibandingkan dengan heatmap yaitu : 
•	L (LOYALTY) : Lama waktu user menjadi membership (LOYALTY_TIME).
•	R (RECENCY) : Jarak waktu sejak penerbangan terakhir ke pesanan teakhir (LAST_TO_END).
•	F (FREQUENCY) : Total jumlah user melakukan penerbangan (FLIGHT_COUNT).
•	C (DISCOUNT) : Rata-rata discount yang didapat user (avg_discount).
-	Melakukan handling outliers.
-	Melakukan standardization & merubah nama kolom menjadi Loyalty, Recency, Frequency, & Discount.

## Modeling
-	Menggunakan clustering K-Means berdasarkan elbow method dan dibandingkan dengan nilai inertia dengan parameter distorsi, maka nilai K-Cluster adalah 5.

## Intepretasi & Rekomendasi
### Cluster 0 - New Customers
Cluster New Customers memiliki tingkat rata-rata loyalty yang cukup tinggi dengan recency yg sangat rendah, tetapi frequency penerbangan dan tingkat discount tergolong tinggi, hal ini dapat menunjukan pelanggan cluster ini cenderung menjadi anggota dalam waktu singkat.
Business Recommendation:
-	Menawarkan voucher atau diskon menarik agar memotivasi untuk bertransaksi lebih lanjut.
-	Menawarkan program member dengan manfaat yang menarik.
### Cluster 1 - Loyal Customers
Cluster Loyal Customers memiliki tingkat Loyalty yang sangat tinggi dimana pelanggan telah menjadi member dalam jangka waktu yang lama meskipun Recency dan aktivitas Frequency penerbangan mereka sedang.
Business Recommendation:
-	Menawarkan program loyalitas pelanggan untuk memperkuat keterikatan dengan pelanggan, dimana dengan bergabung program dapat memperoleh manfaat lebih dibandingkan cluster lain seperti loyalty point yang dapat diredeem dengan reward menarik, diskon khusus, hadiah langsung, atau voucher untuk penerbangan selanjutnya.
### Cluster 2 - Potential Loyal Customers
Cluster Potential Loyal Customers memiliki rata-rata tingkat Loyalty yang rendah. Meskipun belum menjadi Loyal Customers, cluster ini berpotensi karena pelanggan melakukan transaksi Recency sedikit tinggi dan frequency penerbangan lebih tinggi dibanding cluster Loyal Customers.
Business Recommendation:
-	Menawarkan promo bundling atas pemesanan tiket penerbangan.
-	Memberikan point atas setiap transaksi yang dapat diredeem dengan reward.
-	Memberikan diskon atau voucher untuk penerbangan selanjutnya.
### Cluster 3 - Inactive Customers
Cluster Inactive Customers memiliki rata-rata Loyalty yang rendah dan melakukan pesanan penerbangan terakhir sudah sangat lama dan melakukan aktivitas penerbangan sangat rendah. Hal ini dapat menunjukan pelanggan telah lama menjadi anggota tetapi tidak aktif bertransaksi.
Business Recommendation:
-	Memberikan promo khusus atau insentif kepada pelanggan agar bertransaksi kembali, seperti diskon khusus dan program penerbangan.
### Cluster 4 - General Customers
Cluster General Customers memiliki rata-rata Loyalty yang rendah, Recency yang tinggi, Frequency penerbangan sedang dan memiliki tingkat Discount yang sangat rendah.
Business Recommendation:
-	Menawarkan program member dengan manfaat yang menarik untuk bertransaksi lebih lanjut.
