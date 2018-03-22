---
title: "Skonfiguruj SAM-R, aby włączyć wykrywanie ścieżki penetracja sieci w Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "Opisuje sposób konfigurowania SAM-R, aby włączyć wykrywanie ścieżki penetracja sieci w Advanced Threat Analytics (ATA)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a49478698adea15637698f4c715cdd34a9a601c4
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*

# <a name="install-ata---step-9"></a>Instalowanie usługi ATA — krok 9

>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Krok 9. Skonfiguruj SAM-R wymagane uprawnienia

[Ścieżki penetracja sieci](use-case-lateral-movement-path.md) wykrywania opiera się na zapytania, które identyfikują Administratorzy lokalni na określonych komputerach. Te zapytania są wykonywane przy użyciu protokołu SAM-R, za pomocą konta usługi ATA utworzonego w [krok 2. Łączenie z usługą AD](install-ata-step2.md).
 
Aby zapewnić, że klienci systemu Windows i serwery Zezwalaj na konto usługi ATA do wykonania tej operacji SAM-R, muszą być wprowadzane zmiany do zasad grupy.

1. Znajdź zasad:

 - Nazwa zasad: Dostęp do sieci — Ogranicz dozwolone do zdalnego łączenia się SAM klientów
 - Lokalizacja: Konfiguracja komputera, ustawienia systemu Windows, ustawienia zabezpieczeń, zasady lokalne, opcje zabezpieczeń
  
  ![Zlokalizuj zasad](./media/samr-policy-location.png)

2. Dodaj usługę ATA do listy zatwierdzonych kont stanie do wykonania tej akcji nowoczesnych systemach Windows.
 
  ![Dodaj usługę](./media/samr-add-service.png)

3. **Usługa ATA** (tworzone podczas instalacji usługi ATA) teraz ma odpowiednie uprawnienia do wykonania SAMR w środowisku.

Aby uzyskać więcej informacji na SAM-R i zasad grupy, zobacz [dostępu do sieci: ograniczanie klientach dozwolone do zdalnego łączenia się SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[«Krok 8](install-ata-step7.md)

## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania usługi ATA fazy weryfikacji Koncepcji](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
