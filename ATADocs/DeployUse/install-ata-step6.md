---
# required metadata

title: Instalowanie usługi ATA | Usługa Microsoft Advanced Threat Analytics
description: W ostatnim kroku instalowania usługi ATA można skonfigurować podsieci dzierżawy krótkoterminowej i użytkownika wystawionego jako przynęta.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalowanie usługi ATA — Krok 6

>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)

## Krok 6. Konfigurowanie podsieci dzierżawy krótkoterminowej i użytkownika wystawionego jako przynęta
Podsieci dzierżawy krótkoterminowej to podsieci, w których przypisanie adresów IP zmienia się bardzo szybko — w ciągu sekund lub minut. (Na przykład adresy IP używane dla sieci VPN i Wi-Fi). Aby wprowadzić listę podsieci dzierżawy krótkoterminowej używanych w organizacji, wykonaj następujące kroki:

1.  W konsoli usługi ATA na komputerze bramy usługi ATA kliknij ikonę ustawień i wybierz pozycję **Konfiguracja**..

    ![Ustawienia konfiguracji usługi ATA](media/ATA-config-icon.JPG)

2.  W obszarze **Wykrywanie** wprowadź następujące informacje dla podsieci dzierżawy krótkoterminowej. Wprowadź podsieci dzierżawy krótkoterminowej przy użyciu formatu notacji ukośnika, na przykład:  `192.168.0.0/24` i kliknij znak plus.

3.  Dla identyfikatorów SID kont wystawionych jako przynęta wprowadź identyfikator SID konta użytkownika, dla którego nie będzie żadnych działań w sieci, a następnie kliknij znak plus. Na przykład: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Aby znaleźć identyfikator SID użytkownika, uruchom następujące polecenie cmdlet programu Windows PowerShell `Get-ADUser UserName`.

4.  Konfigurowanie wykluczeń: można skonfigurować adresy IP, które mają być wykluczone z określonych podejrzanych działań. Zobacz [Praca z ustawieniami wykrywania usługi ATA](working-with-detection-settings.md), aby uzyskać więcej informacji.

5.  Kliknij polecenie **Zapisz**..

![Zapisz zmiany](media/ATA-VPN-Subnets.JPG)

Gratulacje, usługa Microsoft Advanced Threat Analytics została pomyślnie wdrożona!

Sprawdź wiersz czasu ataku, aby wyświetlić wykryte podejrzane działania i wyszukać użytkowników lub komputery i wyświetlić ich profile.

Należy pamiętać, że utworzenie profilów zachowania zajmuje usłudze ATA co najmniej trzy tygodnie, a więc w pierwszych trzech tygodniach nie będą widoczne żadne podejrzane działania.


>[!div class="step-by-step"]
[« Krok 5](install-ata-step5.md)


## Zobacz też

- [Aby uzyskać pomoc techniczną, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/plan-design/configure-event-collection)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Apr16_HO4-->


