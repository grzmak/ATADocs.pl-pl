---
title: Rozwiązywanie problemów z ATP Azure znane problemy | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak można rozwiązywać problemy w programie Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c430ec58c197c8fcc6e539d0923278cd8469987d
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/30/2018
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Rozwiązywanie problemów z Azure ATP znane problemy 


## <a name="deployment-log-location"></a>Lokalizacja dziennika wdrażania
 
Dzienniki wdrożenia Azure ATP znajdują się w katalogu tymczasowym użytkownika, który zainstalował produkt. W domyślnej lokalizacji instalacji można znaleźć w folderze: C:\Users\Administrator\AppData\Local\Temp (lub w katalogu nadrzędnym % temp %).

## <a name="proxy-authentication-problem-presents-as-licensing-error"></a>Problem z uwierzytelnianiem proxy przedstawia jako błąd licencjonowania

Podczas instalacji czujnik wyświetlony następujący błąd: **czujnika rejestracja nie powiodła się z powodu licencjonowania.**

Wpisy dziennika wdrażania: [1C 60: 1AA8] [2018-03-24T23:59:13] i000: 02:59:13.1237 2018-03-25 InteractiveDeploymentManager ValidateCreateSensorAsync informacje zwracane [\[] validateCreateSensorResult = LicenseInvalid [\]] [60 1 c : 1AA8] [2018-03-24T23:59:56] i000: zwrócone informacje InteractiveDeploymentManager ValidateCreateSensorAsync 02:59:56.4856 2018-03-25 [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 C 60: 1AA8] [2018-03-25T00:27:56] i000: 03:27:56.7399 2018-03-25 debugowania SensorBootstrapperApplication Engine.Quit [\[] deploymentResultStatus = 1602 isRestartRequired = False [\]] [1 C 60: 15B8] [2018-03-25T00:27:56] i500: zamykanie, kod zakończenia: 0x642


**Przyczyna:**

W niektórych przypadkach podczas komunikacji za pośrednictwem serwera proxy podczas uwierzytelniania go może odpowiadać z powodu błędu 401 lub 403 zamiast błędu 407 czujnika Azure ATP. Czujnik Azure ATP zinterpretuje błąd 401 lub 403 jako licencjonowania problem, a nie problem uwierzytelniania serwera proxy. 

**Rozwiązanie:**

Upewnij się, że czujnika można przejść do *. atp.azure.com przez skonfigurowany serwer proxy bez uwierzytelniania. Aby uzyskać więcej informacji, zobacz [skonfigurować serwer proxy, aby umożliwić komunikację](configure-proxy.md).




## <a name="azure-atp-sensor-nic-teaming-issue"></a>Czujnik ATP Azure problem tworzenia zespołu kart interfejsu Sieciowego

Jeśli spróbujesz zainstalować czujnik ATP na komputerze, który został skonfigurowany z kartą zespołu kart interfejsu sieciowego, zostanie wyświetlony błąd instalacji. Jeśli chcesz zainstalować czujnik ATP na komputerze, który został skonfigurowany z zespołu kart interfejsu sieciowego, wykonaj te instrukcje:

Jeśli nie został jeszcze zainstalowany czujnika:

1.  Pobierz Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Odinstaluj WinPcap, jeśli została zainstalowana.
3.  Zainstaluj Npcap z następującymi opcjami: loopback_support = nie & winpcap_mode = tak
4.  Zainstaluj pakiet czujnika.

Jeśli zainstalowano czujnika:

1.  Pobierz Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Odinstaluj czujnika.
3.  Odinstaluj WinPcap.
4.  Zainstaluj Npcap z następującymi opcjami: loopback_support = nie & winpcap_mode = tak
5.  Ponownie zainstaluj pakiet czujnika.

## <a name="windows-defender-atp-integration-issue"></a>Problem integracji Windows Defender ATP

Azure Advanced Threat Protection umożliwia integrację z Windows Defender ATP Azure ATP. Integracja jest aktualnie włączone, tylko jeśli jesteś klientem Windows Defender ATP prywatnej wersji zapoznawczej. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problem czujnik maszyny wirtualnej VMware

Jeśli masz czujnik Azure ATP na maszynach wirtualnych VMware, zostanie zgłoszony alert monitorowania **ruch w sieci nie jest analizowana**. Dzieje się z powodu niezgodności konfiguracji w środowisku programu VMware.

Aby rozwiązać ten problem:

Ustaw następujące ustawienia **0** lub **wyłączone** w konfiguracji karty Sieciowej maszyny wirtualnej: TsoEnable, LargeSendOffload, odciążania TSO, odciążania TSO bardzo duże.
> [!NOTE]
> Dla czujników Azure ATP, konieczne jest wyłączenie **odciążania TSO IPv4** w obszarze Konfiguracja karty Sieciowej.

 ![Problem czujnik VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Planowanie pojemności Azure w ATP](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)