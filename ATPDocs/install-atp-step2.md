---
title: "Azure instalacji Advanced Threat Protection — krok 2 | Dokumentacja firmy Microsoft"
description: "Krok drugi procedury instalowania Azure ATP ułatwia konfigurowanie ustawień łączności domeny na usługi w chmurze Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 11f9d5bf69ffda0843a94c7a2bb31869dc980dce
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-2"></a>Zainstaluj Azure ATP — krok 2

>[!div class="step-by-step"]
[« Krok 1](install-atp-step1.md)
[Krok 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Krok 2. Podaj nazwę użytkownika i hasło, aby nawiązać połączenie z lasu usługi Active Directory

Przy pierwszym otwarciu portalu Azure ATP obszaru roboczego, pojawi się następujący ekran:

![Azure powitalnej ATP etap 1](media/directory-services.png)

> [!IMPORTANT]
> Wprowadzone poświadczenia użytkownika musi być na koncie użytkownika w lokalnej usłudze Active Directory. 


1.  Wprowadź następujące informacje i kliknij przycisk **Zapisz**:

    |Pole|Komentarze|
    |---------|------------|
    |**Nazwa użytkownika** (wymagana)|Wprowadź tylko do odczytu usługi Active Directory nazwę użytkownika, na przykład: **ATPuser**.|
    |**Hasło** (wymagane)|Wprowadź hasło użytkownika tylko do odczytu, na przykład: **Rysik1**.|
    |**Domena** (wymagana)|Wprowadź domenę użytkownika tylko do odczytu, na przykład: **contoso.com**. **Uwaga:** należy wprowadzić pełną nazwę FQDN domeny, w której znajduje się użytkownik. Na przykład jeśli konto użytkownika znajduje się w domenie corp.contoso.com, należy wprowadzić `corp.contoso.com` not contoso.com|

3. W portalu obszaru roboczego kliknij **Pobierz czujnik Instalatora i zainstaluj pierwszy czujnik** aby kontynuować.


>[!div class="step-by-step"]
[« Krok 1](install-atp-step1.md)
[Krok 3 »](install-atp-step3.md)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)