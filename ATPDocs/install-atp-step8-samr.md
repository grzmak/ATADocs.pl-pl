---
title: Konfigurowanie SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego w narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób konfigurowania SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego w narzędzia Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/17/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a529c9751fc993ec0913a54772d46161f39199f6
ms.sourcegitcommit: 8feb9b65dc0e1de0ace00aca11784e54f9852a15
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/17/2018
ms.locfileid: "39098172"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="install-azure-atp---step-8"></a>Zainstaluj narzędzie Azure ATP - kroku 8

>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)
[kroku 9»](atp-multi-forest.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Krok 8. Konfigurowanie uprawnień SAM-R wymagane

[Ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md) metoda wykrywania polega na zapytania, które identyfikują administratorami lokalnymi na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, za pomocą konta usługi Azure ATP Service utworzonego w [krok 2. Łączenie z usługą AD](install-atp-step2.md).
 
Aby upewnić się, Windows klienci i serwery Zezwalaj na konto usługi Azure ATP do wykonania tej operacji SAM-R modyfikację **zasad grupy** należy dodać konto usługi Azure ATP oprócz skonfigurowanego konta, na liście  **Dostęp sieciowy** zasad.

1. Znajdź zasady:

 - Nazwa zasad: Dostęp sieciowy — ograniczać dostępu klientów zezwolenie na wykonywanie wywołań zdalnych do Menedżera kont zabezpieczeń
 - Lokalizacja: Konfiguracja komputera, ustawienia Windows, ustawienia zabezpieczeń, zasady lokalne, opcje zabezpieczeń
  
  ![Znajdź zasad](./media/samr-policy-location.png)

2. Dodaj usługę Azure ATP do listy zatwierdzonych kont, które można wykonać tej akcji na nowoczesnych systemów Windows.
 
  ![Dodaj usługę](./media/samr-add-service.png)

3. **Usługi AATP** (usługa Azure ATP tworzone podczas instalacji) teraz ma odpowiednie uprawnienia, aby wykonać SAMR w środowisku.

Aby uzyskać więcej informacji na SAM-R i tych zasad grupy, zobacz [dostęp sieciowy: ogranicza dostępu klientów zezwolenie na wykonywanie wywołań zdalnych do Menedżera kont zabezpieczeń](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 7](install-atp-step7.md)
[kroku 9»](atp-multi-forest.md)



## <a name="see-also"></a>Zobacz też
- [Badanie ataków ścieżki ruchu poprzecznego za pomocą narzędzia Azure ATP](use-case-lateral-movement-path.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)