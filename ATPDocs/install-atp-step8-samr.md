---
title: Konfigurowanie SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego w narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: Opisano sposób konfigurowania usługi Azure ATP na wykonywanie zdalnych połączeń do Menedżera kont zabezpieczeń
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/07/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 49372ce2432e90b04e0d10b2e8e102c1b05e9c9a
ms.sourcegitcommit: bbbe808c08ce703a314c82b46aedaae79ab256a3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2018
ms.locfileid: "48848477"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Konfigurowanie usługi Azure ATP na wykonywanie zdalnych połączeń do Menedżera kont zabezpieczeń
[Ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md) metoda wykrywania polega na zapytania, które identyfikują administratorami lokalnymi na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, przy użyciu konta usługi Azure ATP Service tworzone podczas instalacji narzędzia Azure ATP [krok 2. Łączenie z usługą AD](install-atp-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Konfigurowanie uprawnień SAM-R wymagane
Upewnij się, Windows klienci i serwery zezwolić na koncie usługi Azure ATP przeprowadzić SAM-R, modyfikację **zasad grupy** należy dodać konto usługi Azure ATP oprócz skonfigurowanego konta, na liście  **Dostęp sieciowy** zasad.

1. Znajdź zasady:

 - Nazwa zasad: Dostęp sieciowy — ograniczać dostępu klientów zezwolenie na wykonywanie wywołań zdalnych do Menedżera kont zabezpieczeń
 - Lokalizacja: Konfiguracja komputera, ustawienia Windows, ustawienia zabezpieczeń, zasady lokalne, opcje zabezpieczeń
  
  ![Znajdź zasad](./media/samr-policy-location.png)

2. Dodaj usługę Azure ATP do listy zatwierdzonych kont, które można wykonać tej akcji na nowoczesnych systemów Windows.
 
  ![Dodaj usługę](./media/samr-add-service.png)

3. **Usługa AATP** (usługa Azure ATP tworzone podczas instalacji) ma teraz uprawnienia wymagane do wykonania SAM-R w środowisku.

> [!NOTE]
> Przed wymuszeniem nowe zasady, upewnij się, że środowisko pozostanie bezpieczne, bez wywierania wpływu na zgodność swojej aplikacji dzięki umożliwieniu oraz weryfikowanie proponowanych zmian w trybie inspekcji.

Aby uzyskać więcej informacji na SAM-R i tych zasad grupy, zobacz [dostęp sieciowy: ogranicza dostępu klientów zezwolenie na wykonywanie wywołań zdalnych do Menedżera kont zabezpieczeń](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).



## <a name="see-also"></a>Zobacz też
- [Badanie ataków ścieżki ruchu poprzecznego za pomocą narzędzia Azure ATP](use-case-lateral-movement-path.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)