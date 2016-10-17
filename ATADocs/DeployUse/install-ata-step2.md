---
title: "Instalacja usługi ATA — krok 2 | Microsoft ATA"
description: "Krok drugi procedury instalowania usługi ATA pomaga skonfigurować ustawienia łączności domeny na serwerze centrum usługi ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3768cd103fc2a938d2d39fe34179d74587abc118
ms.openlocfilehash: be58ce053a2ddb59fa1556027e432c0499f8deb4


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Instalowanie usługi ATA — Krok 2

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## Krok 2. Podaj nazwę użytkownika i hasło, aby nawiązać połączenie z lasem usługi Active Directory

Przy pierwszym otwarciu konsoli ATA zostanie wyświetlony następujący ekran:

![ATA welcome stage 1 (ATA — zapraszamy, etap 1)](media/ATA_1.7-welcome-provide-username.png)

1.  Wprowadź następujące informacje i kliknij przycisk **Zapisz**:

    |Pole|Komentarze|
    |---------|------------|
    |**Nazwa użytkownika** (wymagana)|Wprowadź nazwę użytkownika tylko do odczytu, na przykład: **UżytkownikATA**.|
    |**Hasło** (wymagane)|Wprowadź hasło użytkownika tylko do odczytu, na przykład: **Rysik1**.|
    |**Domena** (wymagana)|Wprowadź domenę użytkownika tylko do odczytu, na przykład: **contoso.com**. **Uwaga:** należy wprowadzić pełną nazwę FQDN domeny, w której znajduje się użytkownik. Na przykład jeśli konto użytkownika znajduje się w domenie corp.contoso.com, należy wprowadzić `corp.contoso.com` not contoso.com|
    

    Po zapisaniu, wiadomość powitalna w konsoli zmieni się na następującą: ![ATA welcome stage 1 finished (ATA — zapraszamy, ukończono etap 1)](media/ATA_1.7-welcome-provide-username-finished.png)

2. W konsoli kliknij opcję **Download Gateway setup and install the first Gateway** (Pobierz instalator bramy i zainstaluj pierwszą bramę), aby kontynuować.


>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Oct16_HO2-->


