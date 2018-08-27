---
title: Ustawianie powiadomień usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób ustawiania alertów usługi ATA w celu otrzymywania powiadomień o wykryciu podejrzanych działań.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 60e02ef1aff6b16bc56b12b8883ca2f5ed4a1f74
ms.sourcegitcommit: ad83eaba24d5a6af465351291ba0e423319f78d3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/24/2018
ms.locfileid: "42903910"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="set-ata-notifications"></a>Ustawianie powiadomień usługi ATA
Usługa ATA może wysyłać powiadomienia w przypadku wykrycia podejrzanych działań za pośrednictwem poczty e-mail lub przy użyciu funkcji przekazywania zdarzeń usługi ATA, przekazując zdarzenia do serwera SIEM/Syslog. Zanim określisz, które powiadomienia chcesz otrzymywać, musisz [skonfigurować serwer poczty e-mail i serwer Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Powiadomienia e-mail zawierają link umożliwiający przejście użytkownika bezpośrednio do podejrzanego działania, które zostało wykryte. Część linku zawierająca nazwę hosta jest pobierana z ustawienia adresu URL konsoli usługi ATA na stronie centrum usługi ATA. Domyślnie adres URL konsoli usługi ATA jest adresem IP wybranym podczas instalacji centrum usługi ATA. Jeśli zamierzasz skonfigurować powiadomienia e-mail, zalecane jest użycie nazwy FQDN jako adresu URL konsoli usługi ATA.
> -   Powiadomienia są wysyłane z centrum usługi ATA do serwera SMTP i serwera Syslog.


Aby otrzymywać powiadomienia, ustaw następujące parametry:


1. Na pasku narzędzi w konsoli usługi ATA wybierz opcję ustawień, a następnie wybierz pozycję **Konfiguracja**.
    
    ![Ikona ustawień konfiguracji usługi ATA](media/ATA-config-icon.png)
    
1. W sekcji **Powiadomienia i raporty** wybierz pozycję **Powiadomienia**.
1. W obszarze **Powiadomienia pocztowe** określ powiadomienia, które mają być wysyłane za pośrednictwem poczty e-mail — nowe podejrzane działania i nowe problemy dotyczące kondycji. Dla podejrzanych działań i dla alertów dotyczących kondycji można ustawić osobne adresy e-mail, aby na przykład powiadomienia o podejrzanych działaniach były wysyłane do analityka ds. zabezpieczeń, a powiadomienia o alertach dotyczących problemów z kondycją — do administratora IT.
    >   [!NOTE]
    >   Alerty e-mail dotyczące podejrzanych działań są wysyłane wyłącznie po utworzeniu podejrzanego działania.
1. W obszarze **powiadomienia Syslog**, określ powiadomienia, które mają być wysyłane do serwera Syslog — nowe podejrzane działania, zaktualizowane podejrzane działania i nowe problemy dotyczące kondycji.
1. Kliknij polecenie **Zapisz**.
    
    ![Obraz ustawień powiadomień pocztowych usługi ATA](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
