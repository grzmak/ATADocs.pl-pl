---
title: Zmienianie konfiguracji usługi Advanced Threat Analytics w centrum usługi ATA | Microsoft Docs
description: Zawiera opis sposobu zmiany adresu IP, portu, adresu URL konsoli lub certyfikatu centrum usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 294b9204f9ca6a40a835e5360a7011947e3255b4
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010044"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="modifying-the-ata-center-configuration"></a>Modyfikowanie konfiguracji centrum usługi ATA


Po początkowym wdrożeniu należy uważnie wprowadzać modyfikacje w centrum usługi ATA. Użyj poniższych procedur, podczas aktualizowania adresu URL konsoli i certyfikat.

## <a name="the-ata-console-url"></a>Adres URL konsoli usługi ATA

Ten adres URL jest używany w następujących scenariuszach:

-   Jest to adres URL używany przez bramy usługi ATA do komunikowania się z Centrum usługi ATA.

- Instalacja bram usługi ATA — podczas instalacji bramy usługi ATA rejestruje się ona w centrum usługi ATA. Ten proces rejestracji odbywa się przez nawiązanie połączenia z konsolą usługi ATA. Po wprowadzeniu nazwy FQDN dla adresu URL konsoli usługi ATA, upewnij się, czy bramy usługi ATA może rozpoznać nazwę FQDN na adres IP powiązane z konsolą usługi ATA.

-   Alerty — Gdy usługa ATA wysyła alert rozwiązania SIEM lub e-mail, dołącza łącze do podejrzanego działania. Częścią hosta tego łącza jest ustawienie adresu URL konsoli usługi ATA.

-   Jeśli certyfikat został zainstalowany z z wewnętrznego urzędu certyfikacji (CA), odpowiadał adresowi URL, do nazwy podmiotu w certyfikacie. Uniemożliwia to użytkownikom uzyskiwanie komunikatu ostrzegawczego podczas nawiązywania połączenia z konsolą usługi ATA.

-   Użycie nazwy FQDN dla adresu URL konsoli usługi ATA pozwala zmodyfikować adres IP, który jest używany przez konsolę usługi ATA bez krytycznych alertów, poprzednie lub ponownie załadować pakietu bramy usługi ATA. Wystarczy tylko zaktualizować DNS przy użyciu nowego adresu IP.

1. Upewnij się, że nowy adres URL, którego chcesz użyć jest rozpoznawana jako adres IP konsoli usługi ATA.

2. W ustawieniach usługi ATA w obszarze **Center**, wprowadź nowy adres URL. W tym momencie Centrum usługi ATA nadal korzysta z oryginalnego adresu URL. 

 ![Zmienianie konfiguracji usługi ATA](media/change-center-config.png)

  > [!NOTE]
  > Jeśli wprowadzono niestandardowy adres IP, nie można kliknąć **Aktywuj** do chwili zainstalowania adres IP Centrum usługi ATA.
    
3. Poczekaj, aż bram usługi ATA do synchronizowania. Teraz mają dwa potencjalne adresy URL za pośrednictwem której można uzyskać dostępu do konsoli usługi ATA. Tak długo, jak bramy usługi ATA mogą łączyć przy użyciu oryginalnego adresu URL, nie jest jego nowego.

4. Po kliknięciu przycisku wszystkich bram usługi ATA zsynchronizowanych z zaktualizowaną konfiguracją, na stronie Konfiguracja centrum **Aktywuj** przycisk, aby aktywować nowy adres URL. Po aktywowaniu nowego adresu URL bram usługi ATA teraz używać nowego adresu URL do Centrum usługi ATA. Po połączeniu z Centrum usługi ATA, bramy usługi ATA pobierze najnowszą konfigurację i będzie mieć tylko nowy adres URL konsoli usługi ATA. 
5. 
 ![Aktywuj certyfikatu](media/center-activation.png)

> [!NOTE]
> -   Jeśli bramy usługi ATA była w trybie offline, gdy aktywować nowy adres URL i nigdy nie otrzymała zaktualizowanej konfiguracji, należy ręcznie zaktualizować pliku JSON konfiguracji na bramie usługi ATA.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego adresu URL, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.


## <a name="the-ata-center-certificate"></a>Certyfikat centrum usługi ATA

> [!WARNING]
> - Proces odnowienie istniejącego certyfikatu nie jest obsługiwane. Jedynym sposobem, aby odnowić certyfikat jest tworzony nowy certyfikat i konfigurowania usługi ATA przy użyciu nowego certyfikatu.


Zastąp certyfikat, wykonując ten proces:

1. Przed wygaśnięciem bieżącego certyfikatu, Utwórz nowy certyfikat i upewnij się, że jest zainstalowany na serwerze Centrum usługi ATA. <br></br>Zalecane jest wybranie certyfikatu od urzędu certyfikacji wewnętrznego, że istnieje również możliwość utworzenia nowego certyfikatu z podpisem własnym. Aby uzyskać więcej informacji, zobacz [SelfSignedCertificate nowy](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. W ustawieniach usługi ATA w obszarze **Center**, wybierz nowo utworzonego certyfikatu. W tym momencie Centrum usługi ATA jest nadal powiązane z oryginalnym certyfikatem. 

 ![Zmienianie konfiguracji usługi ATA](media/change-center-config.png)

3. Poczekaj, aż bram usługi ATA do synchronizowania. Teraz mają dwa potencjalne certyfikaty, które są prawidłowe dla uwierzytelniania wzajemnego. Tak długo, jak bramy usługi ATA mogą łączyć przy użyciu oryginalnego certyfikatu, nie jest jego nowego.

4. Po wszystkich bram usługi ATA zsynchronizowanych z zaktualizowaną konfiguracją aktywować nowy certyfikat powiązany z Centrum usługi ATA. Po aktywowaniu nowego certyfikatu Centrum usługi ATA jest powiązany z nowego certyfikatu. Bramy usługi ATA teraz używać nowego certyfikatu do uwierzytelnienia przy użyciu Centrum usługi ATA. Po połączeniu z Centrum usługi ATA, bramy usługi ATA pobierze najnowszą konfigurację i będzie mieć tylko nowy certyfikat dla Centrum usługi ATA. 

> [!NOTE]
> -   Jeśli bramy usługi ATA była w trybie offline, gdy aktywować nowy certyfikat i nigdy nie otrzymała zaktualizowanej konfiguracji, należy ręcznie zaktualizować pliku JSON konfiguracji na bramie usługi ATA.
> -   Używany certyfikat musi być zaufany przez bramy usługi ATA.
> -   Certyfikat jest również używane w konsoli usługi ATA, więc powinna być zgodna adres konsoli usługi ATA, aby uniknąć ostrzeżeń w przeglądarce.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego certyfikatu, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.



 
## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://aka.ms/ata-forum)
