---
title: Instalowanie usługi Advanced Threat Analytics w trybie dyskretnym | Dokumentacja firmy Microsoft
description: Temat opisuje sposób instalacji usługi ATA w trybie dyskretnym.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4083975599985abe5540becb8a8ce580980f1f14
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134062"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*


# <a name="ata-silent-installation"></a>Instalacja usługi ATA w trybie dyskretnym
Ten artykuł zawiera instrukcje dotyczące instalowania usługi ATA w trybie dyskretnym.

## <a name="prerequisites"></a>Wymagania wstępne

Usługa ATA 1.8 wymaga zainstalowania programu Microsoft .NET Framework 4.6.1. 

Podczas instalowania lub aktualizowania usługi ATA, .net Framework 4.6.1 jest automatycznie instalowany jako część wdrożenia program Microsoft ATA.

> [!Note] 
> Instalacja platformy .Net Framework 4.6.1 może wymagać ponownego uruchomienia serwera. Podczas instalowania bramy usługi ATA na kontrolerach domeny warto pomyśleć o zaplanowaniu okna obsługi dla tych kontrolerów domeny.
W przypadku użycia dyskretnej metody instalacji usługi ATA instalator jest skonfigurowany tak, aby automatycznie uruchomić ponownie serwer na końcu instalacji (w razie potrzeby). Z powodu usterki Instalatora Windows norestart nie można niezawodnie użyć flagi do upewnij się, że serwer nie jest ponownie uruchamiany, dlatego upewnij się, że jest uruchamiana tylko instalacja dyskretna podczas okna obsługi.

Aby śledzić postępy wdrażania, Monitoruj dzienniki Instalatora usługi ATA, które znajdują się w **%AppData%\Local\Temp**.


## <a name="install-the-ata-center"></a>Instalowanie centrum usługi ATA

Użyj poniższego polecenia, aby zainstalować centrum usługi ATA:

**Składnia**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint="<CertThumbprint>"] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint="<CertThumbprint >"]
    
**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Tak|Wskazuje, że licencja została przeczytana i zatwierdzona. Parametr musi być ustawiony w przypadku instalacji dyskretnej.|

**Parametry instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath="<InstallPath>"|Nie|Ustawia ścieżkę instalacji plików binarnych usługi ATA. Domyślna ścieżka to C:\Program Files\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath="<DBPath>"|Nie|Ustawia ścieżkę folderu danych bazy danych usługi ATA. Domyślna ścieżka to C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Tak|Ustawia adres IP centrum usługi ATA.|
|CenterPort|CenterPort=<CenterPort>|Tak|Ustawia port sieciowy centrum usługi ATA.|
|CenterCertificateThumbprint|CenterCertificateThumbprint="<CertThumbprint>"|Nie|Ustawia odcisk palca certyfikatu dla centrum usługi ATA. Ten certyfikat jest wykorzystywany do zabezpieczenia komunikacji między centrum usługi ATA i bramą usługi ATA. W przeciwnym razie zestawu, instalacja wygeneruje certyfikat z podpisem własnym.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Tak|Ustawia adres IP konsoli usługi ATA.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint="<CertThumbprint >"|Nie|Określa odcisk palca certyfikatu dla konsoli usługi ATA. Ten certyfikat jest używany do sprawdzania tożsamości witryny konsoli usługi ATA. Jeśli nie zostanie określony, instalacja wygeneruje certyfikat z podpisem własnym|

**Przykłady**: aby zainstalować centrum usługi ATA przy użyciu domyślnych ścieżek instalacji i pojedynczego adresu IP:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Aby zainstalować centrum usługi ATA przy użyciu domyślnych ścieżek instalacji, dwóch adresów IP i odcisków palców certyfikatów zdefiniowanych przez użytkownika:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint="G9530253C976BFA9342FD1A716C0EC94207BFD5A"

## <a name="update-the-ata-center"></a>Zaktualizuj centrum usługi ATA

Użyj poniższego polecenia, aby zaktualizować centrum usługi ATA:

**Składnia**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|


Podczas aktualizowania usługi ATA instalator automatycznie wykrywa, czy usługa ATA jest już zainstalowana na serwerze i czy nie wymaga się zastosowania aktualizacji instalacji.

**Przykłady**: aby zaktualizować centrum usługi ATA w trybie dyskretnym. W dużych środowiskach aktualizacja centrum usługi ATA może wymagać trochę czasu. Monitoruj dzienniki usługi ATA, aby śledzić postępy aktualizacji.

        "Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-center-silently"></a>Odinstalowywanie centrum usługi ATA w trybie dyskretnym

Aby przeprowadzić odinstalowywanie centrum usługi ATA w trybie dyskretnym, użyj następującego polecenia: **Składnia**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/Help]
     [--DeleteExistingDatabaseData]

**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia dezinstalator bez interfejsu użytkownika i bez monitów.|
|Odinstaluj|/uninstall|Tak|Uruchamia odinstalowywanie centrum usługi ATA z serwera w trybie dyskretnym.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|

**Parametry instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Nie|Usuwa wszystkie pliki z istniejącej bazy danych.|

**Przykłady**: aby odinstalować centrum usługi ATA z serwera w trybie dyskretnym, usuwając wszystkie istniejące dane z bazy danych:


    "Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData

## <a name="ata-gateway-silent-installation"></a>Instalacja bramy usługi ATA w trybie dyskretnym

> [!NOTE]
> Wdrażając dyskretnie bramy ATA Lightweight Gateway, za pomocą programu System Center Configuration Manager lub innym systemem wdrażania oprogramowania, zalecane jest tworzenie dwa pakiety wdrażania:</br>-Net Framework 4.6.1 w tym ponowny rozruch kontrolera domeny</br>— Brama usługi ATA. </br>Wprowadź pakiet bramy usługi ATA zależy od wdrożenia programu .net Framework wdrożenia pakietu. </br>Pobierz [.Net Framework 4.6.1 wdrożenie w trybie offline pakietu](https://www.microsoft.com/download/details.aspx?id=49982). 


Użyj poniższego polecenia, aby zainstalować bramę usługi ATA w trybie dyskretnym:

**Składnia**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [ConsoleAccountName="<AccountName>"] 
    [ConsoleAccountPassword="<AccountPassword>"]

> [!NOTE]
> Jeśli pracujesz na komputerze przyłączonym do domeny i logowanie zostało wykonane za pomocą nazwy użytkownika i hasła administratora usługi ATA, nie trzeba podawać poświadczeń w tym miejscu.


**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|

**Parametry instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|ConsoleAccountName|ConsoleAccountName="<AccountName>"|Tak|Określa nazwę konta użytkownika (user@domain.com), które jest używane do rejestrowania bramy usługi ATA przy użyciu centrum usługi ATA.|
|ConsoleAccountPassword|ConsoleAccountPassword="<AccountPassword>"|Tak|Określa hasło konta użytkownika (user@domain.com), które jest używane do rejestrowania bramy usługi ATA przy użyciu centrum usługi ATA.|

**Przykłady**: aby dyskretnie zainstalować bramę usługi ATA, zaloguj się do domeny przyłączone do komputera przy użyciu poświadczeń administratora usługi ATA, dzięki czemu nie musisz określić poświadczenia, jako część instalacji. W przeciwnym razie zarejestruj ją w centrum usługi ATA za pomocą podanych poświadczeń:

    "Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
    

## <a name="update-the-ata-gateway"></a>Aktualizacja bramy usługi ATA

Użyj poniższego polecenia, aby zaktualizować bramę usługi ATA w trybie dyskretnym:

**Składnia**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|


**Przykłady**: aby zaktualizować bramę usługi ATA w trybie dyskretnym:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-gateway-silently"></a>Odinstalowywanie bramy usługi ATA w trybie dyskretnym

Aby przeprowadzić odinstalowywanie bramy usługi ATA w trybie dyskretnym, użyj następującego polecenia: **Składnia**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia dezinstalator bez interfejsu użytkownika i bez monitów.|
|Odinstaluj|/uninstall|Tak|Uruchamia odinstalowywanie bramy usługi ATA z serwera w trybie dyskretnym.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|

**Przykłady**: aby odinstalować bramę usługi ATA z serwera w trybie dyskretnym:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## <a name="see-also"></a>Zobacz też

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)