---
title: "Zmienianie konfiguracji usługi ATA — certyfikat centrum usługi ATA | Microsoft ATA"
description: "Opis dwuetapowego procesu odnawiania lub wymiany certyfikatu w magazynie komputera lokalnego na serwerze centrum usługi ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: cda6fe75998149a42739907ae5a161d67392a509


---

# Zmienianie konfiguracji usługi ATA — certyfikat centrum usługi ATA

>[!div class="step-by-step"]
[« Adres IP serwera centrum usługi ATA](modifying-ata-config-centerip.md)
[Adres IP konsoli usługi ATA »](modifying-ata-config-consoleip.md)

## Zmienianie certyfikatu centrum usługi ATA
Jeśli Twoje certyfikaty wygasną i konieczne będzie ich odnowienie lub zmiana po zainstalowaniu nowego certyfikatu w magazynie komputera lokalnego na serwerze centrum usługi ATA, zastąp certyfikat, wykonując następujący dwuetapowy proces:

-   Pierwszy etap: zaktualizuj certyfikat, który ma być używany przez centrum usługi ATA. W tym momencie centrum usługi ATA jest nadal powiązane z oryginalnym certyfikatem. Podczas synchronizacji konfiguracji bram usługi ATA będą dostępne dwa potencjalne certyfikaty, za pomocą których będzie możliwe wzajemne uwierzytelnianie. Dopóki brama usługi ATA będzie mogła nawiązywać połączenie przy użyciu oryginalnego certyfikatu, nowy certyfikat nie będzie używany.

-   Drugi etap: po zsynchronizowaniu wszystkich bram usługi ATA z zaktualizowaną konfiguracją można aktywować nowy certyfikat, z którym powiązane jest centrum usługi ATA. Po aktywowaniu nowego certyfikatu centrum usługi ATA zostanie z nim powiązane. Bramy usługi ATA nie będą mogły poprawnie wzajemnie uwierzytelniać centrum usługi ATA i podejmą próbę uwierzytelnienia przy użyciu drugiego certyfikatu. Po nawiązaniu połączenia z centrum usługi ATA brama usługi ATA pobierze najnowszą konfigurację i będzie mieć jeden certyfikat dla centrum usługi ATA. Taka sytuacja będzie miała miejsce pod warunkiem, że proces nie zostanie ponownie rozpoczęty.

> [!NOTE]
> -   Jeśli brama usługi ATA była w trybie offline podczas pierwszego etapu i nigdy nie otrzymała zaktualizowanej konfiguracji, konieczne będzie ręczne zaktualizowanie pliku JSON konfiguracji w tej bramie.
> -   Używany certyfikat musi być zaufany przez bramy usługi ATA.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego certyfikatu, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.

1.  Otwórz konsolę usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

3.  Wybierz pozycję **Centrum usługi ATA**.

4.  W obszarze **Certyfikat** wybierz certyfikat z listy.

5.  Kliknij polecenie **Zapisz**.

6.  Zostanie wyświetlone powiadomienie z informacją o liczbie bram usługi ATA zsynchronizowanych z najnowszą konfiguracją.

7.  Po zsynchronizowaniu wszystkich bram usługi ATA kliknij polecenie **Aktywuj**, aby aktywować nowy certyfikat.
    >[!IMPORTANT]
    >Zanim aktywujesz nową konfigurację, sprawdź, czy wszystkie bramy usługi ATA są zsynchronizowane z najnowszą konfiguracją. Aktywowanie nowej konfiguracji przed zsynchronizowaniem bram usługi ATA może spowodować, że bramy usługi ATA przestaną działać zgodnie z oczekiwaniami. Jeśli jakakolwiek z bram usługi ATA nie jest zsynchronizowana, po kliknięciu pozycji Aktywuj zostanie wyświetlony następujący komunikat o błędzie:
    >
    >    ![Błąd synchronizacji bramy usługi ATA](media/ataGW-not-synced.png)

8.  Po aktywowaniu zmiany upewnij się, że bramy usługi ATA mogą synchronizować swoje konfiguracje.

>[!div class="step-by-step"]
[« Adres IP serwera centrum usługi ATA](modifying-ata-config-centerip.md)
[Adres IP konsoli usługi ATA »](modifying-ata-config-consoleip.md)

## Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Instalowanie usługi ATA](install-ata.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


