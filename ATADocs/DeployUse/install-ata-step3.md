---
title: "Instalacja usługi ATA — krok 3 | Microsoft ATA"
description: "W trzecim kroku procesu instalowania usługi ATA znajdują się informacje ułatwiające pobranie pakietu instalacyjnego bramy usługi ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ba090fdd4f00c001020b1fbedf527e4fd69d3992
ms.openlocfilehash: 277d08756b456d1a61fb9fdcb5014a6a1b4782ad


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# Instalowanie usługi ATA — Krok 3

>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)

## Krok 3. Pobieranie pakietu instalacyjnego bramy usługi ATA
Po skonfigurowaniu ustawień łączności domeny możesz pobrać pakiet instalacyjny bramy usługi ATA. Brama usługi ATA może zostać zainstalowana na dedykowanym serwerze lub w kontrolerze domeny. Jeśli brama zostanie zainstalowana w kontrolerze domeny, będzie ona zainstalowana jako brama ATA Lightweight Gateway. Więcej informacji dotyczących bramy ATA Lightweight Gateway można znaleźć w temacie [Architektura usługi ATA](/advanced-threat-analytics/plan-design/ata-architecture). 

Jeśli pobierasz bramę usługi ATA po raz pierwszy, zostanie wyświetlony następujący ekran:

![Ustawienia konfiguracji bramy usługi ATA](media/ATA_1.7-welcome-download-gateway.PNG)

Jeśli brama usługi ATA była już wcześniej pobierana, komunikat powitalny nie zostanie wyświetlony.

> [!NOTE] 
> Aby później uzyskać dostęp do ekranu konfiguracji, kliknij **ikonę ustawień** (w prawym górnym rogu) i wybierz pozycję **Konfiguracja**, a następnie w obszarze **System** kliknij pozycję **Bramy**.  

1.  Kliknij pozycję **Download Gateway Setup** (Pobierz konfigurację bramy).
2.  Zapisz pakiet lokalnie.
3.  Skopiuj pakiet na dedykowany serwer lub do kontrolera domeny, w którym instalujesz bramę usługi ATA. Alternatywnie możesz otworzyć konsolę usługi ATA na dedykowanym serwerze lub kontrolerze domeny i pominąć ten krok.

Plik zip zawiera następujące składniki:

-   Instalator bramy usługi ATA

-   Plik ustawień konfiguracji z informacjami wymaganymi do nawiązywania połączeń z centrum usługi ATA


>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)

## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Aug16_HO5-->


