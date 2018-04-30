---
title: Skonfiguruj SAM-R, aby włączyć wykrywanie ścieżki penetracja sieci w Azure ATP | Dokumentacja firmy Microsoft
description: Opisuje sposób konfigurowania SAM-R, aby włączyć wykrywanie ścieżki penetracja sieci w Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 24b42c5425933d8931a85e0ba454a69e0ca94a21
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/30/2018
---
*Dotyczy: Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-8"></a>Zainstaluj ATP Azure - kroku 8

>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Krok 8. Skonfiguruj SAM-R wymagane uprawnienia

[Ścieżki penetracja sieci](use-case-lateral-movement-path.md) wykrywania opiera się na zapytania, które identyfikują Administratorzy lokalni na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, za pomocą konta usługi Azure ATP utworzonego w [krok 2. Łączenie z usługą AD](install-atp-step2.md).
 
Zapewnienie systemu Windows klienci i serwery Zezwalaj na konto Azure ATP do wykonania tej operacji SAM-R, modyfikacja **zasad grupy** należy dodać konto usługi Azure ATP oprócz kontom naliście **Dostęp sieciowy** zasad.

1. Znajdź zasad:

 - Nazwa zasad: Dostęp do sieci — Ogranicz dozwolone do zdalnego łączenia się SAM klientów
 - Lokalizacja: Konfiguracja komputera, ustawienia systemu Windows, ustawienia zabezpieczeń, zasady lokalne, opcje zabezpieczeń
  
  ![Zlokalizuj zasad](./media/samr-policy-location.png)

2. Dodaj usługę Azure ATP do listy zatwierdzonych kont stanie do wykonania tej akcji nowoczesnych systemach Windows.
 
  ![Dodaj usługę](./media/samr-add-service.png)

3. **Usługi AATP** (usługa Azure ATP utworzony podczas instalacji) teraz ma odpowiednie uprawnienia do wykonania SAMR w środowisku.

Aby uzyskać więcej informacji na SAM-R i zasad grupy, zobacz [dostępu do sieci: ograniczanie klientach dozwolone do zdalnego łączenia się SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)



## <a name="see-also"></a>Zobacz też
- [Badanie ataków ścieżki penetracja sieci z Azure ATP](use-case-lateral-movement-path.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)