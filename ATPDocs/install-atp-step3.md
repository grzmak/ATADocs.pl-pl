---
title: Install Azure Zaawansowana ochrona przed zagrożeniami — krok 3 | Dokumentacja firmy Microsoft
description: Kroku procesu instalowania usługi Azure ATP pomoże Ci pobrać pakiet instalacyjny czujnik autonomiczny narzędzia Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f10dd0714b2574ff9e1e476bc1865b1a0ed337b8
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125910"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="install-azure-atp---step-3"></a>Zainstaluj narzędzie Azure ATP — krok 3

>[!div class="step-by-step"]
[« Krok 2](install-atp-step2.md)
[Krok 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Krok 3. Pobierz pakiet instalacyjny czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure
Po skonfigurowaniu ustawień łączności domeny, można pobrać pakiet instalacyjny czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Pakiet instalacyjny czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure można zainstalować na dedykowanym serwerze lub na kontrolerze domeny. Instalowanie bezpośrednio na kontrolerze domeny, jest instalowana jako czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure podczas instalowania na dedykowanym serwerze i za pomocą funkcji dublowania portów, instalowana jako czujnik autonomiczny narzędzia Azure ATP. Aby uzyskać więcej informacji na temat czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, zobacz [architektura zaawansowanej ochrony przed zagrożeniami platformy](atp-architecture.md). 

Kliknij przycisk **Pobierz** na liście kroków w górnej części strony aby przejść do **czujnik** strony.

![Ustawienia konfiguracji usługi Azure czujnika zaawansowanej ochrony przed zagrożeniami](media/atp-sensor-config.png)

> [!NOTE] 
> Aby później uzyskać dostęp do ekranu konfiguracji czujników, kliknij przycisk **ikonę ustawienia** (prawy górny róg) i wybierz **konfiguracji**, a następnie w obszarze **systemu**, kliknij przycisk **czujnik**.  

1.  Kliknij przycisk **czujnika**.
2.  Zapisz pakiet lokalnie.
3.  Kopiuj **klucz dostępu**. Klucz dostępu jest wymagany dla czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, nawiązać połączenia z obszaru roboczego usługi Azure ATP. Klucz dostępu jest jeden haseł dla wdrożenia czujnika, po którym cała komunikacja odbywa się za pomocą certyfikatów do uwierzytelniania i szyfrowania TLS. Użyj **ponownie wygenerować** przycisku Jeśli kiedykolwiek zajdzie potrzeba ponownie wygenerować nowy klucz dostępu, możesz i nie wpłynie to na wszystkie wcześniej wdrożonej czujników, ponieważ jest używana tylko dla wstępnej rejestracji czujnika.
4.  Skopiuj pakiet na dedykowany serwer lub kontroler domeny, na którym instalujesz czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Alternatywnie można otworzyć portalu obszaru roboczego usługi Azure ATP z dedykowanego serwera lub kontroler domeny i pominąć ten krok.

Plik zip zawiera następujące pliki:

-   Usługa Azure Instalatora czujnika zaawansowanej ochrony przed zagrożeniami

-   Plik ustawień konfiguracji, podając wymagane informacje, aby nawiązać połączenie z usługą w chmurze usługi Azure ATP


>[!div class="step-by-step"]
[« Krok 2](install-atp-step2.md)
[Krok 4 »](install-atp-step4.md)


## <a name="see-also"></a>Zobacz też

- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)

- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)

- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)