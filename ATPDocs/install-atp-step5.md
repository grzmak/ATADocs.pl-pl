---
title: Zainstaluj usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: W kroku 5 procesu instalowania usługi Azure ATP służy do konfigurowania ustawień dla usługi Azure ATP czujnik autonomiczny.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6f65b3af56e683a385f7128a989170c8c4073b3e
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783869"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="install-azure-atp---step-5"></a>Zainstaluj narzędzie Azure ATP — krok 5

> [!div class="step-by-step"]
> [«Krok 4](install-atp-step4.md)



## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Krok 5. Konfigurowanie ustawień czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure
Po zainstalowaniu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, wykonaj następujące kroki, aby skonfigurować ustawienia czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.

1.  W portalu usługi Azure ATP, przejdź do **konfiguracji** i w obszarze **systemu**, wybierz opcję **czujnika**.
   
     ![Skonfiguruj obraz ustawień czujnika](media/atp-sensor-config.png)


2.  Kliknij czujnik, który chcesz skonfigurować, a następnie wprowadź następujące informacje:

    ![Skonfiguruj obraz ustawień czujnika](media/atp-sensor-config-2.png)

  - **Opis**: wprowadź opis (opcjonalnie) czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.
  - **Kontrolery domeny (FQDN)** (wymagane dla usługi Azure ATP czujnik autonomiczny, to nie można zmienić dla czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure): Wprowadź pełną nazwę FQDN kontrolera domeny, a następnie kliknij znak plus, aby dodać go do listy. Na przykład **dc01.contoso.com**.

      Poniższe informacje dotyczą serwerów wprowadzonych na liście **Kontrolery domeny**:
      - Wszystkie kontrolery domeny, w których ruch jest monitorowany za pośrednictwem funkcji dublowania portów za pomocą narzędzia Azure ATP czujnika autonomicznego musi być wymienione w **kontrolery domeny** listy. Jeśli kontroler domeny nie znajduje się na liście **Kontrolery domeny**, wykrywanie podejrzanych działań może nie funkcjonować zgodnie z oczekiwaniami.
      - Co najmniej jeden kontroler domeny znajdujący się na liście musi być wykazem globalnym. Dzięki temu usługi Azure ATP można rozpoznać obiektów użytkowników i komputerów w innych domenach w lesie.

  - **Karty sieciowe przechwytywania** (wymagane):
   
     - Dla czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure powinna to być wszystkie karty sieciowe, które są używane do komunikacji z innymi komputerami w Twojej organizacji.
    - Dla czujnik autonomiczny narzędzia Azure ATP na dedykowanym serwerze wybierz karty sieciowe, które są skonfigurowane jako docelowy port dublowania. One odbierać zdublowany ruch kontrolera domeny.

    - **Kandydat Synchronizatora domeny**: domyślnie czujników narzędzia Azure ATP nie są kandydatami Synchronizatora domeny, są czujników autonomiczne narzędzia Azure ATP. Aby ręcznie wybrać czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure jako kandydat syncronizer domeny, przełącz się **kandydat Synchronizatora domeny** Przełącz opcję **ON** na ekranie konfiguracji. 
    
        Synchronizator domeny jest odpowiedzialny za synchronizację między usługą Azure ATP i domeny usługi Active Directory. W zależności od wielkości domeny początkowa synchronizacja może zająć trochę czasu i jest dużej ilości zasobów. 
   Zaleca się wyłączenie usługi Azure ATP czujnik(-i) miałyby kandydatami Synchronizatora domeny dla lokacji zdalnych.
   Jeśli kontroler domeny jest tylko do odczytu, nie należy ustawiać go jako kandydata Synchronizatora domeny. Aby uzyskać więcej informacji na temat synchronizacji domeny usługi Azure ATP zobacz [architektury usługi Azure ATP](atp-architecture.md#azure-atp-sensor-features)
  
4. Kliknij polecenie **Zapisz**.


## <a name="validate-installations"></a>Weryfikowanie instalacji
Aby sprawdzić, czy czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure został wdrożony pomyślnie, sprawdź następujące kroki:

1.  Upewnij się, że usługa o nazwie **czujnika zaawansowanej ochrony przed zagrożeniami dla platformy Azure** jest uruchomiona. Po zapisaniu ustawień czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure może potrwać kilka sekund dla usługi, aby rozpocząć.

2.  Jeśli usługa nie zostanie uruchomiona, przejrzyj plik "Microsoft.Tri.sensor-Errors.log" znajdujący się w następującym folderze domyślną "%programfiles%\Azure Zaawansowana ochrona przed zagrożeniami sensor\Version X\Logs".
 
 >[!NOTE]
 > Wersja aktualizacji usługi Azure ATP często, aby sprawdzić najnowszą wersję, w portalu usługi Azure ATP, przejdź do **konfiguracji** i następnie **o**. 

3.  Przejdź do adresu URL obszaru roboczego. W portalu usługi Azure ATP wyszukiwania dowolnego tekstu w pasku wyszukiwania, takie jak użytkownika lub grupy w domenie.



> [!div class="step-by-step"]
> [«Krok 4](install-atp-step4.md)



## <a name="see-also"></a>Zobacz też

- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
