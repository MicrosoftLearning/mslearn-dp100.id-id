---
lab:
  title: Sesuaikan hyperparameter
ms.openlocfilehash: aea02dc80dd1ecec50d45b74078ff569217e0942
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 11/17/2021
ms.locfileid: "145195836"
---
# <a name="tune-hyperparameters"></a>Tune Hyperparameters

Hyperparameter adalah variabel yang memengaruhi bagaimana model dilatih, tetapi tidak dapat diturunkan dari data pelatihan. Memilih nilai hyperparameter yang optimal untuk pelatihan model bisa jadi sulit, dan biasanya melibatkan banyak percobaan dan kesalahan.

Dalam latihan ini, Anda akan menggunakan Azure Machine Learning untuk mengatur hyperparameter dengan melakukan beberapa latihan secara paralel.

## <a name="before-you-start"></a>Sebelum Memulai

Jika Anda belum melakukannya, selesaikan latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Azure Machine Learning dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan notebook, sering kali lebih produktif menggunakan lingkungan pengembangan notebook berfitur lengkap seperti *Jupyter*.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru.

## <a name="run-a-hyperparameter-tuning-experiment"></a>Jalankan eksperimen penyetelan hyperparameter

Dalam latihan ini, kode untuk menjalankan eksperimen penyetelan hyperparameter disediakan di notebook.

1. Di beranda Jupyter, telusuri folder **/users/*your-user-name*/mslearn-dp100** di mana Anda mengkloning repositori notebook, dan buka **Tune Hyperparameters** notebook.
2. Kemudian baca catatan di notebook, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di notebook, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada laman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya. Jika tidak, biarkan berjalan untuk lab berikutnya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.