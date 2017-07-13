---
title: "Opis alertów monitorowania usługi ATA | Microsoft Docs"
description: "Opis sposobu rozwiązywania problemów przy użyciu dzienników usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/13/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4c232ea6bd25f1f13fe8e322719cda6388da9c0e
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



Centrum kondycji usługi ATA informuje o wystąpieniu problemu z wdrożeniem usługi ATA przez wywołanie alertu monitorowania.
W tym artykule opisano wszystkie alerty monitorowania dla poszczególnych składników, ich przyczyny i kroki niezbędne do rozwiązania problemu.
## Problemy z centrum usługi ATA
<a id="ata-center-issues" class="xliff"></a>
### Kończy się wolne miejsce na dysku centrum usługi ATA
<a id="ata-center-running-out-of-disk-space" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Kończy się wolne miejsce na dysku maszyny centrum usługi ATA używanej do przechowywania bazy danych usługi ATA.|Oznacza to, że na dysku twardym jest dostępnych mniej niż 200 GB wolnego miejsca lub jest dostępne mniej niż 20% wolnego miejsca, w zależności od tego, która wartość jest niższa. Gdy usługa ATA rozpozna, że kończy się miejsce na dysku, zacznie usuwać stare dane z bazy danych. Jeśli usunięcie starych danych jest niemożliwe, ponieważ dane są nadal niezbędne dla aparatu wykrywania, zostanie wyświetlony ten alert. W przypadku otrzymania tego alertu usługa ATA przestaje rejestrować nowe działania.|Zwiększ rozmiar dysku lub zwolnij miejsce na tym dysku.|Wysoki|
### Błąd wysyłania wiadomości e-mail
<a id="failure-sending-mails" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Usługa ATA nie może wysłać powiadomienia e-mail do określonego serwera poczty.|Wiadomości e-mail nie będą wysyłane z usługi ATA.|Zweryfikuj konfigurację serwera SMTP.|Niski|

### Przeciążenie centrum usługi ATA
<a id="ata-center-overloaded" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Centrum usługi ATA nie jest w stanie obsłużyć danych w ilościach przesyłanych z bram usługi ATA. |Centrum usługi ATA przestanie analizować nowy ruch sieciowy i nowe zdarzenia. Oznacza to, że dokładność wykrywania i profili jest mniejsza, gdy ten alert monitorowania jest aktywny.|Upewnij się, że zapewniono wystarczającą ilość zasobów dla centrum usługi ATA. Zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md), aby uzyskać więcej informacji na temat prawidłowego planowania pojemności centrum usługi ATA. Zbadaj wydajność centrum usługi ATA, korzystając z informacji przedstawionych w temacie [Rozwiązywanie problemów z usługą ATA przy użyciu liczników wydajności](troubleshooting-ata-using-perf-counters.md).|Wysoki|

### Nie można nawiązać połączenia z serwerem SIEM przy użyciu protokołu Syslog
<a id="failure-connecting-to-the-siem-server-using-syslog" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Usługa ATA nie może wysyłać zdarzeń do określonego rozwiązania SIEM.|Oznacza to, że centrum usługi ATA nie może wysyłać alertów o podejrzanych działaniach i alertów monitorowania do rozwiązania SIEM.|Upewnij się, że [ustawienia serwera Syslog są poprawnie skonfigurowane](setting-syslog-email-server-settings.md).|Niski|
### Certyfikat centrum usługi ATA niedługo wygaśnie
<a id="ata-center-certificate-is-about-to-expire" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat centrum usługi ATA wygaśnie za mniej niż 3 tygodnie.|Po wygaśnięciu certyfikatu połączenia między bramami usługi ATA i centrum usługi ATA będą kończyć się niepowodzeniem. Proces centrum usługi ATA ulegnie awarii i wszystkie funkcje usługi ATA przestaną działać.|[Replace the ATA Center certificate (Zastępowanie certyfikatu centrum usługi ATA)](modifying-ata-center-configuration.md)|Średni|
### Certyfikat centrum usługi ATA wygasł
<a id="ata-center-certificate-expired" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat centrum usługi ATA wygasł.|Po wygaśnięciu certyfikatu połączenia między bramami usługi ATA i centrum usługi ATA będą kończyć się niepowodzeniem. Proces centrum usługi ATA ulegnie awarii i wszystkie funkcje usługi ATA przestaną działać.|[Replace the ATA Center certificate (Zastępowanie certyfikatu centrum usługi ATA)](modifying-ata-center-configuration.md)|Wysoki|
## Problemy z bramą usługi ATA
<a id="ata-gateway-issues" class="xliff"></a>
### Hasło użytkownika tylko do odczytu niedługo wygaśnie
<a id="read-only-user-password-is-about-to-expire" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do rozpoznawania jednostek w usłudze Active Directory wygaśnie za mniej niż 30 dni.|Jeśli hasło dla tego użytkownika wygaśnie, wszystkie bramy usługi ATA przestaną działać i nowe dane nie będą zbierane.|[Zmień hasło do łączności z domeną](modifying-ata-config-dcpassword.md), a następnie zaktualizuj hasło w konsoli usługi ATA.|Średni|
### Hasło użytkownika tylko do odczytu wygasło
<a id="read-only-user-password-expired" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Hasło użytkownika tylko do odczytu używane do pobierania danych z katalogu wygasło.|Wszystkie bramy usługi ATA przestaną działać (lub wkrótce przestaną działać) i nowe dane nie będą zbierane.|[Zmień hasło do łączności z domeną](modifying-ata-config-dcpassword.md), a następnie zaktualizuj hasło w konsoli usługi ATA.|Wysoki|
### Certyfikat bramy usługi ATA niedługo wygaśnie
<a id="ata-gateway-certificate-about-to-expire" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat bramy usługi ATA wygaśnie za mniej niż 3 tygodnie.|Połączenia między określoną bramą usługi ATA i centrum usługi ATA będą kończyć się niepowodzeniem. Z tej bramy usługi ATA nie będą wysyłane żadne dane.|Certyfikat bramy usługi ATA powinien zostać odnowiony automatycznie. Zapoznaj się z dziennikami bramy usługi ATA i centrum usługi ATA, aby dowiedzieć się, dlaczego certyfikat nie został odnowiony automatycznie.|Średni|

### Certyfikat bramy usługi ATA wygasł
<a id="ata-gateway-certificate-expired" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Certyfikat bramy usługi ATA wygasł.|Brak połączenia między bramą usługi ATA i centrum usługi ATA. Z tej bramy usługi ATA nie będą wysyłane żadne dane.|[Odinstaluj bramę usługi ATA i zainstaluj ją ponownie](install-ata-step3.md).|Wysoki|
### Brak przypisanego synchronizatora domeny
<a id="domain-synchronizer-not-assigned" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Nie przypisano żadnego synchronizatora domeny do żadnej bramy usługi ATA. Może się tak zdarzyć, jeśli żadnej bramy usługi ATA nie skonfigurowano jako kandydata synchronizatora domeny.|Jeśli domena nie jest zsynchronizowana, zmiany dotyczące jednostek mogą spowodować brak lub występowanie nieaktualnych informacji o jednostkach w usłudze ATA, ale nie wpłynie to na wykrywanie.|Upewnij się, że co najmniej jedna brama usługi ATA jest ustawiona jako [synchronizator domeny](install-ata-step5.md).|Niski|
### Wszystkie/niektóre karty sieciowe przechwytywania w bramie usługi ATA są niedostępne
<a id="allsome-of-the-capture-network-adapters-on-an-ata-gateway-are-not-available" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Wszystkie/niektóre z wybranych kart sieciowych przechwytywania w bramie usługi ATA są wyłączone lub rozłączone.|Ruch sieciowy dla niektórych/wszystkich kontrolerów domeny nie jest już przechwytywany przez bramę usługi ATA. Wpłynie to na możliwość wykrywania podejrzanych działań związanych z tymi kontrolerami domeny.|Upewnij się, że te wybrane karty sieciowe przechwytywania w bramie usługi ATA są włączone i połączone.|Średni|
### Niektóre kontrolery domeny są niedostępne dla bramy usługi ATA
<a id="some-domain-controllers-are-unreachable-by-a-ata-gateway" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA ma ograniczoną funkcjonalność ze względu na problemy z łącznością z niektórymi ze skonfigurowanych kontrolerów domeny.|Wykrywanie ataków typu Pass-the-Hash może być mniej dokładne, gdy brama usługi ATA nie może wysyłać zapytań do niektórych kontrolerów domeny.|Upewnij się, że kontrolery domeny są uruchomione i działają prawidłowo oraz że ta brama usługi ATA może otwierać połączenia z tymi kontrolerami za pomocą protokołu LDAP.|Średni|
### Wszystkie kontrolery domeny są niedostępne dla bramy usługi ATA
<a id="all-domain-controllers-are-unreachable-by-a-ata-gateway" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA jest obecnie w trybie offline ze względu na problemy z łącznością ze wszystkimi kontrolerami domeny.|Wpłynie to na możliwość wykrywania przez usługę ATA podejrzanych działań związanych z kontrolerami domeny monitorowanymi przez tę bramę usługi ATA.| Upewnij się, że kontrolery domeny są uruchomione i działają prawidłowo oraz że ta brama usługi ATA może otwierać połączenia z tymi kontrolerami za pomocą protokołu LDAP.|Średni|
### Komunikacja z bramą usługi ATA została przerwana
<a id="ata-gateway-stopped-communicating" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brak komunikacji z bramą usługi ATA. Domyślny przedział czasu dla tego alertu wynosi 5 minut.|Ruch sieciowy nie jest już przechwytywany przez kartę sieciową w bramie usługi ATA. Wpłynie to na możliwość wykrywania podejrzanych działań przez usługę ATA, ponieważ ruch sieciowy nie będzie docierać do centrum usługi ATA.|Sprawdź, czy port używany do komunikacji między bramą usługi ATA i centrum usługi ATA nie jest blokowany przez routery lub zapory.|Średni|
### Żaden ruch nie jest odbierany z kontrolera domeny
<a id="no-traffic-received-from-domain-controller" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Nie odebrano żadnego ruchu z kontrolera domeny za pośrednictwem tej bramy usługi ATA.|Może to oznaczać, że funkcja dublowania portów z kontrolerów domeny do bramy usługi ATA nie została jeszcze skonfigurowana lub nie działa.|Sprawdź, czy [funkcja dublowania portów jest skonfigurowana prawidłowo na urządzeniach sieciowych](configure-port-mirroring.md).|Średni|
### Niektóre przekazywane zdarzenia nie są analizowane
<a id="some-forwarded-events-are-not-being-analyzed" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA odbiera więcej zdarzeń niż może przetworzyć.|Niektóre przekazywane zdarzenia nie są analizowane, co może mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Upewnij się, że tylko wymagane zdarzenia są przekazywane do bramy usługi ATA lub spróbuj przekazać niektóre zdarzenia do innej bramy usługi ATA.|Średni|
### Część ruchu sieciowego nie jest analizowana
<a id="some-network-traffic-is-not-being-analyzed" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Brama usługi ATA odbiera więcej ruchu sieciowego niż może przetworzyć.|Część ruchu sieciowego nie jest analizowana, co może mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Rozważ [dodanie dodatkowych procesorów i pamięci](ata-capacity-planning.md) zgodnie z wymaganiami. Jeśli jest to autonomiczna brama usługi ATA, zmniejsz liczbę monitorowanych kontrolerów domeny.|Średni|

### Nieaktualna wersja bramy usługi ATA
<a id="ata-gateway-version-outdated" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Wersja centrum usługi ATA jest nowsza niż wersja zainstalowana na bramie usługi ATA. Powoduje to, że brama usługi ATA przestaje działać zgodnie z oczekiwaniami.|Może to mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Wykonaj automatyczną aktualizację bramy usługi ATA do najnowszej wersji, włączając funkcję [aktualizacji automatycznych](install-ata-step1.md) w konsoli usługi ATA lub pobierając najnowszy pakiet bramy usługi ATA dostępny w konsoli usługi ATA.|Wysoki|
### Uruchomienie bramy usługi ATA nie powiodło się
<a id="ata-gateway-service-failed-to-start" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Od co najmniej 30 minut nie można uruchomić bramy usługi ATA.|Może to mieć wpływ na możliwość wykrywania podejrzanych działań pochodzących z kontrolerów domeny monitorowanych przez tę bramę usługi ATA.|Sprawdź dzienniki bramy usługi ATA, aby [poznać główną przyczynę awarii bramy usługi ATA](troubleshooting-ata-using-logs.md).|Wysoki|
## Uproszczona brama
<a id="lightweight-gateway" class="xliff"></a>
### Osiągnięto limit zasobów pamięci uproszczonej bramy usługi ATA
<a id="lightweight-ata-gateway-reached-a-memory-resource-limit" class="xliff"></a>
|Alert|Opis|Rozwiązanie|Ważność|
|----|----|----|----|
|Uproszczona brama usługi ATA została samoczynnie zatrzymana i zostanie automatycznie uruchomiona ponownie w celu ochrony kontrolera domeny przed warunkiem niskiego poziomu pamięci.|Uproszczona brama usługi ATA wymusza na sobie ograniczenia dotyczące użycia pamięci w celu zapobiegnięcia występowaniu ograniczeń zasobów kontrolera domeny. Ma to miejsce w przypadku, gdy użycie pamięci na kontrolerze domeny jest wysokie. Dane z tego kontrolera domeny są monitorowane tylko częściowo.|Zwiększ ilość pamięci RAM w kontrolerze domeny lub dodaj więcej kontrolerów domeny w tej lokacji, aby zapewnić lepsze rozłożenie obciążenia tego kontrolera domeny.|Średni|


## Zobacz też
<a id="see-also" class="xliff"></a>
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)