---
title: Rozwiązywanie problemów z narzędzia Azure ATP znane problemy dotyczące | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak można rozwiązywać problemy w usłudze Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a56845c619e93ed2fae0e10876a4d49a49e23e7d
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166307"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="troubleshooting-azure-atp-known-issues"></a>Rozwiązywanie problemów z usługi Azure ATP znane problemy 


## <a name="deployment-log-location"></a>Lokalizacja dziennika wdrażania
 
Dzienniki wdrożenia usługi Azure ATP znajdują się w katalogu tymczasowym użytkownika, który zainstalował produkt. W domyślnej lokalizacji instalacji można znaleźć w: C:\Users\Administrator\AppData\Local\Temp (lub w katalogu % temp %). Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z zaawansowanej ochrony przed zagrożeniami przy użyciu dzienników](troubleshooting-atp-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-licensing-error"></a>Problem z uwierzytelnianiem proxy przedstawia jako błąd licencjonowania

Podczas instalacji czujnika zostanie wyświetlony następujący błąd: **czujnika nie powiodło się zarejestrowanie ze względu na problemy z licencjonowaniem.**

Wpisy dziennika wdrażania: [1C 60: 1AA8] [2018-03-24T23:59:13] i000: 2018-03-25 02:59:13.1237 InteractiveDeploymentManager ValidateCreateSensorAsync informacje zwrócone [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 c 60 : 1AA8] [2018-03 — 24T23:59:56] i000: 02:59:56.4856 2018-03-25 InteractiveDeploymentManager ValidateCreateSensorAsync informacje zwrócone [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 C 60: 1AA8] [2018-03-25T00:27:56] i000: 2018-03-25 03:27:56.7399 debugowania SensorBootstrapperApplication Engine.Quit [\[] deploymentResultStatus = 1602 isRestartRequired = False [\]] [1 C 60: 15B8] [2018-03-25T00:27:56] i500: zamknięcia systemu, kod zakończenia: 0x642


**Przyczyna:**

W niektórych przypadkach podczas komunikowania się za pośrednictwem serwera proxy podczas uwierzytelniania go może odpowiadać czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure z powodu błędu 401 lub 403 zamiast błędu 407. Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure interpretują błąd 401 lub 403 jako licencjonowania problem, a nie problemu uwierzytelniania serwera proxy. 

**Rozwiązanie:**

Upewnij się, że czujnik przejść do *. atp.azure.com przez skonfigurowany serwer proxy bez uwierzytelniania. Aby uzyskać więcej informacji, zobacz [skonfigurować serwer proxy w celu umożliwienia komunikacji](configure-proxy.md).




## Usługa Azure czujnika zaawansowanej ochrony przed zagrożeniami problem tworzenia zespołu kart interfejsu Sieciowego <a name="nic-teaming"></a>

Jeśli spróbujesz zainstalować czujnika zaawansowanej ochrony przed zagrożeniami na maszynie skonfigurowane z kartą zespołu kart interfejsu Sieciowego, wystąpi błąd instalacji. Jeśli chcesz zainstalować czujnika zaawansowanej ochrony przed zagrożeniami na maszynie skonfigurowany z kart sieciowych, wykonaj te instrukcje:

Jeśli nie został jeszcze zainstalowany czujnik:

1.  Pobierz Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Odinstaluj WinPcap, jeśli została zainstalowana.
3.  Instalowanie Npcap przy użyciu następujących opcji: loopback_support = no & winpcap_mode = tak
4.  Zainstaluj pakiet czujnika.

Jeśli zainstalowano już czujnika:

1.  Pobierz Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Odinstaluj czujnika.
3.  Odinstaluj WinPcap.
4.  Instalowanie Npcap przy użyciu następujących opcji: loopback_support = no & winpcap_mode = tak
5.  Zainstaluj ponownie pakiet czujnika.

## <a name="windows-defender-atp-integration-issue"></a>Problem z integracją usługi Windows Defender ATP

Usługa Azure Advanced Threat Protection umożliwia Integrowanie usługi Azure ATP z usługi Windows Defender ATP. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problem czujnik maszyn wirtualnych VMware

Jeśli masz czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure na maszynach wirtualnych VMware, może zostać wyświetlony alert monitorowania **część ruchu sieciowego nie jest analizowana**. Dzieje się tak z powodu niezgodności konfiguracji w programie VMware.

Aby rozwiązać ten problem:

Skonfigurować następujące ustawienia, **0** lub **wyłączone** w konfiguracji interfejsu Sieciowego maszyny wirtualnej: TsoEnable, LargeSendOffload, TSO Offload, Odciążanie TSO przychodzące.
> [!NOTE]
> Dla usługi Azure ATP czujników, konieczne jest wyłączenie **Odciążanie TSO IPv4** w obszarze Konfiguracja karty Sieciowej.

 ![Problem z czujnikiem VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)