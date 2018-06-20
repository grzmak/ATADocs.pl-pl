---
title: Praca z raportami Azure ATP | Dokumentacja firmy Microsoft
description: Opisuje sposób generowania raportów w ATP Azure do monitorowania sieci.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8d9c7f9208ce76e6c2ca915729b9c64f769ae7bd
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202293"
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="azure-atp-reports"></a>Raporty Azure ATP

Sekcji raportów Azure ATP w portalu obszaru roboczego można generować raporty, które udostępniają informacje o stanie systemu, wykryte zarówno kondycji systemu, jak i raport o podejrzanych działań w danym środowisku.


Aby uzyskać dostęp do strony raportów, kliknij ikonę raportu na pasku menu: ![ikona raportu](./media/atp-report-icon.png).
Do raportów, które są dostępne, należą: 

- **Raport z podsumowaniem**: raport z podsumowaniem przedstawia pulpit nawigacyjny stanu w systemie. Możesz wyświetlić trzy karty — jeden dla **Podsumowanie** o co został wykryty w sieci, **otwarte podejrzane działania** który wyświetla listę podejrzanych działań, które powinny zadbać, i **Otwórz kondycji problemy z** czy list kondycji Azure ATP problemów, które powinny zajmie się. Wyświetlane podejrzane działania są podzielone według typu, tak jak problemy z kondycją. 

- **Modyfikowanie grupy wrażliwe**: Ten raport zawiera listę za każdym razem, gdy zmiany dotyczące grupy poufne (na przykład Administratorzy, lub ręcznie oznakowanych kont lub grup). Jeśli używasz czujników autonomiczny Azure ATP, aby otrzymać pełny raport o poufnych grup, należy upewnić się, że [zdarzenia są przesyłane z kontrolerów domeny do czujników autonomiczny](configure-event-forwarding.md). 

- **Haseł w zwykłym tekstem**: niektóre usługi protokół LDAP niezabezpieczonego wysłać poświadczenia konta w postaci zwykłego tekstu. Możliwe, nawet w przypadku kont poufnych. Osoby atakujące monitorowanie ruchu w sieci można catch, a następnie używać tych poświadczeń do celów złośliwe. Ten raport zawiera listę wszystkich komputera źródłowego i hasła kont, które wykryte jako ATP Azure wysyłane w postaci zwykłego tekstu. 

- **Penetracji ścieżki ruchu do kont poufnych**: Ten raport zawiera listę kont poufnych, które są dostępne za pośrednictwem ścieżki penetracji sieci. Aby uzyskać więcej informacji, zobacz [penetracji ścieżki przepływu](use-case-lateral-movement-path.md). Ten raport służy do zbierania ścieżek, które zostały utworzone w ciągu ostatnich 60 dni, a nie informacje wyświetlane w portalu obszaru roboczego, co stanowi tylko z dwóch dni.

Istnieją dwa sposoby generowania raportu: na żądanie albo zaplanowanie okresowego wysyłania raportu na adres e-mail.

Aby wygenerować raport na żądanie:

1. Na pasku menu portalu Azure ATP obszaru roboczego kliknij ikonę raportu na pasku menu: ![ikona raportu](./media/atp-report-icon.png).

2. W obszarze albo Ustaw typ wybranego raportu, **z** i **do** dat i kliknij przycisk **Pobierz**. 
 ![raporty](./media/reports.png)

Aby ustawić zaplanowany raport:
 
1. W **raporty** kliknij przycisk **ustawić Zaplanowane raporty**, lub na stronie Konfiguracja portalu Azure ATP obszar roboczy w obszarze powiadomień i raportów, kliknij przycisk **Zaplanowane raporty**.

   ![Planowanie raportów](./media/atp-sched-reports.png)
 
 > [!NOTE]
 > Codziennych raportach są przeznaczone do wysłania wkrótce po północy czasu UTC.

2. Kliknij przycisk **harmonogram** typ wybranego raportu, aby ustawić częstotliwość i adres e-mail w celu dostarczania raportów i kliknij znak plus obok adresów e-mail, aby dodać je, a następnie kliknij przycisk Dalej, aby **zapisać**.

   ![Planowanie częstotliwości raportów i wysyłania poczty e-mail](./media/sched-report1.png)


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Planowanie pojemności Azure w ATP](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)