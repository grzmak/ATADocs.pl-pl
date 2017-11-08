---
title: "Zainstaluj Advanced Threat Analytics — krok 8 | Dokumentacja firmy Microsoft"
description: "W ostatnim kroku instalowania usługi ATA można skonfigurować użytkownika wystawionego jako przynęta."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0feb12a2e86adae124016c90431209ec33cdbcb5
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="install-ata---step-8"></a>Instalowanie usługi ATA — krok 8

>[!div class="step-by-step"]
[«Krok 7](vpn-integration-install-step.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Krok 8. Konfigurowanie wykluczeń adresów IP i konta użytkownika wystawionego jako przynęta
Usługa ATA umożliwia wykluczenie konkretnych adresów IP lub użytkowników z wykrywania według pewnych kryteriów. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wykluczenie pozwala usłudze ATA ignorować takie skanery. Przykładem wykluczenia dotyczącego *ataku typu Pass-the-Ticket* jest urządzenie translatora adresów sieciowych (NAT).    

Usługa ATA umożliwia również konfigurację użytkownika wystawionego jako przynęta, który jest używany jako pułapki złośliwych osób — uwierzytelniania skojarzone z tym kontem (zwykle nieaktywni) wyzwala alert.

Aby to skonfigurować, wykonaj następujące kroki:

1.  W konsoli usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**.

    ![Ustawienia konfiguracji usługi ATA](media/ATA-config-icon.png)

2.  W obszarze **Wykrywanie** kliknij pozycję **Ogólne**.

2. W polu **Konta wystawione jako przynęta** podaj nazwę konta wystawionego jako przynęta. W polu kont wystawionych jako przynęta jest wyszukiwalna i automatycznie wyświetla jednostek w sieci.

   ![Przynęta](media/honeytoken.png)

3. Kliknij pozycję **Wykluczenia**. Dla każdego typu zagrożeń podaj konto użytkownika lub adres IP do wykluczenia z wykrywania zagrożeń tego typu, a następnie kliknij znak *plus*. Pole **Dodaj jednostkę** (użytkownik lub komputer) umożliwia wyszukiwanie i obsługuje automatyczne uzupełnianie przy użyciu jednostek dostępnych w sieci. Aby uzyskać więcej informacji, zobacz [Wykluczanie jednostek z wykryć](excluding-entities-from-detections.md)

   ![Wykluczenia](media/exclusions.png)

4.  Kliknij polecenie **Zapisz**.


Gratulacje, usługa Microsoft Advanced Threat Analytics została pomyślnie wdrożona!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Usługa ATA zaczyna od razu skanowanie w poszukiwaniu podejrzanych działań. Niektóre działania, takie jak niektóre podejrzane działania, jest niedostępny, dopóki usługa ATA miał czas na utworzenie profilów zachowania (co najmniej trzy tygodnie).

Aby sprawdzić, czy usługa ATA działa i wykrywa naruszenia bezpieczeństwa sieci, możesz zapoznać się z [podręcznikiem symulacji ataku za pomocą usługi ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[«Krok 7](vpn-integration-install-step.md)



## <a name="related-videos"></a>Powiązane pliki wideo
- [Przegląd wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniej typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania usługi ATA fazy weryfikacji Koncepcji](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

