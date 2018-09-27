---
title: Zmienianie konfiguracji usługi Advanced Threat Analytics w centrum usługi ATA | Microsoft Docs
description: Zawiera opis sposobu zmiany adresu IP, portu, adresu URL konsoli lub certyfikatu centrum usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 80f96966a1ba9e62b23311cc19ed8fc5a8210bba
ms.sourcegitcommit: 56065ee43dac299203871cd6f025315520750b3b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/26/2018
ms.locfileid: "47233868"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="modifying-the-ata-center-configuration"></a>Modyfikowanie konfiguracji centrum usługi ATA


Po początkowym wdrożeniu należy uważnie wprowadzać modyfikacje w centrum usługi ATA. Użyj następujących procedur podczas aktualizowania adresu URL konsoli oraz certyfikatu.

## <a name="the-ata-console-url"></a>Adres URL konsoli usługi ATA

Ten adres URL jest używany w następujących scenariuszach:

-   Jest to adres URL używany przez bramy usługi ATA do komunikowania się z Centrum usługi ATA.

- Instalacja bram usługi ATA — podczas instalacji bramy usługi ATA rejestruje się ona w centrum usługi ATA. Ten proces rejestracji odbywa się przez nawiązanie połączenia z konsolą usługi ATA. Po wprowadzeniu nazwy FQDN dla adresu URL konsoli usługi ATA, upewnij się, że bramy usługi ATA może rozpoznać nazwę FQDN adresu IP, powiązany z konsolą usługi ATA.

-   Alerty — Gdy usługa ATA wysyła alert rozwiązania SIEM lub e-mail, dołącza łącze do podejrzanego działania. Częścią hosta tego łącza jest ustawienie adresu URL konsoli usługi ATA.

-   Jeśli zainstalowano certyfikat z Twojego wewnętrznego urzędu certyfikacji (CA), odpowiadał adresowi URL do nazwy podmiotu w certyfikacie. Uniemożliwia to użytkownikom pobieranie komunikatu ostrzegawczego podczas nawiązywania połączenia z konsolą usługi ATA.

-   Użycie nazwy FQDN dla adresu URL konsoli usługi ATA pozwala zmodyfikować adres IP, który jest używany przez konsolę usługi ATA bez krytycznych alertów, poprzednie lub ponownie załadować pakietu bramy usługi ATA. Wystarczy tylko zaktualizować DNS przy użyciu nowego adresu IP.

1. Upewnij się, że nowy adres URL, którego chcesz użyć jest rozpoznawana jako adres IP konsoli usługi ATA.

2. W ustawieniach usługi ATA w obszarze **Centrum**, wprowadź nowy adres URL. W tym momencie Centrum usługi ATA nadal używa oryginalny adres URL. 

 ![Zmienianie konfiguracji usługi ATA](media/change-center-config.png)

  > [!NOTE]
  > Jeśli wprowadzono niestandardowy adres IP, nie można kliknąć **Aktywuj** do czasu zainstalowania adres IP Centrum usługi ATA.
    
3. Poczekaj, aż bram usługi ATA do synchronizowania. Ma teraz dwa potencjalne adresy URL za pomocą którego można uzyskać dostęp do konsoli usługi ATA. Tak długo, jak bramy usługi ATA może się łączyć przy użyciu oryginalnego adresu URL nie próbuje nowym.

4. Po kliknięciu przycisku wszystkich bram usługi ATA zsynchronizowanych z zaktualizowaną konfiguracją, na stronie konfiguracji centrum **Aktywuj** przycisk, aby aktywować nowy adres URL. Po aktywowaniu nowego adresu URL bram usługi ATA będą teraz korzystały nowy adres URL, aby dostęp do Centrum usługi ATA. Po połączeniu się z Centrum usługi ATA, bramy usługi ATA pobierze najnowszą konfigurację i będzie mieć tylko nowy adres URL do konsoli usługi ATA. 
5. 
 ![Aktywować certyfikatu](media/center-activation.png)

> [!NOTE]
> -   Jeśli brama usługi ATA była w trybie offline, możesz aktywować nowy adres URL i nigdy nie otrzymała zaktualizowanej konfiguracji, należy ręcznie zaktualizować plik JSON konfiguracji w bramie usługi ATA.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego adresu URL, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.


## <a name="the-ata-center-certificate"></a>Certyfikat centrum usługi ATA

> [!WARNING]
> - Proces odnawiania istniejącego certyfikatu nie jest obsługiwane. Jest jedynym sposobem, aby odnowić certyfikat, tworząc nowy certyfikat i konfigurowania usługi ATA, aby używała nowego certyfikatu.


Zastąp certyfikat, wykonując następujący proces:

1. Przed upływem bieżącego certyfikatu, Utwórz nowy certyfikat i upewnij się, że jest zainstalowany na serwerze Centrum usługi ATA. <br></br>Zalecane jest, że wybierzesz certyfikat od urzędu certyfikacji wewnętrzny, ale jest również możliwość utworzenia nowego certyfikatu z podpisem własnym. Aby uzyskać więcej informacji, zobacz [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. W ustawieniach usługi ATA w obszarze **Centrum**, zaznacz ten nowo utworzonego certyfikatu. W tym momencie Centrum usługi ATA jest nadal powiązane z oryginalnym certyfikatem. 

 ![Zmienianie konfiguracji usługi ATA](media/change-center-config.png)

3. Poczekaj, aż bram usługi ATA do synchronizowania. Ma teraz dwa potencjalne certyfikaty, które są prawidłowe dla uwierzytelniania wzajemnego. Tak długo, jak bramy usługi ATA może się łączyć przy użyciu oryginalnego certyfikatu nie próbuje nowym.

4. Po wszystkich bram usługi ATA zsynchronizowanych z zaktualizowaną konfiguracją należy aktywować nowy certyfikat powiązany z Centrum usługi ATA. Po aktywowaniu nowego certyfikatu Centrum usługi ATA wiąże się na nowy certyfikat. Bramy usługi ATA teraz używać nowego certyfikatu do uwierzytelniania przy użyciu Centrum usługi ATA. Po połączeniu się z Centrum usługi ATA, bramy usługi ATA pobierze najnowszą konfigurację i będzie mieć tylko nowy certyfikat dla Centrum usługi ATA. 

> [!NOTE]
> -   Jeśli brama usługi ATA była w trybie offline, gdy aktywować nowy certyfikat i nigdy nie otrzymała zaktualizowanej konfiguracji, należy ręcznie zaktualizować plik JSON konfiguracji w bramie usługi ATA.
> -   Używany certyfikat musi być zaufany przez bramy usługi ATA.
> -   Certyfikat służy także do konsoli usługi ATA, dlatego powinien pasować adresu konsoli usługi ATA, aby uniknąć wyświetlania ostrzeżeń przeglądarki.
> -   Jeśli zajdzie potrzeba wdrożenia nowej bramy usługi ATA po aktywowaniu nowego certyfikatu, należy ponownie pobrać pakiet instalacyjny bramy usługi ATA.



 
## <a name="see-also"></a>Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Forum usługi ATA](https://aka.ms/ata-forum)
