---
lab:
  title: Membuat ruang kerja Azure Machine Learning
ms.openlocfilehash: c2f33973281221da1a4871f19fbaff8f127d028f
ms.sourcegitcommit: 8601551af6c32a4c75fd9ecffce750583c2ab4b8
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 04/01/2022
ms.locfileid: "145195829"
---
# <a name="create-and-explore-an-azure-machine-learning-workspace"></a>Buat dan Jelajahi Ruang Kerja Azure Machine Learning

Dalam latihan ini, Anda akan membuat dan menjelajahi ruang kerja Azure Machine Learning.

## <a name="create-an-azure-machine-learning-workspace"></a>Membuat ruang kerja Azure Machine Learning

Seperti namanya, ruang kerja adalah tempat terpusat untuk mengelola semua aset Azure ML yang Anda perlukan untuk mengerjakan proyek pembelajaran mesin.

1. Di [Portal Microsoft Azure](https://portal.azure.com), buat sumber daya **Machine Learning** baru, dengan menetapkan pengaturan berikut:

    - **Langganan**: *Langganan Azure Anda*
    - **Grup Sumber Daya**: *Buat atau pilih grup sumber daya*
    - **Nama ruang kerja**: *Masukkan nama unik untuk ruang kerja Anda*
    - **Wilayah**: *Pilih wilayah geografis yang paling dekat dengan Anda*
    - **Akun penyimpanan**: *Perhatikan akun penyimpanan baru default yang akan dibuat untuk ruang kerja Anda*
    - **Brankas kunci**: *Perhatikan brankas kunci baru default yang akan dibuat untuk ruang kerja Anda*
    - **Wawasan aplikasi**: *Perhatikan sumber daya wawasan aplikasi baru default yang akan dibuat untuk ruang kerja Anda*
    - **Registri kontainer**: Tidak ada (*satu registri kontainer akan dibuat secara otomatis saat pertama kali Anda menyebarkan model ke kontainer*)

    > **Catatan**: Saat membuat ruang kerja Azure Machine Learning, Anda dapat menggunakan beberapa opsi lanjutan untuk membatasi akses melalui *titik akhir privat* dan menentukan kunci khusus untuk enkripsi data. Kami tidak akan menggunakan opsi ini dalam latihan ini - tetapi Anda harus mengetahuinya!

2. Saat ruang kerja dan sumber daya terkait telah dibuat, lihat ruang kerja di portal.

## <a name="explore-azure-machine-learning-studio"></a>Jelajahi studio Azure Machine Learning

Anda dapat mengelola beberapa aset ruang kerja di portal Azure, tetapi untuk ilmuwan data, alat ini berisi banyak informasi dan tautan yang tidak relevan yang terkait dengan pengelolaan sumber daya Azure umum. *Azure Machine Learning studio* menyediakan portal web khusus untuk bekerja dengan ruang kerja Anda.

1. Di panel portal Azure untuk ruang kerja Pembelajaran Mesin Azure Anda, klik tautan untuk meluncurkan studio; atau sebagai alternatif, di tab peramban baru, buka [https://ml.azure.com](https://ml.azure.com). Jika diminta, masuk menggunakan akun Microsoft yang Anda gunakan di tugas sebelumnya dan pilih langganan dan ruang kerja Azure Anda.

    > **Kiat** Jika Anda memiliki beberapa langganan Azure, Anda harus memilih *direktori* Azure tempat langganan ditetapkan; lalu pilih langganan, dan terakhir pilih ruang kerja.

2. Lihat antarmuka studio Azure Machine Learning untuk ruang kerja Anda - Anda dapat mengelola semua aset di ruang kerja Anda dari sini.
3. Di studio Azure Machine Learning aktifkan &#9776; ikon di kiri atas untuk menampilkan dan menyembunyikan berbagai halaman di antarmuka. Anda dapat menggunakan halaman ini untuk mengelola sumber daya di ruang kerja.

## <a name="create-a-compute-instance"></a>Buat instans komputasi

Salah satu manfaat Azure Machine Learning adalah kemampuan untuk membuat komputasi berbasis cloud tempat Anda dapat menjalankan eksperimen dan skrip pelatihan dalam skala besar.

1. Di studio Azure Machine Learning, lihat laman **Komputasi**. Di sinilah Anda akan mengelola sumber daya komputasi untuk aktivitas ilmu data Anda. Ada empat jenis sumber daya komputasi yang dapat dibuat:
    - **Instans Komputasi**: Stasiun kerja pengembangan yang dapat digunakan ilmuwan data untuk bekerja dengan data dan model.
    - **Kluster komputasi**: Kluster mesin virtual scalable untuk pemrosesan kode eksperimen sesuai permintaan.
    - **Kluster inferensi**: Target penyebaran untuk layanan prediktif yang menggunakan model terlatih Anda.
    - **Komputasi terlampir**: Tautan ke sumber daya komputasi Azure lainnya, seperti Mesin Virtual atau kluster Azure Databricks.

    Untuk latihan ini, Anda akan membuat instans komputasi sehingga Anda dapat menjalankan beberapa kode di ruang kerja Anda.

2. Pada tab **Instans komputasi**, tambahkan instans komputasi baru dengan pengaturan berikut. Anda akan menggunakan ini sebagai ruang kerja untuk menjalankan kode di notebook.
    - **Nama komputasi**: *masukkan nama unik*
    - **Lokasi**: *Lokasi yang sama dengan ruang kerja Anda*
    - **Jenis mesin virtual**: CPU
    - **Ukuran mesin virtual**: Standard_DS11_v2
    - **Total Kuota yang Tersedia**: Ini menunjukkan inti khusus yang tersedia.
    - **Tampilkan pengaturan lanjutan**: Perhatikan pengaturan berikut, tetapi jangan pilih: 
        - **Aktifkan akses SSH**: Tidak dipilih *(Anda dapat menggunakan ini untuk mengaktifkan akses langsung ke mesin virtual menggunakan klien SSH)*
        - **Aktifkan jaringan virtual**: Tidak dipilih *(Anda biasanya akan menggunakan ini di lingkungan perusahaan untuk meningkatkan keamanan jaringan)*
        - **Tetapkan ke pengguna lain**: Tidak dipilih *(Anda dapat menggunakan ini untuk menetapkan instans komputasi ke ilmuwan data)* 3.Tunggu hingga instans komputasi dimulai dan statusnya berubah menjadi **Berjalan**.

> **Catatan**: Instans dan kluster komputasi didasarkan pada gambar komputer virtual Azure standar. Untuk latihan ini, gambar *Standar_DS11_v2* disarankan untuk mencapai keseimbangan optimal antara saldo dan performa. Jika langganan Anda memiliki kuota yang tidak menyertakan gambar ini, pilih gambar alternatif; tetapi perlu diingat bahwa gambar yang lebih besar dapat dikenakan biaya yang lebih tinggi dan gambar yang lebih kecil mungkin tidak cukup untuk menyelesaikan tugas. Atau, minta administrator Azure Anda memperpanjang kuota Anda.

## <a name="clone-and-run-a-notebook"></a>Mengkloning dan menjalankan notebook

Banyak eksperimen ilmu data dan pembelajaran mesin dilakukan dengan menjalankan kode di *notebook*. Instans komputasi Anda menyertakan lingkungan notebook Python berfitur lengkap (*Jupyter* dan *JuypyterLab*) yang dapat Anda gunakan untuk pekerjaan ekstensif; tetapi untuk pengeditan notebook dasar, Anda dapat menggunakan halaman **Notebook** bawaan di studio Azure Machine learning.

1. Di studio Azure Machine Learning, lihat laman **Notebook**.
2. Jika pesan yang menjelaskan fitur baru ditampilkan, tutup.
3. Pilih **Terminal** atau ikon **Buka terminal** untuk membuka terminal, dan pastikan **Komputasi**-nya disetel ke instans komputasi Anda dan jalur saat ini adalah **/users/your-user-name**.
4. Masukkan perintah berikut untuk mengkloning repositori Git yang berisi notebook, data, dan file lain ke ruang kerja Anda:

    ```bash
    git clone https://github.com/MicrosoftLearning/mslearn-dp100 mslearn-dp100
    ```

4. Setelah perintah selesai, di panel **File**, klik **&#8635;** untuk menyegarkan tampilan dan memverifikasi bahwa **/users/*your-user-name*/mslearn-dp100** telah dibuat. Folder ini berisi beberapa file notebook **.ipynb**.
5. Tutup panel terminal, hentikan sesi.
6. Dalam folder **/users/*your-user-name*/mslearn-dp100**, buka buku catatan **Memulai Notebook**. Kemudian baca catatan dan ikuti instruksi yang ada di dalamnya.

> **Tips:** Untuk menjalankan sel kode, pilih sel yang ingin Anda jalankan, lalu gunakan tombol **&#9655;** untuk menjalankannya. 

> **Baru menggunakan Python?** Gunakan [referensi cepat Python](cheat-sheets/dp100-cheat-sheet-python.pdf) untuk memahami kode.

> **Baru menggunakan pembelajaran mesin?** Gunakan [gambaran umum pembelajaran mesin](cheat-sheets/dp100-cheat-sheet-machine-learning.pdf) untuk mendapatkan gambaran umum yang disederhanakan tentang proses pembelajaran mesin di Azure Machine Learning.

## <a name="stop-your-compute-instance"></a>Hentikan instans komputasi Anda

Jika Anda telah selesai menjelajahi Azure Machine Learning untuk saat ini, Anda harus mematikan instans komputasi untuk menghindari dikenakan biaya yang tidak perlu di langganan Azure Anda.

1. Di Studio Azure Machine Learning, pada halaman **Komputasi**, pilih instans komputasi Anda.
2. Klik **Hentikan** untuk menghentikan instans komputasi Anda. Saat dimatikan, statusnya akan berubah menjadi **Berhenti**.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam rangkaian ini, Anda harus mengulangi lab ini untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.
