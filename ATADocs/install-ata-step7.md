---
title: Instalowanie usługi Advanced Threat Analytics — krok 8 | Dokumentacja firmy Microsoft
description: W ostatnim kroku instalowania usługi ATA można skonfigurować użytkownika wystawionego jako przynęta.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: eacc3c2449e6fd7771c43b97b8ed08276ab130d2
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133549"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="install-ata---step-8"></a>Instalowanie usługi ATA — krok 8

>[!div class="step-by-step"]
[«Krok 7](vpn-integration-install-step.md)
[kroku 9»](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Krok 8. Konfigurowanie wykluczeń adresów IP i konta użytkownika wystawionego jako przynęta
Usługa ATA umożliwia wykluczenie konkretnych adresów IP lub użytkowników z wykrywania według pewnych kryteriów. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wykluczenie pozwala usłudze ATA ignorować takie skanery. Przykładem wykluczenia dotyczącego *ataku typu Pass-the-Ticket* jest urządzenie translatora adresów sieciowych (NAT).    

Usługa ATA umożliwia również konfigurację użytkownika wystawionego jako przynęta, które jest używane jako pułapka dla uczestników złośliwych działań — dowolne uwierzytelnianie związane z tym kontem (kontem zwykle nieaktywnym) powoduje wyzwolenie alertu.

Aby to skonfigurować, wykonaj następujące kroki:

1.  W konsoli usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**.

    ![Ustawienia konfiguracji usługi ATA](media/ATA-config-icon.png)

2.  W obszarze **wykrywania**, kliknij przycisk **tagów jednostki**.

2. W polu **Konta wystawione jako przynęta** podaj nazwę konta wystawionego jako przynęta. Pole konta wystawione jako przynęta umożliwia wyszukiwanie i automatycznie wyświetla jednostki w sieci.

   ![Przynęta](media/honeytoken.png)

3. Kliknij pozycję **Wykluczenia**. Dla każdego typu zagrożeń podaj konto użytkownika lub adres IP do wykluczenia z wykrywania zagrożeń tego typu, a następnie kliknij znak *plus*. Pole **Dodaj jednostkę** (użytkownik lub komputer) umożliwia wyszukiwanie i obsługuje automatyczne uzupełnianie przy użyciu jednostek dostępnych w sieci. Aby uzyskać więcej informacji, zobacz [Wykluczanie jednostek z wykryć](excluding-entities-from-detections.md)

   ![Wykluczenia](media/exclusions.png)

4.  Kliknij polecenie **Zapisz**.


Gratulacje, usługa Microsoft Advanced Threat Analytics została pomyślnie wdrożona!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Usługa ATA uruchamia skanowanie w poszukiwaniu podejrzanych działań od razu. Niektóre działania, takie jak niektóre podejrzane działania, jest niedostępny, dopóki usługa ATA czas na utworzenie profilów zachowania (co najmniej trzy tygodnie).

Aby sprawdzić, czy usługa ATA działa i wykrywa naruszenia bezpieczeństwa sieci, możesz zapoznać się z [podręcznikiem symulacji ataku za pomocą usługi ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[«Krok 7](vpn-integration-install-step.md)
[kroku 9»](install-ata-step9-samr.md)


## <a name="related-videos"></a>Pokrewne wideo
- [Omówienie wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniego typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania weryfikacji Koncepcji usługi ATA](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

