---
title: "Konfigurowanie serwera proxy lub zapory, aby umożliwić komunikację Azure ATP z czujnika | Dokumentacja firmy Microsoft"
description: "Opisuje sposób skonfigurować zaporę lub serwer proxy, aby umożliwić komunikację między czujniki Azure ATP i usługi w chmurze Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 47fa5ad5d6fb7800c7df4b878d16ec335e2b70e5
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="configure-your-proxy-to-allow-communication-between-azure-atp-sensors-and-the-azure-atp-cloud-service"></a>Skonfiguruj serwer proxy, aby umożliwić komunikację między czujniki Azure ATP i usługi w chmurze Azure ATP

Dla kontrolerów domeny do komunikowania się z usługą w chmurze, należy otworzyć: *. atp.azure.com portu 443 w zapory lub serwera proxy. Konfiguracja musi być na poziomie komputera (= konto komputera), a nie na poziomie konta użytkownika. Można przetestować konfigurację, wykonując następujące czynności:
 
1.  Upewnij się, że **bieżącego użytkownika** ma dostęp do punktu końcowego procesora przy użyciu programu Internet Explorer, przechodząc pod następujący adres URL z kontrolera domeny: https://triprd1wcuse1sensorapi.eastus.cloudapp.azure.com (dla Stanów Zjednoczonych), należy pobrać błąd 503:

 ![Usługa jest niedostępna](/media/service-unavailable.png)
 
2.  Jeśli nie wystąpi błąd 503, sprawdź konfigurację serwera proxy i spróbuj ponownie.

3.  Jeśli konfiguracja serwera proxy działa w przypadku **CURRENT_USER** (to znaczy, możesz zobaczyć błąd 503) następnie sprawdź, czy ustawienia serwera proxy WinInet są włączone dla **LOCAL_SYSTEM** konto (używane przez updater czujnik Usługa), uruchamiając następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień:
 
    reg porównania "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet zaawansowane\Połączenia" "HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet zaawansowane\Połączenia" /v DefaultConnectionSettings

Jeśli zostanie wyświetlony błąd "Błąd: system nie może odnaleźć określonego klucza rejestru lub wartość." oznacza to, że ustawiono żadnego serwera proxy na **LOCAL_SYSTEM** poziom
 
 ![Błąd systemu lokalnego serwera proxy](/media/proxy-local-system-error.png)

Jeśli wynik wynosi "wynik w porównaniu: różne" oznacza to, że serwer proxy jest ustawiony dla **LOCAL_SYSTEM** , ale nie jest taka sama jak **CURRENT_USER**:
 
  ![Porównanie wyników serwera proxy](/media/proxy-result-compared.png)

5.  Jeśli **LOCAL_SYSTEM** nie ma ustawienia serwera proxy poprawne (nie skonfigurowany lub inny niż **CURRENT_USER**), to należy skopiować ustawienia serwera proxy z **CURRENT_ Użytkownik** do **LOCAL_SYSTEM**. Upewnij się, że przed rozpoczęciem wprowadzania zmian wykonaj kopię zapasową tego klucza rejestru:

 Bieżący klucz użytkownika: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings "system lokalny klucz: Settings\Connections\ HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet DefaultConnectionSettings"

 
6.  Wykonaj kroki 4 i 5 dla**Local_Service** konta (jest taka sama jak **Local_System** , ale powinien być S-1-5-19 zamiast S-1-5-18.



## <a name="see-also"></a>Zobacz też
- [Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)