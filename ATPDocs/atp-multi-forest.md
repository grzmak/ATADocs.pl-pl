---
title: Pomoc techniczna platformy Azure lasu odpowiednie zaawansowanej ochrony przed zagrożeniami | Dokumentacja firmy Microsoft
description: Jak skonfigurować obsługę wielu lasów usługi Active Directory w usłudze Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/20/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a48bf96bd6a71282455d932a35aac23ba4c8193a
ms.sourcegitcommit: 7909deafdd9323f074d0ff2f590e307bcfaaabad
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2018
ms.locfileid: "39202136"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="install-azure-atp---step-9"></a>Zainstaluj narzędzie Azure ATP - kroku 9

>[!div class="step-by-step"]
[«Krok 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Krok 9.  Konfigurowanie obsługi wielu lasów usługi Azure Advanced Threat Protection

Narzędzie Azure ATP może obsługiwać organizacji z wieloma lasami, które umożliwia monitorowanie działań związanych z możliwością i profilów użytkowników w lasach. 

Przedsiębiorstwo może mieć wiele lasów usługi Active Directory — często używane do różnych celów, w tym starszą infrastrukturę na z fuzji firmowe i przejęcia, rozmieszczenie geograficzne i granice zabezpieczeń (czerwony lasów). Możesz chronić wiele lasów, za pomocą narzędzia Azure ATP, raportowanie wszystkie dane do jednego, podstawowy obszar roboczy, zapewniając możliwość monitorować i badać za pośrednictwem jedną taflę szkła.

Możliwość obsługi wielu lasów usługi Active Directory umożliwia wykonywanie następujących czynności:
-   Można przeglądać i badanie działań wykonywanych przez użytkowników w wielu lasach z jedną taflę szkła. 
-   Obsługa wielu lasu zwiększa wykrywania i zmniejszenie liczby fałszywych alarmów dzięki zaawansowanej integracji usługi Active Directory i rozpoznawanie konta. 
-   Ponieważ obsługa wielu foresst eliminuje konieczność stosowania wielu obszarów roboczych, masz większą kontrolę i łatwiejsze wdrażanie, podczas gdy kontrolery domeny są wszystkie monitorować centralnie, przy użyciu jednego narzędzia Azure ATP konsoli, która zapewnia lepsze monitorowania alertów i Raportowanie dla pokrycia w całej organizacji.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Jak narzędzia Azure ATP wykrywa działania w wielu lasach 

Aby wykryć działania między lasami, czujniki narzędzia Azure ATP zapytania kontrolerów domeny w lasach zdalnych, aby utworzyć profile dla wszystkich jednostek zaangażowani, w tym użytkownicy i komputery z lasów zdalnego. 

> [!NOTE]
> - Usługa Azure ATP czujników można zainstalować na wszystkich lasów (jeśli istnieje zaufanie jednokierunkowe minimalna).
> - Użytkownik, należy skonfigurować w konsoli usługi Azure ATP w obszarze **usługa katalogowa** musi być zaufana w innych lasach.


W przypadku lasów, na których nie narzędzia Azure ATP czujników są zainstalowane narzędzia Azure ATP wciąż mogą przeglądać i monitorować działania pochodzące z tych lasów. Czujniki zaawansowanej ochrony przed zagrożeniami, zainstalowane można badać wszystkich połączonych kontrolery domen w lesie zdalnym rozwiązać użytkowników i maszyn i utworzyć profil dla każdego z nich. 

## <a name="installation-requirements"></a>Wymagania dotyczące instalacji 

-   Jeśli czujników autonomiczne narzędzia Azure ATP są zainstalowane na komputerach autonomicznych, a nie bezpośrednio na kontrolerach domeny, upewnij się, że maszyny mogą komunikować się ze wszystkimi kontrolery domen w lesie zdalnym przy użyciu protokołu LDAP. 
- Użytkownik, należy skonfigurować w konsoli usługi Azure ATP w obszarze **usługa katalogowa** musi być zaufana w innych lasach i musi mieć co najmniej tylko uprawnienia odczytu do wykonywania zapytań LDAP na kontrolerach domeny.

- Aby dla usługi Azure ATP przekazywane za pomocą zaawansowanej ochrony przed zagrożeniami, czujniki i czujniki autonomiczny zaawansowanej ochrony przed zagrożeniami należy otworzyć następujące porty na każdym czerpać, na którym zainstalowano czujnika zaawansowanej ochrony przed zagrożeniami:

 
  |Protokół|Transport|Port|Do/z|Kierunek|
  |----|----|----|----|----|
  |**Porty Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Usługa w chmurze Azure ATP|Wychodzące|
  |**Wewnętrznych portów**||||           
  |LDAP|TCP i UDP|389|Kontrolery domeny|Wychodzące|
  |Bezpieczny protokół LDAP (LDAPS)|TCP|636|Kontrolery domeny|Wychodzące|
  |LDAP do wykazu globalnego|TCP|3268|Kontrolery domeny|Wychodzące|
  |LDAPS do wykazu globalnego|TCP|3269|Kontrolery domeny|Wychodzące|


## <a name="multi-forest-support-network-traffic-impact"></a>Obsługa wielu lasu pomocy technicznej sieci ruchu wpływ 

W przypadku narzędzia Azure ATP mapuje lasów usługi, używa procesu, który ma wpływ na następujące czynności:

-   Po uruchomieniu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure zapytania zdalnego lasów usługi Active Directory i pobiera listę użytkowników i dane maszyny dla tworzenia profilu.
-   Co 5 minut, każdy czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wysyła zapytanie do jednego kontrolera domeny w każdej domenie, w każdym lesie, aby zamapować wszystkich lasów w sieci.
-   Każdy czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure mapuje lasów, używając obiektu "trustedDomain" w usłudze Active Directory, logowania i sprawdzanie typu zaufania.
-   Podczas czujnika zaawansowanej ochrony przed zagrożeniami wykryje działanie wielu lasów, mogą pojawić ruchu ad hoc. W takiej sytuacji czujników zaawansowanej ochrony przed zagrożeniami będzie wysyłać kwerendy LDAP do odpowiednich kontrolerach domeny w kolejności Pobierz informacje o jednostki. 

## <a name="known-limitations"></a>Znane ograniczenia
-   Logowania interakcyjnego, wykonywanych przez użytkowników w jednym lesie na dostęp do zasobów w innym lesie nie są wyświetlane na pulpicie nawigacyjnym usługi Azure ATP.


>[!div class="step-by-step"]
[«Krok 8](install-atp-step8-samr.md)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/aatpsizingtool)
- [Architektura usługi ATA](atp-architecture.md)
- [Instalowanie usługi ATA](install-atp-step1.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)

