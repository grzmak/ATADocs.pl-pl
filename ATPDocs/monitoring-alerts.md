---
title: "Opis usługi Azure ATP alertów monitorowania | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak dzienniki Azure ATP umożliwia rozwiązywanie problemów"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cdb440e92aef0f9d09d3aa9411d0ce65435469d1
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*

# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Opis czujnik Azure ATP i autonomicznych czujnik alertów monitorowania

Centrum kondycji ATP Azure informuje o tym, gdy występuje problem z żadnym z worksapces Azure ATP, wyświetlając symbol alertu monitorowania. W tym artykule opisano wszystkie alerty monitorowania dla poszczególnych składników, ich przyczyny i kroki niezbędne do rozwiązania problemu.

## <a name="read-only-user-password-to-expire-shortly"></a>Hasło użytkownika tylko do odczytu, które wkrótce wygasną

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do rozpoznawania jednostek w usłudze Active Directory wygaśnie za mniej niż 30 dni.|Jeśli hasło dla tego użytkownika, czujników Azure ATP przestanie działać i żadne nowe dane są zbierane.|[Zmienianie hasła do łączności z domeną](modifying-atp-config-dcpassword.md) , a następnie zaktualizuj hasło w konsoli ATP Azure.|Średni|

## <a name="read-only-user-password-expired"></a>Hasło użytkownika tylko do odczytu wygasło

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do pobierania danych z katalogu wygasło.|Czujników Azure ATP przestanie działać (lub przestanie działać szybko) i są zbierane żadne nowe dane.|[Zmienianie hasła do łączności z domeną](modifying-atp-config-dcpassword.md) , a następnie zaktualizuj hasło w konsoli ATP Azure.|Wysoki|

## <a name="domain-synchronizer-not-assigned"></a>Brak przypisanego synchronizatora domeny

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Nie przypisano żadnych Sensor Azure ATP Synchronizatora domeny. To może się zdarzyć, jeśli nie istnieje żadne czujnik Azure ATP skonfigurowany jako kandydata Synchronizatora domeny.|Po domeny nie jest zsynchronizowana, może spowodować informacje o jednostce ATP Azure, aby stać się nieaktualne lub brak zmiany do jednostki, ale nie ma wpływu na dowolnym wykrywania.|Upewnij się, że co najmniej jeden czujnik Azure ATP jest ustawiony jako [Synchronizatora domeny](install-atp-step5.md).|Niski|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Wszystkie/niektóre karty sieciowe przechwytywania na czujnika nie są dostępne

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Wszystkie/niektóre z wybranych przechwytywania kart sieciowych na czujnik Azure ATP są wyłączone lub rozłączone.|Ruch sieciowy dla niektórych lub wszystkich kontrolerów domeny jest już przechwytywane przez czujnik Azure ATP. Ma to wpływ na możliwość wykrywać podejrzane działania związane z tych kontrolerów domeny.|Upewnij się, że te karty sieciowe przechwytywania wybranego na czujnik Azure ATP jest włączona i połączona.|Średni|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Niektóre kontrolery domeny są niedostępne przez czujnik

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnik Azure ATP ma ograniczoną funkcjonalność z powodu problemów z połączeniem z niektórych skonfigurowane kontrolery domeny.|Przekaż skrótu wykrywania może być mniej dokładny w przypadku niektórych kontrolerach domeny nie można zbadać za pomocą czujnika Azure ATP.|Upewnij się, kontrolery domeny są uruchomione i działają prawidłowo i czy ten czujnik Azure ATP można otworzyć połączenia LDAP do nich.|Średni|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Wszystkie kontrolery domeny są niedostępne przez czujnik

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnik Azure ATP jest obecnie w trybie offline z powodu problemów z połączeniem z wszystkie skonfigurowane kontrolery domeny.|Ma to wpływ na możliwość Azure ATP wykrywać podejrzane działania związane z kontrolerów domeny monitorowanych przez ten czujnik Azure ATP.| Upewnij się, kontrolery domeny są uruchomione i działają prawidłowo i czy ten czujnik Azure ATP można otworzyć połączenia LDAP do nich.|Średni|

## <a name="sensor-stopped-communicating"></a>Czujnik zatrzymana komunikacji

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Nie ma w niej Brak komunikacji z czujnika Azure ATP. Domyślny przedział czasu dla tego alertu wynosi 5 minut.|Ruch sieciowy nie są przechwytywane przez kartę sieciową na czujnik Azure ATP. Ma to wpływ na usługi ATA może wykrywać podejrzane działania, ponieważ ruch sieciowy nie będzie mogła nawiązać połączenia usługi w chmurze Azure ATP.|Sprawdź, czy port używany do komunikacji między czujnik Azure ATP i usługi w chmurze Azure ATP nie jest blokowany przez wszystkie routery i zapory.|Średni|

## <a name="no-traffic-received-from-domain-controller"></a>Żaden ruch nie jest odbierany z kontrolera domeny

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Żaden ruch została odebrana z kontrolera domeny za pomocą tego czujnika Azure ATP.|Może to oznaczać, że funkcji dublowania portów z kontrolerów domeny czujnika Azure ATP nie została jeszcze skonfigurowana lub nie działa prawidłowo.|Sprawdź, czy [funkcja dublowania portów jest skonfigurowana prawidłowo na urządzeniach sieciowych](configure-port-mirroring.md).<br></br>Na czujnik Azure ATP przechwytywania karty Sieciowej, wyłącz te funkcje w zaawansowanych ustawieniach:<br></br>Łączenie segmentów odbieranych pakietów (IPv4)<br></br>Łączenie segmentów odbieranych pakietów (IPv6)|Średni|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Niektóre przekazywane zdarzenia nie są analizowane

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnik Azure ATP odbiera więcej zdarzeń niż może przetworzyć.|Niektóre zdarzenia są nie analizowane, która może wpływać wykrywać podejrzane działania pochodzące z kontrolerów domeny monitorowanych przez ten czujnik Azure ATP.|Sprawdź, czy tylko wymagane zdarzenia są przekazywane do czujnik Azure ATP, lub spróbuj przekazywać niektóre zdarzenia do innego czujnik Azure ATP.|Średni|

## <a name="some-network-traffic-is-not-being-analyzed"></a>Część ruchu sieciowego nie jest analizowana

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnik Azure ATP odbiera więcej ruch sieciowy nie może przetworzyć.|Ruch w sieci nie analizowany, która może wpływać wykrywać podejrzane działania pochodzące z kontrolerów domeny monitorowanych przez ten czujnik Azure ATP.|Rozważ [dodanie dodatkowych procesorów i pamięci](atp-capacity-planning.md) zgodnie z wymaganiami. Jeśli jest to autonomiczny czujnika Azure ATP, Zmniejsz liczbę monitorowanych kontrolerów domeny.<br></br>Przyczyną może być także korzystania z kontrolerów domeny na maszynach wirtualnych VMware. Aby zapobiegać tym alertom, można sprawdzić, czy następujące ustawienia maszyny wirtualnej są ustawione na 0 lub wyłączone:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>-Odciążanie TSO IPv4<br></br>Należy również rozważyć wyłączenie ustawienia IPv4 Giant TSO Offload (Bardzo duże odciążanie TSO IPv4). Aby uzyskać więcej informacji zajrzyj do dokumentacji VMware.|Średni|

## <a name="sensor-service-failed-to-start"></a>Nie można uruchomić usługi czujnik

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Usługi czujnik Azure ATP nie powiodło się dla co najmniej 30 minut.|To może wpłynąć na możliwość wykrywać podejrzane działania pochodzące z kontrolerów domeny monitorowanych przez ten czujnik Azure ATP.|Monitor Azure ATP czujnik dzienniki, aby poznać przyczynę niepowodzenia usługi czujnik Azure ATP.|Wysoki|

## <a name="sensor-reached-a-memory-resource-limit"></a>Czujnik osiągnięto limit zasobów pamięci

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnik Azure ATP zatrzymał się i do automatycznego uruchomienia ochrony na kontrolerze domeny z braku pamięci.|Czujnik Azure ATP wymusza ograniczenia pamięci od samego siebie, aby zapobiec występują ograniczenia zasobów na kontrolerze domeny. Ma to miejsce w przypadku, gdy użycie pamięci na kontrolerze domeny jest wysokie. Dane z tego kontrolera domeny są monitorowane tylko częściowo.|Zwiększ ilość pamięci RAM w kontrolerze domeny lub dodaj więcej kontrolerów domeny w tej lokacji, aby zapewnić lepsze rozłożenie obciążenia tego kontrolera domeny.|Średni|


## <a name="see-also"></a>Zobacz też

- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)
- [Planowanie pojemności Azure w ATP](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)