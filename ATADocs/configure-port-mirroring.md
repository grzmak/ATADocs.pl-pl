---
title: Konfigurowanie funkcji dublowania portów podczas wdrażania usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Zawiera opis opcji funkcji dublowania portów i sposobu ich konfigurowana na potrzeby usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9ed585d37363fbae2604fe0ea705a0ea30b9b283
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010299"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="configure-port-mirroring"></a>Konfigurowanie funkcji dublowania portów
> [!NOTE] 
> Ten artykuł dotyczy wyłącznie sytuacji, gdy zamiast uproszczonych bram usługi ATA są wdrażane bramy usługi ATA. Aby ustalić, czy konieczne jest użycie bram usługi ATA, zobacz artykuł [Wybieranie odpowiednich bram dla wdrożenia](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).
 
Główne źródło danych używane przez usługę ATA to głęboka inspekcja pakietów ruchu sieciowego do i z kontrolerów domeny. Aby ruch sieciowy był widoczny dla usługi ATA, należy skonfigurować funkcję dublowania portów lub skorzystać z podsłuchu sieci.

Na potrzeby funkcji dublowania portów należy skonfigurować **funkcję dublowania portów** dla każdego kontrolera domeny, który ma być monitorowany, jako **źródło** ruchu sieciowego. Zazwyczaj należy współpracować z zespołem sieci lub wirtualizacji w celu skonfigurowania funkcji dublowania portów.
Aby uzyskać więcej informacji zobacz dokumentację z dostawcą.

Kontrolery domeny i bramy usługi ATA mogą być fizyczne lub wirtualne. Poniżej opisano typowe metody dublowania portów oraz pewne zagadnienia. Aby uzyskać więcej informacji zobacz dokumentację produktu przełącznika lub wirtualizacji serwera. Producent przełącznika może stosować inną terminologię.

**Switched Port Analyzer (SPAN)** — kopiuje ruch sieciowy z co najmniej jednego portu przełącznika do innego portu w ramach tego samego przełącznika. Zarówno brama usługi ATA, jak i kontrolery domeny muszą być podłączone do tego samego przełącznika fizycznego.

**Remote Switch Port Analyzer (RSPAN)** — umożliwia monitorowanie ruchu sieciowego z portów źródłowych znajdujących się w wielu przełącznikach fizycznych. Funkcja RSPAN kopiuje ruch źródłowy do specjalnej sieci VLAN skonfigurowanej na potrzeby funkcji RSPAN. Ta sieć VLAN musi być połączona magistralą z innymi przełącznikami korzystającymi z tej funkcji. Funkcja RSPAN działa w warstwie 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** — technologia stanowiąca własność firmy Cisco działająca w warstwie 3. Funkcja ERSPAN umożliwia monitorowanie ruchu w obrębie wielu przełączników bez konieczności używania magistral sieci VLAN. Funkcja ERSPAN używa protokołu Generic Routing Encapsulation (GRE) do kopiowania monitorowanego ruchu sieciowego. Aktualnie usługa ATA nie może bezpośrednio odbierać ruchu funkcji ERSPAN. Aby usługa ATA działała z ruchem funkcji ERSPAN przełącznik lub router mogący dehermetyzować ruch musi być skonfigurowany jako miejsce docelowe funkcji erspan, w których ruch jest po dehermetyzacji. Następnie należy skonfigurować przełącznik lub router, aby przesyłał dalej ruch po dehermetyzacji do bramy usługi ATA przy użyciu SPAN lub RSPAN.

> [!NOTE]
> Jeśli kontroler domeny, względem którego działa funkcja dublowania portów, korzysta z połączenia WAN, upewnij się, że połączenie WAN może obsłużyć dodatkowe obciążenie wynikające z ruchu funkcji ERSPAN.
> Usługa ATA obsługuje monitorowanie ruchu tylko wtedy, gdy ruch trafia do karty sieciowej i kontrolera domeny w taki sam sposób. Usługa ATA nie obsługuje monitorowania ruchu, gdy jest on dzielony na różne porty.

## <a name="supported-port-mirroring-options"></a>Obsługiwane opcje funkcji dublowania portów

|Brama usługi ATA|Kontroler domeny|Uwagi|
|---------------|---------------------|------------------|
|Wirtualna|Wirtualny na tym samym hoście|Przełącznik wirtualny musi obsługiwać funkcję dublowania portów.<br /><br />Przeniesienie jednej z maszyn wirtualnych na inny host może spowodować przerwanie działania funkcji dublowania portów.|
|Wirtualna|Wirtualny na różnych hostach|Upewnij się, że ten scenariusz jest obsługiwany przez przełącznik wirtualny.|
|Wirtualna|Fizyczny|Wymaga dedykowanej karty sieciowej w przeciwnym razie ATA widzi wszystkie ruch z i wylogowywanie hosta, nawet ruch wysyłany do Centrum usługi ATA.|
|Fizyczny|Wirtualna|Upewnij się, że przełącznik wirtualny obsługuje ten scenariusz oraz konfigurację funkcji dublowania portów na przełącznikach fizycznych opartą na tym scenariuszu:<br /><br />Jeśli host wirtualny korzysta tego samego przełącznika fizycznego, należy skonfigurować span na poziomie przełącznika.<br /><br />Jeśli host wirtualny korzysta z innego przełącznika, należy skonfigurować RSPAN lub ERSPAN&#42;.|
|Fizyczny|Fizyczny — ten sam przełącznik|Przełącznik fizyczny musi obsługiwać funkcję SPAN lub funkcję dublowania portów.|
|Fizyczny|Fizyczny — inny przełącznik|Wymaga, aby przełączniki fizyczne obsługiwały funkcję RSPAN lub ERSPAN&#42;.|
&#42; Funkcja ERSPAN jest obsługiwana tylko wtedy, gdy przed przeanalizowaniem ruchu przez usługę ATA jest wykonywana dehermetyzacja.

> [!NOTE]
> Upewnij się, że kontrolery domeny i bramy usługi ATA, z którym łączą jest czas synchronizowane w ciągu pięciu minut od siebie.

**W przypadku pracy z klastrami wirtualizacji:**

-   Dla każdego kontrolera domeny uruchomionego w klastrze wirtualizacji w ramach maszyny wirtualnej z bramą usługi ATA należy skonfigurować koligację między kontrolerem domeny a bramą usługi ATA. Dzięki temu po przeniesieniu kontrolera domeny do innego hosta w klastrze bramy usługi ATA następującym. Takie rozwiązanie dobrze się sprawdza, gdy istnieje kilka kontrolerów domeny.
> [!NOTE]
> Jeśli Twoje środowisko obsługuje architekturę Virtual to Virtual na różnych hostach (RSPAN), nie musisz martwić się o koligację.
> 
-   Aby upewnić się, że bramy usługi ATA mają odpowiedni rozmiar do samodzielnego monitorowania wszystkich kontrolerów domeny, zainstaluj maszynę wirtualną na każdym hoście wirtualizacji, a następnie zainstaluj bramę usługi ATA na każdym hoście. Skonfiguruj każdą bramę usługi ATA do monitorowania wszystkich kontrolerów domeny uruchomionych w klastrze. W ten sposób dowolnego hosta, który kontrolerach domeny jest uruchomiony na jest monitorowany.

Po skonfigurowaniu funkcji dublowania portów, ale przed zainstalowaniem bramy usługi ATA, zweryfikuj, czy funkcja dublowania portów działa.

## <a name="see-also"></a>Zobacz też
- [Weryfikowanie funkcji dublowania portów](validate-port-mirroring.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
