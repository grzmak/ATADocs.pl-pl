---
title: "Ustawianie powiadomień usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób ustawiania alertów usługi ATA w celu otrzymywania powiadomień o wykryciu podejrzanych działań."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 11692b6c61c2a06b338615fbf1ad83ace2fae419
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/06/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="set-ata-notifications"></a>Ustawianie powiadomień usługi ATA
Usługa ATA może wysyłać powiadomienia w przypadku wykrycia podejrzanych działań za pośrednictwem poczty e-mail lub przy użyciu funkcji przekazywania zdarzeń usługi ATA, przekazując zdarzenia do serwera SIEM/Syslog. Zanim określisz, które powiadomienia chcesz otrzymywać, musisz [skonfigurować serwer poczty e-mail i serwer Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Powiadomienia e-mail zawierają link powodujący otwarcie informacji o podejrzanym działaniu, które zostało wykryte. Część linku zawierająca nazwę hosta jest pobierana z ustawienia adresu URL konsoli usługi ATA na stronie centrum usługi ATA. Domyślnie adres URL konsoli usługi ATA jest adresem IP wybranym podczas instalacji centrum usługi ATA.  Zalecane jest użycie nazwy FQDN jako adresu URL konsoli usługi ATA w celu skonfigurowania powiadomień e-mail.
> -   Powiadomienia są wysyłane z centrum usługi ATA do serwera SMTP i serwera Syslog.


Aby otrzymywać powiadomienia, określ następujące ustawienia:


1. Na pasku narzędzi w konsoli usługi ATA wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.

![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.png)

2. W sekcji **Powiadomienia i raporty** wybierz pozycję **Powiadomienia**.
3. W obszarze **Powiadomienia pocztowe** określ powiadomienia, które mają być wysyłane za pośrednictwem poczty e-mail — nowe podejrzane działania i nowe problemy dotyczące kondycji. Dla podejrzanych działań i dla alertów dotyczących kondycji można ustawić osobne adresy e-mail, aby na przykład powiadomienia o podejrzanych działaniach były wysyłane do analityka ds. zabezpieczeń, a powiadomienia o alertach dotyczących problemów z kondycją — do administratora IT.
>   [!NOTE]
>   Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.
3. W obszarze **Powiadomienia Syslog** określ powiadomienia, które mają być wysyłane do serwera usługi Syslog — nowe podejrzane działania, zaktualizowane podejrzane działania i nowe problemy dotyczące kondycji.
5. Kliknij polecenie **Zapisz**.

![Obraz ustawień powiadomień pocztowych usługi ATA](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
