---
title: "Zarządzanie bazą danych usługi ATA | Microsoft ATA"
description: "Procedury ułatwiające przenoszenie, tworzenie kopii zapasowej lub przywracanie bazy danych usługi ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 115ec28877665c79e5cbcd557528da156c8d7149
ms.openlocfilehash: fd00623f9be396b3a2c384cce436996b5093cc3f


---

# Zarządzanie bazą danych usługi ATA
Jeśli musisz przenieść bazę danych ATA, utworzyć jej kopię zapasową lub przywrócić ją, należy użyć poniższych procedur do pracy z MongoDB.

## Tworzenie kopii zapasowej bazy danych usługi ATA
Zapoznaj się z [odpowiednią dokumentacją usługi MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## Przywracanie bazy danych usługi ATA
Zapoznaj się z [odpowiednią dokumentacją usługi MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## Przenoszenie bazy danych usługi ATA na inny dysk

1.  Zatrzymaj usługę **Microsoft Advanced Threat Analytics Center**.

2.  Zatrzymaj usługę **MongoDB**.

3.  Otwórz plik konfiguracji Mongo znajdujący się domyślnie w lokalizacji C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Znajdowanie parametru `storage: dbPath`

4.  Przenieś folder wymienione w parametrze `dbPath` do nowej lokalizacji.

5.  Zmień parametr `dbPath` w pliku konfiguracji mongo pliku na nową ścieżkę folderu, a następnie zapisz i zamknij plik.

    ![Modyfikowanie obrazu konfiguracji usługi MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Uruchom usługę **MongoDB**.

7.  Otwórz wiersz polecenia i uruchom powłokę Mongo, uruchamiając plik `mongo.exe ATA`.

    Domyślna lokalizacja pliku mongo.exe to C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin

8.  Uruchom następujące polecenie: `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}})`

   Zamiast <New DB Location>, gdzie `&lt;New DB Location&gt;` jest nową ścieżką folderu.

9.  Zaktualizuj klucz HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath do nowej ścieżki folderu.

9. Uruchom usługę **Microsoft Advanced Threat Analytics Center**.

## Zobacz też
- [Architektura usługi ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jul16_HO3-->


