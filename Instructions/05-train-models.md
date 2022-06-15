---
lab:
  title: Latih model
ms.openlocfilehash: dffa9edda34c599dfbd372fe898ddcf955f6f200
ms.sourcegitcommit: 66d8872bc3d24c2121e225be132b56f4df7920ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 02/12/2022
ms.locfileid: "145195808"
---
# <a name="train-models"></a>Model Kereta

Pembelajaran Mesin terutama tentang model pelatihan yang dapat Anda gunakan untuk menyediakan layanan prediktif ke aplikasi. Dalam latihan ini, Anda akan melihat bagaimana Anda bisa menggunakan eksperimen Azure Machine Learning untuk menjalankan skrip pelatihan, dan cara mendaftarkan model terlatih yang dihasilkan.

## <a name="before-you-start"></a>Sebelum kamu memulai

Jika Anda belum melakukannya, selesaikan latihan *[Buat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Pembelajaran Mesin Azure dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan buku catatan, sering kali lebih produktif menggunakan lingkungan pengembangan buku catatan berfitur lengkap seperti *Jupyter*.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru.

> **Tips**: Baru mengenal Python? Gunakan [Lembar contekan Python](cheat-sheets/dp100-cheat-sheet-python.pdf) untuk memahami kodenya. Baru mengenal pembelajaran mesin? Gunakan [ikhtisar pembelajaran mesin](cheat-sheets/dp100-cheat-sheet-machine-learning.pdf) untuk mendapatkan ikhtisar yang disederhanakan dari ikhtisar proses pembelajaran mesin di Azure Machine Learning.

## <a name="train-models-using-the-azure-machine-learning-sdk"></a>Latih model menggunakan Azure Machine Learning SDK

Dalam latihan ini, kode untuk melatih model disediakan dalam buku catatan.

1. Di beranda Jupyter, jelajahi folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori buku catatan, dan buka buku catatan **Model Kereta**.
2. Kemudian baca catatan di buku catatan, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di buku catatan, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada halaman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya. Jika tidak, biarkan berjalan untuk lab berikutnya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.