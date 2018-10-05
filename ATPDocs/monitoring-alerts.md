---
title: Omówienie usługi Azure ATP alertów monitorowania | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak dzienniki usługi Azure ATP można użyć do rozwiązywania problemów
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: eed1509cb31885bccdfcc40505284dbdbdfc4cca
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783886"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Opis czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i czujnik autonomiczny alertów monitorowania

Centrum kondycji zaawansowanej ochrony przed zagrożeniami w usłudze Azure informuje o tym, gdy występuje problem z obszarem roboczym usługi Azure ATP przez wywołanie alertu monitorowania. W tym artykule opisano wszystkie alerty monitorowania dla poszczególnych składników, ich przyczyny i kroki niezbędne do rozwiązania problemu.

## <a name="read-only-user-password-to-expire-shortly"></a>Hasło użytkownika tylko do odczytu wkrótce wygaśnie

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do rozpoznawania jednostek w usłudze Active Directory wygaśnie za mniej niż 30 dni.|Jeśli hasło dla tego użytkownika wygaśnie, wszystkie czujniki narzędzia Azure ATP przestanie działać, a żadne nowe dane są zbierane.|[Zmienianie hasła do łączności z domeną](modifying-atp-config-dcpassword.md) , a następnie zaktualizuj hasło w portalu usługi Azure ATP.|Średni|

## <a name="read-only-user-password-expired"></a>Hasło użytkownika tylko do odczytu wygasło

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do pobierania danych z katalogu wygasło.|Wszystkie czujniki narzędzia Azure ATP przestanie działać (lub przestanie działać wkrótce), a żadne nowe dane są zbierane.|[Zmienianie hasła do łączności z domeną](modifying-atp-config-dcpassword.md) , a następnie zaktualizuj hasło w portalu usługi Azure ATP.|Wysoki|

## <a name="domain-synchronizer-not-assigned"></a>Brak przypisanego synchronizatora domeny

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Nie przypisano żadnego Synchronizatora domeny do jakiegokolwiek czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. To może się zdarzyć, jeśli nie ma żadnych czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure skonfigurowano jako kandydata Synchronizatora domeny.|Gdy domeny nie jest zsynchronizowana, zmiany dotyczące jednostek może spowodować informacji o jednostkach usługi Azure ATP, aby stać się nieaktualne lub nie istnieje, ale nie ma wpływu na żadnego procesu wykrywania.|Upewnij się, że co najmniej jeden czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest ustawiony jako [Synchronizatora domeny](install-atp-step5.md).|Niski|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Wszystkie/niektóre karty sieciowe przechwytywania na czujniku są niedostępne

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Wszystkie/niektóre wybrane karty sieciowe przechwytywania na czujniku narzędzia Azure ATP jest wyłączona lub odłączona.|Ruch sieciowy dla niektórych/wszystkich kontrolerów domeny nie jest już przechwytywany przez czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Ma to wpływ na możliwość wykrywania podejrzanych działań związanych z tymi kontrolerami domeny.|Upewnij się, że te wybrane karty sieciowe przechwytywania na czujniku narzędzia Azure ATP są włączone i połączone.|Średni|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Niektóre kontrolery domeny są nieosiągalne dla czujnika

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure ma ograniczoną funkcjonalność ze względu na problemy z łącznością z niektórymi skonfigurowanych kontrolerów domeny.|Przekaż wyznaczania wartości skrótu, wykrywania może być mniej dokładne, gdy niektóre kontrolery domeny nie można zbadać za pomocą narzędzia Azure ATP czujnika.|Upewnij się, że kontrolery domeny są uruchomione i że tego czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure można otworzyć połączenia LDAP z tymi.|Średni|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Wszystkie kontrolery domeny są nieosiągalne dla czujnika

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest obecnie w trybie offline z powodu problemów z łącznością na kontrolerach domeny skonfigurowane.|Ma to wpływ na możliwość wykrywania podejrzanych działań związanych z kontrolerów domeny monitorowanych przez czujnik tego narzędzia Azure ATP narzędzia Azure ATP.| Upewnij się, że kontrolery domeny są uruchomione i że tego czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure można otworzyć połączenia LDAP z tymi.|Średni|

## <a name="sensor-stopped-communicating"></a>Komunikacja z czujnikiem została

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Wystąpił brak komunikacji z czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Domyślny przedział czasu dla tego alertu wynosi 5 minut.|Ruch sieciowy nie jest już przechwytywany przez kartę sieciową na czujniku narzędzia Azure ATP. Ma to wpływ na możliwość wykrywania podejrzanych działań, ponieważ ruch sieciowy nie można nawiązać połączenia z usługą w chmurze usługi Azure ATP usługi ATA.|Sprawdź, czy port używany do komunikacji między czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure i usługi w chmurze usługi Azure ATP nie jest blokowany przez routery lub zapory.|Średni|

## <a name="no-traffic-received-from-domain-controller"></a>Żaden ruch nie jest odbierany z kontrolera domeny

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Odebrano żadnego ruchu z kontrolera domeny za pośrednictwem tego czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.|Może to wskazywać, że funkcja dublowania portów z kontrolerów domeny do czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure nie została jeszcze skonfigurowana lub nie działa.|Sprawdź, czy [funkcja dublowania portów jest skonfigurowana prawidłowo na urządzeniach sieciowych](configure-port-mirroring.md).<br></br>Karcie Sieciowej przechwytywania na czujniku narzędzia Azure ATP, wyłącz te funkcje w zaawansowanych ustawieniach:<br></br>Łączenie segmentów odbieranych pakietów (IPv4)<br></br>Łączenie segmentów odbieranych pakietów (IPv6)|Średni|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Niektóre przekazywane zdarzenia nie są analizowane

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure odbiera więcej zdarzeń niż może przetworzyć.|Niektóre przekazywane zdarzenia nie są analizowane, co może mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez czujnik tego narzędzia Azure ATP.|Sprawdź, czy tylko wymagane zdarzenia są przekazywane do czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, lub spróbuj przekazać niektóre zdarzenia do innego czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.|Średni|

## <a name="some-network-traffic-is-not-being-analyzed"></a>Część ruchu sieciowego nie jest analizowana

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure odbiera więcej ruchu sieciowego niż może przetworzyć.|Część ruchu sieciowego nie jest analizowana, co może mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez czujnik tego narzędzia Azure ATP.|Rozważ [dodanie dodatkowych procesorów i pamięci](atp-capacity-planning.md) zgodnie z wymaganiami. Jeśli jest to narzędzia Azure ATP czujnik autonomiczny, Zmniejsz liczbę monitorowanych kontrolerów domeny.<br></br>Może to również nastąpić, jeśli używasz kontrolerów domeny na maszynach wirtualnych VMware. Aby zapobiegać tym alertom, można sprawdzić, czy następujące ustawienia maszyny wirtualnej są ustawione na 0 lub wyłączone:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>-Odciążanie TSO IPv4<br></br>Należy również rozważyć wyłączenie ustawienia IPv4 Giant TSO Offload (Bardzo duże odciążanie TSO IPv4). Aby uzyskać więcej informacji zajrzyj do dokumentacji programu VMware.|Średni|

## <a name="sensor-service-failed-to-start"></a>Nie można uruchomić usługi czujnika

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Usługa czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure nie powiodło się uruchomienie co najmniej 30 minut.|Może to mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez czujnik tego narzędzia Azure ATP.|Dzienniki czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure monitor, aby poznać główną przyczynę niepowodzenia usługi czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.|Wysoki|

## <a name="sensor-reached-a-memory-resource-limit"></a>Czujnik osiągnął limit zasobów pamięci

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure została samoczynnie zatrzymana i zostanie automatycznie ponownie uruchomiona na kontrolerze domeny z stan braku pamięci.|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wymusza pamięci na sobie ograniczenia dotyczące aby zapobiec ograniczeń zasobów kontrolera domeny. Ma to miejsce w przypadku, gdy użycie pamięci na kontrolerze domeny jest wysokie. Dane z tego kontrolera domeny są monitorowane tylko częściowo.|Zwiększ ilość pamięci RAM w kontrolerze domeny lub dodaj więcej kontrolerów domeny w tej lokacji, aby zapewnić lepsze rozłożenie obciążenia tego kontrolera domeny.|Średni|

## <a name="sensor-outdated"></a>Czujnik przestarzałe

|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest nieaktualny.|Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure działa w wersji co najmniej trzy wersje nieaktualna.|Ręcznie zaktualizować czujników i sprawdź, dlaczego czujnika nie są automatycznie aktualizowane. Jeśli to nie rozwiąże problemu, Pobierz najnowszy pakiet instalacji czujnika odinstalować i ponownie zainstalować czujnika. Aby uzyskać więcej informacji, zobacz [instalowanie czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure](install-atp-step4.md).|Średni|

## <a name="see-also"></a>Zobacz też

- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)