---
# required metadata

title: Przewodnik po migracji związanej z aktualizacją usługi ATA do wersji 1.6 | Microsoft Advanced Threat Analytics
description: Procedury aktualizacji usługi ATA do wersji 1.6
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Przewodnik po migracji związanej z aktualizacją usługi ATA do wersji 1.6
Aktualizacja usługi ATA do wersji 1.6 zapewnia następujące ulepszenia:

-   Wykrywanie nowych zagrożeń

-   Ulepszenia istniejącego wykrywania

-   Brama ATA Lightweight Gateway

-   Aktualizacje automatyczne

-   Poprawiona wydajność centrum usługi ATA

-   Niższe wymagania dotyczące magazynu

-   Obsługa IBM QRadar

## Aktualizowanie usługi ATA do wersji 1.6
> [!NOTE] Jeśli usługa ATA nie jest zainstalowana w Twoim środowisku, pobierz pełną wersję usługi ATA, która zawiera wersję 1.6, i postępuj zgodnie ze standardową procedurą instalacji opisaną w artykule [Instalowanie usługi ATA](/advanced-threat-analytics/deploy-use/install-ata).

Jeśli została już wdrożona usługa ATA w wersji 1.5, ta procedura przeprowadzi Cię przez kroki niezbędne do aktualizacji wdrożenia.

> [!NOTE] Nie można zainstalować usługi ATA w wersji 1.6 bezpośrednio na usłudze ATA w wersji 1.4. Należy najpierw zainstalować usługę ATA w wersji 1.5. Jeśli użytkownik przypadkowo spróbuje zainstalować usługę ATA w wersji 1.6 z pominięciem usługi ATA w wersji 1.5, zostanie wyświetlony błąd informujący o tym, że **na tym komputerze jest już zainstalowana nowsza wersja.** Przed zainstalowaniem usługi ATA w wersji 1.5 należy odinstalować wszystkie elementy usługi ATA w wersji 1.6, które pozostały na komputerze — nawet wtedy, gdy instalacja się nie powiodła.

Wykonaj następujące kroki, aby zaktualizować usługę ATA do wersji 1.6:

1. Przed rozpoczęciem procesu uaktualnienia upewnij się, że wykonano procedurę obsługi opisaną w sekcji [Niepowodzenie migracji podczas przeprowadzania aktualizacji do usługi ATA w wersji 1.6](whats-new-version-1.6#Migration-failure-when-updating-from-ATA-1.5).
2. Upewnij się, że masz dostatecznie dużo wolnego miejsca do przeprowadzenia uaktualnienia. Możesz przeprowadzić instalację do momentu sprawdzania gotowości, aby uzyskać szacunkową ilość wymaganego wolnego miejsca, a następnie uruchomić ponownie uaktualnienie po przydzieleniu wymaganego miejsca na dysku. Uaktualnienie wykorzysta co najmniej 2% rozmiaru bazy danych. Aby uzyskać więcej informacji, zobacz [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).
1.  [Pobierz aktualizację do wersji 1.6](http://www.microsoft.com/en-us/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
W tej wersji ten sam plik instalacyjny (Microsoft ATA Center Setup.exe) jest używany do instalowania nowych wdrożeń usługi ATA i uaktualniania istniejących wdrożeń.

2.  Zaktualizuj centrum usługi ATA

3.  Pobierz zaktualizowany pakiet bramy usługi ATA

4.  Zaktualizuj bramy usługi ATA

    > [!IMPORTANT] Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### Krok 1. Zaktualizuj centrum usługi ATA

1.  Utwórz kopię zapasową bazy danych: (opcjonalnie)

    -   Jeśli centrum usługi ATA jest uruchomione jako maszyna wirtualna i chcesz utworzyć punkt kontrolny, najpierw zamknij maszynę wirtualną.

    -   Jeśli centrum usługi ATA jest uruchomione na serwerze fizycznym, postępuj zgodnie z zalecaną procedurą, aby [utworzyć kopię zapasową bazy danych MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Uruchom plik instalacyjny Microsoft ATA Center Setup.exe i postępuj zgodnie z instrukcjami na ekranie, aby zainstalować aktualizację.

    1.  Usługa ATA w wersji 1.6 wymaga zainstalowania platformy .NET Framework 4.6.1. Jeśli ta platforma nie jest jeszcze zainstalowana, usługa ATA zainstaluje platformę .NET Framework 4.6.1 w ramach instalacji.<br>
    > [!NOTE]Instalacja platformy .Net Framework 4.6.1 może wymagać ponownego uruchomienia serwera. Instalacja usługi ATA będzie kontynuowana dopiero po ponownym uruchomieniu serwera.
5.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

    6.  Przeczytaj umowę licencyjną użytkownika oprogramowania. Jeśli akceptujesz jej warunki, kliknij przycisk **Dalej**.

    7.  Obecnie istnieje możliwość użycia usługi Microsoft Update w celu utrzymania aktualnej usługi ATA.  Na stronie Microsoft Update wybierz pozycję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**.
    ![Obraz utrzymywania aktualnej usługi ATA](media/ata_ms_update.png) W ten sposób dostosujesz ustawienia systemu Windows, zezwalając na aktualizowanie innych produktów firmy Microsoft (w tym usługi ATA), jak pokazano w tym miejscu. 
     ![Obraz automatycznej aktualizacji systemu Windows](media/ata_installupdatesautomatically.png)

    8.  Przed rozpoczęciem instalacji usługa ATA wykona sprawdzenie gotowości. Przejrzyj wyniki procesu sprawdzania, aby upewnić się, że wymagania wstępne zostały odpowiednio skonfigurowane i masz co najmniej minimalną wymaganą ilość miejsca na dysku. 
    ![Obraz sprawdzania gotowości usługi ATA](media/ata_install_readinesschecks.png)

    3.  Kliknij przycisk **Aktualizuj**. Po kliknięciu przycisku Aktualizuj usługa ATA pozostaje w trybie offline do chwili, gdy procedura aktualizacji zostanie ukończona.

4.  Po zaktualizowaniu centrum usługi ATA bramy usługi ATA będą sygnalizować, że są przestarzałe.

    ![Obraz przedstawiający przestarzałe bramy](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Aby zapewnić prawidłowe działanie usługi ATA, zaktualizuj wszystkie bramy usługi ATA.

### Krok 2. Pobieranie pakietu instalacyjnego bramy usługi ATA
Po skonfigurowaniu ustawień łączności domeny możesz pobrać pakiet instalacyjny bramy usługi ATA.

Aby pobrać pakiet bramy usługi ATA:

1.  Usuń poprzednie wersje pakietu bramy usługi ATA, które zostały pobrane wcześniej.

2.  Na maszynie bramy usługi ATA otwórz przeglądarkę i wprowadź adres IP skonfigurowany w centrum usługi ATA dla konsoli usługi ATA. Po otwarciu konsoli usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji](media/ATA-config-icon.JPG)

3.  Na karcie **Bramy usługi ATA** kliknij pozycję **Pobierz instalatora bramy usługi ATA**.

4.  Zapisz pakiet lokalnie.

Plik zip zawiera następujące składniki:

-   Instalator bramy usługi ATA

-   Plik ustawień konfiguracji z informacjami wymaganymi do nawiązywania połączeń z centrum usługi ATA

### Krok 3. Zaktualizuj bramy usługi ATA

1.  Dla każdej bramy usługi ATA wyodrębnij pliki z pakietu bramy ATA i uruchom plik **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] Tego pakietu bramy usługi ATA możesz również używać do instalowania nowych bram usługi ATA.

2.  Twoje poprzednie ustawienia zostaną zachowane, ale ponowne uruchomienie usługi może potrwać kilka minut.

3.  Powtórz ten krok dla wszystkich innych wdrożonych bram usługi ATA.

> [!NOTE] Po pomyślnym zaktualizowaniu bramy usługi ATA nieaktualne powiadomienie dla tej bramy usługi ATA zostanie rozwiązane.

Jeśli wszystkie bramy usługi ATA zostaną pomyślnie zaktualizowane, wszystkie bramy usługi ATA będą sygnalizować pomyślne zsynchronizowanie, a komunikat o dostępności zaktualizowanego pakietu bramy usługi ATA nie będzie już wyświetlany.

![Obraz przedstawiający zaktualizowane bramy](media/ATA-gw-updated.png)


## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


