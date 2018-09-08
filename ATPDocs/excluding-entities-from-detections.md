---
title: Wykluczanie jednostek z wykryć w usłudze Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: W tym artykule opisano jak zatrzymać usługi Azure ATP z wykrywanie określonych działań jednostek jako podejrzanych
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/2/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d5ac2ae53dfe13b850a06f6dd4b89a91ffedd946
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166038"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="excluding-entities-from-detections"></a>Wykluczanie jednostek z wykryć
W tym artykule wyjaśniono, jak wykluczać jednostki z procesu wyzwalania alertów, aby zminimalizować niegroźne prawdziwie dodatnie, ale w tym samym czasie, upewnij się, że catch prawdziwie dodatnich. Aby zachować narzędzia Azure ATP miałyby alertów dotyczących działań, które od określonych użytkowników, może być częścią zwykłej działalności biznesowej, możesz wyciszyć — lub wykluczyć — pewne jednostki z procesu zgłaszania alertów.

Na przykład masz skaner zabezpieczeń, który przeprowadza rekonesans systemu DNS, lub administratora, który zdalnie uruchamia skrypty na kontrolerze domeny — i są to oficjalnie zaakceptowane działania przeprowadzane w ramach normalnych operacji IT w Twojej organizacji. Aby uzyskać więcej informacji na temat wykrywania usługi Azure ATP ułatwią podjęcie decyzji o których jednostek do wykluczenia, zobacz [Przewodnik po podejrzanych działań](suspicious-activity-guide.md).

Aby wykluczyć jednostki z procesu zgłaszania alertów w usłudze Azure ATP:

Istnieją dwa sposoby wykluczania jednostek: na poziomie podejrzanego działania lub na karcie **Wykluczenia** na stronie **Konfiguracja**.

- **Na poziomie podejrzanego działania**: na osi czasu działania, gdy otrzymasz alert dotyczący działania dla użytkownika lub komputera lub adres IP, który może wykonywać dane działanie i mogą to zrobić, kliknij prawym przyciskiem myszy trzy kropki znajdujące się na koniec wiersza podejrzanego działania w tej jednostce, a następnie wybierz pozycję **Zamknij i Wyklucz**. <br></br>Spowoduje to dodanie użytkownika, komputera lub adres IP do listy wykluczeń dla danego podejrzanego działania. Zamknięcie podejrzanego działania i nie jest już wyświetlany w **Otwórz** liście zdarzeń **osi czasu podejrzanych działań**.

    ![Wykluczanie jednostki](./media/exclude-in-sa.png)

- **Na stronie Konfiguracja**: Aby przejrzeć lub zmodyfikować jakichkolwiek wykluczeń: w obszarze **konfiguracji**, kliknij przycisk **wykluczenia** , a następnie wybierz podejrzane działanie, takie jak **DNS Rekonesans**.

    ![Konfiguracja wykluczeń](./media/exclusions.png)

Aby dodać jednostkę z **wykluczenia** konfiguracji: Wprowadź nazwę jednostki, a następnie kliknij znak plusa, a następnie kliknij **Zapisz** w dolnej części strony.

Aby usunąć jednostkę z konfiguracji **Wykluczenia**: kliknij znak minus obok nazwy jednostki, a następnie kliknij pozycję **Zapisz** w dolnej części strony.

Dodawanie wykluczeń do wykryć jest zalecane tylko wtedy, gdy otrzymujesz alerty danego typu i określasz, że są one niegroźne prawdziwie dodatnie. 

> [!NOTE]
> Ze względów bezpieczeństwa nie wszystkie wykrycia oferują możliwość ustawienia wykluczeń. 

Niektóre wykrycia udostępniają porady, które pomogą Ci w wyborze jednostek do wykluczenia. 

Każde wykluczenie zależy od kontekstu, w niektórych można ustawić użytkowników, a inne można ustawić komputerów lub adresy IP. 

Jeśli masz możliwości wyłączenia komputera lub adres IP, można wykluczyć jednego lub drugiego — nie należy podać oba.

> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi Azure ATP.


## <a name="see-also"></a>Zobacz też

- [Integracja z usługą Windows Defender ATP](integrate-wd-atp.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)