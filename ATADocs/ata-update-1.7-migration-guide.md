---
title: "Przewodnik po migracji związanej z aktualizacją usługi Advanced Threat Analytics do wersji 1.7 | Dokumentacja firmy Microsoft"
description: "Procedury aktualizacji usługi ATA do wersji 1.7"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8eefcd45-7a4b-4074-ac5b-1ffc48e6654a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a1494f0428593ee58c7e1da64192b45c6d006c15
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
# <a name="ata-update-to-17-migration-guide"></a>Przewodnik po migracji związanej z aktualizacją usługi ATA do wersji 1.7
Aktualizacja usługi ATA do wersji 1.7 zapewnia następujące ulepszenia:

-   Wykrywanie nowych zagrożeń

-   Ulepszenia istniejącego wykrywania
  

## <a name="updating-ata-to-version-17"></a>Aktualizowanie usługi ATA do wersji 1.7

> [!NOTE] 
> Jeśli usługa ATA nie jest zainstalowana w danym środowisku, pobierz pełną wersję usługi ATA, która zawiera wersję 1.7, i postępuj zgodnie ze standardową procedurą instalacji opisaną w artykule [Instalowanie usługi ATA](install-ata-step1.md).

Jeśli została już wdrożona usługa ATA w wersji 1.6, ta procedura przeprowadzi Cię przez kroki niezbędne do aktualizacji wdrożenia.

> [!NOTE] 
> Nie można zainstalować usługi ATA w wersji 1.7 bezpośrednio na usłudze ATA w wersji 1.4 lub 1.5. Należy najpierw zainstalować usługę ATA w wersji 1.6. 

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.7:

1.  [Pobierz aktualizację do wersji 1.7](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
W tej wersji ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

2.  Zaktualizuj centrum usługi ATA

4.  Zaktualizuj bramy usługi ATA

    > [!IMPORTANT]
    > Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1. Zaktualizuj centrum usługi ATA

1.  Utwórz kopię zapasową bazy danych: (opcjonalnie)

    -   Jeśli centrum usługi ATA jest uruchomione jako maszyna wirtualna i chcesz utworzyć punkt kontrolny, najpierw zamknij maszynę wirtualną.

    -   Jeśli centrum usługi ATA jest uruchomione na serwerze fizycznym, postępuj zgodnie z zalecaną procedurą, aby [utworzyć kopię zapasową bazy danych MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Uruchom plik instalacyjny **Microsoft ATA Center Setup.exe** i postępuj zgodnie z instrukcjami na ekranie, aby zainstalować aktualizację.

    -  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

    -  Jeśli aktualizacje automatyczne nie zostały włączone w wersji 1.6, pojawi się monit, aby skonfigurować usługę ATA do używania usługi Microsoft Update w celu zachowania aktualności usługi ATA.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Obraz utrzymywania aktualności usługi ATA](media/ata_ms_update.png) W ten sposób dostosujesz ustawienia systemu Windows, zezwalając na aktualizowanie innych produktów firmy Microsoft (w tym usługi ATA), jak pokazano w tym miejscu. 
     ![Obraz automatycznej aktualizacji systemu Windows](media/ata_installupdatesautomatically.png)

    -  Na ekranie **Migracja danych** wybierz, czy chcesz przeprowadzić migrację wszystkich danych czy ich części. Jeśli wybierzesz przeprowadzenie migracji tylko części danych, wcześniej przechwycone profile ruchu sieciowego i zachowania nie zostaną poddane migracji. Oznacza to, że dopiero po trzech tygodniach zostanie pozyskany pełen profil umożliwiający wykrywanie nietypowego zachowania. Podczas tych trzech tygodni wszystkie pozostałe mechanizmy wykrywania usługi ATA będą działać poprawnie. **Częściowa** migracja danych wymaga mniej czasu na instalację. W przypadku wybrania opcji **Pełna** dla migracji danych ukończenie instalacji może zająć znaczną ilość czasu. Szacowana ilość czasu i wymaganego miejsca na dysku, które są wyświetlane na ekranie **Migracja danych**, zależą od ilości ruchu sieciowego przechwyconego wcześniej i zapisanego w poprzednich wersjach usługi ATA. Przed wybraniem opcji **Częściowa** lub **Pełna** koniecznie sprawdź te wymagania.  
    
    ![Migracja danych usługi ATA](media/migration-data-migration17.png)

    -  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

4.  Po pomyślnym ukończeniu aktualizacji centrum usługi ATA kliknij przycisk **Uruchom**, aby otworzyć ekran **Aktualizacja** w konsoli bram usługi ATA.
    ![Ekran powodzenia aktualizacji](media/migration-center-success17.png)

5.  Jeśli bramy usługi ATA zostały już skonfigurowane do automatycznego aktualizowania, zostaną zaktualizowane na tym etapie. Jeśli nie, kliknij przycisk **Aktualizuj** obok każdej bramy ATA na ekranie **Aktualizacja**.
  ![Obraz aktualizowania bram](media/migration-update-gw-17.png)

  
> [!IMPORTANT] 
> Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.
> Skonfigurowany port odbiornika Syslog na wszystkich bramach zostanie zmieniony na 514.
 
> [!NOTE] 
> W celu zainstalowania nowych bram usługi ATA przejdź do ekranu **Bramy**, kliknij pozycję **Pobierz konfigurację bramy**, aby uzyskać pakiet instalacyjny usługi ATA 1.7, i postępuj zgodnie z instrukcjami dotyczącymi instalacji nowej bramy zgodnie z opisem w części [Krok 4. Instalowanie bramy usługi ATA](install-ata-step4.md).



## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
