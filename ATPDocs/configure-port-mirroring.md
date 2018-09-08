---
title: Konfigurowanie funkcji dublowania portów podczas wdrażania usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Zawiera opis opcji funkcji dublowania portów i sposobu ich konfigurowana na potrzeby usługi Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ac3c584f5eb73b33415c6c1250eee4c41a12763
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125995"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="configure-port-mirroring"></a>Konfigurowanie funkcji dublowania portów
> [!NOTE] 
> Ten artykuł dotyczy tylko wtedy, gdy wdrażanie usługi Azure ATP czujnik autonomiczny zamiast czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Aby określić, jeśli musisz użyć narzędzia Azure ATP czujnik autonomiczny, zobacz [czujników odpowiednie dla danego wdrożenia wybór](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Główne źródło danych używane przez usługi Azure ATP to głęboka inspekcja pakietów ruchu sieciowego do i z kontrolerów domeny. Dla usługi Azure ATP się ruch sieciowy musisz Konfigurowanie funkcji dublowania portów lub skorzystać z PODSŁUCHU sieci.

Na potrzeby funkcji dublowania portów należy skonfigurować **funkcję dublowania portów** dla każdego kontrolera domeny, który ma być monitorowany, jako **źródło** ruchu sieciowego. Zazwyczaj potrzebne do pracy z zespołem sieci lub wirtualizacji, aby skonfigurować funkcję dublowania portów.
Aby uzyskać więcej informacji zobacz dokumentacji udostępnianej przez dostawcę.

Kontrolery domeny i usługi Azure ATP czujnik autonomiczny, może być fizyczne lub wirtualne. Poniżej opisano typowe metody dublowania portów oraz pewne zagadnienia. Aby uzyskać więcej informacji zobacz dokumentację produktu przełącznika lub wirtualizacji serwera. Producent przełącznika może stosować inną terminologię.

**Switched Port Analyzer (SPAN)** — kopiuje ruch sieciowy z co najmniej jednego portu przełącznika do innego portu w ramach tego samego przełącznika. Zarówno usługi Azure ATP autonomiczny czujników i kontrolery domeny musi być podłączony do tego samego przełącznika fizycznego.

**Remote Switch Port Analyzer (RSPAN)** — umożliwia monitorowanie ruchu sieciowego z portów źródłowych znajdujących się w wielu przełącznikach fizycznych. Funkcja RSPAN kopiuje ruch źródłowy do specjalnej sieci VLAN skonfigurowanej na potrzeby funkcji RSPAN. Ta sieć VLAN musi być połączona magistralą z innymi przełącznikami korzystającymi z tej funkcji. Funkcja RSPAN działa w warstwie 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** — technologia stanowiąca własność firmy Cisco działająca w warstwie 3. Funkcja ERSPAN umożliwia monitorowanie ruchu w obrębie wielu przełączników bez konieczności używania magistral sieci VLAN. Funkcja ERSPAN używa protokołu Generic Routing Encapsulation (GRE) do kopiowania monitorowanego ruchu sieciowego. Wartość narzędzie Azure ATP aktualnie nie może bezpośrednio odbierać ruchu funkcji ERSPAN. Do usługi Azure ATP do pracy z ruchu funkcji ERSPAN przełącznik lub router mogący dehermetyzować ruch musi zostać skonfigurowany jako miejsce docelowe funkcji erspan, w których ruch jest po dehermetyzacji. Następnie należy skonfigurować przełącznik lub router przesyłanie ruchu sieciowego po dehermetyzacji do usługi Azure ATP czujnik autonomiczny, za pomocą SPAN lub RSPAN.

> [!NOTE]
> Jeśli kontroler domeny, względem którego działa funkcja dublowania portów, korzysta z połączenia WAN, upewnij się, że połączenie WAN może obsłużyć dodatkowe obciążenie wynikające z ruchu funkcji ERSPAN.
> Narzędzie Azure ATP obsługuje tylko monitorowanie ruchu, gdy ruch trafia karty Sieciowej i kontrolera domeny w taki sam sposób. Narzędzie Azure ATP nie obsługuje monitorowanie ruchu, gdy jest on dzielony na różne porty.

## <a name="supported-port-mirroring-options"></a>Obsługiwane opcje funkcji dublowania portów

|Czujnik autonomiczny usługi Azure ATP|Kontroler domeny|Uwagi|
|---------------|---------------------|------------------|
|Wirtualna|Wirtualny na tym samym hoście|Przełącznik wirtualny musi obsługiwać funkcję dublowania portów.<br /><br />Przeniesienie jednej z maszyn wirtualnych na inny host może spowodować przerwanie działania funkcji dublowania portów.|
|Wirtualna|Wirtualny na różnych hostach|Upewnij się, że ten scenariusz jest obsługiwany przez przełącznik wirtualny.|
|Wirtualna|Fizyczny|Wymaga dedykowanej karty sieciowej w przeciwnym razie narzędzia Azure ATP widzi całego ruchu pochodzącego z hosta, nawet ruch wysyłany do usługi w chmurze usługi Azure ATP.|
|Fizyczny|Wirtualna|Upewnij się, że przełącznik wirtualny obsługuje ten scenariusz oraz konfigurację funkcji dublowania portów na przełącznikach fizycznych opartą na tym scenariuszu:<br /><br />Jeśli host wirtualny korzysta tego samego przełącznika fizycznego, należy skonfigurować span na poziomie przełącznika.<br /><br />Jeśli host wirtualny korzysta z innego przełącznika, należy skonfigurować funkcję RSPAN lub ERSPAN&#42;.|
|Fizyczny|Fizyczny — ten sam przełącznik|Przełącznik fizyczny musi obsługiwać funkcję SPAN lub funkcję dublowania portów.|
|Fizyczny|Fizyczny — inny przełącznik|Wymaga, aby przełączniki fizyczne obsługiwały funkcję RSPAN lub ERSPAN&#42;.|

&#42;Funkcja ERSPAN jest obsługiwana tylko po dehermetyzacji jest wykonywane przed ruchu są analizowane przez zaawansowanej ochrony przed zagrożeniami.

> [!NOTE]
> Upewnij się, że kontrolery domeny i usługi Azure ATP czujnik autonomiczny, z którą się łączą jest różnica czasu ustawionego pięciu minut od siebie nawzajem.

**W przypadku pracy z klastrami wirtualizacji:**

-   Dla każdego kontrolera domeny działających w klastrze wirtualizacji w maszynie wirtualnej za pomocą narzędzia Azure ATP czujnik autonomiczny należy skonfigurować koligację między kontrolerem domeny i czujnik autonomiczny narzędzia Azure ATP. Dzięki temu po przeniesieniu kontrolera domeny do innego hosta w klastrze usługi Azure ATP czujnik autonomiczny po nim następuje. Takie rozwiązanie dobrze się sprawdza, gdy istnieje kilka kontrolerów domeny.

 > [!NOTE]
 > Jeśli Twoje środowisko obsługuje architekturę Virtual to Virtual na różnych hostach (RSPAN), nie musisz martwić się o koligację.
 
-   Użyj tej opcji, aby upewnić się, czujnik autonomiczny narzędzia Azure ATP mają odpowiedni rozmiar do samodzielnego monitorowania wszystkich kontrolerów domeny samodzielnie,: Zainstaluj maszynę wirtualną na każdym hoście wirtualizacji i zainstalować narzędzia Azure ATP czujnik autonomiczny na każdym hoście. Skonfiguruj każdy czujnik autonomiczny narzędzia Azure ATP do monitorowania wszystkich kontrolerów domeny, które działają w klastrze. W ten sposób dowolnego hosta, na którym działają na kontrolery domeny są monitorowane.

Po skonfigurowaniu funkcji dublowania portów, sprawdź, czy funkcja dublowania portów działa przed zainstalowaniem narzędzia Azure ATP czujnik autonomiczny.

## <a name="see-also"></a>Zobacz też
- [Konfigurowanie składnika przesyłanie dalej zdarzeń](configure-event-forwarding.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
