---
title: "Co nowego w wersji 1.7 usługi ATA | Microsoft ATA"
description: "Lista nowości oraz znanych problemów w wersji 1.7 usługi ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae6a3295d2fffabdb8e5f713674379e4af499ac2
ms.openlocfilehash: af9101260b1a0d5d9da32398f638f76e0c8c40a7


---

# Co nowego w wersji 1.7 usługi ATA
Te informacje o wersji zawierają znane problemy w tej wersji usługi Advanced Threat Analytics.

## Co nowego w aktualizacji usługi ATA do wersji 1.7?
Aktualizacja usługi ATA do wersji 1.7 zapewnia następujące ulepszenia:

-   Nowe i zaktualizowane funkcje wykrywania

-   Kontrola dostępu oparta na rolach

-   Obsługa systemu Windows Server 2016 i Windows Server Core

-   Ulepszenia środowiska użytkownika


### Nowe i zaktualizowane funkcje wykrywania


- **Rekonesans przy użyciu wyliczania usług katalogowych** W ramach fazy rekonesansu osoby atakujące zbierają informacje dotyczące jednostek w sieci przy użyciu różnych metod. Wyliczanie usług katalogowych przy użyciu protokołu SAM-R pozwala osobom atakującym uzyskać listę użytkowników i grup w domenie oraz zrozumieć interakcję między różnymi jednostkami. 

- **Ulepszenia wykrywania ataków „pass the hash”** W celu zwiększenia wykrywania ataków „pass the hash” dodaliśmy dodatkowe modele zachowań dla wzorców uwierzytelniania jednostek. Modele te pozwalają usłudze ATA korelować zachowania jednostki z podejrzanymi uwierzytelnieniami NTLM i odróżniać prawdziwe ataki „pass the hash” od innych, podobnych scenariuszy.

- **Ulepszenia wykrywania ataków „pass the ticket”** Pomyślnie wykrywanie zaawansowanych ataków, a w szczególności ataków „pass the ticket”, wymaga dokładnej korelacji między adresem IP a kontem komputera. Jest to wyzwaniem w środowiskach, gdzie adresy IP z założenia szybko się zmieniają (na przykład w sieciach Wi-Fi i przy wielu maszynach wirtualnych korzystających z tego samego hosta). Aby stawić czoła temu wyzwaniu i zwiększyć dokładność wykrywania ataków „pass the ticket”, aparat rozpoznawania nazw sieciowych (NNR) usługi ATA został znacznie poprawiony w celu zmniejszenia ilości fałszywych alarmów.

- **Ulepszenia wykrywania nietypowych zachowań** W usłudze ATA 1.7 dane uwierzytelniania NTLM zostały dodane jako źródła danych służące do wykrywania nietypowych zachowań, umożliwiając działanie algorytmów o szerszym zakresie rozpoznawania zachowania jednostek w sieci. 

- **Ulepszenia wykrywania nietypowych implementacji protokołów** Usługa ATA wykrywa teraz nietypowe implementacje protokołów w protokole Kerberos oraz dodatkowe nieprawidłowości w protokole NTLM. W szczególności te nowe anomalie dotyczące protokołu Kerberos są często używane podczas ataków „pass the hash”.


### Infrastruktura

- **Kontrola dostępu na podstawie roli** Obsługa kontroli dostępu opartej na rolach (RBAC). Usługa ATA 1.7 zawiera trzy role: administrator ATA, analityk ATA i wykonawca ATA.

- **Obsługa systemu Windows Server 2016 i Windows Server Core** Usługa ATA 1.7 obsługuje wdrażanie bram Lightweight Gateway na kontrolerach domeny z systemem Server Core dla systemu Windows Server 2012 i Server Core dla systemu Windows Server 2012 R2. Ponadto ta wersja obsługuje system Windows Server 2016 w przypadku obu składników: centrum usługi ATA i bramy usługi ATA.

### Czynności po stronie użytkownika
- **Środowisko konfiguracji** Środowisko konfiguracji usługi ATA zostało w tej wersji przeprojektowane dla wygody użytkowników i w celu lepszej obsługi środowisk z wieloma bramami ATA. W tej wersji wprowadzono także stronę aktualizacji bramy ATA w celu prostszego, lepszego zarządzania automatycznymi aktualizacjami różnych bram.

## Znane problemy
W tej wersji występują następujące znane problemy.

### Automatyczna aktualizacja bramy może zakończyć się niepowodzeniem
**Objawy:** W środowiskach z wolnymi łączami sieci WAN aktualizacja bramy ATA może osiągnąć limit czasu aktualizacji (100 sekund) i zakończyć się niepowodzeniem.
W konsoli usługi ATA brama ATA będzie mieć stan „Aktualizowanie (pobieranie pakietu)” przez długi czas i ostatecznie zakończy się niepomyślnie.

**Obejście:** Aby obejść ten problem, pobierz najnowszy pakiet bramy ATA z konsoli ATA i ręcznie zaktualizuj bramę ATA.

### Błąd migracji podczas aktualizowania usługi ATA z wersji 1.6
Podczas aktualizowania usługi ATA do wersji 1.7 proces aktualizacji może zakończyć się niepowodzeniem z powodu błędu o kodzie *0x80070643*:

![Update ATA to 1.7 error (Błąd aktualizacji usługi ATA do wersji 1.7)](media/ata-update-error.png)

Przejrzyj dziennik wdrażania, aby znaleźć przyczynę błędu. Dziennik wdrażania znajduje się w lokalizacji **%temp%\..\Microsoft Advanced Thread Analytics Center_{znacznik_daty}_MsiPackage.log**. 

W tabeli poniżej wymieniono błędy do wyszukania oraz odpowiednie skrypty Mongo do usunięcia błędu. Zobacz przykład pod tabelą, aby zobaczyć, jak uruchomić skrypt Mongo:

| Błąd w pliku dziennika wdrażania                                                                                                                  | Skrypt Mongo                                                                                                                                                                         |
|---|---|
| System.FormatException: Size {size},is larger than MaxDocumentSize 16777216 (System.FormatException: Rozmiar {size} jest większy niż wartość MaxDocumentSize 16777216) <br>W dalszej części pliku:<br>  Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateUniqueEntityProfiles(Boolean isPartial)                                                                                        | db.UniqueEntityProfile.find().forEach(function(obj){if(Object.bsonsize(obj) > 12582912) {print(obj._id);print(Object.bsonsize(obj));db.UniqueEntityProfile.remove({_id:obj._id});}}) |
| System.OutOfMemoryException: Exception of type 'System.OutOfMemoryException' was thrown (System.OutOfMemoryException: Został zgłoszony wyjątek typu „System.OutOfMemoryException”)<br>W dalszej części pliku:<br>Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.ReduceSuspiciousActivityDetailsRecords (suspiciousActivityCollection IMongoCollection "1, Int32 deletedDetailRecordMaxCount) | db.SuspiciousActivity.find().forEach(function(obj){if(Object.bsonsize(obj) > 500000),{print(obj._id);print(Object.bsonsize(obj));db.SuspiciousActivity.remove({_id:obj._id});}})     |
|System.Security.Cryptography.CryptographicException: Bad Length (System.Security.Cryptography.CryptographicException: Nieprawidłowa długość)<br>W dalszej części pliku:<br> Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateCenterSystemProfile(IMongoCollection`1 systemProfileCollection)| CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;db.SystemProfile.update({_t:"CenterSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}})|


Aby uruchomić odpowiedni skrypt, wykonaj następujące kroki. 

1.  Z wiersza polecenia z podwyższonym poziomem uprawnień przejdź do następującej lokalizacji: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**
2.  Wpisz polecenie – **Mongo.exe ATA**   (*Uwaga*: ATA musi być napisane wielkimi literami).
3.  Z powyższej tabeli wklej skrypt, który odpowiada błędowi w dzienniku wdrażania.

![Skrypt Mongo usługi ATA](media/ATA-mongoDB-script.png)

Teraz powinno być możliwe ponowne uruchomienie uaktualniania.

### Usługa ATA zgłasza dużą liczbę podejrzanych działań “*Reconnaissance using directory services enumerations*” (Rekonesans przy użyciu wyliczeń usług katalogowych):
 
Dzieje się tak najczęściej wtedy, gdy narzędzie do skanowania sieci jest uruchomione na wszystkich (lub na wielu) maszynach klienckich w organizacji. Jeśli widzisz ten problem:

1. W przypadku zidentyfikowania przyczyny lub konkretnej aplikacji działającej na maszynach klienckich, wyślij wiadomość e-mail na adres ATAEval at Microsoft.com.
2. Użyj następującego skryptu mongo, aby odrzucić wszystkie te zdarzenia (zobacz wyżej, jak uruchomić skrypt mongo):

db.SuspiciousActivity.update({_t: "SamrReconnaissanceSuspiciousActivity"}, {$set: {Status: "Dismissed"}}, {multi: true})

### Usługa ATA wysyła powiadomienia dotyczące odrzuconych podejrzanych działań:
Jeśli powiadomienia zostały skonfigurowane, usługa ATA może nadal wysyłać powiadomienia (przez pocztę e-mail, usługę Syslog i dzienniki zdarzeń) dla odrzuconych podejrzanych działań.
Nie ma obecnie sposobu obejścia tego problemu. 

### Rejestracja bramy usługi ATA w centrum usługi ATA może się nie powieść, jeśli protokoły TLS 1.0 i TLS 1.1 są wyłączone:
Jeśli protokoły TLS 1.0 i TLS 1.1 są wyłączone na bramie usługi ATA (lub bramie ATA Lightweight Gateway), brama może nie być w stanie zarejestrować się w centrum usługi ATA.

### Automatyczne odnawianie certyfikatów używanych przez usługę ATA nie jest obsługiwane
Korzystanie z automatycznego odnawiania certyfikatów może spowodować, że usługa ATA przestanie działać po automatycznym odnowieniu certyfikatu. 


## Zobacz też
[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.7 — przewodnik migracji](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO2-->


