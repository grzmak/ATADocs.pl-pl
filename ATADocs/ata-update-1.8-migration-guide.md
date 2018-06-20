---
title: Przewodnik migracji do usługi Advanced Threat Analytics w wersji 1.8 | Microsoft Docs
description: Procedury aktualizacji usługi ATA do wersji 1.8
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/20/2017
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 540d1cb0754dc9191a985625a8f988cb44c9f000
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
ms.locfileid: "24019004"
---
# <a name="updating-ata-to-version-18"></a>Aktualizowanie usługi ATA do wersji 1.8

> [!NOTE] 
> Jeśli usługa ATA nie jest zainstalowana w Twoim środowisku, Pobierz pełną wersję usługi ATA, która zawiera wersję 1.8 i postępuj zgodnie ze standardową procedurą instalacji opisane w [Instalowanie usługi ATA](install-ata-step1.md).

Jeśli masz już usługi ATA w wersji 1,7 wdrożone, ta procedura przeprowadzi Cię przez kroki niezbędne do aktualizacji wdrożenia.

> [!NOTE] 
>  Do usługi ATA w wersji 1.8 można zaktualizować tylko usługę ATA w wersji 1.7 Update 1 i 1.7 Update 2. Żadnej wcześniejszej wersji usługi ATA nie można bezpośrednio zaktualizować do usługi ATA w wersji 1.8.

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.8:

1.  [Pobierz wersję aktualizacyjną usługi ATA 1.8 z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=55536) lub pełną wersję z [centrum wersji ewaluacyjnych](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
W przypadku wersji do migracji pliku można użyć tylko do aktualizowania z usługi ATA 1.7. W przypadku wersji z centrum wersji ewaluacyjnych ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

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

    -  Jeśli aktualizacje automatyczne w wersji 1,7 nie jest włączone, zostanie wyświetlony monit ustawić ATA Użyj usługi Microsoft Update, aby usługa ATA pozostaje aktualne.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Zachowaj aktualny obraz usługi ATA](media/ata_ms_update.png)
     
     To można dostosować ustawienia systemu Windows w celu włączenia aktualizacji usługi ATA. 
    
    -  Na ekranie **Migracja danych** wybierz, czy chcesz przeprowadzić migrację wszystkich danych czy ich części. Jeśli użytkownik chce migrować tylko częściowe dane, wszystkie wykrycia pracy natychmiast z wyjątkiem wykrywania nietypowe zachowanie, który przyjmuje trzy tygodnie do skonstruowania profilu ukończone.  
    
    **Częściowa** migracja danych wymaga o wiele mniej czasu na instalację. W przypadku wybrania opcji **Pełna** dla migracji danych ukończenie instalacji może zająć znaczną ilość czasu. Zwróć uwagę na szacowaną ilość czasu i wymagane miejsce na dysku wyświetlone na ekranie **Migracja danych**. Te wartości zależą od ilości ruchu sieciowego przechwyconego wcześniej, który został zapisany przez poprzednie wersje usługi ATA. Na przykład na ekranie poniżej możesz sprawdzić migracji danych z dużych bazy danych:
         
    ![Migracja danych usługi ATA](media/migration-data-migration.png)

    -  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

4.  Po pomyślnym ukończeniu aktualizacji centrum usługi ATA kliknij przycisk **Uruchom**, aby otworzyć ekran **Aktualizacja** w konsoli bram usługi ATA.

    ![Ekran powodzenia aktualizacji](media/migration-center-success.png)

5.  W **aktualizacje** ekranu, jeśli ustawisz bram usługi ATA do automatycznego aktualizowania one aktualizacji w tym momencie, jeśli nie, kliknij przycisk **aktualizacji** obok każdej bramy usługi ATA.
  
![Obraz przedstawiający zaktualizowane bramy](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.
 
> [!NOTE] 
> W celu zainstalowania nowych bram usługi ATA przejdź do ekranu **Bramy**, kliknij pozycję **Pobierz instalatora bramy**, aby uzyskać pakiet instalacyjny bramy usługi ATA 1.8, i postępuj zgodnie z instrukcjami dotyczącymi instalacji nowej bramy w części [Krok 4. Instalowanie bramy usługi ATA](install-ata-step4.md).


## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
