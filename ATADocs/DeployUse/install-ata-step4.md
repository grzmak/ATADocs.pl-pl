---
title: "Instalowanie usługi ATA — Krok 4 | Microsoft Advanced Threat Analytics"
description: "W kroku 4 instalowania usługi ATA znajdują się informacje ułatwiające instalowanie bramy usługi ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: f12e43a6918c0c02bb59e4a093720a805b7dbcfc


---

# Instalowanie usługi ATA — Krok 4

>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)

## Krok 4. Instalowanie bramy usługi ATA

Przed zainstalowaniem bramy usługi ATA na dedykowanym serwerze zweryfikuj, czy funkcja dublowania portów jest poprawnie skonfigurowana oraz czy ruch do i z kontrolerów domeny jest widoczny dla bramy usługi ATA. Aby uzyskać więcej informacji, zobacz [Weryfikowanie funkcji dublowania portów](validate-port-mirroring.md).


> [!IMPORTANT]
> Upewnij się, że aktualizacja [KB2919355](http://support.microsoft.com/kb/2919355/) została zainstalowana.  Uruchom następujące polecenie cmdlet programu PowerShell, aby sprawdzić, czy zainstalowano poprawkę:
>
> `Get-HotFix -Id kb2919355`

Na serwerze bramy usługi ATA wykonaj następujące kroki.

1.  Wyodrębnij pliki z archiwum zip. 
> [!NOTE] 
> Instalowanie bezpośrednio z pliku zip zakończy się niepowodzeniem.

2.  Z poziomu wiersza polecenia z podwyższonym poziomem uprawnień uruchom plik **Microsoft ATA Gateway Setup.exe**, a następnie postępuj zgodnie z instrukcjami kreatora instalacji.

3.  Na stronie **Zapraszamy** wybierz swój język i kliknij przycisk **Dalej**.

4.  W obszarze **Konfiguracja bramy usługi ATA** wprowadź następujące informacje w zależności od używanego środowiska:

    ![Obraz przedstawiający konfigurację bramy usługi ATA](media/ATA-Gateway-Configuration.JPG)

    |Pole|Opis|Komentarze|
    |---------|---------------|------------|
    |Ścieżka instalacji|Lokalizacja, w której zostanie zainstalowana brama usługi ATA. Domyślna lokalizacja to %programfiles%\Microsoft Advanced Threat Analytics\Gateway|Pozostaw wartość domyślną.|
    |Certyfikat SSL bramy usługi ATA|Certyfikat, który będzie używany przez bramę usługi ATA.|Certyfikatu z podpisem własnym należy używać tylko w przypadku środowisk laboratoryjnych.|
    |Rejestracja bramy usługi ATA|Wprowadź nazwę użytkownika i hasło administratora usługi ATA.|Aby zarejestrować bramę usługi ATA w centrum usługi ATA, wprowadź nazwę i hasło użytkownika, który zainstalował centrum usługi ATA. Ten użytkownik musi należeć do jednej z następujących grup lokalnych w centrum usługi ATA.<br /><br />— Administratorzy<br />— Administratorzy usługi Microsoft Advanced Threat Analytics (**Uwaga:** te poświadczenia są używane tylko do rejestracji i nie są przechowywane w usłudze ATA)|
    Następujące składniki zostaną zainstalowane i skonfigurowane podczas instalacji bramy usługi ATA:

    -   Aktualizacja KB 3047154

        > [!IMPORTANT]
        > -   Nie należy instalować aktualizacji KB 3047154 na hoście wirtualizacji (host, który uruchamia wirtualizację; można uruchomić ją na maszynie wirtualnej). Może to spowodować nieprawidłowe działanie funkcji dublowania portów. 
        > -   Nie instaluj programu Message Analyzer, programu Wireshark ani innego oprogramowania służącego do przechwytywania ruchu sieciowego w ramach bramy usługi ATA. Jeśli zachodzi potrzeba przechwytywania ruchu sieciowego, zainstaluj i zastosuj program Microsoft Network Monitor 3.4.

    -   Brama usługi ATA

    -   Pakiet redystrybucyjny Microsoft Visual C++ 2013

    -   Niestandardowy zestaw kolekcji danych monitora wydajności

5.  Po zakończeniu instalacji w przypadku bramy usługi ATA kliknij przycisk **Uruchom**, aby otworzyć przeglądarkę, i zaloguj się do konsoli usługi ATA. W przypadku bramy ATA Lightweight Gateway kliknij przycisk **Zakończ**.


>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)

## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


