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

Jeśli masz już wdrożoną usługę ATA w wersji 1.8, ta procedura przeprowadzi Cię przez kroki niezbędne do aktualizacji wdrożenia.

> [!NOTE] 
>  Tylko wersja 1.8 usługi ATA (1.8.6645) oraz usługa ATA 1.8, aktualizacja 1 (1.8.6765) pozwala na aktualizację do wersji 1.9. Wcześniejszych wersji usługi ATA nie można bezpośrednio zaktualizować do wersji 1.9.

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.9:

1.  [Pobierz wersję aktualizacyjną usługi ATA 1.9 z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=56725) lub pełną wersję z [Centrum wersji ewaluacyjnych](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
Pakiet aktualizacyjny może służyć tylko do aktualizowania z usługi ATA 1.8. W przypadku wersji z centrum wersji ewaluacyjnych ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

2.  Zaktualizuj centrum usługi ATA

4.  Zaktualizuj bramy usługi ATA

    > [!IMPORTANT]
    > Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1. Zaktualizuj centrum usługi ATA

1.  Utwórz kopię zapasową bazy danych: (opcjonalnie)

    -   Jeśli Centrum usługi ATA jest uruchomione jako maszyna wirtualna i chcesz utworzyć punkt kontrolny, najpierw zamknij maszynę wirtualną.

    -   Jeśli centrum usługi ATA jest uruchomione na serwerze fizycznym, zobacz artykuł [Odzyskiwanie po awarii](disaster-recovery.md), aby uzyskać informacje o tworzeniu kopii zapasowej bazy danych.

2.  Uruchom plik instalacyjny **Microsoft ATA Center Setup.exe** i postępuj zgodnie z instrukcjami na ekranie, aby zainstalować aktualizację.

    -  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

    -  Jeśli nie zostały włączone aktualizacje automatyczne w wersji 1.8, pojawia się monit o skonfigurowanie usługi ATA do używania usługi Microsoft Update w celu aktualizacji usługi ATA.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Zachowaj aktualny obraz usługi ATA](media/ata_ms_update.png)
     
     To pozwala dopasować ustawienia Windows w celu włączenia aktualizacji usługi ATA. 
    
    -  Ekran **Częściowe dane migracji** informuje o tym, że dane na temat ruchu sieciowego przechwyconego wcześniej, zdarzeń, jednostek i wykrywania zostaną usunięte. Wszystkie metody wykrywania działają natychmiast z wyjątkiem wykrywania nietypowych zachowań, modyfikacji nietypowych grup, rozpoznania przy użyciu usług katalogu (SAM-R) i wykrycia obniżenia poziomu szyfrowania. Maksymalny czas utworzenia (uczenia) pełnego profilu to trzy tygodnie. 
     
      ![Częściowej migracji usługi ATA](media/partial-migration.png)

    -  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

4.  Po pomyślnym ukończeniu aktualizacji centrum usługi ATA kliknij przycisk **Uruchom**, aby otworzyć ekran **Aktualizacja** w konsoli bram usługi ATA.

     ![Ekran powodzenia aktualizacji](media/migration-center-success.png)

5.  Jeżeli na ekranie **Aktualizacje** ustawiono bramy usługi ATA do automatycznego aktualizowania, to są one zaktualizowane na tym etapie, jeśli nie, kliknij przycisk **Aktualizacja** dla każdej bramy usługi ATA.
  
     ![Obraz przedstawiający zaktualizowane bramy](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.
 
> [!NOTE] 
> Aby zainstalować nowe bramy usługi ATA, przejdź do ekranu **Bramy**, a następnie kliknij przycisk **Pobierz instalatora bramy**, żeby uzyskać pakiet instalacyjny bramy usługi ATA 1.9. Następnie postępuj zgodnie z instrukcjami dotyczącymi instalacji nowej bramy opisanymi w [krok 4. Instalowanie bramy usługi ATA](install-ata-step4.md).


## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
