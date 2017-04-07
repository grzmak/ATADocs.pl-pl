---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 6 | Dokumentacja firmy Microsoft"
description: "W ostatnim kroku instalowania usługi ATA można skonfigurować użytkownika wystawionego jako przynęta."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: da6e72ac5c2966f3e77ce3bef8fe23fcda6770a4
ms.sourcegitcommit: 9b128d6946e32b00f595e00902b9ff95f18141ff
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="install-ata---step-6"></a>Instalowanie usługi ATA — Krok 6

>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)

## <a name="step-6-configure--ip-address-exclusions-and-honeytoken-user"></a>Krok 6. Konfigurowanie wykluczeń adresów IP i konta użytkownika wystawionego jako przynęta
Usługa ATA umożliwia wyłączenie określonych adresów IP z dwóch typów wykrywania: **rekonesans przy użyciu systemu DNS** i **atak typu Pass-the-Ticket**. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wykluczenie pozwala usłudze ATA ignorować takie skanery. Przykładem wykluczenia dotyczącego *ataku typu Pass-the-Ticket* jest urządzenie translatora adresów sieciowych (NAT).    

Usługa ATA umożliwia również skonfigurowanie konta użytkownika wystawionego jako przynęta, które jest używane jako pułapka dla uczestników złośliwych działań — dowolne uwierzytelnianie związane z tym kontem (zwykle nieaktywnym) powoduje wyzwolenie alertu.

Aby skonfigurować powyższe opcje, wykonaj następujące kroki:

1.  W konsoli usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**.

    ![Ustawienia konfiguracji usługi ATA](media/ATA-config-icon.JPG)

2.  W obszarze **Detection exclusions** (Wykluczenia wykrywania) wprowadź adresy IP *rekonesansu przy użyciu systemu DNS* lub *ataku typu Pass-the-Ticket* i kliknij znak *plus*.

    ![Zapisz zmiany](media/ATA-exclusions.png)

3.  W obszarze **Detection settings** (Ustawienia wykrywania) wprowadź identyfikator SID konta wystawionego jako przynęta i kliknij znak plus. Na przykład: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![Ustawienia konfiguracji usługi ATA](media/ATA-honeytoken.png)

    > [!NOTE]
    > Aby znaleźć identyfikator SID użytkownika, wyszukaj użytkownika w konsoli ATA, a następnie kliknij kartę **Informacje o koncie**. 

4.  Kliknij polecenie **Zapisz**.


Gratulacje, usługa Microsoft Advanced Threat Analytics została pomyślnie wdrożona!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Usługa ATA natychmiast rozpocznie skanowanie w poszukiwaniu podejrzanych działań. Niektóre działania, np. niektóre działania związane z podejrzanym zachowaniem, nie będą dostępne, dopóki usługa ATA nie utworzy profilów zachowania (trwa to co najmniej trzy tygodnie).

Aby sprawdzić, czy usługa ATA działa i wykrywa naruszenia bezpieczeństwa sieci, możesz zapoznać się z [podręcznikiem symulacji ataku za pomocą usługi ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)


## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

