---
title: Azure Advanced Threat Protection — często zadawane pytania | Dokumentacja firmy Microsoft
description: Zawiera listę często zadawanych pytań dotyczących Azure ATP wraz ze skojarzonymi odpowiedziami
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/13/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d7f7f4841c40fb78dc06bae1c06e3c57d2e7f7ee
ms.sourcegitcommit: c77e378d18e654bea4b4af4f24cc941a6659ce99
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
ms.locfileid: "29883954"
---
*Dotyczy: Azure Advanced Threat Protection*

# <a name="azure-atp-frequently-asked-questions"></a>Azure ATP — często zadawane pytania
Ten artykuł zawiera listę często zadawanych pytań dotyczących Azure ATP oraz wskazówki i odpowiedzi.


## <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Gdzie można uzyskać licencji dla Azure Advanced Threat ochrony (ATP)?

W przypadku uzyskania licencji dla pakietu Enterprise Mobility + Security (EMS E5) 5 bezpośrednio za pomocą [portalu usługi Office 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) lub za pośrednictwem modelu licencjonowania partnera rozwiązanie chmury (CSP).                  

## <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Co należy zrobić, jeśli nie można uruchomić Azure ATP czujnika lub czujnik autonomiczny?
Sprawdź ostatni błąd w bieżącym dzienniku błędów (gdzie ATP Azure jest instalowana w folderze "Dzienniki").

## <a name="how-can-i-test-azure-atp"></a>Jak można przetestować Azure ATP?
Można symulować podejrzane działania jako test na trasie, uruchamiając następujące polecenie:

-  Rekonesans usług DNS przy użyciu pliku Nslookup.exe


Musi on zostać zdalnie uruchamiać na monitorowanym kontrolerze domeny, a nie z czujnika autonomiczny Azure ATP.


## <a name="does-azure-atp-work-with-encrypted-traffic"></a>Azure ATP działa z ruchem zaszyfrowanym?
Azure ATP polega na analizowanie wielu protokołów sieciowych, a także zdarzenia zebrane z systemu SIEM lub za pośrednictwem funkcji przekazywania zdarzeń systemu Windows. Wykryć oparte na protokołach sieciowych z ruchem zaszyfrowanym (na przykład: LDAPS i IPSEC) nie zostały przeanalizowane.


## <a name="does-azure-atp-work-with-kerberos-armoring"></a>Azure ATP działa z ochroną protokołu Kerberos?
Włączanie ochrony protokołu Kerberos, znanej także jako FAST Flexible Authentication Secure Tunneling (), jest obsługiwana przez ATP, z wyjątkiem nadmiernego przekazywania wykrywania wyznaczania wartości skrótu, który nie obsługuje ochrony protokołu Kerberos.

## <a name="how-many-azure-atp-sensors-do-i-need"></a>Ile czujniki Azure ATP należy?

Każdy kontroler domeny w środowisku powinny być objęte przez ATP czujnika lub czujnik autonomicznych. Aby uzyskać więcej informacji, zobacz [czujnik Azure ATP zmiany rozmiaru](atp-capacity-planning.md#sizing). 


## <a name="why-are-certain-accounts-considered-sensitive"></a>Dlaczego niektóre konta są traktowane jako poufne?
Dzieje się tak, gdy konto jest członkiem grupy, które są wyznaczone jako poufne (na przykład: "Administratorzy domeny").

Aby dowiedzieć się, dlaczego konto jest poufne, można przejrzeć jego przynależność do grup i zobaczyć, do jakich poufnych grup należy (te grupy mogą być również poufne z powodu innej grupy, a więc ten proces należy kontynuować do momentu zlokalizowania grupy poufnej najwyższego poziomu). Możesz również [tag kont jako poufne ręcznie](sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Jak monitorować wirtualny kontroler domeny przy użyciu Azure ATP?
Większość wirtualnych kontrolerów domeny może być objętych przez czujnik Azure ATP, aby określić, czy Azure ATP czujnik jest odpowiednie dla danego środowiska, zobacz [planowania pojemności ATP Azure](atp-capacity-planning.md).

Jeśli wirtualny kontroler domeny nie może być objęty czujnik Azure ATP, może mieć albo wirtualnych lub fizycznych Azure ATP autonomiczny czujnika zgodnie z opisem w [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).  <br />Najprostszym sposobem ma wirtualnego czujnik autonomiczny Azure ATP na każdym hoście, na którym znajduje się wirtualny kontroler domeny.<br />Jeśli wirtualne kontrolery domeny są przenoszone między hostami, należy wykonać jedną z następujących czynności:

-   Jeśli wirtualny kontroler domeny jest przenoszony na innego hosta, należy wstępnie skonfigurować czujnik autonomiczny Azure ATP na tym hoście, aby odbierać ruch z ostatnio przeniesionego wirtualnego kontrolera domeny.
-   Upewnij się, powiązana z wirtualnych czujnik autonomiczny Azure ATP z wirtualnego kontrolera domeny, tak, aby w przypadku jego przeniesienia czujnik autonomiczny Azure ATP przenoszona razem z nim.
-   Upewnić się, że istnieją przełączniki wirtualne, które mogą przesyłać dane między hostami.


## <a name="what-can-azure-atp-detect"></a>Co może wykrywać Azure ATP?

Azure ATP wykrywa znane złośliwe ataki i techniki, problemy z zabezpieczeniami i zagrożeń.
Aby uzyskać pełną listę zagrożeń wykrywanych przez usługę Azure ATP, zobacz [jakie wykryć jest sprawdzana Azure ATP?](suspicious-activity-guide.md).

## <a name="how-many-nics-does-the-azure-atp-standalone-sensor-require"></a>Jak wiele kart sieciowych wymaga czujnik autonomiczny Azure ATP?
Czujnik autonomiczny Azure ATP wymaga co najmniej dwie karty sieciowe:<br>1. Karta sieciowa nawiązywania połączenia z siecią wewnętrzną i usługi w chmurze Azure ATP<br>2. Karta sieciowa, która jest używana do przechwytywania ruchu sieciowego kontrolera domeny za pomocą funkcji dublowania portów.<br>* Nie dotyczy czujnika Azure ATP, która natywnie wykorzystuje wszystkie karty sieciowe, które używa kontrolera domeny.

## <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Jakiego rodzaju integracji Azure ATP ma z rozwiązaniem Siem?
Azure ATP ma dwukierunkową integrację z rozwiązaniem Siem w następujący sposób:

1. Azure ATP można skonfigurować do wysyłania alertu Syslog do dowolnego serwera rozwiązania SIEM używającego formatu CEF, alerty dotyczące kondycji i po wykryciu podejrzanych działań.
2. Azure ATP można skonfigurować do odbierania alertu SYSLOG dla zdarzeń systemu Windows z [tych rozwiązań Siem](configure-event-collection.md).

## <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Jak skonfigurować czujników Azure ATP do komunikowania się z usługą w chmurze Azure ATP, gdy serwer proxy?

Dla kontrolerów domeny do komunikowania się z usługą w chmurze, należy otworzyć: *. atp.azure.com portu 443 w zaporą/serwera proxy. Aby uzyskać instrukcje, jak to zrobić, zobacz [skonfigurować serwera proxy lub zapory, aby umożliwić komunikację z czujników Azure ATP](configure-proxy.md).
 

## <a name="can-azure-atp-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Azure ATP można monitorować kontrolerów domeny zwirtualizowanych w rozwiązaniu IaaS?
Tak, można użyć czujnik Azure ATP do monitorowania kontrolerów domeny, które znajdują się w dowolnym rozwiązaniu IaaS.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Czy ta usługa będzie częścią usługi Azure Active Directory lub lokalnej usługi Active Directory?
To rozwiązanie jest obecnie autonomiczny oferty. Nie jest częścią usługi Azure Active Directory lub lokalnej usługi Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Czy trzeba napisać własne reguły i utworzyć wartość progową/punkt odniesienia?
Z usługi Azure Advanced Threat Protection jest niepotrzebna do utworzenia reguły, wartości progowych ani linii bazowych, a następnie dostosowywać. Azure ATP analizuje zachowania użytkowników, urządzeń i zasobów, oraz ich wzajemne relacje — i może szybko wykrywać podejrzane działania i znane ataki szybkie. Trzy tygodnie po wdrożeniu Azure ATP zaczyna wykrywać podejrzane zachowania. Z drugiej strony Azure ATP rozpocznie się wykrywanie znanych złośliwych ataków i problemów z zabezpieczeniami natychmiast po wdrożeniu.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Czy usługa korzysta jedynie z ruchu pochodzącego z usługi Active Directory?
Oprócz analizowania ruchu usługi Active Directory przy użyciu technologii głębokiej inspekcji pakietów, Azure ATP również zbiera odpowiednie zdarzenia z Security Information and Event Management (SIEM) i tworzy profile jednostek na podstawie informacji z usługi Active Directory Usługi domenowe. Jeśli używasz czujnik Azure ATP go wyodrębnia te zdarzenia automatycznie. Do wysyłania tych zdarzeń do czujnik autonomiczny Azure ATP, można użyć funkcji przekazywania zdarzeń systemu Windows. Azure ATP obsługuje również odbierania ewidencjonowania aktywności usługi RADIUS sieci VPN dzienników pochodzących od różnych producentów (Microsoft, Cisco F5 i punktu kontrolnego).

## <a name="what-is-port-mirroring"></a>Co to jest dublowanie portów?
Dublowanie portów, zwane również funkcją SPAN (Switched Port Analyzer), jest metodą monitorowania ruchu sieciowego. Jeśli funkcja dublowania portów jest włączona, przełącznik wysyła kopie wszystkich pakietów sieciowych przekazywanych przez jeden z portów (lub całą sieć VLAN) do innego portu, gdzie można przeanalizować pakiet.

## <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Azure ATP monitoruje tylko urządzenia przyłączone do domeny?
Nie. Azure ATP monitoruje wszystkie urządzenia w sieci wysyłające żądania uwierzytelniania i autoryzacji w usłudze Active Directory, łącznie z systemem innym niż Windows i urządzenia przenośne.

## <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Azure ATP monitorować konta komputera, a także konta użytkowników?
Tak. Ponieważ komputera konta (a także innych jednostek) może służyć do wykonywania złośliwych działań, Azure ATP monitoruje zachowanie wszystkich kont komputerów i wszystkie inne jednostki w środowisku.

## <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Można Azure ATP obsługuje wiele domen i wiele lasów?
Azure Advanced Threat Protection obsługuje w środowiskach wielu domen w obrębie tego samego lasu. Wiele lasów wymaga obszarem roboczym Azure ATP dla każdego lasu.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Czy można przeglądać informacje dotyczące ogólnej kondycji wdrożenia?
Tak, można wyświetlić ogólnej kondycji wdrożenia oraz jak określone problemy związane z konfiguracją, łącznością itp. i są alerty w przypadku występowania.

## <a name="what-data-does-azure-atp-collect"></a>Jakie dane zbiera Azure ATP? 
Azure ATP zbiera i przechowuje informacje z serwerów skonfigurowanych (kontrolery domeny, serwery Członkowskie, itp.) w bazie danych specyficznych dla usług administracji, monitorowania i raportowania. Zbierane informacje obejmują ruch sieciowy do i z kontrolerów domeny (np. uwierzytelnianie Kerberos, NTLM, uwierzytelniania, zapytania DNS), dzienniki zabezpieczeń (na przykład zdarzeń zabezpieczeń systemu Windows), informacji usługi Active Directory (struktury, podsieci, witryn) i informacje o jednostce (takich jak nazwy, adresy e-mail i numery telefonów). 

Firma Microsoft używa tych danych na: 

-   Aktywne identyfikowanie wskaźniki ataku (IOAs) w organizacji 
-   Generuj alerty, jeśli wykryto możliwych ataków 
-   Podaj operacje zabezpieczeń z widokiem do jednostek pokrewnych sygnałów zagrożeń z sieci, dzięki któremu można zbadać i obecności zagrożenia bezpieczeństwa w sieci. 

Microsoft nie moje dane do celów reklamowych lub do innych celów innych niż dostarczać usługę. 

## <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Czy mają możliwość wybrać miejsce przechowywania danych? 

Podczas tworzenia obszaru roboczego Azure ATP, możesz wybrać do przechowywania danych, można przechowywać dane w centrach danych Microsoft Azure w Stanach Zjednoczonych lub w Europie. Po skonfigurowaniu, nie można zmienić lokalizacji przechowywania danych. Microsoft nie zostaną przeniesione dane z określonej lokalizacji. 

## <a name="is-my-data-isolated-from-other-customer-data"></a>Czy moje dane izolowane od innych danych klientów? 

Tak, dane są izolowane za pośrednictwem podział logiczną na podstawie identyfikatora klienta i uwierzytelnianie dostępu do. Każdy klient ma dostęp tylko do danych zbieranych z własnej organizacji i rodzajowy dane, które firma Microsoft udostępnia. 

## <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Jak Microsoft zapobiegają działania złośliwe oprogramowanie i nadużywania ról wysokim poziomie uprawnień? 

Deweloperzy firmy Microsoft i administratorów zgodnie z projektem, mieć wystarczające uprawnienia do wykonywania ich obowiązków przydzielonych do obsługi i rozwijać usługi. Microsoft wdraża kombinacje zapobiegawczych, detektyw i reaktywne formantów, w tym następujących mechanizmów, aby zapewnić ochronę przed nieautoryzowanym deweloperów i/lub działanie administracyjne: 

-   Kontrola ścisłej dostępu do danych poufnych 
-   Kombinacje formantów, które znacznie zwiększyć niezależne wykrywania złośliwych działań 
-   Wiele poziomów monitorowania, rejestrowania i raportowania 

Ponadto firma Microsoft przeprowadza kontrole weryfikacji na niektórych personel i ogranicza dostęp do aplikacji, systemów i infrastruktury sieci proporcjonalnie do poziomu weryfikacji tła. Personel wykonaj formalnego procesu, gdy są one wymagane uzyskać dostęp do konta klienta lub powiązane informacje w trakcie wykonywania obowiązków. 

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Planowanie pojemności Azure w ATP](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
