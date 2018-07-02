---
title: Integracja usługi Azure zaawansowanej ochrony przed zagrożeniami w usłudze Windows Defender ATP | Dokumentacja firmy Microsoft
description: Integracja usługi Azure Advanced Threat Protection przy użyciu usługi Windows Defender ATP dla zasięgu wykrywania zagrożeń pełne
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/5/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6d6c2cdb157d4e3f75794c8c40abfc7556e314d5
ms.sourcegitcommit: b218f60b42a25fe486d774d97719590e6fa74e10
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2018
ms.locfileid: "34760077"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integrowanie usługi Azure ATP z usługą Windows Defender ATP

Usługa Azure Advanced Threat Protection umożliwia Integrowanie usługi Azure ATP za pomocą usługi Windows Defender ATP, dla bardziej pełne rozwiązanie do ochrony przed zagrożeniami. Gdy usługi Azure ATP monitoruje ruch na kontrolerach domeny, usługi Windows Defender ATP monitoruje punktów końcowych, jednocześnie zapewniając jeden interfejs, w którym można chronić środowisko.

Po zintegrowaniu usługi Windows Defender ATP do usługi Azure ATP, możesz korzystać ze wszystkich możliwości obydwu usług i zabezpieczyć swoje środowisko, w tym:

- Azure ATP czujniki i autonomicznych czujniki: może się znajdować bezpośrednio na kontrolerach domeny lub dublowanie portów z kontrolerów domeny do zaawansowanej ochrony przed zagrożeniami, do przechwytywania i analizowania ruchu sieciowego wielu protokołów (takich jak Kerberos, DNS, RPC, NTLM i inne) do uwierzytelniania, autoryzacji i gromadzenia informacji. 

-   Punkt końcowy czujnikach behawioralnych: osadzone w systemie Windows 10, czujniki te zbierania i przetwarzania sygnałów zachowania systemu operacyjnego (na przykład procesu, rejestru, plików i komunikację sieciową) i wysyła te dane czujników do chmury prywatnej, izolowane, wystąpienie usługi Windows Defender ATP.

- Analiza zabezpieczeń w chmurze: Korzystanie z danych big data, uczenia maszynowego i unikatowy widoku firmy Microsoft w ekosystemie Windows (takie jak [Microsoft usuwania złośliwego oprogramowania](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), produktów w chmurze organizacji (np. Office 365) i zasoby online (np. Bing i filtr SmartScreen adresu URL reputacji) zachowań sygnały są tłumaczone w analizy i wykrywania zagrożeń i zalecane odpowiedzi na zaawansowane zagrożenia.

- Analiza zagrożeń: generowane przez program Microsoft łowców, zespoły zabezpieczeń i rozszerzone analizy zagrożeń oferowanych przez partnerów, analiza umożliwia usłudze Windows Defender ATP zidentyfikować narzędzia osoba atakująca, technik i procedur i generowanie ostrzeżenia o zagrożeniach kiedy te pojawiają się w danych zebranych czujnika.

Technologii Azure ATP wykrywa wiele podejrzanych działań, skupiając się na poszczególnych fazach ataku cybernetycznego ataku typu kill chain, takich jak:

- Są jaki różne zasoby Rekonesans, podczas którego osoby atakujące zbierają informacje, w jaki zaprojektowano środowisko i którymi obiektami istnieje. Kompilowanie one zazwyczaj ogólny plan następnych faz ataku.

- Cykl penetracji sieci, podczas którego osoby atakujące inwestują czas i wysiłek w rozszerzanie obszaru ataku wewnątrz sieci.

- W którym osoba atakująca przechwytuje informacje pozwalające na wznowienie kampanii przy użyciu różnych zestawów punkty wejścia, poświadczeń i technik zdominowanie domeny (trwałość).

W tym samym czasie usługi Windows Defender ATP korzysta z technologii firmy Microsoft i doświadczenia w zakresie wykrywania zaawansowanych ataków cybernetycznych, zapewniając:

- Wykrywanie ataków opartych na zachowanie bazujących na chmurze, zaawansowane<br></br>Umożliwia znalezienie przed atakami, które pozwoliło po wszystkich innych mechanizmów obronnych (po wykrycia naruszenia zabezpieczeń), zapewnia przydatnych, skorelowane alerty dotyczące znanych i nieznanych przeciwników próby ukryć swoje działania na punktach końcowych.

- Rozbudowane osi czasu w przypadku postępowania śledczego i środki zaradcze<br></br>Łatwo badać zakresu naruszenia lub podejrzane zachowania na dowolnym komputerze, za pomocą osi czasu sformatowanego maszyny. Plik, adresy URL i spisu połączenia sieciowe w sieci. Uzyskaj dodatkowy wgląd przy użyciu kolekcji głębokie i analiza ("detonation") dla dowolnego pliku lub adresów URL.

- Wbudowane bazy wiedzy analizy zagrożeń unikatowy<br></br>Szczegóły aktora i kontekst elementu intent zapewnia optyką niezrównany threat co opartych na architekturze intel wykrywanie zagrożeń — łączenie analizy pierwszy i innych źródeł.

## <a name="prerequisites"></a>Wymagania wstępne

Aby włączyć tę funkcję, potrzebujesz licencji zarówno dla usługi Azure ATP i usługi Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Jak zintegrować narzędzia Azure ATP z usługą Windows Defender ATP

1. Ustaw obszar roboczy, którą chcesz zintegrować jako **głównej**. Tylko jeden obszar roboczy może być podstawowy obszar roboczy, i tylko podstawowy obszar roboczy można zintegrować z innymi usługami. Jeśli w pewnym momencie w przyszłości, należy chcesz, aby ten obszar roboczy nie jest już podstawowym obszarem roboczym, należy najpierw usunąć integracji, zanim będzie można skonfigurować jako innych niż podstawowe.

 ![podstawowy obszar roboczy](./media/primary-workspace.png)

2. Kliknij przycisk **konfiguracji**, a następnie w obszarze **źródeł danych** wybierz **usługi Windows Defender ATP**. Następnie kliknij link, aby **Zarządzanie obszarem roboczym**. Jest on dostępny tylko wtedy, jeśli masz licencję dla usługi Windows Defender ATP i już przeprowadzono proces wdrażania dla usługi Windows Defender ATP. 

3. Na podstawowym obszarem roboczym kliknij przypominającą koło zębate.

 ![Integracja z obszaru roboczego](./media/edit-workspace.png)
 
3. Ustaw integracji **na**. 

 ![Włączanie integracji](./media/enable-integration.png)

4. W [portalu usługi Windows Defender ATP](https://beta.securitycenter.windows.com/preferences/advanced), przejdź do **ustawienia**, **zaawansowane funkcje** i ustaw **integracji usługi Azure ATP** do  **ON**. 

 ![Integracja Włączanie usługi Windows Defender ATP](./media/wd-atp-enable.png)

5. Aby sprawdzić stan integracji, w portalu usługi Azure ATP obszaru roboczego wybierz **ustawienia** i następnie **integracji usługi Windows Defender ATP**. Można wyświetlić stan integracji; Jeśli coś jest nie tak, zostanie wyświetlony błąd. Można również zobaczyć, który obszar roboczy jest zintegrowana z usługą Windows Defender ATP.

## <a name="how-it-works"></a>Jak to działa

Po zaawansowanej ochrony przed zagrożeniami w usłudze Azure i usługi Windows Defender ATP są w pełni zintegrowane, w portalu usługi Azure ATP obszar roboczy, w oknie podręcznym spowoduje wyświetlenie mini profilu i na stronie profilu jednostki każda jednostka, która znajduje się w usłudze Windows Defender ATP zawiera wskaźnik do pokazania, że jest zintegrowany z Windows Usługa Defender ATP. 

 ![Alerty usługi Windows Defender ATP](./media/profile-alerts-wd.png)

Jednostka zawiera alertów w usłudze Windows Defender ATP, czy liczba obok wskaźnika z informacją, ile alertów zostały zgłoszone.

 ![Alerty usługi Azure ATP](./media/atp-integrated-wd-icon-alerts.png)

Po kliknięciu karty identyfikacyjnej są przenoszone do portalu usługi Windows Defender ATP, gdzie można wyświetlać i eliminowanie alertów. Jeśli jednostki nie jest rozpoznawane przez usługi Windows Defender ATP, wskaźnik jest szary. 

 ![Szary usługi Windows Defender ATP](./media/wd-grey.png)

W portalu usługi Windows Defender ATP, po kliknięciu w punkcie końcowym, możesz wyświetlić alerty usługi Azure ATP. Po kliknięciu alerty dla tej jednostki w usłudze Windows Defender ATP stronę profilu jednostki zostanie otwarty w narzędzia Azure ATP. 
 
 > ! [UWAGA] Obecnie usługa Azure ATP integracji z usługą Windows Defender ATP obsługuje tylko użytkowników i maszyn ze środowiska lokalnego usługi AD. Użytkownicy z usługi Azure AD i maszyn wirtualnych, które są zarządzane na platformie Azure nie będą wyświetlane jako część integracji 

![Alerty usługi Windows Defender ATP](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Zobacz też

- [Badanie ścieżek penetracji sieci za pomocą narzędzia Azure ATP](use-case-lateral-movement-path.md)
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-architecture.md)
- [Zainstaluj zaawansowanej ochrony przed zagrożeniami](install-atp-step1.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)

