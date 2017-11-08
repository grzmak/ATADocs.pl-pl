---
title: "Przewodnik po migracji związanej z aktualizacją usługi Advanced Threat Analytics do wersji 1.6 | Dokumentacja firmy Microsoft"
description: "Procedury aktualizacji usługi ATA do wersji 1.6"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 0756ef64-3aef-4a69-8981-24fa8f285c6a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c1be20cc147e88f55d227818331f06d409dd08e7
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
# <a name="ata-update-to-16-migration-guide"></a>Przewodnik po migracji związanej z aktualizacją usługi ATA do wersji 1.6
Aktualizacja usługi ATA do wersji 1.6 zapewnia następujące ulepszenia:

-   Wykrywanie nowych zagrożeń

-   Ulepszenia istniejącego wykrywania

-   Brama ATA Lightweight Gateway

-   Aktualizacje automatyczne

-   Poprawiona wydajność centrum usługi ATA

-   Niższe wymagania dotyczące magazynu

-   Obsługa IBM QRadar

## <a name="updating-ata-to-version-16"></a>Aktualizowanie usługi ATA do wersji 1.6
> [!NOTE] 
> Jeśli usługa ATA nie jest zainstalowana w Twoim środowisku, Pobierz pełną wersję usługi ATA, która zawiera wersję 1.6 i postępuj zgodnie ze standardową procedurą instalacji opisane w [Instalowanie usługi ATA](install-ata-step1.md).

Jeśli masz już usługi ATA w wersji 1.5 wdrożone, ta procedura przeprowadzi Cię przez kroki niezbędne do aktualizacji wdrożenia.

> [!NOTE] 
> Nie można zainstalować usługi ATA w wersji 1.6 bezpośrednio na usłudze ATA w wersji 1.4. Należy najpierw zainstalować usługę ATA w wersji 1.5. Jeśli użytkownik przypadkowo spróbuje zainstalować 1.6 usługi ATA bez instalowania usługi ATA w wersji 1.5, wystąpi błąd informujący, że **na tym komputerze jest już zainstalowana nowsza wersja.** Należy odinstalować wszystkie elementy w wersji 1.6 usługi ATA, które pozostają na komputerze — nawet jeśli instalacja nie powiodła się — przed zainstalowaniem usługi ATA w wersji 1.5.

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.6:

1. Aby uniknąć problemów z uaktualnianiem, upewnij się, że wykonano kroki od 8 do 10 instrukcji **Błąd migracji podczas aktualizacji do wersji 1.6 usługi ATA** opisanej w temacie [Co nowego w wersji 1.6 usługi ATA](whats-new-version-1.6.md).
2. Upewnij się, że masz dostatecznie dużo wolnego miejsca do przeprowadzenia uaktualnienia. Możesz przeprowadzić instalację do momentu sprawdzania gotowości, aby uzyskać szacunkową ilość wymaganego wolnego miejsca, a następnie uruchomić ponownie uaktualnienie po przydzieleniu wymaganego miejsca na dysku.
1.  [Pobierz aktualizację do wersji 1.6](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
W tej wersji ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

2.  Zaktualizuj centrum usługi ATA

3.  Pobierz zaktualizowany pakiet bramy usługi ATA

4.  Zaktualizuj bramy usługi ATA

    > [!IMPORTANT]
    > Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1. Zaktualizuj centrum usługi ATA

1.  Utwórz kopię zapasową bazy danych: (opcjonalnie)

    -   Jeśli Centrum usługi ATA jest uruchomione jako maszyny wirtualnej i chcesz utworzyć punkt kontrolny, najpierw zamknij maszynę wirtualną.

    -   Jeśli centrum usługi ATA jest uruchomione na serwerze fizycznym, postępuj zgodnie z zalecaną procedurą, aby [utworzyć kopię zapasową bazy danych MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Uruchom plik instalacyjny Microsoft ATA Center Setup.exe i postępuj zgodnie z instrukcjami na ekranie, aby zainstalować aktualizację.

    1.  Usługa ATA w wersji 1.6 wymaga zainstalowania platformy .NET Framework 4.6.1. Jeśli nie jest jeszcze zainstalowana, instalacja usługi ATA zainstaluje .net Framework 4.6.1 w ramach instalacji.
    
        > [!NOTE] 
        > Instalacja platformy .Net Framework 4.6.1 może wymagać ponownego uruchomienia serwera. Instalacja usługi ATA będzie kontynuowana dopiero po ponownym uruchomieniu serwera.
    
    2.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

    3.  Przeczytaj umowę licencyjną użytkownika końcowego i jeśli akceptujesz jej warunki, kliknij przycisk **dalej**.

    4.  Obecnie istnieje możliwość użycia usługi Microsoft Update w celu utrzymania aktualnej usługi ATA.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Zachowaj ATA aktualny obraz](media/ata_ms_update.png) to można dostosować ustawienia systemu Windows, aby włączyć aktualizacje dla innych produktów firmy Microsoft (w tym usługi ATA), jak pokazano poniżej. 
     ![Obraz automatycznej aktualizacji systemu Windows](media/ata_installupdatesautomatically.png)

    5.  Przed rozpoczęciem instalacji usługi ATA wykonuje sprawdzanie gotowości. Przejrzyj wyniki sprawdzania, aby upewnić się, że wymagania wstępne zostały odpowiednio skonfigurowane i że masz co najmniej minimalną ilość miejsca na dysku. 
    ![Obraz sprawdzania gotowości usługi ATA](media/ata_install_readinesschecks.png)

    6.  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

3.  Po zaktualizowaniu centrum usługi ATA bramy usługi ATA będą sygnalizować, że są przestarzałe.

    ![Obraz przedstawiający przestarzałe bramy](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Krok 2. Pobieranie pakietu instalacyjnego bramy usługi ATA
Po skonfigurowaniu ustawień łączności domeny możesz pobrać pakiet instalacyjny bramy usługi ATA.

Aby pobrać pakiet bramy usługi ATA:

1.  Usuń poprzednie wersje pakietu bramy usługi ATA, które zostały pobrane wcześniej.

2.  Na maszynie bramy usługi ATA otwórz przeglądarkę i wprowadź adres IP skonfigurowany w centrum usługi ATA dla konsoli usługi ATA. Po otwarciu konsoli usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji](media/ATA-config-icon.png)

3.  Na karcie **Bramy usługi ATA** kliknij pozycję **Pobierz instalatora bramy usługi ATA**.

4.  Zapisz pakiet lokalnie.

Plik zip zawiera następujące pliki:

-   Instalator bramy usługi ATA

-   Plik ustawień konfiguracji z informacjami wymaganymi do nawiązywania połączeń z centrum usługi ATA

### <a name="step-3-update-the-ata-gateways"></a>Krok 3. Zaktualizuj bramy usługi ATA

1.  Dla każdej bramy usługi ATA wyodrębnij pliki z pakietu bramy ATA i uruchom plik **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] 
    > Tego pakietu bramy usługi ATA możesz również używać do instalowania nowych bram usługi ATA.

2.  Twoje poprzednie ustawienia zostaną zachowane, ale może potrwać kilka minut na ponowne uruchomienie usługi.

3.  Powtórz ten krok dla wszystkich innych wdrożonych bram usługi ATA.

> [!NOTE] 
> Po pomyślnym zaktualizowaniu bramy usługi ATA nieaktualne powiadomienie dla tej bramy usługi ATA zostanie rozwiązane.

Wiadomo, że wszystkie bramy usługi ATA zostały pomyślnie zaktualizowane gdy raport wszystkich bram usługi ATA będą sygnalizować pomyślne zsynchronizowanie, a nie jest wyświetlany komunikat, że zaktualizowanego pakietu bramy usługi ATA jest dostępny.

![Obraz przedstawiający zaktualizowane bramy](media/ATA-gw-updated.png)


## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
