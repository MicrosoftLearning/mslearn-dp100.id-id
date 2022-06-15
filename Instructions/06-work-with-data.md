---
lab:
  title: Bekerja dengan data
ms.openlocfilehash: 6db1dd05ed150a1428ee355c932edc1082c1e3ba
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 11/17/2021
ms.locfileid: "145195814"
---
# <a name="work-with-data"></a>Bekerja dengan Data

Meskipun cukup umum untuk bekerja dengan data pada sistem file lokal mereka, dalam lingkungan perusahaan, menyimpan data di lokasi pusat tempat beberapa ilmuwan data dan insinyur pembelajaran mesin dapat mengaksesnya dapat menjadi lebih efektif.

Dalam latihan ini, Anda akan menjelajahi *penyimpanan data* dan *kumpulan data*, yang merupakan objek utama yang digunakan untuk mengabstraksi akses data di Azure Machine Learning.

## <a name="before-you-start"></a>Sebelum kamu memulai

Jika Anda belum melakukannya, selesaikan latihan *[Buat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja Pembelajaran Mesin Azure dan instans komputasi, dan klon buku catatan yang diperlukan untuk latihan ini.

## <a name="open-jupyter"></a>Buka Jupyter

Meskipun Anda dapat menggunakan halaman **Notebook** di studio Azure Machine Learning untuk menjalankan buku catatan, sering kali lebih produktif menggunakan lingkungan pengembangan buku catatan berfitur lengkap seperti *Jupyter*.

1. Di [Azure Machine Learning studio](https://ml.azure.com), lihat halaman **Komputasi** untuk ruang kerja Anda; dan pada tab **Instans Komputasi**, mulai instans komputasi Anda jika belum berjalan.
2. Saat instans komputasi sedang berjalan, klik tautan **Jupyter** untuk membuka beranda Jupyter di tab browser baru.

## <a name="work-with-datastores-and-datasets"></a>Bekerja dengan penyimpanan data dan kumpulan data

Dalam latihan ini, kode untuk bekerja dengan data disediakan dalam buku catatan.

1. Di beranda Jupyter, jelajahi folder **/users/*your-user-name*/mslearn-dp100** tempat Anda mengkloning repositori buku catatan, dan buka buku catatan **Bekerja dengan Data** .
2. Kemudian baca catatan di buku catatan, jalankan setiap sel kode secara bergantian.
3. Setelah Anda selesai menjalankan kode di buku catatan, pada menu **File**, klik **Tutup dan Hentikan** untuk menutupnya dan mematikan kernel Python-nya. Kemudian tutup semua tab browser Jupyter.

## <a name="clean-up"></a>Pembersihan

Jika Anda sudah selesai bekerja dengan Azure Machine Learning untuk saat ini, di studio Azure Machine Learning, pada halaman **Komputasi**, pada tab **Instans Komputasi**, pilih instans komputasi Anda dan klik **Berhenti** untuk mematikannya. Jika tidak, biarkan berjalan untuk lab berikutnya.

> **Catatan**: Menghentikan komputasi memastikan langganan Anda tidak akan ditagih untuk sumber daya komputasi. Namun Anda akan dikenakan biaya kecil untuk penyimpanan data selama ruang kerja Azure Machine Learning ada di langganan Anda. Jika telah selesai menjelajahi Azure Machine Learning, Anda dapat menghapus ruang kerja Azure Machine Learning dan sumber daya terkait. Namun, jika Anda berencana untuk menyelesaikan lab lain dalam seri ini, Anda harus mengulangi latihan *[Membuat Ruang Kerja Azure Machine Learning](01-create-a-workspace.md)* untuk membuat ruang kerja dan menyiapkan lingkungan terlebih dahulu.