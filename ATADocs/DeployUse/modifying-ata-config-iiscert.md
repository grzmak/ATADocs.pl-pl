---
# required metadata

title: Zmienianie konfiguracji usługi ATA — certyfikat usług IIS | Microsoft Advanced Threat Analytics
description: Opis sposobu zmieniania certyfikatu używanego przez usługi IIS dla centrum usługi ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Zmienianie konfiguracji usługi ATA — certyfikat usług IIS

>[!div class="step-by-step"]
[« Adres IP konsoli usługi ATA](modifying-ata-config-consoleip.md)
[Hasło do łączności z domeną »](modifying-ata-config-dcpassword.md)

## Zmienianie certyfikatu usług IIS
W konsoli można wybrać i zmienić certyfikat dla centrum usługi ATA, ale nie można zmienić certyfikatu używanego przez usługi IIS.

Jeśli chcesz zmienić ten certyfikat, wykonaj następującą procedurę:

> [!NOTE]
> Po zmodyfikowaniu certyfikatu usług IIS należy pobrać pakiet instalacyjny bramy usługi ATA przed zainstalowaniem nowych bram usługi ATA.

Jeśli musisz zmienić certyfikat używany przez usługi IIS dla centrum usługi ATA, wykonaj następujące czynności na serwerze centrum usługi ATA.

1.  Zainstaluj nowy certyfikat na serwerze centrum usługi ATA.

2.  Otwórz menedżera usług Internet Information Services (IIS).

3.  Rozwiń nazwę serwera i rozwiń pozycję **Witryny**..

4.  Wybierz witrynę konsoli usługi Microsoft ATA i w okienku **Akcje** kliknij pozycję **Powiązania**..

    ![Akcje powiązań konsoli usługi ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Wybierz pozycję **HTTPS** i kliknij polecenie **Edytuj**..

6.  W obszarze **Certyfikat SSL** wybierz nowy certyfikat.

7.  Pobierz pakiet instalacyjny bramy usługi ATA przed zainstalowaniem nowej bramy usługi ATA.

>[!div class="step-by-step"]
[« Adres IP konsoli usługi ATA](modifying-ata-config-consoleip.md)
[Hasło do łączności z domeną »](modifying-ata-config-dcpassword.md)

## Zobacz też
- [Praca z konsolą usługi ATA](working-with-ata-console.md)
- [Instalowanie usługi ATA](install-ata.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


