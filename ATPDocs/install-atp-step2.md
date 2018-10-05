---
title: Zainstaluj usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Krok drugi procedury instalowania usługi Azure ATP pomocne podczas konfigurowania ustawień łączności domeny na usługi w chmurze usługi Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7e13bf0e3d32fc14cf1f0a91f3e7d18accea067c
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783005"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="install-azure-atp---step-2"></a>Zainstaluj narzędzie Azure ATP — krok 2

> [!div class="step-by-step"]
> [« Krok 1](install-atp-step1.md)
> [Krok 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Krok 2. Podaj nazwę użytkownika i hasło, aby nawiązać połączenie z lasem usługi Active Directory

Przy pierwszym otwarciu portalu usługi Azure ATP pojawi się następujący ekran:

![Usługa Azure ATP powitalnej etap 1](media/directory-services.png)

> [!IMPORTANT]
> Poświadczenia użytkownika w tym miejscu musi być na koncie użytkownika w usłudze Active Directory w środowisku lokalnym. 


1.  Wprowadź następujące informacje i kliknij przycisk **Zapisz**:

    |Pole|Komentarze|
    |---------|------------|
    |**Nazwa użytkownika** (wymagana)|Wprowadź tylko do odczytu usługi Active Directory nazwę użytkownika, na przykład: **ATPuser**.|
    |**Hasło** (wymagane)|Wprowadź hasło użytkownika tylko do odczytu, na przykład: **Rysik1**.|
    |**Domena** (wymagana)|Wprowadź domenę użytkownika tylko do odczytu, na przykład: **contoso.com**. **Uwaga:** należy wprowadzić pełną nazwę FQDN domeny, w której znajduje się użytkownik. Na przykład jeśli konto użytkownika znajduje się w domenie corp.contoso.com, należy wprowadzić `corp.contoso.com` not contoso.com|

3. W portalu usługi Azure ATP kliknij **Pobierz instalatora czujnika i zainstaluj pierwszy czujnik** aby kontynuować.


> [!div class="step-by-step"]
> [« Krok 1](install-atp-step1.md)
> [Krok 3 »](install-atp-step3.md)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)