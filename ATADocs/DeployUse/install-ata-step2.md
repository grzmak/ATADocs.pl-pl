---
# required metadata

title: Instalowanie usługi ATA — Krok 2 | Usługa Microsoft Advanced Threat Analytics
description: Krok drugi procedury instalowania usługi ATA pomaga skonfigurować ustawienia łączności domeny na serwerze centrum usługi ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalowanie usługi ATA — Krok 2

>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)

## Krok 2. Konfigurowanie ustawień łączności domeny bramy usługi ATA
Ustawienia w sekcji Ustawienia łączności domeny są stosowane do wszystkich bram usługi ATA zarządzanych przez centrum usługi ATA.

Aby skonfigurować ustawienia łączności domeny, wykonaj następujące czynności na serwerze centrum usługi ATA.

1.  Uruchom konsolę usługi ATA i zaloguj się. Aby uzyskać instrukcje, zobacz [Praca z konsolą usługi ATA](/advanced-threat-analytics/understand-explore/working-with-ata-console).

2.  Po pierwszym zalogowaniu do konsoli usługi ATA po zainstalowaniu centrum usługi ATA nastąpi automatyczne przejście na stronę konfiguracji bram usługi ATA. Jeśli któreś z ustawień trzeba później zmodyfikować, kliknij ikonę Ustawienia, a następnie wybierz opcję **Konfiguracja**.

    ![Ustawienia konfiguracji bramy usługi ATA](media/ATA-config-icon.JPG)

3.  Na stronie **Brama** kliknij pozycję **Ustawienia łączności domeny**, wprowadź następujące informacje i kliknij przycisk **Zapisz**.

    |Pole|Komentarze|
    |---------|------------|
    |**Nazwa użytkownika** (wymagana)|Wprowadź nazwę użytkownika tylko do odczytu, na przykład: **użytkownik1**.|
    |**Hasło** (wymagane)|Wprowadź hasło użytkownika tylko do odczytu, na przykład: **Rysik1**. **Uwaga:** Upewnij się, że to hasło jest prawidłowe. Jeśli zapiszesz nieprawidłowe hasło, usługa ATA przestanie działać na serwerach bramy usługi ATA.|
    |**Domena** (wymagana)|Wprowadź domenę użytkownika tylko do odczytu, na przykład **contoso.com**. **Uwaga:** należy wprowadzić pełną nazwę FQDN domeny, w której znajduje się użytkownik. Na przykład jeśli konto użytkownika znajduje się w domenie corp.contoso.com, należy wprowadzić `corp.contoso.com` not contoso.com|
    ![Obraz ustawień łączności domeny usługi ATA](media/ATA-Domain-Connectivity-User.JPG)


>[!div class="step-by-step"]
[« Krok 1](install-ata-step1.md)
[Krok 3 »](install-ata-step3.md)


## Zobacz też

- [Aby uzyskać pomoc techniczną, skorzystaj z naszego forum](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/plan-design/configure-event-collection)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Apr16_HO4-->


