---
title: "Często zadawane pytania dotyczące usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Zawiera listę często zadawanych pytań dotyczących usługi ATA wraz ze skojarzonymi odpowiedziami"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5beabd2617f55ecbcc717338dc40d9f597cc25d4
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/03/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*

# Usługa ATA — często zadawane pytania
<a id="ata-frequently-asked-questions" class="xliff"></a>
Ten artykuł zawiera listę często zadawanych pytań dotyczących usługi ATA oraz wskazówki i odpowiedzi.


## Gdzie mogę uzyskać licencję dla usługi Advanced Threat Analytics (ATA)?
<a id="where-can-i-get-a-license-for-advanced-threat-analytics-ata" class="xliff"></a>

Jeśli masz aktywną umowę Enterprise Agreement, możesz pobrać oprogramowanie z Centrum licencjonowania zbiorczego firmy Microsoft (VLSC).

Jeśli masz licencję usługi Enterprise Mobility + Security (EMS) uzyskaną bezpośrednio przez portal usługi Office 365 lub w ramach modelu licencjonowania Cloud Solution Partner (CSP) i nie masz dostępu do usługi ATA w Centrum licencjonowania zbiorczego firmy Microsoft (VLSC), skontaktuj się z Pomocą techniczną firmy Microsoft, która udostępni proces aktywacji usługi Advanced Threat Analytics.

## Co zrobić, jeśli nie można uruchomić bramy usługi ATA?
<a id="what-should-i-do-if-the-ata-gateway-wont-start" class="xliff"></a>
Sprawdź ostatni błąd w bieżącym dzienniku błędów (gdzie usługa ATA jest zainstalowana w folderze „Dzienniki”).

## Jak można przetestować usługę ATA?
<a id="how-can-i-test-ata" class="xliff"></a>
Można symulować podejrzane działania, aby wykonać pełny test, wykonując jedną z następujących czynności:

1.  Rekonesans usług DNS przy użyciu pliku Nslookup.exe
2.  Wykonanie zdalne przy użyciu pliku psexec.exe


Musi on zostać zdalnie uruchomiony na monitorowanym kontrolerze domeny, a nie z bramy usługi ATA.

## Które kompilacje usługi ATA odnoszą się do poszczególnych wersji?
<a id="which-ata-build-corresponds-to-each-version" class="xliff"></a>

|Wersja|Numer kompilacji|
|----|----|
|1.6|1.6.4103|
|1.6 Update 1|1.6.4317|
|1.7|1.7.5402| 
|1.7 Update 1|1.7.5647|
|1.7 Update 2|1.7.5757|
|1.8|1.8.6645|

## Której wersji mam użyć, aby uaktualnić moje aktualne wdrożenie usługi ATA do najnowszej wersji?
<a id="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version" class="xliff"></a>

![Macierz uaktualniania wersji usługi ATA](./media/version-matrix.png)


## Jak sprawdzić funkcję przekazywania zdarzeń systemu Windows?
<a id="how-do-i-verify-windows-event-forwarding" class="xliff"></a>
Można umieścić w pliku następujący kod, a następnie uruchomić go z wiersza polecenia w katalogu **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** w następujący sposób:

mongo.exe ATA nazwa_pliku

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## Czy usługa ATA współpracuje z ruchem zaszyfrowanym?
<a id="does-ata-work-with-encrypted-traffic" class="xliff"></a>
Usługa ATA opiera się na analizowaniu wielu protokołów sieciowych, a także zdarzeń zebranych z rozwiązania SIEM lub za pośrednictwem funkcji przekazywania zdarzeń systemu Windows, tak aby mimo braku analizy ruchu szyfrowanego (na przykład LDAPS i IPSEC ESP) mogła nadal działać i szyfrowanie nie miało wpływu na wykrywanie w większości przypadków.

## Czy usługa ATA działa z ochroną protokołu Kerberos?
<a id="does-ata-work-with-kerberos-armoring" class="xliff"></a>
Usługa ATA obsługuje włączanie ochrony protokołu Kerberos, znanej także jako protokół FAST (Flexible Authentication Secure Tunneling), z wyjątkiem wykrywania nadmiernego przekazywania skrótu, które nie będzie działać.

## Ile bram usługi ATA potrzebuję?
<a id="how-many-ata-gateways-do-i-need" class="xliff"></a>

Liczba bram usługi ATA zależy od układu sieci, ilości pakietów i ilości zdarzeń przechwytywanych przez usługę ATA. Aby określić dokładną liczbę, zobacz [Ustalanie rozmiaru uproszczonej bramy usługi ATA](ata-capacity-planning.md#ata-lightweight-gateway-sizing). 

## Ile miejsca do magazynowania potrzebuje usługa ATA?
<a id="how-much-storage-do-i-need-for-ata" class="xliff"></a>
Na każdy pełny dzień przy średniej liczbie 1000 pakietów/sekundę potrzeba 0,3 GB przestrzeni dyskowej.<br /><br />Aby uzyskać więcej informacji o ustalaniu rozmiaru centrum usługi ATA, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).


## Dlaczego niektóre konta są traktowane jako poufne?
<a id="why-are-certain-accounts-considered-sensitive" class="xliff"></a>
Dzieje się tak, gdy konto jest członkiem pewnych grup, które zostały wyznaczone jako poufne (na przykład „Administratorzy domeny”).

Aby dowiedzieć się, dlaczego konto jest poufne, można przejrzeć jego przynależność do grup i zobaczyć, do jakich poufnych grup należy (te grupy mogą być również poufne z powodu innej grupy, a więc ten proces należy kontynuować do momentu zlokalizowania grupy poufnej najwyższego poziomu).

## Jak monitorować kontroler domeny za pomocą usługi ATA?
<a id="how-do-i-monitor-a-virtual-domain-controller-using-ata" class="xliff"></a>
Większość wirtualnych kontrolerów domeny może być objętych przez uproszczoną bramę usługi ATA. Aby określić, czy uproszczona brama usługi ATA jest odpowiednia dla danego środowiska, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

Jeśli wirtualny kontroler domeny nie może być objęty przez uproszczoną bramę usługi ATA, możesz zastosować wirtualne lub fizyczne bramy usługi ATA, zgodnie z opisem w sekcji [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).  <br />Najprostszym sposobem jest zainstalowanie wirtualnej bramy usługi ATA na każdym hoście, na którym znajduje się wirtualny kontroler domeny.<br />Jeśli wirtualne kontrolery domeny są przenoszone między hostami, należy wykonać jedną z następujących czynności:

-   Jeśli wirtualny kontroler domeny jest przenoszony na innego hosta, należy wstępnie skonfigurować bramę usługi ATA na tym hoście, aby odbierać ruch z ostatnio przeniesionego wirtualnego kontrolera domeny.
-   Upewnić się, że wirtualna brama usługi ATA jest powiązana z wirtualnym kontrolerem domeny, tak aby w przypadku jego przeniesienia wirtualna brama usługi ATA była przenoszona razem z nim.
-   Upewnić się, że istnieją przełączniki wirtualne, które mogą przesyłać dane między hostami.

## Jak wykonać kopię zapasową danych usługi ATA?
<a id="how-do-i-back-up-ata" class="xliff"></a>

Zobacz sekcja [Odzyskiwanie usługi ATA po awarii](disaster-recovery.md)



## Co usługa ATA może wykrywać?
<a id="what-can-ata-detect" class="xliff"></a>

Usługa ATA wykrywa znane złośliwe ataki oraz techniki, problemy z zabezpieczeniami i ryzyka.
Pełna lista zagrożeń wykrywanych przez usługę ATA znajduje się w artykule [Jakie zagrożenia wykrywa usługa ATA?](ata-threats.md).

## Jakiego rodzaju magazynu potrzebuje usługa ATA?
<a id="what-kind-of-storage-do-i-need-for-ata" class="xliff"></a>
Firma Microsoft zaleca użycie szybkiego magazynu (nie zaleca się stosowania dysków o prędkości 7200 obr./min) o małych opóźnieniach dostępu do dysku (mniej niż 10 ms). Konfiguracja RAID powinna obsługiwać wysokie obciążenia podczas zapisu danych (nie zaleca się stosowania konfiguracji RAID-5/6 i ich pochodnych).

## Jak wiele kart sieciowych wymaga brama usługi ATA?
<a id="how-many-nics-does-the-ata-gateway-require" class="xliff"></a>
Brama ATA wymaga co najmniej dwóch kart sieciowych:<br>1. Karta sieciowa do łączenia się z siecią wewnętrzną i centrum usługi ATA<br>2. Karta sieciowa, która będzie używana do przechwytywania ruchu sieciowego kontrolera domeny za pomocą funkcji dublowania portów.<br>* Nie dotyczy to uproszczonej bramy usługi ATA, która natywnie wykorzystuje wszystkie karty sieciowe używane przez kontroler domeny.

## Jakiego rodzaju integracji używa usługa ATA z rozwiązaniem SIEM?
<a id="what-kind-of-integration-does-ata-have-with-siems" class="xliff"></a>
Usługa ATA ma dwukierunkową integrację z rozwiązaniem SIEM, zgodnie z poniższym opisem:

1. Usługę ATA można skonfigurować do wysyłania alertu Syslog w razie podejrzanego działania do dowolnego serwera rozwiązania SIEM używającego formatu CEF.
2. Usługę ATA można skonfigurować do odbierania komunikatów usługi Syslog dotyczących zdarzeń systemu Windows z [tych rozwiązań SIEM](install-ata-step6.md).

## Czy usługa ATA monitoruje kontrolery domeny zwirtualizowane w rozwiązaniu IaaS?
<a id="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution" class="xliff"></a>
Tak, możesz użyć uproszczonej bramy usługi ATA do monitorowania kontrolerów domeny w dowolnym rozwiązaniu IaaS.

## Czy ta usługa jest instalowana lokalnie czy jest dostępna w chmurze?
<a id="is-this-an-on-premises-or-in-cloud-offering" class="xliff"></a>
Usługa Microsoft Advanced Threat Analytics jest produktem przeznaczonym do instalacji lokalnej.

## Czy ta usługa będzie częścią usługi Azure Active Directory lub lokalnej usługi Active Directory?
<a id="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory" class="xliff"></a>
To rozwiązanie jest obecnie produktem autonomicznym — nie jest częścią usługi Azure Active Directory ani lokalnej usługi Active Directory.

## Czy trzeba napisać własne reguły i utworzyć wartość progową/linię bazową?
<a id="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline" class="xliff"></a>
W przypadku usługi Microsoft Advanced Threat Analytics nie trzeba tworzyć, a następnie dostosowywać reguł, wartości progowych ani linii bazowych. Usługa ATA analizuje zachowania użytkowników, urządzeń i zasobów oraz ich wzajemne relacje i może szybko wykrywać podejrzane działania i znane ataki. Trzy tygodnie po wdrożeniu usługa ATA zaczyna wykrywać podejrzane zachowania. Natomiast wykrywanie znanych złośliwych ataków i problemów z zabezpieczeniami jest rozpoczynane natychmiast po wdrożeniu usługi ATA.

## Czy usługa Microsoft Advanced Threat Analytics może identyfikować nietypowe zachowanie, jeśli nastąpiło już naruszenie zabezpieczeń?
<a id="if-you-are-already-breached-will-microsoft-advanced-threat-analytics-be-able-to-identify-abnormal-behavior" class="xliff"></a>
Tak. Usługa ATA może wykryć podejrzane działania hakera nawet wtedy, gdy zostanie zainstalowana po naruszeniu zabezpieczeń. Usługa ATA obserwuje nie tylko zachowanie użytkowników, ale także działania dotyczące innych użytkowników w systemie zabezpieczeń organizacji. Podczas początkowej analizy nietypowe zachowanie atakującego jest identyfikowane jako „odstające” i zgłaszane przez usługę ATA. Ponadto usługa ATA może wykryć podejrzane działanie, jeśli haker usiłuje ukraść poświadczenia innego użytkownika (np. wykorzystując atak typu Pass-the-Ticket) lub zdalnie wykonać kod na jednym z kontrolerów domeny.

## Czy usługa korzysta jedynie z ruchu pochodzącego z usługi Active Directory?
<a id="does-this-only-leverage-traffic-from-active-directory" class="xliff"></a>
Oprócz analizowania ruchu związanego z usługą Active Directory przy użyciu technologii głębokiej inspekcji pakietów usługa ATA może również zbierać odpowiednie zdarzenia z rozwiązań SIEM (Security Information and Event Management) i tworzyć profile jednostek na podstawie informacji uzyskanych z usług domenowych Active Directory. Usługa ATA może również zbierać zdarzenia z dzienników zdarzeń, jeśli organizacja skonfiguruje przekazywanie dzienników zdarzeń systemu Windows.

## Co to jest dublowanie portów?
<a id="what-is-port-mirroring" class="xliff"></a>
Dublowanie portów, zwane również funkcją SPAN (Switched Port Analyzer), jest metodą monitorowania ruchu sieciowego. Jeśli funkcja dublowania portów jest włączona, przełącznik wysyła kopie wszystkich pakietów sieciowych przekazywanych przez jeden z portów (lub całą sieć VLAN) do innego portu, gdzie można przeanalizować pakiet.

## Czy usługa ATA monitoruje tylko urządzenia przyłączone do domeny?
<a id="does-ata-monitor-only-domain-joined-devices" class="xliff"></a>
Nie. Usługa ATA monitoruje wszystkie urządzenia w sieci wysyłające żądania uwierzytelniania i autoryzacji do usługi Active Directory, w tym urządzenia z systemem innym niż Windows i urządzenia przenośne.

## Czy usługa ATA monitoruje zarówno konta komputerów, jak i konta użytkowników?
<a id="does-ata-monitor-computer-accounts-as-well-as-user-accounts" class="xliff"></a>
Tak. Kont komputerów (a także innych jednostek) można używać do podejmowania złośliwych działań, dlatego usługa ATA monitoruje zachowanie wszystkich kont komputerów i wszystkie inne jednostki w środowisku.

## Czy usługa ATA może obsługiwać wiele domen i wiele lasów?
<a id="can-ata-support-multi-domain-and-multi-forest" class="xliff"></a>
Usługa Microsoft Advanced Threat Analytics obsługuje środowiska wielu domen w obrębie granicy pojedynczego lasu. Większa liczba lasów wymaga wdrożenia usługi ATA w każdym lesie.

## Czy można przeglądać informacje dotyczące ogólnej kondycji wdrożenia?
<a id="can-you-see-the-overall-health-of-the-deployment" class="xliff"></a>
Tak. Można przeglądać informacje dotyczące ogólnej kondycji wdrożenia i konkretne problemy związane z konfiguracją, łącznością itp. oraz otrzymywać alerty w przypadku wystąpienia problemów tego typu.


## Zobacz też
<a id="see-also" class="xliff"></a>
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

