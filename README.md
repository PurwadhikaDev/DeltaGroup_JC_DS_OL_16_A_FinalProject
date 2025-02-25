# DeltaGroup_JC_DS_OL_16_A_FinalProject

<a id="readme-top"></a>


<h3 align="center">TELCO CUSTOMER CHURN ANALYSIS</h3>

  <p align="center">
    
    TEAM DELTA:
    - AHMADES SEPTIAN RAHMADSYAH
    - ERICH DEWANTARA
    - NGURAH BAGUS ARYA WIDIANTARA
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#business-problem-understanding">Business Problem Understanding</a>
      <ul>
        <li><a href="#context">Context</a></li>
        <li><a href="#problem-statement">Problem Statement</a></li>
        <li><a href="#stakeholder-in-charge">Stakeholder In-charge</a></li>
        <li><a href="#goals">Goals</a></li>
        <li><a href="#analytic-approach">Analytic Approach</a></li>
        <li><a href="#metric-evaluation">Metric Evaluation</a></li>
      </ul>
    </li>
    <li>
      <a href="#data-understanding">Data Understanding</a>
      <ul>
        <li><a href="#features">Features</a></li>
        <li><a href="#data-preprocessing">Data Preprocessing</a></li>
      </ul>
    </li>
    <li>
      <a href="#data-analytics">Data Analytics</a>
    </li>
    <li>
      <a href="#tableau-dashboard">Tableau Dashboard</a>
    </li>
    <li>
      <a href="#modeling-and-tuning">Modeling & Tuning</a>
      <ul>
        <li><a href="#modeling">Modeling</a></li>
        <li><a href="#resampling">Resampling</a></li>
        <li><a href="#coefficient">Coefficient</a></li>
        <li><a href="#tuning">Tuning</a></li>
        <li><a href="#confusion-matrix">Confusion Matrix</a></li>
      </ul>
    </li>
    <li><a href="#conclusion-and-recommendation">Conclusion & Recommendation</a></li>
  </ol>
</details>



<!-- Business Problem Understanding -->
## Business Problem Understanding
### Context
Pelanggan selalu menjadi teka-teki bagi sebuah bisnis. Ada banyak sekali buku tentang cara meraih kesuksesan dalam bisnis, tetapi jika ditelaah lebih dalam, semuanya tetap kembali pada pelanggan karena merekalah yang membawa keuntungan.

Sebuah bisnis, termasuk Telco sebagai perusahaan yang berfokus pada internet dan telekomunikasi, tentu ingin selalu memberikan pelayanan terbaik kepada pelanggan agar mereka tetap dapat bertahan di tengah persaingan bisnis yang kompetitif. Namun, ungkapan "Nothing Last Forever" selalu relevan dalam kehidupan sehari-hari, termasuk dalam hubungan antara pelangganan dan langganan. Oleh karena itu, memahami pola perilaku pelanggan menjadi sangat penting untuk menjaga stabilitas bisnis serta mendukung pengambilan keputusan terkait retensi dan loyalitas pelanggan. Di sinilah peran analisis Customer Churn menjadi krusial.

Customer Churn adalah tingkat di mana pelanggan meninggalkan bisnis atau platform komersial dan mengalihkan pengeluarannyaa tempat lain. Customer Churn menjadi metrik yang penting karena memperoleh pelanggan baru bisa lima hingga tujuh kali lebih mahal dibandingkan mempertahankan pelanggan yang sudah ada<sup>[1](https://www.forbes.com/councils/forbesbusinesscouncil/2022/12/12/customer-retention-versus-customer-acquisition/), [2](https://www.outboundengine.com/blog/customer-retention-marketing-vs-customer-acquisition-marketing/#:~:text=Customer%20acquisition%20%26%20retention%20marketing%20stats,profits%20from%2025%2D95%25.)</sup>. Untuk mengurangi tingkat churn, perusahaan perlu memprediksi pelanggan mana yang berisiko tinggi untuk berhenti berlangganan.

Laporan ini mengeksplorasi lebih dalam pola perilaku pelanggan pascabayar di perusahaan Telco guna mengungkap wawasan dan strategi dalam meningkatkan retensi serta kepuasan pelanggan dalam industri telekomunikasi, sehingga dapat meminimalkan risiko churn.

### Problem Statement
Pelanggan dapat dengan mudah berganti paket bahkan berganti provider dalam industri telekomunikasi. Menurut laporan dari [MaxBill (Maret, 2023)](https://www.dataportabilitycooperation.org/data-portability-telecom-customer-churn-rates/#:~:text=As%20reported%20by%20MaxBill%20in%20March%202023%2C%20the,times%20more%20costly%20than%20retaining%20an%20existing%20one), industri ini menghadapi tingkat *churn rate* sebesar 20-40 persen, yang menunjukkan peningkatan signifikan dalam perpindahan pelanggan.

Telco, sebagai perusahaan telekomunikasi, terus dihadapkan pada tantangan dalam menentukan langkah terbaik untuk mengatasi tingkat *churn* yang cukup signifikan, yaitu sebesar 26,5 persen. Untuk **menurunkan persentase *churn*, perusahaan perlu mengidentifikasi pelanggan yang memiliki potensi berhenti berlangganan**, sehingga dapat memutuskan strategi retensi yang lebih efisien.

*Stakeholder* dalam perusahaan telekomunikasi dapat menerapkan berbagai strategi retensi, seperti memberikan potongan harga, menawarkan paket layanan yang menarik, atau memberikan prioritas pelayanan, untuk mempertahankan pelanggan. Namun, kebijakan pemberian insentif retensi belum sepenuhnya efektif. Apabila tidak ditargetkan dengan tepat, insentif ini dapat meningkatkan biaya operasional dan mengurangi potensi keuntungan, terutama jika diberikan kepada pelanggan yang sebenarnya sudah loyal dan tidak berencana untuk berhenti berlangganan.

### Stakeholder In-charge
- **Manajemen Eksekutif**, karena mereka perlu memahami dampak *churn* terhadap pendapatan dan proyeksi keuangan perusahaan, serta mengambil keputusan strategis untuk meminimalkan tingkat *churn*.

- **Marketing Departemen**, karena mereka bertanggung jawab untuk mengidentifikasi segmen pelanggan dengan risiko *churn* yang tinggi dan merancang strategi promosi atau kampanye yang efektif untuk mempertahankan pelanggan.

- **Customer Service Team**, karena mereka adalah garda terdepan dalam menangani keluhan dan permasalahan pelanggan yang dapat menyebabkan *churn*, sehingga diperlukan akses terhadap data *churn* agar dapat menangani masalah secara proaktif dan meningkatkan kepuasan pelanggan.

### Goals
Berdasarkan permasalahan yang ada, perusahaan Telco tentunya ingin mengembangkan sebuah tool yang dapat mengidentifikasi pelanggan berisiko churn dengan tingkat akurasi model di atas 80 persen. Dengan adanya alat prediksi ini, perusahaan dapat mengambil keputusan yang lebih tepat dan berbasis data untuk meningkatkan efektivitas retensi pelanggan.

Selain itu, perusahaan juga ingin mengetahui faktor-faktor utama yang mempengaruhi pelanggan berhenti berlangganan, seperti kualitas layanan, tenor, harga, dan faktor lainnya. Dengan pemahaman ini, perusahaan dapat merancang strategi yang lebih terarah, seperti meningkatkan pengalaman pelanggan, menyediakan layanan yang lebih personal, maupun mengoptimalkan program retensi.

Harapan dari solusi analitik ini adalah menurunkan tingkat churn pelanggan Telco menjadi 10 persen. Dengan pencapaian tersebut, perusahaan dapat mempertahankan lebih banyak pelanggan, mengurangi biaya akuisisi pelanggan baru, serta meningkatkan keuntungan jangka panjang. Penurunan churn yang signifikan tidak hanya membuat perusahaan lebih cost-efficient tetapi juga semakin kompetitif dalam industri telekomunikasi.

### Analytic Approach
Analisis dilakukan untuk mengidentifikasi pola dari berbagai fitur dalam data untuk memperoleh wawasan yang lebih mendalam mengenai perilaku pelanggan. Berdasarkan hasil analsiis tersebut, dapat **dikembangkan model klasifikasi yang berfungsi sebagai alat prediktif** dalam mengidentifikasi kemungkinan pelanggan untuk berhenti berlangganan. Model ini diharapkan dapat mendukung perusahaan dalam merancang strategi retensi.

### Metric Evaluation
![Confusion Matrix Final Project](https://github.com/user-attachments/assets/3a179f37-c723-45de-bcba-0f87f0e57c23)
Type 1 Error: False Positive (pelanggan yang aktualnya tidak churn, tetapi diprediksi churn).
- Konsekuensi: tidak efektifnya pemberian insentif retensi.

Type 2 Error: False Negative (pelanggan yang aktualnya churn, tetapi diprediksi tidak akan churn).
- Konsekuensi: kehilangan pelanggan. 

Berdasarkan konsekuensinya, konsekuensi *False Negative* memiliki dampak yang lebih signifikan karena biaya akuisisi pelanggan baru jauh lebih tinggi dibandingkan dengan biaya mempertahankan pelanggan yang sudah ada. Oleh karena itu, pendekatan yang akan diterapkan dala model ini adalah mengurangi kemungkinan terjadinya *False Negative*.

Untuk mencapai tujuan tersebut, **Recall menjadi parameter paling sesuai** dalam mengevaluasi kinerja model prediksi, yang berfokus pada memaksimalkan *True Positive* dan meminimalkan *False Negative*.


<!-- DATA UNDERSTANDING -->
## Data Understanding
Dataset Telco Customer ini berisi informasi mengenai pelanggan dari sebuah perusahaan telekomunikasi fiktif yang menyediakan layanan telepon rumah dan internet. Dataset mencakup pelanggan yang berlokasi di California, US, selama kuartal ketiga, yang mencerminkan status pelanggan, yaitu apakah mereka baru, tetap, atau berhenti berlangganan.

### Features
| No. | **Attribute** | **Description** |
| - | - | - |
| 1. | **customerID** | ID customer. |
| 2. | **gender** | Jenis kelamin customer (***Male, Female***). |
| 3. | **SeniorCitizen** | Indikasi customer berusia 65 tahun atau lebih (***1, 0***). |
| 4. | **Partner** | Indikasi apakah customer memiliki pasangan (***Yes, No***). |
| 5. | **Dependents** | Indikasi apakah customer memiliki tanggungan (***Yes, No***). |
| 6. | **tenure** | Jumlah bulan customer telah berlangganan layanan perusahaan. |
| 7. | **PhoneService** | Layanan langganan telepon rumah (***Yes, No***). |
| 8. | **MultipleLines** | Layanan langganan beberapa saluran telepon (***Yes, No, No phone service***). |
| 9. | **InternetService** | Layanan langganan internet (***DSL, Fiber optic, No***). |
| 10. | **OnlineSecurity** | Layanan langganan keamanan online tambahan (***Yes, No, No internet service***). |
| 11. | **OnlineBackup** | Layanan langganan backup online tambahan (***Yes, No, No internet service***). |
| 12. | **DeviceProtection** | Layanan langganan perlindungan perangkat tambahan (***Yes, No, No internet service***). |
| 13. | **TechSupport** | Layanan dukungan teknis tambahan dengan waktu respon lebih singkat (***Yes, No, No internet service***). |
| 14. | **StreamingTV** | Indikasi apakah customer menggunakan layanan internet untuk streaming program TV pihak ketiga (***Yes, No, No internet service***). |
| 15. | **StreamingMovies** | Indikasi apakah customer menggunakan layanan internet untuk streaming film pihak ketiga (***Yes, No, No internet service***). |
| 16. | **Contract** | Jenis kontrak layanan customer (***Month-to-month, One year, Two year***). |
| 17. | **PaperlessBilling** | Indikasi customer memilih paperless billing (***Yes, No***). |
| 18. | **PaymentMethod** | Metode pembayaran tagihan (***Electronic check, Mailed check, Bank transfer (automatic), Credit card (automatic)***). |
| 19. | **MonthlyCharges** | Jumlah tagihan bulanan. |
| 20. | **TotalCharges** | Akumulasi total tagihan hingga akhir masa langganan. |
| 21. | **Churn** | Indikasi apakah customer churned (***Yes, No***). |

### Data Preprocessing
Tahap cleaning: 
- Data formatting.
- Missing values.
- Data duplicates.
- Outliers.

## Data Analytics
Dalam tahapan ini, kami melakukan beberapa analisis terhadap dataset. Diantaranya adalah:
1. Data distribution.
2. Demographic distribution.
3. Hubungan target (churn) terhadap feature numerik.
4. Hubungan target (churn) terhadap feature kategorikal pada dataset.
5. Hubungan antar feature.

## Tableau Dashboard
[Link to Tableau](https://public.tableau.com/views/DeltaGroup_JC_DS_OL_16_A_FinalProject/HRANALYTICSDASHBOARD?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
![image](https://github.com/user-attachments/assets/ab71cb48-7404-43fe-b575-9e7f6886dd9f)

## Data Preparation
1. Feature Selection:  
Metode feature selection yang digunakan adalah model-based selection, di mana feature dipilih menggunakan model machine learning. Metode ini dipertimbangkan karena model dapat menangkap hubungan atau interaksi antar fitur yang mungkin tidak terlihat dengan metode seleksi lainnya. Selain itu, beberapa feature mungkin baru terlihat pengaruhnya ketika dikombinasikan dengan feature lain, sehingga pendekatan model-based memberikan hasil yang lebih optimal setelah adanya penyesuaian yang dilakukan oleh model machine learning.
2. Feature Engineering:  
Langkah ini dilakukan untuk mengubah fitur dalam dataset agar model machine learning dapat bekerja lebih optimal. Kami menggunakan Onehot-encoding dan Ordinal encoding.


<!-- Modeling and Tuning -->
## Modeling and Tuning
### Modeling
Kami menggunakan beberapa model, yaitu: 
- logreg = LogisticRegression()
- svm = SVC()
- dt = DecisionTreeClassifier()
- rf = RandomForestClassifier()
- xgb = XGBClassifier()
- lgbm = LGBMClassifier()

Setelah dilakukan modeling, hasil terbaik adalah dengan menggunakan model **Logistic Regression**.

### Resampling
Resampling adalah teknik yang digunakan dalam pembelajaran mesin untuk menangani masalah ketidakseimbangan kelas dalam dataset (imbalance). Ketidakseimbangan kelas sering terjadi ketika satu kelas lebih banyak jumlahnya dibandingkan dengan kelas lainnya dalam hal ini pada kolom churn, yang dapat menyebabkan model tidak dapat mempelajari pola dari kelas minoritas dengan baik. Dua pendekatan umum untuk mengatasi masalah ini adalah SMOTE (Synthetic Minority Over-sampling Technique) dan Penalized Model.

SMOTE bekerja dengan menciptakan data sintetis baru untuk kelas minoritas, membantu model mengenali pola yang lebih baik pada kelas yang lebih sedikit.

Penalized Model memberi penalti pada kesalahan klasifikasi untuk kelas minoritas, sehingga model lebih fokus pada kesalahan tersebut, tanpa memerlukan perubahan pada data.

### Coefficient
Dalam Model-based selection, kami menggunakan nilai coefficient sebagai feature selection. Tujuan dari feature selection adalah untuk meningkatkan performa model, mengurangi kompleksitas, menghindari overfitting, dan mengurangi waktu komputasi.

### Tuning
Hyperparameter tuning adalah proses untuk menemukan kombinasi hyperparameter terbaik yang akan menghasilkan model pembelajaran mesin yang paling optimal. Hyperparameter adalah parameter yang ditetapkan sebelum proses pelatihan dimulai dan tidak dipelajari oleh model selama pelatihan. Model yang digunakan adalah Logistic Regression dengan parameter sebagai berikut:

1. `C`: [0.001, 0.01, 0.1, 1, 10, 100], 
2. `penalty`: ["l1", "l2", "elasticnet", "none"], 
3. `solver`: ["liblinear", "lbfgs", "newton-cg", "sag", "saga"], 
4. `max_iter`: [100, 200, 500]

### Confusion Matrix
Terdapat Confusion Matrix sebelum dan sesudah tuning.


<!-- Conclusion and recommendation -->
## Conclusion and Recommendation
Terdapat konklusi dan rekomendasi model dari hasil analisis, serta rekomendasi bisnis kepada stakeholder in-charge.


<!-- ABOUT PROJECT -->
## About Project
Project ini sebagai syarat Final Project dari Purwadhika Digital Technology School.


<!-- CONTACT -->
## Contact
Ahmades Septian Rahmadsyah - ahmades0516@gmail.com
- Project Link: [https://github.com/Ahmades0516](https://github.com/Ahmades0516)

Erich Dewantara - erich.dewantara@gmail.com
- Project Link: [github.com/erichdewantara](github.com/erichdewantara)

Arya Widiantara - arya.wtr@gmail.com
- Project Link: [https://github.com/arya-wtr](https://github.com/arya-wtr)

 

<p align="right">(<a href="#readme-top">back to top</a>)</p>
