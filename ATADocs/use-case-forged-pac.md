---
title: "Badanie ataków typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji | Microsoft Docs"
description: "W tym artykule opisano ataki typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji oraz instrukcje dotyczące badania w przypadku wykrycia tego typu zagrożenia w sieci."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 842e9866c5fdb447f49600501c4486da6db902f2
ms.sourcegitcommit: 4118dd4bd98994ec8a7ea170b09aa301a4be2c8a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*

# <a name="investigating-privilege-escalation-using-forged-authorization-data-attacks"></a>Badanie ataków typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji

Firma Microsoft nieustannie usprawnia swoje możliwości wykrywania zagrożeń oraz zapewniania analitykom zabezpieczeń informacji, dzięki którym mogą podejmować działania, niemal w czasie rzeczywistym. Usługa Advanced Threat Analytics (ATA) firmy Microsoft ułatwia wprowadzanie tych zmian. Jeśli usługa ATA wykrywa w Twojej sieci podejrzane działanie związane z podwyższeniem poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji i ostrzega o tym, ten artykuł pomoże Ci zrozumieć i zbadać sytuację.

## <a name="what-is-a-privileged-attribute-certificate-pac"></a>Co to jest certyfikat atrybutu uprawnień (PAC, Privileged Attribute Certificate)?

Certyfikat atrybutu uprawnień (PAC) to struktura danych w bilecie protokołu Kerberos, która przechowuje informacje dotyczące autoryzacji, takie jak członkostwa w grupach, identyfikatory zabezpieczeń i informacje o profilu użytkownika. W domenie usługi Active Directory umożliwia to przekazanie danych autoryzacji dostarczonych przez kontroler domeny do innych serwerów członkowskich i stacji roboczych w celu uwierzytelnienia i autoryzacji. Poza informacjami o członkostwie certyfikat PAC zawiera także dodatkowe informacje o poświadczeniach, informacje o profilach i zasadach oraz pomocnicze metadane zabezpieczeń. 

Protokoły uwierzytelniania (protokoły weryfikujące tożsamości) używają struktury danych certyfikatu PAC do transportowania informacji o autoryzacji, które kontrolują dostęp do zasobów.

### <a name="pac-validation"></a>Walidacja certyfikatu PAC

Walidacja certyfikatu PAC to funkcja zabezpieczeń uniemożliwiająca osobie atakującej uzyskanie nieautoryzowanego dostępu do systemu lub jego zasobów przy użyciu ataku typu man-in-the-middle, zwłaszcza w aplikacjach, w których jest stosowana personifikacja użytkownika. Personifikacja wymaga zaufanej tożsamości, na przykład konta usługi o podwyższonym poziomie uprawnień na potrzeby dostępu do zasobów i wykonywania zadań. Walidacja certyfikatu PAC wspiera bezpieczniejsze środowisko w ustawieniach uwierzytelniania Kerberos, gdzie ma miejsce personifikacja. [Walidacja certyfikatu PAC](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/) daje pewność, że użytkownik przedstawia dokładne dane autoryzacji udzielone w bilecie protokołu Kerberos i że uprawnienia biletu nie zostały zmodyfikowane.

Podczas walidacji certyfikatu PAC serwer koduje komunikat żądania zawierający długość oraz typ podpisu certyfikatu PAC i przekazuje go do kontrolera domeny. Kontroler domeny dekoduje żądanie i wyodrębnia sumę kontrolną serwera oraz wartości sum kontrolnych centrum dystrybucji kluczy. Jeśli weryfikacja sum kontrolnych powiedzie się, kontroler domeny zwróci kod powodzenia do serwera. Kod niepowodzenia oznacza, że certyfikat PAC został zmieniony. 

Zawartość certyfikatu PAC Kerberos jest podpisywana dwukrotnie: 
- Raz przy użyciu klucza głównego centrum dystrybucji kluczy, aby uniemożliwić złośliwym usługom po stronie serwera dokonywanie zmian danych autoryzacji
- Raz przy użyciu klucza głównego konta docelowego serwera zasobów, aby uniemożliwić użytkownikowi modyfikowanie zawartości certyfikatu PAC i dodanie własnych danych autoryzacji

### <a name="pac-vulnerability"></a>Luki w zabezpieczeniach certyfikatu PAC
Biuletyny zabezpieczeń [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) i [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) zawierają informacje o lukach w zabezpieczeniach w centrum dystrybucji kluczy Kerberos, które mogą umożliwić osobie atakującej manipulowanie polem certyfikatu PAC w prawidłowym bilecie protokołu Kerberos i przyznanie sobie dodatkowych uprawnień.

## <a name="privilege-escalation-using-forged-authorization-data-attack"></a>Atak typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji

Podczas ataku typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji osoba atakująca próbuje wykorzystać luki w zabezpieczeniach certyfikatu PAC do podniesienia swoich uprawnień w domenie lub lesie usługi Active Directory. Aby wykonać ten atak, osoba atakująca musi:
-   mieć poświadczenia użytkownika domeny;
-   mieć łączność sieciową z kontrolerem domeny, za pomocą którego można uwierzytelnić przejęte poświadczenia domeny;
-   mieć odpowiednie narzędzia. Python Kerberos Exploitation Kit (PyKEK) to znane narzędzie umożliwiające fałszowanie certyfikatów PAC.

Jeśli osoba atakująca ma potrzebne poświadczenia i łączność, może zmodyfikować lub sfałszować certyfikat atrybutu uprawnień (PAC) istniejącego tokenu logowania użytkownika protokołu Kerberos (TGT). Osoba atakująca zmienia oświadczenie członkostwa w grupie na grupę o wyższych uprawnieniach (na przykład „Administratorzy domeny” lub „Administratorzy przedsiębiorstwa”). Następnie osoba atakująca dodaje zmodyfikowany certyfikat PAC do biletu protokołu Kerberos. Bilet protokołu Kerberos jest potem używany do zażądania biletu usługi z kontrolera domeny bez zainstalowanej poprawki, co daje osobie atakującej podwyższony poziom uprawnień w domenie i autoryzację do wykonywania działań, do których ta osoba nie powinna mieć dostępu. Żądając tokenów dostępu do zasobów (TGS), osoba atakująca może za pomocą tokenu logowania użytkownika protokołu Kerberos (TGT) uzyskać dostęp do dowolnego zasobu w domenie. To oznacza, że osoba atakująca może pominąć wszystkie skonfigurowane listy ACL, które ograniczają dostęp do sieci, fałszując dane autoryzacji (PAC) dowolnego użytkownika w usłudze Active Directory.

## <a name="discovering-the-attack"></a>Wykrywanie ataku
Gdy osoba atakująca spróbuje podnieść poziom swoich uprawnień, usługa ATA wykryje to działanie i oznaczy jako alert o wysokiej ważności.

![Podejrzane działanie związane ze sfałszowanym certyfikatem PAC](./media/forged-pac.png)

Usługa ATA poinformuje w alercie dotyczącym podejrzanego działania o tym, czy podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji powiodło się, czy nie. Należy zbadać oba typy alertów, ponieważ próby zakończone niepowodzeniem oznaczają, że w środowisku jest obecna osoba atakująca.

## <a name="investigating"></a>Badanie
Po otrzymaniu w usłudze ATA alertu o podwyższeniu poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji należy określić sposób zminimalizowania skuteczności ataku. Aby to zrobić, należy najpierw sklasyfikować alert jako jeden z następujących: 
-   Wynik prawdziwie dodatni: złośliwa akcja wykryta przez usługę ATA
-   Wynik fałszywie dodatni: fałszywy alarm — podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji w rzeczywistości nie miało miejsca (usługa ATA pomyliła to zdarzenie z atakiem typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji)
-   Niegroźny wynik prawdziwie dodatni: akcja wykryta przez usługę ATA miała miejsce, ale nie jest złośliwa — może to być na przykład test penetracyjny

Poniższy wykres ułatwi podjęcie odpowiednich kroków:

![Diagram badania alertu o sfałszowanym certyfikacie PAC](./media/forged-pac-diagram.png)

1. Najpierw sprawdź alert w osi czasu ataków w usłudze ATA, aby dowiedzieć się, czy próba sfałszowania autoryzacji powiodła się, nie powiodła się, czy jedynie ją podjęto (próby ataków są także atakami zakończonymi niepowodzeniem). Zarówno ataki zakończone powodzeniem, jak i niepowodzeniem mogą mieć wynik prawdziwie dodatni, ale z różnymi poziomami ważności w środowisku.
 
 ![Podejrzane działanie związane ze sfałszowanym certyfikatem PAC](./media/forged-pac-sa.png)


2.  Jeśli wykryty atak typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji zakończył się powodzeniem:
    -   Jeśli kontroler domeny, którego dotyczy alert, ma zainstalowane odpowiednie poprawki, jest to wynik fałszywie dodatni. W tym przypadku należy odrzucić alert i wysłać wiadomość e-mail z powiadomieniem do zespołu usługi ATA (ATAEval@microsoft.com), abyśmy mogli usprawnić nasze funkcje wykrywania. 
    -   Jeśli kontroler domeny w alercie nie ma zainstalowanych odpowiednich poprawek:
        -   Jeśli usługa wymieniona w alercie nie ma własnego mechanizmu autoryzacji, jest to wynik prawdziwie dodatni i należy uruchomić proces reagowania na zdarzenia organizacji. 
        -   Jeśli usługa wymieniona w alercie ma wewnętrzny mechanizm autoryzacji żądający danych autoryzacji, może on zostać błędnie zidentyfikowany jako atak typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji. 

3.  Jeśli wykryty atak zakończył się niepowodzeniem:
    -   Jeśli system operacyjny lub aplikacja modyfikują certyfikat PAC, prawdopodobnie jest to wynik niegroźny prawdziwie dodatni i należy rozwiązać ten problem z pomocą właściciela aplikacji lub systemu operacyjnego.

    -   Jeśli system operacyjny lub aplikacja nie modyfikuje certyfikatu PAC: 

        -   Jeśli wymieniona usługa nie ma własnej usługi autoryzacji, jest to wynik prawdziwie dodatni i należy uruchomić proces reagowania na zdarzenia organizacji. Mimo iż osobie atakującej nie udało się podnieść swoich uprawnień w domenie, można założyć, że w sieci jest obecna osoba atakująca, i należy ją jak najszybciej odnaleźć, zanim spróbuje podnieść swoje uprawnienia przy użyciu innych zaawansowanych ataków ciągłych. 
        -   Jeśli usługa wymieniona w alercie ma własny mechanizm autoryzacji żądający danych autoryzacji, może on zostać błędnie zidentyfikowany jako atak typu podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji.

## <a name="post-investigation"></a>Po badaniu
Firma Microsoft zaleca skorzystanie z pomocy profesjonalnego zespołu ds. reagowania na zdarzenia i odzyskiwania (z którym można się skontaktować za pośrednictwem zespołu kont Microsoft), aby ustalić, czy osoba atakująca użyła w sieci metod ciągłych.


## <a name="mitigation"></a>Środki zaradcze

Zastosuj biuletyny zabezpieczeń [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) i [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx), które dotyczą luk w zabezpieczeniach w centrum dystrybucji kluczy Kerberos. 


## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
