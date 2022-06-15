---
lab:
  title: Memantau penyimpangan data
ms.openlocfilehash: 92bff45e94e3b96f9ef7d457601807c1cc759746
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 11/17/2021
ms.locfileid: "145195812"
---
# <a name="monitor-data-drift"></a>Memantau Data Drift

Mengubah tren data dari waktu ke waktu dapat mengurangi keakuratan prediksi yang dibuat oleh model. Memantau *pergeseran data* ini dan pelatihan ulang seperlunya adalah cara penting untuk memastikan solusi mpembelajaran mesin Anda terus memprediksi secara akurat.

## <a name="before-you-start"></a>Sebelum kamu memulai

Jika Anda belum melakukannya, selesaikan latihan *[Buat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Pembelajaran Mesin Azure dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan buku catatan, sering kali lebih produktif menggunakan lingkungan pengembangan buku catatan berfitur lengkap seperti *Jupyter*.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru.

## <a name="monitor-data-drift-for-a-dataset"></a>Memantau penyimpangan data untuk kumpulan data

Pada latihan ini, kode untuk memonitor data drift disediakan dalam sebuah buku catatan.

1. Di beranda Jupyter, jelajahi folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori buku catatan, dan buka **Monitor Data Drift**  buku catatan.
2. Kemudian baca catatan di buku catatan, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di buku catatan, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada halaman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.