---
title: "Zmienianie konfiguracji usługi ATA — adres IP konsoli usługi ATA | Usługa Microsoft Advanced Threat Analytics"
description: "Opisuje sposób zmiany adresu IP konsoli usługi ATA, używanego do tworzenia skrótów do konsoli usługi ATA w bramach usługi ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 08/24/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: b3d11a87f1909c1fd964fa990e5d36a91691a844


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Zmienianie konfiguracji usługi ATA — adres URL konsoli usługi ATA

>[!div class="step-by-step"]
[« Certyfikat centrum usługi ATA](modifying-ata-config-centercert.md)
[Hasło łączności domenowej »](modifying-ata-config-dcpassword.md)

## Zmienianie adresu URL konsoli usługi ATA
Domyślnie adres URL konsoli usługi ATA to adres IP wybrany jako adres IP konsoli usługi ATA podczas instalacji centrum usługi ATA.

Ten adres URL jest używany w następujących scenariuszach:

-   Instalacja bram usługi ATA — podczas instalacji bramy usługi ATA rejestruje się ona w centrum usługi ATA. Ten proces rejestracji odbywa się przez nawiązanie połączenia z konsolą usługi ATA. Po wprowadzeniu nazwy FQDN dla adresu URL konsoli usługi ATA należy upewnić się, że brama usługi ATA może rozpoznać nazwę FQDN jako adres IP, z którym jest powiązana konsola usługi ATA.

-   Alerty — Gdy usługa ATA wysyła alert rozwiązania SIEM lub e-mail, dołącza łącze do podejrzanego działania. Częścią hosta tego łącza jest ustawienie adresu URL konsoli usługi ATA.

-   Jeśli zainstalowano certyfikat z wewnętrznego urzędu certyfikacji, możesz dopasować adres URL do nazwy podmiotu w certyfikacie, aby użytkownicy nie otrzymywali komunikatu ostrzegawczego podczas nawiązywania połączenia z konsolą usług ATA.

-   Użycie nazwy FQDN dla adresu URL konsoli usługi ATA pozwala zmodyfikować adres IP używany przez konsolę usługi ATA bez krytycznych alertów, które były wysyłane w przeszłości, lub potrzeby ponownego pobierania pakietu bramy usługi ATA. Wystarczy tylko zaktualizować DNS przy użyciu nowego adresu IP.

> [!NOTE]
> Po zmodyfikowaniu adresu URL konsoli usługi ATA należy pobrać pakiet instalacyjny bramy usługi ATA umożliwiający instalowanie nowych bram usługi ATA.

Jeśli musisz zmienić adres URL konsoli usługi ATA, wykonaj następujące czynności na serwerze centrum usługi ATA.

1.  Otwórz konsolę usługi ATA.

2.  Na pasku narzędzi wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

3.  Wybierz pozycję **Centrum**.

4.  W obszarze **Console IP Address** (Adres IP konsoli) wybierz jeden z istniejących adresów IP.

5.  W obszarze **Console URL** (Adres URL konsoli) zmodyfikuj adres URL:

    ![Adres URL konsoli usługi ATA](media/ATA-chge-center-URL.png)
6.  Kliknij polecenie **Zapisz**.

>[!div class="step-by-step"]
[« Certyfikat centrum usługi ATA](modifying-ata-config-centercert.md)
[Hasło łączności domenowej »](modifying-ata-config-dcpassword.md)


## Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Instalowanie usługi ATA](install-ata.md)
- [Zapoznaj się z forum usługi ATA!](https://aka.ms/ata-forum)



<!--HONumber=Aug16_HO5-->


