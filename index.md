---
title: Petunjuk Host Online
permalink: index.html
layout: home
ms.openlocfilehash: a2eb157b1d188655f4cfbcc575befec4a2e9c623
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 11/17/2021
ms.locfileid: "145195828"
---
# <a name="azure-machine-learning-exercises"></a>Latihan Pembelajaran Azure Machine Learning

Repositori ini berisi latihan lab langsung untuk kursus Microsoft [DP-100 *Merancang dan Menerapkan Solusi Ilmu Data di Azure*](https://docs.microsoft.com/learn/certifications/courses/dp-100t01) dan [modul mandiri yang setara di Microsoft Learn](https://docs.microsoft.com/learn/paths/build-ai-solutions-with-azure-ml-service/). Latihan ini didesain untuk melengkapi materi pembelajaran dan memungkinkan Anda mempraktikkan teknologi yang dijelaskan.

Untuk menyelesaikan latihan ini, Anda memerlukan langganan Microsoft Azure. Jika instruktur Anda belum menyediakannya, Anda dapat mendaftar untuk coba gratis di [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Latihan |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
