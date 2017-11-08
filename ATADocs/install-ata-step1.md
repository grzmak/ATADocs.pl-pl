---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 1 | Dokumentacja firmy Microsoft"
description: "Pierwszy krok w celu zainstalowania usługi ATA polega na pobraniu i zainstalowaniu centrum usługi ATA na wybranym serwerze."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f35c495193806f1c1ccc00800402d9b0aca36982
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# <a name="install-ata---step-1"></a>Instalowanie usługi ATA — Krok 1

>[!div class="step-by-step"]
[Krok 2 »](install-ata-step2.md)

Ta procedura instalacji zawiera instrukcje dotyczące przeprowadzania świeżej instalacji usługi ATA 1.8. Informacje na temat aktualizowania istniejącego wdrożenia usługi ATA ze starszej wersji znajdują się w [przewodniku migracji dla usługi ATA 1.8](ata-update-1.8-migration-guide.md).

> [!IMPORTANT] 
> Jeśli używasz systemu Windows 2012 R2, można zainstalować aktualizację KB2934520 na serwerze Centrum usługi ATA i na serwerach bramy usługi ATA przed rozpoczęciem instalacji, w przeciwnym razie instalacja usługi ATA zainstaluje tę aktualizację i wymaga ponownego uruchomienia komputera w trakcie instalacji usługi ATA.

## <a name="step-1-download-and-install-the-ata-center"></a>Krok 1. Pobieranie i instalowanie centrum usługi ATA
Po sprawdzeniu, czy serwer spełnia wymagania, możesz kontynuować instalację centrum usługi ATA.
    
> [!NOTE]
>Jeśli masz licencję usługi Enterprise Mobility + Security (EMS) uzyskaną bezpośrednio przez portal usługi Office 365 lub w ramach modelu licencjonowania Cloud Solution Partner (CSP) i nie masz dostępu do usługi ATA w Centrum licencjonowania zbiorczego firmy Microsoft (VLSC), skontaktuj się z Pomocą techniczną firmy Microsoft, która udostępni proces aktywacji usługi Advanced Threat Analytics.

Na serwerze centrum usługi ATA wykonaj następujące kroki.

1.  Pobierz usługę ATA z [Centrum usługi licencjonowania zbiorowego firmy Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [Centrum ewaluacji TechNet](http://www.microsoft.com/evalcenter/) lub z [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Zaloguj się do komputera, na którym instalujesz Centrum usługi ATA jako użytkownik, który jest członkiem lokalnej grupy administratorów.

3.  Uruchom plik **Microsoft ATA Center Setup.EXE**, a następnie postępuj zgodnie z komunikatami kreatora instalacji.

> [!NOTE]   
> Pamiętaj, aby uruchomić plik instalacyjny z dysku lokalnego, a nie z zainstalowanego pliku ISO. Pozwoli to na uniknięcie problemów w przypadku, gdy w ramach instalacji jest wymagany ponowny rozruch.   

4.  Jeśli nie zainstalowano programu Microsoft .net Framework, są monit o jej zainstalowanie po rozpoczęciu instalacji. Po zakończeniu instalacji platformy .Net Framework może pojawić się prośba o ponowne uruchomienie.
5.  Na stronie **Zapraszamy** wybierz język do zastosowania na ekranach instalacji usługi ATA i kliknij przycisk **Dalej**.

6.  Przeczytaj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft i, jeśli akceptujesz jej warunki, zaznacz pole wyboru, a następnie kliknij przycisk **dalej**.

7.  Zaleca się ustawienie automatycznej aktualizacji usługi ATA. Jeśli system Windows nie jest skonfigurowany w tym celu na komputerze, możesz uzyskać **Użyj usługi Microsoft Update, aby chronić komputer i aktualne** ekranu. 
    ![Obraz utrzymywania aktualności usługi ATA](media/ata_ms_update.png)

8. Wybierz opcję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**. To można dostosować ustawienia systemu Windows, aby włączyć aktualizacje dla innych produktów firmy Microsoft (w tym usługi ATA), jak pokazano poniżej. 

    ![Obraz automatycznej aktualizacji systemu Windows](media/ata_installupdatesautomatically.png)

8.  Na stronie **Konfiguracja centrum** podaj następujące informacje odpowiednie dla używanego środowiska:

    |Pole|Opis|Komentarze|
    |---------|---------------|------------|
    |Ścieżka instalacji|Jest to lokalizacja, w którym zainstalowano Centrum usługi ATA. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Center|Pozostaw wartość domyślną.|
    |Ścieżka danych bazy danych|Jest to lokalizacja, w którym znajdują się pliki bazy danych MongoDB. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Zmień lokalizację na taką, w której będzie wystarczająca ilość miejsca do przechowywania powiększającej się bazy danych na podstawie ustalonego rozmiaru. **Uwaga:** <ul><li>W środowisku produkcyjnym należy używać dysku, który ma za mało miejsca na podstawie podczas planowania pojemności.</li><li>W przypadku dużych wdrożeń baza danych powinna znajdować się na oddzielnym dysku fizycznym.</li></ul>Aby uzyskać informacje dotyczące ustalania rozmiaru, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).|
    |Certyfikat SSL centrum usługi|Jest to certyfikat, który jest używany przez usługę konsoli usługi ATA i Centrum usługi ATA.|Kliknij ikonę klucza, aby wybrać zainstalowany certyfikat, lub zaznacz opcję Certyfikat z podpisem własnym w przypadku wdrażania w środowisku laboratoryjnym. Istnieje możliwość utworzenia certyfikatu z podpisem własnym.|
        
    ![Obraz przedstawiający konfigurowanie centrum usługi ATA](media/ATA-Center-Configuration.png)

10.  Kliknij przycisk **Zainstaluj**, aby zainstalować centrum usługi ATA i jego składniki.
    Następujące składniki zostaną zainstalowane i skonfigurowane podczas instalacji centrum usługi ATA:

    -   Centrum usługi ATA

    -   Baza danych MongoDB

    -   Niestandardowy zestaw kolekcji danych monitora wydajności

    -   Certyfikaty z podpisem własnym (jeśli zostały wybrane podczas instalacji)

11.  Po zakończeniu instalacji kliknij przycisk **Uruchom**, aby otworzyć konsolę usługi ATA i zakończyć instalację na stronie **Konfiguracja**.
W tym momencie zostanie wyświetlona automatycznie **ogólne** strony ustawień umożliwiająca kontynuowanie konfiguracji i wdrażania bram usługi ATA.
Ponieważ logujesz się do witryny przy użyciu adresu IP, zostanie wyświetlone ostrzeżenie związane z certyfikatem. jest to normalne, i kliknij przycisk **Kontynuuj przeglądanie tej witryny sieci Web**.

### <a name="validate-installation"></a>Weryfikowanie instalacji

1.  Sprawdź, czy usługa o nazwie **Microsoft Advanced Threat Analytics Center** jest uruchomiona.
2.  Na pulpicie kliknij skrót do usługi **Microsoft Advanced Threat Analytics**, aby nawiązać połączenie z konsolą usługi ATA. Zaloguj się przy użyciu tych samych poświadczeń użytkownika, które zostały użyte do zainstalowania centrum usługi ATA.



>[!div class="step-by-step"]
[« Przed rozpoczęciem instalacji](configure-port-mirroring.md)
[Krok 2 »](install-ata-step2.md)

## <a name="related-videos"></a>Powiązane pliki wideo
- [Wybieranie odpowiedniej typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [Przegląd wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania usługi ATA fazy weryfikacji Koncepcji](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

