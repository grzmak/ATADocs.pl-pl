---
title: Jak badać użytkowników i komputerów z Azure ATP | Dokumentacja firmy Microsoft
description: Zawiera opis sposobu badania podejrzane działania wykonywane przez użytkowników, jednostek, komputery lub urządzenia przy użyciu usługi Azure Advanced Threat ochrony (ATP)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4ef4151a311dd5b076737cba9f3c7aa7454a32a7
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/16/2018
---
*Dotyczy: Azure Advanced Threat Protection wersji 1.9*



# <a name="investigate-an-entity-with-azure-atp"></a>Zbadaj jednostki z Azure ATP

W tym artykule opisano proces badanie jednostek po podejrzanych działań wykryto z Azure Advanced Threat ochrony (ATP). Po wyświetleniu podejrzanych działań w osi czasu, można przejść do jednostki zaangażowane w działaniu i użyj następujące parametry i szczegóły, aby dowiedzieć się więcej o co się stało i co należy zrobić w celu ograniczenia ryzyka.

## <a name="look-at-the-entity-profile"></a>Przyjrzyj się profilu jednostki

Profilu jednostki zapewnia kompleksowe jednostki strony z przeznaczone do badania pełnej szczegółowo użytkowników, komputerów, urządzeń, i zasoby, które mają dostęp do historii. Strony profilu korzysta z nowych translator aktywności logicznej Azure ATP, można przyjrzeć się grupy działań występujących (zagregowane maksymalnie minutę) i grupować w pojedyncze działanie logiczne które pozwalają na lepsze zrozumienie działania rzeczywiste Użytkownicy.

Aby uzyskać dostęp do strony profilu jednostki, kliknij nazwę podmiotu, takie jak nazwa użytkownika, na osi czasu podejrzanych działań. Można również sprawdzić minimalnej wersji na stronie podejrzanych działań profilu jednostki, ustawiając kursor nad nazwa jednostki.

Profilu jednostki umożliwia wyświetlanie jednostki działań, wyświetlać dane katalogu i wyświetlanie ścieżek penetracja sieci dla jednostki. Aby uzyskać więcej informacji, zobacz [badanie profile jednostek ](entity-profiles.md).

## <a name="check-entity-tags"></a>Wybierz tagi jednostek

Azure ATP pobiera tagi z usługi Active Directory, aby mieć jeden interfejs monitorowanie użytkowników usługi Active Directory i jednostek. Znaczniki dostarczają informacji na temat jednostki z usługi Active Directory, w tym:
- Częściowe: Użytkownika, komputera lub grupy nie został zsynchronizowany z domeny, a częściowo został rozwiązany za pomocą wykazu globalnego. Niektóre atrybuty nie są dostępne.
- Nierozpoznane: Tego komputera nie została rozpoznana na prawidłową jednostkę w lesie usługi active directory. Informacje katalogu są niedostępne.
- Usunięto: Jednostka została usunięta z usługi Active Directory.
- Wyłączone: Jednostka jest wyłączone w usłudze Active Directory.
- Zablokowane: Jednostka wprowadzony zbyt wiele razy nieprawidłowe hasło i jest zablokowany.
- Ważność: Jednostka wygasła w usłudze Active Directory.
- Nowy: Mniej niż 30 dni temu została utworzona jednostka.

## <a name="look-at-the-user-access-control-flags"></a>Przyjrzyj się flag kontroli dostępu użytkownika

Flagi kontrolne dostępu użytkownika również są importowane z usługi Active Directory. Azure ATP zawiera 10 flagi, które zostaną zastosowane do badania: 
- Hasło nigdy nie wygasa
- Zaufany w kwestii delegowania
- Wymagana karta inteligentna
- Hasło wygasło
- Puste hasło może
- Przechowywane hasła zwykłego tekstu
- Nie może być delegowane
- Tylko szyfrowania DES
- Wstępne uwierzytelnianie Kerberos nie jest wymagane
- Konto jest wyłączone 

Azure ATP informuje o tym, jeśli te flagi są lub wyłącz w usłudze Azure Active Directory. Kolorowe ikony wskazują, że flaga jest na, w usłudze Active Directory; w przykładzie poniżej tylko **Konto wyłączone** jest włączona w usłudze Active Directory.

 ![Flagi kontrolne dostępu użytkownika](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Zweryfikować usługa Windows Defender

Aby zapewnić iloczyn wektorowy szczegółowe informacje, profilu jednostki udostępnia obiektów, które mają otwarte alerty w programie Windows Defender z wskaźnika. Wyróżnienie informuje liczbę otwartych alertów jednostka znajduje się w usłudze Windows Defender i ich poziom ważności jest. Kliknij pozycję wskaźnika, aby przejść bezpośrednio do alerty powiązane z tą jednostką w usłudze Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Śledzić poufnych użytkowników i grup

Azure ATP importuje informacje o grupie użytkowników i z usługi Azure Active Directory, dzięki któremu można zidentyfikować użytkowników, którzy automatycznie są traktowane jako poufne, ponieważ są oni członkami następujących grup w usłudze Active Directory:

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
-   Kontrolery domeny tylko do odczytu 
-   Administratorzy schematu 
-   Enterprise Admins

Ponadto można **ręcznie tagu** jednostek jako poufne w Azure ATP. Jest to ważne, ponieważ niektóre wykryć Azure ATP, takich jak grupy poufnej modyfikacji wykrywania i ścieżka penetracja sieci, korzystają z stan czułości jednostki. Jeśli ręcznie tagu dodatkowych użytkowników lub grup jako poufne, takie jak tablicy elementów członkowskich, członkowie kadry kierowniczej w firmie i dyrektora sprzedaży Azure ATP będzie uwzględniać ich poufnych. Aby uzyskać więcej informacji, zobacz [Praca z kont poufnych](sensitive-accounts.md).

## <a name="be-aware-of-lateral-movement-paths"></a>Należy pamiętać o penetracji sieci ścieżki

Azure ATP ułatwia zapobieganie atakom, które używają ścieżek penetracji sieci. Penetracja sieci to, gdy osoba atakująca aktywnie używa konta niepoufnych uzyskanie dostępu do kont poufnych.

Jeśli istnieje ścieżka penetracja sieci dla jednostki, na stronie profilu jednostki można kliknąć przycisk **penetracji ścieżki przepływu** kartę. Diagram, który jest wyświetlany zawiera mapy możliwych ścieżek użytkownikowi poufnych. 

Aby uzyskać więcej informacji, zobacz [Investigating ścieżek penetracja sieci Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>Jest to jednostka wystawionego jako przynęta?

Przed przeniesieniem o badaniu należy sprawdzić, czy jednostka jest wystawionego jako przynęta. Dla wygody Azure ATP umożliwia utworzenie tagu konta i jednostki jako honeytokens. Następnie podczas badania, po otwarciu profilu jednostki lub mini profilu, zobaczysz wskaźnika wystawionego jako przynęta, aby ostrzec o tym, że działanie, które są patrzeć została wykonana przez użytkownika konta, które są oznaczone jako wystawionego jako przynęta.


    
## <a name="see-also"></a>Zobacz też

- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)