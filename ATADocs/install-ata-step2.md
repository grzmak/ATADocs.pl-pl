---
title: Instalowanie usługi Advanced Threat Analytics — Krok 2 | Dokumentacja firmy Microsoft
description: Krok drugi procedury instalowania usługi ATA pomaga skonfigurować ustawienia łączności domeny na serwerze centrum usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4b2e7ae1dad939db3a2394876acfe9ed4042924b
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133263"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="install-ata---step-2"></a>Instalowanie usługi ATA — Krok 2

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Krok 2. Podaj nazwę użytkownika i hasło, aby nawiązać połączenie z lasem usługi Active Directory

Przy pierwszym otwarciu konsoli ATA zostanie wyświetlony następujący ekran:

![ATA welcome stage 1 (ATA — zapraszamy, etap 1)](media/ATA_1.7-welcome-provide-username.png)

1.  Wprowadź następujące informacje i kliknij przycisk **Zapisz**:

    |Pole|Komentarze|
    |---------|------------|
    |**Nazwa użytkownika** (wymagana)|Wprowadź nazwę użytkownika tylko do odczytu, na przykład: **UżytkownikATA**.|
    |**Hasło** (wymagane)|Wprowadź hasło użytkownika tylko do odczytu, na przykład: **Rysik1**.|
    |**Domena** (wymagana)|Wprowadź domenę użytkownika tylko do odczytu, na przykład: **contoso.com**. **Uwaga:** należy wprowadzić pełną nazwę FQDN domeny, w której znajduje się użytkownik. Na przykład jeśli konto użytkownika znajduje się w domenie corp.contoso.com, należy wprowadzić `corp.contoso.com` not contoso.com|

2. Możesz kliknąć pozycję **Testuj połączenie**, aby przetestować łączność z domeną i sprawdzić, czy podane poświadczenia umożliwiają uzyskiwanie dostępu. To działa, jeśli Centrum usługi ATA ma łączność z domeną.    

    Po zapisaniu, wiadomość powitalna w konsoli zmieni się na następujący komunikat: ![ATA Welcome stage 1 zakończona — Zapraszamy](media/ATA_1.7-welcome-provide-username-finished.png)

3. W konsoli kliknij opcję **Download Gateway setup and install the first Gateway** (Pobierz instalator bramy i zainstaluj pierwszą bramę), aby kontynuować.


>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## <a name="see-also"></a>Zobacz też
## <a name="related-videos"></a>Pokrewne wideo
- [Omówienie wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniego typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania weryfikacji Koncepcji usługi ATA](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
