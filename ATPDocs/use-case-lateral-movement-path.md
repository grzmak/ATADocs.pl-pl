---
title: "Badanie ataków ścieżki penetracja sieci z Azure ATP | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób wykrywania ataków ścieżki penetracja sieci z Azure Advanced Threat ochrony (ATP)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7deeec2c2ee2c2d964b6495921eba0fa378bd8ee
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection wersji 1.9*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Badanie ścieżek penetracja sieci Azure ATP

Azure ATP ułatwia zapobieganie atakom, które używają ścieżek penetracji sieci. Nawet wtedy, gdy użytkownik starań w celu ochrony poufnych użytkowników, administratorów ma złożonych haseł, które często zmienia, mają wzmocnione zabezpieczenia ich maszyn i bezpiecznie, są przechowywane ich dane osoby atakujące można nadal używać ścieżek penetracja sieci, przeniesienie w sieci między użytkownikami i komputerami, dopóki ich trafień jackpot wirtualnego zabezpieczeń: poświadczeń konta administratora poufnych.

## <a name="what-is-a-lateral-movement-path"></a>Co to jest ścieżka penetracja sieci?

Penetracja sieci to, gdy osoba atakująca aktywnie używa konta niepoufnych uzyskanie dostępu do kont poufnych. Ich użyć dowolnej z metod opisanych w [przewodnik podejrzanych działań](suspicious-activity-guide.md) uzyskanie hasła początkowego niepoufnych, a następnie użyć narzędzia, takie jak Bloodhound, zrozumienie, którzy są administratorami w Twojej sieci i komputery, które one dostępne. Można następnie korzystać z dostępnych danych na ataki na kontrolerach domeny, aby dowiedzieć się, kto ma, które konta i dostęp do zasobów i plików i mogą wykradać poświadczeń innych użytkowników (użytkownicy czasami poufnych) przechowywanych na komputerach, które mają już dostępne, a następnie bok przenieść więcej użytkowników i zasoby do momentu osiągnięcia one uprawnień administratora w sieci. 

Azure ATP umożliwiają przełączanie uprzedzające działania w sieci, aby uniemożliwić osobom atakującym pomyślne o penetracji sieci.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Odnajdywanie zagrożonych kont poufnych

Aby dowiedzieć się, które poufnych konta w sieci są narażone z powodu ich połączenie do kont niepoufnych lub zasobów, wykonaj następujące kroki. Aby zabezpieczyć sieć przed atakami penetracja sieci, Azure ATP działa z elementu end z poprzednimi wersjami, co oznacza, że Azure ATP zapewnia mapy, który rozpoczyna się od konta uprzywilejowanego, a następnie pokaże Ci, którzy użytkownicy i urządzenia znajdują się w ścieżce penetracji tych użytkowników i ich poświadczenia.

1. W menu portalu obszaru roboczego Azure ATP kliknij ikonę raportów ![Ikona raportów](./media/atp-report-icon.png).

2. W obszarze **penetracji przeniesień ścieżki do kont poufnych**, jeśli brak znaleziono ścieżek penetracja sieci, raport będzie szary. W przypadku ścieżek penetracja sieci, następnie daty automatycznie wybierz raport pierwszy data po odpowiednich danych. Raport ścieżki penetracja sieci zawiera dane w ciągu ostatnich 60 dni.

 ![raporty](./media/reports.png)

3. Kliknij przycisk **Pobierz**.

3. Plik programu Excel, który jest tworzony udostępnia szczegółowe informacje dotyczące konta poufnych, które są narażeni na ataki. **Podsumowanie** karta zawiera wykresy, które zawierają liczby kont poufnych, komputerów i średnie zagrożonych zasobów. **Szczegóły** karta zawiera listę kont poufnych, które należy zwrócić uwagę.

4. Aby uzyskać instrukcje dotyczące sposobu konfigurowania serwerów umożliwiają ATP Azure do wykonywania operacji SAM-R, potrzebnego do wykrycia ścieżki penetracja sieci [skonfigurować SAM-R](install-atp-step8-samr.md).

## <a name="investigate"></a>Badanie

Teraz, znając kont poufnych, które są narażeni na ataki, możesz głębokość zajrzyj dostęp ATP Azure, aby dowiedzieć się więcej i podjęcia środków zapobiegawczych.

1. W portalu Azure ATP obszaru roboczego przeglądać użytkownika, którego konto jest wymieniony jako zagrożone w **penetracji przeniesień ścieżki do kont poufnych** raport, na przykład Samira Abbasi. Można również wyszukać wskaźnika przepływu penetracja dodawanej do profilu jednostki, gdy obiekt jest w ścieżce penetracja sieci ![penetracji ikona](./media/lateral-movement-icon.png) lub ![ikonę ścieżki](./media/paths-icon.png). To jest dostępna, jeśli wystąpił penetracja sieci w ciągu ostatnich dwóch dni. 

2. Na stronie profilu użytkownika, którego kliknięcie spowoduje otwarcie, kliknij przycisk **penetracji ścieżki przepływu** kartę. 

3. Diagram, który jest wyświetlany zawiera mapy możliwych ścieżek użytkownikowi poufnych. Wykres przedstawia połączeń, które zostały wprowadzone w ciągu ostatnich dwóch dni, więc narażenia jest odświeżona. Jeśli działanie nie została wykryta w ciągu ostatnich dwóch dni wykresu nie jest wyświetlana, ale [penetracji przepływu Ścieżka raportu](reports.md) będą nadal dostępne uzyskać informacje o penetracji sieci ścieżek w ciągu ostatnich 60 dni.

4. Przejrzyj wykres tak, aby zobaczyć, jakie informacje na temat zagrożeń poświadczeń użytkowników poufnych. Na przykład na tej mapie, możesz wykonać Samira Abbasi **zalogowanym przez** szary strzałki, aby zobaczyć, których Samira zalogował się za pomocą ich poświadczeń uprzywilejowanych. W takim przypadku na komputerze REDMOND-WA-odchyleń zostały zapisane poświadczenia poufnych przez Samira Następnie sprawdź, która zalogowani inni użytkownicy na komputery, które tworzone najbardziej zagrożeń i luk w zabezpieczeniach. Zobacz ten analizując **administratora na** czarne strzałki, aby zobaczyć, kto ma uprawnienia administratora na zasobie. W tym przykładzie wszyscy użytkownicy w grupie wszystkie firmy Contoso ma możliwość dostępu do poświadczeń użytkownika z tego zasobu.  

 ![ścieżki penetracja sieci profilu użytkownika](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Program prewencyjnej najlepsze rozwiązania

- Należy upewnić się, że użytkownicy poufnych poświadczeń administratora tylko po zalogowaniu się na komputerach ze wzmocnionymi zabezpieczeniami jest najlepszy sposób, aby zapobiec penetracji sieci. W tym przykładzie upewnij się, że jeśli administrator Samira musi mieć dostęp do deweloperów — WA-REDMOND, rejestrują się przy użyciu nazwy użytkownika i hasło, ich poświadczeń administratora.

- Zalecane jest również, że należy upewnić się, że nikt nie ma uprawnienia administracyjne na niepotrzebne. W tym przykładzie należy sprawdzić, czy wszyscy w Contoso wszystkie rzeczywiście wymaga uprawnień administratora na REDMOND-WA-odchyleń

- On jest zawsze upewnij się, że osoby tylko mają dostęp do zasobów konieczne. Jak widać w przykładzie Oscar Posada znacznie rozszerzenie narażenia na Samira. Czy jest umieszczenie użytkownika w Contoso wszystkie niezbędne? Czy istnieją podgrupy, które można utworzyć, aby zminimalizować ryzyko?


## <a name="see-also"></a>Zobacz też

- [Skonfiguruj SAM-R wymagane uprawnienia](install-atp-step8-samr.md)
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)