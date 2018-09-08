---
title: Jak badać użytkownicy i komputery za pomocą narzędzia Azure ATP | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu badania podejrzanych działań wykonywanych przez użytkowników, jednostki, komputery lub urządzenia przy użyciu usługi Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/6/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0c0558dbe0b4eba849adb635a84bc934e406e56f
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166565"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="investigate-an-entity-with-azure-atp"></a>Badanie jednostki za pomocą narzędzia Azure ATP

W tym artykule opisano proces badania jednostki po wykryciu podejrzanych działań za pomocą usługi Azure Advanced Threat Protection (ATP). Po obejrzeniu podejrzanych działań na osi czasu, możesz przejść do szczegółów do jednostki, które są zaangażowani w działanie i użyj następujących parametrów i szczegółowe informacje, aby dowiedzieć się więcej na temat co się stało i co należy zrobić, aby zmniejszyć zagrożenie.

## <a name="look-at-the-entity-profile"></a>Przyjrzyj się profilu jednostki

Profilu jednostki zawiera ze stroną kompleksowej jednostki przeznaczone do badania szczegółowym omówieniu użytkowników, komputerów, urządzeń i zasobów, do których mają dostęp wraz z ich historii. Strona profilu korzysta z nowych translator aktywności logicznego usługi Azure ATP, można przyjrzeć się grupę działań, które pojawiają się (zagregowane maksymalnie minutę) i zgrupować je w jedno działanie logicznych daje lepsze zrozumienie działania rzeczywistych Użytkownicy.

Aby uzyskać dostęp do strony profilu jednostki, kliknij nazwę jednostki, takie jak nazwa użytkownika, na osi czasu podejrzanych działań. Widać również minimalnej wersji na stronie podejrzanych działań profilu jednostki, ustawiając kursor nad nazwa jednostki.

Profilu jednostki pozwala wyświetlić jednostki działania, wyświetlić danych katalogowych oraz ścieżki ruchu poprzecznego dla jednostki. Aby uzyskać więcej informacji, zobacz [Opis profilów jednostki ](entity-profiles.md).

## <a name="check-entity-tags"></a>Wybierz tagi jednostki

Narzędzie Azure ATP ściąga tagi z usługi Active Directory, aby zapewnić pojedynczy interfejs do monitorowania usługi Active Directory, użytkowników i jednostek. Tagi te udostępniają informacje o tej jednostce z usługi Active Directory, w tym:
- Częściowa: Użytkownika, komputera lub grupy nie jest zsynchronizowane z domeny, a częściowo został rozwiązany za pomocą wykazu globalnego. Niektóre atrybuty nie są dostępne.
- Nierozpoznane: Ten komputer nie została rozpoznana na prawidłową jednostkę w lesie usługi active directory. Brak informacji o katalogu jest dostępna.
- Usunięto: Jednostka została usunięta z usługi Active Directory.
- Wyłączone: Jednostka jest wyłączona w usłudze Active Directory.
- Zablokowane: Jednostka wprowadziła niepoprawne hasło zbyt wiele razy i jest zablokowany.
- Ważność: Jednostka wygasła w usłudze Active Directory.
- Nowość: Jednostka została utworzona mniej niż 30 dni temu.

## <a name="look-at-the-user-account-control-flags"></a>Przyjrzyj się flagi kontroli konta użytkownika

Flagi kontroli konta użytkownika, również są importowane z usługi Active Directory. Danych jednostki w usłudze Azure ATP obejmuje 10 flagi, które zostaną zastosowane na badania: 
- Hasło nigdy nie wygasa
- Zaufany do delegowania
- Wymagana karta inteligentna
- Hasło wygasło
- Puste hasło jest dozwolone
- Przechowywanie hasła w postaci zwykłego tekstu
- Nie można delegować
- Tylko szyfrowanie DES
- Niewymagane w uwierzytelnianiu wstępnym protokołu Kerberos
- Konto jest wyłączone 

Narzędzie Azure ATP poinformuje Cię o tym, jeśli te flagi są lub wyłączyć w usłudze Azure Active Directory. Kolorowymi ikonami i odpowiedniego przełącznika wskazują stan każdego flagi. W przykładzie poniżej, tylko **hasło nigdy nie wygasa** znajduje się na usłudze Active Directory.

 ![flagi kontroli konta użytkownika](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Zweryfikować za pomocą usługi Windows Defender

Aby zapewnić wgląd obejmujących wiele produktów, profilu jednostki zawiera obiektów, które są otwarte alerty w usłudze Windows Defender za pomocą wskaźnika. Wyróżnienie informuje o tym, ile otwartych alertów, jednostka ma w usłudze Windows Defender i ich poziom ważności jest. Kliknij wskaźnik, aby przejść bezpośrednio do alerty związane z tej jednostki w usłudze Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Zwracaj uwagę na wrażliwi użytkownicy i grupy

Narzędzie Azure ATP Importuje grupę informacji o użytkowniku i z usługi Azure Active Directory, dzięki któremu można zidentyfikować użytkowników, którzy automatycznie są traktowane jako poufne, ponieważ są oni członkami następujących grup w usłudze Active Directory:

-   Administratorzy
-   Użytkownicy zaawansowani
-   Operatorzy kont
-   Operatorzy serwerów
-   Operatorzy drukowania
-   Operatorzy kopii zapasowych
-   Replikatorzy
-   Użytkownicy pulpitu zdalnego 
-   Operatorzy konfiguracji sieci 
-   Konstruktorzy przychodzących zaufań lasu
-   Administratorzy domeny
-   Kontrolery domeny
-   Twórcy-właściciele zasad grupy 
-   Kontrolery domeny tylko do odczytu 
-   Kontrolery domeny tylko do odczytu przedsiębiorstwa 
-   Administratorzy schematu 
-   Enterprise Admins

Ponadto mogą **ręcznie oznaczyć** jednostki jako poufnych w ramach usługi Azure ATP. Jest to ważne, ponieważ niektóre wykrywania zagrożeń usługi Azure ATP, np. wykrywania modyfikacji wrażliwych grup i ścieżki ruchu poprzecznego zależą od stanu czułości jednostki. Jeśli ręcznie oznaczyć dodatkowych użytkowników lub grup jako poufne, takie jak elementy członkowskie tablicy, kierownictwo firmy i dyrektorów sprzedaży narzędzia Azure ATP uzna je poufnych. Aby uzyskać więcej informacji, zobacz [Praca z kontami poufnymi](sensitive-accounts.md).

## <a name="be-aware-of-lateral-movement-paths"></a>Należy pamiętać o ścieżki ruchu poprzecznego

Narzędzie Azure ATP może pomóc w przed atakami wykorzystującymi ścieżki ruchu poprzecznego. Penetracja sieci to gdy osoba atakująca aktywnie używa niewrażliwe konta do uzyskania dostępu do wrażliwych kont.

Jeśli ścieżki ruchu poprzecznego istnieje dla jednostki, na stronie profilu jednostki można kliknąć przycisk **ścieżki ruchu poprzecznego** kartę. Diagram, który jest wyświetlany zawiera mapę możliwe ścieżki do wrażliwych użytkowników. 

Aby uzyskać więcej informacji, zobacz [Investigating ścieżkom penetracji sieci za pomocą narzędzia Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>To jest jednostka wystawionego jako przynęta

Przed przeniesieniem dochodzenie jest ważne, aby dowiedzieć się, czy jednostka jest wystawionego jako przynęta. Konta i jednostki można oznaczyć jako honeytokens w narzędzia Azure ATP. Po otwarciu profilu jednostki lub spowoduje wyświetlenie mini profilu konta lub obiekt, który został opatrzony tagami jako wystawionego jako przynęta, zostanie wyświetlony wskaźnik wystawionego jako przynęta. Podczas badania, wskaźnik wystawionego jako przynęta ostrzega o tym, czy wykonano działanie w ramach przeglądu, za pomocą konta, który został opatrzony tagami jako wystawionego jako przynęta.


    
## <a name="see-also"></a>Zobacz także

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)