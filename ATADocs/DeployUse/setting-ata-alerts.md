---
title: "Ustawianie powiadomień usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób ustawiania alertów usługi ATA w celu otrzymywania powiadomień o wykryciu podejrzanych działań."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 782c066e6a7ef8a5da9e2b8ceb16742da6f52506


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="set-ata-notifications"></a>Ustawianie powiadomień usługi ATA
Usługa ATA może wysyłać powiadomienia w przypadku wykrycia podejrzanych działań za pośrednictwem poczty e-mail lub przy użyciu funkcji przekazywania zdarzeń usługi ATA, przekazując zdarzenia do serwera SIEM/Syslog. Zanim określisz, które powiadomienia chcesz otrzymywać, musisz [skonfigurować serwer poczty e-mail i serwer Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Powiadomienia e-mail zawierają link powodujący otwarcie informacji o podejrzanym działaniu, które zostało wykryte. Część linku zawierająca nazwę hosta jest pobierana z ustawienia adresu URL konsoli usługi ATA na stronie centrum usługi ATA. Domyślnie adres URL konsoli usługi ATA jest adresem IP wybranym podczas instalacji centrum usługi ATA.  Zalecane jest użycie nazwy FQDN jako adresu URL konsoli usługi ATA w celu skonfigurowania powiadomień e-mail.
> -   Powiadomienia są wysyłane z centrum usługi ATA do serwera SMTP i serwera Syslog.

## <a name="mail-notifications"></a>Powiadomienia pocztowe
Aby otrzymywać powiadomienia pocztowe, określ następujące ustawienia:


1. Na pasku narzędzi w konsoli usługi ATA wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.
![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

2. W obszarze **Powiadomienia** wybierz pozycję **Ustawienia**.
3. W obszarze **Adresaci poczty** określ adresatów, którzy będą otrzymywać powiadomienia pocztą e-mail.
>   [!NOTE]
>   Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.

4. W obszarze **Powiadom gdy:** użyj przełączników, aby wybrać powiadomienia, które mają być wysyłane:
  - Wykryto nowe podejrzane działanie
  - Wykryto nowy problem z kondycją
  - Dostępna jest nowa aktualizacja oprogramowania

5. Kliknij polecenie **Zapisz**.

![Obraz ustawień powiadomień pocztowych usługi ATA](media/ATA-mail-notification-settings-1.7.png)


## <a name="syslog-notification"></a>Powiadomienie Syslog

Aby otrzymywać powiadomienia Syslog, określ następujące ustawienia:


1. Na pasku narzędzi w konsoli usługi ATA wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.
![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.JPG)

2. W obszarze **Powiadomienia** wybierz pozycję **Ustawienia**.
3. W obszarze **Powiadomienia Syslog** użyj przełączników, aby wybrać powiadomienia, które mają być wysyłane:


    - Wykryto nowe podejrzane działanie
    - Zaktualizowano istniejące podejrzane działanie
    - Wykryto nowy problem z kondycją
5. Kliknij polecenie **Zapisz**.

![Ilustracja ustawień powiadomień usługi ATA](media/ATA-syslog-notification-settings-1.7.png)




## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


