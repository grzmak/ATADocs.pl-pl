---
title: "Konfigurowanie przekazywania zdarzeń systemu Windows w usłudze Advanced Threat Analytics | Microsoft Docs"
description: "Opisuje opcje konfigurowania przekazywania zdarzeń w systemie Windows za pomocą usługi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/29/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: fb34b1d10e923620e1c5e59ef210ebbac15e1ef0
ms.sourcegitcommit: 9ce330726e5de8c05eae6a20d3e6c1d8bef3cd0e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*



# <a name="configuring-windows-event-forwarding"></a>Konfigurowanie funkcji przekazywania zdarzeń systemu Windows

> [!NOTE]
> W przypadku usługi ATA w wersji 1.8 i nowszych nie trzeba już konfigurować zbierania zdarzeń dla uproszczonych bram usługi ATA. Uproszczona brama usługi ATA może teraz odczytywać zdarzenia lokalnie — bez potrzeby konfigurowania przekazywania zdarzeń.


W celu zwiększenia możliwości wykrywania usługa ATA potrzebuje zdarzeń systemu Windows z identyfikatorami 4776, 4732, 4733, 4728, 4729, 4756, 4757. Można albo je odczytać automatycznie przez bramę ATA Lightweight Gateway lub w przypadku bramy ATA Lightweight Gateway nie została wdrożona, jego może być przekazywany do bramy usługi ATA na jeden z dwóch sposobów przez skonfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM lub przez skonfigurowanie zdarzeń systemu Windows Przekazywanie.



### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Konfiguracja funkcji przekazywania zdarzeń (WEF) bramy usługi ATA z dublowaniem portów

Po skonfigurowaniu dublowania portów z kontrolerów domeny z bramą usługi ATA postępuj zgodnie z poniższymi instrukcjami, aby skonfigurować przekazywanie zdarzeń systemu Windows za pomocą konfiguracji inicjowanej przez obiekt źródłowy. Jest to jeden ze sposobów konfigurowania przekazywania zdarzeń systemu Windows. 

**Krok 1: Dodaj konto usługi sieciowej do grupy Czytelnicy dzienników zdarzeń domeny** 

W tym scenariuszu zakładamy, że brama usługi ATA należy do domeny.

1.  Otwórz narzędzie Użytkownicy i komputery usługi Active Directory, przejdź do folderu **BuiltIn** i dwukrotnie kliknij grupę **Czytelnicy dzienników zdarzeń**. 
2.  Wybierz **członków**.
4.  Jeśli pozycji **Usługa sieciowa** nie ma na liście, kliknij przycisk **Dodaj** i wpisz **Usługa sieciowa** w polu **Wprowadź nazwy obiektów do wybrania**. Następnie kliknij opcję **Sprawdź nazwy** i kliknij dwukrotnie przycisk **OK**. 

Pamiętaj, że po dodaniu elementu **Usługa sieciowa** do grupy **Czytelnicy dzienników zdarzeń** musisz ponownie uruchomić kontrolery domeny, aby zmiana zaczęła obowiązywać.

**Krok 2: Utwórz zasady na kontrolerach domeny, aby skonfigurować ustawienie Konfiguruj docelowego Menedżera subskrypcji** 
> [!Note] 
> Można tworzyć dla tych ustawień zasady grupy i stosować zasady grupy do każdego kontrolera domeny monitorowanego przez bramę usługi ATA. Poniższe kroki umożliwiają modyfikację zasad lokalnych kontrolera domeny.     

1.  Uruchom następujące polecenie na każdym kontrolerze domeny: *winrm quickconfig*
2.  W wierszu polecenia wpisz ciąg *gpedit.msc*.
3.  Rozwiń węzeł **Konfiguracja komputera > Szablony administracyjne > Składniki systemu Windows > Przesyłanie dalej zdarzeń**

 ![Obraz edytora lokalnych zasad grupy](media/wef 1 local group policy editor.png)

4.  Kliknij dwukrotnie opcję **Konfiguruj docelowego Menedżera subskrypcji**.
   
    1.  Wybierz opcję **Włączono**.
    2.  W obszarze **Opcje** kliknij opcję **Pokaż**.
    3.  W obszarze **Menedżerowie subskrypcji** wprowadź poniższą wartość, a następnie kliknij przycisk **OK**:  *Server = http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (na przykład: Server = http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Obraz konfigurowania subskrypcji docelowej](media/wef 2 config target sub manager.png)
   
    5.  Kliknij przycisk **OK**.
    6.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *gpupdate /force*. 

**Krok 3: W odniesieniu do bramy usługi ATA wykonaj następujące kroki** 

1.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *wecutil qc*
2.  Otwórz **Podgląd zdarzeń**. 
3.  Kliknij prawym przyciskiem myszy węzeł **Subskrypcje** i wybierz polecenie **Utwórz subskrypcję**. 

   1.   Wprowadź nazwę i opis subskrypcji. 
   2.   Upewnij się, że w obszarze **Dziennik docelowy** jest zaznaczona opcja **Zdarzenia przesyłane dalej**. Aby usługa ATA mogła odczytywać zdarzenia, dla dziennika docelowego musi być wybrana opcja **Zdarzenia przesyłane dalej**. 
   3.   Wybierz opcję **Zainicjowane przez komputer źródłowy** i kliknij przycisk **Wybierz grupy komputerów**.
        1.  Kliknij przycisk **Dodaj komputer w domenie**.
        2.  Wprowadź nazwę kontrolera domeny w polu **Wprowadź nazwę obiektu do wybrania**. Kliknij opcję **Sprawdź nazwy** i kliknij przycisk **OK**. 
       
        ![Obraz Podglądu zdarzeń](media/wef3 event viewer.png)
   
        
        3.  Kliknij przycisk **OK**.
   4.   Kliknij przycisk **Wybierz zdarzenia**.

        1. Kliknij przycisk **Według dzienników** i wybierz opcję **Zabezpieczenia**.
        2. W polu **Obejmuje/wyklucza zdarzenie o identyfikatorze** wpisz numer zdarzenia i kliknij przycisk **OK**. 

 ![Obraz przedstawiający filtr kwerendy](media/wef 4 query filter.png)

   5.   Kliknij prawym przyciskiem myszy utworzoną subskrypcję i wybierz pozycję **Stan czasu wykonywania**, aby zobaczyć, czy występują problemy dotyczące stanu. 
   6.   Po kilku minutach sprawdź, czy zdarzenia ustawione do przekazania są wyświetlane w zdarzeniach przekazanych w bramie usługi ATA.


Aby uzyskać więcej informacji, zobacz [Konfigurowanie komputerów do przekazywania i zbierania zdarzeń](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Zobacz też
- [Instalowanie usługi ATA](install-ata-step1.md)
- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
