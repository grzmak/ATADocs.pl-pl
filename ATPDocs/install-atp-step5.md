---
title: Install Azure Zaawansowana ochrona przed zagrożeniami — krok 5 | Dokumentacja firmy Microsoft
description: W kroku 5 procesu instalowania usługi Azure ATP służy do konfigurowania ustawień dla usługi Azure ATP czujnik autonomiczny.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 03aa84b4288e4155b579acc12f03b7ecdb55b160
ms.sourcegitcommit: 8e80f59409c65e7d8d60ec7de8b96b621795699a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2018
ms.locfileid: "47168607"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="install-azure-atp---step-5"></a>Zainstaluj narzędzie Azure ATP — krok 5

>[!div class="step-by-step"]
[« Krok 4](install-atp-step4.md)
[Krok 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Krok 5. Konfigurowanie ustawień czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure
Po zainstalowaniu czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, wykonaj następujące kroki, aby skonfigurować ustawienia czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure.

1.  W portalu obszaru roboczego usługi Azure ATP, przejdź do **konfiguracji** i w obszarze **systemu**, wybierz opcję **czujnika**.
   
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
   Jeśli kontroler domeny jest kontrolerem tylko do odczytu, nie należy ustawiać go jako kandydata synchronizatora domeny. Aby uzyskać więcej informacji na temat synchronizacji domeny usługi Azure ATP zobacz [architektury usługi Azure ATP](atp-architecture.md#azure-atp-sensor-features)
  
4. Kliknij polecenie **Zapisz**.


## <a name="validate-installations"></a>Weryfikowanie instalacji
Aby sprawdzić, czy czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure został wdrożony pomyślnie, sprawdź następujące kroki:

1.  Upewnij się, że usługa o nazwie **czujnika zaawansowanej ochrony przed zagrożeniami dla platformy Azure** jest uruchomiona. Po zapisaniu ustawień czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure może potrwać kilka sekund dla usługi, aby rozpocząć.

2.  Jeśli usługa nie zostanie uruchomiona, przejrzyj plik "Microsoft.Tri.sensor-Errors.log" znajdujący się w następującym folderze domyślną "%programfiles%\Azure Zaawansowana ochrona przed zagrożeniami sensor\Version X\Logs".
 
 >[!NOTE]
 > Wersja aktualizacji usługi Azure ATP często, aby sprawdzić najnowszą wersję, w portalu usługi Azure ATP miejsca pracy, przejdź do **konfiguracji** i następnie **o**. 

3.  Przejdź do adresu URL obszaru roboczego. W portalu w obszarze roboczym Wyszukaj jakiś element na pasku wyszukiwania, takie jak użytkownika lub grupy w domenie.



>[!div class="step-by-step"]
[« Krok 4](install-atp-step4.md)
[Krok 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Zobacz też

- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
