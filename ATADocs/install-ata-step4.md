---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 4 | Dokumentacja firmy Microsoft"
description: "W kroku 4 instalowania usługi ATA znajdują się informacje ułatwiające instalowanie bramy usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/18/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2713f6939c8756d0ecb438e866e6649f13d3c490
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# Instalowanie usługi ATA — Krok 4
<a id="install-ata---step-4" class="xliff"></a>

>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)

## Krok 4. Instalowanie bramy usługi ATA
<a id="step-4-install-the-ata-gateway" class="xliff"></a>

Przed zainstalowaniem bramy usługi ATA na dedykowanym serwerze zweryfikuj, czy funkcja dublowania portów jest poprawnie skonfigurowana oraz czy ruch do i z kontrolerów domeny jest widoczny dla bramy usługi ATA. Aby uzyskać więcej informacji, zobacz [Weryfikowanie funkcji dublowania portów](validate-port-mirroring.md).


> [!IMPORTANT]
> Upewnij się, że aktualizacja [KB2919355](http://support.microsoft.com/kb/2919355/) została zainstalowana.  Uruchom następujące polecenie cmdlet programu PowerShell, aby sprawdzić, czy zainstalowano poprawkę:
>
> `Get-HotFix -Id kb2919355`

Na serwerze bramy usługi ATA wykonaj następujące kroki.

1.  Wyodrębnij pliki z archiwum zip. 
> [!NOTE] 
> Instalowanie bezpośrednio z pliku zip zakończy się niepowodzeniem.

2.  Uruchom plik **Microsoft ATA Gateway Setup.exe**, a następnie postępuj zgodnie z instrukcjami kreatora instalacji.

3.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

4.  Kreator instalacji automatycznie sprawdzi, czy serwer jest kontrolerem domeny czy serwerem dedykowanym. Jeśli jest to kontroler domeny, zostanie zainstalowana uproszczona brama usługi ATA. Jeśli jest to dedykowany serwer, zostanie zainstalowana brama usługi ATA. 
    
    Na przykład w przypadku bramy usługi ATA zostanie wyświetlony następujący ekran z informacją, że brama usługi ATA zostanie zainstalowana na dedykowanym serwerze:
    
    ![Instalacja bramy usługi ATA](media/ata-gw-install.png) Kliknij przycisk **Dalej**.

    > [!NOTE] 
    > Jeśli kontroler domeny lub dedykowany serwer nie spełnia minimalnych wymagań sprzętowych dotyczących instalacji, zostanie wyświetlone ostrzeżenie. To nie uniemożliwia kliknięcia przycisku **Dalej** ani kontynuowania instalacji. Ta opcja może być właściwa w przypadku instalacji usługi ATA w małym, laboratoryjnym środowisku testowym, w którym nie potrzeba tak dużo miejsca do przechowywania danych. W środowiskach produkcyjnych zdecydowanie zaleca się korzystanie z przewodnika [planowania pojemności](ata-capacity-planning.md) usługi ATA w celu upewnienia się, że kontrolery domeny lub dedykowane serwery spełniają niezbędne wymagania.

4.  W obszarze **Konfiguracja bramy** podaj następujące informacje w zależności od używanego środowiska:

    ![Obraz przedstawiający konfigurację bramy usługi ATA](media/ata-gw-configure.png)

    > [!NOTE]
    > Podczas wdrażania bramy usługi ATA nie musisz podawać poświadczeń. Jeśli podczas instalacji bramy usługi ATA pobranie poświadczeń za pomocą funkcji logowania jednokrotnego nie powiedzie się (na przykład centrum usługi ATA lub brama usługi ATA nie należy do domeny albo nie masz poświadczeń administratora usługi ATA), zostanie wyświetlony monit o podanie poświadczeń przedstawiony na następującym ekranie. 

  ![Podanie poświadczeń bramy usługi ATA](media/ata-install-credentials.png)

   - Ścieżka instalacji: lokalizacja, w której zostanie zainstalowana brama usługi ATA. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Gateway. Pozostaw wartość domyślną.
    
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

## Zobacz też
<a id="see-also" class="xliff"></a>

- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

