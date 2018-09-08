---
title: Badanie ataków ścieżki ruchu poprzecznego za pomocą narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak wykrywać ataki ścieżki ruchu poprzecznego za pomocą usługi Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0fcdfdbeaeed7e42aff9d63f4f88300346c73465
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165579"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Badanie ścieżek penetracji sieci za pomocą narzędzia Azure ATP


Penetracja sieci to gdy osoba atakująca używa niewrażliwe konta w celu uzyskania dostępu do wrażliwych kont. Można to zrobić za pomocą metod opisanych w [Przewodnik po podejrzanych działaniach](suspicious-activity-guide.md). Penetracji sieci jest używana przez osoby atakujące do identyfikowania i uzyskiwanie dostępu do wrażliwych kont i komputerach w sieci przy użyciu niewrażliwe konta, mających poświadczenia przechowywane w dzienniku w kont, grup i komputerów. Gdy osoba atakująca ma uzyskali dostęp, osoba atakująca również korzystać z zalet danych na kontrolerach domeny.


## <a name="discover-your-at-risk-sensitive-accounts"></a>Odkryj swoje zagrożonych wrażliwych kont

Aby sprawdzić, które wrażliwych kont w sieci są dostępne ze względu na ich połączenie do zwykłych kont, grup i komputerów, wykonaj następujące kroki. 

1. W menu portalu obszaru roboczego usługi Azure ATP kliknij ikonę raportów ![Ikona raportów](./media/atp-report-icon.png).

2. W obszarze **boczne ścieżki ruchów do wrażliwych kont**, jeśli nie ma potencjał, nie można odnaleźć ścieżki ruchu poprzecznego raportu jest wyszarzona. W przypadku potencjalnych ścieżki ruchu poprzecznego raport automatycznie wstępnie wybiera pierwszy data, gdy ma odpowiednich danych. Raport ścieżki ruchu poprzecznego udostępnia dane dla maksymalnie 60 dni.

 ![raporty](./media/reports.png)

3. Kliknij przycisk **Pobierz**.

4. Utworzono plik programu Excel, która zawiera szczegółowe informacje o potencjalnych ścieżki ruchu poprzecznego i ujawnienia poufnych kont dla dat wybrano. **Podsumowanie** karta zawiera wykresy, które szczegółowo liczby wrażliwych kont, komputerów i średnie odpływowi dostępu. **Szczegóły** karta zawiera listę kont poufnych, które powinny zbadania. Należy pamiętać, że ścieżki szczegółowe w raporcie do pobrania może nie będą już dostępne, ponieważ zostały one wykryte w ciągu ostatnich 60 dni i mogą mieć zmieniony lub została zmodyfikowana.


## <a name="investigate"></a>Badanie



1. W portalu obszaru roboczego usługi Azure ATP Wyszukaj wskaźnika przenoszenia poprzecznych dodaną do profilu jednostki, gdy jednostka jest ścieżki ruchu poprzecznego ![Ikona poprzecznego](./media/lateral-movement-icon.png) lub ![Ikona ścieżki](./media/paths-icon.png). Należy pamiętać, że znaczka będą wyświetlane tylko w przypadku ruchu poprzecznego w ostatnich 48 godzinach. 

2. Na stronie profilu użytkownika, która zostanie otwarta, kliknij przycisk **ścieżki ruchu poprzecznego** kartę. 

3. Wykres, który jest wyświetlany zawiera mapę możliwe ścieżki do wrażliwego użytkownika. Na wykresie przedstawiono możliwe połączenia zaobserwowane w ciągu ostatnich 48 godzin. Jeśli działanie nie zostało wykryte w ciągu ostatnich dwóch dni, nie pojawi się wykres. 

4. Przejrzyj wykres, aby zobaczyć, co omówiono ujawniania poświadczeń użytkownika wielkość liter. Na przykład na tej mapie możesz wykonać **Zalogowało** szary strzałki, aby zobaczyć, gdzie Samira zalogowania się przy użyciu swoich poświadczeń dla konta uprzywilejowanego. W tym przypadku poświadczenia poufne firmy Samira zostały zapisane na komputerze REDMOND-WA-DEV. Teraz, zwróć uwagę, które użytkownicy zalogowani na komputerach, które tworzone najbardziej zagrożeń i luk w zabezpieczeniach. Można to zobaczyć, analizując **administratora na** czarne strzałki, aby zobaczyć, kto ma uprawnienia administratora dla zasobu. W tym przykładzie każdy grupy cała firma Contoso ma możliwość dostępu do poświadczeń użytkownika z tego zasobu.  

 ![ścieżki ruchu poprzecznego profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Zapobiegawczych najlepszych rozwiązań

- Najlepszym sposobem, aby zapobiec penetracji sieci jest upewnij się, czy tylko wtedy, gdy logując się do komputerów ze wzmocnionymi zabezpieczeniami użytkownicy poufnych przy użyciu poświadczeń administratora. W przykładzie upewnij się, że jeśli Samira administrator musi mieć dostęp do REDMOND-WA-DEV, zalogowaniu się przy użyciu nazwy użytkownika i hasło, ich poświadczeń administratora.

- Zalecane jest również przez należy upewnić się, że nikt nie miał niepotrzebnych uprawnień administracyjnych. W tym przykładzie należy sprawdzić, jeśli wszyscy w Contoso wszystkie faktycznie wymaga uprawnień administratora w REDMOND-WA-DEV.

- Upewnij się, że osoby mają tylko dostęp do niezbędnych zasobów. W tym przykładzie Oscar Posada rozszerza znacznie się zagrożeń Samira firmy. Jest to konieczne, czy ten użytkownik jest uwzględniona w grupie **wszystkie Contoso**? Czy istnieją podgrupy, które można utworzyć, aby zminimalizować ryzyko?

**Porada** — po wykryciu żadnych działań w ciągu ostatnich 48 godzin i wykres jest niedostępny, raport ścieżki ruchu poprzecznego jest nadal dostępne i udostępnia informacje o potencjalnych ścieżek penetracji sieci wykryte w ciągu ostatnich 60 dni. 

**Porada** — instrukcje dotyczące sposobu ustawiania klientów i serwerów Zezwalaj na narzędzia Azure ATP do wykonywania operacji SAM-R służące do wykrywania ścieżki ruchu poprzecznego, znajdują się [skonfigurować SAM-R](install-atp-step8-samr.md).


## <a name="see-also"></a>Zobacz też

- [Konfigurowanie uprawnień SAM-R wymagane](install-atp-step8-samr.md)
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)