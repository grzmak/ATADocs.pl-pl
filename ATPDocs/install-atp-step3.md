---
title: "Azure instalacji Advanced Threat Protection — krok 3 | Dokumentacja firmy Microsoft"
description: "W trzecim kroku procesu instalowania Azure ATP ułatwia pobrać pakiet instalacyjny czujnik autonomiczny Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: aa07d6ce4418c051362652e70968a8e41313affb
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-3"></a>Zainstaluj Azure ATP — krok 3

>[!div class="step-by-step"]
[« Krok 2](install-atp-step2.md)
[Krok 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Krok 3. Pobierz pakiet instalacyjny czujnik Azure ATP
Po skonfigurowaniu ustawień łączności domeny, można pobrać pakiet instalacyjny czujnik Azure ATP. Pakiet instalacyjny czujnik Azure ATP można zainstalować na dedykowanym serwerze lub na kontrolerze domeny. Instalowanie bezpośrednio na kontrolerze domeny, jest instalowana jako czujnik Azure ATP podczas instalowania na dedykowanym serwerze i za pomocą funkcji dublowania portów, jest zainstalowany jako czujnik autonomiczny Azure ATP. Aby uzyskać więcej informacji na czujnik Azure ATP, zobacz [architektura ATP Azure](atp-architecture.md). 

Kliknij przycisk **Pobierz** na liście kroków w górnej części strony, aby przejść do **czujnik** strony.

![Ustawienia konfiguracji czujnik w usłudze Azure ATP](media/atp-sensor-config.png)

> [!NOTE] 
> Aby otrzymać na ekranie konfiguracji czujnik później, kliknij przycisk **ikonę ustawień** (prawym górnym rogu) i wybierz **konfiguracji**, następnie w obszarze **systemu**, kliknij przycisk **czujnik**.  

1.  Kliknij przycisk **czujnik**.
2.  Zapisz pakiet lokalnie.
3.  Kopiuj **klucz dostępu**. Klucz dostępu jest wymagany dla czujnika Azure ATP nawiązać połączenia z obszaru roboczego Azure ATP. Klucz dostępu jest jednorazowe haseł dla wdrożenia czujnika, po którym cała komunikacja odbywa się przy użyciu certyfikatów do uwierzytelniania i szyfrowania TLS. Użyj **ponownie wygenerować** przycisku Jeśli kiedykolwiek zajdzie potrzeba ponownie wygenerować nowy klucz dostępu, możesz i nie ma wpływ na wszystkie wcześniej wdrożone czujników, ponieważ jest używana tylko do pierwszej rejestracji czujnika.
4.  Skopiuj pakiet na dedykowany serwer lub kontroler domeny, na którym instalujesz czujnik Azure ATP. Alternatywnie można otworzyć portalu Azure ATP obszaru roboczego z dedykowanym serwerze lub kontrolerze domeny i pominąć ten krok.

Plik zip zawiera następujące pliki:

-   Azure Instalator czujnik ATP

-   Plik ustawień konfiguracji z informacje wymagane do nawiązania połączenia usługi w chmurze Azure ATP


>[!div class="step-by-step"]
[« Krok 2](install-atp-step2.md)
[Krok 4 »](install-atp-step4.md)


## <a name="see-also"></a>Zobacz też

- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)

- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)