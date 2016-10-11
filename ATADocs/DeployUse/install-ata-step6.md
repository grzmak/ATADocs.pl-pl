---
title: "Instalacja usługi ATA | Microsoft ATA"
description: "W ostatnim kroku instalowania usługi ATA można skonfigurować użytkownika wystawionego jako przynęta."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 9ee2f36d8f0b7eae061873e8735139ccc4da00d1


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Instalowanie usługi ATA — Krok 6

>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)

## Krok 6. Konfigurowanie wykluczeń adresów IP i konta użytkownika wystawionego jako przynęta
Usługa ATA umożliwia wyłączenie określonych adresów IP i podsieci IP z dwóch typów wykrywania: **rekonesans przy użyciu systemu DNS** i **atak typu Pass-the-Ticket**. 

Na przykład można **wykluczyć z rekonesansu przy użyciu systemu DNS** skaner zabezpieczeń, który wykorzystuje system DNS jako mechanizm skanowania. Wykluczenie pozwala usłudze ATA ignorować takie skanery. Przykładem wykluczenia dotyczącego *ataku typu Pass-the-Ticket* jest urządzenie translatora adresów sieciowych (NAT).    

Usługa ATA umożliwia również skonfigurowanie konta użytkownika wystawionego jako przynęta, które jest używane jako pułapka dla uczestników złośliwych działań — dowolne uwierzytelnianie związane z tym kontem (zwykle nieaktywnym) powoduje wyzwolenie alertu.

Aby skonfigurować powyższe opcje, wykonaj następujące kroki:

1.  W konsoli usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**.

    ![Ustawienia konfiguracji usługi ATA](media/ATA-config-icon.JPG)

2.  W obszarze **Detection exclusions** (Wykluczenia wykrywania) wprowadź adresy IP *rekonesansu przy użyciu systemu DNS* lub *ataku typu Pass-the-Ticket*. Użyj formatu CIDR, na przykład: `192.168.1.0/24` i kliknij znak *plus*.

    ![Zapisz zmiany](media/ATA-exclusions.png)

3.  W obszarze **Detection settings** (Ustawienia wykrywania) wprowadź identyfikator SID konta wystawionego jako przynęta i kliknij znak plus. Na przykład: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![Ustawienia konfiguracji usługi ATA](media/ATA-honeytoken.png)

    > [!NOTE]
    > Aby znaleźć identyfikator SID użytkownika, wyszukaj użytkownika w konsoli ATA, a następnie kliknij kartę **Informacje o koncie**. 

4.  Kliknij polecenie **Zapisz**.


Gratulacje, usługa Microsoft Advanced Threat Analytics została pomyślnie wdrożona!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Usługa ATA natychmiast rozpocznie skanowanie w poszukiwaniu podejrzanych działań. Niektóre działania, np. niektóre działania związane z podejrzanym zachowaniem, nie będą dostępne, dopóki usługa ATA nie utworzy profilów zachowania (trwa to co najmniej trzy tygodnie).


>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)


## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Sep16_HO4-->


