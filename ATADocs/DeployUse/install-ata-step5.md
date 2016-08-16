---
title: "Instalacja usługi ATA — krok 5 | Microsoft ATA"
description: "W kroku 5 procesu instalowania usługi ATA znajdują się informacje ułatwiające skonfigurowanie ustawień bramy usługi ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 3580e748d21db73b6fa8384d84e03b9954b823f8


---

# Instalowanie usługi ATA — Krok 5

>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)


## Krok 5. Konfigurowanie ustawień bramy usługi ATA
Po zainstalowaniu bramy usługi ATA wykonaj następujące kroki, aby skonfigurować ustawienia bramy usługi ATA.

1.  W konsoli usługi ATA kliknij pozycję **Konfiguracja**, a następnie wybierz stronę **Bramy usługi ATA**.

2.  Wprowadź następujące informacje.

  - **Opis**: <br>Wprowadź opis bramy usługi ATA (opcjonalnie).
  - **Kontrolery domeny po dublowaniu portów (FQDN)** (pozycja wymagana w przypadku bramy usługi ATA; nie można jej ustawić w przypadku bramy ATA Lightweight Gateway): <br>Wpisz pełną nazwę FQDN kontrolera domeny, a następnie kliknij znak plus, aby dodać go do listy. Na przykład **dc01.contoso.com**.<br /><br />![Obraz z przykładową nazwą FQDN](media/ATAGWDomainController.png)

Poniższe informacje dotyczą serwerów wprowadzonych na liście **Kontrolery domeny**:

- Wszystkie kontrolery domeny, których ruch jest monitorowany za pośrednictwem funkcji dublowania portów przez bramę usługi ATA, muszą znajdować się na liście **Kontrolery domeny**. Jeśli kontroler domeny nie znajduje się na liście **Kontrolery domeny**, wykrywanie podejrzanych działań może nie funkcjonować zgodnie z oczekiwaniami.
- Co najmniej jeden kontroler domeny znajdujący się na liście musi być serwerem wykazu globalnego. Umożliwi to rozpoznawanie przez usługę ATA obiektów użytkowników i komputerów znajdujących się w innych domenach w lesie.
- **Karty sieciowe przechwytywania** (wymagane):<br>
     - W przypadku bramy usługi ATA na dedykowanym serwerze wybierz karty sieciowe, które są skonfigurowane jako docelowy port dublowania. Będą one odbierać zdublowany ruch kontrolera domeny.
     - W przypadku bramy ATA Lightweight Gateway powinny to być wszystkie karty sieciowe, które są wykorzystywane do komunikacji z innymi komputerami w organizacji.

![Obraz przedstawiający konfigurowanie ustawień bramy](media/ATA-Config-GW-Settings.jpg)

 - **Kandydat synchronizatora domeny**<br>
Wszystkie bramy usługi ATA ustawione jako kandydaci synchronizatora domeny mogą odpowiadać za synchronizację między usługą ATA i domeną usługi Active Directory. W zależności od wielkości domeny początkowa synchronizacja może zająć sporo czasu i dużą część zasobów. Domyślnie tylko bramy usługi ATA są ustawione jako kandydaci synchronizatora domeny. <br>Zaleca się usunięcie ustawienia Kandydat synchronizatora domeny dla wszystkich bram usługi ATA dla lokacji zdalnych.<br>Jeśli kontroler domeny jest kontrolerem tylko do odczytu, nie należy ustawiać go jako kandydata synchronizatora domeny. Aby uzyskać więcej informacji, zobacz [Architektura usługi ATA](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features).

> [!NOTE] 
> Pierwsze uruchomienie bramy usługi ATA potrwa kilka minut. Jest to spowodowane tworzeniem pamięci podręcznej analizatorów przechwytywania ruchu sieciowego.<br>
> Zmiany konfiguracji zostaną zastosowane względem bramy usługi ATA podczas następnej zaplanowanej synchronizacji między bramą usługi ATA a centrum usługi ATA.



    

3. Opcjonalnie możesz ustawić [odbiornik programu Syslog i funkcję zbierania przekazywania zdarzeń systemu Windows](configure-event-collection.md). 
4. Włącz opcję **Aktualizuj bramę usługi ATA automatycznie**, aby w nadchodzących wersjach usługi ta brama usługi ATA była automatycznie aktualizowana, gdy użytkownik zaktualizuje centrum usługi ATA.
3.  Kliknij polecenie **Zapisz**.


## Weryfikowanie instalacji
Aby zweryfikować, czy brama usługi ATA została pomyślnie wdrożona:

1.  Sprawdź, czy jest uruchomiona usługa o nazwie **Microsoft Advanced Threat Analytics Gateway**. Po zapisaniu ustawień bramy usługi ATA może minąć kilka minut, zanim usługa zostanie uruchomiona.

2.  Jeśli usługa nie zostanie uruchomiona, przejrzyj plik „Microsoft.Tri.Gateway-Errors.log” domyślnie znajdujący się w folderze „%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs”.

3.  Sprawdź sekcję [Rozwiązywanie problemów z usługą ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors), aby uzyskać pomoc.

4.  Jeśli jest to pierwsza zainstalowana brama usługi ATA, po kilku minutach zaloguj się do konsoli usługi ATA i otwórz okienko powiadomień, szybko przesuwając od prawej strony ekranu. Na pasku powiadomień po prawej stronie konsoli powinna zostać wyświetlona lista **Ostatnio poznane jednostki**.

5.  Na pulpicie kliknij skrót do usługi **Microsoft Advanced Threat Analytics**, aby nawiązać połączenie z konsolą usługi ATA. Zaloguj się przy użyciu tych samych poświadczeń użytkownika, które zostały użyte do zainstalowania centrum usługi ATA.
6.  W konsoli wyszukaj jakiś element na pasku wyszukiwania, na przykład użytkownika lub grupę w Twojej domenie.
7.  Otwórz Monitor wydajności. W drzewie Wydajność kliknij pozycję **Monitor wydajności**, a następnie kliknij ikonę znaku plus, aby **dodać licznik**. Rozwiń pozycję **Brama usługi Microsoft ATA**, przewiń w dół do pozycji **Liczba komunikatów PEF przechwytywanych przez odbiornik sieci na sekundę** i dodaj ten licznik. Następnie upewnij się, że wykres jest aktywny.

    ![Obraz przedstawiający dodawanie liczników wydajności](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)

## Zobacz też

- [Zapoznaj się z forum usługi ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO4-->


