---
title: Usługa Azure Advanced Threat Protection zaawansowane zasady inspekcji wyboru | Dokumentacja firmy Microsoft
description: Ten artykuł zawiera omówienie wyboru Zaawansowane zasady inspekcji usługi Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d7207388702c659a08258862326ee89a49ae3ac2
ms.sourcegitcommit: f3f80c5d3e2e5c1bcf975ae0cbae1469da7ab74d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/12/2018
ms.locfileid: "44515512"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="azure-atp-advanced-audit-policy-check"></a>Usługa Azure ATP zaawansowane zasady inspekcji wyboru

Wykrywanie zaawansowanej ochrony przed zagrożeniami w usłudze Azure opiera się na określonych Windows dzienniki zdarzeń widoczność w niektórych scenariuszach, takich jak logowanie, modyfikacji grup zabezpieczeń i podobne zdarzenia uwierzytelniania NTLM. Poprawne zdarzeń inspekcji i uwzględnione w dzienniku zdarzeń Windows kontrolerów domeny wymaga ustawienia zaawansowane zasady inspekcji. Nieprawidłowe ustawienia zaawansowane zasady inspekcji pozostawić krytyczne zdarzenia z dzienników i wyników narzędzia Azure ATP opartych na niepełnych danych.

Aby ułatwić sprawdzić bieżący stan poszczególnych zasad inspekcji zaawansowanych kontrolera domeny usługi Azure ATP automatycznie sprawdza, czy Twoje istniejące zaawansowane zasady inspekcji i problemy alerty dotyczące kondycji dla ustawień zasad, które wymagają modyfikacji. Każdy alertów dotyczących kondycji udostępnia szczegółowe informacje dotyczące kontrolera domeny, zasady problematyczne, jak również sugestie dotyczące korygowania.

![Alert zasad dotyczących kondycji zaawansowanej inspekcji](media/atp-health-alert-audit-policy.png)


Zaawansowane zasady inspekcji zabezpieczeń jest włączone za pomocą **domyślne zasady kontrolerów domeny** obiektu zasad grupy. Te inspekcji na kontrolerze domeny Windows zdarzenia są rejestrowane zdarzenia. 

<br>Modyfikowanie zasad inspekcji zaawansowanych, kontrolera domeny przy użyciu następujących instrukcji:

1. Zaloguj się do serwera jako **Administrator domeny**.
2. Ładowanie Edytor zarządzania zasadami grupy z **Menedżera serwera** > **narzędzia** > **Zarządzanie zasadami grupy**. 
3. Rozwiń **jednostki organizacyjnej Kontrolery domeny**, kliknij prawym przyciskiem myszy **domyślne zasady kontrolerów domeny** i wybierz **Edytuj**. 

    ![Edytuj zasady kontrolera domeny](media/atp-advanced-audit-policy-check-step-1.png)

4. W oknie zostanie otwarta, przejdź do **konfiguracji komputera** > **zasady** > **ustawienia Windows**  >  **Ustawienia zabezpieczeń** > **konfigurację zaawansowanych zasad inspekcji**.

    ![Konfiguracja zaawansowanych zasad inspekcji](media/atp-advanced-audit-policy-check-step-2.png)

5. Przejdź do konta logowania, kliknij dwukrotnie **inspekcja weryfikacji poświadczeń** i wybierz **Konfiguruj następujące zdarzenia inspekcji** sukcesów i niepowodzeń zdarzenia. 

    ![Sprawdzanie poprawności poświadczeń](media/atp-advanced-audit-policy-check-step-3.png)

6. Przejdź do zarządzania kontami, kliknij dwukrotnie **Inspekcja zarządzania grupami zabezpieczeń** i wybierz **Konfiguruj następujące zdarzenia inspekcji** sukcesów i niepowodzeń zdarzenia.

    ![Inspekcja zarządzania grupami zabezpieczeń](media/atp-advanced-audit-policy-check-step-4.png)

7. Po zastosowaniu za pośrednictwem zasad grupy, nowe zdarzenia są widoczne w obszarze usługi **dzienniki zdarzeń Windows**.

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
