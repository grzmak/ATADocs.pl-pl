---
title: Praca z raportami usługi ATA | Microsoft Docs
description: Opisuje sposób generowania raportów w usłudze ATA w celu monitorowania sieci.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9a113d8d090c5a90a07043a0ef75e1be0fc840c3
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202259"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*


# <a name="ata-reports"></a>Raporty usługi ATA

Sekcja raportów usługi ATA w konsoli umożliwia generowanie raportów, które udostępniają informacje o stanie systemu: zarówno o kondycji systemu, jak i raport o podejrzanych działaniach wykrytych w środowisku.

Aby uzyskać dostęp do strony raportów, kliknij ikonę raportu na pasku menu: ![ikona raportu](./media/ata-report-icon.png).
Do raportów, które są dostępne, należą: 

- **Raport z podsumowaniem**: raport z podsumowaniem przedstawia pulpit nawigacyjny stanu w systemie. Możesz wyświetlić trzy karty — jedną dla **podsumowania** tego, co zostało wykryte w sieci, jedną dla **otwierania podejrzanych działań** z podejrzanymi działaniami, którymi należy się zająć, i jedną dla **otwierania problemów z kondycją** z problemami z kondycją systemu usługi ATA, którymi należy się zająć. Wyświetlane podejrzane działania są podzielone według typu, tak jak problemy z kondycją. 

- **Modyfikowanie grupy wrażliwe**: Ten raport zawiera listę za każdym razem, gdy zmiany dotyczące grupy poufne (na przykład Administratorzy).

- **Haseł w zwykłym tekstem**: niektóre usługi protokół LDAP niezabezpieczonego wysłać poświadczenia konta w postaci zwykłego tekstu. Możliwe, nawet w przypadku kont poufnych. Osoby atakujące monitorowanie ruchu w sieci można catch, a następnie używać tych poświadczeń do celów złośliwe. Ten raport zawiera listę wszystkich źródła komputerze i koncie haseł, których ATA wykryte jako wysyłane w postaci zwykłego tekstu. 

- **Penetracji ścieżki ruchu do kont poufnych**: Ten raport zawiera listę kont poufnych, które są dostępne za pośrednictwem ścieżki penetracji sieci. Aby uzyskać więcej informacji, zobacz [penetracji ścieżki ruchu](use-case-lateral-movement-path.md)

Istnieją dwa sposoby generowania raportu: na żądanie albo zaplanowanie okresowego wysyłania raportu na adres e-mail.

Aby wygenerować raport na żądanie:

1. Na pasku menu konsoli usługi ATA kliknij ikonę raportu: ![ikona raportu](./media/ata-report-icon.png).

2. W obszarze albo Ustaw typ wybranego raportu, **z** i **do** dat i kliknij przycisk **Pobierz**. 
 ![raporty](./media/reports.png)

Aby ustawić zaplanowany raport:
 
1. Na stronie **Raporty** kliknij przycisk **Ustaw zaplanowane raporty** lub na stronie konfiguracji konsoli usługi ATA, w obszarze powiadomień i raportów, kliknij przycisk **Zaplanowane raporty**.

   ![Planowanie raportów](./media/ata-sched-reports.png)

  > [!NOTE]
  > Codziennych raportach są przeznaczone do wysłania wkrótce po północy czasu UTC.

2. Kliknij przycisk **harmonogram** typ wybranego raportu, aby ustawić częstotliwość i adres e-mail w celu dostarczania raportów i kliknij znak plus obok adresów e-mail, aby dodać je, a następnie kliknij przycisk Dalej, aby **zapisać**.

   ![Planowanie częstotliwości raportów i wysyłania poczty e-mail](./media/sched-report1.png)


> [!NOTE]
> Zaplanowane raporty są dostarczane za pośrednictwem poczty e-mail i mogą być wysyłane tylko jeśli został już skonfigurowany serwer poczty e-mail w obszarze **konfiguracji** , a następnie w obszarze **powiadomienia i raporty**, wybierz pozycję **poczty Serwer**.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
