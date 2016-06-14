---
# required metadata

title: Instalowanie usługi ATA — Krok 1 | Microsoft Advanced Threat Analytics
description: Pierwszy krok w celu zainstalowania usługi ATA polega na pobraniu i zainstalowaniu centrum usługi ATA na wybranym serwerze.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalowanie usługi ATA — Krok 1

>[!div class="step-by-step"]

[Krok 2 »](install-ata-step2.md)

Ta procedura instalacji zawiera instrukcje dotyczące przeprowadzania nowej instalacji usługi ATA w wersji 1.6. Informacje na temat aktualizowania istniejącego wdrożenia usługi ATA ze starszej wersji znajdują się w temacie [Przewodnik po migracji usługi ATA dla wersji 1.6](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide).

> [!IMPORTANT] Zainstaluj aktualizację KB2934520 na serwerze centrum usługi ATA i na serwerach bramy usługi ATA przed rozpoczęciem instalacji, w przeciwnym razie instalacja usługi ATA zainstaluje tę aktualizację i będzie wymagać ponownego uruchomienia komputera w trakcie instalacji usługi ATA.

## Krok 1. Pobieranie i instalowanie centrum usługi ATA
Po sprawdzeniu, czy serwer spełnia wymagania, możesz kontynuować instalację centrum usługi ATA.

Na serwerze centrum usługi ATA wykonaj następujące kroki.

1.  Pobierz usługę ATA z [Centrum usługi licencjonowania zbiorowego firmy Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [Centrum ewaluacji TechNet](http://www.microsoft.com/en-us/evalcenter/) lub z [MSDN](https://msdn.microsoft.com/en-us/subscriptions/downloads).

2.  Zaloguj się na komputerze, na którym instalujesz centrum usługi ATA, jako użytkownik, który jest członkiem lokalnej grupy administratorów.

3.  Uruchom plik **Microsoft ATA Center Setup.EXE**, a następnie postępuj zgodnie z komunikatami kreatora instalacji.

4.  Jeśli nie zainstalowano platformy Microsoft .Net Framework, po rozpoczęciu instalacji otrzymasz monit o jej zainstalowanie. Po zakończeniu instalacji platformy .Net Framework może pojawić się prośba o ponowne uruchomienie.
5.  Na stronie **Zapraszamy** wybierz język do zastosowania na ekranach instalacji usługi ATA i kliknij przycisk **Dalej**.

6.  Przeczytaj Postanowienia licencyjne dotyczące oprogramowania firmy Microsoft. Jeśli je akceptujesz, kliknij pole wyboru, a następnie kliknij przycisk **Dalej**.

7.  Zaleca się ustawienie automatycznej aktualizacji usługi ATA. Jeśli system Windows nie został skonfigurowany do takiego działania na tym komputerze, zobaczysz ekran **Skorzystaj z usługi Microsoft Update do zapewnienia bezpieczeństwa i aktualizowania komputera**. 
    ![Obraz utrzymywania aktualnej usługi ATA](media/ata_ms_update.png)

8. Wybierz opcję **Użyj usługi Microsoft Update, gdy wyszukuję aktualizacje (zalecane)**. W ten sposób dostosujesz ustawienia systemu Windows, zezwalając na aktualizowanie innych produktów firmy Microsoft (w tym usługi ATA), jak wspomniano w tym miejscu. 
    ![Obraz automatycznej aktualizacji systemu Windows](media/ata_installupdatesautomatically.png)

8.  Na stronie **Konfiguracja centrum usługi ATA** wprowadź następujące informacje w zależności od używanego środowiska:

    |Pole|Opis|Komentarze|
    |---------|---------------|------------|
    |Ścieżka instalacji|Lokalizacja, w której zostanie zainstalowane centrum usługi ATA. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Center|Pozostaw wartość domyślną.|
    |Ścieżka danych bazy danych|Lokalizacja, w której zostaną umieszczone pliki bazy danych MongoDB. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Zmień lokalizację na taką, w której będzie wystarczająca ilość miejsca do przechowywania powiększającej się bazy danych na podstawie ustalonego rozmiaru. **Uwaga:** <ul><li>W środowiskach produkcyjnych należy użyć dysku z wystarczającą ilością miejsca, które zostało ustalone podczas planowania pojemności.</li><li>W przypadku dużych wdrożeń baza danych powinna znajdować się na oddzielnym dysku fizycznym.</li></ul>Aby uzyskać informacje dotyczące ustalania rozmiaru, zobacz [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).|
    |Adres IP centrum usługi ATA: port|Adres IP, na którym centrum usługi ATA będzie nasłuchiwać komunikacji z bram usługi ATA.<br /><br />**Port domyślny:** 443|Kliknij strzałkę w dół, aby wybrać adres IP, który będzie używany przez centrum usługi ATA.<br /><br />Adres IP i port centrum usługi ATA nie może być taki sam, jak adres IP i port konsoli usługi ATA. Upewnij się, że port konsoli usługi ATA został zmieniony.|
    |Certyfikat SSL centrum usługi ATA|Jest to certyfikat, który będzie używany przez centrum usługi ATA.|Kliknij ikonę klucza, aby wybrać zainstalowany certyfikat, lub zaznacz opcję Certyfikat z podpisem własnym w przypadku wdrażania w środowisku laboratoryjnym.|
    |Adres IP konsoli usługi ATA|Adres IP, który będzie używany przez usługi IIS na potrzeby konsoli usługi ATA.|Kliknij strzałkę w dół, aby wybrać adres IP używany przez konsolę usługi ATA. **Uwaga:** zapisz ten adres IP, aby ułatwić dostęp do konsoli usługi ATA z poziomu bramy usługi ATA.|
    |Certyfikat SSL konsoli usługi ATA|Certyfikat, który będzie używany przez usługi IIS.|Kliknij ikonę klucza, aby wybrać zainstalowany certyfikat, lub zaznacz opcję Certyfikat z podpisem własnym w przypadku wdrażania w środowisku laboratoryjnym.|

    ![Obraz przedstawiający konfigurowanie centrum usługi ATA](media/ATA-Center-Configuration.JPG)

10.  Kliknij przycisk **Zainstaluj**, aby zainstalować centrum usługi ATA i jego składniki.
    Następujące składniki zostaną zainstalowane i skonfigurowane podczas instalacji centrum usługi ATA:

    -   Internet Information Services (IIS)

    -   Centrum usługi ATA i witryna usług IIS konsoli usługi ATA

    -   Baza danych MongoDB

    -   Niestandardowy zestaw kolekcji danych monitora wydajności

    -   Certyfikaty z podpisem własnym (jeśli zostały wybrane podczas instalacji)

11.  Po zakończeniu instalacji kliknij polecenie **Uruchom**, aby nawiązać połączenie z konsolą usługi ATA.
W tym momencie zostanie automatycznie wyświetlona strona ustawień **Ogólne** umożliwiająca kontynuowanie konfiguracji i wdrażania bram usługi ATA.
Ponieważ logujesz się do witryny za pomocą adresu IP, zostanie wyświetlone ostrzeżenie związane z certyfikatem. Jest to normalne zachowanie. Możesz kliknąć przycisk **Kontynuuj przeglądanie tej witryny sieci Web**.

### Weryfikowanie instalacji

1.  Sprawdź, czy usługa o nazwie **Microsoft Advanced Threat Analytics Center** jest uruchomiona.
2.  Na pulpicie kliknij skrót do usługi **Microsoft Advanced Threat Analytics**, aby nawiązać połączenie z konsolą usługi ATA. Zaloguj się przy użyciu tych samych poświadczeń użytkownika, które zostały użyte do zainstalowania centrum usługi ATA.



>[!div class="step-by-step"] [« Przed rozpoczęciem instalacji](preinstall-ata.md)
[Krok 2 »](install-ata-step2.md)

## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO4-->


