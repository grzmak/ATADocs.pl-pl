---
title: Wykluczanie jednostek wykryć Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opisuje sposób zatrzymania Azure ATP z Wykrywanie podejrzanych działań określonej jednostki
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 60a2fae0ef044993786fb3b7e2d21a3ac27bb9f0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446029"
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="excluding-entities-from-detections"></a>Wykluczanie jednostek z wykryć
W tym artykule opisano sposób wykluczanie jednostek z wyzwalania alertów, aby zminimalizować alarmów niegroźne wartość true, ale w tym samym czasie, upewnij się, że catch alarmów wartość true. Aby zachować Azure ATP przed generujące dużo alertów dotyczących działań, które z określonych użytkowników, może być częścią Twojego normalne tempie firm, można quiet — lub wykluczyć - konkretnych obiektów zbierania alertów.

Na przykład masz skaner zabezpieczeń, który przeprowadza rekonesans systemu DNS, lub administratora, który zdalnie uruchamia skrypty na kontrolerze domeny — i są to oficjalnie zaakceptowane działania przeprowadzane w ramach normalnych operacji IT w Twojej organizacji. Aby uzyskać więcej informacji na temat wykryć Azure ATP, aby określić którymi obiektami, które mają zostać wykluczone, zobacz [przewodnik podejrzanych działań](suspicious-activity-guide.md).

Aby wykluczyć jednostki zbierania alertów w usłudze Azure ATP:

Istnieją dwa sposoby wykluczania jednostek: na poziomie podejrzanego działania lub na karcie **Wykluczenia** na stronie **Konfiguracja**.

- **Podejrzane działania**: W podejrzane osi czasu działania po otrzymaniu alertu w działaniu dla użytkownika lub komputera lub adres IP, który może wykonać określone działanie i mogą to zrobić, kliknij prawym przyciskiem myszy trzy kropki znajdujące się na koniec wiersza dla podejrzanych działań w jednostki, a następnie wybierz **Zamknij i Wyklucz**. <br></br>Spowoduje to dodanie użytkownika, komputera lub adres IP do listy wykluczeń dla danego podejrzane działania. Zamyka podejrzanego działania i nie jest już wyświetlany w **Otwórz** listę zdarzeń w **osi czasu podejrzanych działań**.

    ![Wykluczanie jednostki](./media/exclude-in-sa.png)

- **Na stronie konfiguracji**: można przeglądać lub modyfikować wszelkie wyjątki: w obszarze **konfiguracji**, kliknij przycisk **wykluczenia** , a następnie wybierz podejrzanych działań, takich jak **DNS Rekonesans**.

    ![Konfiguracja wykluczeń](./media/exclusions.png)

Aby dodać jednostkę z **wykluczenia** konfiguracji: Wprowadź nazwę jednostki, a następnie kliknij przycisk plus, a następnie kliknij **zapisać** w dolnej części strony.

Aby usunąć jednostkę z konfiguracji **Wykluczenia**: kliknij znak minus obok nazwy jednostki, a następnie kliknij pozycję **Zapisz** w dolnej części strony.

Dodawanie wykluczeń do wykryć jest zalecane tylko wtedy, gdy otrzymujesz alerty danego typu i określasz, że są one niegroźne prawdziwie dodatnie. 

> [!NOTE]
> Ze względów bezpieczeństwa nie wszystkie wykrycia oferują możliwość ustawienia wykluczeń. 

Niektóre wykrycia udostępniają porady, które pomogą Ci w wyborze jednostek do wykluczenia. 

Każdy wykluczeń zależy od kontekstu, w niektórych można ustawić użytkowników, gdy inne można ustawić komputerów lub adresy IP. 

Jeśli masz możliwości wyłączenia adresu IP lub na komputerze, można wykluczyć jednego lub drugiego — nie musisz podać obie.

> [!NOTE]
> Strony konfiguracji może zostać zmodyfikowany tylko przez administratorów Azure ATP.


## <a name="see-also"></a>Zobacz też

- [Integrowanie z usługi Windows Defender ATP](integrate-wd-atp.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)