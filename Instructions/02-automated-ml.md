---
lab:
  title: Gunakan Pembelajaran Mesin Otomatis
ms.openlocfilehash: 9836a169752705779f263e7b005baf11e2f7b616
ms.sourcegitcommit: 8601551af6c32a4c75fd9ecffce750583c2ab4b8
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 04/01/2022
ms.locfileid: "145195835"
---
# <a name="use-automated-machine-learning"></a>Gunakan Pembelajaran Mesin Otomatis

Azure Machine Learning mencakup kemampuan *pembelajaran mesin otomatis* yang memanfaatkan skalabilitas komputasi cloud untuk secara otomatis mencoba beberapa teknik prapemrosesan dan algoritme pelatihan model secara paralel untuk menemukan model pembelajaran mesin yang diawasi dengan performa terbaik untuk data Anda.

Dalam latihan ini, Anda akan menggunakan antarmuka visual untuk pembelajaran mesin otomatis di studio Azure Machine Learning

> **Catatan**: Anda juga dapat menggunakan pembelajaran Azure Machine Learning SDK.

## <a name="before-you-start"></a>Sebelum Anda memulai

Jika Anda belum melakukannya, selesaikan latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Azure Machine Learning dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="configure-compute-resources"></a>Mengonfigurasi sumber daya komputasi

Untuk menggunakan pembelajaran mesin otomatis, Anda memerlukan komputasi untuk menjalankan eksperimen pelatihan model.

1. Masuk ke [Azure Machine Learning studio](https://ml.azure.com?azure-portal=true) dengan kredensial Microsoft yang terkait dengan langganan Azure Anda, dan pilih ruang kerja Azure Machine Learning Anda.
2. Di Azure Machine Learning studio, lihat halaman **Komputasi**; dan pada tab **Instans komputasi**, mulai instans komputasi Anda jika belum berjalan. Anda akan menggunakan instans komputasi ini untuk menguji model terlatih Anda.
3. Saat instans komputasi dimulai, alihkan ke tab **kluster Komputasi**, dan tambahkan kluster komputasi baru dengan pengaturan berikut. Anda akan menjalankan eksperimen pembelajaran mesin otomatis di cluster ini untuk memanfaatkan kemampuan mendistribusikan pelatihan yang berjalan di beberapa node komputasi:
    - **Lokasi**: *Lokasi yang sama dengan ruang kerja Anda*
    - **Tingkat Mesin Virtual**: Khusus
    - **Jenis Komputer Virtual**: CPU
    - **Ukuran Komputer Virtual**: Standard_DS11_v2
    - **Nama komputasi**: *masukkan nama unik*
    - **Jumlah minimum node**: 0
    - **Jumlah maksimum node**: 2
    - **Detik menganggur sebelum menurunkan skala**: 120
    - **Aktifkan akses SSH**: Tidak dipilih

## <a name="create-a-dataset"></a>Buat himpunan data

Sekarang setelah Anda memiliki beberapa sumber daya komputasi yang dapat digunakan untuk memproses data, Anda memerlukan cara untuk menyimpan dan menyerap data yang akan diproses.

1. Lihat data yang dipisahkan koma di https://aka.ms/diabetes-data di browser web Anda. Kemudian simpan ini sebagai file lokal bernama **diabetes.csv** (tidak masalah di mana Anda menyimpannya).
2. Di Azure Machine Learning studio, lihat halaman **Himpunan Data**. Himpunan data mewakili file data atau tabel tertentu yang Anda rencanakan untuk dikerjakan di Azure ML.
3. Buat himpunan data baru dari file lokal, menggunakan pengaturan berikut:
    * **Info dasar**:
        * **Nama**: himpunan data diabetes
        * **Jenis himpunan data**: Tabular
        * **Deskripsi**: Data diabetes
    * **Datastore dan pemilihan file**:
        * **Memilih atau membuat datastore**: Datastore yang saat ini dipilih
        * **Pilih file untuk kumpulan data Anda**: Telusuri file **diabetes.csv** yang Anda unduh.
        * **Jalur unggah**: *Biarkan pilihan default-nya*
        * **Lewati validasi data**: Tidak dipilih
    * **Pengaturan dan pratinjau**:
        * **Format file**: Dibatasi
        * **Pemisah**: Koma
        * **Pengodean**: UTF-8
        * **Header kolom**: Hanya file pertama yang memiliki header
        * **Lewati baris**: Tidak ada
    * **Skema**:
        * Sertakan semua kolom selain **Jalur**
        * Meninjau jenis yang terdeteksi secara otomatis
    * **Konfirmasikan detail**:
        * Jangan membuat profil himpunan data setelah pembuatan
4. Setelah himpunan data dibuat, buka dan tampilkan halaman **Jelajahi** untuk melihat sampel data. Data ini mewakili detail dari pasien yang telah diuji diabetes, dan Anda akan menggunakannya untuk melatih model yang memprediksi kemungkinan pasien positif diabetes berdasarkan pengukuran klinis.

    > **Catatan**: Secara opsional, Anda dapat membuat *profil* kumpulan data untuk melihat detail statistik lainnya.

## <a name="run-an-automated-machine-learning-experiment"></a>Menjalankan eksperimen pembelajaran mesin otomatis

Di Azure Machine Learning, operasi yang Anda jalankan disebut *eksperimen*. Ikuti langkah-langkah di bawah ini untuk menjalankan eksperimen yang menggunakan pembelajaran mesin otomatis untuk melatih model klasifikasi yang memprediksi diagnosis diabetes.

1. Di studio Azure Machine Learning, lihat laman **ML Otomatis** (di bawah **Penulis**).
2. Buat ML Otomatis baru yang dijalankan dengan pengaturan berikut:
    - **Pilih himpunan data**:
        - **Himpunan data**: himpunan data diabetes
    - **Konfigurasikan eksekusi**:
        - **Nama eksperimen baru**: mslearn-automl-diabetes
        - **Kolom target**: Diabetes (*ini adalah label yang akan diprediksi oleh model yang akan dilatih)*
        - **Pilih jenis komputasi**: Kluster komputasi
        - **Pilih kluster komputasi Azure ML**: *kluster komputasi yang Anda buat sebelumnya*
    - **Jenis dan pengaturan tugas**:
        - **Jenis tugas**: Klasifikasi
        - Pilih **Lihat pengaturan konfigurasi tambahan** untuk membuka **Konfigurasi tambahan**:
            - **Metrik utama**: Pilih **AUC_Weighted** *(selengkapnya tentang metrik ini nanti!)*
            - **Jelaskan model terbaik**: Dipilih - *opsi ini menyebabkan pembelajaran mesin otomatis untuk menghitung kepentingan fitur untuk model terbaik; memungkinkan untuk menentukan pengaruh setiap fitur pada label yang diprediksi.*
            - **Gunakan semua model yang didukung**: <u>Tidak</u>dipilih - kami akan membatasi eksperimen untuk mencoba beberapa algoritme tertentu.
            - **Model yang diizinkan**: Pilih hanya **LogisticRegression** dan **RandomForest**. Ini akan menjadi satu-satunya algoritma yang dicoba dalam percobaan.
            - **Kriteria keluar**:
                - **Waktu kerja pelatihan (jam)**: 0,5 - *ini menyebabkan eksperimen berakhir setelah maksimal 30 menit.*
                - **Ambang skor metrik**: 0,90 - *ini menyebabkan eksperimen berakhir jika model mencapai metrik AUC berbobot 90% atau lebih tinggi.*
        - Pilih **Lihat pengaturan fitur** untuk membuka **Fiturisasi**:
            - **Aktifkan fiturisasi**: Dipilih - *ini menyebabkan Azure Machine Learning otomatis melakukan praproses fitur sebelum pelatihan.*
    - **Pilih validasi dan jenis pengujian**:
        - **Jenis validasi**: Pembagian validasi kereta
        - **Validasi persentase data**: 30
        - **Menguji himpunan data**: Tidak diperlukan himpunan data pengujian

3. Setelah Anda mengirimkan detail eksekusi ML otomatis, ini akan dimulai secara otomatis. Anda dapat mengamati status proses di panel **Properti**.
4. Saat status eksekusi berubah menjadi *Berjalan*, lihat tab **Model** dan amati karena setiap kemungkinan kombinasi algoritme pelatihan dan langkah-langkah prapemrosesan dicoba dan performa model yang dihasilkan dievaluasi. Halaman akan otomatis di-refresh secara berkala, tetapi Anda juga dapat memilih **&#8635; Refresh**. Mungkin diperlukan waktu sekitar sepuluh menit sebelum model mulai muncul, karena node kluster perlu diinisialisasi dan proses fiturisasi data selesai sebelum pelatihan dapat dimulai. Sekarang mungkin saat yang tepat untuk istirahat!
5. Tunggu hingga eksperimen selesai.

## <a name="review-the-best-model"></a>Meninjau model terbaik

Setelah percobaan selesai; Anda dapat meninjau model berkinerja terbaik yang dihasilkan (perhatikan bahwa dalam kasus ini, kami menggunakan kriteria keluar untuk menghentikan eksperimen - jadi model "terbaik" yang ditemukan oleh eksperimen mungkin bukan model terbaik, hanya model terbaik yang ditemukan dalam batasan waktu dan metrik yang diizinkan untuk latihan ini!).

1. Di tab **Detail** proses pembelajaran mesin otomatis, perhatikan ringkasan model terbaik.
2. Pilih **Nama algoritma** untuk model terbaik guna melihat turunan yang menghasilkannya.

    Model terbaik diidentifikasi berdasarkan metrik evaluasi yang Anda tentukan (*AUC_Weighted*). Untuk menghitung metrik ini, proses pelatihan menggunakan beberapa data untuk melatih model, dan menerapkan teknik yang disebut *validasi silang* untuk menguji model terlatih secara berulang dengan data yang tidak dilatih dan membandingkan nilai yang diprediksi dengan nilai yang diketahui sebenarnya. Dari perbandingan ini, *matriks yang bingung* dengan positif-benar, positif-palsu, negatif-benar, dan negatif-palsu ditabulasi dan metrik klasifikasi tambahan dihitung - termasuk bagan Kurva Operator Penerima (ROC) yang membandingkan Tingkat Benar-Positif dan tingkat Salah-Positif. Area di bawah kurva ini (AUC) adalah metrik umum yang digunakan untuk mengevaluasi kinerja klasifikasi.
3. Di samping nilai *AUC_Weighted*, pilih **Lihat semua metrik lainnya** untuk melihat nilai metrik evaluasi lain yang memungkinkan untuk model klasifikasi.
4. Pilih tab **Metrik** dan tinjau metrik kinerja yang dapat Anda lihat untuk model tersebut. Ini termasuk visualisasi **confusion_matrix** yang menunjukkan matriks kebingungan untuk model yang divalidasi, dan visualisasi **akurasi_tabel** yang menyertakan bagan ROC.
5. Pilih tab **Penjelasan**, pilih **ID Penjelasan**, lalu lihat laman **Kepentingan Agregat**. Ini menunjukkan sejauh mana setiap fitur dalam kumpulan data memengaruhi prediksi label.

## <a name="deploy-a-predictive-service"></a>Menyebarkan layanan prediktif

Setelah menggunakan pembelajaran mesin otomatis untuk melatih beberapa model, Anda dapat menyebarkan model dengan performa terbaik sebagai layanan untuk digunakan aplikasi klien.

> **Catatan**: Di Azure Machine Learning, Anda dapat menyebarkan layanan sebagai Azure Container Instances (ACI) atau ke kluster Azure Kubernetes Service (AKS). Untuk skenario produksi, penyebaran AKS disarankan, yang harus Anda buat target komputasi *kluster inferensinya*. Dalam latihan ini, Anda akan menggunakan layanan ACI, yang merupakan target penyebaran yang sesuai untuk pengujian, dan tidak mengharuskan Anda membuat kluster inferensi.

1. Pilih tab **Detail** untuk eksekusi yang menghasilkan model terbaik.
2. Dari opsi **Sebarkan**, gunakan tombol **Sebarkan ke layanan web** untuk menerapkan model dengan setelan berikut:
    - **Nama**: prediksi otomatis-diabetes
    - **Deskripsi:** Prediksi diabetes
    - **Jenis komputasi**: Azure Container Instance
    - **Aktifkan autentikasi**: Dipilih
    - **Gunakan aset penyebaran khusus**: Tidak dipilih
3. Tunggu penyebaran dimulai - ini mungkin memakan waktu beberapa detik. Kemudian, pada tab **Model**, di bagian **Gambaran Umum model**, amati **Status Penyebaran** untuk layanan **prediksi-otomatis-diabetes**, yang seharusnya **Eksekusi**. Tunggu hingga status ini berubah menjadi **Berhasil**. Anda mungkin perlu memilih **&#8635; Refresh** secara berkala.  **CATATAN** Ini bisa memakan waktu cukup lama - bersabarlah!
4. Di studio Azure Machine Learning, lihat laman **Endpoints** dan pilih **auto-predict-diabetes** titik akhir waktu nyata. Kemudian, pilih tab **Konsumsi** dan perhatikan informasi berikut di sana. Anda memerlukan informasi ini untuk menyambungkan ke layanan yang disebarkan dari aplikasi klien.
    - Titik akhir REST untuk layanan Anda
    - Kunci Primer untuk layanan Anda
5. Perhatikan bahwa Anda dapat menggunakan tautan &#10697; di samping nilai-nilai ini untuk menyalinnya ke clipboard.

## <a name="test-the-deployed-service"></a>Menguji layanan yang disebarkan

Setelah menyebarkan layanan, Anda dapat mengujinya menggunakan beberapa kode sederhana.

1. Dengan laman **Konsumsi** untuk laman layanan **prediksi-otomatis-diabetes** di peramban Anda, buka tab peramban baru dan buka contoh kedua dari studio Azure Machine Learning. Kemudian di tab baru, lihat laman **Notebooks**.
2. Di laman **Notebook**, di bawah **File saya**, ramban ke folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori notebook, dan membuka notebook **Dapatkan Prediksi AutoML**.
3. Saat buku catatan telah dibuka, pastikan bahwa instans komputasi yang Anda buat sebelumnya dipilih dalam kotak **Hitung**, dan statusnya **Berjalan**.
4. Di notebook, ganti tempat penampung **ENDPOINT** dan **PRIMARY_KEY** dengan nilai untuk layanan Anda, yang dapat Anda salin dari tab **Konsumsi** pada laman untuk titik akhir Anda.
5. Jalankan sel kode dan lihat output yang dikembalikan oleh layanan web Anda.

## <a name="clean-up"></a>Pembersihan

Layanan web yang Anda buat dihosting dalam *Azure Container Instance*. Jika tidak berniat untuk bereksperimen dengan ini lebih lanjut, Anda harus menghapus titik akhir untuk menghindari mengumpulkan penggunaan Azure yang tidak perlu. Anda juga harus menghentikan instans komputasi hingga membutuhkannya lagi.

1. Di studio Azure Machine Learning, pada tab **Titik Akhir**, pilih titiik akhir **auto-predict-diabetes**. Lalu, pilih **Hapus** (&#128465;) dan konfirmasikan bahwa Anda ingin menghapus titik akhir.
2. Di halaman **Komputasi**, di tab **Instans Komputasi**, pilih instans komputasi Anda lalu pilih **Hentikan**.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.
