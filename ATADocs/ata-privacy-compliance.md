---
title: Advanced Threat Analytics danych osobowych zasad | Dokumentacja firmy Microsoft
description: Zawiera łącza do informacji o sposobie usuwania informacji prywatnych, jak i dane osobiste z usługi ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 08876085e3fe5d86c8219c6b0ad7beb8c44c700a
ms.sourcegitcommit: 1b23381ca4551a902f6343428d98f44480077d30
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2018
ms.locfileid: "47403237"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*

# <a name="ata-data-security-and-privacy"></a>Bezpieczeństwo danych usługi ATA i ochrona prywatności

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Wyszukiwanie i identyfikowanie danych osobowych 

Wszystkie dane w usłudze ATA, które odnoszą się do indywidualnych osób pochodzą z usługi Active Directory (AD) i są lokalnie replikowane do usługi ATA. Podstawowym repozytorium danych osobowych jest usługa Active Directory. 

Centrum usługi ATA umożliwia wyświetlanie na pasku wyszukiwania danych osobowych, które są przechowywane w bazie danych. Użytkownicy mogą wyszukiwać dane dla określonego użytkownika lub urządzenia. Kliknięcie jednostki spowoduje wyświetlenie danych użytkownika lub strony profilu urządzenia. Profil zapewnia kompleksową informację o użytkowniku, jego historię oraz działania związane z siecią i pochodzące z usługi AD. 

## <a name="updating-personal-data"></a>Aktualizowanie danych osobowych 

Dane osobowe dotyczące użytkowników i jednostek w usłudze ATA są tworzone na podstawie danych użytkownika w AD w twojej organizacji. W efekcie wszelkie zmiany wprowadzone do profilu użytkownika w AD są odzwierciedlane w usłudze ATA. 

## <a name="deleting-personal-data"></a>Usuwanie danych osobowych 

Mimo że dane w usłudze ATA są replikowane i zawsze aktualizowane z usługi AD, to gdy użytkownik zostanie usunięty w AD, jego dane w usłudze ATA są obsługiwane dla potrzeb badania zabezpieczeń. 

Aby trwale usunąć dane związane z bazy danych usługi ATA, wykonaj poniższą procedurę: 

1. [Pobierz](https://aka.ms/ata-gdpr-script) skrypt bazy danych MongoDB (gdpr.js).  

2. Skopiuj skrypt do folderu usługi ATA (znajdujący się w `"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB"` i uruchom następujące polecenie z poziomu maszyny Centrum Usługi ATA: 

Użyj skryptu bazy danych RODO ATA do usuwania jednostek i usuń dane o aktywności jednostki, zgodnie z opisem w poniższych sekcjach.

### <a name="delete-entities"></a>Usuwanie jednostek

Ta akcja trwale usuwa jednostki z bazy danych usługi ATA. Do uruchomienia tego polecenia, należy podać nazwę polecenia `deleteAccount`i `SamName`, `UpnName` lub `GUID` komputera lub nazwy użytkownika do usunięcia. Przykład: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

Uruchomiony skrypt całkowicie usunie jednostki przy użyciu nazwy UPN admin1@contoso.com z bazy danych wraz z wszystkimi działaniami i alertami zabezpieczeń skojarzonymi z jednostką. 

### <a name="delete-entity-activity-data"></a>Usuń dane o aktywności jednostki

Ta akcja trwale usuwa dane dotyczące działań jednostki z bazy danych usługi ATA. Jednostki nie ulegają zmianie, podczas gdy ich działania i alerty zabezpieczeń z nimi związane są usuwane dla zadanego okresu czasu. 

Do uruchomienia tego polecenia, należy podać nazwę polecenia `deleteOldData`oraz liczbę dni, które chcesz przechowywać w bazie danych. 

Przykład: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

Ten skrypt powoduje usunięcie wszystkich danych, dla wszystkich jednostek działań i alertów zabezpieczeń z bazy danych, które są starsze niż 30 dni. Zostanie zachowane tylko ostatnich 30 dni danych.

## <a name="exporting-personal-data"></a>Eksportowanie danych osobowych 

Ponieważ dane powiązane z jednostkami w usłudze ATA są tworzone na podstawie usługi AD, tylko podzbiór tych danych jest przechowywany w bazie danych usługi ATA. Z tego powodu należy wyeksportować dane dotyczące jednostki z usługi AD. 

Usługa ATA umożliwia eksportowanie do programu Excel wszystkich, mogących zawierać dane osobowe, informacji związanych z zabezpieczeniami. 

 
## <a name="opt-out-of-system-generated-logs"></a>Rezygnacja z dzienników generowanych przez system 

Usługa ATA zbiera anonimowe dzienniki generowane przez system — informacje dla każdego wdrożenia i przekazuje te dane przy użyciu protokołu HTTPS do serwerów firmy Microsoft. Te dane są używane przez firmę Microsoft w celu ulepszania przyszłych wersji usługi ATA. 

Aby uzyskać więcej informacji, zobacz [Zarządzanie dziennikami generowanymi przez system](manage-telemetry-settings.md).

Aby wyłączyć zbieranie danych:

1. Zaloguj się do konsoli usługi ATA, kliknij wielokropek na pasku narzędzi, a następnie wybierz pozycję **Informacje**. 
2. Usuń zaznaczenie pola **Wysyłaj do nas informacje o użyciu w celu ulepszenia środowiska klienta w przyszłości**. 

## <a name="additional-resources"></a>Dodatkowe zasoby

- Aby uzyskać informacji na temat usługi ATA, zaufania i zgodności, zobacz [portal zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) i [witryny Microsoft 365 Enterprise RODO zgodności](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
