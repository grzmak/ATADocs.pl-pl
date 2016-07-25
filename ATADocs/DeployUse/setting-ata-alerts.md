---
title: "Ustawianie powiadomień usługi ATA | Microsoft ATA"
description: "W tym artykule opisano sposób ustawiania alertów usługi ATA w celu otrzymywania powiadomień o wykryciu podejrzanych działań."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 03f6f184e7f34d6985103f503b8d88a3fc820c18


---

# Ustawianie powiadomień usługi ATA
Usługa ATA może wysyłać powiadomienia w przypadku wykrycia podejrzanych działań za pośrednictwem poczty e-mail lub przy użyciu funkcji przekazywania zdarzeń usługi ATA, przekazując zdarzenia do serwera SIEM/Syslog. Zanim określisz, które powiadomienia chcesz otrzymywać, musisz [skonfigurować serwer poczty e-mail i serwer Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Powiadomienia e-mail zawierają link powodujący otwarcie informacji o podejrzanym działaniu, które zostało wykryte. Część linku zawierająca nazwę hosta jest pobierana z ustawienia adresu URL konsoli usługi ATA na stronie centrum usługi ATA. Domyślnie adres URL konsoli usługi ATA jest adresem IP wybranym podczas instalacji centrum usługi ATA.  Zalecane jest użycie nazwy FQDN jako adresu URL konsoli usługi ATA w celu skonfigurowania powiadomień e-mail.
> -   Powiadomienia są wysyłane z centrum usługi ATA do serwera SMTP i serwera Syslog.

Aby otrzymywać powiadomienia e-mail, określ następujące ustawienia:


1. Na pasku narzędzi w konsoli usługi ATA wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.
![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

2. Wybierz pozycję **Powiadomienia**.
3. W obszarze **Powiadomienia e-mail** użyj przełączników, aby wybrać powiadomienia, które mają być wysyłane:


    - Wykryto nowe podejrzane działanie
    - Wykryto nowy problem z kondycją
    - Dostępna jest nowa aktualizacja oprogramowania

4. Określ adresatów, którzy będą otrzymywać powiadomienia pocztą e-mail.

    [!Uwaga:] Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.


5. Kliknij polecenie **Zapisz**.

Aby otrzymywać powiadomienia Syslog, określ następujące ustawienia:


1. Na pasku narzędzi w konsoli usługi ATA wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.
![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

2. Wybierz pozycję **Powiadomienia**.
3. W obszarze **Powiadomienia Syslog** użyj przełączników, aby wybrać powiadomienia, które mają być wysyłane:


    - Wykryto nowe podejrzane działanie
    - Zaktualizowano istniejące podejrzane działanie
    - Wykryto nowy problem z kondycją
5. Kliknij polecenie **Zapisz**.
![Ilustracja ustawień powiadomień usługi ATA](media/ATA-notification-settings.png)




## Zobacz też
[Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


