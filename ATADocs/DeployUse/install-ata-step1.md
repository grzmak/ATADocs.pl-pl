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
[« Przed rozpoczęciem instalacji](install-ata-preinstall.md)
[Krok 2 »](install-ata-step2.md)

## Krok 1. Pobieranie i instalowanie centrum usługi ATA
Po sprawdzeniu, czy serwer spełnia wymagania, możesz kontynuować instalację centrum usługi ATA.

Na serwerze centrum usługi ATA wykonaj następujące kroki.

1.  Pobierz usługę ATA z witryny [TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/)..

2.  Zaloguj się jako użytkownik będący członkiem lokalnej grupy administratorów.

3.  Z poziomu wiersza polecenia z podwyższonym poziomem uprawnień uruchom plik Microsoft ATA Center Setup.EXE, a następnie postępuj zgodnie z komunikatami kreatora instalacji.

4.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**..

5.  Przeczytaj umowę licencyjną użytkownika oprogramowania. Jeśli akceptujesz jej warunki, kliknij przycisk **Dalej**..

6.  Na stronie **Konfiguracja centrum** wprowadź następujące informacje w zależności od używanego środowiska:

    |Pole|Opis|Komentarze|
    |---------|---------------|------------|
    |Ścieżka instalacji|Lokalizacja, w której zostanie zainstalowane centrum usługi ATA. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Center|Pozostaw wartość domyślną.|
    |Ścieżka danych bazy danych|Lokalizacja, w której zostaną umieszczone pliki bazy danych MongoDB. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Zmień lokalizację na taką, w której będzie wystarczająca ilość miejsca do przechowywania powiększającej się bazy danych na podstawie ustalonego rozmiaru. **Uwaga:** <ul><li>W środowiskach produkcyjnych należy użyć dysku z wystarczającą ilością miejsca, które zostało ustalone podczas planowania pojemności.</li><li>W przypadku dużych wdrożeń baza danych powinna znajdować się na oddzielnym dysku fizycznym.</li></ul>Aby uzyskać informacje dotyczące ustalania rozmiaru, zobacz [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).|
    |Ścieżka dziennika bazy danych|Lokalizacja, w której zostaną umieszczone pliki dziennika bazy danych. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal|W przypadku dużych wdrożeń dziennik bazy danych powinien znajdować się na innym dysku fizycznym niż baza danych i system. Zmień lokalizację na taką, w której będzie wystarczająca ilość miejsca do przechowywania dziennika bazy danych.|
    |Adres IP centrum usługi ATA: port|Adres IP, na którym centrum usługi ATA będzie nasłuchiwać komunikacji z bram usługi ATA.<br /><br />**Port domyślny:** 443|Kliknij strzałkę w dół, aby wybrać adres IP, który będzie używany przez centrum usługi ATA.<br /><br />Adres IP i port centrum usługi ATA nie może być taki sam, jak adres IP i port konsoli usługi ATA. Upewnij się, że port konsoli usługi ATA został zmieniony.|
    |Certyfikat SSL centrum usługi ATA|Jest to certyfikat, który będzie używany przez centrum usługi ATA.|Kliknij ikonę klucza, aby wybrać zainstalowany certyfikat, lub zaznacz opcję Certyfikat z podpisem własnym w przypadku wdrażania w środowisku laboratoryjnym.|
    |Adres IP konsoli usługi ATA|Adres IP, który będzie używany przez usługi IIS na potrzeby konsoli usługi ATA.|Kliknij strzałkę w dół, aby wybrać adres IP używany przez konsolę usługi ATA. **Uwaga:** zapisz ten adres IP, aby ułatwić dostęp do konsoli usługi ATA z poziomu bramy usługi ATA.|
    |Certyfikat SSL konsoli usługi ATA|Certyfikat, który będzie używany przez usługi IIS.|Kliknij ikonę klucza, aby wybrać zainstalowany certyfikat, lub zaznacz opcję Certyfikat z podpisem własnym w przypadku wdrażania w środowisku laboratoryjnym.|
    ![Obraz przedstawiający konfigurowanie centrum usługi ATA](media/ATA-Center-Configuration.JPG)

7.  Kliknij polecenie **Zainstaluj**, aby zainstalować usługę ATA i jej składniki oraz utworzyć połączenie między centrum usługi ATA i konsolą usługi ATA.

8.  Po zakończeniu instalacji kliknij polecenie **Uruchom**, aby nawiązać połączenie z konsolą usługi ATA.

    Następujące składniki zostaną zainstalowane i skonfigurowane podczas instalacji centrum usługi ATA:

    -   Internet Information Services (IIS)

    -   Baza danych MongoDB

    -   Centrum usługi ATA i witryna usług IIS konsoli usługi ATA

    -   Niestandardowy zestaw kolekcji danych monitora wydajności

    -   Certyfikaty z podpisem własnym (jeśli zostały wybrane podczas instalacji)

> [!NOTE]
> Aby ułatwić rozwiązywanie problemów i rozszerzanie produktu, zaleca się zainstalowanie dodatku MongoVue oraz wszelkich innych dodatków bazy danych MongoDB (bądź dowolnego wybranego narzędzia innej firmy). Dodatek MongoVue wymaga zainstalowania platformy .NET Framework 3.5.

### Weryfikowanie instalacji

1.  Sprawdź, czy centrum usługi Microsoft Advanced Threat Analytics jest uruchomione.

2.  Na pulpicie kliknij skrót do usługi Microsoft Advanced Threat Analytics, aby nawiązać połączenie z konsolą usługi ATA. Zaloguj się przy użyciu tych samych poświadczeń użytkownika, które zostały użyte do zainstalowania centrum usługi ATA. Po pierwszym zalogowaniu się do konsoli usługi ATA zostanie automatycznie wyświetlona strona **Ustawienia łączności domeny** umożliwiająca kontynuowanie konfiguracji i wdrażania bram usługi ATA.

3.  Przejrzyj plik błędów **Microsoft.Tri.Center-Errors.log**, który można znaleźć w następującej lokalizacji domyślnej: %programfiles%\Microsoft Advanced Threat Analytics\Center\Logs.

>[!div class="step-by-step"]
[« Przed rozpoczęciem instalacji](install-ata-preinstall.md)
[Krok 2 »](install-ata-step2.md)

## Zobacz też

- [Aby uzyskać pomoc techniczną, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/plan-design/configure-event-collection)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Apr16_HO4-->


