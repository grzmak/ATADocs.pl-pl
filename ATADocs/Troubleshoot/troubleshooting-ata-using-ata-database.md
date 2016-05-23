---
# required metadata

title: Rozwiązywanie problemów z usługą ATA przy użyciu bazy danych usługi ATA | Microsoft Advanced Threat Analytics
description: Opis sposobu rozwiązywania problemów przy użyciu bazy danych usługi ATA 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rozwiązywanie problemów z usługą ATA przy użyciu bazy danych usługi ATA
Usługa ATA używa produktu MongoDB jako swojej bazy danych.
W celu wykonywania zaawansowanych zadań i rozwiązywania problemów możesz użyć domyślnego wiersza polecenia lub narzędzia interfejsu użytkownika bazy danych.

## Interakcja z bazą danych
Domyślną i najbardziej podstawową metodą wysyłania zapytań do bazy danych jest użycie powłoki Mongo:

1.  Otwórz okno wiersza polecenia i zmień ścieżkę na folder bin bazy danych MongoDB. Domyślna ścieżka to **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**..

2.  Uruchom polecenie `mongo.exe ATA`. Upewnij się, że ciąg „ATA” jest wpisany tylko wielkimi literami.

|Zadanie|Składnia|Uwagi|
|-------------|----------|---------|
|Sprawdzanie kolekcji w bazie danych.|`show collections`|Użyteczne jako kompletny test umożliwiający sprawdzenie, czy ruch sieciowy jest zapisywany w bazie danych oraz czy zdarzenie 4776 jest odbierane przez usługę ATA.|
|Pobieranie szczegółów użytkownika/komputera/grupy (UniqueEntity), takich jak identyfikator użytkownika.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Znajdowanie ruchu sieciowego uwierzytelniania Kerberos pochodzącego z określonego komputera w określonym dniu.|`db.KerberosAs_<date>.find({SourceComputerId: "<Id of the source computer>"})`|Aby uzyskać wartość &lt;ID of the source computer&gt; (identyfikator komputera źródłowego), można wykonać zapytanie względem kolekcji UniqueEntity, jak pokazano w przykładzie.<br /><br />Każdy typ działania w sieci, na przykład uwierzytelnienia Kerberos, ma swoją własną kolekcję dla daty UTC.|
|Znajdowanie ruchu NTLM pochodzącego z określonego komputera i związanego z określonym kontem w określonym dniu.|`db.Ntlm_<date>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Aby uzyskać wartość &lt;ID of the source computer&gt; (identyfikator komputera źródłowego) i &lt;ID of the account&gt; (identyfikator konta), można wykonać zapytanie względem kolekcji UniqueEntity, jak pokazano w przykładzie.<br /><br />Każdy typ działania w sieci, na przykład uwierzytelnienia NTLM, ma swoją własną kolekcję dla daty UTC.|
|Wyszukiwanie zaawansowanych właściwości, takich jak daty aktywności konta. |`db.Profile.find({UniqueEntityId: "<Id of the account>")`|Aby uzyskać wartość &lt;ID of the account&gt; (identyfikator konta), można wykonać zapytanie względem kolekcji UniqueEntity, jak pokazano w przykładzie.<br>Nazwa właściwości zawierającej daty aktywności konta to „ActiveDates”. <br>
Na przykład konieczne może być ustalenie, czy konto było aktywne przez co najmniej 21 dni, aby można było uruchomić dla tego konta algorytm uczenia maszynowego umożliwiający rozpoznawanie nietypowego zachowania.|
|Wprowadzanie zaawansowanych zmian konfiguracji. W tym przykładzie rozmiar kolejki wysyłania dla wszystkich bram usługi ATA jest zmieniany na 10 000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

W poniższym przykładzie przedstawiono przykładowy kod, w którym użyto powyższej składni. Jeśli badane są podejrzane działania z dnia 2015-10-20 i chcesz dowiedzieć się więcej o działaniach związanych z protokołem NTLM podejmowanych przez użytkownika „John Doe” w tym dniu:<br /><br />Po pierwsze znajdź identyfikator użytkownika „John Doe”.

`db.UniqueEntity.find({Name: "John Doe"})`<br>Zanotuj jego identyfikator określony przez wartość „`_id`”. W naszym przykładzie załóżmy, że identyfikator to „`123bdd24-b269-h6e1-9c72-7737as875351`"<br>Następnie wyszukaj kolekcję z najbliższą datą poprzedzającą poszukiwaną datę (2015-10-20 w naszym przykładzie).<br>Następnie wyszukaj działania związane z protokołem NTLM konta użytkownika John Doe:


    `db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})
## Plik konfiguracji usługi ATA
Konfiguracja usługi ATA jest przechowywana w kolekcji „SystemProfile” w bazie danych.
Kopia zapasowa tej kolekcji jest tworzona co godzinę przez centrum usługi ATA w pliku o nazwie „SystemProfile.json”. Znajduje się on w podfolderze o nazwie „Backup”. W domyślnej lokalizacji instalacji usługi ATA położenie tego pliku to **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json**.. 

**Uwaga**: zalecane jest wykonanie kopii zapasowej tego pliku w innej lokalizacji w przypadku wprowadzania istotnych zmian w usłudze ATA.

Możesz przywrócić wszystkie ustawienia, uruchamiając następujące polecenie:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`


<!--HONumber=Apr16_HO4-->


