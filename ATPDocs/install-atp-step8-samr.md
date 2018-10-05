---
title: Konfigurowanie SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego w narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób konfigurowania usługi Azure ATP na wykonywanie zdalnych połączeń do Menedżera kont zabezpieczeń
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d7875202c05deb98c301cb18153f8080fa42459c
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782883"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Konfigurowanie usługi Azure ATP na wykonywanie zdalnych połączeń do Menedżera kont zabezpieczeń

<a name="-head"></a><<<<<<< HEAD
=======
> [!div class="step-by-step"]
> [«Krok 7](install-atp-step7.md)
> [kroku 9»](atp-multi-forest.md)
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

## <a name="configure-sam-r-required-permissions"></a>Konfigurowanie uprawnień SAM-R wymagane


[Ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md) metoda wykrywania polega na zapytania, które identyfikują administratorami lokalnymi na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, przy użyciu konta usługi Azure ATP Service tworzone podczas instalacji narzędzia Azure ATP [krok 2. Łączenie z usługą AD](install-atp-step2.md).
 
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


<a name="-head"></a><<<<<<< HEAD
=======
> [!div class="step-by-step"]
> [«Krok 7](install-atp-step7.md)
> [kroku 9»](atp-multi-forest.md)


>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

## <a name="see-also"></a>Zobacz też
- [Badanie ataków ścieżki ruchu poprzecznego za pomocą narzędzia Azure ATP](use-case-lateral-movement-path.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)