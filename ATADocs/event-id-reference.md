---
title: Odniesienie identyfikator zdarzenia usługi ATA | Dokumentacja firmy Microsoft
description: Zawiera listę zdarzeń usługi ATA identyfikatorów i ich opisy.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0c37024719a9037cb0522ba40115714a35a399b2
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166446"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*


# <a name="ata-event-id-reference"></a>Odniesienie identyfikator zdarzenia usługi ATA

Podgląd zdarzeń Centrum usługi ATA rejestruje zdarzenia usługi ATA. Ten artykuł zawiera listę identyfikatorów zdarzeń i zawiera opis każdego z nich.

Zdarzenia można znaleźć tutaj:

![Lokalizacja identyfikator zdarzenia](./media/event-id-location.png)

## <a name="ata-health-events"></a>Zdarzenia dotyczące kondycji usługi ATA

1001 — Centrum usługi ATA bazy danych dysku alertów dotyczących kondycji wolnego miejsca 

1003 — Centrum usługi ATA przeciążone alertów dotyczących kondycji 

1004 — alert dotyczący kondycji wygaśnięcia certyfikatu 

1005 — baza danych Centrum Rozłączono alertów dotyczących kondycji 

1006 — brama usługi ATA katalogu usług klienta konta hasła ważności alertu dotyczącego kondycji 

1007 — brama usługi ATA alertów dotyczących kondycji nie przypisano Synchronizatora domeny 

1008 — brama usługi ATA Przechwytywanie sieci karty uszkodzoną kondycji alertu 

1009 — brama usługi ATA Przechwytywanie sieci karty Brak alertów dotyczących kondycji 

1010 — alert kondycji łączności klienta bramy usługi ATA katalogu usług 

1011 — brama usługi ATA Rozłączono alertów dotyczących kondycji 

1012 — brama usługi ATA przeciążone alertu kondycji działania zdarzenia 

1013 — brama usługi ATA przeciążone alertów dotyczących kondycji działania sieci 

1014 — Centrum wiadomości e-mail alertów dotyczących kondycji 

1015 — Centrum alertów dotyczących kondycji usługi Syslog 

1016 — alert dotyczący kondycji nieaktualne bram usługi ATA 

1017 — Centrum nie odbierają ruchu alertów dotyczących kondycji 

1018 — brama usługi ATA Niepowodzenie uruchamiania alertów dotyczących kondycji 

1019 — alert o kondycji bramy usługi ATA małej ilości pamięci 

1020 — alert o kondycji odbiornika usługi RADIUS z bramy usługi ATA zdarzenie 

1021 — alert o kondycji odbiornika Syslog do bramy usługi ATA zdarzenie 

1022 — Centrum usługi ATA zewnętrznego adresu IP adres rozpoznawania błędu alertów dotyczących kondycji 
 
## <a name="ata-suspicious-activity-events"></a>Zdarzenia podejrzanych działań usługi ATA

2001 – podejrzane działanie nietypowe zachowanie 

2002 – podejrzane działanie nietypowy protokół 

2003 – podejrzane działanie wyliczenia kont 

2004 — LDAP atak wymusić podejrzanego działania 

2006 — katalog usług replikacji podejrzanego działania 

2007 — podejrzanych działań rekonesansu DNS 

2008 — podejrzane działanie obniżenia poziomu szyfrowania 

2012 — Wyliczanie sesji podejrzanego działania 

2013 — podejrzane działanie sfałszowany element PAC 

2014 — wystawione jako przynęta działanie podejrzanego działania 

2016 — dużej liczby obiektów usunięciu podejrzanej aktywności 

2017 — przebiegu skrótu podejrzanego działania 

2018 — przekazać bilet podejrzanego działania 

2019 — podejrzane działanie zdalne wykonywanie kodu 

2020 — pobieranie danych kopii zapasowej klucza podejrzanych działań ochrony 

2021 — podejrzanych działań rekonesansu SAMR 

2022 — biletu uwierzytelniania Golden Ticket podejrzanego działania 

2023 — atak siłowy podejrzanego działania 

2024 - podejrzane działania zmiany członkostwa nietypowe wrażliwych grup  

## <a name="ata-auditing-events"></a>Zdarzenia inspekcji usługi ATA

3001 — Zmienianie konfiguracji usługi ATA 

3002 — bramy usługi ATA dodano

3003 — bramy usługi ATA usunięto

3004 - licencja ATA aktywowany

3005 — Zaloguj się do konsoli usługi ATA

3006 — ręczne zmiany kondycji stanu działania 

3007 — ręczne zmiany stan podejrzanego działania 


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
