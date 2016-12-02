---
title: "Zmienianie konfiguracji usługi ATA — adres IP centrum usługi ATA | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu zmiany adresu IP, portu lub certyfikatu centrum usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/29/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bc7af91a925928183d179391f15d3a24cda2b576
ms.openlocfilehash: d0fed03deb5f50747383a398dfb2eca74ad0cdf0


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="change-ata-configuration---ata-center-ip-address"></a>Zmienianie konfiguracji usługi ATA — adres IP centrum usługi ATA

>[!div class="step-by-step"]
[Certyfikat centrum usługi ATA »](modifying-ata-config-centercert.md)

Po początkowym wdrożeniu należy uważnie wprowadzać modyfikacje w centrum usługi ATA. Podczas aktualizowania adresu IP i portu lub certyfikatu użyj następujących procedur.

## <a name="change-the-ip-address-used-by-the-ata-center-server"></a>Zmienianie adresu IP używanego przez serwer centrum usługi ATA
Jeśli zajdzie potrzeba zmiany adresu IP i portu lub certyfikatu centrum usługi ATA, należy wziąć pod uwagę następujące kwestie.

Bramy usługi ATA lokalnie przechowują adres IP centrum usługi ATA, z którym się łączą. Regularnie nawiązują one połączenie z centrum usługi ATA i pobierają zmiany konfiguracji. Wprowadzanie zmian w sposobie nawiązywania połączenia przez bramy usługi ATA z centrum usługi ATA jest wykonywane w dwóch etapach.

-   Pierwszy etap: zaktualizuj adres IP i port, które mają być używane przez bramę usługi ATA. W tym momencie centrum usługi ATA nadal nasłuchuje na oryginalnym adresie IP, a po następnej synchronizacji konfiguracji brama usługi ATA będzie mieć dwa adresy IP dla centrum usługi ATA. Dopóki brama usługi ATA będzie mogła nawiązywać połączenie przy użyciu oryginalnego (pierwszego) adresu IP, nowy adres IP i port nie będą używane.

-   Drugi etap: po zsynchronizowaniu wszystkich bram usługi ATA z zaktualizowaną konfiguracją aktywuj nowy adres IP oraz port, na którym nasłuchuje centrum usługi ATA. Po aktywowaniu nowego adresu IP centrum usługi ATA zostanie z nim powiązane. Bramy usługi ATA nie będą mogły nawiązywać połączenia z oryginalnym adresem IP i będą teraz podejmowały próbę nawiązania połączenia z drugim (nowym) adresem IP centrum usługi ATA. Po nawiązaniu połączenia z centrum usługi ATA za pomocą nowego adresu IP brama usługi ATA pobierze najnowszą konfigurację i będzie mieć jeden adres IP dla centrum usługi ATA. Taka sytuacja będzie miała miejsce pod warunkiem, że proces nie zostanie ponownie rozpoczęty.

> [!NOTE]
> -   Jeśli brama usługi ATA była w trybie offline podczas pierwszego etapu i nigdy nie otrzymała zaktualizowanej konfiguracji, konieczne będzie ręczne zaktualizowanie pliku JSON konfiguracji w tej bramie.
> -   Jeśli nowy adres IP został zainstalowany na serwerze centrum usługi ATA, możesz wybrać ten adres z listy adresów IP podczas wprowadzania zmian. Jeśli jednak z jakiegoś powodu nie można zainstalować adresu IP na serwerze centrum usługi ATA, możesz wybrać niestandardowy adres IP i dodać go ręcznie. Nowego adresu IP nie będzie można aktywować, dopóki nie zostanie on zainstalowany na serwerze.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego adresu IP, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.

1.  Otwórz konsolę usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

3.  Wybierz pozycję **Centrum**.

4.  W obszarze **Center service IP address : port** (Adres IP centrum usługi : port) wybierz jeden z istniejących adresów IP lub wybierz pozycję **Add custom IP address** (Dodaj niestandardowy adres IP) i wprowadź adres IP.

5.  Kliknij polecenie **Zapisz**.

6.  Zostanie wyświetlone powiadomienie z informacją o liczbie bram usługi ATA zsynchronizowanych z najnowszą konfiguracją.

    ![Obraz przedstawiający zsynchronizowane bramy centrum usługi ATA](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Zanim aktywujesz nową konfigurację, sprawdź, czy wszystkie bramy usługi ATA są zsynchronizowane z najnowszą konfiguracją. Aktywowanie nowej konfiguracji przed zsynchronizowaniem bram usługi ATA może spowodować, że bramy usługi ATA przestaną działać zgodnie z oczekiwaniami. Jeśli jakakolwiek z bram usługi ATA nie jest zsynchronizowana, po kliknięciu pozycji Aktywuj zostanie wyświetlony następujący komunikat o błędzie:
    >
    >    ![Błąd synchronizacji bramy usługi ATA](media/ataGW-not-synced.png)


7.  Po zsynchronizowaniu wszystkich bram usługi ATA kliknij polecenie **Aktywuj**, aby aktywować nowy adres IP.

    > [!NOTE]
    > Jeśli wprowadzono niestandardowy adres IP, nie będzie możliwości kliknięcia polecenia **Aktywuj**, dopóki adres IP nie zostanie zainstalowany w centrum usługi ATA.

8.  Po aktywowaniu zmiany upewnij się, że bramy usługi ATA mogą synchronizować swoje konfiguracje. Na pasku powiadomień będzie znajdować się informacja o liczbie bram usługi ATA, które pomyślnie zsynchronizowały swoją konfigurację.

>[!div class="step-by-step"]
[Zmienianie certyfikatu centrum usługi ATA »](modifying-ata-config-centercert.md)


## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://aka.ms/ata-forum)



<!--HONumber=Nov16_HO5-->


