---
lab:
  title: Buat layanan inferensi batch
ms.openlocfilehash: b1dfd26b9f440e80500dd3753434ac2a11cad947
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 11/17/2021
ms.locfileid: "145195800"
---
# <a name="create-a-batch-inferencing-service"></a>Buat Layanan Inferensi Batch

Dalam banyak skenario, inferensi dilakukan sebagai proses batch yang menggunakan model prediktif untuk mencetak sejumlah besar kasus. Untuk menerapkan solusi inferensi semacam ini di Azure Machine Learning, Anda bisa membuat saluran inferensi batch.

## <a name="before-you-start"></a>Sebelum Memulai

Jika Anda belum melakukannya, selesaikan latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Azure Machine Learning dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan notebook, sering kali lebih produktif menggunakan lingkungan pengembangan notebook berfitur lengkap seperti *Jupyter*.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru.

## <a name="create-a-batch-inferencing-service"></a>Buat layanan inferensi batch

Dalam latihan ini, kode untuk menyebarkan model sebagai layanan inferensi batch disediakan di notebook.

1. Di beranda Jupyter, telusuri ke folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori notebook, dan buka **Buat Batch Notebook Layanan Inferensi**.
2. Kemudian baca catatan di notebook, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di notebook, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada laman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya. Jika tidak, biarkan berjalan untuk lab berikutnya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.