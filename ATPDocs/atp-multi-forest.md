---
title: Pomoc techniczna platformy Azure lasu odpowiednie zaawansowanej ochrony przed zagrożeniami | Dokumentacja firmy Microsoft
description: Obsługa wielu lasów usługi Active Directory w usłudze Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40bd468226f3c8db17663d02aed561b77cc2a128
ms.sourcegitcommit: bbbe808c08ce703a314c82b46aedaae79ab256a3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2018
ms.locfileid: "48848494"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="azure-advanced-threat-protection-multi-forest-support"></a>Pomoc techniczna platformy Azure obejmującego wiele lasów zaawansowanej ochrony przed zagrożeniami


## <a name="multi-forest-support-set-up"></a>Obsługa wielu lasów, konfigurowanie 

Narzędzie Azure ATP może obsługiwać organizacji z wieloma lasami, które daje możliwość i łatwo monitorować działania użytkowników profilów między lasami — z jedną taflę szkła. 

Przedsiębiorstwa to organizacje zazwyczaj mają wiele lasów usługi Active Directory — często używane do różnych celów, w tym starszą infrastrukturę na z fuzji firmowe i przejęcia, rozmieszczenie geograficzne i granice zabezpieczeń (czerwony lasów). Możesz chronić wiele lasów, za pomocą narzędzia Azure ATP, zapewniając możliwość monitorować i badać za pośrednictwem jedną taflę szkła.

Możliwość obsługi wielu lasów usługi Active Directory umożliwia wykonywanie następujących czynności:
-   Wyświetlanie i badanie działań wykonywanych przez użytkowników w wielu lasach z jedną taflę szkła. 
-   Ulepszone wykrywanie i zmniejszenie liczby wyników fałszywie dodatnich, zapewniając zaawansowane rozwiązania integracji i konto usługi Active Directory. 
-   Większą kontrolę i łatwiejsze wdrażanie. Monitorowanie alertów i ulepszone raportowanie dla pokrycia w całej organizacji, gdy kontrolery domeny są monitorowane przy użyciu pojedynczej konsoli narzędzia Azure ATP.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Jak narzędzia Azure ATP wykrywa działania w wielu lasach 

Aby wykryć działania między lasami, czujniki narzędzia Azure ATP zapytania kontrolerów domeny w lasach zdalnych, aby utworzyć profile dla wszystkich jednostek zaangażowani, w tym użytkownicy i komputery z lasów zdalnego. 

> [!NOTE]
> - Usługa Azure ATP czujników można zainstalować na wszystkich lasów (jeśli istnieje zaufanie jednokierunkowe minimalna).
> - Użytkownik, należy skonfigurować w konsoli usługi Azure ATP w obszarze **usługa katalogowa** musi być zaufana w innych lasach.


W przypadku lasów, na których nie narzędzia Azure ATP czujników są zainstalowane narzędzia Azure ATP wciąż mogą przeglądać i monitorować działania pochodzące z tych lasów. Czujniki zaawansowanej ochrony przed zagrożeniami, zainstalowane można badać wszystkich połączonych kontrolery domen w lesie zdalnym Rozpoznaj użytkowników, komputerów i tworzyć profile dla każdego z nich. 

## <a name="installation-requirements"></a>Wymagania dotyczące instalacji 

-   Jeśli czujników autonomiczne narzędzia Azure ATP są zainstalowane na komputerach autonomicznych, a nie bezpośrednio na kontrolerach domeny, upewnij się, że maszyny mogą komunikować się ze wszystkimi kontrolery domen w lesie zdalnym przy użyciu protokołu LDAP. 
- Użytkownik, należy skonfigurować w konsoli usługi Azure ATP w obszarze **usługa katalogowa** musi być zaufana w innych lasach i musi mieć co najmniej tylko uprawnienia odczytu do wykonywania zapytań LDAP na kontrolerach domeny.

- Aby dla usługi Azure ATP do komunikowania się za pomocą narzędzia Azure ATP czujników i zure zaawansowanej ochrony przed zagrożeniami autonomiczny czujników należy otworzyć następujące porty na każdym czerpać, na którym jest zainstalowany czujnik narzędzia Azure ATP:

 
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
-   Podczas czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure wykryje działanie wielu lasów, mogą pojawić ruchu ad hoc. W takiej sytuacji czujników narzędzia Azure ATP będzie wysyłać kwerendy LDAP do odpowiednich kontrolerach domeny w celu pobrania informacji o jednostkach. 

## <a name="known-limitations"></a>Znane ograniczenia
-   Logowania interakcyjnego, wykonywanych przez użytkowników w jednym lesie na dostęp do zasobów w innym lesie nie są wyświetlane na pulpicie nawigacyjnym usługi Azure ATP.



## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-architecture.md)
- [Zainstaluj narzędzie Azure ATP](install-atp-step1.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)

