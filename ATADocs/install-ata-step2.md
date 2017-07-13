---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 2 | Dokumentacja firmy Microsoft"
description: "Krok drugi procedury instalowania usługi ATA pomaga skonfigurować ustawienia łączności domeny na serwerze centrum usługi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: aa5e752fa10644165cb70d2cd8c08a1145261edb
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/03/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Instalowanie usługi ATA — Krok 2
<a id="install-ata---step-2" class="xliff"></a>

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## Krok 2. Podaj nazwę użytkownika i hasło, aby nawiązać połączenie z lasem usługi Active Directory
<a id="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest" class="xliff"></a>

Przy pierwszym otwarciu konsoli ATA zostanie wyświetlony następujący ekran:

![ATA welcome stage 1 (ATA — zapraszamy, etap 1)](media/ATA_1.7-welcome-provide-username.png)

1.  Wprowadź następujące informacje i kliknij przycisk **Zapisz**:

    |Pole|Komentarze|
    |---------|------------|
    |**Nazwa użytkownika** (wymagana)|Wprowadź nazwę użytkownika tylko do odczytu, na przykład: **UżytkownikATA**.|
    |**Hasło** (wymagane)|Wprowadź hasło użytkownika tylko do odczytu, na przykład: **Rysik1**.|
    |**Domena** (wymagana)|Wprowadź domenę użytkownika tylko do odczytu, na przykład: **contoso.com**. **Uwaga:** należy wprowadzić pełną nazwę FQDN domeny, w której znajduje się użytkownik. Na przykład jeśli konto użytkownika znajduje się w domenie corp.contoso.com, należy wprowadzić `corp.contoso.com` not contoso.com|

2. Możesz kliknąć pozycję **Testuj połączenie**, aby przetestować łączność z domeną i sprawdzić, czy podane poświadczenia umożliwiają uzyskiwanie dostępu. Ta opcja zadziała tylko, jeśli centrum usługi ATA ma łączność z domeną.   

    Po zapisaniu wiadomość powitalna w konsoli zmieni się na następującą: ![ATA welcome stage 1 finished (ATA — zapraszamy, ukończono etap 1)](media/ATA_1.7-welcome-provide-username-finished.png)

3. W konsoli kliknij opcję **Download Gateway setup and install the first Gateway** (Pobierz instalator bramy i zainstaluj pierwszą bramę), aby kontynuować.


>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## Zobacz też
<a id="see-also" class="xliff"></a>

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
