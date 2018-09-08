---
title: Badanie ataków ścieżki ruchu poprzecznego za pomocą usługi ATA | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak wykrywać ataki ścieżki ruchu poprzecznego z Advanced Threat Analytics (ATA).
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 11f67ba077251d552c5a5a4d0391e5668b349215
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166305"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Badanie ścieżek penetracji sieci za pomocą usługi ATA

Nawet wtedy, gdy użytkownik starań w celu ochrony poufnych użytkownikom i administratorom są złożonych haseł, które zmieniają się często, ich maszyn są wzmocnione i ich dane są bezpiecznie przechowywane, osoby atakujące można nadal używać ścieżki ruchu poprzecznego do dostępu do poufnych konta. W ataki, penetracji sieci osoba atakująca wykorzystuje wystąpień wrażliwi użytkownicy po zalogowaniu się na maszynę gdzie niewrażliwych użytkownik ma lokalne prawa. Osoby atakujące mogą następnie przenieść bok, uzyskiwanie dostępu do mniej wrażliwych użytkowników, a następnie przenoszenia na komputerze w przejęcie poświadczeń dla poufnych użytkownika. 

## <a name="what-is-a-lateral-movement-path"></a>Jaka jest ścieżka ruchu poprzecznego?

Penetracja sieci to gdy osoba atakująca używa niewrażliwe konta w celu uzyskania dostępu do wrażliwych kont. Można to zrobić za pomocą metod opisanych w[Przewodnik po podejrzanych działaniach](suspicious-activity-guide.md). Aby dowiedzieć się, kto administratorów znajdują się w sieci i komputery, które osoba atakująca może uzyskać dostęp, osoba atakująca może wykorzystać dane na kontrolerach domeny. 

Usługa ATA umożliwia konieczności podjęcia odpowiednich akcji wyprzedzających w sieci, aby uniemożliwić osobom atakującym powodzeniem w ruchu poprzecznego.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Odnajdowanie usługi zagrożonych wrażliwych kont

Aby dowiedzieć się, które wrażliwych kont w sieci są narażone ze względu na ich połączenie niewrażliwe konta lub zasobów w określonym przedziale czasu, wykonaj następujące kroki. 

1. W przedstawionym menu konsoli usługi ATA kliknij ikonę raportów ![Ikona raportów](./media/ata-report-icon.png).

2. W obszarze **boczne ścieżki ruchów do wrażliwych kont**, jeśli znaleziono żadnych ścieżek ruchu poprzecznego raportu jest wyszarzona. W przypadku ścieżki ruchu poprzecznego następnie daty raport automatycznie wybierz pierwszy daty po odpowiednich danych. 

 ![raporty](./media/reports.png)

3. Kliknij przycisk **Pobierz**.

3. Plik programu Excel, który jest tworzony zapewnia szczegółowe informacje o Twojej wrażliwych kont, które są zagrożone. **Podsumowanie** karta zawiera wykresy, które szczegółowo liczby wrażliwych kont, komputerów i średnie odpływowi zasobów. **Szczegóły** karta zawiera listę kont poufnych, które powinny być zajmującym się ochroną. Należy pamiętać, że ścieżki są ścieżki, które wcześniej istniejących i mogą nie być dostępne już dzisiaj.


## <a name="investigate"></a>Badanie

Teraz, gdy wiesz, które wrażliwych kont są zagrożone, możesz głębokiego zajrzyj, aby dowiedzieć się więcej i podjęcia środków zapobiegawczych w usłudze ATA.

1. W konsoli usługi ATA Wyszukaj wskaźnika przenoszenia poprzecznych dodaną do profilu jednostki, gdy jednostka jest ścieżki ruchu poprzecznego ![Ikona poprzecznego](./media/lateral-movement-icon.png) lub ![Ikona ścieżki](./media/paths-icon.png). Jest on dostępny, jeśli wystąpił ścieżki ruchu poprzecznego w ciągu ostatnich dwóch dni.

2. Na stronie profilu użytkownika, która zostanie otwarta, kliknij przycisk **ścieżki ruchu poprzecznego** kartę.

3. Wykres, który jest wyświetlany zawiera mapę możliwe ścieżki do wrażliwego użytkownika. Na wykresie widać połączeń, które zostały wprowadzone w ciągu ostatnich dwóch dni.

4. Przejrzyj wykres, aby zobaczyć, co omówiono ujawniania poświadczeń użytkownika wielkość liter. Na przykład na tej mapie możesz wykonać **Zalogowało** szary strzałki, aby zobaczyć, gdzie Samira zalogowania się przy użyciu swoich poświadczeń uprzywilejowanych. W tym przypadku poświadczenia poufne firmy Samira zostały zapisane na komputerze REDMOND-WA-DEV. Następnie sprawdź, która zalogowani inni użytkownicy w komputery, które tworzone najbardziej zagrożeń i luk w zabezpieczeniach. Można to zobaczyć, analizując **administratora na** czarne strzałki, aby zobaczyć, kto ma uprawnienia administratora dla zasobu. W tym przykładzie, wszystkie osoby w grupie **wszystkie Contoso** umożliwia dostęp do poświadczeń użytkownika z tego zasobu.  

 ![ścieżki ruchu poprzecznego profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Zapobiegawczych najlepszych rozwiązań

- Najlepszym sposobem, aby zapobiec penetracji sieci jest upewnienie się, czy tylko wtedy, gdy logując się do komputerów ze wzmocnionymi zabezpieczeniami użytkownicy poufnych przy użyciu poświadczeń administratora w przypadku, gdy nie ma żadnego użytkownika niewrażliwych, kto ma uprawnienia administratora na tym samym komputerze. W przykładzie upewnij się, że jeśli Samira musi mieć dostęp do REDMOND-WA-DEV, ona zaloguje się za pomocą nazwy użytkownika i hasła innych niż swoje poświadczenia administratora lub Usuń grupę wszystkich Contoso z lokalnej grupy administratorów na REDMOND-WA-DEV.

- Zalecane jest również przez należy upewnić się, że nikt nie miał niepotrzebne lokalnych uprawnień administracyjnych. W tym przykładzie należy sprawdzić, czy wszyscy w Contoso wszystkie naprawdę potrzebuje uprawnień administratora w REDMOND-WA-DEV.

- Upewnij się, że osoby mają tylko dostęp do niezbędnych zasobów. W tym przykładzie Oscar Posada rozszerza znacznie się zagrożeń Samira firmy. Jest to konieczne, on być uwzględniona w grupie **wszystkie Contoso**? Czy istnieją podgrupy, które można utworzyć, aby zminimalizować ryzyko?

**Porada** — Jeśli działanie nie zostanie wykryty w ciągu ostatnich dwóch dni, wykres jest niewidoczny, ale raport ścieżki ruchu poprzecznego nadal będzie można uzyskać informacje na temat ścieżek ruchu poprzecznego ostatnich 60 dni.

**Porada** — Aby uzyskać instrukcje dotyczące sposobu konfigurowania serwerów Zezwalaj na wykonywanie operacji SAM-R służące do wykrywania ścieżki ruchu poprzecznego, usługa ATA [skonfigurować SAM-R](install-ata-step9-samr.md).




## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
