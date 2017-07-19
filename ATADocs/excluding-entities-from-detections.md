---
title: "Wykluczanie jednostek z wykryć w usłudze Advanced Threat Analytics | Microsoft Docs"
description: "Opisuje, jak uniemożliwić usłudze ATA wykrywanie określonych działań jednostek jako podejrzanych"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/9/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ff60b026c754a27da62c01ce6c551d206338ef4e
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="excluding-entities-from-detections"></a>Wykluczanie jednostek z wykryć
W tym temacie wyjaśniono, jak wykluczać jednostki z procesu wyzwalania alertów w celu zminimalizowania zapytań niegroźnych prawdziwie dodatnich, zapewniając równocześnie wychwycenie zapytań prawdziwie dodatnich. Aby usługa ATA nie generowała niepotrzebnych alertów dotyczących działań, które w przypadku niektórych użytkowników mogą być częścią zwykłej działalności biznesowej, możesz wyciszyć — lub wykluczyć — pewne jednostki z procesu zgłaszania alertów.

Na przykład masz skaner zabezpieczeń, który przeprowadza rekonesans systemu DNS, lub administratora, który zdalnie uruchamia skrypty na kontrolerze domeny — i są to oficjalnie zaakceptowane działania przeprowadzane w ramach normalnych operacji IT w Twojej organizacji.

Aby wykluczyć jednostki z procesu zgłaszania alertów w usłudze ATA:

Istnieją dwa sposoby wykluczania jednostek: na poziomie podejrzanego działania lub na karcie **Wykluczenia** na stronie **Konfiguracja**.

- **Na poziomie podejrzanego działania**: gdy otrzymasz alert dotyczący działania dla użytkownika, komputera lub adresu IP, które mogą wykonywać dane działanie i mogą wykonywać je często, na osi czasu podejrzanych działań kliknij prawym przyciskiem myszy trzy kropki na końcu wiersza podejrzanego działania danej jednostki, a następnie wybierz pozycję **Zamknij i wyklucz**. <br></br>Spowoduje to dodanie użytkownika, komputera lub adresu IP do listy wykluczeń dla danego podejrzanego działania. Ponadto podejrzane działanie zostanie zamknięte i nie będzie już wyświetlane na liście zdarzeń **Otwarte** na **osi czasu podejrzanych działań**.

    ![Wykluczanie jednostki](./media/exclude-in-sa.png)

- **Na stronie Konfiguracja**: aby przejrzeć lub zmodyfikować ustawione wykluczenia, w obszarze **Konfiguracja** kliknij pozycję **Wykluczenia**, a następnie wybierz podejrzane działanie, takie jak **Ujawnione poufne poświadczenia konta**.

    ![Konfiguracja wykluczeń](./media/exclusions-config-page.png)

Aby usunąć jednostkę z konfiguracji **Wykluczenia**: kliknij znak minus obok nazwy jednostki, a następnie kliknij pozycję **Zapisz** w dolnej części strony.

Dodawanie wykluczeń do wykryć jest zalecane tylko wtedy, gdy otrzymujesz alerty danego typu i określasz, że są one niegroźne prawdziwie dodatnie. 

> [!NOTE]
> Ze względów bezpieczeństwa nie wszystkie wykrycia oferują możliwość ustawienia wykluczeń. 

Niektóre wykrycia udostępniają porady, które pomogą Ci w wyborze jednostek do wykluczenia. 

Każde wykluczenie zależy od kontekstu. W niektórych można ustawić użytkowników, a w innych — komputery lub adresy IP. 

Jeśli masz możliwość wykluczenia adresu IP lub komputera, możesz wykluczyć jeden lub drugi element — nie musisz wybierać obydwu.

> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi ATA.


## <a name="see-also"></a>Zobacz też
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-center-configuration.md)
