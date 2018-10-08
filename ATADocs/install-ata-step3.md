---
title: Instalowanie usługi Advanced Threat Analytics — Krok 3 | Dokumentacja firmy Microsoft
description: W trzecim kroku procesu instalowania usługi ATA znajdują się informacje ułatwiające pobranie pakietu instalacyjnego bramy usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d49770f435985027690ddfc05a9359e84841c0ff
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454041"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="install-ata---step-3"></a>Instalowanie usługi ATA — Krok 3

> [!div class="step-by-step"]
> [« Krok 2](install-ata-step2.md)
> [Krok 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Krok 3. Pobieranie pakietu instalacyjnego bramy usługi ATA
Po skonfigurowaniu ustawień łączności z domeną możesz pobrać pakiet instalacyjny bramy usługi ATA. Brama usługi ATA może zostać zainstalowana na dedykowanym serwerze lub na kontrolerze domeny. Jeśli brama zostanie zainstalowana na kontrolerze domeny, to jest instalowana jako uproszczona brama usługi ATA. Więcej informacji dotyczących uproszczonej bramy usługi ATA można znaleźć w temacie [Architektura usługi ATA](ata-architecture.md).

Kliknij przycisk **Pobierz instalatora bramy** na liście kroków w górnej części strony, aby przejść do strony dotyczącej **bram**.

![Ustawienia konfiguracji bramy usługi ATA](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Aby później uzyskać dostęp do ekranu konfiguracji bramy, kliknij **ikonę ustawień** (w prawym górnym rogu) i wybierz pozycję **Konfiguracja**, a następnie w obszarze **System** kliknij pozycję **Bramy**.  

1.  Kliknij pozycję **Instalacja bramy**.
  ![Pobieranie instalatora bramy usługi ATA](media/download-gateway-setup.png)
2.  Zapisz pakiet lokalnie.
3.  Skopiuj pakiet na dedykowany serwer lub do kontrolera domeny, w którym instalujesz bramę usługi ATA. Alternatywnie możesz otworzyć konsolę usługi ATA na dedykowanym serwerze lub kontrolerze domeny i pominąć ten krok.

Plik zip zawiera następujące pliki:

-   Instalator bramy usługi ATA

-   Plik ustawień konfiguracji z informacjami wymaganymi do nawiązywania połączeń z centrum usługi ATA


> [!div class="step-by-step"]
> [« Krok 2](install-ata-step2.md)
> [Krok 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Pokrewne wideo
- [Omówienie wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniego typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania weryfikacji Koncepcji usługi ATA](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
