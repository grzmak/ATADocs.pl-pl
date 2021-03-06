---
title: Co nowego w wersji 1.6 usługi Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: Zawiera listę nowych funkcji oraz znanych problemów w wersji 1.6 usługi ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 27b139e5-12b9-4953-8f53-eb58e8ce0038
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5fd3b7a0abb3c70e87634e28273fe5ce8b6d4d9a
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133620"
---
# <a name="whats-new-in-ata-version-16"></a>Co nowego w wersji 1.6 usługi ATA
Te informacje o wersji zawierają znane problemy w tej wersji usługi Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-16-update"></a>Co nowego w aktualizacji usługi ATA do wersji 1.6?
Aktualizacja usługi ATA do wersji 1.6 zapewnia następujące ulepszenia:

-   Wykrywanie nowych zagrożeń

-   Ulepszenia istniejącego wykrywania

-   Brama ATA Lightweight Gateway

-   Aktualizacje automatyczne

-   Poprawiona wydajność centrum usługi ATA

-   Niższe wymagania dotyczące magazynu

-   Obsługa IBM QRadar

### <a name="new-detections"></a>Wykrywanie nowych zagrożeń


- **Złośliwe żądanie informacji prywatnych z zakresu ochrony danych** Interfejs API ochrony danych (DPAPI) to usługa ochrony danych oparta na hasłach. Ta usługa ochrony jest używana przez różne aplikacje, które przechowują Twoje tajemnice, takie jak hasła witryn sieci Web i poświadczenia udziałów plików. W celu obsługi scenariuszy utraty hasła, użytkownicy mogą odszyfrowywać chronione dane przy użyciu klucza odzyskiwania, który nie zawiera ich hasła. W środowisku domeny osoby atakujące mogą zdalnie wykraść klucz odzyskiwania i użyć go do odszyfrowywania chronionych danych na wszystkich komputerach przyłączonych do domeny.


- **Wyliczenie sesji sieciowej** Rekonesans to kluczowy etap w łańcuchu kończenia ataku zaawansowanego. Kontrolery domeny (DC) działają jako serwery plików na potrzeby dystrybucji obiektów zasad grupy za pomocą protokołu bloku komunikatów serwera (SMB). Częścią fazy rekonesansu osoby atakujące mogą wysyłać zapytania kontrolera domeny dla wszystkich aktywnych sesji protokołu SMB na serwerze. Zezwalaj na uzyskanie dostępu do wszystkich użytkowników i adresów IP skojarzonych z tymi sesjami protokołu SMB. Wyliczenie sesji SMB może posłużyć osobom atakującym do atakowania kont poufnych, ułatwiając im penetrację całej sieci.


- **Złośliwe żądania replikacji** W środowiskach usługi Active Directory replikacja między kontrolerami domeny odbywa się regularnie. Osoba atakująca może spreparować żądanie replikacji usługi Active Directory (czasami podszywając się pod kontroler domeny). To fałszywe umożliwia osobie atakującej na danych przechowywanych w usłudze Active Directory, w tym skrótów haseł, bez konieczności zastosowania bardziej natrętnych technik, takich jak kopiowanie woluminów w tle.


- **Wykrywanie luk w zabezpieczeniach MS11-013**  
Brak podniesienie uprawnień w protokole Kerberos, który umożliwia do sfałszowanie niektórych aspektów biletu usługi Kerberos. Złośliwy użytkownik lub osoba atakująca, która z sukcesem wykorzystuje tę lukę w zabezpieczeniach, może uzyskać token z podwyższonym poziomem uprawnień na kontrolerze domeny.


- **Implementacja nietypowego protokołu** Żądania uwierzytelniania (Kerberos lub NTLM) zazwyczaj są realizowane przy użyciu standardowego zestawu metod i protokołów. Jednak w celu pomyślnego uwierzytelnienia żądanie musi spełniać jedynie określony zestaw wymagań. Osoby atakujące mogą zaimplementować te protokoły z drobnymi odchyleniami od standardowego wdrożenia w danym środowisku. Tego rodzaju odchylenia mogą wskazywać na obecność osoba atakująca próbuje przeprowadzić ataki, takie jak Pass--Hash, atak Siłowy i inne.


### <a name="improvements-to-existing-detections"></a>Ulepszenia istniejącego wykrywania
Usługa ATA 1.6 zawiera ulepszoną logikę wykrywania redukuje scenariuszy fałszywie dodatnimi lub fałszywie ujemnymi wynikami wykrywania, takie jak bilet uwierzytelniania Golden Ticket, wystawione jako przynęta, atak Siłowy i zdalne wykonywanie kodu.

### <a name="the-ata-lightweight-gateway"></a>Brama ATA Lightweight Gateway
W tej wersji usługi ATA wprowadzono nową opcję wdrażania bramy usługi ATA, która umożliwia instalowanie bramy ATA bezpośrednio na kontrolerze domeny. W tej opcji wdrażania usunięto niekrytyczne funkcje bramy usługi ATA i wprowadzono dynamiczne zarządzanie zasobami w oparciu o dostępne zasoby na kontrolerze domeny, co nie ma żadnego wpływu na istniejące operacje kontrolera domeny. Brama ATA Lightweight Gateway pozwala zmniejszyć koszt wdrożenia usługi ATA. W tym samym czasie ułatwia wdrażanie w lokacjach oddziałów, w których istnieje pojemność zasobów ograniczenia sprzętowe lub brakiem, aby ustawić Konfigurowanie funkcji dublowania portów pomocy technicznej.
Aby uzyskać więcej informacji na temat bramy ATA Lightweight Gateway, zobacz [Architektura usługi ATA](ata-architecture.md#ata-gateway-and-ata-lightweight-gateway)

Aby uzyskać więcej informacji na temat zagadnień dotyczących wdrażania i wybierania właściwego typu bram, zobacz [Planowanie pojemności usługi ATA](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment)


### <a name="automatic-updates"></a>Aktualizacje automatyczne
Począwszy od wersji 1.6, centrum usługi ATA można aktualizować za pomocą usługi Microsoft Update. Ponadto bramy usługi ATA mogą być teraz automatycznie aktualizowane przy użyciu ich standardowego kanału komunikacyjnego z centrum usługi ATA.
### <a name="improved-ata-center-performance"></a>Poprawiona wydajność centrum usługi ATA
Mniejsze obciążenie bazy danych i wydajniejszy sposób wykrywania w tej wersji umożliwiają monitorowanie znacznie większej liczby kontrolerów domeny za pomocą pojedynczego centrum usługi ATA.

### <a name="lower-storage-requirements"></a>Niższe wymagania dotyczące magazynu
Usługa ATA 1.6 wymaga znacznie mniej miejsca w magazynie do uruchomienia bazy danych usługi ATA — teraz zaledwie 20% miejsca używanego w poprzednich wersjach.

### <a name="support-for-ibm-qradar"></a>Obsługa IBM QRadar
Usługa ATA umożliwia obecnie odbieranie zdarzeń z rozwiązania QRadar SIEM firmy IBM, oprócz obsługiwanych wcześniej rozwiązań SIEM.

## <a name="known-issues"></a>Znane problemy
W tej wersji występują następujące znane problemy.

### <a name="failure-to-recognize-new-path-in-manually-moved-databases"></a>Nie można rozpoznać nowej ścieżki w ręcznie przeniesionych bazach danych

W przypadku wdrożeń, w których ścieżka bazy danych została przeniesiona ręcznie, wdrożenie usługi ATA nie używa nowej ścieżki bazy danych do aktualizacji. Przeniesiona ręcznie czy ścieżki bazy danych może spowodować następujące problemy:


- Bez cyklicznego usuwania starych działań sieciowych usługa ATA może zużyć całe wolne miejsce na dysku systemowym centrum usługi ATA.


- Proces aktualizowania usługi ATA do wersji 1.6 może zakończyć się niepowodzeniem na etapie sprawdzania gotowości przed aktualizacją, jak pokazano na poniższej ilustracji.
    ![Sprawdzanie gotowości zakończone niepowodzeniem](media/ata_failed_readinesschecks.png)
    
    > [!IMPORTANT]
    > Przed zaktualizowaniem usługi ATA do wersji 1.6, zaktualizuj następujący klucz rejestru prawidłową ścieżką bazy danych: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`
    
### <a name="migration-failure-when-updating-from-ata-15"></a>Błąd migracji podczas aktualizowania usługi ATA z wersji 1.5
Podczas aktualizowania usługi ATA do wersji 1.6 proces aktualizacji może zakończyć się niepowodzeniem z powodu błędu o następującym kodzie:

![Błąd aktualizowania usługi ATA do wersji 1.6](http://i.imgur.com/QrLSApr.png) Jeśli zostanie wyświetlony ten błąd, przejrzyj dziennik wdrażania w folderze: **C:\Users\<Użytkownik>\AppData\Local\Temp**, szukając następującego wyjątku:

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

Może również zostać wyświetlony ten błąd: System.ArgumentNullException: Wartość nie może być pusta.
    
Jeśli zostanie wyświetlony jeden z tych błędów, należy uruchomić następującego obejścia:

**Obejście**: 

1.  Przenieś folder „data_old” do folderu tymczasowego (zazwyczaj znajdującego się w folderze %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin).
2.  Odinstaluj centrum usługi ATA w wersji 1.5 i usuń wszystkie dane z bazy danych.
![Odinstalowywanie usługi ATA w wersji 1.5](http://i.imgur.com/x4nJycx.png)
3.  Zainstaluj ponownie Centrum usługi ATA w wersji 1.5. Upewnij się, że używasz takiej samej konfiguracji jak w poprzedniej instalacji usługi ATA w wersji 1.5 (certyfikaty, adresy IP, ścieżka bazy danych itp.).
4.  Zatrzymaj poniższe usługi w następującej kolejności:
    1.  Microsoft Advanced Threat Analytics Center
    2.  MongoDB
5.  Zastąp pliki bazy danych MongoDB plikami z folderu „data_old”.
6.  Uruchom poniższe usługi w następującej kolejności:
    1.  Baza danych MongoDB
    2.  Microsoft Advanced Threat Analytics Center
7.  Przejrzyj dzienniki, aby sprawdzić, czy produkt działa bez błędów.
8.  [Pobierz](http://aka.ms/ataremoveduplicateprofiles "Pobierz") narzędzie „RemoveDuplicateProfiles.exe” i skopiuj je do głównej ścieżki instalacji (%ProgramFiles%\Microsoft Advanced Threat Analytics\Center).
9.  W wierszu polecenia z podwyższonym poziomem uprawnień uruchom `RemoveDuplicateProfiles.exe` i zaczekaj, aż zostanie pomyślnie zakończona.
10. W tym miejscu: …\Microsoft Advanced Threat Analytics\Center\MongoDB\bin katalog: **Mongo ATA** wpisz następujące polecenie:

          db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![Obejście aktualizacji](http://i.imgur.com/Nj99X2f.png)

Powinny zostać zwrócone `WriteResult({ "nRemoved" : XX })` gdzie "XX" oznacza liczbę podejrzanych działań, które zostały usunięte. Jeśli liczba jest większa niż 0, zamknij wiersz polecenia i kontynuuj proces aktualizacji.


### <a name="net-framework-461-requires-restarting-the-server"></a>Platforma .Net Framework 4.6.1 wymaga ponownego uruchomienia serwera

![Ponowne uruchomienie platformy .Net Framework](media/ata-net-framework-restart.png)

### <a name="historical-network-activities-no-longer-migrated"></a>Historyczne działania sieciowe nie są już poddawane migracji
W tej wersji usługi ATA znajduje się ulepszony aparat wykrywania, który zapewnia bardziej precyzyjne wykrywanie i zmniejsza liczbę fałszywie dodatnich scenariuszy, szczególnie w przypadku ataków typu Pass-the-Hash.
Nowy, ulepszony aparat wykrywania korzysta z wbudowanej technologii wykrywania, która umożliwia wykrywanie bez uzyskiwania dostępu do historycznych działań sieciowych, można znacznie zwiększyć wydajność Centrum usługi ATA. Oznacza to, że jest nie trzeba migrować historycznych działań sieciowych podczas wykonywania procedury aktualizacji.
Procedura aktualizacji usługi ATA eksportuje dane (na wypadek, gdyby były potrzebne do badań w przyszłości) do folderu `<Center Installation Path>\Migration` w formacie JSON.

## <a name="see-also"></a>Zobacz też
[Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizacja usługi ATA do wersji 1.6 — przewodnik migracji](ata-update-1.6-migration-guide.md)
