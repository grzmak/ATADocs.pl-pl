---
title: Instalowanie usługi Advanced Threat Analytics — Krok 4 | Dokumentacja firmy Microsoft
description: W kroku 4 instalowania usługi ATA znajdują się informacje ułatwiające instalowanie bramy usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5414539edca088b49d16dc03c17dfe0ee0a2bfc5
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125876"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="install-ata---step-4"></a>Instalowanie usługi ATA — Krok 4

>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Krok 4. Instalowanie bramy usługi ATA

Przed zainstalowaniem bramy usługi ATA na dedykowanym serwerze zweryfikuj, czy funkcja dublowania portów jest poprawnie skonfigurowana oraz czy ruch do i z kontrolerów domeny jest widoczny dla bramy usługi ATA. Aby uzyskać więcej informacji, zobacz [weryfikowanie funkcji dublowania portów](validate-port-mirroring.md).


> [!IMPORTANT]
> Upewnij się, że aktualizacja [KB2919355](http://support.microsoft.com/kb/2919355/) została zainstalowana.  Uruchom następujące polecenie cmdlet programu PowerShell, aby sprawdzić, czy zainstalowano poprawkę:
>
> `Get-HotFix -Id kb2919355`

Na serwerze bramy usługi ATA wykonaj następujące kroki.

1.  Wyodrębnij pliki z archiwum zip. 
> [!NOTE] 
> Instalowanie bezpośrednio z pliku zip kończy się niepowodzeniem.

2.  Uruchom plik **Microsoft ATA Gateway Setup.exe**, a następnie postępuj zgodnie z instrukcjami kreatora instalacji.

3.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

4.  Kreator instalacji automatycznie sprawdza, czy serwer jest kontrolerem domeny czy serwerem dedykowanym. Jeśli jest kontrolerem domeny, uproszczonej bramy usługi ATA jest zainstalowany, jeśli jest dedykowany serwer, jest zainstalowana brama usługi ATA. 
    
    Na przykład w przypadku bramy usługi ATA wyświetlony jest następujący ekran z informacją, że brama usługi ATA zostanie zainstalowana na dedykowanym serwerze:
    
    ![Instalacja bramy usługi ATA](media/ata-gw-install.png) Kliknij przycisk **Dalej**.

    > [!NOTE] 
    > Jeśli kontroler domeny lub dedykowany serwer nie spełnia minimalnych wymagań sprzętowych dla instalacji, zostanie wyświetlone ostrzeżenie. To nie uniemożliwia kliknięcia przycisku **Dalej** ani kontynuowania instalacji. Może to być odpowiedniej opcji instalacji usługi ATA w małym, laboratoryjnym środowisku testowym, w którym nie potrzeba tak dużo miejsca, do przechowywania danych. W środowiskach produkcyjnych zdecydowanie zaleca się korzystanie z przewodnika [planowania pojemności](ata-capacity-planning.md) usługi ATA w celu upewnienia się, że kontrolery domeny lub dedykowane serwery spełniają niezbędne wymagania.

4.  W obszarze **Konfiguracja bramy** podaj następujące informacje w zależności od używanego środowiska:

    ![Obraz przedstawiający konfigurację bramy usługi ATA](media/ata-gw-configure.png)

    > [!NOTE]
    > Podczas wdrażania bramy usługi ATA, nie trzeba podać poświadczenia. W przypadku niepowodzenia instalacji bramy usługi ATA można pobrać poświadczeń za pomocą funkcji logowania jednokrotnego (na przykład, to może się zdarzyć, jeśli Centrum usługi ATA nie znajduje się w domenie, jeśli brama usługi ATA nie jest w domenie, nie masz poświadczeń administratora usługi ATA), zostanie wyświetlony monit o podanie poświadczeń przedstawiony na poniższym ekranie: 

  ![Podanie poświadczeń bramy usługi ATA](media/ata-install-credentials.png)

   - Ścieżka instalacji: Jest to lokalizacja, w którym zainstalowano bramę usługi ATA. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Gateway. Pozostaw wartość domyślną.
    
5. Kliknij przycisk **Zainstaluj**. Następujące składniki zostaną zainstalowane i skonfigurowane podczas instalacji bramy usługi ATA:

    -   KB 3047154 (tylko dla systemu Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Nie należy instalować aktualizacji KB 3047154 na hoście wirtualizacji (host, który uruchamia wirtualizację; można uruchomić ją na maszynie wirtualnej). Może to spowodować nieprawidłowe działanie funkcji dublowania portów. 
        > -   Nie instaluj programu Message Analyzer, programu Wireshark ani innego oprogramowania służącego do przechwytywania ruchu sieciowego w ramach bramy usługi ATA. Jeśli zachodzi potrzeba przechwytywania ruchu sieciowego, zainstaluj i zastosuj program Microsoft Network Monitor 3.4.

    -   Brama usługi ATA
    -   Pakiet redystrybucyjny Microsoft Visual C++ 2013
    -   Niestandardowy zestaw kolekcji danych monitora wydajności

5.  Po zakończeniu instalacji w przypadku bramy usługi ATA kliknij przycisk **Uruchom**, aby otworzyć przeglądarkę, i zaloguj się do konsoli usługi ATA. W przypadku uproszczonej bramy usługi ATA kliknij przycisk **Zakończ**.


>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)


## <a name="related-videos"></a>Pokrewne wideo
- [Omówienie wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniego typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania weryfikacji Koncepcji usługi ATA](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

