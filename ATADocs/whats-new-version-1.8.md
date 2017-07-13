---
title: "Co nowego w wersji 1.8 usługi ATA | Microsoft Docs"
description: "Zawiera listę nowych funkcji oraz znanych problemów w wersji 1.8 usługi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: f2a4ed151db38497a6cec977f1090faf2eb4133e
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2017
---
# Co nowego w wersji 1.8 usługi ATA
<a id="whats-new-in-ata-version-18" class="xliff"></a>
Te informacje o wersji obejmują aktualizacje, nowe funkcje, poprawki i znane problemy w tej wersji usługi Advanced Threat Analytics.



## Nowe i zaktualizowane funkcje wykrywania
<a id="new--updated-detections" class="xliff"></a>

- Implementacja nietypowego protokołu została ulepszona, aby umożliwić wykrycie złośliwego oprogramowania WannaCry.

- NOWOŚĆ! **Odbiegająca od normy modyfikacja poufnych grup** — W fazie podwyższenia poziomu uprawnień osoby atakujące modyfikują grupy z wysokim poziomem uprawnień w celu uzyskania dostępu do wrażliwych zasobów. Usługa ATA wykrywa teraz odbiegające od normy zmiany w grupach z podwyższonym poziomem uprawnień.
- NOWOŚĆ! **Podejrzane niepowodzenia uwierzytelniania** (behawioralne ataki siłowe) — osoby atakujące usiłują użyć ataku siłowego na poświadczenia, aby naruszyć bezpieczeństwo kont. Usługa ATA zgłasza teraz alert po wykryciu odbiegających od normy niepowodzeń uwierzytelniania.   

- **Próba zdalnego wykonania kodu — metoda WMI exec** — osoby atakujące mogą próbować kontrolować sieć, zdalnie uruchamiając kod na kontrolerze domeny. Usługa ATA ma rozszerzone wykrywanie zdalnego wykonywania kodu w celu uwzględnienia wykrywania metod WMI do zdalnego uruchamiania kodu.

- Rekonesans przy użyciu zapytań usługi katalogowej — to wykrywanie zostało rozszerzone, aby można było przechwycić zapytania względem pojedynczej wrażliwej jednostki i zmniejszyć liczbę fałszywych alarmów, które były generowane w poprzedniej wersji. Jeśli ta funkcja została wyłączona w wersji 1.7, to zainstalowanie wersji 1.8 włączy ją teraz automatycznie.

- Działanie biletu uwierzytelniania Golden Ticket protokołu Kerberos — usługa ATA 1.8 zawiera dodatkową technikę do wykrywania ataków na bilet uwierzytelniania Golden Ticket.
    - Usługa ATA wykrywa teraz podejrzane działania, w których okres istnienia biletu uwierzytelniania Golden Ticket wygasł. Jeśli bilet protokołu Kerberos jest używany przez więcej niż dozwolony okres istnienia, usługa ATA wykryje go jako podejrzane działanie oznaczające, że prawdopodobnie został utworzony bilet uwierzytelniania Golden Ticket.
- Aby usunąć znane fałszywe alarmy, wprowadzono ulepszenia następujących wykryć:  
    - Wykrywanie podwyższenia poziomu uprawnień (sfałszowany element PAC) 
    - Działanie obniżenia poziomu szyfrowania (wytrych)
    - Implementacja nietypowego protokołu
    - Zerwanie relacji zaufania

## Ulepszona klasyfikacja podejrzanych działań
<a id="improved-triage-of-suspicious-activities" class="xliff"></a>

-   NOWOŚĆ! Usługa ATA 1.8 umożliwia uruchamianie następujących akcji podejrzanych działań w trakcie procesu klasyfikacji: 
    - **Wykluczanie jednostek** ze zgłaszania przyszłych podejrzanych działań, aby zapobiec alertom, gdy usługa ATA wykryje niegroźne fałszywe alarmy (na przykład uruchamianie zdalnego kodu przez administratora lub wykrywanie skanerów zabezpieczeń).
    - **Pomijanie powtarzających się** podejrzanych działań z generowania alertów.
    - **Usuwanie podejrzanych działań** z osi czasu ataków.
-   Proces wykonywania kolejnych czynności dla alertów podejrzanych działań jest teraz efektywniejszy. Oś czasu podejrzanych działań została przeprojektowana. W usłudze ATA 1.8 będzie można wyświetlić o wiele więcej podejrzanych działań na jednym ekranie zawierającym lepsze informacje dla celów klasyfikacji i badania. 

## Nowe raporty pomagają w badaniach
<a id="new-reports-to-help-you-investigate" class="xliff"></a> 
-   NOWOŚĆ! Dodano **raport z podsumowaniem** w celu umożliwienia wyświetlenia wszystkich danych podsumowania z usługi ATA, w tym podejrzanych działań, problemów z kondycją itd. Możesz nawet określić dostosowany raport, który jest automatycznie generowany cyklicznie.
-   NOWOŚĆ! Dodano **raport wrażliwych grup** w celu umożliwienia wyświetlenia wszystkich zmian wprowadzonych we wrażliwych grupach w danym okresie.


## Ulepszenia infrastruktury
<a id="infrastructure-improvements" class="xliff"></a>

-   Wydajność centrum usługi ATA została ulepszona. W usłudze ATA 1.8 centrum usługi ATA może obsługiwać więcej niż 1 mln pakietów na sekundę.
-   Uproszczona brama usługi ATA może teraz odczytywać zdarzenia lokalnie — bez potrzeby konfigurowania przekazywania zdarzeń.
-   Ulepszenie ułatwień dostępu — usługa ATA wraz z firmą Microsoft zapewniają produkt, który jest dostępny dla wszystkich użytkowników. 
-   Możesz teraz oddzielnie skonfigurować pocztę e-mail do monitorowania alertów i podejrzanych działań.

## Ulepszenia zabezpieczeń
<a id="security-improvements" class="xliff"></a>

-   NOWOŚĆ! **Logowanie jednokrotne do zarządzania usługą ATA**. Usługa ATA obsługuje logowanie jednokrotne zintegrowane z uwierzytelnianiem systemu Windows — jeśli użytkownik jest już zalogowany na komputerze, usługa ATA użyje tego tokenu do zalogowania na konsoli usługi ATA. Możesz również się zalogować przy użyciu karty inteligentnej. Skrypty instalacji dyskretnej dla bramy usługi ATA i uproszczonej bramy usługi ATA używają teraz kontekstu zalogowanego użytkownika bez konieczności podawania poświadczeń.
-   Lokalne uprawnienia systemu zostały usunięte z procesu bramy usługi ATA, dzięki czemu można teraz używać kont wirtualnych (dostępnych tylko dla autonomicznych bram usługi ATA), zarządzanych kont usług i kont usług zarządzanych przez grupę do uruchamiania procesu bramy usługi ATA.   
-   Zostały dodane dzienniki inspekcji dla centrum usługi ATA i bram. Wszystkie akcje są obecnie rejestrowane w dzienniku zdarzeń systemu Windows.
-   Dodano obsługę certyfikatów dostawcy magazynu kluczy dla centrum usługi ATA.




## Zobacz też
<a id="see-also" class="xliff"></a>
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.8 — przewodnik migracji](ata-update-1.8-migration-guide.md)

