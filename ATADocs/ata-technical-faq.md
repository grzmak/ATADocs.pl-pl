---
title: Często zadawane pytania dotyczące usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Zawiera listę często zadawanych pytań dotyczących usługi ATA wraz ze skojarzonymi odpowiedziami
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f372b4b85c240079da157052e2c20c46801398be
ms.sourcegitcommit: 39a1ddeb6c9dd0817f92870b711627350b7f6f03
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/08/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*

# <a name="ata-frequently-asked-questions"></a>Usługa ATA — często zadawane pytania
Ten artykuł zawiera listę często zadawanych pytań dotyczących usługi ATA oraz wskazówki i odpowiedzi.


## <a name="where-can-i-get-a-license-for-advanced-threat-analytics-ata"></a>Gdzie mogę uzyskać licencję dla usługi Advanced Threat Analytics (ATA)?

Jeśli masz aktywną umowę Enterprise Agreement, możesz pobrać oprogramowanie z Centrum licencjonowania zbiorczego firmy Microsoft (VLSC).

Jeśli masz licencję usługi Enterprise Mobility + Security (EMS) uzyskaną bezpośrednio przez portal usługi Office 365 lub w ramach modelu licencjonowania Cloud Solution Partner (CSP) i nie masz dostępu do usługi ATA w Centrum licencjonowania zbiorczego firmy Microsoft (VLSC), skontaktuj się z Pomocą techniczną firmy Microsoft, która udostępni proces aktywacji usługi Advanced Threat Analytics.

## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>Co zrobić, jeśli nie można uruchomić bramy usługi ATA?
Sprawdź ostatni błąd w bieżącym dzienniku błędów (gdzie usługa ATA jest zainstalowana w folderze „Dzienniki”).

## <a name="how-can-i-test-ata"></a>Jak można przetestować usługę ATA?
Można symulować podejrzane działania, aby wykonać pełny test, wykonując jedną z następujących czynności:

1.  Rekonesans usług DNS przy użyciu pliku Nslookup.exe
2.  Wykonanie zdalne przy użyciu pliku psexec.exe


Musi on zostać zdalnie uruchomiony na monitorowanym kontrolerze domeny, a nie z bramy usługi ATA.

## <a name="which-ata-build-corresponds-to-each-version"></a>Które kompilacje usługi ATA odnoszą się do poszczególnych wersji?

Do uaktualnienia informacje o wersji, zobacz [ścieżka uaktualnienia ATA](upgrade-path.md).

## <a name="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version"></a>Której wersji mam użyć, aby uaktualnić moje aktualne wdrożenie usługi ATA do najnowszej wersji?

Macierzy uaktualnienia wersji usługi ATA, zobacz [ścieżka uaktualnienia ATA](upgrade-path.md).


## <a name="how-does-the-ata-center-update-its-latest-signatures"></a>Jak Centrum usługi ATA zaktualizować jej najnowszych sygnatur?

Mechanizm wykrywania usługi ATA została rozszerzona o nowej wersji jest zainstalowany w Centrum usługi ATA. Centrum można uaktualnić za pomocą usługi Microsoft Update (MU) lub ręcznie pobrać nową wersję z Centrum pobierania lub licencji woluminu.

## <a name="how-do-i-verify-windows-event-forwarding"></a>Jak sprawdzić funkcję przekazywania zdarzeń systemu Windows?
Można umieścić w pliku następujący kod, a następnie uruchomić go z wiersza polecenia w katalogu **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** w następujący sposób:

mongo.exe ATA nazwa_pliku

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## <a name="does-ata-work-with-encrypted-traffic"></a>Czy usługa ATA współpracuje z ruchem zaszyfrowanym?
Usługa ATA polega na analizowanie wielu protokołów sieciowych, a także zdarzenia zebrane z systemu SIEM lub za pośrednictwem funkcji przekazywania zdarzeń systemu Windows. Wykryć oparte na protokołach sieciowych z ruchem zaszyfrowanym (na przykład: LDAPS i IPSEC) nie zostanie przeanalizowany.


## <a name="does-ata-work-with-kerberos-armoring"></a>Czy usługa ATA działa z ochroną protokołu Kerberos?
Usługa ATA obsługuje włączanie ochrony protokołu Kerberos, znanej także jako protokół FAST (Flexible Authentication Secure Tunneling), z wyjątkiem wykrywania nadmiernego przekazywania skrótu, które nie będzie działać.

## <a name="how-many-ata-gateways-do-i-need"></a>Ile bram usługi ATA potrzebuję?

Liczba bram usługi ATA zależy od układu sieci, ilości pakietów i ilości zdarzeń przechwytywanych przez usługę ATA. Aby określić dokładną liczbę, zobacz [Ustalanie rozmiaru uproszczonej bramy usługi ATA](ata-capacity-planning.md#ata-lightweight-gateway-sizing). 

## <a name="how-much-storage-do-i-need-for-ata"></a>Ile miejsca do magazynowania potrzebuje usługa ATA?
Na każdy pełny dzień przy średniej liczbie 1000 pakietów/sekundę potrzeba 0,3 GB przestrzeni dyskowej.<br /><br />Aby uzyskać więcej informacji o ustalaniu rozmiaru centrum usługi ATA, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).


## <a name="why-are-certain-accounts-considered-sensitive"></a>Dlaczego niektóre konta są traktowane jako poufne?
Dzieje się tak, gdy konto jest członkiem pewnych grup, które zostały wyznaczone jako poufne (na przykład „Administratorzy domeny”).

Aby dowiedzieć się, dlaczego konto jest poufne, można przejrzeć jego przynależność do grup i zobaczyć, do jakich poufnych grup należy (te grupy mogą być również poufne z powodu innej grupy, a więc ten proces należy kontynuować do momentu zlokalizowania grupy poufnej najwyższego poziomu). 

Ponadto można ręcznie oznaczyć użytkownika, grupy lub komputera jako poufne. Aby uzyskać więcej informacji, zobacz [kont poufne Tag](tag-sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>Jak monitorować kontroler domeny za pomocą usługi ATA?
Większość wirtualnych kontrolerów domeny może być objętych przez uproszczoną bramę usługi ATA. Aby określić, czy uproszczona brama usługi ATA jest odpowiednia dla danego środowiska, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md).

Jeśli wirtualny kontroler domeny nie może być objęte przez bramy ATA Lightweight Gateway, może mieć albo wirtualne lub fizyczne bramy usługi ATA, zgodnie z opisem w [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).  <br />Najprostszym sposobem jest zainstalowanie wirtualnej bramy usługi ATA na każdym hoście, na którym znajduje się wirtualny kontroler domeny.<br />Jeśli wirtualne kontrolery domeny są przenoszone między hostami, należy wykonać jedną z następujących czynności:

-   Jeśli wirtualny kontroler domeny jest przenoszony na innego hosta, należy wstępnie skonfigurować bramę usługi ATA na tym hoście, aby odbierać ruch z ostatnio przeniesionego wirtualnego kontrolera domeny.
-   Upewnić się, że wirtualna brama usługi ATA jest powiązana z wirtualnym kontrolerem domeny, tak aby w przypadku jego przeniesienia wirtualna brama usługi ATA była przenoszona razem z nim.
-   Upewnić się, że istnieją przełączniki wirtualne, które mogą przesyłać dane między hostami.

## <a name="how-do-i-back-up-ata"></a>Jak wykonać kopię zapasową danych usługi ATA?

Zobacz sekcja [Odzyskiwanie usługi ATA po awarii](disaster-recovery.md)



## <a name="what-can-ata-detect"></a>Co usługa ATA może wykrywać?

Usługa ATA wykrywa znane złośliwe ataki oraz techniki, problemy z zabezpieczeniami i ryzyka.
Pełna lista zagrożeń wykrywanych przez usługę ATA znajduje się w artykule [Jakie zagrożenia wykrywa usługa ATA?](ata-threats.md).

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>Jakiego rodzaju magazynu potrzebuje usługa ATA?
Firma Microsoft zaleca szybki magazyn (dyski 7200 OBR nie są zalecane) o małych opóźnieniach dostępu do dysku (mniej niż 10 ms). Konfiguracja RAID powinna obsługiwać wysokie obciążenia podczas zapisu danych (nie zaleca się stosowania konfiguracji RAID-5/6 i ich pochodnych).

## <a name="how-many-nics-does-the-ata-gateway-require"></a>Jak wiele kart sieciowych wymaga brama usługi ATA?
Brama ATA wymaga co najmniej dwóch kart sieciowych:<br>1. Karta sieciowa do łączenia się z siecią wewnętrzną i centrum usługi ATA<br>2. Karta sieciowa, która jest używana do przechwytywania ruchu sieciowego kontrolera domeny za pomocą funkcji dublowania portów.<br>* Nie dotyczy to uproszczonej bramy usługi ATA, która natywnie wykorzystuje wszystkie karty sieciowe używane przez kontroler domeny.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>Jakiego rodzaju integracji używa usługa ATA z rozwiązaniem SIEM?
Usługa ATA ma dwukierunkową integrację z rozwiązaniem SIEM, zgodnie z poniższym opisem:

1. Usługę ATA można skonfigurować do wysyłania alertu Syslog do dowolnego serwera rozwiązania SIEM używającego formatu CEF, po wykryciu podejrzanych działań.
2. Usługę ATA można skonfigurować do odbierania komunikatów usługi Syslog dotyczących zdarzeń systemu Windows z [tych rozwiązań SIEM](install-ata-step6.md).

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Czy usługa ATA monitoruje kontrolery domeny zwirtualizowane w rozwiązaniu IaaS?
Tak, możesz użyć uproszczonej bramy usługi ATA do monitorowania kontrolerów domeny w dowolnym rozwiązaniu IaaS.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>Czy ta usługa jest instalowana lokalnie czy jest dostępna w chmurze?
Usługa Microsoft Advanced Threat Analytics jest produktem przeznaczonym do instalacji lokalnej.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Czy ta usługa będzie częścią usługi Azure Active Directory lub lokalnej usługi Active Directory?
To rozwiązanie jest obecnie produktem autonomicznym — nie jest częścią usługi Azure Active Directory ani lokalnej usługi Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Czy trzeba napisać własne reguły i utworzyć wartość progową/punkt odniesienia?
W przypadku usługi Microsoft Advanced Threat Analytics nie trzeba tworzyć, a następnie dostosowywać reguł, wartości progowych ani punktów odniesienia. Usługa ATA analizuje zachowania użytkowników, urządzeń i zasobów oraz ich wzajemne relacje i może szybko wykrywać podejrzane działania i znane ataki. Trzy tygodnie po wdrożeniu usługa ATA zaczyna wykrywać podejrzane zachowania. Natomiast wykrywanie znanych złośliwych ataków i problemów z zabezpieczeniami jest rozpoczynane natychmiast po wdrożeniu usługi ATA.

## <a name="if-you-are-already-breached-can-microsoft-advanced-threat-analytics-identify-abnormal-behavior"></a>Jeśli nastąpiło już naruszenie zabezpieczeń, można Microsoft Advanced Threat Analytics identyfikować nietypowe zachowanie?
Tak. Usługa ATA może wykryć podejrzane działania hakera nawet wtedy, gdy zostanie zainstalowana po naruszeniu zabezpieczeń. Usługa ATA obserwuje nie tylko zachowanie użytkowników, ale także działania dotyczące innych użytkowników w systemie zabezpieczeń organizacji. Podczas początkowej analizy nietypowe zachowanie atakującego jest identyfikowane jako „odstające” i zgłaszane przez usługę ATA. Ponadto usługa ATA może wykryć podejrzane działanie, jeśli haker usiłuje ukraść poświadczenia innego użytkownika (np. wykorzystując atak typu Pass-the-Ticket) lub zdalnie wykonać kod na jednym z kontrolerów domeny.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Czy usługa korzysta jedynie z ruchu pochodzącego z usługi Active Directory?
Oprócz analizowania ruchu związanego z usługą Active Directory przy użyciu technologii głębokiej inspekcji pakietów usługa ATA może również zbierać odpowiednie zdarzenia z rozwiązań SIEM (Security Information and Event Management) i tworzyć profile jednostek na podstawie informacji uzyskanych z usług domenowych Active Directory. Usługa ATA może również zbierać zdarzenia z dzienników zdarzeń, jeśli organizacja skonfiguruje przekazywanie dzienników zdarzeń systemu Windows.

## <a name="what-is-port-mirroring"></a>Co to jest dublowanie portów?
Dublowanie portów, zwane również funkcją SPAN (Switched Port Analyzer), jest metodą monitorowania ruchu sieciowego. Jeśli funkcja dublowania portów jest włączona, przełącznik wysyła kopie wszystkich pakietów sieciowych przekazywanych przez jeden z portów (lub całą sieć VLAN) do innego portu, gdzie można przeanalizować pakiet.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>Czy usługa ATA monitoruje tylko urządzenia przyłączone do domeny?
Nie. Usługa ATA monitoruje wszystkie urządzenia w sieci wysyłające żądania uwierzytelniania i autoryzacji do usługi Active Directory, w tym urządzenia z systemem innym niż Windows i urządzenia przenośne.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>Czy usługa ATA monitoruje zarówno konta komputerów, jak i konta użytkowników?
Tak. Ponieważ komputera konta (a także innych jednostek) może służyć do wykonywania złośliwych działań, usługa ATA monitoruje zachowanie wszystkich kont komputerów i wszystkie inne jednostki w środowisku.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>Czy usługa ATA może obsługiwać wiele domen i wiele lasów?
Usługa Microsoft Advanced Threat Analytics obsługuje środowiska wielu domen w obrębie granicy pojedynczego lasu. Większa liczba lasów wymaga wdrożenia usługi ATA w każdym lesie.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Czy można przeglądać informacje dotyczące ogólnej kondycji wdrożenia?
Tak, można wyświetlić ogólnej kondycji wdrożenia oraz jak określone problemy związane z konfiguracją, łącznością itp. i są alerty w przypadku występowania.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

