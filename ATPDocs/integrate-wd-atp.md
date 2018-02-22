---
title: Integracja Advanced Threat Protection Azure z systemem Windows Defender ATP | Dokumentacja firmy Microsoft
description: "Integrowanie usługi Azure Advanced Threat Protection z Windows Defender ATP pokrycia wykrywania zagrożeń Pełna"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3521e500548b04febbff37d3dfe9150cf6f2d35b
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
---
*Dotyczy: Azure Advanced Threat Protection*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integrowanie Azure ATP z usługi Windows Defender ATP

Azure Advanced Threat Protection umożliwia Azure ATP można zintegrować z Windows Defender ATP, aby jeszcze bardziej kompleksowe rozwiązanie ochrony zagrożeń. Podczas Azure ATP monitoruje ruch na kontrolerach domeny, Windows Defender ATP monitoruje punktów końcowych, jednocześnie zapewniając jeden interfejs, z którego można chronić środowisko.

> [!NOTE]
> Integracja jest włączona tylko wtedy, gdy klient Windows Defender ATP prywatnej wersji zapoznawczej.
 
Dzięki integracji z systemem Windows Defender ATP do Azure ATP, możesz korzystać ze wszystkich możliwości obu usług i zabezpieczeniu środowiska, w tym:

- Autonomiczny czujniki i Azure czujników ATP: można sit bezpośrednio na kontrolerach domeny lub dublowanie portów z kontrolerów domeny do ATP do przechwytywania i analizowania ruchu sieciowego na wiele protokołów (na przykład protokołu Kerberos, DNS, RPC, NTLM i inne) do uwierzytelniania, Autoryzacja i zbierania informacji. 

-   Czujniki zachowania punktu końcowego: osadzone w systemie Windows 10, takich czujników zbierania i przetwarzania behawioralnej sygnały z systemu operacyjnego (na przykład procesu, rejestru, plików i komunikacji sieciowej) i wysyła te dane czujników do chmury prywatnej, izolowanych, wystąpienie programu Windows Defender ATP.

- Analiza zabezpieczeń w chmurze: wykorzystanie danych big data, uczenie maszynowe i unikatowe widoku firmy Microsoft w ekosystemie systemu Windows (takie jak [Microsoft usuwania złośliwego oprogramowania](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), produktów chmury przedsiębiorstwa (takich jak Office 365), i zasoby online (na przykład reputacji Bing i adres URL SmartScreen), behawioralnej sygnały są przetłumaczyć wgląd, wykrywania i zalecane odpowiedzi na zagrożenia zaawansowane.

- Analizy zagrożeń: wygenerowany myśliwi Microsoft zespoły zabezpieczeń i rozszerzony o analizy zagrożeń zapewniana przez partnerów, zagrożenie analizy umożliwia Windows Defender ATP do identyfikowania osoby atakującej narzędzia, technik i procedur i generowania alertów podczas te są przestrzegane czujnik zebranych danych.

Technologia ATP Azure wykrywa wiele podejrzanych działań koncentrujących się na tym łańcuchu kill ataku przez kilka faz:

- Rekonesans, podczas których osoby atakujące Zbierz informacje dotyczące sposobu środowiska są wbudowane i jakie różne zasoby są i którymi obiektami istnieje. Tworzenie one zazwyczaj ich planu dla następnej fazy ataku.

- Cykl penetracji sieci, podczas którego osoby atakujące inwestują czas i wysiłek w rozszerzanie obszaru ataku wewnątrz sieci.

- Podczas którego osoba atakująca przechwytuje informacje, dzięki czemu można wznowić ich kampanii przy użyciu różnych zestawów punktów wejścia, poświadczeń i technik zdominowanie domeny (trwałości).

W tym samym czasie Windows Defender ATP korzysta z technologii firmy Microsoft i doświadczenia w celu wykrywania zaawansowanych ataków przez, zapewniając:

- Wykrywanie ataków opartych na zachowanie, obsługiwane w chmurze, zaawansowane<br></br>Znajduje atakami wprowadzone go poza innych zabezpieczenia (po wykrywanie naruszenia), można wykonać, skorelowane alerty do znanych i nieznanych atakujący próby Ukryj ich działania w punktach końcowych.

- Oś czasu sformatowanego w przypadku postępowania śledczego i środki zaradcze<br></br>Zbadaj łatwo zakresu naruszenia lub podejrzane zachowania na dowolnym komputerze za pomocą zaawansowanych maszyny osi czasu. Plik, adresy URL i spisu połączenia sieciowe w sieci. Uzyskać szczegółowe informacje o dodatkowych za pomocą bezpośrednich zbierania i analizowania ("detonację") dla dowolnego pliku lub adresy URL.

- Wbudowane bazy wiedzy analizy zagrożeń unikatowy<br></br>Światłowodowa bezkonkurencyjne zagrożeń zawiera informacje aktora i konwersji kontekst dla każdego z procesorem intel wykrywanie zagrożeń — łączenie analizy pierwszy i innych źródeł.

## <a name="prerequisites"></a>Wymagania wstępne

Aby włączyć tę funkcję, potrzebna jest licencja Azure ATP i programu Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Integrowanie Azure ATP z systemem Windows Defender ATP

1. Ustaw obszar roboczy chcesz zintegrować jako **głównej**. Tylko jeden obszar roboczy może być podstawowym obszarem roboczym i tylko podstawowym obszarem roboczym można zintegrować z innymi usługami. Chcąc, w pewnym momencie w przyszłości, należy utworzyć ten obszar roboczy nie jest już podstawowym obszarem roboczym, należy najpierw usunąć integrację przed skonfigurowaniem jako innego niż podstawowy.

 ![podstawowym obszarem roboczym](./media/primary-workspace.png)

2. Kliknij przycisk **konfiguracji**, a następnie w obszarze **źródeł danych** wybierz **Windows Defender ATP**. Następnie kliknij łącze, aby **zarządzania obszaru roboczego**. Jest to dostępne tylko wtedy, jeśli masz licencję dla Windows Defender ATP i wykonano już procesu dołączania dla Windows Defender ATP. 

3. W podstawowym obszarem roboczym kliknij koło zębate ustawień.

 ![Integracja z obszaru roboczego](./media/edit-workspace.png)
 
3. Ustaw integrację **na**. 

 ![Włącz integrację](./media/enable-integration.png)

4. W [portalu Windows Defender ATP](https://beta.securitycenter.windows.com/preferences/advanced), przejdź do **ustawienia**, **zaawansowane funkcje** i ustaw **integracji Azure ATP** do  **ON**. 

 ![Integracja Włącz Windows Defender ATP](./media/wd-atp-enable.png)

5. Aby sprawdzić stan integracji, w portalu Azure ATP obszaru roboczego, przejdź do **ustawienia** , a następnie **integracji Windows Defender ATP**. Można wyświetlić stan integracji; Jeśli dany element jest nieprawidłowe, zostanie wyświetlony błąd. Można również sprawdzić, które obszaru roboczego jest zintegrowany z Windows Defender ATP.

## <a name="how-it-works"></a>Jak to działa

Po Azure ATP i programu Windows Defender ATP są w pełni zintegrowane, w portalu Azure ATP obszaru roboczego, w oknie podręcznym mini profilu i strony profilu jednostki, każdy obiekt, który istnieje w systemie Windows Defender ATP zawiera znak, aby pokazać, że jest zintegrowane z systemem Windows Usługa Defender ATP 

 ![Alerty systemu Windows Defender ATP](./media/profile-alerts-wd.png)

Jeśli obiekt zawiera alerty w programie Windows Defender ATP, jest liczbą obok wskaźnika informacją o tym, jak wiele alertów zostały zgłoszone.

 ![Azure alerty ATP](./media/atp-integrated-wd-icon-alerts.png)

Po kliknięciu wskaźnika są wprowadzane do portalu Windows Defender ATP, gdzie można przeglądać i ograniczyć alerty. Jeśli jednostka nie jest rozpoznawany przez program Windows Defender ATP, wskaźnik jest szary. 

 ![Szary Windows Defender ATP](./media/wd-grey.png)

W portalu Windows Defender ATP po kliknięciu punktu końcowego można wyświetlić alerty Azure ATP. Po kliknięciu alerty dla tego obiektu w programie Windows Defender ATP w Azure ATP zostanie otwarta strona profilu jednostki. 

 ![Alerty systemu Windows Defender ATP](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Zobacz też

- [Badanie ścieżek penetracja sieci Azure ATP](use-case-lateral-movement-path.md)
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura ATP Azure](atp-architecture.md)
- [Zainstaluj ATP](install-atp-step1.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)

