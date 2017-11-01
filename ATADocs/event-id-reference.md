---
title: "Odwołanie do Identyfikatora zdarzeń usługi ATA | Dokumentacja firmy Microsoft"
description: "Zawiera listę zdarzeń usługi ATA identyfikatorów i ich opisy."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/25/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 7bd0f90acbb6a2d8eb84fd09bc4d859fff082273
ms.sourcegitcommit: 5563c6861bb5db5cb73e058e5a51b4938b9a7d46
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# <a name="ata-event-id-reference"></a>Odwołanie do Identyfikatora zdarzeń usługi ATA

Podgląd zdarzeń Centrum usługi ATA w dziennikach zdarzeń usługi ATA. Ten artykuł zawiera listę identyfikatorów zdarzeń i zawiera opis każdego z nich.

Zdarzenia można znaleźć tutaj:

![Lokalizacja identyfikator zdarzenia](./media/event-id-location.png)

## <a name="ata-health-events"></a>Zdarzenia kondycji usługi ATA

1001 — dane z bazy danych Centrum usługi ATA dysk alertu health wolnego miejsca 

1003 — Centrum usługi ATA przeciążony alertu health 

1004 — alert dotyczący kondycji wygaśnięcia certyfikatu 

1005 — baza danych Centrum rozłączona alertu health 

1006 — brama usługi ATA katalogu usług klienta konto hasła wygaśnięcia alert dotyczący kondycji 

1007 — alert kondycji nieprzypisany Synchronizatora domeny bramy usługi ATA 

1008 — brama usługi ATA przechwytywania sieci karty błędnej kondycja alertu 

1009 — Brak alertu health sieci karty przechwytywania bramy usługi ATA 

1010 — alert dotyczący bramy usługi ATA katalogu usług klienta łączności kondycji 

1011 — brama usługi ATA odłączona alertu health 

1012 — brama usługi ATA przeciążony alertu health działania zdarzenia 

1013 — alert dotyczący kondycji działania sieci przeciążona bramy usługi ATA 

1014 — alert dotyczący kondycji poczty center 

1015 — alertu health Syslog center 

1016 — alert dotyczący kondycji nieaktualne bram usługi ATA 

1017 — Centrum nie odbiera ruch alertu health 

1018 — alert o niepowodzeniu kondycji uruchomić bramy usługi ATA 

1019 — alert dotyczący bramy usługi ATA Brak pamięci kondycji 

1020 — alertu health odbiornika zdarzeń RADIUS bramy usługi ATA 

1021 — alertu health odbiornika zdarzeń Syslog bramy usługi ATA 

1022 — Centrum usługi ATA zewnętrznego adresu IP adres rozpoznawania kondycji alert o niepowodzeniu 
 
## <a name="ata-suspicious-ctivity-events"></a>Usługa ATA ctivity podejrzane zdarzenia

2001 – podejrzane działania nietypowe zachowanie 

2002 — protokół nietypowe podejrzanego działania 

2003 — konto wyliczenie podejrzanego działania 

2004 — LDAP ukierunkowany wymusić podejrzanego działania 

2005 — wstępnego uwierzytelniania komputera podejrzane działanie nie powiodło się 

2006 — directory usługi replikacji podejrzanego działania 

2007 — podejrzane działania Rekonesans DNS 

2008 — szyfrowanie obniżenia poziomu podejrzanego działania 

2012 — Wyliczanie sesji podejrzanego działania 

2013 — forged PAC podejrzanych działań. 

2014 — wystawionego jako przynęta działania podejrzanego działania 

2015 — podejrzane działania hasło jako zwykły tekst LDAP 

2016 — dużego obiektu usunięcia podejrzanego działania 

2017 — przebieg skrótu podejrzanego działania 

2018 — dostęp próbny biletu podejrzanego działania 

2019 — zdalne wykonywanie kodu podejrzanego działania 

2020 — pobieranie danych kopii zapasowej klucza podejrzanych działań ochrony 

2021 — SAMR Rekonesans podejrzanego działania 

2022 — golden ticket podejrzanego działania 

2023 — nietypowe grupy poufnej członkostwa zmiany podejrzanego działania 

2023 — siłowych podejrzanego działania 

## <a name="ata-auditing-events"></a>Zdarzenia inspekcji usługi ATA

3001 — Zmień konfigurację usługi ATA 

3002 — bramy usługi ATA dodano

3003 — bramy usługi ATA usunięte

3004 - licencja ATA aktywowany

3005 — Zaloguj się do konsoli usługi ATA

3006 — ręczne zmiana stanu działania kondycji 

3007 — ręczne zmiana stanu podejrzanego działania 


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
