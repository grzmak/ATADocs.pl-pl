---
title: Konfigurowanie funkcji przekazywania zdarzeń systemu Windows w Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opisuje opcje konfigurowania funkcji przekazywania zdarzeń systemu Windows za pomocą usługi Azure ATP
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
ms.openlocfilehash: df06235de3a29051f9ffcd889bb95936ed9fc27d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446092"
---
*Dotyczy: Azure Advanced Threat Protection wersji 1.9*



# <a name="configuring-windows-event-forwarding"></a>Konfigurowanie funkcji przekazywania zdarzeń systemu Windows

> [!NOTE]
> Czujnik Azure ATP automatycznie odczytuje zdarzenia lokalnie, bez konieczności konfigurowania funkcji przekazywania zdarzeń.


W celu zwiększenia możliwości wykrywania Azure ATP musi następujące zdarzenia systemu Windows: 4776, 4732 4733, 4728, 4729, 4756, 4757 i 7045. Można albo je odczytać automatycznie przez czujnik Azure ATP lub w przypadku, gdy czujnik Azure ATP nie została wdrożona, go mogą być przekazywane do czujnik autonomiczny Azure ATP w jeden z dwóch sposobów, konfigurując czujnik autonomiczny Azure ATP do nasłuchiwania zdarzeń SIEM lub przez configuri NG funkcji przekazywania zdarzeń systemu Windows.

> [!NOTE]
> Sprawdź, czy kontroler domeny jest prawidłowo skonfigurowane do przechwytywania zdarzeń wymagane.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>Konfiguracja WEF Azure ATP autonomiczny czujnika dublowanie portów

Po skonfigurowaniu funkcji dublowania portów z kontrolerów domeny czujnika autonomiczny Azure ATP wykonaj następujące instrukcje dotyczące konfigurowania funkcji przekazywania zdarzeń systemu Windows za pomocą konfiguracji źródła zainicjowane. Jest to jeden ze sposobów konfigurowania przekazywania zdarzeń systemu Windows. 

**Krok 1: Dodaj konto usługi sieciowej do grupy Czytelnicy dzienników zdarzeń domeny** 

W tym scenariuszu zakładać, że czujnik autonomiczny Azure ATP jest członkiem domeny.

1.  Otwórz przystawkę Użytkownicy usługi Active Directory i komputery, przejdź do **wbudowane** folder i kliknij dwukrotnie **Czytelnicy dzienników zdarzeń**. 
2.  Wybierz **członków**.
4.  Jeśli pozycji **Usługa sieciowa** nie ma na liście, kliknij przycisk **Dodaj** i wpisz **Usługa sieciowa** w polu **Wprowadź nazwy obiektów do wybrania**. Następnie kliknij opcję **Sprawdź nazwy** i kliknij dwukrotnie przycisk **OK**. 

Po dodaniu **usługi sieciowej** do **Czytelnicy dzienników zdarzeń** grupy, ponownego uruchamiania kontrolerów domeny, aby zmiany zaczęły obowiązywać.

**Krok 2: Utwórz zasady na kontrolerach domeny, aby skonfigurować ustawienie Konfiguruj docelowego Menedżera subskrypcji** 
> [!Note] 
> Można tworzyć dla tych ustawień zasad grupy i stosowania zasad grupy dla każdy z kontrolerów domeny monitorowanych przez czujnik autonomiczny Azure ATP. Poniższe kroki zmodyfikuj zasady lokalnego kontrolera domeny.     

1.  Uruchom następujące polecenie na każdym kontrolerze domeny: *winrm quickconfig*
2.  W wierszu polecenia wpisz ciąg *gpedit.msc*.
3.  Rozwiń węzeł **Konfiguracja komputera > Szablony administracyjne > Składniki systemu Windows > Przesyłanie dalej zdarzeń**

 ![Obraz edytora lokalnych zasad grupy](media/wef 1 local group policy editor.png)

4.  Kliknij dwukrotnie **konfigurowanie docelowej subskrypcji Menedżera**.
   
    1.  Wybierz opcję **Włączono**.
    2.  W obszarze **opcje**, kliknij przycisk **Pokaż**.
    3.  W obszarze **SubscriptionManagers**, wprowadź następujące wartości i kliknij przycisk **OK**: *Server = http: / /<fqdnATPSensor>: 5985/wsman/SubscriptionManager/WEC, Odśwież = 10* () For example: serwer = http://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC, Odśwież = 10)
 
   ![Obraz konfigurowania subskrypcji docelowej](media/wef 2 config target sub manager.png)
   
    5.  Kliknij przycisk **OK**.
    6.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *gpupdate /force*. 

**Krok 3: Wykonaj następujące czynności na czujnik autonomiczny Azure ATP** 

1.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *wecutil qc*
2.  Otwórz **Podgląd zdarzeń**. 
3.  Kliknij prawym przyciskiem myszy **subskrypcje** i wybierz **Utwórz subskrypcję**. 

   1.   Wprowadź nazwę i opis subskrypcji. 
   2.   Dla **Dziennik docelowy**, upewnij się, że **zdarzenia przekazane** jest zaznaczone. ATP Azure mają być odczytywane zdarzenia, dziennika docelowego musi być **zdarzenia przekazane**. 
   3.   Wybierz opcję **Zainicjowane przez komputer źródłowy** i kliknij przycisk **Wybierz grupy komputerów**.
        1.  Kliknij przycisk **Dodaj komputer w domenie**.
        2.  Wprowadź nazwę kontrolera domeny w polu **Wprowadź nazwę obiektu do wybrania**. Kliknij opcję **Sprawdź nazwy** i kliknij przycisk **OK**. 
       
        ![Obraz Podglądu zdarzeń](media/wef3 event viewer.png)
   
        
        3.  Kliknij przycisk **OK**.
   4.   Kliknij przycisk **Wybierz zdarzenia**.

        1. Kliknij przycisk **Według dzienników** i wybierz opcję **Zabezpieczenia**.
        2. W polu **Obejmuje/wyklucza zdarzenie o identyfikatorze** wpisz numer zdarzenia i kliknij przycisk **OK**. Na przykład wpisz 4776, podobnie jak w poniższym przykładzie:

 ![Obraz przedstawiający filtr kwerendy](media/wef-4-query-filter.png)

   5.   Kliknij prawym przyciskiem myszy utworzona subskrypcja i wybierz **stanu w czasie wykonywania** aby zobaczyć, jeśli występują problemy ze stanem. 
   6.   Po kilku minutach Sprawdź zdarzenia ustawienie przekazywanych jest wyświetlana w zdarzenia przekazane na czujnik autonomiczny Azure ATP.


Aby uzyskać więcej informacji, zobacz: [Konfigurowanie komputerów do przekazywania i zbierania zdarzeń](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Zobacz też

- [Zainstaluj Azure ATP](install-atp-step1.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)