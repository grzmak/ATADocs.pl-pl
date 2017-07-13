---
title: "Przewodnik migracji do usługi Advanced Threat Analytics w wersji 1.8 | Microsoft Docs"
description: "Procedury aktualizacji usługi ATA do wersji 1.8"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/5/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1042f464f424d2805542a8145d2e09d592fe8a51
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2017
---
# Aktualizowanie usługi ATA do wersji 1.8
<a id="updating-ata-to-version-18" class="xliff"></a>

> [!NOTE] 
> Jeśli usługa ATA nie jest zainstalowana w Twoim środowisku, pobierz pełną wersję usługi ATA, która zawiera wersję 1.8, i postępuj zgodnie ze standardową procedurą instalacji opisaną w artykule [Instalowanie usługi ATA](install-ata-step1.md).

Jeśli masz już wdrożoną usługę ATA w wersji 1.7, ta procedura przeprowadzi Cię przez kroki wymagane do aktualizacji wdrożenia.

> [!NOTE] 
>  Do usługi ATA w wersji 1.8 można zaktualizować tylko usługę ATA w wersji 1.7 Update 1 i 1.7 Update 2. Żadnej wcześniejszej wersji usługi ATA nie można bezpośrednio zaktualizować do usługi ATA w wersji 1.8.

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.8:

1.  [Pobierz wersję aktualizacyjną usługi ATA 1.8 z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=55536) lub pełną wersję z [centrum wersji ewaluacyjnych](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
W przypadku wersji do migracji pliku można użyć tylko do aktualizowania z usługi ATA 1.7. W przypadku wersji z centrum wersji ewaluacyjnych ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

2.  Zaktualizuj centrum usługi ATA

4.  Zaktualizuj bramy usługi ATA

    > [!IMPORTANT]
    > Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### Krok 1. Zaktualizuj centrum usługi ATA
<a id="step-1-update-the-ata-center" class="xliff"></a>

1.  Utwórz kopię zapasową bazy danych: (opcjonalnie)

    -   Jeśli centrum usługi ATA jest uruchomione jako maszyna wirtualna i chcesz utworzyć punkt kontrolny, najpierw zamknij maszynę wirtualną.

    -   Jeśli centrum usługi ATA jest uruchomione na serwerze fizycznym, zobacz artykuł [Odzyskiwanie po awarii](disaster-recovery.md), aby uzyskać informacje o tworzeniu kopii zapasowej bazy danych.

2.  Uruchom plik instalacyjny **Microsoft ATA Center Setup.exe** i postępuj zgodnie z instrukcjami na ekranie, aby zainstalować aktualizację.

    -  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

    -  Jeśli aktualizacje automatyczne nie zostały włączone w wersji 1.7, pojawi się monit o skonfigurowanie usługi ATA pod kątem używania usługi Microsoft Update do zachowania aktualności usługi ATA.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Obraz utrzymywania aktualności usługi ATA](media/ata_ms_update.png)
     
     W ten sposób dostosujesz ustawienia systemu Windows, zezwalając na aktualizowanie innych produktów firmy Microsoft (w tym usługi ATA), jak wspomniano w tym miejscu. 
    ![Obraz automatycznej aktualizacji systemu Windows](media/ata_installupdatesautomatically.png)

    -  Na ekranie **Migracja danych** wybierz, czy chcesz przeprowadzić migrację wszystkich danych czy ich części. Jeśli zmigrujesz tylko część danych, wszystkie funkcje wykrywania będą działać natychmiast — z wyjątkiem wykrywania nietypowych zachowań, w przypadku którego utworzenie pełnego profilu trwa 3 tygodnie.  
    
    **Częściowa** migracja danych wymaga o wiele mniej czasu na instalację. W przypadku wybrania opcji **Pełna** dla migracji danych ukończenie instalacji może zająć znaczną ilość czasu. Zwróć uwagę na szacowaną ilość czasu i wymagane miejsce na dysku wyświetlone na ekranie **Migracja danych**. Te wartości zależą od ilości ruchu sieciowego przechwyconego wcześniej, który został zapisany przez poprzednie wersje usługi ATA. Na przykład na ekranie poniżej przedstawiono migrację danych z bardzo dużej bazy danych:
         
    ![Migracja danych usługi ATA](media/migration-data-migration.png)

    -  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

4.  Po pomyślnym ukończeniu aktualizacji centrum usługi ATA kliknij przycisk **Uruchom**, aby otworzyć ekran **Aktualizacja** w konsoli bram usługi ATA.

    ![Ekran powodzenia aktualizacji](media/migration-center-success.png)

5.  Jeśli bramy usługi ATA zostały już skonfigurowane do automatycznego aktualizowania, zostaną zaktualizowane na tym etapie. Jeśli nie, kliknij przycisk **Aktualizuj** obok każdej bramy ATA na ekranie **Aktualizacja**.
  
![Obraz przedstawiający zaktualizowane bramy](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.
 
> [!NOTE] 
> W celu zainstalowania nowych bram usługi ATA przejdź do ekranu **Bramy**, kliknij pozycję **Pobierz instalatora bramy**, aby uzyskać pakiet instalacyjny bramy usługi ATA 1.8, i postępuj zgodnie z instrukcjami dotyczącymi instalacji nowej bramy w części [Krok 4. Instalowanie bramy usługi ATA](install-ata-step4.md).


## Zobacz też
<a id="see-also" class="xliff"></a>

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)