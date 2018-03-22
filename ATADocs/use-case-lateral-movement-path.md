---
title: "Badanie ataków ścieżki penetracja sieci przy użyciu usługi ATA | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób wykrywania ataków ścieżki penetracja sieci z Advanced Threat Analytics (ATA)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dc03cfe1719541dac0f8509c0f8f22987ecb96bb
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Badanie ścieżek penetracja sieci przy użyciu usługi ATA

Nawet wtedy, gdy użytkownik starań w celu ochrony poufnych użytkowników i administratorów są złożone hasła, które często zmienia, mają wzmocnione zabezpieczenia swoich urządzeń i ich dane są bezpiecznie przechowywane, osoby atakujące do można nadal używać ścieżki penetracja sieci dostęp do poufnych konta. W ataków penetracja sieci osoba atakująca wykorzystuje wystąpień podczas logowania użytkowników poufnych na maszynę gdzie niepoufnych użytkownik ma lokalne prawa. Osoby atakujące mogą następnie penetrację, uzyskiwanie dostępu do mniej poufnych użytkownika, a następnie przeniesieniu na komputerze przejęcie poświadczeń dla poufnych użytkownika. 

## <a name="what-is-a-lateral-movement-path"></a>Co to jest ścieżka penetracja sieci?

Penetracja sieci to, gdy osoba atakująca aktywnie używa konta niepoufnych uzyskanie dostępu do kont poufnych. Ich użyć dowolnej z metod opisanych w [przewodnik podejrzanych działań](suspicious-activity-guide.md) uzyskanie hasła początkowego niepoufnych, a następnie użyć narzędzia, takie jak Bloodhound, zrozumienie, którzy są administratorami w Twojej sieci i komputery, które one dostępne. Mogą one następnie uzyskać dostęp do danych na kontrolerach domeny, aby wiedzieć, kto ma kont, które i dostęp do zasobów i plików, kradzież poświadczeń innych użytkowników (czasami poufnych użytkowników), które są przechowywane na komputerach już mieć dostęp, a następnie bok przenieść między użytkownikami i zasobami, aż do osiągnięcia ich uprawnień administratora w sieci. 

Usługa ATA włącza podjęcia odpowiednich działań uprzedzające w sieci, aby uniemożliwić osobom atakującym pomyślne o penetracji sieci.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Odnajdywanie zagrożonych kont poufnych

Aby dowiedzieć się, które poufnych konta w sieci są narażone z powodu ich połączenie do kont niepoufnych lub zasobów, wykonaj następujące kroki. Aby zabezpieczyć sieć przed atakami penetracja sieci, usługa ATA działa z elementu end z poprzednimi wersjami, co oznacza, że ATA zapewnia mapy, który rozpoczyna się od konta uprzywilejowanego, a następnie przedstawia użytkowników, którzy i urządzenia są w ścieżce penetracji tych użytkowników i ich poświadczeń.

1. W menu konsoli usługi ATA kliknij ikonę raportów ![Ikona raportów](./media/ata-report-icon.png).

2. W obszarze **penetracji przeniesień ścieżki do kont poufnych**, jeśli brak znaleziono ścieżek penetracja sieci, raport będzie szary. W przypadku ścieżek penetracja sieci, następnie daty automatycznie wybierz raport pierwszy data po odpowiednich danych. 

 ![raporty](./media/reports.png)

3. Kliknij przycisk **Pobierz**.

3. Plik programu Excel, który jest tworzony udostępnia szczegółowe informacje dotyczące konta poufnych, które są narażeni na ataki. **Podsumowanie** karta zawiera wykresy, które zawierają liczby kont poufnych, komputerów i średnie zagrożonych zasobów. **Szczegóły** karta zawiera listę kont poufnych, które należy zwrócić uwagę.


## <a name="investigate"></a>Badanie

Teraz, znając kont poufnych, które są narażeni na ataki, możesz głębokość zajrzyj dostęp usługi ATA, aby dowiedzieć się więcej i podjęcia środków zapobiegawczych.

1. W konsoli usługi ATA, przeglądać użytkownika, którego konto jest wymieniony jako zagrożone w **penetracji przeniesień ścieżki do kont poufnych** raport, na przykład Samira Abbasi. Możesz również wyszukać wskaźnika przepływu penetracja dodawanej do profilu jednostki, gdy obiekt jest w ścieżce penetracja sieci ![penetracji ikona](./media/lateral-movement-icon.png) lub ![ikonę ścieżki](./media/paths-icon.png).

2. Na stronie profilu użytkownika, którego kliknięcie spowoduje otwarcie, kliknij przycisk **penetracji ścieżki przepływu** kartę.

3. Diagram, który jest wyświetlany zawiera mapy możliwych ścieżek użytkownikowi poufnych. Wykres przedstawia połączeń, które zostały wprowadzone w ciągu ostatnich dwóch dni, więc narażenia jest odświeżona.

4. Przejrzyj wykres tak, aby zobaczyć, jakie informacje na temat zagrożeń poświadczeń użytkowników poufnych. Na przykład na tej mapie, możesz wykonać Samira Abbasi **zalogowanym przez** szary strzałki, aby zobaczyć, których Samira zalogowania się przy użyciu swoich poświadczeń uprzywilejowanych. W takim przypadku na komputerze REDMOND-WA-odchyleń zostały zapisane poświadczenia poufnych przez Samira Następnie sprawdź, która zalogowani inni użytkownicy na komputery, które tworzone najbardziej zagrożeń i luk w zabezpieczeniach. Zobacz ten analizując **administratora na** czarne strzałki, aby zobaczyć, kto ma uprawnienia administratora na zasobie. W tym przykładzie wszyscy użytkownicy w grupie wszystkie firmy Contoso ma możliwość dostępu do poświadczeń użytkownika z tego zasobu.  

 ![ścieżki penetracja sieci profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Program prewencyjnej najlepsze rozwiązania

- Najlepszy sposób, aby zapobiec penetracja sieci jest należy upewnić się, że użytkownicy poufnych poświadczeń administratora tylko po zalogowaniu się na komputerach ze wzmocnionymi zabezpieczeniami w przypadku, gdy nie ma żadnego niepoufnych użytkownika, który ma prawa administratora na tym samym komputerze. W przykładzie upewnij się, że jeśli Samira potrzebuje dostępu do deweloperów — WA-REDMOND, użytkownik zaloguje się za pomocą nazwy użytkownika i hasła innego niż swoje poświadczenia administratora lub Usuń grupę wszystkich Contoso z grupy administratorów lokalnych na REDMOND-WA-odchyleń

- Zalecane jest również, że należy upewnić się, że nikt nie ma niepotrzebnych lokalne uprawnienia administracyjne. W tym przykładzie należy sprawdzić, czy wszyscy w Contoso wszystkie rzeczywiście wymaga uprawnień administratora na REDMOND-WA-odchyleń

- On jest zawsze upewnij się, że osoby tylko mają dostęp do zasobów konieczne. Jak widać w przykładzie Oscar Posada znacznie rozszerzenie narażenia na Samira. Jest on zostać uwzględnione w Contoso wszystkie niezbędne? Czy istnieją podgrupy, które można utworzyć, aby zminimalizować ryzyko?


## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
