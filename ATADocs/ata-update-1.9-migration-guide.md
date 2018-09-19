---
title: Aktualizacją usługi Advanced Threat Analytics do przewodnika migracji 1.9 | Dokumentacja firmy Microsoft
description: Procedury aktualizacji usługi ATA do wersji 1.9
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 03/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cfcf40c0c5776a29e3aa680096930b50ac04396f
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133297"
---
# <a name="updating-ata-to-version-19"></a>Aktualizowanie usługi ATA do wersji 1.9

> [!NOTE] 
> Jeśli usługa ATA nie jest zainstalowana w Twoim środowisku, Pobierz pełną wersję usługi ATA, która zawiera informacje dotyczące wersji 1.9 i postępuj zgodnie ze standardową procedurą instalacji opisane w [Instalowanie usługi ATA](install-ata-step1.md).

Jeśli masz już usługę ATA w wersji 1.8 wdrożone, ta procedura przeprowadzi Cię przez kroki niezbędne do aktualizacji wdrożenia.

> [!NOTE] 
>  Tylko wersji 1.8 usługi ATA (1.8.6645) i usłudze ATA 1.8, aktualizacja 1 (1.8.6765) można zaktualizować usługę ATA do wersji 1.9, jego wcześniejszą wersję usługi ATA nie można bezpośrednio zaktualizować usługę ATA do wersji 1.9.

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.9:

1.  [Pobierz wersję aktualizacyjną usługi ATA 1.9 z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=56725) lub pełną wersję z [Centrum wersji ewaluacyjnych](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
W przypadku wersji do migracji pliku może służyć tylko do aktualizowania z usługi ATA 1.8. W przypadku wersji z centrum wersji ewaluacyjnych ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

2.  Zaktualizuj centrum usługi ATA

4.  Zaktualizuj bramy usługi ATA

    > [!IMPORTANT]
    > Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1. Zaktualizuj centrum usługi ATA

1.  Utwórz kopię zapasową bazy danych: (opcjonalnie)

    -   Jeśli Centrum usługi ATA jest uruchomione jako maszyny wirtualnej i chcesz utworzyć punkt kontrolny, najpierw zamknij maszynę wirtualną.

    -   Jeśli centrum usługi ATA jest uruchomione na serwerze fizycznym, zobacz artykuł [Odzyskiwanie po awarii](disaster-recovery.md), aby uzyskać informacje o tworzeniu kopii zapasowej bazy danych.

2.  Uruchom plik instalacyjny **Microsoft ATA Center Setup.exe** i postępuj zgodnie z instrukcjami na ekranie, aby zainstalować aktualizację.

    -  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

    -  Jeśli nie zostały włączone aktualizacje automatyczne w wersji 1.8, pojawia się monit o skonfigurowanie usługi ATA do używania usługi Microsoft Update, aby usługa ATA aktualnych.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Zachowaj aktualny obraz usługi ATA](media/ata_ms_update.png)
     
     To pozwala dopasować ustawienia Windows w celu włączenia aktualizacji usługi ATA. 
    
    -  **Częściowe dane migracji** ekran informuje o tym, że ruchu sieciowego przechwyconego wcześniej, zdarzenia, jednostek i wykrywanie powiązane dane zostaną usunięte. Wszystkie wykrycia działać natychmiast z wyjątkiem wykrywania nietypowych zachowań, modyfikacja grupy nietypowe, Rekonesans przy użyciu usług katalogu (SAM-R) i wykrycia obniżenia poziomu szyfrowania, które maksymalnie trzy tygodnie po utworzeniu pełnego profilu czas wymagany uczenia. 
     
      ![Częściowej migracji usługi ATA](media/partial-migration.png)

    -  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

4.  Po pomyślnym ukończeniu aktualizacji centrum usługi ATA kliknij przycisk **Uruchom**, aby otworzyć ekran **Aktualizacja** w konsoli bram usługi ATA.

     ![Ekran powodzenia aktualizacji](media/migration-center-success.png)

5.  W **aktualizacje** ekranu, jeśli ustawisz bram usługi ATA do automatycznego aktualizowania są zaktualizowane na tym etapie, jeśli nie, kliknij przycisk **aktualizacji** obok każdej bramy usługi ATA.
  
     ![Obraz przedstawiający zaktualizowane bramy](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.
 
> [!NOTE] 
> Aby zainstalować nowych bram usługi ATA, przejdź **bram** ekranu, a następnie kliknij przycisk **Pobierz instalatora bramy** uzyskać pakiet instalacyjny bramy usługi ATA 1.9 usług i postępuj zgodnie z instrukcjami dotyczącymi instalacji nowej bramy jako opisane w [krok 4. Instalowanie bramy usługi ATA](install-ata-step4.md).


## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
