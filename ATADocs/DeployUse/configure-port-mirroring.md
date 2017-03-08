---
title: "Konfigurowanie funkcji dublowania portów podczas wdrażania usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Zawiera opis opcji funkcji dublowania portów i sposobu ich konfigurowana na potrzeby usługi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f91c728614cbe03f794fd0ad45ccc19af712cf54
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="configure-port-mirroring"></a>Konfigurowanie funkcji dublowania portów
> [!NOTE] 
> Ten artykuł dotyczy wyłącznie sytuacji, gdy zamiast bram ATA Lightweight Gateway są wdrażane bramy usługi ATA. Aby ustalić, czy konieczne jest użycie bram usługi ATA, zobacz artykuł [Wybieranie odpowiednich bram dla wdrożenia](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment).
 
Główne źródło danych używane przez usługę ATA to głęboka inspekcja pakietów ruchu sieciowego do i z kontrolerów domeny. Aby ruch sieciowy był widoczny dla usługi ATA, należy skonfigurować funkcję dublowania portów lub skorzystać z podsłuchu sieci.

Na potrzeby funkcji dublowania portów należy skonfigurować **funkcję dublowania portów** dla każdego kontrolera domeny, który ma być monitorowany, jako **źródło** ruchu sieciowego. Zwykle w celu skonfigurowania funkcji dublowania portów konieczna jest współpraca z zespołem ds. sieci lub wirtualizacji.
Więcej informacji znajduje się w dokumentacji udostępnianej przez dostawcę.

Kontrolery domeny i bramy usługi ATA mogą być fizyczne lub wirtualne. Poniżej opisano typowe metody dublowania portów oraz pewne zagadnienia. Aby uzyskać dodatkowe informacje, zapoznaj się z dokumentacją przełącznika lub serwera wirtualizacji. Producent przełącznika może stosować inną terminologię.

**Switched Port Analyzer (SPAN)** — kopiuje ruch sieciowy z co najmniej jednego portu przełącznika do innego portu w ramach tego samego przełącznika. Zarówno brama usługi ATA, jak i kontrolery domeny muszą być podłączone do tego samego przełącznika fizycznego.

**Remote Switch Port Analyzer (RSPAN)** — umożliwia monitorowanie ruchu sieciowego z portów źródłowych znajdujących się w wielu przełącznikach fizycznych. Funkcja RSPAN kopiuje ruch źródłowy do specjalnej sieci VLAN skonfigurowanej na potrzeby funkcji RSPAN. Ta sieć VLAN musi być połączona magistralą z innymi przełącznikami korzystającymi z tej funkcji. Funkcja RSPAN działa w warstwie 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** — technologia stanowiąca własność firmy Cisco działająca w warstwie 3. Funkcja ERSPAN umożliwia monitorowanie ruchu w obrębie wielu przełączników bez konieczności używania magistral sieci VLAN. Funkcja ERSPAN używa protokołu Generic Routing Encapsulation (GRE) do kopiowania monitorowanego ruchu sieciowego. Aktualnie usługa ATA nie może bezpośrednio odbierać ruchu funkcji ERSPAN. Aby usługa ATA działała z ruchem funkcji ERSPAN, przełącznik lub router mogący dehermetyzować ruch musi zostać skonfigurowany jako miejsce docelowe funkcji ERSPAN, w którym ruch zostanie zdehermetyzowany. Następnie należy skonfigurować przełącznik lub router w taki sposób, aby ruch był przekazywany do bramy usługi ATA przy użyciu funkcji SPAN lub RSPAN.

> [!NOTE]
> Jeśli kontroler domeny, względem którego działa funkcja dublowania portów, korzysta z połączenia WAN, upewnij się, że połączenie WAN może obsłużyć dodatkowe obciążenie wynikające z ruchu funkcji ERSPAN.

## <a name="supported-port-mirroring-options"></a>Obsługiwane opcje funkcji dublowania portów

|Brama usługi ATA|Kontroler domeny|Uwagi|
|---------------|---------------------|------------------|
|Wirtualna|Wirtualny na tym samym hoście|Przełącznik wirtualny musi obsługiwać funkcję dublowania portów.<br /><br />Przeniesienie jednej z maszyn wirtualnych na inny host może spowodować przerwanie działania funkcji dublowania portów.|
|Wirtualna|Wirtualny na różnych hostach|Upewnij się, że ten scenariusz jest obsługiwany przez przełącznik wirtualny.|
|Wirtualna|Fizyczny|Wymaga dedykowanej karty sieciowej. W przeciwnym razie dla usługi ATA będzie widoczny cały ruch z i do hosta, nawet ruch wysyłany do centrum usługi ATA.|
|Fizyczny|Wirtualna|Upewnij się, że przełącznik wirtualny obsługuje ten scenariusz oraz konfigurację funkcji dublowania portów na przełącznikach fizycznych opartą na tym scenariuszu:<br /><br />Jeśli host wirtualny korzysta z tego samego przełącznika fizycznego, należy skonfigurować funkcję SPAN na poziomie przełącznika.<br /><br />Jeśli host wirtualny korzysta z innego przełącznika, należy skonfigurować funkcję RSPAN lub ERSPAN&#42;.|
|Fizyczny|Fizyczny — ten sam przełącznik|Przełącznik fizyczny musi obsługiwać funkcję SPAN lub funkcję dublowania portów.|
|Fizyczny|Fizyczny — inny przełącznik|Wymaga, aby przełączniki fizyczne obsługiwały funkcję RSPAN lub ERSPAN&#42;.|
&#42; Funkcja ERSPAN jest obsługiwana tylko wtedy, gdy przed przeanalizowaniem ruchu przez usługę ATA jest wykonywana dehermetyzacja.

> [!NOTE]
> Upewnij się, że różnica czasu ustawionego w kontrolerach domeny i bramach usługi ATA, z którymi te kontrolery nawiązują połączenie, nie jest większa niż 5 minut.

**W przypadku pracy z klastrami wirtualizacji:**

-   Dla każdego kontrolera domeny uruchomionego w klastrze wirtualizacji w ramach maszyny wirtualnej z bramą usługi ATA należy skonfigurować koligację między kontrolerem domeny a bramą usługi ATA. Dzięki temu po przeniesieniu kontrolera domeny do innego hosta w klastrze brama usługi ATA również zostanie przeniesiona. Takie rozwiązanie dobrze się sprawdza, gdy istnieje kilka kontrolerów domeny.
> [!NOTE]
> Jeśli Twoje środowisko obsługuje architekturę Virtual to Virtual na różnych hostach (RSPAN), nie musisz martwić się o koligację.
> 
-   Aby upewnić się, że bramy usługi ATA mają odpowiedni rozmiar do samodzielnego monitorowania wszystkich kontrolerów domeny, zainstaluj maszynę wirtualną na każdym hoście wirtualizacji, a następnie zainstaluj bramę usługi ATA na każdym hoście. Skonfiguruj każdą bramę usługi ATA do monitorowania wszystkich kontrolerów domeny uruchomionych w klastrze. W ten sposób będą monitorowane wszystkie hosty, na których działają kontrolery domeny.

Po skonfigurowaniu funkcji dublowania portów, ale przed zainstalowaniem bramy usługi ATA, zweryfikuj, czy funkcja dublowania portów działa.

## <a name="see-also"></a>Zobacz też
- [Weryfikowanie funkcji dublowania portów](validate-port-mirroring.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
