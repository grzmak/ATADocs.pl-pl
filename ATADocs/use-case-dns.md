---
title: "Badanie rekonesansu przy użyciu systemu DNS | Microsoft Docs"
description: "W tym artykule opisano rekonesans przy użyciu systemu DNS oraz instrukcje dotyczące badania w przypadku wykrycia tego typu zagrożenia przez usługę ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f85d52420c55e2f1119ad14eb1a6c957fbc50be6
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*

# <a name="investigating-reconnaissance-using-dns"></a>Badanie rekonesansu przy użyciu systemu DNS

Jeśli usługa ATA wykrywa w Twojej sieci **rekonesans przy użyciu systemu DNS** i ostrzega o tym, ten artykuł pomoże Ci zbadać ten alert i zrozumieć, jak można rozwiązać ten problem.

## <a name="what-is-reconnaissance-using-dns"></a>Co to jest rekonesans przy użyciu systemu DNS?

Alert **Rekonesans przy użyciu systemu DNS** wskazuje, że nietypowy host wysyła podejrzane zapytania systemu nazw domen (DNS, Domain Name System) w celu przeprowadzenia rekonesansu w Twojej sieci wewnętrznej.

System nazw domen (DNS) to usługa zaimplementowana jako hierarchiczna, rozproszona baza danych, która umożliwia rozpoznawanie nazw hostów i nazw domen. Nazwy w bazie danych DNS tworzą hierarchiczną strukturę drzewa nazywaną obszarem nazw domeny.
Dla osoby atakującej system DNS zawiera cenne informacje umożliwiające mapowanie sieci wewnętrznej, w tym listę wszystkich serwerów, a często także wszystkich klientów zamapowanych na adresy IP. Ponadto te informacje są wartościowe, ponieważ zawierają listę nazw hostów, które często są opisowe w danym środowisku sieciowym. Uzyskanie tych informacji umożliwia osobie atakującej efektywniejsze priorytetyzowanie wysiłków dotyczących jednostek odpowiednich dla kampanii. Narzędzia takie jak [Nmap](https://nmap.org/) i [Fierce](https://github.com/mschwager/fierce) oraz wbudowane narzędzia takie jak [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx) pozwalają na odnajdywanie hostów za pomocą rekonesansu DNS.
Wykrycie rekonesansu przy użyciu zapytań DNS z hosta wewnętrznego daje powód do niepokoju i wskazuje na możliwość istniejącego naruszenia hosta, szerszego naruszenia sieci lub na możliwość zagrożenia wewnętrznego.

## <a name="dns-query-types"></a>Typy zapytań DNS

W protokole DNS istnieje kilka typów zapytań. Usługa ATA wykrywa żądania AXFR (transferu) i tworzy alert, gdy są one widoczne. Zapytania tego typu powinny pochodzić tylko z serwerów DNS.

## <a name="discovering-the-attack"></a>Wykrywanie ataku

Gdy osoba atakująca próbuje wykonać rekonesans przy użyciu systemu DNS, usługa ATA wykrywa to działanie i oznacza je ze średnią ważnością.

![Wykrycie rekonesansu DNS przez usługę ATA](./media/dns-recon.png)
 
Usługa ATA wyświetla nazwę maszyny źródłowej oraz dodatkowe szczegóły dotyczące rzeczywiście wykonanego zapytania DNS. Przykładowo z tego samego hosta może zostać podjętych wiele prób.

## <a name="investigating"></a>Badanie

Aby zbadać rekonesans przy użyciu systemu DNS, najpierw należy ustalić przyczynę zapytań. Można je przydzielić do jednej z następujących kategorii: 
-   Prawdziwie dodatnie — do sieci dostała się osoba atakująca lub znajduje się w niej złośliwe oprogramowanie. Może to być osoba atakująca, która złamała obwód sieci, lub zagrożenie wewnętrzne.
-   Niegroźne prawdziwie dodatnie — mogą to być alerty wyzwalane przez testowanie penetracyjne, działania zespołu ekspertów, skanery zabezpieczeń, zaporę nowej generacji lub administratorów IT wykonujących oficjalnie zaakceptowane działania.
-   Fałszywie dodatnie — możesz otrzymywać alerty spowodowane błędami konfiguracji, na przykład jeśli port 53 protokołu UDP zostanie zablokowany między bramą usługi ATA i serwerem DNS (może to być także każdy inny problem sieciowy).

Poniższy wykres ułatwi ustalenie odpowiednich kroków badania:

![Rozpoznawanie rekonesansu DNS za pomocą usługi ATA](./media/dns-recon-diagram.png)
 
1.  Pierwszym krokiem jest zidentyfikowanie maszyny, z której pochodzi alert, jak przedstawiono poniżej:
 
    ![Wyświetlanie podejrzanych działań rekonesansu DNS w usłudze ATA](./media/dns-recon.png)
2.  Zidentyfikuj przeznaczenie danej maszyny. Czy jest to stacja robocza, serwer, administracyjna stacja robocza, stacja do testowania penetracyjnego itp.?
3.  Jeśli dany komputer jest serwerem DNS i ma uzasadnione prawa do żądania dodatkowej kopii strefy, to wynik jest fałszywie dodatni. Po znalezieniu wyniku fałszywie dodatniego użyj opcji **Wyklucz**, aby nie otrzymywać więcej tego określonego alertu dla tej maszyny.
4. Upewnij się, że port 53 protokołu UDP między bramą usługi ATA i serwerem DNS jest otwarty.
4.  Jeśli komputer jest używany do pracy administracyjnej lub do testowania penetracyjnego, to wynik jest niegroźnie prawdziwie dodatni, a daną maszynę także można skonfigurować jako wyjątek.
5.  Jeśli nie jest on używany do testowania penetracyjnego, sprawdź, czy na maszynie działa skaner zabezpieczeń lub zapora nowej generacji, co także może powodować wysyłanie żądań DNS typu AXFR.
6.  Jeśli żadne z tych kryteriów nie jest spełnione, istnieje możliwość, że maszyna została naruszona, i musi zostać w pełni zbadana. 
7.  Jeśli zapytania pochodzą z określonych maszyn i ustalono, że nie są one niegroźne, należy wykonać następujące czynności:
    1.  Przejrzyj dostępne źródła dzienników. 
    2.  Przeprowadź analizę opartą na hoście. 
    3.  Jeśli działanie nie pochodzi od podejrzanego użytkownika, na danej maszynie należy przeprowadzić analizę śledczą, aby określić, czy została ona naruszona za pomocą złośliwego oprogramowania.

## <a name="post-investigation"></a>Po badaniu

Złośliwe oprogramowanie użyte do naruszenia bezpieczeństwa hosta może zawierać konie trojańskie z funkcją tylnego wejścia. W przypadku wykrycia pomyślnej penetracji sieci z naruszonego hosta działania zaradcze powinny uwzględniać zmianę wszelkich haseł i poświadczeń używanych na danym hoście i na każdym hoście objętym penetracją sieci. 

Jeśli po wykonaniu działań zaradczych nie można potwierdzić, że zaatakowany host jest czysty, lub nie można określić głównej przyczyny naruszenia bezpieczeństwa, firma Microsoft zaleca wykonanie kopii zapasowej krytycznych danych i ponowne skompilowanie hosta. Ponadto należy wzmocnić zabezpieczenia nowych lub odbudowanych hostów przed umieszczeniem ich w sieci, aby zapobiec ponownej infekcji. 

Firma Microsoft zaleca skorzystanie z pomocy profesjonalnego zespołu ds. reagowania na zdarzenia i odzyskiwania (z którym można się skontaktować za pośrednictwem zespołu kont Microsoft), aby ustalić, czy osoba atakująca użyła w sieci metod ciągłych.

## <a name="mitigation"></a>Środki zaradcze

Aby zabezpieczyć wewnętrzny serwer DNS w celu uniemożliwienia przeprowadzenia rekonesansu przy użyciu systemu DNS, można wyłączyć transfery stref lub ograniczyć je tylko do określonych adresów IP. Aby uzyskać dodatkowe informacje o ograniczaniu transferów stref, zobacz artykuł w witrynie TechNet systemu Windows Server [Ograniczanie transferów stref](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx). Ograniczone transfery stref można dalej zablokować przez [zabezpieczenie transferów stref przy użyciu protokołu IPsec](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx). Modyfikacja transferów stref jest jednym z zadań na liście czynności, które należy wykonać w celu [zabezpieczenia serwerów DNS przed atakami wewnętrznymi i zewnętrznymi](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).



## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
