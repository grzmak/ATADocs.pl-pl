---
title: "Azure instalacji Advanced Threat Protection — krok 7 | Dokumentacja firmy Microsoft"
description: "W ostatnim kroku instalowania Azure ATP możesz skonfigurować użytkownika wystawionego jako przynęta."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bef13d0f4799a4483eda6604a8ed96befaa13508
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-7"></a>Zainstaluj Azure ATP — krok 7

>[!div class="step-by-step"]
[« Krok 6](install-atp-step6-vpn.md)
[Krok 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-user"></a>Krok 7. Konfigurowanie wykluczeń wykrywania i użytkownika wystawionego jako przynęta

Azure ATP umożliwia wykluczenie określonych adresów IP lub użytkowników z liczba wykryć. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wyłączenie pomaga ignorowania takich skanery ATP Azure.  

Azure ATP umożliwia również Konfigurowanie użytkownika wystawionego jako przynęta, który jest używany jako pułapki złośliwych osób — uwierzytelniania skojarzone z tym kontem (zwykle nieaktywni) wyzwala alert.

Aby to skonfigurować, wykonaj następujące kroki:

1.  W portalu Azure ATP obszaru roboczego kliknij ikonę ustawień i wybierz pozycję **konfiguracji**.

    ![Ustawienia konfiguracji w usłudze Azure ATP](media/atp-config-menu.png)

2.  W obszarze **wykrywania**, kliknij przycisk **tagi jednostek**.

3. W obszarze **kont wystawionych jako przynęta** wystawionego jako przynęta nazwę konta i kliknij przycisk  **+**  logowania. W polu kont wystawionych jako przynęta jest wyszukiwalna i automatycznie wyświetla jednostek w sieci. Kliknij polecenie **Zapisz**.

   ![Przynęta](media/honeytoken-sensitive.png)

4. Kliknij pozycję **Wykluczenia**. Dla każdego typu zagrożeń podaj konto użytkownika lub adres IP do wykluczenia z wykrywania zagrożeń tego typu, a następnie kliknij znak *plus*. Pole **Dodaj jednostkę** (użytkownik lub komputer) umożliwia wyszukiwanie i obsługuje automatyczne uzupełnianie przy użyciu jednostek dostępnych w sieci. Aby uzyskać więcej informacji, zobacz [wykluczanie jednostek wykryć](excluding-entities-from-detections.md) i [przewodnik podejrzanych działań](suspicious-activity-guide.md).

   ![Wykluczenia](media/exclusions.png)

5.  Kliknij polecenie **Zapisz**.


Gratulacje, zostały pomyślnie wdrożone Azure Advanced Threat Protection!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Azure ATP rozpoczyna się od razu skanowanie w poszukiwaniu podejrzanych działań. Niektóre wykrywania, takie jak nietypowe grupy zmian, wymagają okres uczenie i nie są dostępne natychmiast po ich wdrożeniu Azure ATP.



>[!div class="step-by-step"]
[« Krok 6](install-atp-step6-vpn.md)
[Krok 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
