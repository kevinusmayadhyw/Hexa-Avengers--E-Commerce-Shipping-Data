# **Hexa Avengers (E-Commerce Shipping Data)**

# **Info Dataset**

Dataset yang digunakan merupakan dataset [E-Commerce Shipping Data](https://www.kaggle.com/datasets/prachi13/customer-analytics) yang diambil dari kaggle yang terdiri dari 10999 baris dan 12 kolom. Kolom pada dataset ini terdiri dari:
- **ID**: ID Number of Customers.
- **Warehouse block**: The Company have big Warehouse which is divided in to block such as A,B,C,D,E.
- **Mode of shipment**:The Company Ships the products in multiple way such as Ship, Flight and Road.
- **Customer care calls**: The number of calls made from enquiry for enquiry of the shipment.
- **Customer rating**: The company has rated from every customer. 1 is the lowest (Worst), 5 is the highest (Best).
- **Cost of the product**: Cost of the Product in US Dollars.
- **Prior purchases**: The Number of Prior Purchase.
- **Product importance**: The company has categorized the product in the various parameter such as low, medium, high.
- **Gender**: Male and Female.
- **Discount offered**: Discount offered on that specific product.
- **Weight in gms**: It is the weight in grams.
- **Reached on time**: It is the target variable, where 1 Indicates that the product has NOT reached on time and 0 indicates it has reached on time.

# **Info Bisnis**
## a. Problem
<div style="text-align: justify">
<p>
PT. Avengers adalah sebuah perusahaan yang bergerak dalam bidang e-commerce. Didirikan tahun 2022 dan kini memiliki 10.999 transaksi yang tercatat dalam database. Pimpinan hendak mengevaluasi terkait kinerja divisi shipping terkait temuan bahwa  sebanyak 6.563 (59.7%) dari total transaksi mengalami keterlambatan pengiriman yang diduga mempengaruhi penilaian customer terhadap kinerja perusahaan. 
</p>
<p>
Tim bisnis menugaskan tim data untuk melakukan analisis terhadap data yang disediakan perusahaan untuk mengidentifikasi penyebab keterlambatan pengiriman sehingga dapat memberi rekomendasi terkait penyelesaian problem not on time rate yang tinggi.
</p>
</div>

## b. Peran
Sebagai Tim Data yang terdiri dari\
Project Leader: Kevin Usmayadhy Wijaya\
Data Analyst: Vicky Clarissa Jennie Damara\
Data Scientist : Nabil Abduh Aqil\
Machine Learning Engineer: Febiya Jomy Pratiwi\
Business Analyst: Qistina Muharrifa & Riel Jeremy Jordan Umboh

## c. Goal
Goal yang ingin dicapai adalah Menurunkan persentase keterlambatan barang

## d. Objective
- Membuat model klasifikasi yang bisa memprediksi keterlambatan barang sehingga perusahaan dapat memberikan notifikasi keterlambatan kepada customer
- Mengetahui faktor-faktor yang mempengaruhi keterlambatan

## e. Business Metrics
Not on-time Rate (Persentase produk yang tidak tepat waktu)

# **EDA**
## Data Numerik
![Numerik](img/datanumerik.png)
## Data Numerik Berdasarkan Variable Target (Is_Not_Ontime)
![Numerik Target](img/datanumerik_target.png)

Berdasarkan hasil dari violin plot sebelumnya, dapat ditarik beberapa kesimpulan diantaranya:
- Column Prior_purchases dan Discount_offered secara keseluruhan terdapat nilai outlier yang tidak normal sehingga perlu dilakukan penanganan khusus (bisa didrop atau direplace).
- Setelah dipisah berdasarkan targetnya, column Discount_offered dan Weight_in_gms memiliki perbedaan persebaran data yang cukup signifikan pada produk yang on-time dan yang tidak on-time. Oleh karena itu, column ini bisa kita tandai sebagai column yang berkemungkinan berpengaruh terhadap ketepatan produk yang dikirim.
- Selain column diatas, persebarannya normal.

## Data Kategorikal
![Kategorikal](img/datakategorikal.png)
## Data Kategorikal Berdasarkan Variable Target (Is_Not_Ontime)
![Kategorikal Target](img/datakategorikal_target.png)

Berdasarkan hasil dari countplot diatas, dapat ditarik beberapa kesimpulan diantaranya:
1. Sebelum Dipisah
- Persebaran pada column **Warehouse_block** terdapat 1 block yang memiliki **jumlah yang jauh lebih banyak** dengan block lainnya, yaitu **block F**.
- Pada column **Mode_of_Shipment** terdapat 1 mode yang memiliki **jumlah jauh lebih banyak** dibandingkan dengan mode lainnya yaitu mode pengiriman menggunakan **Ship**.
- Pada column **Product_importance** terdapat 1 kategori importance yang memiliki **jumlah jauh lebih sedikit** dibandingkan dengan kategori lainnya yaitu kategori **High**.
- Pada column **Gender tidak ada perbandingan yang signifikan**.
- Pada column **Is_Late**, perbandingan data yang **late:ontime** sekitar sebesar **3:2**
2. Setelah Dipisah
- Persebaran data pada column yang dipisah berdasarkan column targetnya, **tidak ada perbedaan yang signifikan antara target disetiap kategorinya**

## Korelasi
![Korelasi](img/korelasi.png)

Berdasarkan matrix korelasi dapat disimpulkan bahwa:

**Positif Correlation**
- Adanya korelasi positif antara discount offered dengan Is_Not_Ontime sebesar 40%. Tingginya discount yang ditawarkan menyebabkan banyaknya barang yang mengalami keterlambatan.
- Adanya korelasi positif antara customer care calls dengan cost product sebanyak 32%.  Hal ini menyebabkan semakin tinggi cost product, maka ada kecenderungan semakin tinggi customer care calls.
- Adanya korelasi positif antara customer care calls dengan prior purchase sebanyak 18%. Customer care calls tertinggi ada pada prior purchase 3.

**Negatif Correlation**
- Adanya korelasi negatif antara discount offer dan weight in gms sebesar -38%. Adanya kecenderungan bahwa kecilnya berat barang menyebabkan barang mendapatkan diskon yang besar.
- Adanya korelasi negatif antara customer care calls dengan weight in gms sebesar -28%. Adanya kecenderungan bahwa semakin kecil berat barang, maka semakin tinggi customer care calls nya.
- Adanya korelasi negatif antara customer care calls dengan discount offered sebesar -13%. Adanya kecenderungan bahwa semakin kecil diskon yang ditawarkan, maka akan semakin tinggi customer care calls nya.


Sehingga Korelasi tertinggi antara target (Is_late) dengan column fiturnya adalah column Discount_offered yaitu sebesar 0.40, lalu diikuti dengan column Weight_in_gms sebesar -0.27.

## PairPlot
![Pair Plot](img/pairplot.png)

- Terdapat pola pada column Discount_offered yang mana sekitar jumlah diskon lebih dari 15% berpeluang untuk produk Is_Late.
- Terdapat pola pada column Weight_in_gms dimana persebaran barang yang Is_Late mayoritas terdapat pada jumlah berat 2000 - 4000 gram.

# Business Insight
Business Insight yang diambil dikaitkan dengan target variablenya (bisnis metrics) yaitu colomn Is_Late
## - Persentase Orderan berdasarkan Discount Offered dan Is_Late
![Discount Offered](img/discount_offered.png)

Berdasarkan persebaran data pada grafik terlihat bahwa penawaran diskon diatas 15%, 100% merupakan barang yang Late. Sedangkan untuk penawaran diskonnya dibawah 15% terdapat barang yang dikirim ontime meskipun masih banyak orderan yang Late diatas 50%.

## - Persentase Orderan berdasarkan Weight dan Is_Late
![Weight_in_gms](img/Weight_in_gms.png)

Berdasarkan persebaran data pada grafik diatas terlihat bahwa berat sekitaran 2500-3500 dan diatas 6000 gram, 100% dari orderannya merupakan barang yang Late. Sedangkan untuk barang yang memiliki berat 0-2500 dan 3500-6500 gram masih terdapat barang yang ontime meskipun masih terdapat barang yang late diatas 20%.

## - Persebaran Orderan berdasarkan Weight, Discount Offered, dan Is_Late
![Discount_Weight_in_gms](img/Discount_Weight_in_gms.png)

Berdasarkan grafik terlihat bahwa semua barang yang memiliki berat 2000-4000 gram dan memiliki diskon diatas 10%, semuanya merupakan barang yang terlambat. Dan juga dengan berat 2000-4000 gram memiliki diskon dibawah 10%, semuanya juga merupakan barang yang terlambat.

## - Persentase Orderan berdasarkan Customer Care Calls dan Is_Late
![Customer_care_calls](img/Customer_care_calls.png)

Jika dilihat dari grafik diatas semakin tinggi jumlah Customer_care_calls justru tidak merepresentasikan barang tersebut Late, yang terjadi justru sebaliknya. Hal ini mengidentifikasikan bahwa barang yang dikirim secara ontime tidak akan mengurangi Customer_care_calls.

## - Jumlah Warehouse Block, Shipment dan Is_Late
![warehouse](img/warehouse.png)

Berdasarkan bar plot berikut, dapat disimpulkan:
- Baik di warehouse block A, B, C, D, F lebih banyak barang mengalami keterlambatan pengiriman daripada barang datang tepat waktu
- Pada setiap warehouse, barang mode pengiriman dengan Ship memiliki jumlah barang datang tidak tepat waktu dan datang tepat waktu tertinggi dibandingkan mode lainnya.

## - Persentase Mode of Shipment terhadap Persentase Is_Late
![Mode of Shipment](img/ModeofShipment.png)

Berdasarkan pie plot di atas, dapat disimpulkan bahwa:
- Barang dengan mode shipment Flight memiliki persentase keterlambatan tertinggi dibandingkan mode shipment lainnya.
- Barang dengan mode shipment Road memiliki persentase keterlambatan terkecil dibandingkan kedua mode shipment lainnya.
- Namun Baik barang dengan mode of shipment ship, road, dan flight tetap mengalami persentase keterlambatan yang relatif besar.

## - Persentase Product Importance terhadap Persentase Is_Late
![Product Importance](img/Product_Importance.png)

Baik barang dengan product importance high, medium, dan low tetap mengalami keterlambatan yang relatif besar.

# Business Recommendation
1. Mengevaluasi kembali model perhitungan estimasi produk sampai (jika diperlukan buat kembali model yang lebih akurat).
2. Meminimalisir keterlambatan pengiriman dengan mengevaluasi metode pengiriman (terutama pada mode shipment Flight) dan mempercepat proses packing.
3. Mengevaluasi kembali berdasarkan pemberian diskon yang ditawarkan, terutama pada dua kategori yaitu pemberian diskon antara 0-10 dan lebih dari 10. Apa yang membedakan produk antara dua kategori tersebut. Mengapa barang yang memiliki banyak diskon semuanya tidak ontime. 
4. Mengevaluasi kembali berdasarkan beratnya, terdapat 3 kategori yang perlu difokuskan pada kategori ini yaitu 0-2000, 4000-6000, dan sisanya. Mengapa pada berat selain 0-2000 dan 4000-6000 tidak terdapat produk yang on-time.
