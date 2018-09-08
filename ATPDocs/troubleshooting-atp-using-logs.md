---
title: Rozwiązywanie problemów z usługi Azure Advanced Threat Protection przy użyciu dzienników | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak dzienniki usługi Azure ATP można użyć do rozwiązywania problemów
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: fee526b836b9fbbf28624bdce4354267ab968cd6
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166092"
---
*Dotyczy: Zaawansowana ochrona przed zagrożeniami*



# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Rozwiązywanie problemów z usługi Azure Advanced Threat Protection (ATP) dzienniki czujnika przy użyciu zaawansowanej ochrony przed zagrożeniami
Dzienniki zaawansowanej ochrony przed zagrożeniami zapewniają wgląd w poszczególnych składników usługi Azure ATP czujnik czynności w dowolnym danym momencie w czasie.


Dzienniki usługi Azure ATP znajdują się w podfolderze o nazwie **dzienniki** gdzie zaawansowanej ochrony przed zagrożeniami jest zainstalowany; domyślna lokalizacja to: **C:\Program Files\Azure Advanced Threat ochrony czujnika\\**. W domyślnej lokalizacji instalacji można znaleźć w: **number\Logs C:\Program Files\Azure Advanced Threat Protection Sensor\version**.

Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure ma następujące dzienniki:

-   **Microsoft.Tri.Sensor.log** — ten dziennik zawiera wszystko, co się dzieje w czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure (w tym rozwiązania i błędów). Służy on głównie do uzyskiwania informacji o ogólnym stanie wszystkich operacji w kolejności chronologicznej, w której miały miejsce.

-   **Microsoft.Tri.Sensor-Resolution.log** — ten dziennik zawiera szczegóły rozwiązań jednostek widocznych w ruchu czujnika zaawansowanej ochrony przed zagrożeniami. Służy on głównie do badania problemów dotyczących rozwiązań jednostek.

-   **Microsoft.Tri.Sensor-Errors.log** — ten dziennik zawiera tylko błędy wykryte przez czujnika zaawansowanej ochrony przed zagrożeniami. Służy on głównie do przeprowadzania kontroli kondycji i badania problemów, które muszą zostać skorelowane z określonymi godzinami.

-   **Microsoft.Tri.Sensor.Updater.log** — ten dziennik jest używany dla procesu aktualizacji czujnika, który jest odpowiedzialny za aktualizowanie czujnika zaawansowanej ochrony przed zagrożeniami, jeśli skonfigurowane do automatycznego. 


> [!NOTE]
> Maksymalny rozmiar pierwszych trzech plików dziennika wynosi 50 MB. Po osiągnięciu tego rozmiaru tworzony jest nowy plik, a nazwa poprzedniego jest zmieniana zgodnie ze wzorcem „&lt;oryginalna nazwa pliku&gt;-Archived-00000”, gdzie numer jest zwiększany po każdej zmianie nazwy. Domyślnie, jeśli istnieje więcej niż 10 plików tego samego typu, najstarsze są usuwane.

## <a name="azure-atp-deployment-logs"></a>Dzienniki wdrażania zaawansowanej ochrony przed zagrożeniami na platformie Azure
Dzienniki wdrożenia usługi Azure ATP znajdują się w katalogu tymczasowym użytkownika, który zainstalował produkt. W domyślnej lokalizacji instalacji można je znaleźć w folderze: **C:\Users\Administrator\AppData\Local\Temp** (lub w katalogu nadrzędnym folderu %temp%).

Usługa Azure dzienniki wdrożenia czujnika zaawansowanej ochrony przed zagrożeniami:

-   **Azure Sensor_YYYYMMDDHHMMSS.log ochrony przed zagrożeniami zaawansowane** — ten dziennik zawiera listę czynności w procesie wdrożenia czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Głównie jest do śledzenia procesu wdrażania czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.

-   **Azure Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log ochrony przed zagrożeniami zaawansowane** — ten plik dziennika zawiera listę czynności w procesie wdrożenia plików binarnych czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Głównie służy do śledzenia wdrożenia plików binarnych czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.


> [!NOTE] 
> Oprócz dzienników wdrażania wspomnianych tutaj istnieją inne dzienniki zaczynające się od "Azure Advanced Threat Protection" które także mogą zawierać dodatkowe informacje na temat procesu wdrażania.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)