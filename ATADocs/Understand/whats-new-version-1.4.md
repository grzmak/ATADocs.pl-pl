---
title: "Co nowego w wersji 1.4 usługi ATA | Microsoft Advanced Threat Analytics"
description: "Zawiera listę nowych funkcji oraz znanych problemów w wersji 1.4 usługi ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 3f7e2b32c43966cbb1adab1f88dd0e197313de65


---

# Co nowego w wersji 1.4 usługi ATA
Te informacje o wersji zawierają znane problemy w wersji 1.4 usługi Advanced Threat Analytics.

## Co nowego w tej wersji?

-   Obsługa funkcji przekazywania zdarzeń systemu Windows służącej do wysyłania zdarzeń bezpośrednio z kontrolerów domeny do bramy usługi ATA.

-   Ulepszenia funkcji wykrywania ataków typu Pass-The-Hash dotyczących zasobów firmowych polegające na połączeniu głębokiej inspekcji pakietów i dzienników zdarzeń systemu Windows.

-   Ulepszenia obsługi urządzeń niedołączonych do domeny oraz urządzeń z systemem innym niż Windows dotyczące wykrywania i widoczności.

-   Ulepszenia wydajności umożliwiające obsługę większego ruchu przez pojedynczą bramę usługi ATA.

-   Ulepszenia wydajności umożliwiające obsługę większej liczby bram usługi ATA przez pojedyncze centrum usługi ATA.

-   Dodano nowy proces automatycznego rozpoznawania nazw, który dopasowuje nazwy komputerów i adresy IP — ta wyjątkowa możliwość oszczędzi cenny czas w procesie dochodzenia i zapewni silne dowody dla analityków zabezpieczeń.

-   Ulepszona możliwość gromadzenia danych wejściowych od użytkowników w celu automatycznego dostosowania procesu wykrywania.

-   Automatyczne wykrywanie urządzeń NAT.

-   Automatyczne przełączanie w tryb failover, gdy kontrolery domeny są niedostępne.

-   Funkcja monitorowania kondycji systemu i powiadomień zapewnia teraz informacje o ogólnej kondycji wdrożenia oraz o określonych problemach związanych z konfiguracją i łącznością.

-   Wgląd w lokacje i lokalizacje, w których działają jednostki.

-   Obsługa wielu domen.

-   Obsługa domen z nazwą bez rozszerzenia.

-   Obsługa modyfikowania adresu IP i certyfikatu bram usługi ATA oraz centrum usługi ATA.

-   Telemetria umożliwiająca poprawę środowiska użytkownika.

## Znane problemy
W tej wersji występują następujące znane problemy.

### Oprogramowanie do przechwytywania ruchu sieciowego
Jedynym obsługiwanym oprogramowaniem do przechwytywania ruchu sieciowego, które można zainstalować na bramie usługi ATA, jest program [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865). Nie należy instalować programu Microsoft Message Analyzer ani żadnego innego oprogramowania do przechwytywania ruchu sieciowego. Zainstalowanie innego oprogramowania spowoduje nieprawidłowe działanie bramy usługi ATA.

### Instalacja z pliku Zip
Podczas instalacji bramy usługi ATA należy wyodrębnić pliki z pliku zip do katalogu lokalnego i zainstalować ją z tej lokalizacji. Nie należy instalować bramy usługi ATA bezpośrednio z pliku zip, ponieważ instalacja zakończy się niepowodzeniem.

### Odinstalowywanie poprzednich wersji usługi ATA
Jeśli zainstalowano poprzednią wersję usługi ATA, publiczną wersję zapoznawczą lub prywatną wersję zapoznawczą, należy odinstalować centrum usługi ATA i bramy usługi ATA przed zainstalowaniem tej wersji usługi ATA.

Należy również usunąć pliki bazy danych i pliki dziennika. Bazy danych poprzednich wersji usługi ATA nie są zgodne z wersją GA usługi ATA.

Jeśli podczas próby odinstalowania centrum ATA lub bramy ATA zamiast procesu odinstalowania usługi ATA zostanie uruchomiony proces instalowania, należy dodać następujący klucz rejestru, a następnie ponownie odinstalować usługę ATA.

**Centrum usługi ATA**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   Dodaj nową wartość ciągu o nazwie `InstallationPath` i wartości `C:\Program Files\Microsoft Advanced Threat Analytics\Center`. To jest domyślny folder instalacji. Jeśli folder instalacji został zmieniony, wprowadź ścieżkę, w której zainstalowano usługę ATA.

    ![Wprowadzanie ścieżki instalacji centrum usługi ATA w edytorze rejestru](media/ATA-uninstall-center-bug.jpg)

**Brama usługi ATA**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   Dodaj nową wartość ciągu o nazwie `InstallationPath` i wartości `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway`. To jest domyślny folder instalacji.  Jeśli folder instalacji został zmieniony, wprowadź ścieżkę, w której zainstalowano usługę ATA.

    ![Wprowadzanie ścieżki instalacji bramy usługi ATA w edytorze rejestru](media/ATA-GW-uninstall-bug.jpg)

Po odinstalowaniu usuń folder instalacji w centrum usługi ATA i bramie usługi ATA.  Jeśli baza danych została zainstalowana w oddzielnym folderze, usuń folder bazy danych w centrum usługi ATA.

### Alert dotyczący kondycji — rozłączona brama usługi ATA
Jeśli istnieje więcej niż jedna brama usługi ATA i korzystasz z alertów dotyczących rozłączenia bramy ATA, funkcja automatycznego rozwiązywania będzie działać tylko dla jednej z nich, a reszta pozostanie w stanie Otwarte. Należy ręcznie potwierdzić, że brama usługi ATA jest uruchomiona oraz że usługa działa, a następnie ręcznie rozwiązać alert.

### Aktualizacja na hoście wirtualizacji
Nie należy instalować aktualizacji KB 3047154 na hoście wirtualizacji. Może to spowodować nieprawidłowe działanie funkcji dublowania portów.

## Zobacz też

[Aktualizacja usługi ATA do wersji 1.6 — przewodnik migracji](ata-update-1.6-migration-guide.md)

[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


<!--HONumber=Jun16_HO4-->


