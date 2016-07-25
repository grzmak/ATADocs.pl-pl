---
title: "Praca z ustawieniami wykrywania usługi ATA | Microsoft ATA"
description: "Opis sposobu konfigurowania listy nietypowych adresów IP i podsieci, które powinny być obsługiwane inaczej niż pozostałe jednostki w sieci."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 3575bb9489cae181f7902be23c680830203fafe7


---

# Praca z ustawieniami wykrywania usługi ATA
Strona konfiguracji **Wykrywanie** umożliwia określenie listy nietypowych adresów IP i podsieci, które powinny być obsługiwane inaczej niż pozostałe jednostki w sieci.

## Konfigurowanie wykrywania
Na stronie **Wykrywanie** można określić następujące elementy:

-   **Podsieci dzierżawy krótkoterminowej** — jeśli organizacja ma podsieci, w których adresy IP są przydzielane na bardzo krótki okres, na przykład podsieci adresów IP VPN lub podsieci Wi-Fi, ważne jest, aby wprowadzić te adresy IP i podsieci do usługi ATA, aby poinformować usługę ATA, że skojarzenia komputerów i adresów IP z tych zakresów powinny być przechowywane krócej niż w przypadku innych adresów IP.

-   **Identyfikatory SID kont wystawionych jako przynęta** — to jest konto użytkownika, dla którego nie powinny istnieć żadne działania w sieci. To konto zostanie skonfigurowane jako użytkownik usługi ATA wystawiony jako przynęta. Jeśli ktoś spróbuje użyć tego konta użytkownika usługi ATA, spowoduje podejrzane działanie, które będzie wskazywać na złośliwe działania. Do skonfigurowania użytkownika wystawionego jako przynęta potrzebny jest identyfikator SID konta użytkownika, a nie nazwa użytkownika.

Można wykluczyć adresy IP z następujących wykryć. W przypadku wprowadzenia adresu IP na jedną z tych list usługa ATA wykluczy ten adres IP z określonego typu wykrywanych działań.

-   Wykluczenia adresów IP rekonesansu DNS

-   Wykluczenia adresów IP ataków typu Pass-the-Ticket

## Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-configuration.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


