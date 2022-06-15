---
lab:
  title: Menjalankan eksperimen
ms.openlocfilehash: 62b6b79c99142d4311c2d9c0db4b02cfd710feb6
ms.sourcegitcommit: 66d8872bc3d24c2121e225be132b56f4df7920ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 02/12/2022
ms.locfileid: "145195822"
---
# <a name="run-experiments"></a>Menjalankan Eksperimen

Eksperimen adalah inti dari pekerjaan ilmuwan data. Dalam Pembelajaran Mesin Azure, *eksperimen* digunakan untuk menjalankan skrip atau saluran, dan biasanya menghasilkan metrik keluaran dan catatan. Dalam latihan ini, Anda akan menggunakan Azure Machine Learning SDK untuk menjalankan kode Python sebagai eksperimen.

## <a name="before-you-start"></a>Sebelum kamu memulai

Jika Anda belum melakukannya, selesaikan latihan *[Buat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Pembelajaran Mesin Azure dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan buku catatan, sering kali lebih produktif menggunakan lingkungan pengembangan buku catatan berfitur lengkap seperti *Jupyter*. Untungnya, instans komputasi Azure Machine Learning Anda menyertakan instalasi Jupyter.

> **Tips**: Jupyter Notebook adalah alat open source yang umum digunakan untuk ilmu data. Anda dapat merujuk ke [dokumentasi](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html) jika Anda tidak terbiasa dengannya.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru. Pastikan untuk membuka *Jupyter* dan bukan *JupyterLab*.

> **Tips**: Baru mengenal Python? Gunakan [Lembar contekan Python](cheat-sheets/dp100-cheat-sheet-python.pdf) untuk memahami kodenya.

## <a name="verify-the-azure-machine-learning-sdk-is-installed"></a>Verifikasi bahwa Azure Machine Learning SDK telah diinstal

SDK Pembelajaran Mesin Azure diinstal secara default pada instans komputasi Anda. Ikuti langkah-langkah ini untuk memverifikasi penginstalan.

1. Di lingkungan buku catatan Jupyter, buat **Terminal** baru. Ini akan membuka tab baru dengan shell perintah.
2. Masukkan perintah berikut untuk memverifikasi bahwa Azure ML SDK telah diinstal:

    ```bash
    pip show azureml-sdk
    ```

    Perhatikan versi paket SDK yang diinstal.

3. Paket SDK **azureml-sdk** menyediakan pustaka terpenting yang diperlukan untuk bekerja dengan Pembelajaran Mesin Azure> Namun, ada beberapa paket tambahan yang berisi pustaka berguna lainnya yang tidak disertakan dalam paket SDK utama. Gunakan perintah berikut untuk memverifikasi bahwa paket **azureml-widgets**, yang berisi pustaka untuk menampilkan informasi Pembelajaran Mesin Azure di buku catatan, juga diinstal:

    ```bash
    pip show azureml-widgets
    ```

4. Tutup tab **Terminal** dan kembali ke tab yang berisi beranda Jupyter.

> **Informasi Lebih Lanjut**: Untuk detail selengkapnya tentang menginstal Azure ML SDK dan komponen opsionalnya, lihat [Dokumentasi Azure ML SDK](https://docs.microsoft.com/python/api/overview/azure/ml/install?view=azure-ml-py).

## <a name="run-experiments-in-a-notebook"></a>Jalankan eksperimen di buku catatan

Eksperimen dalam Pembelajaran Mesin Azure perlu dimulai dari semacam lapisan *kontrol*; sering berupa skrip atau program. Dalam latihan ini, Anda akan menggunakan buku catatan untuk mengontrol eksperimen.

1. Di beranda Jupyter, jelajahi folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori buku catatan, dan buka buku catatan **Jalankan Eksperimen**.
2. Kemudian baca catatan di buku catatan, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di buku catatan, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada halaman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya. Jika tidak, biarkan berjalan untuk lab berikutnya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.