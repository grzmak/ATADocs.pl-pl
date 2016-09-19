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
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 579e49a8dd9a5cc67961af14259bb8bb27130de5


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

 > [!IMPORTANT]
 Automatyczne odnawianie certyfikatów używanych przez usługę ATA nie jest obsługiwane. Użycie tych certyfikatów może spowodować, że usługa ATA przestanie działać w przypadku automatycznego odnowienia certyfikatu. 


## Zobacz też
[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.7 — przewodnik migracji](ata-update-1.7-migration-guide.md)




<!--HONumber=Aug16_HO5-->


