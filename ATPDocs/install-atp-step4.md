---
title: Install Azure Zaawansowana ochrona przed zagrożeniami — krok 4 | Dokumentacja firmy Microsoft
description: W kroku 4 instalowania usługi Azure ATP pomaga zainstalować czujnik autonomiczny narzędzia Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 87a2b47261293fffffe9d822d698b551a332a481
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454143"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="install-azure-atp---step-4"></a>Zainstaluj narzędzie Azure ATP — krok 4

> [!div class="step-by-step"]
> [« Krok 3](install-atp-step3.md)
> [Krok 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Krok 4. Instalowanie czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure

Przed zainstalowaniem narzędzia Azure ATP czujnik autonomiczny na dedykowanym serwerze Zweryfikuj, czy funkcja dublowania portów jest prawidłowo skonfigurowane i że czujnik autonomiczny narzędzia Azure ATP może widzieć ruch do i z kontrolerów domeny. 


> [!IMPORTANT]
>Upewnij się, że .net Framework 4.7 jest zainstalowany na komputerze. Jeśli .net Framework 4.7 to nie jest zainstalowany pakiet instalacyjny czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure instaluje go, co wymaga ponownego uruchomienia serwera.

Wykonaj następujące czynności na serwerze czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure lub kontrolera domeny.

1. Sprawdź, czy komputer ma łączność z odpowiednimi punktu końcowego usługi chmury usługi Azure ATP:
  - https://triprd1wceuw1sensorapi.atp.azure.com (w przypadku Europy)  
  - https://triprd1wcuse1sensorapi.atp.azure.com (dla Stanów Zjednoczonych)
  - https://triprd1wcasse1sensorapi.atp.azure.com (w przypadku Azja)

2. Wyodrębnienie plików instalacyjnych z pliku zip. 
> [!NOTE] 
> Instalowanie bezpośrednio z pliku zip kończy się niepowodzeniem.

3.  Uruchom **setup.exe czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure** i postępuj zgodnie z Kreatora instalacji.

4.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

     ![Azure język instalacji czujnika zaawansowanej ochrony przed zagrożeniami autonomiczny](media/sensor-install-language.png)


5.  Kreator instalacji automatycznie sprawdza, czy serwer jest kontrolerem domeny czy serwerem dedykowanym. Jeśli jest kontrolerem domeny, czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jest zainstalowany, jeśli jest dedykowany serwer, jest zainstalowany czujnik autonomiczny narzędzia Azure ATP. 
    
    Na przykład dla usługi Azure ATP czujnik autonomiczny, wyświetlony jest następujący ekran z informacją, że czujnik autonomiczny narzędzia Azure ATP jest zainstalowany na dedykowanym serwerze:
    
    ![Instalowanie czujnika autonomicznego w usłudze Azure ATP](media/sensor-install-deployment-type.png)

    Kliknij przycisk **Dalej**.

    > [!NOTE] 
    > Jeśli kontroler domeny lub dedykowany serwer nie spełnia minimalnych wymagań sprzętowych dla instalacji, zostanie wyświetlone ostrzeżenie. To nie uniemożliwia kliknięcia przycisku **Dalej** ani kontynuowania instalacji. Może to być odpowiedniej opcji instalacji narzędzia Azure ATP w małym, laboratoryjnym środowisku testowym, w którym nie potrzeba tak dużo miejsca, do przechowywania danych. W środowiskach produkcyjnych zdecydowanie zaleca do pracy z narzędzia Azure ATP [planowania pojemności](atp-capacity-planning.md) przewodnika, aby upewnić się, że kontrolery domeny lub dedykowane serwery spełniają niezbędne wymagania.

6.  W obszarze **Konfiguracja czujnika**, wprowadź ścieżkę instalacji i klucz dostępu, który został skopiowany w poprzednim kroku, w zależności od używanego środowiska:

    ![Azure ATP autonomicznego czujnik konfiguracji obrazu](media/sensor-install-config.png)

      - Ścieżka instalacji: To lokalizacja, w którym jest zainstalowany czujnik autonomiczny narzędzia Azure ATP. Domyślnie jest to czujnika zaawansowanej ochrony przed zagrożeniami %programfiles%\Azure. Pozostaw wartość domyślną.

      - Klucz dostępu: jest pobierana z portalu obszaru roboczego w poprzednim kroku.
    
7. Kliknij przycisk **Zainstaluj**. Następujące składniki są zainstalowane i skonfigurowane podczas instalacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure:

    -   KB 3047154 (tylko dla systemu Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Nie należy instalować aktualizacji KB 3047154 na hoście wirtualizacji (host, który uruchamia wirtualizację; można uruchomić ją na maszynie wirtualnej). Może to spowodować nieprawidłowe działanie funkcji dublowania portów. 
        > -   Jeśli program Wireshark jest zainstalowany na komputerze z czujnika zaawansowanej ochrony przed zagrożeniami, po uruchomieniu programu Wireshark zachodzi potrzeba ponownego uruchomienia czujnika zaawansowanej ochrony przed zagrożeniami, ponieważ używa ona te same sterowniki.

    -   Usługa Azure service czujnika zaawansowanej ochrony przed zagrożeniami i usługę aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure
    -   Pakiet redystrybucyjny Microsoft Visual C++ 2013

8.  Po zakończeniu instalacji kliknij przycisk **Uruchom** Otwórz przeglądarkę i zaloguj się do portalu obszaru roboczego usługi Azure ATP.


> [!div class="step-by-step"]
> [« Krok 3](install-atp-step3.md)
> [Krok 5 »](install-atp-step5.md)


## <a name="see-also"></a>Zobacz też

- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)

- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
