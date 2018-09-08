---
title: Konfigurowanie SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób konfigurowania SAM-R, aby włączyć wykrywanie ścieżki ruchu poprzecznego w Advanced Threat Analytics (ATA)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8a1de6e0f3d5234eb96d710b54ded8c8a894f440
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125740"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*

# <a name="install-ata---step-9"></a>Instalowanie usługi ATA — krok 9

>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Krok 9. Konfigurowanie uprawnień SAM-R wymagane

[Ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md) metoda wykrywania polega na zapytania, które identyfikują administratorami lokalnymi na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, za pomocą konta usługi ATA, utworzonego w [krok 2. Łączenie z usługą AD](install-ata-step2.md).
 
Aby upewnić się, czy serwery i klienci Windows zezwalają na konto usługi ATA do wykonania tej operacji SAM-R modyfikację usługi **zasady grupy** muszą być wykonane, dodaje konto usługi ATA, oprócz skonfigurowanego konta, na liście w **dostęp sieciowy** zasad.

1. Znajdź zasady:

 - Nazwa zasad: Dostęp sieciowy — ograniczać dostępu klientów zezwolenie na wykonywanie wywołań zdalnych do Menedżera kont zabezpieczeń
 - Lokalizacja: Konfiguracja komputera, ustawienia Windows, ustawienia zabezpieczeń, zasady lokalne, opcje zabezpieczeń
  
  ![Znajdź zasad](./media/samr-policy-location.png)

2. Dodaj usługę ATA do listy zatwierdzonych kont, które można wykonać tej akcji na nowoczesnych systemów Windows.
 
  ![Dodaj usługę](./media/samr-add-service.png)

3. **Usługa ATA** (tworzona podczas instalacji usługi ATA) teraz ma odpowiednie uprawnienia, aby wykonać SAM-R w środowisku.

> [!NOTE]
> Przed wymuszeniem nowe zasady, upewnij się, że środowisko pozostanie bezpieczne, bez wywierania wpływu na zgodność aplikacji dzięki umożliwieniu oraz weryfikowanie proponowane zmiany w trybie inspekcji. 

 Aby uzyskać więcej informacji na temat SAM-R i zasad grupy, zobacz [dostęp sieciowy: ogranicza dostępu klientów zezwolenie na wykonywanie wywołań zdalnych do Menedżera kont zabezpieczeń](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania weryfikacji Koncepcji usługi ATA](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
