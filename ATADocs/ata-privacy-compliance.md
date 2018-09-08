---
title: Advanced Threat Analytics danych osobowych zasad | Dokumentacja firmy Microsoft
description: Zawiera łącza do informacji o sposobie usuwania informacji prywatnych, jak i dane osobiste z usługi ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: ae5a28f793abe74331e58e92f2cbc2e021f772ea
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126324"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*

# <a name="ata-data-security-and-privacy"></a>Bezpieczeństwo danych usługi ATA i ochrona prywatności

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Wyszukiwanie i identyfikowanie danych osobowych 

Wszystkie dane w usłudze ATA, które odnoszą się do jednostek jest pochodzi z usługi Active Directory (AD) i replikowane do usługi ATA, w tym miejscu. Podczas wyszukiwania danych osobowych, pierwsze miejsce, należy rozważyć, wyszukiwanie jest AD. 

Z Centrum usługi ATA umożliwia wyświetlanie identyfikację danych osobowych, które są przechowywane w bazie danych na pasku wyszukiwania. Użytkownicy mogą wyszukiwać dla określonego użytkownika lub urządzenia. Kliknięcie jednostki spowoduje otwarcie, użytkownika lub strony profilu urządzenia. Profil, który zapewnia kompleksowe szczegóły jednostki, jego historię i działania związane z siecią, pochodzące z usługi AD. 

## <a name="updating-personal-data"></a>Aktualizowanie danych osobowych 

Dane osobowe dotyczące użytkowników i jednostek w usłudze ATA jest tworzony na podstawie użytkownika obiektu w Twojej organizacji przez usługi AD. W związku z tym wszelkie zmiany wprowadzone do profilu użytkownika w AD są odzwierciedlane w usłudze ATA. 

## <a name="deleting-personal-data"></a>Usuwanie danych osobowych 

Mimo że danych w usłudze ATA jest replikowana i zawsze aktualizowane z usługi AD, gdy jednostka zostanie usunięty w AD, dane jednostki w usłudze ATA są obsługiwane na potrzeby badania zabezpieczeń. 

Aby trwale usunąć dane związane z bazy danych usługi ATA, wykonaj poniższą procedurę: 

1. [Pobierz](https://aka.ms/ata-gdpr-script) skryptu bazy danych MongoDB (gdpr.js).  

2. Skopiuj skrypt na komputerze Centrum usługi ATA i uruchom następujące polecenie z poziomu maszyny Centrum usługi ATA: 

Użyj skryptu bazy danych RODO ATA usuwanie jednostek i usunąć dane o aktywności jednostki, zgodnie z opisem w poniższych sekcjach.

### <a name="delete-entities"></a>Usuwanie jednostek

Ta akcja trwale usuwa jednostki z bazy danych usługi ATA. Do uruchomienia tego polecenia, należy podać nazwę polecenia `deleteAccount`i `SamName`, `UpnName` lub `GUID` komputera lub nazwy użytkownika do usunięcia. Przykład: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

Uruchomiony całkowicie usunie jednostki przy użyciu nazwy UPN admin1@contoso.com z bazy danych wraz z wszystkich działań i alertów zabezpieczeń skojarzony z jednostką. 

### <a name="delete-entity-activity-data"></a>Usuń dane o aktywności jednostki

Ta akcja trwale usuwa danych dotyczących jednostki działań związanych z bazy danych usługi ATA. Wszystkie jednostki będą ulegną zmianie, ale działań i alertów zabezpieczeń z nimi związane, dla określonego przedziału czasu są usuwane. 

Do uruchomienia tego polecenia, należy podać nazwę polecenia `deleteOldData`oraz liczbę dni, które chcesz przechowywać w bazie danych. 

Przykład: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

Ten skrypt powoduje usunięcie wszystkich danych, dla wszystkich jednostek działań i alertów zabezpieczeń z bazy danych, które są starsze niż 30 dni. Zostanie zachowana tylko ostatnich 30 dni danych.

## <a name="exporting-personal-data"></a>Eksportowanie danych osobowych 

Ponieważ dane powiązane z jednostkami w usłudze ATA jest tworzony na podstawie usługi AD, tylko podzbiór tych danych są przechowywane w bazie danych usługi ATA. Z tego powodu należy wyeksportować dane dotyczące jednostki z usługi AD. 

Usługa ATA umożliwia eksportowanie do programu Excel wszystkie informacje związane z zabezpieczeniami, które mogą zawierać dane osobowe. 

 
## <a name="opt-out-of-system-generated-logs"></a>Zrezygnować z dzienników generowanych przez system 

Usługa ATA zbiera anonimowe dzienniki generowane przez system — informacje dla każdego wdrożenia i przekazuje te dane przy użyciu protokołu HTTPS do serwerów firmy Microsoft. Te dane są używane przez firmę Microsoft w celu ulepszania przyszłych wersji usługi ATA. 

Aby uzyskać więcej informacji, zobacz [Zarządzanie dzienniki generowane przez system](manage-telemetry-settings.md).

Aby wyłączyć zbieranie danych:

1. Zaloguj się do konsoli usługi ATA, kliknij wielokropek na pasku narzędzi, a następnie wybierz pozycję **Informacje**. 
2. Usuń zaznaczenie pola **Wysyłaj do nas informacje o użyciu w celu ulepszenia środowiska klienta w przyszłości**. 

## <a name="additional-resources"></a>Dodatkowe zasoby

- Aby uzyskać informacji na temat usługi ATA, zaufania i zgodność, zobacz [portal zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) i [witryny Microsoft 365 Enterprise RODO zgodności](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
