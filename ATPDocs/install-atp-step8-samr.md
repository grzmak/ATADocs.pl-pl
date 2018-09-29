---
title: Konfigurowanie SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego w narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób konfigurowania SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego w narzędzia Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/31/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 34ee1589d59b0740e9d3b05eb117991325619295
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453996"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="install-azure-atp---step-8"></a>Zainstaluj narzędzie Azure ATP - kroku 8

> [!div class="step-by-step"]
> [«Krok 7](install-atp-step7.md)
> [kroku 9»](atp-multi-forest.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Krok 8. Konfigurowanie uprawnień SAM-R wymagane

[Ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md) metoda wykrywania polega na zapytania, które identyfikują administratorami lokalnymi na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, przy użyciu usługi Azure ATP konto utworzone w [krok 2. Łączenie z usługą AD](install-atp-step2.md).
 
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


> [!div class="step-by-step"]
> [«Krok 7](install-atp-step7.md)
> [kroku 9»](atp-multi-forest.md)



## <a name="see-also"></a>Zobacz też
- [Badanie ataków ścieżki ruchu poprzecznego za pomocą narzędzia Azure ATP](use-case-lateral-movement-path.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)