---
title: Praca z raportami usługi ATA | Microsoft Docs
description: Opisuje sposób generowania raportów w usłudze ATA w celu monitorowania sieci.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1802a278a8d125f0d1b86eb8bead3918ef1586e6
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166124"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*


# <a name="ata-reports"></a>Raporty usługi ATA

Sekcja raportów usługi ATA w konsoli umożliwia generowanie raportów, które udostępniają informacje o stanie systemu: zarówno o kondycji systemu, jak i raport o podejrzanych działaniach wykrytych w środowisku.

Aby uzyskać dostęp do strony raportów, kliknij ikonę raportu na pasku menu: ![ikona raportu](./media/ata-report-icon.png).
Do raportów, które są dostępne, należą: 

- **Raport z podsumowaniem**: raport z podsumowaniem przedstawia pulpit nawigacyjny stanu systemu. Możesz wyświetlić trzy karty — jedną dla **podsumowania** tego, co zostało wykryte w sieci, jedną dla **otwierania podejrzanych działań** z podejrzanymi działaniami, którymi należy się zająć, i jedną dla **otwierania problemów z kondycją** z problemami z kondycją systemu usługi ATA, którymi należy się zająć. Wyświetlane podejrzane działania są podzielone według typu, tak jak problemy z kondycją. 

- **Modyfikacja wrażliwych grup**: Ten raport zawiera listę za każdym razem, gdy zostanie podjęta modyfikacja wrażliwych grup (takich jak Administratorzy).

- **Hasła ujawnione w zwykłym tekście**: niektóre usługi protokół LDAP — zabezpieczanie wysyłają poświadczenia kont w postaci zwykłego tekstu. Można to zrobić nawet w przypadku kont poufnych. Osoby atakujące monitorujące ruch sieciowy może przechwytywać i korzystać z nich te poświadczenia do złośliwych celów. Ten raport zawiera listę wszystkich komputera i konta haseł źródła, które usługa ATA wykrył jako wysyłane w postaci zwykłego tekstu. 

- **Boczne ścieżki ruchu do wrażliwych kont**: Ten raport zawiera listę kont poufnych, które są udostępniane za pośrednictwem ścieżki ruchu poprzecznego. Aby uzyskać więcej informacji, zobacz [ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md)

Istnieją dwa sposoby generowania raportu: na żądanie albo zaplanowanie okresowego wysyłania raportu na adres e-mail.

Aby wygenerować raport na żądanie:

1. Na pasku menu konsoli usługi ATA kliknij ikonę raportu: ![ikona raportu](./media/ata-report-icon.png).

2. W obszarze typu wybranego raportu, ustaw **z** i **do** dat i kliknij przycisk **Pobierz**. 
 ![raporty](./media/reports.png)

Aby ustawić zaplanowany raport:
 
1. Na stronie **Raporty** kliknij przycisk **Ustaw zaplanowane raporty** lub na stronie konfiguracji konsoli usługi ATA, w obszarze powiadomień i raportów, kliknij przycisk **Zaplanowane raporty**.

   ![Planowanie raportów](./media/ata-sched-reports.png)

  > [!NOTE]
  > Codzienne raporty są przeznaczone do wysłania wkrótce po północy czasu UTC.

2. Kliknij przycisk **harmonogram** obok typu wybranego raportu, aby ustawić częstotliwość i adres e-mail dostarczania raportów, a następnie kliknij znak plus obok adresów e-mail, aby je dodać, a następnie kliknij przycisk **Zapisz**.

   ![Planowanie częstotliwości raportów i wysyłania poczty e-mail](./media/sched-report1.png)


> [!NOTE]
> Zaplanowane raporty są dostarczane za pośrednictwem poczty e-mail i może go wysłać tylko jeśli został już skonfigurowany serwer poczty e-mail w ramach **konfiguracji** a następnie w obszarze **powiadomienia i raporty**, wybierz opcję **poczty Serwer**.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
