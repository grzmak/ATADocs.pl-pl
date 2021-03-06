---
title: Instalowanie usługi Advanced Threat Analytics — Krok 5 | Dokumentacja firmy Microsoft
description: W kroku 5 procesu instalowania usługi ATA znajdują się informacje ułatwiające skonfigurowanie ustawień bramy usługi ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f43503bb64ab79280782c1fc81a4821a8b905ff7
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454058"
---
*Dotyczy: Advanced Threat Analytics w wersji 1.9*



# <a name="install-ata---step-5"></a>Instalowanie usługi ATA — Krok 5

> [!div class="step-by-step"]
> [« Krok 4](install-ata-step4.md)
> [Krok 6 »](install-ata-step6.md)


## <a name="step-5-configure-the-ata-gateway-settings"></a>Krok 5. Konfigurowanie ustawień bramy usługi ATA
Po zainstalowaniu bramy usługi ATA wykonaj następujące kroki, aby skonfigurować ustawienia bramy usługi ATA.

1.  W konsoli ATA przejdź do węzła **Konfiguracja** i w obszarze **System** wybierz pozycję **Bramy**.
   
     ![Obraz przedstawiający konfigurowanie ustawień bramy](media/ata-gw-config-1.png)


2.  Kliknij bramę, którą chcesz skonfigurować, i podaj następujące informacje:

    ![Obraz przedstawiający konfigurowanie ustawień bramy](media/ATA-Gateways-config-2.png)

  - **Opis**: wprowadź opis bramy usługi ATA (opcjonalnie).
  - **Port Mirrored Domain Controllers (FQDN)** (Kontrolery domeny z dublowaniem portów (FQDN))(wymagane dla bramy usługi ATA, nie można zmienić dla uproszczonej bramy usługi ATA): należy wprowadzić pełną nazwę FQDN kontrolera domeny, a następnie kliknąć znak plus, aby dodać go do listy. Na przykład **dc01.contoso.com**.

    Poniższe informacje dotyczą serwerów wprowadzonych na liście **Kontrolery domeny**:
    - Wszystkie kontrolery domeny, których ruch jest monitorowany za pośrednictwem funkcji dublowania portów przez bramę usługi ATA, muszą znajdować się na liście **Kontrolery domeny**. Jeśli kontroler domeny nie znajduje się na liście **Kontrolery domeny**, wykrywanie podejrzanych działań może nie funkcjonować zgodnie z oczekiwaniami.
    - Co najmniej jeden kontroler domeny znajdujący się na liście musi być wykazem globalnym. Dzięki temu usługa ATA może rozpoznać obiektów użytkowników i komputerów w innych domenach w lesie.

  - **Karty sieciowe przechwytywania** (wymagane):
  - W przypadku bramy usługi ATA na dedykowanym serwerze wybierz karty sieciowe, które są skonfigurowane jako docelowy port dublowania. Będą one odbierać zdublowany ruch kontrolera domeny.
  - W przypadku uproszczonej bramy usługi ATA powinny to być wszystkie karty sieciowe, które są wykorzystywane do komunikacji z innymi komputerami w organizacji.
  
  - **Domain synchronizer candidate** (Kandydat na synchronizatora domeny): dowolna brama usługi ATA ustawiona jako kandydat na synchronizatora domeny może odpowiadać za synchronizację między usługą ATA a domeną Active Directory. W zależności od wielkości domeny początkowa synchronizacja może zająć trochę czasu i wymagać dużej ilości zasobów. Domyślnie wszystkie bramy usługi ATA są kandydatami na synchronizatora.
   Zaleca się wyłączenie bram usługi ATA dla lokacji zdalnych z listy kandydatów na synchronizatora domeny.
   Jeśli kontroler domeny jest kontrolerem tylko do odczytu, nie należy ustawiać go jako kandydata synchronizatora domeny. Aby uzyskać więcej informacji, zobacz [Architektura usługi ATA](ata-architecture.md#ata-lightweight-gateway-features).

  > [!NOTE] 
  > Pierwsze uruchomienie bramy usługi ATA po instalacji potrwa kilka minut. Jest to spowodowane tworzeniem pamięci podręcznej analizatorów przechwytywania ruchu sieciowego.
  > Zmiany konfiguracji są stosowane do bramy usługi ATA podczas następnej zaplanowanej synchronizacji między bramą usługi ATA a Centrum usługi ATA.

3. Opcjonalnie możesz ustawić [odbiornik programu Syslog i funkcję zbierania przekazywania zdarzeń systemu Windows](configure-event-collection.md). 
4. Włącz opcję **Aktualizuj bramę usługi ATA automatycznie** , aby po zaktualizowaniu Centrum usługi ATA do następnych wersji ta brama usługi ATA była również automatycznie aktualizowana.

5. Kliknij polecenie **Zapisz**.


## <a name="validate-installations"></a>Weryfikowanie instalacji
Aby sprawdzić, czy brama usługi ATA została wdrożona pomyślnie, wykonaj następujące kroki:

1.  Sprawdź, czy jest uruchomiona usługa o nazwie **Microsoft Advanced Threat Analytics Gateway**. Po zapisaniu ustawień bramy usługi ATA może minąć kilka minut, zanim usługa zostanie uruchomiona.

2.  Jeśli usługa nie zostanie uruchomiona, przejrzyj plik „Microsoft.Tri.Gateway-Errors.log” domyślnie znajdujący się w folderze „%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs” i zapoznaj się z artykułem [Rozwiązywanie problemów z usługą ATA](troubleshooting-ata-known-errors.md), aby uzyskać pomoc.

3.  Jeśli jest to pierwsza zainstalowana brama usługi ATA, po kilku minutach zaloguj się do konsoli usługi ATA i otwórz okienko powiadomień, szybko przesuwając od prawej strony ekranu. Na pasku powiadomień po prawej stronie konsoli powinna zostać wyświetlona lista **Ostatnio poznane jednostki**.

4.  Na pulpicie kliknij skrót do usługi **Microsoft Advanced Threat Analytics**, aby nawiązać połączenie z konsolą usługi ATA. Zaloguj się przy użyciu tych samych poświadczeń użytkownika, które zostały użyte do zainstalowania centrum usługi ATA.
5.  W konsoli wyszukaj jakiś element na pasku wyszukiwania, na przykład użytkownika lub grupę w Twojej domenie.
6.  Otwórz Monitor wydajności. W drzewie Wydajność kliknij pozycję **Monitor wydajności**, a następnie kliknij ikonę znaku plus, aby **dodać licznik**. Rozwiń pozycję **Brama usługi Microsoft ATA**, przewiń w dół do pozycji **Liczba komunikatów PEF przechwytywanych przez odbiornik sieci na sekundę** i dodaj ten licznik. Następnie upewnij się, że wykres jest aktywny.

    ![Obraz przedstawiający dodawanie liczników wydajności](media/ATA-performance-monitoring-add-counters.png)


> [!div class="step-by-step"]
> [« Krok 4](install-ata-step4.md)
> [Krok 6 »](install-ata-step6.md)



## <a name="related-videos"></a>Pokrewne wideo
- [Omówienie wdrożenia usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Wybieranie odpowiedniego typu bramy usługi ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Zobacz też
- [Przewodnik wdrażania weryfikacji Koncepcji usługi ATA](http://aka.ms/atapoc)
- [Narzędzia do określania rozmiaru usługi ATA](http://aka.ms/atasizingtool)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)

