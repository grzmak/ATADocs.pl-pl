---
title: Konfigurowanie funkcji przekazywania zdarzeń Windows w usłudze Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opisuje opcje konfigurowania przekazywania zdarzeń Windows za pomocą narzędzia Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1b37bcbfc304ee0ef71d80eb84f6298d64e50d3f
ms.sourcegitcommit: eebf1156aaae199b6aaa7e431cd6372e572b1e9f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/01/2018
ms.locfileid: "39396421"
---
*Dotyczy: Azure Advanced Threat Protection wersji 1.9*



# <a name="configuring-windows-event-forwarding"></a>Konfigurowanie funkcji przekazywania zdarzeń systemu Windows

> [!NOTE]
> Czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure automatycznie odczytuje zdarzenia lokalnie — bez konieczności konfigurowania przekazywania zdarzeń.


W celu zwiększenia możliwości wykrywania, narzędzia Azure ATP potrzebuje następujących zdarzeń Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 i 7045. One może odczytywać je automatycznie za pomocą czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure lub w przypadku, gdy czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure nie została wdrożona, zdarzenia mogą być przekazywane do czujnika autonomicznego narzędzia Azure ATP w jeden z dwóch sposobów, konfigurując czujnik autonomiczny narzędzia Azure ATP do nasłuchiwania zdarzeń SIEM lub przez configuri Przekazywanie zdarzeń Windows ng.

> [!NOTE]
> Sprawdź, czy kontroler domeny jest prawidłowo skonfigurowane i Przechwytywanie zdarzeń wymagane.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>Konfiguracja funkcji WEF dla usługi Azure ATP czujnik autonomiczny firmy za pomocą funkcji dublowania portów

Po skonfigurowaniu funkcji dublowania portów z kontrolerów domeny do usługi Azure ATP czujnik autonomiczny, wykonaj poniższe instrukcje konfigurowania przekazywania zdarzeń Windows za pomocą konfiguracji inicjowanej przez obiekt źródłowy. Jest to jeden ze sposobów konfigurowania przekazywania zdarzeń systemu Windows. 

**Krok 1: Dodaj konto usługi sieciowej do grupy Czytelnicy dzienników zdarzeń domeny** 

W tym scenariuszu założono, że czujnik autonomiczny narzędzia Azure ATP jest elementem członkowskim domeny.

1.  Otwórz narzędzie Użytkownicy usługi Active Directory i komputerów, przejdź do **BuiltIn** folder i kliknij dwukrotnie plik **Czytelnicy dzienników zdarzeń**. 
2.  Wybierz **członków**.
4.  Jeśli pozycji **Usługa sieciowa** nie ma na liście, kliknij przycisk **Dodaj** i wpisz **Usługa sieciowa** w polu **Wprowadź nazwy obiektów do wybrania**. Następnie kliknij opcję **Sprawdź nazwy** i kliknij dwukrotnie przycisk **OK**. 

Po dodaniu **Usługa sieciowa** do **Czytelnicy dzienników zdarzeń** grupie, przeprowadź ponowny rozruch kontrolerów domeny, aby zmiana zaczęła obowiązywać.

**Krok 2: Utwórz zasady na kontrolerach domeny, aby skonfigurować ustawienie Konfiguruj docelowego Menedżera subskrypcji** 
> [!Note] 
> Można utworzyć dla tych ustawień zasad grupy i zastosowanie zasad grupy do każdego kontrolera domeny monitorowanych przez czujnik autonomiczny narzędzia Azure ATP. Poniższe kroki modyfikację zasad lokalnych kontrolera domeny.     

1.  Uruchom następujące polecenie na każdym kontrolerze domeny: *winrm quickconfig*
2.  W wierszu polecenia wpisz ciąg *gpedit.msc*.
3.  Rozwiń węzeł **Konfiguracja komputera > Szablony administracyjne > Składniki systemu Windows > Przesyłanie dalej zdarzeń**

 ![Obraz edytora lokalnych zasad grupy](media/wef%201%20local%20group%20policy%20editor.png)

4.  Kliknij dwukrotnie **Konfiguruj docelowego Menedżera subskrypcji**.
   
    1.  Wybierz opcję **Włączono**.
    2.  W obszarze **opcje**, kliknij przycisk **Pokaż**.
    3.  W obszarze **SubscriptionManagers**, wprowadź następujące wartości i kliknij przycisk **OK**: *Server=http://<fqdnATPSensor>: 5985/wsman/SubscriptionManager/WEC,Odśwież=10* (For example: serwer=http://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Odśwież=10)
 
   ![Obraz konfigurowania subskrypcji docelowej](media/wef%202%20config%20target%20sub%20manager.png)
   
    5.  Kliknij przycisk **OK**.
    6.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *gpupdate /force*. 

**Krok 3: Wykonaj następujące czynności na czujnik autonomiczny narzędzia Azure ATP** 

1.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *wecutil qc*
2.  Otwórz **Podgląd zdarzeń**. 
3.  Kliknij prawym przyciskiem myszy **subskrypcje** i wybierz **Utwórz subskrypcję**. 

   1.   Wprowadź nazwę i opis subskrypcji. 
   2.   Aby uzyskać **Dziennik docelowy**, upewnij się, że **zdarzenia przesyłane dalej** jest zaznaczone. Narzędzia Azure ATP mogła odczytywać zdarzenia, Dziennik docelowy musi być **zdarzenia przesyłane dalej**. 
   3.   Wybierz opcję **Zainicjowane przez komputer źródłowy** i kliknij przycisk **Wybierz grupy komputerów**.
        1.  Kliknij przycisk **Dodaj komputer w domenie**.
        2.  Wprowadź nazwę kontrolera domeny w polu **Wprowadź nazwę obiektu do wybrania**. Kliknij opcję **Sprawdź nazwy** i kliknij przycisk **OK**. 
       
        ![Obraz Podglądu zdarzeń](media/wef3%20event%20viewer.png)
   
        
        3.  Kliknij przycisk **OK**.
   4.   Kliknij przycisk **Wybierz zdarzenia**.

        1. Kliknij przycisk **Według dzienników** i wybierz opcję **Zabezpieczenia**.
        2. W polu **Obejmuje/wyklucza zdarzenie o identyfikatorze** wpisz numer zdarzenia i kliknij przycisk **OK**. Na przykład wpisz 4776, podobnie jak w następującym przykładzie:

 ![Obraz przedstawiający filtr kwerendy](media/wef-4-query-filter.png)

   5.   Kliknij prawym przyciskiem myszy utworzoną subskrypcję i wybierz **stan czasu wykonywania** aby zobaczyć, jeśli występują problemy ze stanem. 
   6.   Po kilku minutach Sprawdź, czy zdarzenia ustawione do przekazania są wyświetlane w zdarzeniach przekazanych w czujnik autonomiczny narzędzia Azure ATP.


Aby uzyskać więcej informacji, zobacz: [Konfigurowanie komputerów do przekazywania i zbierania zdarzeń](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Zobacz też

- [Zainstaluj narzędzie Azure ATP](install-atp-step1.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
