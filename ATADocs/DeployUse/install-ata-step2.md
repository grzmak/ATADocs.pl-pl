---
title: "Instalacja usługi ATA — krok 2 | Microsoft ATA"
description: "Krok drugi procedury instalowania usługi ATA pomaga skonfigurować ustawienia łączności domeny na serwerze centrum usługi ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 54f5652e980dd8b62d5bbfb642e56eaac7d6e343


---

# Instalowanie usługi ATA — Krok 2

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## Krok 2. Konfigurowanie ogólnych ustawień bramy usługi ATA
Ustawienia na karcie **Ogólne** są stosowane do wszystkich bram usługi ATA zarządzanych przez centrum usługi ATA.

Aby skonfigurować ogólne ustawienia bramy usługi ATA, wykonaj następujące czynności:

1.  Uruchom konsolę usługi ATA i zaloguj się. Aby uzyskać instrukcje, zobacz [Praca z konsolą usługi ATA](working-with-ata-console.md).

2.  Kliknij ikonę Ustawienia i wybierz pozycję **Konfiguracja**.

    ![Ustawienia konfiguracji bramy usługi ATA](media/ATA-config-icon.JPG)

3.  Na karcie **Ogólne** w obszarze **Bramy usługi ATA** wprowadź następujące informacje i kliknij przycisk **Zapisz**.

    |Pole|Komentarze|
    |---------|------------|
    |**Nazwa użytkownika** (wymagana)|Wprowadź nazwę użytkownika tylko do odczytu, na przykład: **użytkownik1**.|
    |**Hasło** (wymagane)|Wprowadź hasło użytkownika tylko do odczytu, na przykład: **Rysik1**. **Uwaga:** upewnij się, że to hasło jest prawidłowe. Jeśli zapiszesz nieprawidłowe hasło, usługa ATA przestanie działać na serwerach bramy usługi ATA.|
    |**Domena** (wymagana)|Wprowadź domenę użytkownika tylko do odczytu, na przykład: **contoso.com**. **Uwaga:** należy wprowadzić pełną nazwę FQDN domeny, w której znajduje się użytkownik. Na przykład jeśli konto użytkownika znajduje się w domenie corp.contoso.com, należy wprowadzić `corp.contoso.com` not contoso.com|
    |Automatyczna aktualizacja wszystkich bram usługi ATA |Jeśli to ustawienie jest włączone, w nadchodzących wersjach usługi wszystkie bramy ATA będą automatycznie aktualizowane, gdy użytkownik zaktualizuje centrum usługi ATA.|

    ![Obraz ustawień łączności domeny usługi ATA](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jul16_HO3-->


