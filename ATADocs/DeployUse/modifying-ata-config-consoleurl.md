---
title: "Zmienianie konfiguracji usługi Advanced Threat Analytics — adres IP konsoli | Usługa Microsoft Advanced Threat Analytics"
description: "Opisuje sposób zmiany adresu IP konsoli usługi ATA, używanego do tworzenia skrótów do konsoli usługi ATA w bramach usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: stevenpo
ms.date: 1/23/2017
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: db179445a0ea80411a0462e639f1d8c890bf21b0
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="change-ata-configuration---ata-console-url"></a>Zmienianie konfiguracji usługi ATA — adres URL konsoli usługi ATA

>[!div class="step-by-step"]
[« Certyfikat centrum usługi ATA](modifying-ata-config-centercert.md)
[Hasło łączności domenowej »](modifying-ata-config-dcpassword.md)

## <a name="change-the-ata-console-url"></a>Zmienianie adresu URL konsoli usługi ATA
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
> [!NOTE]
> Nie umieszczaj ukośnika „/” na końcu adresu URL.

6.  Kliknij polecenie **Zapisz**.

>[!div class="step-by-step"]
[« Certyfikat centrum usługi ATA](modifying-ata-config-centercert.md)
[Hasło łączności domenowej »](modifying-ata-config-dcpassword.md)


## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://aka.ms/ata-forum)
