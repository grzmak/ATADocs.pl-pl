---
title: Opis alertów monitorowania usługi ATA | Microsoft Docs
description: Opis sposobu rozwiązywania problemów przy użyciu dzienników usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cf3090ae1248125c9ff4d55bc1db7540ae532720
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133909"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*


# <a name="understanding-ata-monitoring-alerts"></a>Opis alertów monitorowania usługi ATA
Centrum kondycji usługi ATA informuje o wystąpieniu problemu z wdrożeniem usługi ATA przez wywołanie alertu monitorowania.
W tym artykule opisano wszystkie alerty monitorowania dla poszczególnych składników, ich przyczyny i kroki niezbędne do rozwiązania problemu.
## <a name="ata-center-issues"></a>Problemy z centrum usługi ATA
### <a name="center-running-out-of-disk-space"></a>Centrum wyczerpuje się miejsce na dysku
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Kończy się wolne miejsce na dysku maszyny centrum usługi ATA używanej do przechowywania bazy danych usługi ATA.|Oznacza to, że na dysku twardym jest dostępnych mniej niż 200 GB wolnego miejsca lub jest dostępne mniej niż 20% wolnego miejsca, w zależności od tego, która wartość jest niższa. Gdy usługa ATA rozpozna, że kończy się miejsce na dysku, zacznie usuwać stare dane z bazy danych. Jeśli go nie można usunąć stare dane, ponieważ nadal potrzebuje danych do aparatu wykrywania, zostanie wyświetlony ten alert. W przypadku otrzymania tego alertu usługa ATA przestaje rejestrować nowe działania.|Zwiększ rozmiar dysku lub zwolnij miejsce na tym dysku.|Wysoki|
### <a name="failure-sending-mail"></a>Błąd wysyłania wiadomości e-mail
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Usługa ATA nie może wysłać powiadomienia e-mail do określonego serwera poczty.|Wiadomości e-mail nie są wysyłane z usługi ATA.|Zweryfikuj konfigurację serwera SMTP.|Niski|

### <a name="center-overloaded"></a>Przeciążenie Centrum
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Centrum usługi ATA nie jest w stanie obsłużyć danych w ilościach przesyłanych z bram usługi ATA. |Centrum usługi ATA przestaje analizowanie nowy ruch sieciowy i zdarzenia. Oznacza to, że dokładność wykrywania i profili jest mniejsza, gdy ten alert monitorowania jest aktywny.|Upewnij się, że zapewniono wystarczającą ilość zasobów dla centrum usługi ATA. Aby uzyskać więcej informacji na temat prawidłowego planowania pojemności centrum usługi ATA, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md). Zbadaj wydajność centrum usługi ATA, korzystając z informacji przedstawionych w temacie [Rozwiązywanie problemów z usługą ATA przy użyciu liczników wydajności](troubleshooting-ata-using-perf-counters.md).|Wysoki|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>Nie można nawiązać połączenia z serwerem SIEM przy użyciu protokołu Syslog
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Usługa ATA nie może wysyłać zdarzeń do określonego rozwiązania SIEM.|Oznacza to, że centrum usługi ATA nie może wysyłać alertów o podejrzanych działaniach i alertów monitorowania do rozwiązania SIEM.|Upewnij się, że [ustawienia serwera Syslog są poprawnie skonfigurowane](setting-syslog-email-server-settings.md).|Niski|
### <a name="center-certificate-is-about-to-expire"></a>Certyfikat Centrum niedługo wygaśnie
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat centrum usługi ATA wygaśnie za mniej niż 3 tygodnie.|Po wygaśnięciu certyfikatu połączenia między bramami usługi ATA i centrum usługi ATA będą kończyć się niepowodzeniem. Wszystkie funkcje usługi ATA i Centrum usługi ATA, które proces ulegnie awarii będzie się zatrzymuje.|[Replace the ATA Center certificate (Zastępowanie certyfikatu centrum usługi ATA)](modifying-ata-center-configuration.md)|Średni|
### <a name="ata-center-certificate-expired"></a>Certyfikat centrum usługi ATA wygasł
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat centrum usługi ATA wygasł.|Po wygaśnięciu certyfikatu: połączenia między bramami usługi ATA i Centrum usługi ATA kończy się niepowodzeniem. Proces Centrum usługi ATA ulegnie awarii i zatrzymuje wszystkie funkcje usługi ATA.|[Replace the ATA Center certificate (Zastępowanie certyfikatu centrum usługi ATA)](modifying-ata-center-configuration.md)|Wysoki|
## <a name="ata-gateway-issues"></a>Problemy z bramą usługi ATA
### <a name="read-only-user-password-to-expire-shortly"></a>Hasło użytkownika tylko do odczytu wkrótce wygaśnie
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do rozpoznawania jednostek w usłudze Active Directory wygaśnie za mniej niż 30 dni.|Jeśli hasło dla tego użytkownika wygaśnie, wszystkie bramy usługi ATA przestanie działać, a żadne nowe dane są zbierane.|[Zmień hasło do łączności z domeną](modifying-ata-config-dcpassword.md), a następnie zaktualizuj hasło w konsoli usługi ATA.|Średni|
### <a name="read-only-user-password-expired"></a>Hasło użytkownika tylko do odczytu wygasło
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do pobierania danych z katalogu wygasło.|Wszystkie bramy usługi ATA przestanie działać (lub przestanie działać wkrótce), a żadne nowe dane są zbierane.|[Zmień hasło do łączności z domeną](modifying-ata-config-dcpassword.md), a następnie zaktualizuj hasło w konsoli usługi ATA.|Wysoki|
### <a name="gateway-certificate-about-to-expire"></a>Certyfikat bramy o zbliżającym się
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat bramy usługi ATA wygaśnie za mniej niż 3 tygodnie.|Łączność z daną bramę usługi ATA i Centrum usługi ATA kończy się niepowodzeniem. Są wysyłane żadne dane z tej bramy usługi ATA.|Certyfikat bramy usługi ATA powinien zostać odnowiony automatycznie. Zapoznaj się z dziennikami bramy usługi ATA i centrum usługi ATA, aby dowiedzieć się, dlaczego certyfikat nie został odnowiony automatycznie.|Średni|

### <a name="gateway-certificate-expired"></a>Certyfikat bramy wygasł
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat bramy usługi ATA wygasł.|Brak połączenia między bramą usługi ATA i centrum usługi ATA. Są wysyłane żadne dane z tej bramy usługi ATA.|[Odinstaluj bramę usługi ATA i zainstaluj ją ponownie](install-ata-step3.md).|Wysoki|
### <a name="domain-synchronizer-not-assigned"></a>Brak przypisanego synchronizatora domeny
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Nie przypisano żadnego synchronizatora domeny do żadnej bramy usługi ATA. Może się tak zdarzyć, jeśli żadnej bramy usługi ATA nie skonfigurowano jako kandydata synchronizatora domeny.|Gdy domeny nie jest zsynchronizowana, zmiany dotyczące jednostek może spowodować informacji dotyczących jednostki w usłudze ATA, aby stać się nieaktualne lub nie istnieje, ale nie ma wpływu na żadnego procesu wykrywania.|Upewnij się, że co najmniej jedna brama usługi ATA jest ustawiona jako [synchronizator domeny](install-ata-step5.md).|Niski|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>Wszystkie/niektóre karty sieciowe przechwytywania w bramie nie są dostępne
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Wszystkie/niektóre z wybranych kart sieciowych przechwytywania w bramie usługi ATA są wyłączone lub rozłączone.|Ruch sieciowy dla niektórych/wszystkich kontrolerów domeny nie jest już przechwytywany przez bramę usługi ATA. Ma to wpływ na możliwość wykrywania podejrzanych działań związanych z tymi kontrolerami domeny.|Upewnij się, że te wybrane karty sieciowe przechwytywania w bramie usługi ATA są włączone i połączone.|Średni|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>Niektóre kontrolery domeny są niedostępne dla bramy
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA ma ograniczoną funkcjonalność ze względu na problemy z łącznością z niektórymi ze skonfigurowanych kontrolerów domeny.|Wykrywanie ataków typu Pass-the-Hash może być mniej dokładne, gdy brama usługi ATA nie może wysyłać zapytań do niektórych kontrolerów domeny.|Upewnij się, że kontrolery domeny są uruchomione i działają prawidłowo oraz że ta brama usługi ATA może otwierać połączenia z tymi kontrolerami za pomocą protokołu LDAP.|Średni|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>Wszystkie kontrolery domeny są niedostępne dla bramy
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA jest obecnie w trybie offline ze względu na problemy z łącznością ze wszystkimi kontrolerami domeny.|Ma to wpływ na możliwość wykrywania podejrzanych działań związanych z kontrolerami domeny monitorowanymi przez tę bramę usługi ATA usługi ATA.| Upewnij się, że kontrolery domeny są uruchomione i działają prawidłowo oraz że ta brama usługi ATA może otwierać połączenia z tymi kontrolerami za pomocą protokołu LDAP.|Średni|
### <a name="gateway-stopped-communicating"></a>Brama zatrzymana podczas komunikowania się
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brak komunikacji z bramą usługi ATA. Domyślny przedział czasu dla tego alertu wynosi 5 minut.|Ruch sieciowy nie jest już przechwytywany przez kartę sieciową w bramie usługi ATA. Ma to wpływ na możliwość wykrywania podejrzanych działań, ponieważ ruch sieciowy nie będzie można uzyskać dostępu do Centrum usługi ATA usługi ATA.|Sprawdź, czy port używany do komunikacji między bramą usługi ATA i centrum usługi ATA nie jest blokowany przez routery lub zapory.|Średni|
### <a name="no-traffic-received-from-domain-controller"></a>Żaden ruch nie jest odbierany z kontrolera domeny
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Nie odebrano żadnego ruchu z kontrolera domeny za pośrednictwem tej bramy usługi ATA.|Może to oznaczać, że funkcja dublowania portów z kontrolerów domeny do bramy usługi ATA nie została jeszcze skonfigurowana lub nie działa.|Sprawdź, czy [funkcja dublowania portów jest skonfigurowana prawidłowo na urządzeniach sieciowych](configure-port-mirroring.md).<br></br>Karcie Sieciowej przechwytywania w bramie usługi ATA, należy wyłączyć te funkcje w zaawansowanych ustawieniach:<br></br>Łączenie segmentów odbieranych pakietów (IPv4)<br></br>Łączenie segmentów odbieranych pakietów (IPv6)|Średni|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>Niektóre przekazywane zdarzenia nie są analizowane
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA odbiera więcej zdarzeń niż może przetworzyć.|Niektóre przekazywane zdarzenia nie są analizowane, co może mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Upewnij się, że tylko wymagane zdarzenia są przekazywane do bramy usługi ATA lub spróbuj przekazać niektóre zdarzenia do innej bramy usługi ATA.|Średni|
### <a name="some-network-traffic-is-not-being-analyzed"></a>Część ruchu sieciowego nie jest analizowana
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA odbiera więcej ruchu sieciowego niż może przetworzyć.|Część ruchu sieciowego nie jest analizowana, co może mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Rozważ [dodanie dodatkowych procesorów i pamięci](ata-capacity-planning.md) zgodnie z wymaganiami. Jeśli jest to autonomiczna brama usługi ATA, zmniejsz liczbę monitorowanych kontrolerów domeny.<br></br>Może to również nastąpić, jeśli używasz kontrolerów domeny na maszynach wirtualnych VMware. Aby zapobiegać tym alertom, można sprawdzić, czy następujące ustawienia maszyny wirtualnej są ustawione na 0 lub wyłączone:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>-Odciążanie TSO IPv4<br></br>Należy również rozważyć wyłączenie ustawienia IPv4 Giant TSO Offload (Bardzo duże odciążanie TSO IPv4). Aby uzyskać więcej informacji zapoznaj się z dokumentacją programu VMware.|Średni|

### <a name="gateway-version-outdated"></a>Nieaktualna wersja bramy
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Wersja centrum usługi ATA jest nowsza niż wersja zainstalowana na bramie usługi ATA. Powoduje to, że brama usługi ATA przestaje działać zgodnie z oczekiwaniami.|Może to mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Wykonaj automatyczną aktualizację bramy usługi ATA do najnowszej wersji, włączając funkcję [aktualizacji automatycznych](install-ata-step1.md) w konsoli usługi ATA lub pobierając najnowszy pakiet bramy usługi ATA dostępny w konsoli usługi ATA.|Wysoki|
### <a name="gateway-service-failed-to-start"></a>Nie można uruchomić usługi bramy
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Od co najmniej 30 minut nie można uruchomić bramy usługi ATA.|Może to mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Sprawdź dzienniki bramy usługi ATA, aby [poznać główną przyczynę awarii bramy usługi ATA](troubleshooting-ata-using-logs.md).|Wysoki|
## <a name="lightweight-gateway"></a>Uproszczona brama
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>Uproszczona brama osiągnięto limit zasobów pamięci
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Uproszczona brama usługi ATA została samoczynnie zatrzymana i zostanie automatycznie uruchomiona ponownie w celu ochrony kontrolera domeny przed warunkiem niskiego poziomu pamięci.|Uproszczona brama usługi ATA wymusza na sobie ograniczenia dotyczące użycia pamięci w celu zapobiegnięcia występowaniu ograniczeń zasobów kontrolera domeny. Ma to miejsce w przypadku, gdy użycie pamięci na kontrolerze domeny jest wysokie. Dane z tego kontrolera domeny są monitorowane tylko częściowo.|Zwiększ ilość pamięci RAM w kontrolerze domeny lub dodaj więcej kontrolerów domeny w tej lokacji, aby zapewnić lepsze rozłożenie obciążenia tego kontrolera domeny.|Średni|


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
