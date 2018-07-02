---
title: Zaktualizuj swoje czujników narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: Opisuje sposób aktualizacji czujników w usłudze Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/24/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b6a9cbb203068e1318425631f9f83c796bb26aa8
ms.sourcegitcommit: 7d025a2518ce63f38ce609dc21d8c3bacdd6a8e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/26/2018
ms.locfileid: "36949022"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="update-azure-atp-sensors"></a>Aktualizacja usługi Azure ATP czujników
Istotne jest usługi Azure Advanced Threat Protection na bieżąco umożliwiające najlepszą możliwą ochronę dla Twojej organizacji.

Usługi Azure ATP jest aktualizowane kilka razy w miesiącu poprawki błędów, ulepszenia wydajności i wykrywanie nowych zagrożeń. Czasami te aktualizacje wymagają odpowiednich aktualizacji do czujników. 

Jeśli nie zaktualizujesz z czujników, nie może być może komunikować się z narzędzia Azure ATP usługę w chmurze, co może spowodować uszkodzenie usługi.

Każda aktualizacja jest przetestowane i zweryfikowane na wszystkich obsługiwanych systemach operacyjnych, aby spowodować minimalny wpływ na sieć i operacji.

### <a name="azure-atp-sensor-update-types"></a>Usługa Azure typy aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami   

Usługa Azure ATP czujników obsługuje dwa rodzaje aktualizacje:
- Wersja pomocnicza aktualizacje: 
  - Częste odzyskiwanie pamięci 
  - Wymagaj instalować żadnego pliku MSI i nie zmiany w rejestrze
  - Azure ponowne uruchomienie usługi czujnika zaawansowanej ochrony przed zagrożeniami
  - Kontrolery domeny i serwer nie być konieczne ponowne uruchomienie

- Wersja główna aktualizacje:
 - Rzadki
 - Może wymagać ponownego uruchomienia kontrolerów domeny i serwerów
 - Ważnymi zmianami 

> [!NOTE]
>- Automatyczne ponowne uruchomienie czujników (w ważne aktualizacje) mogą być kontrolowane na stronie konfiguracji. 
> - Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure zawsze zachowuje co najmniej 15% pamięci i procesora CPU jest dostępne. Jeśli usługa zużywa zbyt dużej ilości pamięci, który zostanie ponownie uruchomiony przez usługę aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.

## <a name="delayed-sensor-update"></a>Opóźnione aktualizacji czujnika
Aby umożliwić bardziej stopniowy proces aktualizacji, narzędzia Azure ATP pozwala ustawić czujnik jako **opóźnione aktualizacji** Release candidate. 

Zazwyczaj czujników są aktualizowane automatycznie po zaktualizowaniu usługi w chmurze usługi Azure ATP. Ustaw czujników **opóźnione aktualizacji** zostanie zaktualizowana po 24 godzinach od aktualizacji usługi chmury początkowej.

Dzięki temu można wybrać określone czujniki, na których aktualizacji jest wycofywany się automatycznie i aktualizacji pozostałej części Twojej czujników na opóźnienia, tylko wtedy, gdy zostanie wyświetlony, sprawnie poszło pierwszej wersji aktualizacji.

> [!NOTE]
> Jeśli wystąpi błąd i nie powoduje aktualizacji czujnika, otwórz bilet pomocy technicznej.

Aby ustawić czujnika opóźnione aktualizacji:

1. W portalu usługi Azure ATP obszaru roboczego kliknij ikonę ustawień i wybierz pozycję **konfiguracji**.
2. Kliknij pozycję **aktualizacje** kartę.
3. W wierszu tabeli obok każdego sensor ma opóźnić ustaw **opóźnione aktualizacji** suwak, aby **na**.
4. Kliknij polecenie **Zapisz**.
 
## <a name="sensor-update-process"></a>Procesu aktualizacji czujnika

Co kilka minut, czujniki narzędzia Azure ATP Sprawdź, czy mają one najnowszej wersji. Po zaktualizowaniu do nowszej wersji usługi w chmurze usługi Azure ATP usługi czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure rozpoczyna się proces aktualizacji:

1. Aktualizacje usług chmury usługi Azure ATP do najnowszej wersji.
2. Usługę aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure uczy się, że jest zaktualizowana wersja.
3. Czujniki, które nie są ustawione na **opóźnione aktualizacji** rozpocząć proces aktualizacji:
  1. Usługa aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure ściąga zaktualizowaną wersję w usłudze w chmurze (w formacie pliku cab).
  2. Aktualizator czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure sprawdza poprawność podpisu pliku.
  3. Usługa aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wyodrębnić pliku cab do nowego folderu w folderze instalacyjnym czujnika. Domyślnie zostaną wyodrębnione do *C:\Program Files\Azure Advanced Threat ochrony czujnika\<numer wersji >*
  4. Usługa aktualizacji czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure powoduje ponowne uruchomienie usługi czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.
  5. Usługa czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wskazuje nowe pliki, które są wyodrębniane z pliku cab.
  > [!NOTE]
  >Aktualizację pomocniczą czujników nie Zainstaluj Instalator MSI lub zmienić żadnych wartości rejestru lub wszystkie inne pliki systemowe. Nawet oczekuje na ponowne uruchomienie nie będzie mieć wpływ na aktualizację czujników. 
  6. Czujników uruchomienia w oparciu o zaktualizowanych wersji.
  7. Czujnik odbiera przestrzeń w usłudze w chmurze platformy Azure. Można to sprawdzić w **aktualizacje** strony.
  8. Czujnik dalej rozpoczyna się proces aktualizacji. 

4. Zaktualizowano usługę w chmurze po 24 godzinach od usługi Azure ATP, czujniki wybranych dla ** aktualizacja opóźnione uruchomienie procesu aktualizacji.

![Czujnik aktualizacji](./media/sensor-update.png)


W przypadku awarii jeśli czujnika nie została ukończona proces aktualizacji, odpowiedni alert monitorowania jest wyzwalany i jest wysyłany jako powiadomienie.

![Czujnik przestarzałe](./media/sensor-outdated.png)


## <a name="see-also"></a>Zobacz też

- [Konfigurowanie składnika przesyłanie dalej zdarzeń](configure-event-forwarding.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)