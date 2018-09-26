---
title: Architektura zaawansowanej ochrony przed zagrożeniami na platformie Azure | Dokumentacja firmy Microsoft
description: W tym artykule opisano architekturę z usługi Azure Advanced Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fb9e99d43a800f6b7bc080fa3fe0bc2453f3d754
ms.sourcegitcommit: 8e80f59409c65e7d8d60ec7de8b96b621795699a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2018
ms.locfileid: "47168573"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="azure-atp-architecture"></a>Architektura zaawansowanej ochrony przed zagrożeniami na platformie Azure

Narzędzie Azure ATP monitoruje kontrolery domeny przez przechwytywania i analizowania ruchu sieciowego i wykorzystując zdarzenia Windows (bezpośrednio z kontrolerów domeny lub z serwera SIEM) i analizuje je pod kątem ataków i zagrożeń. Przy użyciu profilowania, wykrywanie deterministyczne, uczenie maszynowe i algorytmy behawioralne, które narzędzia Azure ATP uzyskuje informacje o sieci, włącza wykrywanie anomalii i ostrzega o podejrzanych działaniach.

Architektura zaawansowanej ochrony przed zagrożeniami na platformie Azure:

![Diagram topologii architektury usługi Azure ATP](media/atp-architecture-topology.png)

W tej sekcji opisano, jak działa przepływ sieci i Przechwytywanie zdarzeń usługi Azure ATP i podano bardziej szczegółowe informacje dotyczące funkcjonalności głównych składników: portal usługi Azure ATP, czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i usługi w chmurze usługi Azure ATP. 

Zainstalowany bezpośrednio na kontrolerach domeny, czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure uzyskuje dostęp do wymaganych dzienników zdarzeń bezpośrednio z poziomu kontrolera domeny. Po ruchu sieciowego i dzienniki są analizowane przez czujnik, narzędzia Azure ATP wysyła przeanalizowane informacje do usługi w chmurze usługi Azure ATP (określonego odsetka dzienniki są wysyłane). 

## <a name="azure-atp-components"></a>Składniki usługi Azure ATP
Narzędzie Azure ATP składa się z następujących składników:

-   **Witryna Azure portal zaawansowanej ochrony przed zagrożeniami** <br>
Portal usługi Azure ATP pozwala na tworzenie wystąpienia usługi Azure ATP, wyświetla danych odebranych z czujników narzędzia Azure ATP i pozwala na monitorowanie, zarządzanie i badanie zagrożeń w danym środowisku sieciowym.  

-   **Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami**<br>
Usługa Azure ATP czujników są instalowane bezpośrednio na kontrolerach domeny. Czujnik bezpośrednio monitoruje ruch kontrolerów domeny, bez konieczności użycia serwera dedykowanego lub funkcji dublowania portów.

-   **Usługa w chmurze Azure ATP**<br>
Usługa w chmurze Azure ATP jest uruchamiany w infrastrukturze platformy Azure i jest obecnie wdrożona w Stanach Zjednoczonych, Europie i Azji. Usługa w chmurze Azure ATP jest podłączony do firmy Microsoft usługę intelligent security graph. 

## <a name="azure-atp-portal"></a>Witryna Azure portal zaawansowanej ochrony przed zagrożeniami 
Użyj portalu usługi Azure ATP:
- Tworzenie wystąpienia usługi Azure ATP
- Integracja z innymi usługami zabezpieczeń firmy Microsoft 
- Zarządzanie ustawieniami konfiguracji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure 
- Wyświetlanie danych odebranych z czujników narzędzia Azure ATP
- Monitorowanie wykrytych podejrzanych działań i potencjalnie złośliwych programów ataki oparte na modelu łańcuchu kończenia ataku
- **Opcjonalnie**: portalu można również skonfigurować do wysyłania wiadomości e-mail i zdarzeń po wykryciu alerty zabezpieczeń lub problemów z kondycją

> [!NOTE]
> - Jeśli nie czujnik jest zainstalowany w obszarze roboczym usługi w ciągu 60 dni, obszaru roboczego mogą zostać usunięte, a użytkownik będzie należy utworzyć ją ponownie.

## <a name="azure-atp-sensor"></a>Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami
Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure zawiera następujące podstawowe funkcje:
- Przechwytują i sprawdzają ruch sieciowy kontrolera domeny (ruch lokalny kontrolera domeny)
- Odbieranie zdarzeń Windows bezpośrednio z kontrolerów domeny 
- Odbieranie informacji o kontach usługi RADIUS z dostawcę sieci VPN
- Pobierają dane o użytkownikach i komputerach z domeny usługi Active Directory
- Przeprowadzają rozpoznawanie jednostek sieci (użytkowników, grup i komputerów)
- Transferują odpowiednie dane do usługi w chmurze usługi Azure ATP
> [!NOTE]
> - Domyślnie narzędzia Azure ATP obsługuje maksymalnie 100 czujników. Jeśli chcesz zainstalować więcej się z pomocą techniczną usługi Azure ATP.
 
## <a name="azure-atp-sensor-features"></a>Funkcje platformy Azure czujnika zaawansowanej ochrony przed zagrożeniami
Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami odczytuje zdarzenia lokalnie — bez konieczności zakupu i obsługa dodatkowego sprzętu ani konfiguracji. Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure obsługuje również zdarzeń wątku dla Windows (ETW) zawiera informacje dziennika dla wielu wykrywania. ETW oparte odmiany to między innymi podejrzane żądania replikacji i podejrzane podwyższania poziomu kontrolera domeny, są potencjalnymi atakami kontrolera domeny w tle.
- Kandydat synchronizatora domeny

    Kandydat Synchronizatora domeny jest odpowiedzialna za aktywne synchronizowanie wszystkich jednostek z określonej domeny usługi Active Directory (podobnie do mechanizmu używanego przez kontrolery domeny w przypadku replikacji). Jeden czujnik jest wybierany losowo, z listy kandydatów, która będzie służyć jako Synchronizator domeny. 

    Jeśli synchronizator będzie w trybie offline przez ponad 30 minut, zamiast niego zostanie wybrany inny kandydat. Jeśli żadnego Synchronizatora domeny jest dostępny dla określonej domeny, usługi Azure ATP aktywnie synchronizuje jednostek i ich zmian, jednak narzędzia Azure ATP pobiera nowe jednostki po ich wykryciu w monitorowanym ruchu. 
    
    Jeśli żadnego Synchronizatora domeny jest dostępny i wyszukiwać jednostkę, które nie mają cały ruch odnoszących się do niego, są wyświetlane żadne wyniki wyszukiwania.

    Domyślnie narzędzia Azure ATP czujników nie są kandydatami Synchronizatora. Aby ręcznie ustawić czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jako kandydat Synchronizatora domeny, wykonaj kroki opisane w [przepływ pracy instalacji narzędzia Azure ATP](install-atp-step5.md#step-5-configure-the-azure-atp-sensor-settings).
- Ograniczenia zasobów

    Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure zawiera składnik monitorowania, który ocenia dostępne moc obliczeniową i pamięć na kontrolerze domeny, na którym jest uruchomiony. Proces monitorowania jest wykonywana co 10 sekund i dynamicznie aktualizuje przydział użycia procesora CPU i pamięci na temat procesu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Proces monitorowania sprawia, że się, że kontroler domeny zawsze ma co najmniej 15% wolnego zasobów obliczeniowych i pamięci dostępnych zasobów.

    Bez względu na to zachowanie występujące na kontrolerze domeny proces monitorowania stale zwolnienie zasobów, aby upewnić się, że podstawowa funkcjonalność kontrolera domeny nigdy nie ma wpływu.

    Jeśli proces monitorowania powoduje czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure brakować zasobów, tylko część ruchu będzie monitorowana, a alert monitorowania "Opuszczono ruch po dublowaniu portów sieciowych" pojawia się na stronie kondycji z portalu usługi Azure ATP.

-  Zdarzenia Windows

    Aby zwiększyć pokrycie wykrywania usługi Azure ATP Pass--Hash, podejrzane błędy uwierzytelniania, modyfikacji wrażliwych grup, tworzenie podejrzanego usług i typy działań wystawionego jako przynęta ataku, potrzeb zaawansowanej ochrony przed zagrożeniami w usłudze Azure do analizy dzienników z następujących czynności Zdarzenia Windows: 4776,4732,4733,4728,4729,4756,4757 i 7045. Te zdarzenia są odczytywane automatycznie przez czujniki narzędzia Azure ATP z poprawną [Zaawansowane ustawienia zasad inspekcji](atp-advanced-audit-policy.md). 

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/trisizingtool)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie składnika przesyłanie dalej zdarzeń](configure-event-forwarding.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
