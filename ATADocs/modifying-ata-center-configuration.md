---
title: "Zmienianie konfiguracji usługi Advanced Threat Analytics w centrum usługi ATA | Microsoft Docs"
description: "Zawiera opis sposobu zmiany adresu IP, portu, adresu URL konsoli lub certyfikatu centrum usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1e9fa2d104c52087746e7c03fea27e3cb596adf0
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="modifying-the-ata-center-configuration"></a>Modyfikowanie konfiguracji centrum usługi ATA


Po początkowym wdrożeniu należy uważnie wprowadzać modyfikacje w centrum usługi ATA. Użyj następujących procedur podczas aktualizowania adresu IP i portu, adresu URL konsoli oraz certyfikatu.

## <a name="the-ata-center-ip-address"></a>Adres IP centrum usługi ATA

Bramy usługi ATA lokalnie przechowują adres IP centrum usługi ATA, z którym się łączą. Regularnie nawiązują one połączenie z centrum usługi ATA i pobierają zmiany konfiguracji. Wprowadzanie zmian w sposobie nawiązywania połączenia przez bramy usługi ATA z centrum usługi ATA jest wykonywane w dwóch etapach.

-   Pierwszy etap: zaktualizuj adres IP i port, które mają być używane przez bramę usługi ATA. W tym momencie centrum usługi ATA nadal nasłuchuje na oryginalnym adresie IP, a po następnej synchronizacji konfiguracji brama usługi ATA będzie mieć dwa adresy IP dla centrum usługi ATA. Dopóki brama usługi ATA będzie mogła nawiązywać połączenie przy użyciu oryginalnego (pierwszego) adresu IP, nowy adres IP i port nie będą używane.

-   Drugi etap: po zsynchronizowaniu wszystkich bram usługi ATA z zaktualizowaną konfiguracją aktywuj nowy adres IP oraz port, na którym nasłuchuje centrum usługi ATA. Po aktywowaniu nowego adresu IP centrum usługi ATA zostanie z nim powiązane. Bramy usługi ATA nie będą mogły nawiązywać połączenia z oryginalnym adresem IP i będą teraz podejmowały próbę nawiązania połączenia z drugim (nowym) adresem IP centrum usługi ATA. Po nawiązaniu połączenia z centrum usługi ATA za pomocą nowego adresu IP brama usługi ATA pobierze najnowszą konfigurację i będzie mieć jeden adres IP dla centrum usługi ATA. Taka sytuacja będzie miała miejsce pod warunkiem, że proces nie zostanie ponownie rozpoczęty.

> [!NOTE]
> -   Jeśli brama usługi ATA była w trybie offline podczas pierwszego etapu i nigdy nie otrzymała zaktualizowanej konfiguracji, konieczne będzie ręczne zaktualizowanie pliku JSON konfiguracji w tej bramie.
> -   Jeśli nowy adres IP został zainstalowany na serwerze centrum usługi ATA, możesz wybrać ten adres z listy adresów IP podczas wprowadzania zmian. Jeśli jednak z jakiegoś powodu nie można zainstalować adresu IP na serwerze centrum usługi ATA, możesz wybrać niestandardowy adres IP i dodać go ręcznie. Nowego adresu IP nie będzie można aktywować, dopóki nie zostanie on zainstalowany na serwerze.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego adresu IP, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.

## <a name="the-console-url"></a>Adres URL konsoli

Ten adres URL jest używany w następujących scenariuszach:

-   Instalacja bram usługi ATA — podczas instalacji bramy usługi ATA rejestruje się ona w centrum usługi ATA. Ten proces rejestracji odbywa się przez nawiązanie połączenia z konsolą usługi ATA. Po wprowadzeniu nazwy FQDN dla adresu URL konsoli usługi ATA należy upewnić się, że brama usługi ATA może rozpoznać nazwę FQDN jako adres IP, z którym jest powiązana konsola usługi ATA.

-   Alerty — Gdy usługa ATA wysyła alert rozwiązania SIEM lub e-mail, dołącza łącze do podejrzanego działania. Częścią hosta tego łącza jest ustawienie adresu URL konsoli usługi ATA.

-   Jeśli zainstalowano certyfikat z wewnętrznego urzędu certyfikacji, możesz dopasować adres URL do nazwy podmiotu w certyfikacie, aby użytkownicy nie otrzymywali komunikatu ostrzegawczego podczas nawiązywania połączenia z konsolą usług ATA.

-   Użycie nazwy FQDN dla adresu URL konsoli usługi ATA pozwala zmodyfikować adres IP używany przez konsolę usługi ATA bez krytycznych alertów, które były wysyłane w przeszłości, lub potrzeby ponownego pobierania pakietu bramy usługi ATA. Wystarczy tylko zaktualizować DNS przy użyciu nowego adresu IP.

> [!NOTE]
> Po zmodyfikowaniu adresu URL konsoli usługi ATA należy pobrać pakiet instalacyjny bramy usługi ATA umożliwiający instalowanie nowych bram usługi ATA.

## <a name="the-ata-center-certificate"></a>Certyfikat centrum usługi ATA
Jeśli Twój certyfikat wkrótce wygaśnie i konieczne będzie jego odnowienie lub zmiana po zainstalowaniu nowego certyfikatu w magazynie komputera lokalnego na serwerze centrum usługi ATA, zastąp certyfikat, wykonując następujący dwuetapowy proces:

-   Pierwszy etap: zaktualizuj certyfikat, który ma być używany przez centrum usługi ATA. W tym momencie centrum usługi ATA jest nadal powiązane z oryginalnym certyfikatem. Podczas synchronizacji konfiguracji bram usługi ATA będą dostępne dwa potencjalne certyfikaty, za pomocą których będzie możliwe wzajemne uwierzytelnianie. Dopóki brama usługi ATA będzie mogła nawiązywać połączenie przy użyciu oryginalnego certyfikatu, nowy certyfikat nie będzie używany.

-   Drugi etap: po zsynchronizowaniu wszystkich bram usługi ATA z zaktualizowaną konfiguracją można aktywować nowy certyfikat, z którym powiązane jest centrum usługi ATA. Po aktywowaniu nowego certyfikatu centrum usługi ATA zostanie z nim powiązane. Bramy usługi ATA nie będą mogły poprawnie wzajemnie uwierzytelniać centrum usługi ATA i podejmą próbę uwierzytelnienia przy użyciu drugiego certyfikatu. Po nawiązaniu połączenia z centrum usługi ATA brama usługi ATA pobierze najnowszą konfigurację i będzie mieć jeden certyfikat dla centrum usługi ATA. Taka sytuacja będzie miała miejsce pod warunkiem, że proces nie zostanie ponownie rozpoczęty.

> [!NOTE]
> -   Jeśli brama usługi ATA była w trybie offline podczas pierwszego etapu i nigdy nie otrzymała zaktualizowanej konfiguracji, konieczne będzie ręczne zaktualizowanie pliku JSON konfiguracji w tej bramie.
> -   Używany certyfikat musi być zaufany przez bramy usługi ATA.
> -   Certyfikat jest również używany w konsoli usługi ATA, dlatego powinien pasować do adresu konsoli usługi ATA, aby uniknąć wyświetlania ostrzeżeń przeglądarki.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego certyfikatu, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.

## <a name="changing-the-ata-center-configuration"></a>Zmienianie konfiguracji centrum usługi ATA

1.  Otwórz konsolę usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.png)

3.  Wybierz pozycję **Centrum**.

  ![Zmienianie konfiguracji usługi ATA](media/change-center-config.png)

4.  W obszarze **Adres URL** wybierz pozycję **Dodaj niestandardową nazwę DNS/adres IP** i nowy adres DNS lub adres IP albo w obszarze **Certyfikat** wybierz nowy certyfikat.

5.  Kliknij polecenie **Zapisz**.

6.  Zostanie wyświetlone powiadomienie z informacją o liczbie bram usługi ATA zsynchronizowanych z najnowszą konfiguracją.

    >[!IMPORTANT]
    >Zanim aktywujesz nową konfigurację, sprawdź, czy wszystkie bramy usługi ATA są zsynchronizowane z najnowszą konfiguracją. Aktywowanie nowej konfiguracji przed zsynchronizowaniem bram usługi ATA może spowodować, że bramy usługi ATA przestaną działać zgodnie z oczekiwaniami. Jeśli jakakolwiek z bram usługi ATA nie jest zsynchronizowana, po kliknięciu pozycji Aktywuj zostanie wyświetlony następujący komunikat o błędzie:


7.  Po zsynchronizowaniu wszystkich bram usługi ATA kliknij polecenie **Aktywuj**, aby aktywować nowy adres IP lub certyfikat.

    > [!NOTE]
    > Jeśli wprowadzono niestandardowy adres IP, nie będzie możliwości kliknięcia polecenia **Aktywuj**, dopóki adres IP nie zostanie zainstalowany w centrum usługi ATA.

8.  Po aktywowaniu zmiany upewnij się, że bramy usługi ATA mogą synchronizować swoje konfiguracje. Na pasku powiadomień będzie znajdować się informacja o liczbie bram usługi ATA, które pomyślnie zsynchronizowały swoją konfigurację.




## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://aka.ms/ata-forum)
