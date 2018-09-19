---
title: Zarządzanie bazą danych usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Procedury ułatwiające przenoszenie, tworzenie kopii zapasowej lub przywracanie bazy danych usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1374b57a4633c45bce2d4ab88952197a7b8f168a
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134028"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="ata-database-management"></a>Zarządzanie bazą danych usługi ATA
Jeśli musisz przenieść bazę danych ATA, utworzyć jej kopię zapasową lub przywrócić ją, należy użyć poniższych procedur do pracy z MongoDB.

## <a name="backing-up-the-ata-database"></a>Tworzenie kopii zapasowej bazy danych usługi ATA
Zapoznaj się z [odpowiednią dokumentacją usługi MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Przywracanie bazy danych usługi ATA
Zapoznaj się z [odpowiednią dokumentacją usługi MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Przenoszenie bazy danych usługi ATA na inny dysk

1.  Zatrzymaj usługę **Microsoft Advanced Threat Analytics Center**.
> [!Important] 
> Przed przejściem do następnego kroku upewnij się, że centrum usługi ATA zostało zatrzymane.

2.  Zatrzymaj usługę **MongoDB**.

3.  Otwórz plik konfiguracji Mongo znajdujący się domyślnie w lokalizacji C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Znajdź parametr `storage: dbPath`

4.  Przenieś folder wymienione w parametrze `dbPath` do nowej lokalizacji.

5.  Zmień parametr `dbPath` w pliku konfiguracji mongo pliku na nową ścieżkę folderu, a następnie zapisz i zamknij plik.

    ![Modyfikowanie obrazu konfiguracji usługi MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Uruchom usługę **MongoDB**.

7. Uruchom usługę **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Zobacz też
- [Architektura usługi ATA](ata-architecture.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

