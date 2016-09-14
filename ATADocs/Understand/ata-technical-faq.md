---
title: "Często zadawane pytania dotyczące usługi ATA | Microsoft ATA"
description: "Zawiera listę często zadawanych pytań dotyczących usługi ATA wraz ze skojarzonymi odpowiedziami"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b8ad2f343b8397184cd860803f06b0d59c492f5a
ms.openlocfilehash: 96b3ce171ca07bf44163d49b50377fccd6472a08


---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*

# Usługa ATA — często zadawane pytania
Ten artykuł zawiera listę często zadawanych pytań dotyczących usługi ATA oraz wskazówki i odpowiedzi.


## Jak jest licencjonowana usługa ATA?
Informacje o licencji zbiorczej można znaleźć w temacie [Jak kupić usługę Advanced Threat Analytics](https://www.microsoft.com/cloud-platform/advanced-threat-analytics-pricing)


## Co zrobić, jeśli nie można uruchomić bramy usługi ATA?
Sprawdź ostatni błąd w bieżącym dzienniku błędów (gdzie usługa ATA jest zainstalowana w folderze „Dzienniki”).
## Jak można przetestować usługę ATA?
Można symulować podejrzane działania, aby wykonać pełny test, wykonując jedną z następujących czynności:

1.  Rekonesans usług DNS przy użyciu pliku Nslookup.exe
2.  Wykonanie zdalne przy użyciu pliku psexec.exe


Musi on zostać zdalnie uruchomiony na monitorowanym kontrolerze domeny, a nie z bramy usługi ATA.

## Jak sprawdzić funkcję przekazywania zdarzeń systemu Windows?
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
Usługa ATA bazuje na analizowaniu wielu protokołów sieciowych, a także zdarzeń zebranych z rozwiązania SIEM lub za pośrednictwem przesyłania dalej zdarzeń systemu Windows, tak aby mimo braku analizy ruchu szyfrowanego (na przykład LDAPS i IPSEC ESP) usługa ATA mogła nadal działać i nie wpływało to na większość wykryć.

## Czy usługa ATA działa z ochroną protokołu Kerberos?
Usługa ATA obsługuje włączanie ochrony protokołu Kerberos, znanej także jako protokół FAST (Flexible Authentication Secure Tunneling), z wyjątkiem wykrywania nadmiernego przekazywania skrótu, które nie będzie działać.
## Ile bram usługi ATA potrzebuję?

Liczba bram usługi ATA zależy od układu sieci, ilości pakietów i ilości zdarzeń przechwytywanych przez usługę ATA. Aby określić dokładną liczbę, zobacz [Ustalanie rozmiaru bramy ATA Lightweight Gateway](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing). 

## Ile miejsca do magazynowania potrzebuje usługa ATA?
Na każdy pełny dzień przy średniej liczbie 1000 pakietów/sekundę potrzeba 0,3 GB przestrzeni dyskowej.<br /><br />Aby uzyskać więcej informacji o ustalaniu rozmiaru centrum usługi ATA, zobacz [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## Dlaczego niektóre konta są traktowane jako poufne?
Dzieje się tak, gdy konto jest członkiem pewnych grup, które zostały wyznaczone jako poufne (na przykład „Administratorzy domeny”).

Aby dowiedzieć się, dlaczego konto jest poufne, można przejrzeć jego przynależność do grup i zobaczyć, do jakich poufnych grup należy (te grupy mogą być również poufne z powodu innej grupy, a więc ten proces należy kontynuować do momentu zlokalizowania grupy poufnej najwyższego poziomu).

## Jak monitorować kontroler domeny za pomocą usługi ATA?
Większość wirtualnych kontrolerów domeny może być objętych przez bramę ATA Lightweight Gateway. Aby określić, czy brama ATA Lightweight Gateway jest odpowiednia dla danego środowiska, zobacz [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Jeśli wirtualny kontroler domeny nie może być objęty przez bramę ATA Lightweight Gateway, możesz zastosować wirtualne lub fizyczne bramy usługi ATA, zgodnie z opisem w sekcji [Konfigurowanie funkcji dublowania portów](/advanced-threat-analytics/deploy-use/configure-port-mirroring).  <br />Najprostszym sposobem jest zainstalowanie wirtualnej bramy usługi ATA na każdym hoście, na którym znajduje się wirtualny kontroler domeny.<br />Jeśli wirtualne kontrolery domeny są przenoszone między hostami, należy wykonać jedną z następujących czynności:

-   Jeśli wirtualny kontroler domeny jest przenoszony na innego hosta, należy wstępnie skonfigurować bramę usługi ATA na tym hoście, aby odbierać ruch z ostatnio przeniesionego wirtualnego kontrolera domeny.
-   Upewnić się, że wirtualna brama usługi ATA jest powiązana z wirtualnym kontrolerem domeny, tak aby w przypadku jego przeniesienia wirtualna brama usługi ATA była przenoszona razem z nim.
-   Upewnić się, że istnieją przełączniki wirtualne, które mogą przesyłać dane między hostami.

## Jak wykonać kopię zapasową danych usługi ATA?
Istnieją dwa elementy, których kopię zapasową należy wykonać:

-   Ruch i zdarzenia zapisane przez usługę ATA, których kopię zapasową można wykonać przy użyciu dowolnej obsługiwanej procedury tworzenia kopii zapasowej. Aby uzyskać więcej informacji, zobacz [Zarządzanie bazą danych usługi ATA](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   Konfiguracja usługi ATA. Jest przechowywana w bazie danych, a jej kopia zapasowa jest tworzona automatycznie co godzinę w folderze **Backup** w lokalizacji wdrożenia centrum usługi ATA.  Zobacz artykuł [Zarządzanie bazą danych usługi ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/ata-database-management), aby uzyskać więcej informacji.
## Co usługa ATA może wykrywać?
Usługa ATA wykrywa znane złośliwe ataki oraz techniki, problemy z zabezpieczeniami i ryzyka.
Pełna lista zagrożeń wykrywanych przez usługę ATA znajduje się w artykule [Jakie zagrożenia wykrywa usługa ATA?](ata-threats.md).

## Jakiego rodzaju magazynu potrzebuje usługa ATA?
Firma Microsoft zaleca użycie szybkiego magazynu (nie zaleca się stosowania dysków o prędkości 7200 obr./min) o małych opóźnieniach dostępu do dysku (mniej niż 10 ms). Konfiguracja RAID powinna obsługiwać wysokie obciążenia podczas zapisu danych (nie zaleca się stosowania konfiguracji RAID-5/6 i ich pochodnych).

## Jak wiele kart sieciowych wymaga brama usługi ATA?
Brama ATA wymaga co najmniej dwóch kart sieciowych:<br>1. Karta sieciowa do łączenia się z siecią wewnętrzną i centrum usługi ATA<br>2. Karta sieciowa, która będzie używana do przechwytywania ruchu sieciowego kontrolera domeny za pomocą funkcji dublowania portów.<br>* Nie dotyczy to bramy ATA Lightweight Gateway, która natywnie wykorzystuje wszystkie karty sieciowe używane przez kontroler domeny.

## Jakiego rodzaju integracji używa usługa ATA z rozwiązaniem SIEM?
Usługa ATA ma dwukierunkową integrację z rozwiązaniem SIEM, zgodnie z poniższym opisem:

1. Usługę ATA można skonfigurować do wysyłania alertu Syslog w razie podejrzanego działania do dowolnego serwera rozwiązania SIEM używającego formatu CEF.
2. Usługę ATA można skonfigurować do odbierania komunikatów Syslog dotyczących zdarzeń systemu Windows o identyfikatorze 4776 z [tych rozwiązań SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support).

## Czy usługa ATA monitoruje kontrolery domeny zwirtualizowane w rozwiązaniu IaaS?

Tak, możesz użyć bramy ATA Lightweight Gateway do monitorowania kontrolerów domeny w dowolnym rozwiązaniu IaaS.

## Czy ta usługa jest instalowana lokalnie czy jest dostępna w chmurze?
Usługa Microsoft Advanced Threat Analytics jest produktem przeznaczonym do instalacji lokalnej.

## Czy ta usługa będzie częścią usługi Azure Active Directory lub lokalnej usługi Active Directory?
To rozwiązanie jest obecnie produktem autonomicznym — nie jest częścią usługi Azure Active Directory ani lokalnej usługi Active Directory.

## Czy trzeba napisać własne reguły i utworzyć wartość progową/linię bazową?
W przypadku usługi Microsoft Advanced Threat Analytics nie trzeba tworzyć, a następnie dostosowywać reguł, wartości progowych ani linii bazowych. Usługa ATA analizuje zachowania użytkowników, urządzeń i zasobów oraz ich wzajemne relacje i może szybko wykrywać podejrzane działania i znane ataki. Trzy tygodnie po wdrożeniu usługa ATA zaczyna wykrywać podejrzane zachowania. Natomiast wykrywanie znanych złośliwych ataków i problemów z zabezpieczeniami jest rozpoczynane natychmiast po wdrożeniu usługi ATA.

## Czy usługa Microsoft Advanced Threat Analytics może identyfikować nietypowe zachowanie, jeśli nastąpiło już naruszenie zabezpieczeń?
Tak. Usługa ATA może wykryć podejrzane działania hakera nawet wtedy, gdy zostanie zainstalowana po naruszeniu zabezpieczeń. Usługa ATA obserwuje nie tylko zachowanie użytkowników, ale także działania dotyczące innych użytkowników w systemie zabezpieczeń organizacji. Podczas początkowej analizy nietypowe zachowanie atakującego jest identyfikowane jako „odstające” i zgłaszane przez usługę ATA. Ponadto usługa ATA może wykryć podejrzane działanie, jeśli haker usiłuje ukraść poświadczenia innego użytkownika (np. wykorzystując atak typu Pass-the-Ticket) lub zdalnie wykonać kod na jednym z kontrolerów domeny.

## Czy usługa korzysta jedynie z ruchu pochodzącego z usługi Active Directory?
Oprócz analizowania ruchu związanego z usługą Active Directory przy użyciu technologii głębokiej inspekcji pakietów usługa ATA może również zbierać odpowiednie zdarzenia z rozwiązań SIEM (Security Information and Event Management) i tworzyć profile jednostek na podstawie informacji uzyskanych z usług domenowych Active Directory. Usługa ATA może również zbierać zdarzenia z dzienników zdarzeń, jeśli organizacja skonfiguruje przekazywanie dzienników zdarzeń systemu Windows.

## Co to jest dublowanie portów?
Dublowanie portów, zwane również funkcją SPAN (Switched Port Analyzer), jest metodą monitorowania ruchu sieciowego. Jeśli funkcja dublowania portów jest włączona, przełącznik wysyła kopie wszystkich pakietów sieciowych przekazywanych przez jeden z portów (lub całą sieć VLAN) do innego portu, gdzie można przeanalizować pakiet.

## Czy usługa ATA monitoruje tylko urządzenia przyłączone do domeny?
Nie. Usługa ATA monitoruje wszystkie urządzenia w sieci wysyłające żądania uwierzytelniania i autoryzacji do usługi Active Directory, w tym urządzenia z systemem innym niż Windows i urządzenia przenośne.

## Czy usługa ATA monitoruje zarówno konta komputerów, jak i konta użytkowników?
Tak. Kont komputerów (a także innych jednostek) można używać do podejmowania złośliwych działań, dlatego usługa ATA monitoruje zachowanie wszystkich kont komputerów i wszystkie inne jednostki w środowisku.

## Czy usługa ATA może obsługiwać wiele domen i wiele lasów?
Usługa Microsoft Advanced Threat Analytics obsługuje środowiska wielu domen w obrębie granicy pojedynczego lasu. Większa liczba lasów wymaga wdrożenia usługi ATA w każdym lesie.
## Czy można przeglądać informacje dotyczące ogólnej kondycji wdrożenia?
Tak. Można przeglądać informacje dotyczące ogólnej kondycji wdrożenia i konkretne problemy związane z konfiguracją, łącznością itp. oraz otrzymywać alerty w przypadku wystąpienia problemów tego typu.


## Zobacz też
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


