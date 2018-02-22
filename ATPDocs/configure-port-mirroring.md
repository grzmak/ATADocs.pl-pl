---
title: "Konfigurowanie funkcji dublowania portów podczas wdrażania usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft"
description: "Zawiera opis opcji funkcji dublowania portów i sposobu ich konfigurowana na potrzeby Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1cc622f1a8306530423920873e5efa05e8c87064
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="configure-port-mirroring"></a>Konfigurowanie funkcji dublowania portów
> [!NOTE] 
> Ten artykuł dotyczy tylko wtedy, gdy wdrażanie czujnik autonomiczny Azure ATP zamiast czujnik Azure ATP. Aby określić, jeśli należy użyć czujnik autonomiczny Azure ATP, zobacz [Wybieranie prawo czujników wdrożenia](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
Główne źródło danych używane przez Azure ATP to głęboka inspekcja pakietów ruchu sieciowego do i z kontrolerów domeny. Dla ATP Azure zobaczyć ruchu sieciowego musisz Konfigurowanie funkcji dublowania portów lub użyj PODSŁUCHU sieci.

Na potrzeby funkcji dublowania portów należy skonfigurować **funkcję dublowania portów** dla każdego kontrolera domeny, który ma być monitorowany, jako **źródło** ruchu sieciowego. Zazwyczaj należy współpracować z zespołem sieci lub wirtualizacji w celu skonfigurowania funkcji dublowania portów.
Aby uzyskać więcej informacji zobacz dokumentację z dostawcą.

Kontrolery domeny i czujnik autonomiczny Azure ATP może być fizyczne lub wirtualne. Poniżej opisano typowe metody dublowania portów oraz pewne zagadnienia. Aby uzyskać więcej informacji zobacz dokumentację produktu przełącznika lub wirtualizacji serwera. Producent przełącznika może stosować inną terminologię.

**Switched Port Analyzer (SPAN)** — kopiuje ruch sieciowy z co najmniej jednego portu przełącznika do innego portu w ramach tego samego przełącznika. Zarówno Azure ATP autonomiczny czujnik i kontrolery domeny musi być podłączony do tego samego przełącznika fizycznego.

**Remote Switch Port Analyzer (RSPAN)** — umożliwia monitorowanie ruchu sieciowego z portów źródłowych znajdujących się w wielu przełącznikach fizycznych. Funkcja RSPAN kopiuje ruch źródłowy do specjalnej sieci VLAN skonfigurowanej na potrzeby funkcji RSPAN. Ta sieć VLAN musi być połączona magistralą z innymi przełącznikami korzystającymi z tej funkcji. Funkcja RSPAN działa w warstwie 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** — technologia stanowiąca własność firmy Cisco działająca w warstwie 3. Funkcja ERSPAN umożliwia monitorowanie ruchu w obrębie wielu przełączników bez konieczności używania magistral sieci VLAN. Funkcja ERSPAN używa protokołu Generic Routing Encapsulation (GRE) do kopiowania monitorowanego ruchu sieciowego. Wartość Azure ATP aktualnie nie może bezpośrednio odbierać ruchu funkcji ERSPAN. Aby ATP Azure do pracy z ruchu funkcji ERSPAN przełącznik lub router mogący dehermetyzować ruch musi być skonfigurowany jako miejsce docelowe funkcji erspan, w których ruch jest po dehermetyzacji. Następnie należy skonfigurować przełącznik lub router, aby przesyłał dalej ruch po dehermetyzacji czujnika autonomiczny Azure ATP przy użyciu SPAN lub RSPAN.

> [!NOTE]
> Jeśli kontroler domeny, względem którego działa funkcja dublowania portów, korzysta z połączenia WAN, upewnij się, że połączenie WAN może obsłużyć dodatkowe obciążenie wynikające z ruchu funkcji ERSPAN.
> Azure ATP obsługuje tylko, gdy ruch osiągnie karty Sieciowej, a kontrolerem domeny w taki sam sposób monitorowania ruchu. Azure ATP nie obsługuje monitorowania ruchu, jeśli ruch jest podzielone na różne porty.

## <a name="supported-port-mirroring-options"></a>Obsługiwane opcje funkcji dublowania portów

|Azure czujnik autonomiczny ATP|Kontroler domeny|Uwagi|
|---------------|---------------------|------------------|
|Wirtualna|Wirtualny na tym samym hoście|Przełącznik wirtualny musi obsługiwać funkcję dublowania portów.<br /><br />Przeniesienie jednej z maszyn wirtualnych na inny host może spowodować przerwanie działania funkcji dublowania portów.|
|Wirtualna|Wirtualny na różnych hostach|Upewnij się, że ten scenariusz jest obsługiwany przez przełącznik wirtualny.|
|Wirtualna|Fizyczny|Wymaga dedykowanej karty sieciowej w przeciwnym razie ATP Azure widzi wszystkie ruch do i hosta, nawet ruch wysyłany do usługi w chmurze Azure ATP.|
|Fizyczny|Wirtualna|Upewnij się, że przełącznik wirtualny obsługuje ten scenariusz oraz konfigurację funkcji dublowania portów na przełącznikach fizycznych opartą na tym scenariuszu:<br /><br />Jeśli host wirtualny korzysta tego samego przełącznika fizycznego, należy skonfigurować span na poziomie przełącznika.<br /><br />Jeśli host wirtualny korzysta z innego przełącznika, należy skonfigurować funkcję RSPAN lub ERSPAN &#42;.|
|Fizyczny|Fizyczny — ten sam przełącznik|Przełącznik fizyczny musi obsługiwać funkcję SPAN lub funkcję dublowania portów.|
|Fizyczny|Fizyczny — inny przełącznik|Wymaga, aby przełączniki fizyczne obsługiwały funkcję RSPAN lub ERSPAN&#42;.|
&#42; Funkcja ERSPAN jest obsługiwana tylko po dehermetyzacji jest wykonywane przed ruchu są analizowane przez ATP.

> [!NOTE]
> Upewnij się, że kontrolery domeny i czujnik autonomiczny Azure ATP, z którym łączą jest czas synchronizowane w ciągu pięciu minut od siebie.

**W przypadku pracy z klastrami wirtualizacji:**

-   Dla każdego kontrolera domeny uruchomionego w klastrze wirtualizacji na maszynie wirtualnej z czujnika autonomiczny Azure ATP należy skonfigurować koligację między kontrolerem domeny i czujnik autonomiczny Azure ATP. Dzięki temu, gdy kontroler domeny jest przenoszony na innego hosta w klastrze czujnik autonomiczny Azure ATP następującym. Takie rozwiązanie dobrze się sprawdza, gdy istnieje kilka kontrolerów domeny.

 > [!NOTE]
 > Jeśli Twoje środowisko obsługuje architekturę Virtual to Virtual na różnych hostach (RSPAN), nie musisz martwić się o koligację.
 
-   Użyj tej opcji, aby upewnić się, czujnik autonomiczny Azure ATP mają odpowiedni rozmiar do samodzielnego monitorowania wszystkich kontrolerów domeny przez siebie,: Zainstaluj maszynę wirtualną na każdym hoście wirtualizacji i zainstalować czujnik autonomiczny Azure ATP na każdym hoście. Skonfiguruj każdy czujnik autonomiczny Azure ATP do monitorowania wszystkich kontrolerów domeny, które są uruchamiane w klastrze. W ten sposób dowolnego hosta, który kontrolerach domeny jest uruchomiony na jest monitorowany.

Po skonfigurowaniu funkcji dublowania portów należy zweryfikować, czy funkcja dublowania portów działa przed zainstalowaniem czujnik autonomiczny Azure ATP.

## <a name="see-also"></a>Zobacz też
- [Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)