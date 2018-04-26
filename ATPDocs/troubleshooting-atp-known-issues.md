---
title: Rozwiązywanie problemów z ATP Azure znane problemy | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak można rozwiązywać problemy w programie Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2112e9fea1f316ff12d87b3a477b78bff4457a5f
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2018
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Rozwiązywanie problemów z Azure ATP znane problemy 


## <a name="deployment-log-location"></a>Lokalizacja dziennika wdrażania
 
Dzienniki wdrożenia Azure ATP znajdują się w katalogu tymczasowym użytkownika, który zainstalował produkt. W domyślnej lokalizacji instalacji można znaleźć w folderze: C:\Users\Administrator\AppData\Local\Temp (lub w katalogu nadrzędnym % temp %).

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