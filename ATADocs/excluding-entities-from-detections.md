---
title: Wykluczanie jednostek z wykryć w usłudze Advanced Threat Analytics | Microsoft Docs
description: Opisuje, jak uniemożliwić usłudze ATA wykrywanie określonych działań jednostek jako podejrzanych
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e15a4ab34b0389b2c69d8cdf2e5ac04771a24fc9
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165783"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="excluding-entities-from-detections"></a>Wykluczanie jednostek z wykryć
W tym artykule wyjaśniono, jak wykluczać jednostki z procesu wyzwalania alertów, aby zminimalizować niegroźne prawdziwie dodatnie, ale w tym samym czasie, upewnij się, że catch prawdziwie dodatnich. Aby usługa ATA generowała alertów dotyczących działań, które od określonych użytkowników, może być częścią zwykłej działalności biznesowej, możesz wyciszyć — lub wykluczyć — pewne jednostki z procesu zgłaszania alertów.

Na przykład masz skaner zabezpieczeń, który przeprowadza rekonesans systemu DNS, lub administratora, który zdalnie uruchamia skrypty na kontrolerze domeny — i są to oficjalnie zaakceptowane działania przeprowadzane w ramach normalnych operacji IT w Twojej organizacji.

Aby wykluczyć jednostki z procesu zgłaszania alertów w usłudze ATA:

Istnieją dwa sposoby wykluczania jednostek: na poziomie podejrzanego działania lub na karcie **Wykluczenia** na stronie **Konfiguracja**.

- **Na poziomie podejrzanego działania**: W osi czasu, gdy otrzymasz alert dotyczący działania dla użytkownika lub komputera lub adres IP, który może wykonywać dane działanie i mogą to zrobić, kliknij prawym przyciskiem myszy trzy kropki znajdujące się na koniec wiersza podejrzanego działania w tej jednostce, a następnie wybierz pozycję **Zamknij i Wyklucz**. <br></br>Spowoduje to dodanie użytkownika, komputera lub adres IP do listy wykluczeń dla danego podejrzanego działania. Zamknięcie podejrzanego działania i nie jest już wyświetlany w **Otwórz** liście zdarzeń **osi czasu podejrzanych działań**.

    ![Wykluczanie jednostki](./media/exclude-in-sa.png)

- **Na stronie Konfiguracja**: Aby przejrzeć lub zmodyfikować jakichkolwiek wykluczeń: w obszarze **konfiguracji**, kliknij przycisk **wykluczenia** , a następnie wybierz podejrzane działanie, takie jak  **Ujawniono poufne poświadczenia konta**.

    ![Konfiguracja wykluczeń](./media/exclusions-config-page.png)

Aby usunąć jednostkę z konfiguracji **Wykluczenia**: kliknij znak minus obok nazwy jednostki, a następnie kliknij pozycję **Zapisz** w dolnej części strony.

Dodawanie wykluczeń do wykryć jest zalecane tylko wtedy, gdy otrzymujesz alerty danego typu i określasz, że są one niegroźne prawdziwie dodatnie. 

> [!NOTE]
> Ze względów bezpieczeństwa nie wszystkie wykrycia oferują możliwość ustawienia wykluczeń. 

Niektóre wykrycia udostępniają porady, które pomogą Ci w wyborze jednostek do wykluczenia. 

Każde wykluczenie zależy od kontekstu, w niektórych można ustawić użytkowników, a inne można ustawić komputerów lub adresy IP. 

Jeśli masz możliwości wyłączenia komputera lub adres IP, można wykluczyć jednego lub drugiego — nie należy podać oba.

> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi ATA.


## <a name="see-also"></a>Zobacz też
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-center-configuration.md)
