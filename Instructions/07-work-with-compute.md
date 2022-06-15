---
lab:
  title: Bekerja dengan komputasi
ms.openlocfilehash: 7f20c3ac54bd6dd770c9874cf4e9f9f96d5924f0
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 11/17/2021
ms.locfileid: "145195827"
---
# <a name="work-with-compute"></a>Bekerja dengan Komputasi

Semua kode Python berjalan dalam konteks lingkungan, yang menentukan paket Python yang tersedia. Kode dapat dijalankan di lingkungan di stasiun kerja lokal Anda, atau di beberapa target komputasi lainnya; seperti cluster untuk meningkatkan skalabilitas.

Dalam latihan ini, Anda akan menjelajahi *lingkungan* dan *mengkomputasi target*, yang dapat Anda gunakan untuk menjalankan eksperimen di Azure Machine Learning.

## <a name="before-you-start"></a>Sebelum Memulai

Jika Anda belum melakukannya, selesaikan latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Azure Machine Learning dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan notebook, sering kali lebih produktif menggunakan lingkungan pengembangan notebook berfitur lengkap seperti *Jupyter*.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru.

## <a name="work-with-environments-and-compute-targets"></a>Bekerja dengan lingkungan dan komputasi target

Dalam latihan ini, kode untuk bekerja dengan komputasi disediakan di notebook.

1. Di beranda Jupyter, telusuri ke folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori notebook, dan buka **Work with Compute**  notebook.
2. Kemudian baca catatan di notebook, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di notebook, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada laman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya. Jika tidak, biarkan berjalan untuk lab berikutnya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.