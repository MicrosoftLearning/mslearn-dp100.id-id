---
lab:
  title: Membuat alur
ms.openlocfilehash: d76c9c66876fcb03aa02d48ee47ae92e327dd8c9
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 11/17/2021
ms.locfileid: "145195809"
---
# <a name="create-a-pipeline"></a>Membuat Alur

Anda dapat menggunakan Azure Machine Learning SDK untuk melakukan semua tugas yang diperlukan untuk membuat dan mengoperasikan solusi pembelajaran mesin di Azure. Daripada melakukan tugas ini satu per satu, Anda dapat menggunakan *alur* untuk mengatur langkah-langkah yang diperlukan untuk menyiapkan data, menjalankan skrip pelatihan, mendaftarkan model, dan tugas lainnya.

## <a name="before-you-start"></a>Sebelum kamu memulai

Jika Anda belum melakukannya, selesaikan latihan *[Buat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Pembelajaran Mesin Azure dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan buku catatan, sering kali lebih produktif menggunakan lingkungan pengembangan buku catatan berfitur lengkap seperti *Jupyter*.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru.

## <a name="create-and-publish-a-pipeline"></a>Buat dan publikasikan alur

Dalam latihan ini, kode untuk membuat dan memublikasikan alur disediakan di buku catatan.

1. Di beranda Jupyter, jelajahi folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori buku catatan, dan buka buku catatan **Buat Alur** .
2. Kemudian baca catatan di buku catatan, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di buku catatan, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada halaman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya. Jika tidak, biarkan berjalan untuk lab berikutnya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.