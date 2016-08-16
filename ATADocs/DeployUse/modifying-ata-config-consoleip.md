---
title: "Zmienianie konfiguracji usługi ATA — adres IP konsoli usługi ATA | Microsoft ATA"
description: "Opisuje sposób zmiany adresu IP konsoli usługi ATA, używanego do tworzenia skrótów do konsoli usługi ATA w bramach usługi ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 03062652dd14183629ab1234f2d151931998c108


---

# Zmienianie konfiguracji usługi ATA — adres IP konsoli usługi ATA

>[!div class="step-by-step"]
[« Certyfikat centrum usługi ATA](modifying-ata-config-centercert.md)
[Certyfikat IIS »](modifying-ata-config-iiscert.md)

## Zmienianie adresu IP konsoli usługi ATA
Domyślnie adres URL konsoli usługi ATA to adres IP wybrany jako adres IP konsoli usługi ATA podczas instalacji centrum usługi ATA.

Ten adres URL jest używany w następujących scenariuszach:

-   Instalacja bram usługi ATA — podczas instalacji bramy usługi ATA rejestruje się ona w centrum usługi ATA. Ten proces rejestracji odbywa się przez nawiązanie połączenia z konsolą usługi ATA. Po wprowadzeniu nazwy FQDN dla adresu URL konsoli usługi ATA należy się upewnić, że brama usługi ATA może rozpoznać nazwę FQDN jako adres IP, z którym konsola usługi ATA jest powiązana w usłudze IIS. Ponadto adres URL jest wykorzystywany do tworzenia skrótu do konsoli usługi ATA w bramach usługi ATA.

-   Alerty — Gdy usługa ATA wysyła alert rozwiązania SIEM lub e-mail, dołącza łącze do podejrzanego działania. Częścią hosta tego łącza jest ustawienie adresu URL konsoli usługi ATA.

-   Jeśli zainstalowano certyfikat z wewnętrznego urzędu certyfikacji, możesz dopasować adres URL do nazwy podmiotu w certyfikacie, aby użytkownicy nie otrzymywali komunikatu ostrzegawczego podczas nawiązywania połączenia z konsolą usług ATA.

-   Użycie nazwy FQDN dla adresu URL konsoli usługi ATA pozwala zmodyfikować adres IP używany przez usługi IIS dla konsoli usługi ATA bez krytycznych alertów, które były wysyłane w przeszłości, lub potrzeby ponownego ładowania pakietu bramy usługi ATA. Wystarczy tylko zaktualizować DNS przy użyciu nowego adresu IP.

> [!NOTE]
> Po zmodyfikowaniu adresu URL konsoli usługi ATA należy pobrać pakiet instalacyjny bramy usługi ATA umożliwiający instalowanie nowych bram usługi ATA.

Jeśli musisz zmienić adres IP używany przez usługi IIS dla konsoli usługi ATA, wykonaj następujące czynności na serwerze centrum usługi ATA.

1.  Zainstaluj adres IP na serwerze centrum usługi ATA.

2.  Otwórz Menedżera internetowych usług informacyjnych (IIS).

3.  Rozwiń nazwę serwera i rozwiń pozycję **Witryny**.

4.  Wybierz witrynę konsoli usługi Microsoft ATA i w okienku **Akcje** kliknij pozycję **Powiązania**.

    ![Obraz akcji powiązań konsoli usługi ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Wybierz pozycję **HTTP** i kliknij opcję **Edytuj**, aby wybrać nowy adres IP. Wykonaj to samo dla pozycji **HTTPS**, wybierając ten sam adresu IP.

    ![Obraz edycji powiązania witryny](media/ATA-change-console-IP.jpg)

6.  W okienku **Akcja** kliknij przycisk **Uruchom ponownie** w obszarze **Zarządzaj witryną internetową**.

7.  Otwórz wiersz polecenia w trybie administratora i wpisz następujące polecenia, aby zaktualizować sterownik HTTP.SYS:

    -   Aby dodać nowy adres IP: `netsh http add iplisten ipaddress=newipaddress`

    -   Aby zobaczyć, czy nowy adres jest używany: `netsh http show iplisten`

    -   Aby usunąć stary adres IP: `netsh http delete iplisten ipaddress=oldipaddress`

8.  Jeśli adres URL konsoli usługi ATA nadal korzysta z adresu IP, zaktualizuj adres URL konsoli usługi ATA przy użyciu nowego adresu IP i pobierz pakiet instalacyjny bramy usługi ATA przed przystąpieniem do wdrażania nowych bram usługi ATA.

9. Jeśli adres URL konsoli usługi ATA jest nazwą FQDN, zaktualizuj DNS przy użyciu nowego adresu IP dla nazwy FQDN.

>[!div class="step-by-step"]
[« Certyfikat centrum usługi ATA](modifying-ata-config-centercert.md)
[Certyfikat IIS »](modifying-ata-config-iiscert.md)


## Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Instalowanie usługi ATA](install-ata.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


