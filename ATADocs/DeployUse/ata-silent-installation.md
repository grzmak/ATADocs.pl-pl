---
title: "Instalowanie usługi ATA w trybie dyskretnym | Usługa Microsoft Advanced Threat Analytics"
description: "Temat opisuje sposób instalacji usługi ATA w trybie dyskretnym."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 2e51bc9cac43ff90000ca74cccd158e119cc6ec0


---

# Instalacja usługi ATA w trybie dyskretnym
Ten artykuł zawiera instrukcje dotyczące instalowania usługi ATA w trybie dyskretnym.
## Wymagania wstępne

Usługa Microsoft ATA w wersji 1.6 wymaga zainstalowania programu Microsoft .NET Framework w wersji 4.6.1. 

W przypadku instalacji lub aktualizacji usługi ATA platforma .Net Framework 4.6.1 zostanie automatycznie zainstalowana jako część wdrożenia usługi Microsoft ATA.

> [!Note] 
> Instalacja platformy .Net Framework 4.6.1 może wymagać ponownego uruchomienia serwera. Podczas instalowania bramy usługi ATA na kontrolerach domeny warto pomyśleć o zaplanowaniu okna obsługi dla tych kontrolerów domeny.
W przypadku użycia dyskretnej metody instalacji usługi ATA instalator jest skonfigurowany tak, aby automatycznie uruchomić ponownie serwer na końcu instalacji (w razie potrzeby). Aby uniknąć ponownego uruchomienia serwera w ramach instalacji, użyj flagi `-NoRestart`. W sytuacji, w której użyto flagi `-NoRestart` i wymaga się ponownego uruchomienia serwera w ramach instalacji, instalator wstrzyma pracę aż do ponownego uruchomienia serwera. Aby śledzić postępy wdrażania, monitoruj dzienniki instalatora usługi ATA, które znajdują się w folderze **%AppData%\Local\Temp**.


## Instalowanie centrum usługi ATA

Użyj poniższego polecenia, aby zainstalować centrum usługi ATA:

**Składnia**:

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**Opcje instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|NoRestart|/norestart|Nie|Pomija wszelkie próby ponownego uruchomienia. Domyślnie interfejs użytkownika wyświetla monit przed ponownym uruchomieniem.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Tak|Wskazuje, że licencja została przeczytana i zatwierdzona. Parametr musi być ustawiony w przypadku instalacji dyskretnej.|

**Parametry instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=“<InstallPath>”|Nie|Ustawia ścieżkę instalacji plików binarnych usługi ATA. Domyślna ścieżka to C:\Program Files\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|Nie|Ustawia ścieżkę folderu danych bazy danych usługi ATA. Domyślna ścieżka to C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Tak|Ustawia adres IP centrum usługi ATA.|
|CenterPort|CenterPort=<CenterPort>|Tak|Ustawia port sieciowy centrum usługi ATA.|
|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|Nie|Ustawia odcisk palca certyfikatu dla centrum usługi ATA. Ten certyfikat jest wykorzystywany do zabezpieczenia komunikacji między centrum usługi ATA i bramą usługi ATA. Jeśli parametr jest nieustawiony, instalacja wygeneruje certyfikat z podpisem własnym.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Tak|Ustawia adres IP konsoli usługi ATA.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=”<CertThumbprint >”|Nie|Określa odcisk palca certyfikatu dla konsoli usługi ATA. Ten certyfikat jest wykorzystywany do sprawdzania tożsamości witryny konsoli usługi ATA. Jeśli nie jest określony, instalacja wygeneruje certyfikat z podpisem własnym.|

**Przykłady**: aby zainstalować centrum usługi ATA przy użyciu domyślnych ścieżek instalacji i pojedynczego adresu IP:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Aby zainstalować centrum usługi ATA przy użyciu domyślnych ścieżek instalacji, dwóch adresów IP i odcisków palców certyfikatów zdefiniowanych przez użytkownika:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## Zaktualizuj centrum usługi ATA

Użyj poniższego polecenia, aby zaktualizować centrum usługi ATA:

**Składnia**:

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**Opcje instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|NoRestart|/norestart|Nie|Pomija wszelkie próby ponownego uruchomienia. Domyślnie interfejs użytkownika wyświetla monit przed ponownym uruchomieniem.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|


Podczas aktualizowania usługi ATA instalator automatycznie wykrywa, czy usługa ATA jest już zainstalowana na serwerze i czy nie wymaga się zastosowania aktualizacji instalacji.

**Przykłady**: aby zaktualizować centrum usługi ATA w trybie dyskretnym. W dużych środowiskach aktualizacja centrum usługi ATA może wymagać trochę czasu. Monitoruj dzienniki usługi ATA, aby śledzić postępy aktualizacji.

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## Odinstalowywanie centrum usługi ATA w trybie dyskretnym

Aby przeprowadzić odinstalowywanie centrum usługi ATA w trybie dyskretnym, użyj następującego polecenia: **Składnia**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**Opcje instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia dezinstalator bez interfejsu użytkownika i bez monitów.|
|Odinstaluj|/uninstall|Tak|Uruchamia odinstalowywanie centrum usługi ATA z serwera w trybie dyskretnym.|
|NoRestart|/norestart|Nie|Pomija wszelkie próby ponownego uruchomienia. Domyślnie interfejs użytkownika wyświetla monit przed ponownym uruchomieniem.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|

**Parametry instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Nie|Usuwa wszystkie pliki z istniejącej bazy danych.|

**Przykłady**: aby odinstalować centrum usługi ATA z serwera w trybie dyskretnym, usuwając wszystkie istniejące dane z bazy danych:


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## Instalacja bramy usługi ATA w trybie dyskretnym
Użyj poniższego polecenia, aby zainstalować bramę usługi ATA w trybie dyskretnym:

**Składnia**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**Opcje instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|NoRestart|/norestart|Nie|Pomija wszelkie próby ponownego uruchomienia. Domyślnie interfejs użytkownika wyświetla monit przed ponownym uruchomieniem.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Tak|Wskazuje, że licencja została przeczytana i zatwierdzona. Parametr musi być ustawiony w przypadku instalacji dyskretnej.|

**Parametry instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|Nie|Ustawia odcisk palca certyfikatu dla centrum usługi ATA. Ten certyfikat jest wykorzystywany do zabezpieczenia komunikacji między centrum usługi ATA i bramą usługi ATA. Jeśli parametr jest nieustawiony, instalacja wygeneruje certyfikat z podpisem własnym.|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Tak|Określa nazwę konta użytkownika (uzytkownik@domena.com), które jest używane do rejestrowania bramy usługi ATA przy użyciu centrum usługi ATA.|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Tak|Określa hasło konta użytkownika (uzytkownik@domena.com), które jest używane do rejestrowania bramy usługi ATA przy użyciu centrum usługi ATA.|

**Przykłady**: aby dyskretnie zainstalować bramę usługi ATA i zarejestrować ją w centrum usługi ATA za pomocą określonych poświadczeń:

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## Aktualizacja bramy usługi ATA

Użyj poniższego polecenia, aby zaktualizować bramę usługi ATA w trybie dyskretnym:

**Składnia**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**Opcje instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|NoRestart|/norestart|Nie|Pomija wszelkie próby ponownego uruchomienia. Domyślnie interfejs użytkownika wyświetla monit przed ponownym uruchomieniem.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|


**Przykłady**: aby zaktualizować bramę usługi ATA w trybie dyskretnym:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## Odinstalowywanie bramy usługi ATA w trybie dyskretnym

Aby przeprowadzić odinstalowywanie bramy usługi ATA w trybie dyskretnym, użyj następującego polecenia: **Składnia**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**Opcje instalacji**:

|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia dezinstalator bez interfejsu użytkownika i bez monitów.|
|Odinstaluj|/uninstall|Tak|Uruchamia odinstalowywanie bramy usługi ATA z serwera w trybie dyskretnym.|
|NoRestart|/norestart|Nie|Pomija wszelkie próby ponownego uruchomienia. Domyślnie interfejs użytkownika wyświetla monit przed ponownym uruchomieniem.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|

**Przykłady**: aby odinstalować bramę usługi ATA z serwera w trybie dyskretnym:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Jun16_HO4-->


