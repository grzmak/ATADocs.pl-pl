---
title: "Praca z raportami usługi ATA | Microsoft Docs"
description: "Opisuje sposób generowania raportów w usłudze ATA w celu monitorowania sieci."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4f29dfcc8b18ff755f6c0dcdaa08eaa807b08072
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# <a name="ata-reports"></a>Raporty usługi ATA

Sekcja raportów usługi ATA w konsoli umożliwia generowanie raportów, które udostępniają informacje o stanie systemu: zarówno o kondycji systemu, jak i raport o podejrzanych działaniach wykrytych w środowisku.

Aby uzyskać dostęp do strony raportów, kliknij ikonę raportu na pasku menu: ![ikona raportu](./media/ata-report-icon.png).
Do raportów, które są dostępne, należą: 
- Raport z podsumowaniem: raport z podsumowaniem przedstawia pulpit nawigacyjny stanu systemu. Możesz wyświetlić trzy karty — jedną dla **podsumowania** tego, co zostało wykryte w sieci, jedną dla **otwierania podejrzanych działań** z podejrzanymi działaniami, którymi należy się zająć, i jedną dla **otwierania problemów z kondycją** z problemami z kondycją systemu usługi ATA, którymi należy się zająć. Wyświetlane podejrzane działania są podzielone według typu, tak jak problemy z kondycją. 
- Modyfikacja wrażliwych grup: ten raport jest wyświetlany za każdym razem, gdy nastąpi modyfikacja wrażliwych grup (takich jak administratorzy).

Istnieją dwa sposoby generowania raportu: na żądanie albo zaplanowanie okresowego wysyłania raportu na adres e-mail.

Aby wygenerować raport na żądanie:

1. Na pasku menu konsoli usługi ATA kliknij ikonę raportu: ![ikona raportu](./media/ata-report-icon.png).
2. W obszarze **Podsumowanie** albo **Modyfikacje wrażliwych grup** ustaw daty **Od** i **Do**, a następnie kliknij przycisk **Pobierz**. 
![raporty](./media/reports.png)

Aby ustawić zaplanowany raport:
 
1. Na stronie **Raporty** kliknij przycisk **Ustaw zaplanowane raporty** lub na stronie konfiguracji konsoli usługi ATA, w obszarze powiadomień i raportów, kliknij przycisk **Zaplanowane raporty**.

   ![Planowanie raportów](./media/ata-sched-reports.png)

2. Kliknij przycisk **Harmonogram** obok pozycji **Podsumowanie** lub **Modyfikacje wrażliwych grup**, aby ustawić częstotliwość i adres e-mail dostarczania raportów, a następnie kliknij znak plus obok adresów e-mail, aby je dodać, po czym kliknij przycisk **Zapisz**.

   ![Planowanie częstotliwości raportów i wysyłania poczty e-mail](./media/sched-report1.png)


> [!NOTE]
> Zaplanowane raporty są dostarczane za pośrednictwem poczty e-mail i mogą być wysyłane tylko wtedy, gdy serwer poczty e-mail został już skonfigurowany w obszarze **Konfiguracja** , a następnie w obszarze powiadomień i raportów wybierz **Serwer poczty**.


## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
