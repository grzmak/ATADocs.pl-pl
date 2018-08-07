---
title: What's new in Azure ATP | Dokumentacja firmy Microsoft
description: W tym artykule opisano zainstalowane najnowsze wersje usługi Azure ATP i zawiera informacje o nowościach w każdej wersji.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/06/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0062fc22df357e338d8eaf446688ea8bba56019c
ms.sourcegitcommit: 14c05a210ae92d35100c984ff8c6d171db7c3856
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567954"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*

# <a name="whats-new-in-azure-atp"></a>What's new in Azure ATP 


## <a name="azure-atp-release-243"></a>Usługa Azure ATP release 2.43

Wydanej 5 sierpnia 2018 r.

- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów.



## <a name="azure-atp-release-242"></a>Usługa Azure ATP release 2,42

Wydana 29 lipca 2018 r.

- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 


## <a name="azure-atp-release-241"></a>Usługa Azure ATP release 2.41

Wydana 22 lipca 2018 r.

- **Obsługa wielu lasów usługi Azure ATP jest stopniowo wdrażana (wersja zapoznawcza)** <br> Narzędzie Azure ATP może teraz obsługiwać organizacji z wieloma lasami, które umożliwia monitorowanie działań związanych z możliwością i profilów użytkowników w lasach. Ta nowa funkcja pozwala na:

  - Wyświetlanie i badanie działań wykonywanych przez użytkowników w wielu lasach z jedną taflę szkła.
  - Zwiększa wykrywania i zmniejszenie liczby fałszywych alarmów dzięki zaawansowanej integracji usługi Active Directory i rozpoznawanie konta.
  - Uzyskaj lepsze monitorowanie alertów i raportowanie dla pokrycia w całej organizacji.


-   **Wykrywanie nowych zagrożeń: DCShadow**<br>Dwie nowe funkcje wykrywania zostały dodane do ochrony przed atakami w tle (DCShadow) kontrolera domeny:

    -   Podwyższanie poziomu kontrolera domeny podejrzane (potencjalny atak DCShadow) — wykrywanie pomaga wykrywać ataki, w których maszynę podszyć się pod kontroler domeny, a następnie próbuje przy użyciu replikacji się propagujące zmiany do innych kontrolerów domeny w domenie.

    -   Podejrzana replikacja żądania (potencjalny atak DCShadow) — to wykrywanie, który pomaga chronić przed atakami wykorzystującymi podjął próbę podwyższenia poziomu kontrolera domeny maszyn, które nie są kontrolerami domeny w celu zmiany obiektów katalogu.

-   **Ulepszone informacje o obniżenie poziomu szyfrowania**<br>Teraz wykrywanie obniżenia poziomu szyfrowania zawiera więcej informacji na temat określonego rodzaju atak: overpass--hash i bilet uwierzytelniania golden ticket, złośliwe oprogramowanie skeleton key. Ponadto te alerty mają zostały zagregowane umożliwiające łatwiejszego badania.
- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 



## <a name="azure-atp-release-240"></a>Usługa Azure ATP release 2,40

Wydanie: 15 lipca 2018 r.

- Teraz za pomocą wykrywania pass--ticket zawiera sekcja dowodów na stronie szczegółów alertu. Zapewnia to dodatkowe informacje dotyczące badania alertu.

- Flagi kontroli dostępu użytkownika, które znajdują się w profilu użytkownika w katalogu danych, obejmują teraz legendy, dzięki czemu można lepiej zrozumieć, których atrybutów znajdują się na i które są wyłączone.  

## <a name="azure-atp-release-239"></a>Usługa Azure ATP release 2.39

Wydanej 5 lipca 2018 r.
-   **Nowe wykrycie dodane: bilet protokołu Kerberos, uwierzytelniania golden - nieistniejące konto** (wersja zapoznawcza)<br>Wykrycie nowych pomaga chronić swoją organizację przed atakami, w których bilet uwierzytelniania golden ticket jest tworzony dla konta które nie istnieje w domenie. Aby uzyskać więcej informacji, zobacz [Przewodnik po podejrzanych działaniach usługi Azure Advanced Threat Protection](suspicious-activity-guide.md#golden-ticket)

- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 


## <a name="azure-atp-release-238"></a>Usługa Azure ATP release 2,38

Wydana 1 lipca 2018 r.

- Ta wersja zawiera poprawki i ulepszenia dla wielu problemów, a także ulepszenia w portalu usługi Azure ATP.

## <a name="azure-atp-release-237"></a>Usługa Azure ATP release 2,37

Wydanie: 24 czerwca 2018 r.

- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 

## <a name="azure-atp-release-236"></a>Usługa Azure ATP release 2,36

Wydana 17 czerwca 2018 r.

- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 


## <a name="azure-atp-release-235"></a>Usługa Azure ATP release 2.35

Wydana 10 czerwca 2018 r.
 
- **Wykrywanie nowych zagrożeń (wersja zapoznawcza)**<br></br>Od teraz, zaawansowanej ochrony przed zagrożeniami w usłudze Azure będzie korzystać z faktu, że jest to usługa w chmurze — gdzie nowe funkcje mogą być dostarczane w cykle — szybkie i umożliwiają wykrywanie nowych zagrożeń tak szybko, jak to możliwe. Te nowe funkcje wykrywania zostanie oznaczone jako "wersja zapoznawcza" po raz pierwszy są zwolnione. Zazwyczaj nowe wykrycie zostaną przeniesione z wersji zapoznawczej do ogólnej dostępności w ciągu kilku tygodni. Domyślnie zostanie wyświetlony podgląd wykrywania. Aby dowiedzieć się, jak zrezygnować, zobacz [wykrywania w wersji zapoznawczej](working-with-suspicious-activities.md#preview-detections).
 
- **Podejrzane wykrywania sieci VPN**<br></br>W tej wersji wprowadzono wersję zapoznawczą Wykrywanie podejrzanych sieci VPN. Narzędzie Azure ATP uczy się zachowania użytkowników sieci VPN, łącznie z maszynami, użytkownicy zalogowani do i lokalizacje, w których użytkownikom łączenie się z, a następnie powiadamia użytkownika, gdy istnieje odchylenie od oczekiwanego zachowania. Aby uzyskać więcej informacji, zobacz [Wykrywanie podejrzanych VPN](suspicious-activity-guide.md#suspicious-vpn-detection).

- **Opóźnione aktualizacji**<br></br>Masz teraz możliwość ustawienia usługi Azure ATP czujników do zaktualizowania w późniejszym czasie, każdym razem, gdy aktualizacje usługi Azure ATP. Można teraz ustawić każdego czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure **opóźnione aktualizacji** tak, aby go spowoduje zaktualizowanie 24 godziny po zaktualizowaniu usługi w chmurze usługi Azure ATP. Ta funkcja umożliwia testowanie aktualizacji na czujników testów określonych i aktualizować tylko z czujników produkcji później. Jeśli zostanie wykryty problem podczas pierwszego cyklu aktualizacji, należy otworzyć bilet pomocy technicznej. Aby uzyskać więcej informacji, zobacz [czujników aktualizacji usługi Azure ATP](sensor-update.md).

- **Wykrywanie implementacji zaktualizowane nietypowego protokołu**<br></br>Teraz wykrywanie implementacja nietypowego protokołu zawiera więcej informacji. Teraz możesz znaleźć, w których potencjalnych ataków narzędzia Azure ATP podejrzewa jest w miejscu pracy w sieci. Aby uzyskać więcej informacji, zobacz [Przewodnik po podejrzanych działaniach](suspicious-activity-guide.md).
 
- **Czujnik nieaktualne alertu**<br></br>Narzędzie Azure ATP obejmuje nowy alert monitorowania z informacją, czy czujnik jest więcej niż trzy wersje przestarzałe. Jeśli widzisz ten alert, należy zaktualizować czujnika lub zbadać, dlaczego czujnika nie są automatycznie aktualizowane. Jeśli alert będzie się powtarzać, odinstaluj i ponownie zainstaluj czujnika.

- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 

## <a name="azure-atp-release-234"></a>Usługa Azure ATP release 2.34

Wydana 3 czerwca 2018 r.
 
- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 

 
## <a name="azure-atp-release-233"></a>Usługa Azure ATP release 2,33

Wydana 27 maja 2018 r.

- Funkcja w wersji zapoznawczej: Azure ATP obsługuje teraz nowe języki i 13 nowych ustawień regionalnych:
    - Czeski
    - Węgierski
    - Włoski
    - Koreański
    - Holenderski
    - Polski
    - Portugalski (Brazylia)
    - Portugalski (Portugalia)
    - Rosja
    - Szwedzki
    - Turecki
    - Chiński (Chiny)
    - Chiński (Tajwan)



## <a name="azure-atp-release-232"></a>Usługa Azure ATP release 2.32

Wydana 13 maja 2018 r.
 
- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 

## <a name="azure-atp-release-231"></a>Usługa Azure ATP release 2.31

Wydana 6 maja 2018 r.
 
- Wprowadzono ulepszenia do rozpoznawania nazw. W ramach tego procesu, oprócz rozwiązania active RPC i NetBIOS czujnika mogą wydawać TLS klienta Hello pakiet do punktu końcowego protokołu RDP (3389) portu. 
- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 

## <a name="azure-atp-release-230"></a>Usługa Azure ATP release 2,30

Wydana 29 kwietnia 2018 r.
 
- Podejrzane działania obniżenie poziomu szyfrowania obejmują teraz sekcji dowód, który opisano objawy, wykrytych przez narzędzia Azure ATP powodujące podejrzewać, że działanie obniżenia poziomu szyfrowania odwzorowanie. 
-   Narzędzie Azure ATP używa teraz Orchestrator E-mail Azure we wszystkich wiadomościach e-mail wysyłanych z usługi Azure ATP, w tym podejrzanych działań monitorowania alertów i raportów. Zobaczysz, że te powiadomienia e-mail wykonaj teraz spójny format łatwe w użyciu i pliki programu Excel będzie połączony z wiadomości e-mail, które mają być pobrane z konsoli.
 
 

## <a name="azure-atp-release-229"></a>Usługa Azure ATP release 2.29

Wydana 22 kwietnia 2018 r.
 
- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 
 
 
## <a name="azure-atp-release-228"></a>Usługa Azure ATP release 2.28

Wydanie: 15 kwietnia 2018 r.
 
-   Użytkownicy, którzy są członkami grupy ról usługi Azure ATP użytkownikom i Azure ATP użytkownikom teraz mieć uprawnienia do wyświetlania alertów monitorowania.
- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 


## <a name="azure-atp-release-227"></a>Usługa Azure ATP release 2,27

Wydana 8 kwietnia 2018 r.

- Masz teraz możliwość zapewnienia opinie użytkowników z górnego paska nawigacyjnego. Klikając ikonę uśmiechniętej buźki na pasku menu umożliwia wysłanie wiadomości e-mail do zespołu usługi Azure Advanced Threat Protection z Twoją opinią.

- Ta wersja zawiera poprawki i ulepszenia w przypadku wielu problemów. 
 

## <a name="azure-atp-release-226"></a>Usługa Azure ATP release 2.26

Wydanie: 25 marca 2018 r.

- W przypadku narzędzia Azure ATP alerty o podejrzanym działaniu, które możesz zidentyfikować jako niegroźne wynik dodatni (prawidłowe działanie nie będący podejrzanego działania) masz możliwość wykluczenia komputerów i adresów IP dla więcej wykrywania zagrożeń, w tym: obniżenie poziomu szyfrowania, LDAP atak siłowy, sfałszowany element PAC, wymuś metodą ataku siłowego i ataków typu Pass--hash.
-   Ulepszono wydajności czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.
-   Nowy region została dodana do wdrożenia obszaru roboczego, można teraz wdrożyć obszaru roboczego w Azji. 


## <a name="azure-atp-release-225"></a>Usługa Azure ATP release 2,25

Wydana 18 marca 2018 r.

- Uwierzytelnianie wieloskładnikowe (MFA) jest teraz obsługiwane w przypadku narzędzia Azure ATP. Dzierżaw przy użyciu uwierzytelniania Wieloskładnikowego można teraz wprowadzić portalu usługi Azure ATP.
- Narzędzie Azure ATP ma teraz [ **stan systemu** ](https://health.atp.azure.com/) stronę, aby dostarczyć informacji w portalu zarządzania obszarami roboczymi jest w górę, jak i aktywnych, jeśli występują problemy z rozwiązaniami do wykrywania i czujnik jest możliwość wysyłania ruchu do chmury. Możesz uzyskać dostęp **stan systemu** na pasku menu Narzędzia Azure ATP.


## <a name="azure-atp-release-224"></a>Usługa Azure ATP release 2.24

Wydana 11 marca 2018 r.

**Nowe i zaktualizowane funkcje wykrywania**
  - Podejrzanie utworzenie usługi — osoby atakujące usiłują podwyższyć do uruchamiania usług podejrzane w sieci. Narzędzie Azure ATP zgłasza teraz alert, gdy zidentyfikuje ono, że ktoś na określonym komputerze działa Nowa usługa, która jest podejrzana. Wykrywanie bazuje na zdarzeniach (a nie ruch sieciowy) i zostanie wykryty na dowolny kontroler domeny w sieci, która przekazuje zdarzenia 7045 do usługi Azure ATP. Aby uzyskać więcej informacji, zobacz [Przewodnik po podejrzanych działaniach](suspicious-activity-guide.md).

**Ulepszone badania**
  - Narzędzie Azure ATP obejmuje wzbogacony [profilu jednostki](entity-profiles.md). Profilu jednostki umożliwia to platforma, która jest przeznaczona dla szczegółowe badanie działań użytkownika, obejmuje to zasoby, które są dostępne, komputerów, które mogą się zalogować i wielu innych. Profilu jednostki również zawiera dane katalogu i pozwala na identyfikację potencjalnych ścieżek penetracji sieci do lub z jednostki, dzięki któremu można dowiedzieć się więcej na temat potencjalnych naruszeń w organizacji.

  - Zaawansowanej ochrony przed zagrożeniami umożliwia ręczne tag jednostki jako *poufnych* do zwiększenia wykrywania i monitorowania. To tagowanie ma wpływ na wiele wykrywania usługi Azure ATP, np. wykrywania modyfikacji wrażliwych grup i [ścieżki ruchu poprzecznego](use-case-lateral-movement-path.md), które zależą od jednostek, które są traktowane jako poufne.

**Nowe raporty pomagają w badaniach**
  - [Hasła ujawnione w postaci zwykłego tekstu raporcie](reports.md) pozwala wykrywać, gdy services wysłać poświadczenia konta są wysyłane w postaci zwykłego tekstu. Dzięki temu można zbadać usług i zwiększyć poziom zabezpieczeń sieci. Ten raport zastępuje alertów podejrzanych działań w formie zwykłego tekstu.
  - [Boczne ścieżki ruchu do wrażliwych kont raportu](reports.md) zawiera listę kont poufnych, które są udostępniane za pośrednictwem ścieżki ruchu poprzecznego. Dzięki temu można zmniejszyć tych ścieżek i ochrony sieci, aby zminimalizować ryzyko powierzchni ataku. Pozwala to zapobiegać penetracji sieci, dzięki czemu osoby atakujące nie można przenieść w sieci między użytkownicy i komputery, do momentu ich trafień Pula nagród zabezpieczeń wirtualnego: poświadczenia konta administratora poufnych.

- Możesz teraz łatwo zapewnić dostęp do dokumentacji z linkiem w alert dotyczący podejrzanego działania, aby wyświetlić [kroki badania, które można wykonać](suspicious-activity-guide.md). 

**Ulepszenia wydajności**
 -  Infrastruktura czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure poprawiła wydajność: zagregowany widok ruchu włącza optymalizację potoku procesora CPU i pakietów, a następnie ponownie używa gniazda na kontrolerach domeny, aby zminimalizować sesji SSL do kontrolera domeny.

## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Usługa Azure Planowanie pojemności zaawansowanej ochrony przed zagrożeniami](atp-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)