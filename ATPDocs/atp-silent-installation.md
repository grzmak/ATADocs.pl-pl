---
title: Install Azure Zaawansowana ochrona przed zagrożeniami w trybie dyskretnym | Dokumentacja firmy Microsoft
description: Opisuje sposób instalacji w trybie dyskretnym narzędzia Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/7/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b318e4eefe05aee9ab99221d4ccd1e20764047a2
ms.sourcegitcommit: be87b7bf30270a4b8f9886199748bb664274331b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/08/2018
ms.locfileid: "39631637"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="azure-atp-switches-and-silent-installation"></a>Usługa Azure przełączników zaawansowanej ochrony przed zagrożeniami i instalacji dyskretnej
Ten artykuł zawiera wskazówki i instrukcje dotyczące instalacji dyskretnej i przełączniki narzędzia Azure ATP.

## <a name="prerequisites"></a>Wymagania wstępne

Narzędzie Azure ATP wymaga zainstalowania programu Microsoft .NET Framework 4.7. 

Po zainstalowaniu narzędzia Azure ATP, .net Framework 4.7 jest automatycznie instalowany jako część wdrożenia usługi Azure ATP.

> [!IMPORTANT] 
> Upewnij się, że masz najnowszą wersję platformy .net Framework zainstalowanej. Jeśli zainstalowano poprzednią wersję programu .net, usługi Azure ATP instalacji dyskretnej będą zatrzymywane w pętli i nie powiedzie się. 

> [!NOTE] 
> Instalacja programu .net framework 4.7 może wymagać ponownego uruchomienia serwera. Podczas instalacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure na kontrolerach domeny, należy wziąć pod uwagę planowanie okna obsługi dla kontrolerów domeny.
Za pomocą narzędzia Azure ATP instalacji dyskretnej, Instalator jest skonfigurowany do automatycznego ponownego uruchamiania serwera, na końcu instalacji (jeśli jest to konieczne). Upewnij się uruchomić instalację dyskretną tylko podczas okna obsługi. Z powodu usterki Instalatora Windows *norestart* flagi nie można niezawodnie się upewnić, że serwer nie jest ponownie uruchamiany.

Aby śledzić swoje postępy wdrażania, Monitoruj dzienniki Instalatora usługi Azure ATP, które znajdują się w **%AppData%\Local\Temp**.



## <a name="azure-atp-sensor-silent-installation"></a>Usługa Azure instalacji dyskretnej czujnika zaawansowanej ochrony przed zagrożeniami

> [!NOTE]
> Wdrażając dyskretnie czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure za pomocą programu System Center Configuration Manager lub innym systemem wdrażania oprogramowania, zalecane jest tworzenie dwa pakiety wdrażania:</br>-Net Framework 4.7 tym ponowny rozruch kontrolera domeny</br>— Platforma azure czujnika zaawansowanej ochrony przed zagrożeniami. </br>Wprowadź pakietu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure zależy od wdrożenia programu .net Framework wdrożenia pakietu. </br>Pobierz [.Net Framework 4.7 wdrożenie w trybie offline pakietu](https://www.microsoft.com/download/details.aspx?id=49982). 


Użyj następującego polecenia do wykonania w pełni dyskretnej instalacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure:


**Składnia**:

    Azure ATP sensor Setup.exe /AccessKey=<Access Key> /quiet NetFrameworkCommandLineArguments ="/q" 
   

> [!NOTE]
> Skopiuj klucz dostępu z portalem obszarów roboczych w obszarze **konfiguracji** i następnie **czujnika**.


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
|accessKey|AccessKey = "\*\*"|Tak|Ustawia klucz dostępu, który służy do rejestrowania czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure z obszarem roboczym usługi Azure ATP.|

**Przykłady**: do przeprowadzenia instalacji dyskretnej czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, zaloguj się do domeny przyłączone do komputera przy użyciu poświadczeń administratora usługi Azure ATP, dzięki czemu nie musisz określić poświadczenia, jako część instalacji. W przeciwnym razie zarejestruj je przy użyciu narzędzia Azure ATP usługi w chmurze przy użyciu określonych poświadczeń:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Aktualizacja czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure

Aby dyskretnie zaktualizować czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, użyj następującego polecenia:

**Składnia**:

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku instalacji dyskretnej?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia instalator bez interfejsu użytkownika i bez monitów.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Tak|Określa parametry dla instalacji programu .Net Framework. Parametr musi być ustawiony w celu wymuszenia instalacji dyskretnej programu .Net Framework.|


**Przykłady**: Aby zaktualizować czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure w trybie dyskretnym:

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Odinstalowywanie czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure w trybie dyskretnym

Użyj następującego polecenia, aby przeprowadzić odinstalowywanie dyskretnej czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure: **składni**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Opcje instalacji**:

> [!div class="mx-tableFixed"]
|Nazwa|Składnia|Obowiązkowy element w przypadku odinstalowywania w trybie dyskretnym?|Opis|
|-------------|----------|---------|---------|
|Quiet|/quiet|Tak|Uruchamia dezinstalator bez interfejsu użytkownika i bez monitów.|
|Odinstaluj|/uninstall|Tak|Uruchamianie odinstalowywania w trybie dyskretnym, czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure z poziomu serwera.|
|Pomoc|/help|Nie|Zapewnia pomoc i szybki dostęp do informacji. Wyświetla prawidłowe użycie poleceń instalatora, łącznie z listą wszystkich opcji i zachowań.|

**Przykłady**: aby dyskretnie odinstalować czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure z serwera:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Zobacz też

- [Konfigurowanie składnika przesyłanie dalej zdarzeń](configure-event-forwarding.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
