---
title: Usługa Azure Advanced Threat Protection — często zadawane pytania | Dokumentacja firmy Microsoft
description: Zawiera listę często zadawanych pytań dotyczących usługi Azure ATP wraz ze skojarzonymi odpowiedziami
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/2/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 33493463eeb4ed23e33d81c9eb60b17c23285649
ms.sourcegitcommit: 0634dda829699edf8bfd984eb9f896a67c5b15e7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/02/2018
ms.locfileid: "48039400"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="azure-atp-frequently-asked-questions"></a>Narzędzie Azure ATP — często zadawane pytania
Ten artykuł zawiera listę często zadawanych pytań i odpowiedzi na pytania dotyczące usługi Azure ATP podzielone na następujące catergories: 
- [Co to jest Azure ATP](#What-is-Azure-ATP)
- [Licencjonowanie i ochrona prywatności](#Licensing-and-privacy)
- [Wdrożenia](#Deployment)
- [Operacje](#Operations)
- [Rozwiązywanie problemów](#Troubleshooting)

## <a name="what-is-azure-atp"></a>Co to jest Azure ATP?

### <a name="what-can-azure-atp-detect"></a>Co można wykryć usługi Azure ATP?

Narzędzie Azure ATP wykrywa znane złośliwe ataki i techniki, problemy z zabezpieczeniami i ryzyka.
Aby uzyskać pełną listę zagrożeń wykrywanych narzędzia Azure ATP, zobacz [jakie zagrożenia wykrywa powoduje wykonania narzędzia Azure ATP?](suspicious-activity-guide.md).

### <a name="what-data-does-azure-atp-collect"></a>Jakie dane są zbierane w narzędzia Azure ATP 
Narzędzie Azure ATP zbiera i przechowuje informacje z serwerów skonfigurowanych (kontrolery domeny, serwery członkowskie itp.) w bazie danych określonej do usługi w przypadku administracja, śledzenia i raportowania. Zbierane informacje dotyczące ruchu sieciowego do i z kontrolerów domeny (na przykład uwierzytelnianie Kerberos, uwierzytelniania NTLM, zapytania DNS), dzienniki zabezpieczeń (np. Windows zdarzenia zabezpieczeń), informacji usługi Active Directory (struktura, podsieci, witryn) i informacji dotyczących jednostki (takie jak nazwy, adresy e-mail i numery telefonów). 

Firma Microsoft wykorzystuje te dane, aby: 

-   Proaktywnej identyfikacji wskaźniki ataku (IOAs) w Twojej organizacji 
-   Generuj alerty, jeśli wykryto możliwych ataków 
-   Podaj operacji zabezpieczeń przy użyciu widoku do podmiotów powiązanych sygnałów przed zagrożeniami z sieci, dzięki któremu można zbadać i Poznaj obecności zagrożenia bezpieczeństwa w sieci. 

Microsoft nie Moje danych do celów reklamowych i do żadnych innych celów innych niż zapewnia usługa. 

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>Usługi Azure ATP jedynie z ruchu pochodzącego z usługi Active Directory?
Oprócz analizowania ruchu usługi Active Directory przy użyciu technologii głębokiej inspekcji pakietów, narzędzia Azure ATP również zbiera odpowiednie zdarzenia z Security Information and Event Management (SIEM) i tworzy profile jednostek na podstawie informacji z usługi Active Directory Usługi domenowe. Jeśli używasz czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, wyodrębnia te zdarzenia automatycznie. Windows funkcji przekazywania zdarzeń służy do wysyłania tych zdarzeń do usługi Azure ATP czujnik autonomiczny. Narzędzie Azure ATP obsługuje również odbieranie ewidencjonowania aktywności usługi RADIUS sieci VPN dzienników pochodzących od różnych dostawców (firmy Microsoft, Cisco, F5 i punktu kontrolnego).

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Usługi Azure ATP monitoruje tylko urządzenia przyłączone do domeny?
Nie. Narzędzie Azure ATP monitoruje wszystkie urządzenia w sieci wysyłające żądania uwierzytelniania i autoryzacji w usłudze Active Directory, w tym innych niż Windows i urządzenia przenośne.

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Usługi Azure ATP monitorować konta komputera, a także kont użytkowników?
Tak. Ponieważ komputer konta (a także innych jednostek) może służyć do wykonywania złośliwych działań, narzędzia Azure ATP monitoruje zachowanie wszystkich kont komputerów i wszystkie inne jednostki w środowisku.

## <a name="licensing-and-privacy"></a>Licencjonowanie i ochrona prywatności 
### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Gdzie można uzyskać licencję dla usługi Azure Advanced Threat Protection (ATP)?

Można uzyskać licencji dla pakietu Enterprise Mobility + Security (EMS E5) 5 bezpośrednio za pośrednictwem [portalu usługi Office 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) lub za pomocą modelu licencjonowania Cloud Solution Partner (CSP).  

### <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Czy ta usługa będzie częścią usługi Azure Active Directory lub lokalnej usługi Active Directory?
To rozwiązanie jest obecnie autonomiczny oferty. Go nie jest częścią usługi Azure Active Directory lub lokalnej usługi Active Directory.

### <a name="is-my-data-isolated-from-other-customer-data"></a>Czy moje dane są izolowane od innych danych klienta? 

Tak, Twoje dane są izolowane poprzez podział logiczną na podstawie identyfikatora klienta i uwierzytelnianie dostępu do. Każdy klient dostęp tylko do danych zbieranych z organizacji i ogólne dane, które firma Microsoft udostępnia.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Należy wybrać miejsce przechowywania danych? 

Podczas tworzenia obszaru roboczego usługi Azure ATP, możesz przechowywać dane, można przechowywać dane w centrach danych Microsoft Azure w Stanach Zjednoczonych lub Europy. Po skonfigurowaniu nie można zmienić lokalizację przechowywania danych. Firma Microsoft nie będzie przenosić dane z określonej lokalizacji.                

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Jak Microsoft zapobiec działań intruzowi i nadużycia związane z wysokim poziomie uprawnień ról? 

Microsoft deweloperom i administratorom zgodnie z projektem, mieć wystarczające uprawnienia do wykonywania ich obowiązków przypisane do obsługi i rozwijać usługę. Firma Microsoft wdraża kombinacji zapobiegawczych, detektyw i reaktywne kontrolek, w tym następujących mechanizmów, aby ułatwić ochronę przed nieautoryzowanym dla deweloperów i/lub działanie administracyjne: 

-   Kontrola ścisłej dostępu do poufnych danych 
-   Kombinacje elementów sterujących, które znacznie zwiększyć, niezależnie od wykrywania złośliwych działań 
-   Wiele poziomów monitorowania, rejestrowania i raportowania 

Ponadto firma Microsoft przeprowadza testy weryfikacyjne opisane w tle na niektórych personel i ogranicza dostęp do aplikacji, systemów i infrastruktury sieciowej proporcjonalnie poziom weryfikacji tła. Personel postępuj zgodnie z formalnym procesem żądanie dostępu do konta klienta lub powiązane informacje w trakcie wykonywania ich zadań. 

## <a name="deployment"></a>wdrażania
### <a name="how-many-azure-atp-sensors-do-i-need"></a>Jak wiele czujników narzędzia Azure ATP jest potrzebne?

Każdy kontroler domeny w środowisku powinny być objęte przez zaawansowanej ochrony przed zagrożeniami czujnik lub czujnik autonomiczny. Aby uzyskać więcej informacji, zobacz [czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure rozmiaru](atp-capacity-planning.md#sizing). 

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>Narzędzia Azure ATP działa z ruchem zaszyfrowanym?
Narzędzie Azure ATP opiera się na analizowaniu wielu protokołów sieciowych, a także zdarzeń zebranych z rozwiązania SIEM lub za pośrednictwem funkcji przekazywania zdarzeń Windows.  Protokoły sieciowe przy użyciu ruchu szyfrowanego (na przykład LDAPS i IPSEC) nie są odszyfrowywane, ale są analizowane.

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>Narzędzia Azure ATP działa z ochroną protokołu Kerberos?
Włączanie ochrony protokołu Kerberos, znanej także jako elastyczne Authentication Secure Tunneling (FAST), jest obsługiwana przez zaawansowanej ochrony przed zagrożeniami, z wyjątkiem nadmiernego przekazywania wykrywanie wyznaczania wartości skrótu, które nie obsługuje ochrony protokołu Kerberos.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Jak monitorować wirtualnego kontrolera domeny przy użyciu narzędzia Azure ATP?
Większość wirtualnych kontrolerów domeny może być objętych przez czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, aby ustalić, czy narzędzia Azure ATP czujnik jest odpowiednie dla danego środowiska, zobacz [Planowanie pojemności zaawansowanej ochrony przed zagrożeniami w usłudze Azure](atp-capacity-planning.md).

Jeśli wirtualny kontroler domeny nie może być objęty czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, może mieć albo wirtualny lub fizyczny narzędzia Azure ATP czujnik autonomiczny, zgodnie z opisem w [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md).  <br />Najprostszym sposobem jest wirtualny czujnik autonomiczny narzędzia Azure ATP na każdym hoście, na którym znajduje się wirtualny kontroler domeny.<br />Jeśli wirtualne kontrolery domeny są przenoszone między hostami, należy wykonać jedną z następujących czynności:

-   Jeśli wirtualny kontroler domeny jest przenoszony na innego hosta, należy wstępnie skonfigurować czujnik autonomiczny narzędzia Azure ATP na tym hoście, aby odbierać ruch z ostatnio przeniesionego wirtualnego kontrolera domeny.
-   Upewnij się, stowarzyszony wirtualnego czujnik autonomiczny narzędzia Azure ATP z wirtualnym kontrolerem domeny, tak aby w przypadku jego przeniesienia czujnik autonomiczny narzędzia Azure ATP z nim.
-   Upewnić się, że istnieją przełączniki wirtualne, które mogą przesyłać dane między hostami.

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Jak skonfigurować usługi Azure ATP czujników do komunikowania się z usługą w chmurze usługi Azure ATP, gdy serwer proxy?

Dla kontrolerów domeny do komunikowania się z usługą w chmurze, możesz otworzyć: *. atp.azure.com portu 443 w zapory/serwera proxy. Aby uzyskać instrukcje, jak to zrobić, zobacz [konfigurowania serwera proxy lub zapory, aby umożliwić komunikację za pomocą narzędzia Azure ATP czujników](configure-proxy.md).

### <a name="can-azure-atp-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Narzędzia Azure ATP monitorować kontrolery domeny zwirtualizowane w rozwiązaniu IaaS?
Tak, można użyć czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure do monitorowania kontrolerów domeny, które znajdują się w dowolnym rozwiązaniu IaaS.

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Narzędzia Azure ATP może obsługiwać, obejmujące wiele domen i wiele lasów?
Usługa Azure Advanced Threat Protection obsługuje środowiska wielu domen i lasów. Ta funkcja jest obecnie w publicznej wersji zapoznawczej. Aby uzyskać dodatkowe informacje i znane ograniczenia, zobacz [obsługi wielu lasów](atp-multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Czy można przeglądać informacje dotyczące ogólnej kondycji wdrożenia?
Tak, można wyświetlić ogólnej kondycji wdrożenia oraz jak określonych problemach związanych z konfiguracji, łącznością itp., a alerty są wyzwalane w momencie ich wystąpienia.

## <a name="operation"></a>Operacja

### <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Jakiego rodzaju integracji usługi Azure ATP ma z rozwiązaniem Siem?
Narzędzie Azure ATP ma dwukierunkową integrację z rozwiązaniem Siem w następujący sposób:

1. Narzędzie Azure ATP można skonfigurować do wysyłania alertu Syslog do dowolnego serwera rozwiązania SIEM używającego formatu CEF, alerty dotyczące kondycji i po wykryciu podejrzanych działań.
2. Narzędzie Azure ATP można skonfigurować do odbierania komunikatów Syslog dotyczących zdarzeń Windows [tych rozwiązań Siem](configure-event-collection.md).

### <a name="why-are-certain-accounts-considered-sensitive"></a>Dlaczego niektóre konta są traktowane jako poufne?
Tak się stanie, gdy konto jest członkiem grupy, które są oznaczone jako poufne (na przykład: "Administratorzy domeny").

Aby dowiedzieć się, dlaczego konto jest poufne, można przejrzeć jego przynależność do grup i zobaczyć, do jakich poufnych grup należy (te grupy mogą być również poufne z powodu innej grupy, a więc ten proces należy kontynuować do momentu zlokalizowania grupy poufnej najwyższego poziomu). Możesz również [tag kont jako poufne ręcznie](sensitive-accounts.md).

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Czy trzeba napisać własne reguły i utworzyć wartość progową/punkt odniesienia?
Za pomocą usługi Azure Advanced Threat Protection nie ma potrzeby do tworzenia reguł, progi lub odniesienia, a następnie dostosowywać. Narzędzie Azure ATP analizuje zachowania użytkowników, urządzeń i zasobów — oraz ich wzajemne relacje ze sobą — i może wykrywać podejrzane działania i znane ataki szybko. Trzy tygodnie po wdrożeniu usługi Azure ATP zaczyna wykrywać podejrzane zachowania. Z drugiej strony narzędzia Azure ATP rozpocznie się wykrywanie znanych złośliwych ataków i problemów z zabezpieczeniami bezpośrednio po wdrożeniu.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Co należy zrobić, jeśli nie uruchomi się narzędzia Azure ATP czujnik lub czujnik autonomiczny?
Szukaj na najnowszy błąd w bieżącym błąd [dziennika](troubleshooting-atp-using-logs.md) (gdzie narzędzia Azure ATP jest zainstalowany w folderze "Dzienniki").

### <a name="how-can-i-test-azure-atp"></a>Jak mogę przetestować narzędzia Azure ATP
Jako test end-to-end można symulować podejrzane działania. W poniższym scenariuszu jest symulowane DNS reconnaisance:

1.  Sprawdź usługi Azure ATP czujników są zainstalowane i skonfigurowane na kontrolerach domeny (lub autonomiczny czujniki i powiązane dublowanie portów są zainstalowane i skonfigurowane)
2.  Otwórz CMD
3.  Uruchom następujące polecenie: nslookup —<DC iP address>
    -   Naciśnij klawisz enter
    -   Typ: -D jest <FQDN>
    -   W zależności od konfiguracji środowiska odpowiedzi będzie się różnić od "Odrzucono kwerendę" na listę rekordów DNS. 
4. Wyświetl alert związane z symulowanego reconnaisance DNS w konsoli usługi Azure ATP. 

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Rozwiązywanie problemów](troubleshooting-atp-known-issues.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
