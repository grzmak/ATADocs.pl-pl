---
title: "Wykluczanie jednostek z wykryć w usłudze Advanced Threat Analytics | Microsoft Docs"
description: "Opisuje, jak uniemożliwić usłudze ATA wykrywanie określonych działań jednostek jako podejrzanych"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 21b1d8a4537bb77de120dac4b2f15bc785161749
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="excluding-entities-from-detections"></a>Wykluczanie jednostek z wykryć
W tym artykule opisano sposób wykluczanie jednostek z wyzwalania alertów, aby zminimalizować alarmów niegroźne wartość true, ale w tym samym czasie, upewnij się, że catch alarmów wartość true. Aby zapewnić usługi ATA przed generujące dużo alertów dotyczących działań, które z określonych użytkowników, może być częścią Twojego normalne tempie firm, można quiet — lub wykluczyć - konkretnych obiektów zbierania alertów.

Na przykład masz skaner zabezpieczeń, który przeprowadza rekonesans systemu DNS, lub administratora, który zdalnie uruchamia skrypty na kontrolerze domeny — i są to oficjalnie zaakceptowane działania przeprowadzane w ramach normalnych operacji IT w Twojej organizacji.

Aby wykluczyć jednostki z procesu zgłaszania alertów w usłudze ATA:

Istnieją dwa sposoby wykluczania jednostek: na poziomie podejrzanego działania lub na karcie **Wykluczenia** na stronie **Konfiguracja**.

- **Podejrzane działania**: W podejrzane działania osi czasu, gdy zostanie wyświetlony alert w działaniu dla użytkownika lub komputera lub adres IP, który może wykonać określone działanie i mogą to zrobić, kliknij prawym przyciskiem myszy trzy kropki znajdujące się na koniec wiersza dla podejrzanych działań w jednostki, a następnie wybierz **Zamknij i Wyklucz**. <br></br>Spowoduje to dodanie użytkownika, komputera lub adres IP do listy wykluczeń dla danego podejrzane działania. Zamyka podejrzanego działania i nie jest już wyświetlany w **Otwórz** listę zdarzeń w **osi czasu podejrzanych działań**.

    ![Wykluczanie jednostki](./media/exclude-in-sa.png)

- **Na stronie konfiguracji**: można przeglądać lub modyfikować wszelkie wyjątki: w obszarze **konfiguracji**, kliknij przycisk **wykluczenia** , a następnie wybierz podejrzanych działań, takich jak  **Poufne konto poświadczeniami ujawnionymi**.

    ![Konfiguracja wykluczeń](./media/exclusions-config-page.png)

Aby usunąć jednostkę z konfiguracji **Wykluczenia**: kliknij znak minus obok nazwy jednostki, a następnie kliknij pozycję **Zapisz** w dolnej części strony.

Dodawanie wykluczeń do wykryć jest zalecane tylko wtedy, gdy otrzymujesz alerty danego typu i określasz, że są one niegroźne prawdziwie dodatnie. 

> [!NOTE]
> Ze względów bezpieczeństwa nie wszystkie wykrycia oferują możliwość ustawienia wykluczeń. 

Niektóre wykrycia udostępniają porady, które pomogą Ci w wyborze jednostek do wykluczenia. 

Każdy wykluczeń zależy od kontekstu, w niektórych można ustawić użytkowników, gdy inne można ustawić komputerów lub adresy IP. 

Jeśli masz możliwości wyłączenia adresu IP lub na komputerze, można wykluczyć jednego lub drugiego — nie musisz podać obie.

> [!NOTE]
> Strony konfiguracji mogą być modyfikowane tylko przez administratorów usługi ATA.


## <a name="see-also"></a>Zobacz też
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modyfikowanie konfiguracji usługi ATA](modifying-ata-center-configuration.md)
