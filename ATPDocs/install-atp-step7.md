---
title: Install Azure Zaawansowana ochrona przed zagrożeniami — krok 7 | Dokumentacja firmy Microsoft
description: W ostatnim kroku instalowania usługi Azure ATP możesz skonfigurować użytkownika wystawionego jako przynęta.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/2/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9252e47978a4adc0e2059a3111b362ff2b042daf
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453803"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="install-azure-atp---step-7"></a>Zainstaluj narzędzie Azure ATP — krok 7

> [!div class="step-by-step"]
> [« Krok 6](install-atp-step6-vpn.md)
> [Krok 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-accounts"></a>Krok 7. Konfiguruj wykluczenia z wykrywania i konta wystawione jako przynęta

Narzędzie Azure ATP umożliwia wyłączenie określonych adresów IP lub użytkowników z liczba wykryć. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wykluczenie pozwala narzędzia Azure ATP ignorować takie skanery.  

Narzędzie Azure ATP umożliwia także konfigurację konta wystawione jako przynęta, które są używane jako pułapek dla uczestników złośliwych działań — dowolne uwierzytelnianie związane z tych kont wystawionych jako przynęta (kontem zwykle nieaktywnym), wyzwala alert.

Aby skonfigurować, wykonaj następujące kroki:

1.  W portalu usługi Azure ATP obszaru roboczego kliknij ikonę ustawień i wybierz pozycję **konfiguracji**.

    ![Ustawienia konfiguracji usługi Azure ATP](media/atp-config-menu.png)

2.  W obszarze **wykrywania**, kliknij przycisk **tagów jednostki**.

3. W obszarze **konta wystawione jako przynęta**, wprowadź nazwę konta wystawionego jako przynęta i kliknij przycisk **+** logowania. Pole konta wystawione jako przynęta umożliwia wyszukiwanie i automatycznie wyświetla jednostki w sieci. Kliknij polecenie **Zapisz**.

   ![Przynęta](media/honeytoken-sensitive.png)

4. Kliknij pozycję **Wykluczenia**. Wprowadź konto użytkownika lub adres IP do wykluczenia z wykrywania, dla każdego typu zagrożeń. 
5. Kliknij przycisk *oraz* logowania. Pole **Dodaj jednostkę** (użytkownik lub komputer) umożliwia wyszukiwanie i obsługuje automatyczne uzupełnianie przy użyciu jednostek dostępnych w sieci. Aby uzyskać więcej informacji, zobacz [wykluczanie jednostek z wykryć](excluding-entities-from-detections.md) i [Przewodnik po podejrzanych działaniach](suspicious-activity-guide.md).

   ![Wykluczenia](media/exclusions.png)

6.  Kliknij polecenie **Zapisz**.


Gratulacje, pomyślnie wdrożono usługi Azure Advanced Threat Protection!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Usługa Azure ATP skanowanie w poszukiwaniu podejrzanych działań rozpoczyna się natychmiast. Niektóre funkcje wykrywania, takie jak nietypowe modyfikacji grup, wymagają okresu uczenia i nie są dostępne od razu po wdrożeniu usługi Azure ATP.



> [!div class="step-by-step"]
> [« Krok 6](install-atp-step6-vpn.md)
> [Krok 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
