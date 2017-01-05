---
title: "Praca z ustawieniami wykrywania usługi ATA | Dokumentacja firmy Microsoft"
description: "Opis sposobu konfigurowania listy nietypowych adresów IP i podsieci, które powinny być obsługiwane inaczej niż pozostałe jednostki w sieci."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 93f2a72c9623674c73b3ee83ecf12be8e0766365


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="working-with-ata-detection-settings"></a>Praca z ustawieniami wykrywania usługi ATA
Strona konfiguracji **Wykrywanie** umożliwia określenie listy nietypowych adresów IP i podsieci, które powinny być obsługiwane inaczej niż pozostałe jednostki w sieci.

## <a name="setting-up-detection"></a>Konfigurowanie wykrywania
W sekcji **Wykrywanie** można określić następujące elementy:

-   **Identyfikatory SID kont wystawionych jako przynęta** — to jest konto użytkownika, dla którego nie powinny istnieć żadne działania w sieci. To konto zostanie skonfigurowane jako użytkownik usługi ATA wystawiony jako przynęta. Jeśli ktoś spróbuje użyć tego konta użytkownika usługi ATA, spowoduje podejrzane działanie, które będzie wskazywać na złośliwe działania. Do skonfigurowania użytkownika wystawionego jako przynęta potrzebny jest identyfikator SID konta użytkownika, a nie nazwa użytkownika.

>[!NOTE]
> Identyfikator SID użytkownika można znaleźć na karcie *Informacje o koncie* profilu użytkownika w konsoli ATA.


![Wystawianie konta jako przynęty w ustawieniach wykrywania usługi ATA](media/ata-detection-settings-honeytoken-1.7.png)


**Detection Exclusions** (Wykluczenia wykrywania) — można wykluczyć adresy IP z zakresu wykrywania następujących zagrożeń. W przypadku wprowadzenia adresu IP na jedną z tych list usługa ATA wykluczy ten adres IP z określonego typu wykrywanych działań.

-   Wykluczenia adresów IP rekonesansu DNS

-   Wykluczenia adresów IP ataków typu Pass-the-Ticket

![Wykluczenia w ustawieniach wykrywania usługi ATA](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-configuration.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


