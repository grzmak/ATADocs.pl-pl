---
title: "Rozwiązywanie problemów z usługą ATA przy użyciu dzienników usługi ATA | Microsoft ATA"
description: "Opis sposobu rozwiązywania problemów przy użyciu dzienników usługi ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c71d5ed1c705de558f1144820703ffe84850679b
ms.openlocfilehash: f8024edbfad1961db7fa469cc2907c55bb5ec93f


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Rozwiązywanie problemów z usługą ATA przy użyciu dzienników usługi ATA
Dzienniki usługi ATA zapewniają wgląd w działania wykonywane przez poszczególne składniki usługi ATA w dowolnym momencie.

## Dzienniki bramy usługi ATA
W tej sekcji każde odwołanie do bramy usługi ATA dotyczy także bramy ATA Lightweight Gateway. 

Dzienniki bramy usługi ATA znajdują się w podfolderze o nazwie **Logs** w folderze instalacji usługi ATA. Domyślna lokalizacja to: **C:\Program Files\Microsoft Advanced Threat Analytics\**. W domyślnej lokalizacji instalacji można je znaleźć w folderze **C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**.

Brama usługi ATA ma następujące dzienniki:

-   **Microsoft.Tri.Gateway.log** — ten dziennik zawiera informacje o wszystkich zdarzeniach w bramie usługi ATA (w tym o rozwiązaniach i błędach). Służy on głównie do uzyskiwania informacji o ogólnym stanie wszystkich operacji w kolejności chronologicznej, w której miały miejsce.

-   **Microsoft.Tri.Gateway-Resolution.log** — ten dziennik zawiera szczegóły rozwiązań jednostek widocznych w ruchu dla bramy usługi ATA. Służy on głównie do badania problemów dotyczących rozwiązań jednostek.

-   **Microsoft.Tri.Gateway-Errors.log** — ten dziennik zawiera tylko błędy wykryte przez bramę usługi ATA. Służy on głównie do przeprowadzania kontroli kondycji i badania problemów, które muszą zostać skorelowane z określonymi godzinami.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** — w tym dzienniku grupowane i zliczane są wszystkie błędy i wyjątki.
    Po każdym uruchomieniu bramy usługi ATA tworzony jest pusty plik, który jest następnie aktualizowany co minutę. Służy on głównie do uzyskiwania informacji o nowych błędach lub problemach dotyczących bramy usługi ATA (pogrupowane błędy jest łatwiej odczytywać i szybko sprawdzać, czy wystąpiły nowe problemy).
-   **Microsoft.Tri.Gateway.Updater.log** — ten dziennik jest używany w procesie aktualizatora bramy, który jest odpowiedzialny za aktualizowanie bramy, jeśli został skonfigurowany do automatycznego działania. W przypadku bramy ATA Lightweight Gateway proces aktualizatora bramy jest również odpowiedzialny za ograniczenia zasobów bramy ATA Lightweight Gateway.
-   **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** — w tym dzienniku grupowane i zliczane są wszystkie podobne błędy i wyjątki. Po każdym uruchomieniu aktualizatora usługi ATA tworzony jest pusty plik, który jest następnie co minutę aktualizowany. Umożliwia zorientowanie się, czy wystąpiły nowe błędy lub problemy związane z aktualizatorem usługi ATA. Błędy są grupowane w celu ułatwienia szybkiego rozpoznania wykrycia nowych błędów lub problemów.

> [!NOTE]
> Maksymalny rozmiar pierwszych trzech plików dziennika wynosi 50 MB. Po osiągnięciu tego rozmiaru tworzony jest nowy plik, a nazwa poprzedniego jest zmieniana zgodnie ze wzorcem „&lt;oryginalna nazwa pliku&gt;-Archived-00000”, gdzie numer jest zwiększany po każdej zmianie nazwy. Domyślnie, jeśli istnieje więcej niż 10 plików tego samego typu, najstarsze są usuwane.

## Dzienniki centrum usługi ATA
Dzienniki centrum usługi ATA znajdują się w podfolderze o nazwie **Logs**. W domyślnej lokalizacji instalacji można je znaleźć w folderze: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**.
> [!Note]
> Dzienniki konsoli ATA, które były wcześniej dziennikami usług IIS, teraz znajdują się w obszarze dzienników centrum usługi ATA.

Centrum usługi ATA ma następujące dzienniki:

-   **Microsoft.Tri.Center.log** — ten dziennik zawiera informacje o wszystkich zdarzeniach w centrum usługi ATA, w tym o wykrytych zdarzeniach i błędach. Służy on głównie do uzyskiwania informacji o ogólnym stanie wszystkich operacji w kolejności chronologicznej, w której miały miejsce.

-   **Microsoft.Tri.Center-Detection.log** — ten dziennik zawiera tylko szczegóły wykrytych zdarzeń centrum usługi ATA. Służy on głównie do badania problemów dotyczących wykrywania.

-   **Microsoft.Tri.Center-Errors.log** — ten dziennik zawiera tylko błędy wykryte przez centrum usługi ATA. Służy on głównie do przeprowadzania kontroli kondycji i badania problemów, które muszą zostać skorelowane z określonymi godzinami.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** — w tym dzienniku grupowane i zliczane są wszystkie błędy i wyjątki.
    Po każdym uruchomieniu centrum usługi ATA tworzony jest pusty plik, który jest następnie aktualizowany co minutę. Służy on głównie do rozpoznania, czy wystąpiły nowe błędy lub problemy dotyczące centrum usługi ATA — pogrupowane błędy można łatwiej odczytać i szybciej zorientować się, czy pojawiły się nowe błędy lub problemy.

> [!NOTE]
> Maksymalny rozmiar pierwszych trzech plików dziennika wynosi 50 MB. Po osiągnięciu tego rozmiaru tworzony jest nowy plik, a nazwa poprzedniego jest zmieniana zgodnie ze wzorcem „&lt;oryginalna nazwa pliku&gt;-Archived-00000”, gdzie numer jest zwiększany po każdej zmianie nazwy. Domyślnie, jeśli istnieje więcej niż 10 plików tego samego typu, najstarsze są usuwane.


## Dzienniki wdrożenia usługi ATA
Dzienniki wdrożenia usługi ATA znajdują się w katalogu tymczasowym użytkownika, który zainstalował produkt. W domyślnej lokalizacji instalacji można je znaleźć w folderze: **C:\Users\Administrator\AppData\Local\Temp** (lub w katalogu nadrzędnym folderu %temp%).

Dzienniki wdrożenia centrum usługi ATA:

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDGGMMSS.log** — ten dziennik zawiera listę czynności w procesie wdrożenia centrum usługi ATA. Służy on głównie do śledzenia procesu wdrażania centrum usługi ATA.

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDGGMMSS_0_MongoDBPackage.log** — ten dziennik zawiera listę czynności w procesie wdrożenia bazy danych MongoDB w centrum usługi ATA. Służy on głównie do śledzenia procesu wdrażania bazy danych MongoDB.

-   **Microsoft Advanced Threat Analytics Center_RRRRMMDDGGMMSS_1_MsiPackage.log** — ten dziennik zawiera listę czynności w procesie wdrożenia plików binarnych centrum usługi ATA. Służy on głównie do śledzenia wdrożenia plików binarnych centrum usługi ATA.

Dzienniki wdrażania bramy usługi ATA i bramy ATA Lightweight Gateway:

-   **Microsoft Advanced Threat Analytics Gateway_RRRRMMDDGGMMSS.log** — ten dziennik zawiera listę czynności w procesie wdrożenia bramy usługi ATA. Służy on głównie do śledzenia procesu wdrażania bramy usługi ATA.

-   **Microsoft Advanced Threat Analytics Gateway_RRRRMMDDGGMMSS_001_MsiPackage.log** — ten dziennik zawiera listę czynności w procesie wdrożenia plików binarnych bramy usługi ATA. Służy on głównie do śledzenia wdrożenia plików binarnych bramy usługi ATA.


## Zobacz też
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Oct16_HO4-->


