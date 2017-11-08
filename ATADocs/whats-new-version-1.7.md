---
title: "Co nowego w wersji 1.7 usługi ATA | Dokumentacja firmy Microsoft"
description: "Lista nowości oraz znanych problemów w wersji 1.7 usługi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: be9ee613-4eb3-40f1-8973-e7f0a707ff57
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 7bbca4eeb6ad8c5b9cf161f60144bbd27ca3c8d2
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
# <a name="whats-new-in-ata-version-17"></a>Co nowego w wersji 1.7 usługi ATA
Te informacje o wersji zawierają znane problemy w tej wersji usługi Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-17-update"></a>Co nowego w aktualizacji usługi ATA do wersji 1.7?
Aktualizacja usługi ATA do wersji 1.7 zapewnia następujące ulepszenia:

-   Nowe i zaktualizowane funkcje wykrywania

-   Kontrola dostępu oparta na rolach

-   Obsługa systemu Windows Server 2016 i Windows Server 2016 Core

-   Ulepszenia środowiska użytkownika

-   Drobne zmiany


### <a name="new--updated-detections"></a>Nowe i zaktualizowane funkcje wykrywania


- **Rekonesans przy użyciu wyliczania usług katalogowych** W ramach fazy rekonesansu osoby atakujące zbierają informacje dotyczące jednostek w sieci przy użyciu różnych metod. Wyliczanie usług katalogowych przy użyciu protokołu SAM-R pozwala osobom atakującym uzyskać listę użytkowników i grup w domenie oraz zrozumieć interakcję między różnymi jednostkami. 

- **Ulepszenia wykrywania ataków „pass the hash”** W celu zwiększenia wykrywania ataków „pass the hash” dodaliśmy dodatkowe modele zachowań dla wzorców uwierzytelniania jednostek. Modele te pozwalają usłudze ATA korelować zachowania jednostki z podejrzanymi uwierzytelnieniami NTLM i odróżniać prawdziwe ataki „pass the hash” od innych, podobnych scenariuszy.

- **Ulepszenia wykrywania ataków „pass the ticket”** Pomyślnie wykrywanie zaawansowanych ataków, a w szczególności ataków „pass the ticket”, wymaga dokładnej korelacji między adresem IP a kontem komputera. Jest to wyzwaniem w środowiskach, gdzie adresy IP z założenia szybko się zmieniają (na przykład w sieciach Wi-Fi i przy wielu maszynach wirtualnych korzystających z tego samego hosta). Aby stawić czoła temu wyzwaniu i zwiększyć dokładność wykrywania ataków „pass the ticket”, aparat rozpoznawania nazw sieciowych (NNR) usługi ATA został znacznie poprawiony w celu zmniejszenia ilości fałszywych alarmów.

- **Ulepszenia wykrywania nietypowych zachowań** W usłudze ATA 1.7 dane uwierzytelniania NTLM zostały dodane jako źródła danych służące do wykrywania nietypowych zachowań, umożliwiając działanie algorytmów o szerszym zakresie rozpoznawania zachowania jednostek w sieci. 

- **Ulepszenia wykrywania nietypowych implementacji protokołów** Usługa ATA wykrywa teraz nietypowe implementacje protokołów w protokole Kerberos oraz dodatkowe nieprawidłowości w protokole NTLM. W szczególności te nowe anomalie dotyczące protokołu Kerberos są często używane podczas ataków „pass the hash”.


### <a name="infrastructure"></a>Infrastruktura

- **Kontrola dostępu na podstawie roli** Obsługa kontroli dostępu opartej na rolach (RBAC). Usługa ATA 1.7 zawiera trzy role: administrator ATA, analityk ATA i wykonawca ATA.

- **Obsługa systemu Windows Server 2016 i Windows Server Core** Usługa ATA 1.7 obsługuje wdrażanie bram Lightweight Gateway na kontrolerach domeny z systemami Windows Server 2008 R2 z dodatkiem SP1 (bez instalacji Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (z instalacją Core, ale nie Nano). Ponadto ta wersja obsługuje system Windows Server 2016 w przypadku obu składników: centrum usługi ATA i bramy usługi ATA.

### <a name="user-experience"></a>Czynności po stronie użytkownika
- **Środowisko konfiguracji** Środowisko konfiguracji usługi ATA zostało w tej wersji przeprojektowane dla wygody użytkowników i w celu lepszej obsługi środowisk z wieloma bramami ATA. W tej wersji wprowadzono także stronę aktualizacji bramy ATA w celu prostszego, lepszego zarządzania automatycznymi aktualizacjami różnych bram.

## <a name="known-issues"></a>Znane problemy
W tej wersji występują następujące znane problemy.

### <a name="gateway-automatic-update-may-fail"></a>Automatyczna aktualizacja bramy może zakończyć się niepowodzeniem
**Objawy:** W środowiskach z wolnymi łączami sieci WAN aktualizacja bramy ATA może osiągnąć limit czasu aktualizacji (100 sekund) i zakończyć się niepowodzeniem.
W konsoli usługi ATA brama ATA będzie mieć stan „Aktualizowanie (pobieranie pakietu)” przez długi czas i ostatecznie zakończy się niepomyślnie.
**Obejście:** Aby obejść ten problem, pobierz najnowszy pakiet bramy ATA z konsoli ATA i ręcznie zaktualizuj bramę ATA.

 > [!IMPORTANT]
 Automatyczne odnawianie certyfikatów używanych przez usługę ATA nie jest obsługiwane. Użycie tych certyfikatów może spowodować, że usługa ATA przestanie działać w przypadku automatycznego odnowienia certyfikatu. 

### <a name="no-browser-support-for-jis-encoding"></a>Brak obsługi kodowania JIS w przeglądarce
**Objawy:** konsola ATA może nie działać zgodnie z oczekiwaniami w przeglądarkach wykorzystujących kodowanie JIS. **Obejście:** zmień kodowanie przeglądarki na Unicode UTF-8.
 
### <a name="dropped-port-mirror-traffic-when-using-vmware"></a>Porzucony ruch sieciowy na zdublowanym porcie podczas korzystania z programu VMware

Alerty dotyczące porzuconego ruchu sieciowego na zdublowanym porcie podczas korzystania z lekkiej bramy w programie VMware.

Jeśli używasz kontrolerów domeny na maszynach wirtualnych programu VMware, możesz odbierać alerty dotyczące **porzuconego ruchu sieciowego na zdublowanym porcie**. Może to dziać się z powodu niezgodności konfiguracji w programie VMware. Aby zapobiegać tym alertom, można sprawdzić, czy następujące ustawienia maszyny wirtualnej są ustawione na 0 lub wyłączone:  

- TsoEnable (Włączanie TSO)
- LargeSendOffload (IPv4) (Odciążanie dużego wysyłania ruchu IPv4)
- IPv4 TSO Offload (Odciążanie TSO IPv4)

Należy również rozważyć wyłączenie ustawienia IPv4 Giant TSO Offload (Bardzo duże odciążanie TSO IPv4). Aby uzyskać więcej informacji, zapoznaj się z dokumentacją programu VMware.

### <a name="automatic-gateway-update-fail-when-updating-to-17-update-1"></a>Nie można zaktualizować bramy automatycznej podczas aktualizowania do wersji 1.7 Update 1

Podczas aktualizowania usługi ATA 1.7 do wersji ATA 1.7 Update 1 procesy automatycznej aktualizacji bramy usługi ATA i ręcznej instalacji bram przy użyciu pakietu bramy mogą przebiegać niezgodnie z oczekiwaniami.
Ten problem występuje, jeśli certyfikat używany przez centrum usługi ATA został zmieniony przed zaktualizowaniem usługi ATA.
Aby zweryfikować ten problem, zapoznaj się z dziennikiem **Microsoft.Tri.Gateway.Updater.log** w bramie usługi ATA i zwróć uwagę na następujące wyjątki: **System.Net.Http.HttpRequestException: Wystąpił błąd podczas wysyłania żądania. ---> System.Net.WebException: Połączenie podstawowe zostało zamknięte: wystąpił nieoczekiwany błąd podczas wysyłania.---> System.IdentityModel.Tokens.SecurityTokenValidationException: Nie można zweryfikować odcisku palca certyfikatu**

![usterka bramy podczas aktualizacji usługi ATA](media/17update_gatewaybug.png)

Aby rozwiązać ten problem, po zmianie certyfikatu w wierszu polecenia z podwyższonym poziomem uprawnień przejdź do następującej lokalizacji: **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** i uruchom następujące elementy:

1. Mongo.exe ATA (ciąg „ATA” należy zapisać przy użyciu wielkich liter) 

2. CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;

3. db.SystemProfile.update({_t:"ServiceSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}}, {multi: true})

### <a name="export-suspicious-activity-details-to-excel-may-fail"></a>Eksportowanie szczegółów podejrzanego działania do programu Excel może zakończyć się błędem
Jeśli próbujesz wyeksportować szczegóły podejrzanego działania do pliku programu Excel, operacja może zakończyć się następującym błędem: *Błąd [BsonClassMapSerializer`1] System.FormatException: Wystąpił błąd podczas deserializacji właściwości Activity klasy Microsoft.Tri.Common.Data.NetworkActivities.SuspiciousActivityActivity: Element „ResourceIdentifier” nie pasuje do żadnego pola ani właściwości klasy Microsoft.Tri.Common.Data.EventActivities.NtlmEvent. ---> System.FormatException: Element „ResourceIdentifier” nie pasuje do żadnego pola ani właściwości klasy Microsoft.Tri.Common.Data.EventActivities.NtlmEvent.*

Aby rozwiązać ten problem, z wiersza polecenia z podwyższonym poziomem uprawnień, przejdź do następującej lokalizacji: **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** i uruchom następujące polecenia:
1.  `Mongo.exe ATA`(Musi być Wielka ATA)
2.  `db.SuspiciousActivityActivity.update({ "Activity._t": "NtlmEvent" },{$unset: {"Activity.ResourceIdentifier": ""}}, {multi: true});`

## <a name="minor-changes"></a>Drobne zmiany

- Usługa ATA używa teraz usługi OWIN zamiast usług IIS dla konsoli ATA.
- Centrum usługi ATA jest wyłączony, nie można uzyskać dostępu do konsoli usługi ATA.
- Krótkoterminowe dzierżawy podsieci nie są już konieczne z powodu zmian w aparacie rozpoznawania nazw sieciowych (NNR) usługi ATA.

## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.7 — przewodnik migracji](ata-update-1.7-migration-guide.md)

