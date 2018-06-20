---
title: Azure instalacji Advanced Threat Protection — krok 5 | Dokumentacja firmy Microsoft
description: W kroku 5 procesu instalowania Azure ATP ułatwia konfigurowanie ustawień z czujnika autonomiczny Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a2e61758e06aedfe607afc0d3365227af872fe20
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446036"
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-5"></a>Zainstaluj Azure ATP — krok 5

>[!div class="step-by-step"]
[« Krok 4](install-atp-step4.md)
[Krok 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Krok 5. Skonfiguruj ustawienia czujnik Azure ATP
Po zainstalowaniu czujnika Azure ATP, wykonaj następujące kroki, aby skonfigurować ustawienia dla czujnika Azure ATP.

1.  W portalu Azure ATP obszaru roboczego, przejdź do **konfiguracji** i w obszarze **systemu**, wybierz pozycję **czujnik**.
   
     ![Konfigurowanie czujnik ustawienia obrazu](media/atp-sensor-config.png)


2.  Kliknij czujnik, który chcesz skonfigurować, a następnie wprowadź następujące informacje:

    ![Konfigurowanie czujnik ustawienia obrazu](media/atp-sensor-config-2.png)

  - **Opis elementu**: wprowadź opis czujnika Azure ATP (opcjonalnie).
  - **Kontrolery domeny (FQDN)** (wymaga czujnik autonomiczny Azure ATP, nie można zmienić dla czujnika Azure ATP): Wprowadź pełną nazwę FQDN kontrolera domeny, a następnie kliknij znak plus, aby dodać go do listy. Na przykład **dc01.contoso.com**.

      Poniższe informacje dotyczą serwerów wprowadzonych na liście **Kontrolery domeny**:
      - Wszystkie kontrolery domeny, których ruch jest monitorowany za pośrednictwem funkcji dublowania portów przez czujnik autonomiczny Azure ATP musi być wymienione w **kontrolerów domeny** listy. Jeśli kontroler domeny nie znajduje się na liście **Kontrolery domeny**, wykrywanie podejrzanych działań może nie funkcjonować zgodnie z oczekiwaniami.
      - Co najmniej jeden kontroler domeny znajdujący się na liście musi być wykazem globalnym. Dzięki temu ATP Azure rozwiązać obiektów komputerów i użytkowników w innych domenach w lesie.

  - **Karty sieciowe przechwytywania** (wymagane):
     - Czujnik autonomiczny Azure ATP na dedykowanym serwerze wybierz karty sieciowe, które są skonfigurowane jako docelowy port dublowania. One odbierać zdublowany ruch kontrolera domeny.
     - Czujnik Azure ATP powinna to być wszystkie karty sieciowe, które są używane do komunikacji z innymi komputerami w Twojej organizacji.


  - **Kandydat Synchronizatora domeny**: Any Azure ATP autonomiczny czujnik ustawione jako kandydaci Synchronizatora domeny mogą odpowiadać za synchronizację między Azure ATP i domeny usługi Active Directory. W zależności od wielkości domeny początkowa synchronizacja może zająć pewien czas i obciąża. Domyślnie tylko czujników autonomiczny Azure ATP są ustawione jako kandydaci Synchronizatora domeny.
   Zaleca się wyłączenie czujnik Azure ATP dowolnej lokacji zdalnej z Kandydat Synchronizatora domeny.
   Jeśli kontroler domeny jest kontrolerem tylko do odczytu, nie należy ustawiać go jako kandydata synchronizatora domeny. Aby uzyskać więcej informacji, zobacz [architektura Azure ATP](atp-architecture.md#azure-atp-sensor-features).
  
4. Kliknij polecenie **Zapisz**.


## <a name="validate-installations"></a>Weryfikowanie instalacji
Aby sprawdzić, czy czujnik Azure ATP została pomyślnie wdrożona, sprawdź następujące kroki:

1.  Sprawdź, czy usługa o nazwie **czujnik Azure Advanced Threat Protection** jest uruchomiona. Po zapisaniu ustawień czujnik Azure ATP może potrwać kilka sekund dla usługi, aby uruchomić.

2.  Jeśli usługa nie zostanie uruchomiona, przejrzyj plik "Microsoft.Tri.sensor-Errors.log" znajduje się w następującym folderze domyślne "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs".
 
 >[!NOTE]
 > Wersja aktualizacji Azure ATP często, aby sprawdzić najnowszą wersję, w portalu Azure ATP miejsca pracy, przejdź do **konfiguracji** , a następnie **o**. 

3.  Przejdź do adresu URL obszaru roboczego. W portalu obszaru roboczego Wyszukaj jakiś element na pasku wyszukiwania, na przykład użytkownika lub grupy w domenie.



>[!div class="step-by-step"]
[« Krok 4](install-atp-step4.md)
[Krok 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Zobacz też

- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne platformy Azure ATP](atp-prerequisites.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
