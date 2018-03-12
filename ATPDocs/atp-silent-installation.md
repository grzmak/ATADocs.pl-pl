---
title: "Zainstaluj Azure Zaawansowana ochrona przed zagrożeniami w trybie dyskretnym | Dokumentacja firmy Microsoft"
description: "Opisuje sposób instalacji dyskretnej Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f27020f1b4a5fa7aa8fefbda28eac0c2ad6c64d0
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2018
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="azure-atp-silent-installation"></a>Azure instalacji dyskretnej ATP
Ten artykuł zawiera instrukcje dotyczące instalowania w trybie dyskretnym Azure ATP.

## <a name="prerequisites"></a>Wymagania wstępne

Azure ATP wymaga zainstalowania programu Microsoft .NET Framework 4.7. 

Po zainstalowaniu Azure ATP .net Framework 4.7 jest automatycznie instalowany jako część wdrożenia Azure ATP.

> [!IMPORTANT] 
> Upewnij się, że masz najnowszą wersję platformy .net Framework zainstalowana. Jeśli jest zainstalowana poprzednia wersja programu .net, instalacji dyskretnej Azure ATP będą zatrzymywane w pętli i uniemożliwić instalację. 

> [!NOTE] 
> Instalacja programu .net framework 4.7 może wymagać ponownego uruchomienia serwera. Instalując czujnik Azure ATP na kontrolerach domeny warto pomyśleć o zaplanowaniu okna obsługi dla tych kontrolerów domeny.
Korzystając z metody instalacji dyskretnej Azure ATP, Instalator jest skonfigurowany do automatycznego ponownego uruchamiania serwera po zakończeniu instalacji (Jeśli to konieczne). Z powodu błędu Instalatora Windows *norestart* flagi nie można niezawodnie do upewnij się, że serwer zostanie ponownie uruchomiony, dlatego upewnij się, że tylko uruchamiania instalacji dyskretnej w oknie obsługi.

Aby śledzić postępy wdrażania, Monitoruj dzienniki Instalatora Azure ATP, które znajdują się w **%AppData%\Local\Temp**.



## <a name="azure-atp-sensor-silent-installation"></a>Azure instalacji dyskretnej czujnik ATP

> [!NOTE]
> Wdrażając dyskretnie czujnik Azure ATP za pomocą programu System Center Configuration Manager lub inny system wdrożenia oprogramowania, zalecane jest tworzenie dwa pakiety wdrożeniowe:</br>-Net Framework 4.7 tym ponowny rozruch kontrolera domeny</br>-Czujnik ATP azure. </br>Skonfiguruj pakiet czujnik Azure ATP zależał od wdrożenia programu .net Framework wdrożenia pakietu. </br>Pobierz [.Net Framework 4.7 pakietu wdrożeniowego w trybie offline](https://www.microsoft.com/download/details.aspx?id=49982). 


Do przeprowadzenia instalacji dyskretnej czujnik Azure ATP, użyj następującego polecenia:

**Składnia**:

    Azure ATP sensor Setup.exe [/AccessKey=<Access Key>] [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
   

> [!NOTE]
> Kopiowanie klucza dostępu z portalu obszar roboczy w obszarze **konfiguracji** , a następnie **czujnik**.


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
|AccessKey|AccessKey="**"|Tak|Ustawia klawisz dostępu, który służy do rejestrowania czujnik Azure ATP z obszaru roboczego Azure ATP.|

**Przykłady**: do przeprowadzenia instalacji dyskretnej czujnik Azure ATP, zaloguj się do domeny przyłączony komputer przy użyciu poświadczeń administratora Azure ATP, dzięki czemu nie trzeba określić poświadczenia w ramach instalacji. W przeciwnym razie Zarejestruj go z usługą w chmurze Azure ATP przy użyciu określonych poświadczeń:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Aktualizacja czujnik Azure ATP

Użyj następującego polecenia w trybie dyskretnym zaktualizować czujnik Azure ATP:

**Składnia**:

    Azure ATP  sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|


**Przykłady**: Aby zaktualizować czujnik Azure ATP w trybie dyskretnym:

        Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Odinstalowywanie czujnika Azure ATP w trybie dyskretnym

Użyj następującego polecenia, aby przeprowadzić odinstalowywanie dyskretnej czujnika Azure ATP: **składni**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia dezinstalator bez interfejsu użytkownika i bez monitów.|
|Odinstaluj|/uninstall|Tak|Uruchamia odinstalowywania w trybie dyskretnym czujnika Azure ATP z serwera.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|

**Przykłady**: aby dyskretnie odinstalować czujnik Azure ATP z serwera:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Zobacz też

- [Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)