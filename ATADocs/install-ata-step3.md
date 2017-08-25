---
title: "Instalowanie usługi Advanced Threat Analytics — Krok 3 | Dokumentacja firmy Microsoft"
description: "W trzecim kroku procesu instalowania usługi ATA znajdują się informacje ułatwiające pobranie pakietu instalacyjnego bramy usługi ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/20/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 22541007bd6ebf0e37818e205bac57191ca6f28d
ms.sourcegitcommit: 129bee06ff89b72d21b64f9aa0d1a29f66bf9153
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/20/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="install-ata---step-3"></a>Instalowanie usługi ATA — Krok 3

>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Krok 3. Pobieranie pakietu instalacyjnego bramy usługi ATA
Po skonfigurowaniu ustawień łączności domeny możesz pobrać pakiet instalacyjny bramy usługi ATA. Brama usługi ATA może zostać zainstalowana na dedykowanym serwerze lub w kontrolerze domeny. Jeśli brama zostanie zainstalowana w kontrolerze domeny, będzie ona zainstalowana jako uproszczone brama usługi ATA. Więcej informacji dotyczących uproszczonej bramy usługi ATA można znaleźć w temacie [Architektura usługi ATA](ata-architecture.md). 

Kliknij pozycję Pobierz instalatora bramy na liście kroków w górnej części strony, aby przejść do strony Bramy.

![Ustawienia konfiguracji bramy usługi ATA](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Aby później uzyskać dostęp do ekranu konfiguracji bramy, kliknij **ikonę ustawień** (w prawym górnym rogu) i wybierz pozycję **Konfiguracja**, a następnie w obszarze **System** kliknij pozycję **Bramy**.  

1.  Kliknij pozycję **Instalacja bramy**.
  ![Pobieranie instalatora bramy usługi ATA](media/download-gateway-setup.png)
2.  Zapisz pakiet lokalnie.
3.  Skopiuj pakiet na dedykowany serwer lub do kontrolera domeny, w którym instalujesz bramę usługi ATA. Alternatywnie możesz otworzyć konsolę usługi ATA na dedykowanym serwerze lub kontrolerze domeny i pominąć ten krok.

Plik zip zawiera następujące składniki:

-   Instalator bramy usługi ATA

-   Plik ustawień konfiguracji z informacjami wymaganymi do nawiązywania połączeń z centrum usługi ATA


>[!div class="step-by-step"]
[« Krok 2](install-ata-step2.md)
[Krok 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Powiązane pliki wideo
- [Wybieranie odpowiedniej typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania usługi ATA fazy weryfikacji Koncepcji](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
