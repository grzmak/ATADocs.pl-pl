---
title: "Azure instalacji Advanced Threat Protection — krok 4 | Dokumentacja firmy Microsoft"
description: "W kroku 4 instalowania Azure ATP pomaga zainstalować czujnik autonomiczny Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7b003882f21f22b3427fb95534ca2bde255b14e6
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-4"></a>Zainstaluj Azure ATP — krok 4

>[!div class="step-by-step"]
[« Krok 3](install-atp-step3.md)
[Krok 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Krok 4. Zainstaluj czujnik Azure ATP

Przed zainstalowaniem czujnik autonomiczny Azure ATP na dedykowanym serwerze Zweryfikuj, że funkcja dublowania portów jest poprawnie skonfigurowany i czy czujnik autonomiczny Azure ATP widzą ruchu do i z kontrolerów domeny. 


> [!IMPORTANT]
>Upewnij się, że .net Framework 4.7 jest zainstalowany na tym komputerze. Jeśli jest Framework 4.7 .net nie jest zainstalowany pakiet instalacyjny czujnik Azure ATP instaluje go, co wymaga ponownego uruchomienia serwera. Sprawdź, czy komputer ma połączenie z punktem końcowym usługi chmury Azure ATP: https://triprd1wceuw1sensorapi.atp.azure.com (dla Europy) lub https://triprd1wcuse1sensorapi.atp.azure.com (dla Stanów Zjednoczonych).

Wykonaj następujące czynności na serwerze czujnik Azure ATP lub kontrolera domeny.

1.  Wyodrębnij pliki z archiwum zip. 
> [!NOTE] 
> Instalowanie bezpośrednio z pliku zip kończy się niepowodzeniem.

2.  Uruchom **setup.exe czujnik Azure ATP** i postępuj zgodnie z kreatorem.

3.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

     ![Język instalacji czujnik autonomiczny Azure ATP](media/sensor-install-language.png)


4.  Kreator instalacji automatycznie sprawdza, czy serwer jest kontrolerem domeny dedykowanego serwera. Jeśli jest kontrolerem domeny, czujnik Azure ATP jest zainstalowany, jeśli jest dedykowany serwer czujnik autonomiczny Azure ATP jest zainstalowany. 
    
    Na przykład dla czujnika autonomiczny Azure ATP, następujący ekran jest wyświetlany pozwala stwierdzić, że czujnik autonomiczny Azure ATP jest zainstalowana na dedykowanym serwerze:
    
    ![Azure ATP czujnik autonomicznej](media/sensor-install-deployment-type.png)

    Kliknij przycisk **Dalej**.

    > [!NOTE] 
    > Jeśli kontroler domeny lub dedykowany serwer nie spełnia minimalne wymagania sprzętowe dotyczące instalacji, zostanie wyświetlone ostrzeżenie. To nie uniemożliwia kliknięcia przycisku **Dalej** ani kontynuowania instalacji. Może to być odpowiedniej opcji instalacji Azure ATP w środowisku testowym małych laboratorium, w którym nie ma potrzeby tyle samo miejsca do przechowywania danych. W środowiskach produkcyjnych zalecane jest praca z Azure ATP [planowania pojemności](atp-capacity-planning.md) przewodnik upewnij się, że z kontrolerów domeny lub dedykowanych serwerów spełnia niezbędnych wymagań.

4.  W obszarze **skonfigurować czujnika**, wprowadź ścieżkę instalacji i klucza dostępu, który został skopiowany w poprzednim kroku, w zależności od używanego środowiska:

    ![Obraz konfiguracji czujnik autonomiczny Azure ATP](media/sensor-install-config.png)

      - Ścieżka instalacji: Jest to lokalizacja zainstalowanym czujnik autonomiczny Azure ATP. Domyślnie jest to %programfiles%\Azure czujnik Advanced Threat Protection. Pozostaw wartość domyślną.

      - Klucz dostępu: jest pobierana z portalu obszaru roboczego w poprzednim kroku.
    
5. Kliknij przycisk **Zainstaluj**. Następujące składniki zostaną zainstalowane i skonfigurowane podczas instalacji czujnik Azure ATP:

    -   KB 3047154 (tylko dla systemu Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Nie należy instalować aktualizacji KB 3047154 na hoście wirtualizacji (host, który uruchamia wirtualizację; można uruchomić ją na maszynie wirtualnej). Może to spowodować nieprawidłowe działanie funkcji dublowania portów. 
        > -   Jeśli Wireshark jest zainstalowany na maszynie czujnik ATP po uruchomieniu programu Wireshark, musisz ponownie uruchomić czujnik ATP, ponieważ wykorzystuje te same sterowniki.

    -   Azure usługi czujnik ATP i Azure ATP czujnik updater
    -   Pakiet redystrybucyjny Microsoft Visual C++ 2013

5.  Po zakończeniu instalacji kliknij przycisk **uruchamianie** Otwórz przeglądarkę i zalogować się do portalu Azure ATP obszaru roboczego.


>[!div class="step-by-step"]
[« Krok 3](install-atp-step3.md)
[Krok 5 »](install-atp-step5.md)


## <a name="see-also"></a>Zobacz też

- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)

- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)