---
title: Advanced Threat Analytics aktualizacji w przewodniku migracji 1,9 | Dokumentacja firmy Microsoft
description: Procedury aktualizacji usługi ATA do wersji 1.9
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 03/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0bd4bca536facb9ad4b7fea627f2ef512949728e
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202337"
---
# <a name="updating-ata-to-version-19"></a>Aktualizowanie usługi ATA do wersji 1.9

> [!NOTE] 
> Jeśli usługa ATA nie jest zainstalowana w Twoim środowisku, Pobierz pełną wersję usługi ATA, która zawiera wersję 1.9 i postępuj zgodnie ze standardową procedurą instalacji opisane w [Instalowanie usługi ATA](install-ata-step1.md).

Jeśli masz już usługi ATA w wersji 1.8 wdrożone, ta procedura przeprowadzi Cię przez kroki niezbędne do aktualizacji wdrożenia.

> [!NOTE] 
>  Tylko usługi ATA w wersji 1.8 (1.8.6645) i aktualizacja usługi ATA 1.8 1 (1.8.6765) można zaktualizować usługę ATA do wersji 1.9, jakakolwiek wcześniejsza wersja usługi ATA nie można bezpośrednio zaktualizować usługę ATA do wersji 1.9.

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.9:

1.  [Pobierz wersję aktualizacji 1.9 usługi ATA z Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=56725) lub pełnej wersji z [Eval center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
W wersji migracji pliku może służyć tylko w przypadku aktualizowania z 1.8 usługi ATA. W przypadku wersji z centrum wersji ewaluacyjnych ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

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

    -  Jeśli nie włączysz aktualizacji automatycznych w wersji 1.8, zostanie wyświetlony monit ustawić ATA Użyj usługi Microsoft Update, aby usługa ATA pozostaje aktualne.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Zachowaj aktualny obraz usługi ATA](media/ata_ms_update.png)
     
     To można dostosować ustawienia systemu Windows w celu włączenia aktualizacji usługi ATA. 
    
    -  **Migracji danych z częściowa** ekranu informujące, że ruch sieciowy wcześniej przechwycone, zdarzenia, jednostki i wykrywania powiązane dane zostaną usunięte. Wszystkie wykrycia pracować bezpośrednio z wyjątkiem wykrywania nietypowe zachowanie, nietypowe grupy modyfikacji, Rekonesans przy użyciu usług katalogowych (SAM-R) i wykrycia obniżenia poziomu szyfrowania, przyjmujących trzy tygodnie do tworzenia profilu pełną po czas nauki wymagane. 
     
      ![Częściowe migracji usługi ATA](media/partial-migration.png)

    -  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

4.  Po pomyślnym ukończeniu aktualizacji centrum usługi ATA kliknij przycisk **Uruchom**, aby otworzyć ekran **Aktualizacja** w konsoli bram usługi ATA.

     ![Ekran powodzenia aktualizacji](media/migration-center-success.png)

5.  W **aktualizacje** ekranu, jeśli ustawisz bram usługi ATA do automatycznego aktualizowania one aktualizacji w tym momencie, jeśli nie, kliknij przycisk **aktualizacji** obok każdej bramy usługi ATA.
  
     ![Obraz przedstawiający zaktualizowane bramy](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.
 
> [!NOTE] 
> Aby zainstalować nowych bram usługi ATA, przejdź **bram** ekranu, a następnie kliknij przycisk **Pobierz instalatora bramy** pobrać pakiet instalacyjny bramy usługi ATA 1.9, a następnie postępuj zgodnie z instrukcjami dotyczącymi nowa instalacja bramy jako opisane w [krok 4. Instalowanie bramy usługi ATA](install-ata-step4.md).


## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
