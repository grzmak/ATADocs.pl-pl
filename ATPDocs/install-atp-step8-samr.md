---
title: "Skonfiguruj SAM-R, aby włączyć wykrywanie ścieżki penetracja sieci w Azure ATP | Dokumentacja firmy Microsoft"
description: "Opisuje sposób konfigurowania SAM-R, aby włączyć wykrywanie ścieżki penetracja sieci w Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0e2ac4fb68fb1429610a0416582c871c9ae704df
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-8"></a>Zainstaluj ATP Azure - kroku 8

>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Krok 8. Skonfiguruj SAM-R wymagane uprawnienia

[Ścieżki penetracja sieci](use-case-lateral-movement-path.md) wykrywania opiera się na zapytania, które identyfikują Administratorzy lokalni na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, za pomocą konta usługi Azure ATP utworzonego w [krok 2. Łączenie z usługą AD](install-atp-step2.md).
 
Aby zapewnić, że klienci systemu Windows i serwery Zezwalaj na konto usługi ATP Azure do wykonania tej operacji SAM-R, muszą być wprowadzane zmiany do zasad grupy.

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