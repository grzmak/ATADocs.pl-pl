---
title: "Rozwiązywanie problemów z usługą Advanced Threat Analytics przy użyciu bazy danych | Dokumentacja firmy Microsoft"
description: "Opis sposobu rozwiązywania problemów przy użyciu bazy danych usługi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 174918812562b9bfe892fcde90d92e208b26ffc3
ms.sourcegitcommit: 42ce07e3207da10e8dd7585af0e34b51983c4998
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/25/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="troubleshooting-ata-using-the-ata-database"></a>Rozwiązywanie problemów z usługą ATA przy użyciu bazy danych usługi ATA
Usługa ATA używa produktu MongoDB jako swojej bazy danych.
W celu wykonywania zaawansowanych zadań i rozwiązywania problemów możesz użyć domyślnego wiersza polecenia lub narzędzia interfejsu użytkownika bazy danych.

## <a name="interacting-with-the-database"></a>Interakcja z bazą danych
Domyślną i najbardziej podstawową metodą wysyłania zapytań do bazy danych jest użycie powłoki Mongo:

1.  Otwórz okno wiersza polecenia i zmień ścieżkę na folder bin bazy danych MongoDB. Domyślna ścieżka to: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Uruchom polecenie `mongo.exe ATA`. Upewnij się, że ciąg „ATA” jest wpisany tylko wielkimi literami.

> [!div class="mx-tableFixed"]
|Zadanie|Składnia|Uwagi|
|-------------|----------|---------|
|Sprawdzanie kolekcji w bazie danych.|`show collections`|Użyteczne jako kompletny test umożliwiający sprawdzenie, czy ruch sieciowy jest zapisywany w bazie danych oraz czy zdarzenie 4776 jest odbierane przez usługę ATA.|
|Pobieranie szczegółów użytkownika/komputera/grupy (UniqueEntity), takich jak identyfikator użytkownika.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Znajdowanie ruchu sieciowego uwierzytelniania Kerberos pochodzącego z określonego komputera w określonym dniu.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Aby uzyskać wartość &lt;ID of the source computer&gt; (identyfikator komputera źródłowego), można wykonać zapytanie względem kolekcji UniqueEntity, jak pokazano w przykładzie.<br /><br />Każdy typ działania w sieci, na przykład uwierzytelnienia Kerberos, ma swoją własną kolekcję dla daty UTC.|
|Znajdowanie ruchu NTLM pochodzącego z określonego komputera i związanego z określonym kontem w określonym dniu.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Aby uzyskać wartość &lt;ID of the source computer&gt; (identyfikator komputera źródłowego) i &lt;ID of the account&gt; (identyfikator konta), można wykonać zapytanie względem kolekcji UniqueEntity, jak pokazano w przykładzie.<br /><br />Każdy typ działania w sieci, na przykład uwierzytelnienia NTLM, ma swoją własną kolekcję dla daty UTC.|
|Wyszukiwanie zaawansowanych właściwości, takich jak daty aktywności konta. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Aby uzyskać wartość &lt;ID of the account&gt; (identyfikator konta), można wykonać zapytanie względem kolekcji UniqueEntity, jak pokazano w przykładzie.<br>Nazwa właściwości zawierającej daty aktywności konta to „ActiveDates”. Na przykład konieczne może być ustalenie, czy konto było aktywne przez co najmniej 21 dni, aby można było uruchomić dla tego konta algorytm uczenia maszynowego umożliwiający rozpoznawanie nietypowego zachowania.|
|Wprowadzanie zaawansowanych zmian konfiguracji. W tym przykładzie rozmiar kolejki wysyłania dla wszystkich bram usługi ATA jest zmieniany na 10 000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

W poniższym przykładzie przedstawiono przykładowy kod, w którym użyto powyższej składni. Jeśli badane są podejrzane działania z dnia 2015-10-20 i chcesz dowiedzieć się więcej o działaniach związanych z protokołem NTLM podejmowanych przez użytkownika „John Doe” w tym dniu:<br /><br />Po pierwsze znajdź identyfikator użytkownika „John Doe”.

`db.UniqueEntity.find({Name: "John Doe"})`<br>Zanotuj jego identyfikator określony przez wartość `_id`. W naszym przykładzie załóżmy, że identyfikator to `123bdd24-b269-h6e1-9c72-7737as875351`.<br>Następnie wyszukaj kolekcję z najbliższą datą poprzedzającą poszukiwaną datę (2015-10-20 w naszym przykładzie).<br>Następnie wyszukaj działania związane z protokołem NTLM konta użytkownika John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
