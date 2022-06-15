---
lab:
  title: Menggunakan Desainer Azure Machine Learning
ms.openlocfilehash: 3bfe1bf2e119c295ad3931c569e1f09b41bb2174
ms.sourcegitcommit: 38540a481d1dfa9bab570777b72e3cf9b6ee6da7
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 12/16/2021
ms.locfileid: "145195823"
---
# <a name="use-azure-machine-learning-designer"></a>Menggunakan Desainer Azure Machine Learning

*Perancang* Azure Machine Learning menyediakan lingkungan seret & lepas tempat Anda dapat menentukan alur kerja, atau *saluran* penyerapan data, transformasi, dan modul pelatihan model untuk membuat model pembelajaran komputer. Anda kemudian dapat memublikasikan saluran pipa ini sebagai layanan web yang dapat digunakan aplikasi klien untuk *inferensi* (menghasilkan prediksi dari data baru).

## <a name="before-you-start"></a>Sebelum Memulai

Jika Anda belum melakukannya, selesaikan latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Azure Machine Learning dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="configure-compute-resources"></a>Mengonfigurasi sumber daya komputasi

Untuk menggunakan perancang Azure Machine Learning, Anda memerlukan komputasi untuk menjalankan eksperimen pelatihan model.

1. Masuk ke [Azure Machine Learning studio](https://ml.azure.com?azure-portal=true) dengan kredensial Microsoft yang terkait dengan langganan Azure Anda, dan pilih ruang kerja Azure Machine Learning Anda.
2. Di Azure Machine Learning studio, lihat halaman **Komputasi**; dan pada tab **Instans komputasi**, mulai instans komputasi Anda jika belum berjalan. Anda akan menggunakan instans komputasi ini untuk menguji model terlatih Anda.
3. Saat instans komputasi dimulai, alihkan ke tab **Kluster komputasi**. Jika Anda belum memiliki kluster komputasi yang ada, tambahkan kluster komputasi baru dengan pengaturan berikut. Anda akan menggunakan kluster ini untuk menjalankan alur pelatihan.
    - **Region**: *Wilayah yang sama dengan ruang kerja Anda*
    - **Prioritas Komputer Virtual**: Khusus
    - **Jenis Komputer Virtual**: CPU
    - **Ukuran Komputer Virtual**: Standard_DS11_v2
    - **Nama komputasi**: *masukkan nama unik*
    - **Jumlah minimum node**: 0
    - **Jumlah maksimum node**: 2
    - **Detik menganggur sebelum menurunkan skala**: 120
    - **Aktifkan akses SSH**: Tidak dipilih

## <a name="review-the-training-dataset"></a>Meninjau himpunan data pelatihan

Sekarang setelah Anda memiliki beberapa sumber daya komputasi yang dapat digunakan untuk menjalankan alur pelatihan, Anda memerlukan beberapa data untuk melatih model.

1. Di Azure Machine Learning studio, lihat halaman **Himpunan Data**. Himpunan data mewakili file data atau tabel tertentu yang Anda rencanakan untuk dikerjakan di Azure ML.
2. Jika Anda sebelumnya telah membuat kumpulan data **himpunan data diabetes**, buka. Jika tidak, buat kumpulan data baru dari file web, menggunakan pengaturan berikut, lalu buka:
    * **Info dasar**:
        * **URL Web**: 
        * **Nama**: himpunan data diabetes
        * **Jenis himpunan data**: Tabular
        * **Deskripsi**: Data diabetes
    * **Pengaturan dan pratinjau**:
        * **Format file**: Dibatasi
        * **Pemisah**: Koma
        * **Pengodean**: UTF-8
        * **Header kolom**: Menggunakan header dari file pertama
        * **Lewati baris**: Tidak ada
    * **Skema**:
        * Sertakan semua kolom selain **Jalur**
        * Meninjau jenis yang terdeteksi secara otomatis
    * **Konfirmasikan detail**:
        * Jangan membuat profil himpunan data setelah pembuatan

4. Lihat laman **Jelajahi** untuk melihat contoh data. Data ini mewakili detail dari pasien yang telah diuji diabetes, dan Anda akan menggunakannya untuk melatih model yang memprediksi kemungkinan pasien positif diabetes berdasarkan pengukuran klinis.

## <a name="create-a-designer-pipeline"></a>Membuat alur desainer

Untuk memulai dengan desainer, pertama-tama Anda harus membuat alur dan menambahkan himpunan data yang ingin Anda kerjakan.

1. Di studio Azure Machine Learning, lihat laman **Perancang** dan buat alur baru.
2. Ubah nama alur default (**Pipeline-Created-on-* date***) menjadi **Visual Diabetes Training** Dengan mengeklik nama default ikon (atau klik **&#9881 ;** di sebelah nama alur dan ubah dari sana)
3. Perhatikan bahwa Anda harus menentukan target komputasi untuk menjalankan alur. Di panel **Pengaturan**, klik **Pilih target komputasi** dan pilih kluster komputasi Anda.
4. Di sisi kiri perancang, luaskan bagian **Himpunan data**, dan seret himpunan data **himpunan data diabetes** ke kanvas.
5. Pilih modul **himpunan data diabetes** di kanvas. Kemudian klik kanan, dan pilih **Pratinjau data**.
6. Di panel DatasetOutput, pilih tab **Profil**.
7. Tinjau skema data, perhatikan bahwa Anda dapat melihat distribusi berbagai kolom sebagai histogram. Kemudian tutup visualisasi.

## <a name="add-transformations"></a>Menambahkan transformasi

Sebelum dapat melatih model, Anda biasanya perlu menerapkan beberapa transformasi pemrosesan awal ke data.

1. Di panel di sebelah kiri, perluas bagian **Transformasi Data**, yang berisi berbagai modul yang bisa Anda gunakan untuk mengubah data sebelum pelatihan model.
2. Seret modul **Normalkan Data** ke kanvas, di bawah modul **himpunan data diabetes**. Kemudian hubungkan output dari modul **himpunan data diabetes** ke input modul **Normalkan Data**.
3. Pilih modul **Normalize Data** dan lihat pengaturannya, perhatikan bahwa Anda harus menentukan metode transformasi dan kolom yang akan diubah. Kemudian, biarkan transformasi sebagai **ZScore**, edit kolom untuk menyertakan nama kolom berikut:
    * PlasmaGlucose
    * DiastolicBloodPressure
    * TricepsThickness
    * SerumInsulin
    * BMI
    * DiabetesPedigree

    **Catatan**: Kami menormalkan kolom numerik menempatkannya pada skala yang sama, dan menghindari kolom dengan nilai besar yang mendominasi pelatihan model. Anda biasanya menerapkan sejumlah besar transformasi pra-pemrosesan seperti ini untuk menyiapkan data Anda untuk pelatihan, tetapi kami akan menyederhanakannya dalam latihan ini.

4. Sekarang kita siap untuk membagi data menjadi himpunan data terpisah untuk pelatihan dan validasi. Di panel sebelah kiri, di bagian **Transformasi Data**, seret modul **Split Data** ke kanvas di bawah modul **Normalize Data**. Selanjutnya sambungkan output *Himpunan Data yang Diubah* (kiri) dari modul **Normalize Data** ke input modul **Split Data**.
5. Pilih modul **Split Data**, dan konfigurasikan pengaturannya sebagai berikut:
    * **Mode pemisah** Split Rows
    * **Pecahan baris dalam himpunan data output pertama**: 0,7
    * **Nilai awal acak**: 123
    * **Pemisahan bertingkat**: False

## <a name="add-model-training-modules"></a>Menambahkan modul pelatihan model

Dengan data yang disiapkan dan dibagi menjadi himpunan data pelatihan dan validasi, Anda siap mengonfigurasi alur untuk melatih dan mengevaluasi model.

1. Perluas bagian **Pelatihan Model** di panel sebelah kiri, dan seret modul **Train Model** ke kanvas, di bawah modul **Split Data**. Selanjutnya sambungkan output *Hasil dataset1* (kiri) dari modul **Split Data** ke input *Himpunan data* (kanan) dari modul **Train Model**.
2. Model yang kita latih akan memprediksi nilai **Diabetes**, jadi, pilih modul **Train Model** dan ubah pengaturannya untuk mengatur **kolom Label** ke **Diabetes** (huruf besar/kecil dan ejaannya harus sama persis!)
3. Label **Diabetes** yang akan diprediksi model adalah kolom biner (1 untuk pasien yang menderita diabetes, 0 untuk pasien yang tidak), jadi kita perlu melatih model menggunakan *klasifikasi* algoritma. Perluas bagian **Algoritma Pembelajaran Mesin**, dan di bawah **Klasifikasi**, seret modul **Two-Class Logistic Regression** ke kanvas, ke sebelah kiri modul **Split Data** dan di atas modul **Train Model**. Selanjutnya sambungkan output-nya ke input **model Untrained** (kiri) dari modul **Train Model**.
4. Untuk menguji model yang dilatih, kita perlu menggunakannya untuk menilai himpunan data validasi yang kita tahan saat kita membagi data asli. Perluas bagian **Penilaian & Evaluasi Model** dan seret modul **Score Model** ke kanvas, di bawah modul **Train Model**. Selanjutnya sambungkan output modul **Train Model** ke input **Trained model** (kiri) dari modul **Score Model**; dan seret output **Hasil dataset2** (kanan) dari modul **Split Data** ke input **Himpunan data** (kanan) dari modul **Score Model**.
5. Untuk mengevaluasi seberapa baik kinerja model, kita perlu melihat beberapa metrik yang dihasilkan dengan menilai himpunan data validasi. Dari bagian **Penilaian & Evaluasi Model**, seret modul **Evaluasi Model** ke kanvas, di bawah modul **Beri Nilai Model**, dan hubungkan output dari  **Beri Nilai Model** ke input **Himpunan data skor** (kiri) dari modul **Evaluasi Model**.

## <a name="run-the-training-pipeline"></a>Menjalankan alur pelatihan

Dengan langkah-langkah aliran data yang ditentukan, Anda sekarang siap untuk menjalankan alur pelatihan dan melatih model.

1. Verifikasi bahwa alur terlihat mirip dengan yang berikut:

    ![Jalur Pelatihan Visual](images/visual-training.jpg)

2. Di kanan atas, klik **Kirim**. Kemudian saat diminta, buat eksperimen baru bernama **mslearn-designer-train-diabetes**, dan jalankan.  Ini akan menginisialisasi kluster komputasi dan kemudian menjalankan alur, yang mungkin memerlukan waktu 10 menit atau lebih lama. Anda dapat melihat status eksekusi alur di bagian atas kanan kanvas desain.

    > **Tips**: Jika terjadi kesalahan **GraphDatasetNotFound**, pilih himpunan data dan di panel Propertinya, ubah **Versi** (Anda dapat beralih antara "Selalu gunakan yang terbaru" dan "1") - lalu ulangi menjalankan alur.
    >
    > Saat berjalan, Anda dapat melihat alur dan eksperimen yang telah dibuat di laman **Alur** dan **Eksperimen**. Beralih kembali ke saluran **Pelatihan Diabetes Visual** di laman **Perancang** setelah selesai.

3. Setelah modul **Normalisasi Data** selesai, pilih modul tersebut, dan di panel **Pengaturan**, pada tab **Output + log**, di bawah **Output data** di bagian **Set data yang diubah**, klik ikon **Pratinjau data**, dan perhatikan bahwa Anda dapat melihat statistik dan visualisasi distribusi kolom yang diubah.
4. Tutup visualisasi **Normalisasi Data** dan tunggu modul lainnya selesai. Kemudian visualisasikan output modul **Evaluasi Model** untuk melihat metrik kinerja model.

    **Catatan**: Performa model ini tidak terlalu bagus, sebagian karena kita hanya melakukan rekayasa fitur minimal dan pemrosesan awal. Anda dapat mencoba beberapa algoritme klasifikasi yang berbeda dan membandingkan hasilnya (Anda dapat menghubungkan keluaran modul **Data Terpisah** ke beberapa modul **Model Kereta** dan **Model Skor**, dan Anda dapat menghubungkan model skor kedua ke modul **Evaluasi Model** untuk melihat perbandingan berdampingan). Inti dari latihan ini hanyalah untuk memperkenalkan Anda pada antarmuka desainer, bukan untuk melatih model yang sempurna!

## <a name="create-an-inference-pipeline"></a>Membuat alur inferensi

Sekarang Anda telah menggunakan *alur pelatihan* untuk melatih model, Anda dapat membuat *alur inferensi* yang menggunakan model terlatih untuk memprediksi label data baru.

1. Di daftar drop-down **Buat alur masuk**, klik **Alur inferensi real-time**. Setelah beberapa detik, versi baru saluran Anda yang bernama **Inferensi real-time Pelatihan Diabetes Visual** akan dibuka.
2. Ganti nama alur baru menjadi **Prediksi Diabetes**, lalu tinjau alur baru. Perhatikan bahwa transformasi normalisasi dan model terlatih telah dirangkum dalam alur ini sehingga statistik dari data pelatihan Anda akan digunakan untuk menormalisasi nilai data baru, dan model terlatih akan digunakan untuk menilai data baru.
3. Perhatikan bahwa saluran inferensi mengasumsikan bahwa data baru akan cocok dengan skema data pelatihan asli, sehingga himpunan data **himpunan data diabetes** dari saluran pelatihan disertakan. Namun, data input ini menyertakan label **Diabetes** yang diprediksi model, yang tidak intuitif untuk disertakan dalam data pasien baru yang prediksi diabetesnya belum dibuat.
4. Hapus himpunan data **himpunan data diabetes** dari saluran inferensi dan ganti dengan modul **Masukkan Data Secara Manual** dari bagian **Input dan Output Data**; menghubungkannya ke input **himpunan data** yang sama dari modul **Terapkan Transformasi** sebagai **Input Layanan Web**. Kemudian ubah pengaturan modul **Masukkan Data Secara Manual** untuk menggunakan masukan CSV berikut, yang menyertakan nilai fitur tanpa label untuk tiga pengamatan pasien baru:

```CSV
PatientID,Pregnancies,PlasmaGlucose,DiastolicBloodPressure,TricepsThickness,SerumInsulin,BMI,DiabetesPedigree,Age
1882185,9,104,51,7,24,27.36983156,1.350472047,43
1662484,6,73,61,35,24,18.74367404,1.074147566,75
1228510,4,115,50,29,243,34.69215364,0.741159926,59
```

5. Alur inferensi menyertakan modul **Evaluate Model**, yang tidak berguna saat memprediksi dari data baru, jadi, hapus modul ini.
6. Output dari modul **Score Model** mencakup semua fitur input serta label yang diprediksi dan skor peluang. Untuk membatasi keluaran hanya pada prediksi dan probabilitas, hapus koneksi antara modul **Model Skor** dan **Output Layanan Web**, tambahkan modul **Menjalankan Skrip Python** dari bagian **Bahasa Python**, sambungkan output dari modul **Model Skor** ke input **Dataset1** (paling kiri) dari **Menjalankan Skrip Python**, dan hubungkan output modul **Menjalankan Skrip Python** ke **Output Layanan Web**. Kemudian ubah pengaturan modul **Menjalankan Skrip Python** untuk menggunakan kode berikut (mengganti semua kode yang ada):

```Python
import pandas as pd

def azureml_main(dataframe1 = None, dataframe2 = None):

    scored_results = dataframe1[['PatientID', 'Scored Labels', 'Scored Probabilities']]
    scored_results.rename(columns={'Scored Labels':'DiabetesPrediction',
                                    'Scored Probabilities':'Probability'},
                            inplace=True)
    return scored_results
```
> **Catatan**: Setelah menempelkan kode di modul **Menjalankan Skrip Python**, pastikan kode terlihat mirip dengan kode di atas. Indentasi penting dalam Python dan modul akan gagal jika indentasi tidak disalin dengan benar. 

7. Verifikasi bahwa alur terlihat mirip dengan yang berikut:

    ![Alur Inferensi Visual](images/visual-inference.jpg)

9. Kirimkan alur sebagai eksperimen baru bernama **mslearn-designer-predict-diabetes** di kluster komputasi yang Anda gunakan untuk pelatihan. Tindakan ini mungkin memerlukan waktu beberapa saat!

## <a name="deploy-the-inference-pipeline-as-a-web-service"></a>Terapkan alur inferensi sebagai layanan web

Sekarang Anda memiliki saluran inferensi untuk inferensi waktu nyata, yang dapat Anda terapkan sebagai layanan web untuk digunakan aplikasi klien.

> **Catatan**: Dalam latihan ini, Anda akan menyebarkan layanan web ke Azure Container Instance (ACI). Jenis komputasi ini dibuat secara dinamis, dan berguna untuk pengembangan dan pengujian. Untuk produksi, Anda harus membuat *kluster inferensi*, yang menyediakan kluster Azure Kubernetes Service (AKS) yang memberikan skalabilitas dan keamanan yang lebih baik.

1. Jika saluran inferensi **Prediksi Diabetes** belum selesai berjalan, tunggu sampai selesai. Kemudian visualisasikan output **Himpunan data hasil** dari modul **Menjalankan Skrip Python** untuk melihat label yang diprediksi dan probabilitas untuk tiga pengamatan pasien dalam data input.
2. Di kanan atas, klik **Terapkan**, dan terapkan titik akhir waktu nyata yang baru, menggunakan pengaturan berikut:
    -  **Nama**: designer-predict-diabetes
    -  **Deskripsi:** Prediksi diabetes.
    - **Jenis komputasi**: Azure Container Instance
3. Tunggu hingga layanan web disebarkan - ini bisa memakan waktu beberapa menit. Status penyebaran ditampilkan di kiri atas antarmuka perancang.

## <a name="test-the-web-service"></a>Menguji aplikasi web

Sekarang Anda dapat menguji layanan yang diterapkan dari aplikasi klien - dalam hal ini, Anda akan menggunakan notebook.

1. Pada laman **Titik akhir**, buka titik akhir real time **designer-predict-diabetes**.
2. Saat titik akhir **designer-predict-diabetes** terbuka, pada tab **Konsumsi**, catat nilai **titik akhir REST** dan **Kunci utama**.
3. Dengan laman **Konsumsi** untuk laman layanan **designer-predict-diabetes** terbuka di peramban Anda, buka tab peramban baru dan buka contoh kedua dari studio Azure Machine Learning. Kemudian di tab baru, lihat laman **Notebooks**.
4. Di laman **Notebooks**, di bawah **File saya**, telusuri folder **/users/*nama-pengguna-Anda*/mslearn-dp100** tempat Anda mengkloning repositori notebook, dan buka notebook **Dapatkan Prediksi Perancang**.
5. Saat buku catatan telah dibuka, pastikan bahwa instans komputasi yang Anda buat sebelumnya dipilih dalam kotak **Hitung**, dan statusnya **Berjalan**.
6. Di notebook, ganti tempat penampung **ENDPOINT** dan **PRIMARY_KEY** dengan nilai untuk layanan Anda, yang dapat Anda salin dari tab **Konsumsi** pada laman untuk titik akhir Anda.
7. Jalankan sel kode dan lihat output yang dikembalikan oleh layanan web Anda.

## <a name="clean-up"></a>Pembersihan

Layanan web yang Anda buat dihosting dalam *Azure Container Instance*. Jika tidak berniat untuk bereksperimen dengan ini lebih lanjut, Anda harus menghapus titik akhir untuk menghindari mengumpulkan penggunaan Azure yang tidak perlu. Anda juga harus menghentikan instans komputasi hingga membutuhkannya lagi.

1. Di studio Azure Machine Learning, pada tab **Titik akhir**, pilih titik akhir **designer-predict-diabetes**. Kemudian klik tombol **Hapus** (&#128465;) dan konfirmasi bahwa Anda ingin menghapus titik akhir.
2. Jika Anda sudah selesai bekerja dengan Azure Machine Learning saat ini, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Hentikan** untuk mematikannya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.
