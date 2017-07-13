---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 7 | Microsoft Docs"
description: "W ostatnim kroku instalowania usługi ATA można skonfigurować użytkownika wystawionego jako przynęta."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d261273adfa23392a9c0b8408483aa02708f1eee
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/03/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Instalowanie usługi ATA — Krok 7
<a id="install-ata---step-7" class="xliff"></a>

>[!div class="step-by-step"]
[« Krok 6](install-ata-step6.md)

## Krok 7. Konfigurowanie wykluczeń adresów IP i konta użytkownika wystawionego jako przynęta
<a id="step-7-configure-ip-address-exclusions-and-honeytoken-user" class="xliff"></a>
Usługa ATA umożliwia wykluczenie konkretnych adresów IP lub użytkowników z wykrywania według pewnych kryteriów. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wykluczenie pozwala usłudze ATA ignorować takie skanery. Przykładem wykluczenia dotyczącego *ataku typu Pass-the-Ticket* jest urządzenie translatora adresów sieciowych (NAT).    

Usługa ATA umożliwia również skonfigurowanie konta użytkownika wystawionego jako przynęta, które jest używane jako pułapka dla uczestników złośliwych działań — dowolne uwierzytelnianie związane z tym kontem (zwykle nieaktywnym) powoduje wyzwolenie alertu.

Aby skonfigurować powyższe opcje, wykonaj następujące kroki:

1.  W konsoli usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**.

    ![Ustawienia konfiguracji usługi ATA](media/ATA-config-icon.png)

2.  W obszarze **Wykrywanie** kliknij pozycję **Ogólne**.

2. W polu **Konta wystawione jako przynęta** podaj nazwę konta wystawionego jako przynęta. Pole Konta wystawione jako przynęta umożliwia wyszukiwanie i automatycznie wyświetla jednostki dostępne w sieci.

   ![Przynęta](media/honeytoken.png)

3. Kliknij pozycję **Wykluczenia**. Dla każdego typu zagrożeń podaj konto użytkownika lub adres IP do wykluczenia z wykrywania zagrożeń tego typu, a następnie kliknij znak *plus*. Pole dodawania jednostki (użytkownika lub komputera) umożliwia wyszukiwanie i obsługuje automatyczne uzupełnianie przy użyciu jednostek dostępnych w sieci.

   ![Wykluczenia](media/exclusions.png)


  > [!NOTE]
  > Aby znaleźć identyfikator SID użytkownika, wyszukaj użytkownika w konsoli ATA, a następnie kliknij kartę **Informacje o koncie**. 

4.  Kliknij polecenie **Zapisz**.


Gratulacje, usługa Microsoft Advanced Threat Analytics została pomyślnie wdrożona!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Usługa ATA natychmiast rozpocznie skanowanie w poszukiwaniu podejrzanych działań. Niektóre działania, np. niektóre działania związane z podejrzanym zachowaniem, nie będą dostępne, dopóki usługa ATA nie utworzy profilów zachowania (trwa to co najmniej trzy tygodnie).

Aby sprawdzić, czy usługa ATA działa i wykrywa naruszenia bezpieczeństwa sieci, możesz zapoznać się z [podręcznikiem symulacji ataku za pomocą usługi ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[« Krok 6](install-ata-step6.md)


## Zobacz też
<a id="see-also" class="xliff"></a>

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

