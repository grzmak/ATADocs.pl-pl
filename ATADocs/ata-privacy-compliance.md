---
title: Advanced Threat Analytics danych osobowych zasad | Dokumentacja firmy Microsoft
description: Zawiera linki do informacji na temat sposobu usuwania prywatne informacje i dane osobowe z usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: cf08f2d46eaa939f414d1e3793446384cd22100b
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*

# <a name="ata-data-security"></a>Bezpieczeństwo danych usługi ATA 

Aby uzyskać informacje dotyczące zaufania usługi ATA i zgodności, zobacz [portal usługi zaufania](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) i [witryny Microsoft 365 Enterprise GDPR zgodności](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

## <a name="searching-for-and-identifying-personal-data"></a>Wyszukiwanie i zidentyfikowaniu danych osobowych 

Wszystkie dane w usłudze ATA, które odnoszą się do jednostek jest pochodzące z usługi Active Directory (AD) i replikowane do usługi ATA z tego miejsca. Podczas wyszukiwania danych osobowych, pierwsze miejsce, należy rozważyć wyszukiwanie jest AD. 

Z Centrum usługi ATA umożliwia wyświetlanie osobistych danych umożliwiających identyfikację użytkownika, który jest przechowywany w bazie danych na pasku wyszukiwania. Użytkownicy mogą przeszukiwać dla określonego użytkownika lub urządzenia. Kliknięcie jednostki spowoduje otwarcie, użytkownika lub urządzenia strony profilu. Profil zapewnia kompleksowe szczegóły jednostki, jego historię i działania związane z siecią pochodzące z usługi Active Directory. 

## <a name="updating-personal-data"></a>Aktualizowanie danych osobowych 

Dane osobowe dotyczące użytkowników i jednostek w usłudze ATA pochodzi od użytkownika AD do obiektu w Twojej organizacji. W związku z tym zmiany wprowadzone do profilu użytkownika w usłudze AD są odzwierciedlane w usłudze ATA. 

## <a name="deleting-personal-data"></a>Usuwanie danych osobowych 

> [!NOTE]
> Jeśli interesuje Cię przeglądanie lub usuwanie danych osobowych, przejrzyj wskazówki firmy Microsoft w [Menedżer zgodności Microsoft](https://servicetrust.microsoft.com/ComplianceManager) w [sekcji GDPR witryny Microsoft 365 Enterprise zgodności] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Jeśli szukasz ogólne informacje o GDPR, zobacz [GDPR części portalu zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


Mimo że dane w usłudze ATA są replikowane i zawsze aktualizowane z usługi Active Directory, po usunięciu jednostki w usłudze AD, dane jednostki w usłudze ATA są obsługiwane na potrzeby badania zabezpieczeń. 

Aby trwale usunąć dane związane z bazy danych usługi ATA, wykonaj poniższą procedurę: 

1. [Pobierz](https://aka.ms/ata-gdpr-script) skryptu bazy danych MongoDB (gdpr.js).  

2. Skopiuj skrypt na maszynie Centrum usługi ATA i uruchom następujące polecenie na komputerze Centrum usługi ATA: 

Użyj skryptu bazy danych usługi ATA GDPR do usuwania jednostek i usunąć dane działanie jednostki, zgodnie z opisem w poniższych sekcjach.

### <a name="delete-entities"></a>Usuwanie jednostek

Ta akcja trwale usuwa obiekt z bazy danych usługi ATA. Aby uruchomić to polecenie, podaj nazwę polecenia `deleteAccount`i `SamName`, `UpnName` lub `GUID` komputera lub nazwy użytkownika do usunięcia. Przykład: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteAccount,admin1@contoso.com;” GDPR.js `

Uruchamianie to całkowicie usuwa jednostki nazwy UPN admin1@contoso.com z bazy danych wraz z działaniami i alerty zabezpieczeń skojarzonego z jednostką. 

### <a name="delete-entity-activity-data"></a>Usuń dane działanie jednostki

Ta akcja trwale usuwa z bazy danych usługi ATA dane działań jednostki. Wszystkie jednostki zostanie uległy zmianie, ale działań i powiązane z nimi dla określonego przedziału czasu alerty zabezpieczeń są usuwane. 

Aby uruchomić to polecenie, podaj nazwę polecenia `deleteOldData`oraz liczbę dni, które mają być zachowane w bazie danych. 

Przykład: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteOldData,30;” GDPR.js`

Ten skrypt powoduje usunięcie wszystkich danych dla wszystkich działań jednostki i alertów zabezpieczeń z bazy danych, które są starsze niż 30 dni. Tylko ostatnich 30 dni dane zostaną zachowane.

## <a name="exporting-personal-data"></a>Eksportowanie danych osobowych 

> [!NOTE]
> Jeśli interesuje Cię przeglądanie lub usuwanie danych osobowych, przejrzyj wskazówki firmy Microsoft w [Menedżer zgodności Microsoft](https://servicetrust.microsoft.com/ComplianceManager) w [sekcji GDPR witryny Microsoft 365 Enterprise zgodności] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Jeśli szukasz ogólne informacje o GDPR, zobacz [GDPR części portalu zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


Ponieważ dane powiązane z jednostkami w usłudze ATA pochodzi z usługi Active Directory, tylko podzbiór danych są przechowywane w bazie danych usługi ATA. Z tego powodu należy wyeksportować dane dotyczące jednostki z usługi Active Directory. 

Usługa ATA umożliwia eksportowanie do programu Excel, wszystkie informacje związane z zabezpieczeniami, która może obejmować dane osobowe. 

 
## <a name="opt-out-of-system-generated-logs"></a>Wypisz dzienników generowanych przez system 

> [!NOTE]
> Jeśli interesuje Cię przeglądanie lub usuwanie danych osobowych, przejrzyj wskazówki firmy Microsoft w [Menedżer zgodności Microsoft](https://servicetrust.microsoft.com/ComplianceManager) w [sekcji GDPR witryny Microsoft 365 Enterprise zgodności] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Jeśli szukasz ogólne informacje o GDPR, zobacz [GDPR części portalu zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

ATA zbiera anonimowe generowanych przez system dzienników dotyczących każdego wdrożenia i przesyła te dane przy użyciu protokołu HTTPS do serwerów firmy Microsoft. Te dane są używane przez firmę Microsoft w celu ulepszania przyszłych wersji usługi ATA. 

Aby uzyskać więcej informacji, zobacz [zarządzania dziennikami generowanych przez system](manage-telemetry-settings.md).

Aby wyłączyć zbieranie danych:

1. Zaloguj się do konsoli usługi ATA, kliknij wielokropek na pasku narzędzi, a następnie wybierz pozycję **Informacje**. 
2. Usuń zaznaczenie pola **Wysyłaj do nas informacje o użyciu w celu ulepszenia środowiska klienta w przyszłości**. 

 

 

 

## <a name="additional-resources"></a>Dodatkowe zasoby

[Strona 9 kanału zabezpieczeń firmy Microsoft](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Zasoby społeczności

[Blog usługi ATA](https://aka.ms/ATABlog)
[społeczności ATA](https://aka.ms/ATACommunity)
[Prześlij opinię dotyczącą usługi ATA](https://aka.ms/ATAUserVoice)
