---
title: Konfigurowanie przekazywania zdarzeń systemu Windows w usłudze Advanced Threat Analytics | Microsoft Docs
description: Opisuje opcje konfigurowania przekazywania zdarzeń w systemie Windows za pomocą usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 512e7fa979a6fd5e140d65836b533b720a6dc03b
ms.sourcegitcommit: 1b23381ca4551a902f6343428d98f44480077d30
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2018
ms.locfileid: "47403220"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="configuring-windows-event-forwarding"></a>Konfigurowanie funkcji przekazywania zdarzeń systemu Windows

> [!NOTE]
> W przypadku usługi ATA w wersji 1.8 i nowszych nie trzeba już konfigurować zbierania zdarzeń dla uproszczonych bram usługi ATA. Uproszczona brama usługi ATA teraz odczytywać zdarzenia lokalnie — bez konieczności konfigurowania przekazywania zdarzeń.

W celu zwiększenia możliwości wykrywania usługa ATA potrzebuje następujących zdarzeń Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045. One może odczytywać je automatycznie przez bramę ATA Lightweight Gateway lub w przypadku uproszczonej bramy usługi ATA nie została wdrożona, zdarzenia mogą być przekazywane do bramy usługi ATA na jeden z dwóch sposobów, przez skonfigurowanie bramy usługi ATA do nasłuchiwania zdarzeń SIEM lub przez skonfigurowanie zdarzeń Windows Przekazywanie.

> [!NOTE]
> Jeśli używasz Server Core [wecutil](https://docs.microsoft.com/windows-server/administration/windows-commands/wecutil) może służyć do tworzenia i zarządzania subskrypcjami zdarzeń, które są przekazywane z komputerów zdalnych.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Konfiguracja funkcji przekazywania zdarzeń (WEF) bramy usługi ATA z dublowaniem portów

Po skonfigurowaniu funkcji dublowania portów z kontrolerów domeny do bramy usługi ATA, wykonaj następujące instrukcje konfigurowania przekazywania zdarzeń Windows za pomocą konfiguracji inicjowanej przez obiekt źródłowy. Jest to jeden ze sposobów konfigurowania przekazywania zdarzeń systemu Windows. 

**Krok 1: Dodaj konto usługi sieciowej do grupy Czytelnicy dzienników zdarzeń domeny** 

W tym scenariuszu założono, że brama usługi ATA jest elementem członkowskim domeny.

1.  Otwórz narzędzie Użytkownicy usługi Active Directory i komputerów, przejdź do **BuiltIn** folder i kliknij dwukrotnie plik **Czytelnicy dzienników zdarzeń**. 
2.  Wybierz **członków**.
3.  Jeśli pozycji **Usługa sieciowa** nie ma na liście, kliknij przycisk **Dodaj** i wpisz **Usługa sieciowa** w polu **Wprowadź nazwy obiektów do wybrania**. Następnie kliknij opcję **Sprawdź nazwy** i kliknij dwukrotnie przycisk **OK**. 

Po dodaniu **Usługa sieciowa** do **Czytelnicy dzienników zdarzeń** grupie, przeprowadź ponowny rozruch kontrolerów domeny, aby zmiana zaczęła obowiązywać.

**Krok 2: Utwórz zasady na kontrolerach domeny, aby skonfigurować ustawienie Konfiguruj docelowego Menedżera subskrypcji** 
> [!Note] 
> Można tworzyć dla tych ustawień zasady grupy i stosować zasady grupy do każdego kontrolera domeny monitorowanego przez bramę usługi ATA. Poniższe kroki umożliwiają modyfikację zasad lokalnych kontrolera domeny.     

1.  Uruchom następujące polecenie na każdym kontrolerze domeny: *winrm quickconfig*
2.  W wierszu polecenia wpisz ciąg *gpedit.msc*.
3.  Rozwiń węzeł **Konfiguracja komputera > Szablony administracyjne > Składniki systemu Windows > Przesyłanie dalej zdarzeń**

![Obraz edytora lokalnych zasad grupy](media/wef%201%20local%20group%20policy%20editor.png)

4.  Kliknij dwukrotnie **Konfiguruj docelowego Menedżera subskrypcji**.
   
    1.  Wybierz opcję **Włączono**.
    2.  W obszarze **opcje**, kliknij przycisk **Pokaż**.
    3.  W obszarze **menedżerowie subskrypcji**, wprowadź następujące wartości i kliknij przycisk **OK**: *Server = http: / /<fqdnATAGateway>: 5985/wsman/SubscriptionManager/WEC, Refresh = 10* 
    
        *(Na przykład: Server = http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC, Odśwież = 10)*
 
    ![Obraz konfigurowania subskrypcji docelowej](media/wef%202%20config%20target%20sub%20manager.png)
   
    5.  Kliknij przycisk **OK**.
    6.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *gpupdate /force*. 

**Krok 3: W odniesieniu do bramy usługi ATA wykonaj następujące kroki** 

1.  Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i wpisz *wecutil qc*
2.  Otwórz **Podgląd zdarzeń**. 
3.  Kliknij prawym przyciskiem myszy **subskrypcje** i wybierz **Utwórz subskrypcję**. 

    1.  Wprowadź nazwę i opis subskrypcji. 
    2.  Aby uzyskać **Dziennik docelowy**, upewnij się, że **zdarzenia przesyłane dalej** jest zaznaczone. Aby usługa ATA mogła odczytywać zdarzenia, dla dziennika docelowego musi być wybrana opcja **Zdarzenia przesyłane dalej**. 
    3.  Wybierz opcję **Zainicjowane przez komputer źródłowy** i kliknij przycisk **Wybierz grupy komputerów**.
        1.  Kliknij przycisk **Dodaj komputer w domenie**.
        2.  Wprowadź nazwę kontrolera domeny w polu **Wprowadź nazwę obiektu do wybrania**. Kliknij opcję **Sprawdź nazwy** i kliknij przycisk **OK**.  
          ![Obraz podglądu zdarzeń](media/wef3%20event%20viewer.png)  
        3.  Kliknij przycisk **OK**.
     4. Kliknij przycisk **Wybierz zdarzenia**.

        1. Kliknij przycisk **Według dzienników** i wybierz opcję **Zabezpieczenia**.
        2. W polu **Obejmuje/wyklucza zdarzenie o identyfikatorze** wpisz numer zdarzenia i kliknij przycisk **OK**. Na przykład wpisz 4776, podobnie jak w następującym przykładzie.

        ![Obraz przedstawiający filtr kwerendy](media/wef%204%20query%20filter.png)

    5.  Kliknij prawym przyciskiem myszy utworzoną subskrypcję i wybierz **stan czasu wykonywania** aby zobaczyć, jeśli występują problemy ze stanem. 
    6.  Po kilku minutach sprawdź, czy zdarzenia ustawione do przekazania są wyświetlane w zdarzeniach przekazanych w bramie usługi ATA.


Aby uzyskać więcej informacji, zobacz: [Konfigurowanie komputerów do przekazywania i zbierania zdarzeń](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Zobacz też
- [Instalowanie usługi ATA](install-ata-step1.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
