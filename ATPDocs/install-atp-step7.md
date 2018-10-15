---
title: Usługa Azure Advanced Threat Protection Konfigurowanie wykluczenia z wykrywania i konta wystawione jako przynęta | Dokumentacja firmy Microsoft
description: Konfiguracja wykrywania. wykluczenia i konta użytkownika wystawionego jako przynęta.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9202ba7c2519de0c7cd2eb3103578159dc437e83
ms.sourcegitcommit: 58c75026e5ec4dcab3b0852a41f9f0a0ad6f22eb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2018
ms.locfileid: "49315748"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Konfiguruj wykluczenia z wykrywania i konta wystawione jako przynęta

Narzędzie Azure ATP umożliwia wyłączenie określonych adresów IP lub użytkowników z liczba wykryć. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wykluczenie pozwala narzędzia Azure ATP ignorować takie skanery.  

Narzędzie Azure ATP umożliwia także konfigurację konta wystawione jako przynęta, które są używane jako pułapek dla uczestników złośliwych działań — dowolne uwierzytelnianie związane z tych kont wystawionych jako przynęta (kontem zwykle nieaktywnym), wyzwala alert.

Aby skonfigurować, wykonaj następujące kroki:

1.  W portalu usługi Azure ATP kliknij ikonę ustawień i wybierz pozycję **konfiguracji**.

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


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami zure](https://aka.ms/azureatpcommunity)
