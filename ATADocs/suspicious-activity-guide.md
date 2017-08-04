---
title: "Przewodnik usługi ATA dotyczący podejrzanych działań | Microsoft Docs"
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8c93f4485998bbb1b2b440f01fed8d96ad4e2842
ms.sourcegitcommit: 7bc04eb4d004608764b3ded1febf32bc4ed020be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/02/2017
---
*Dotyczy: Advanced Threat Analytics w wersji 1.8*


# <a name="introduction"></a>Wprowadzenie

Usługa ATA wykrywa następujące fazy zaawansowanego ataku: rekonesans, przejęcie poświadczeń, penetracja sieci, podwyższenie poziomu uprawnień, zdominowanie domeny i inne.

Fazy w łańcuchu kończenia gdzie usługa ATA zapewnia obecnie wykryć zostały wyróżnione na tym diagramie.

![Usługa ATA skupia się na penetracji sieci w ataku typu kill chain](media/attack-kill-chain-small.jpg)

W tym artykule przedstawiono szczegóły każdego podejrzanego działania w poszczególnych fazach.


## <a name="reconnaissance-using-account-enumeration"></a>Rekonesans przy użyciu wyliczania kont

> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Atak polegający na wyliczaniu kont to technika używana przez osoby atakujące w celu odgadnięcia różnych nazw kont. Wykorzystuje ona próby uwierzytelnienia Kerberos w celu określenia, czy dany użytkownik występuje w sieci. Pomyślnie odgadnięte konta mogą być stosowane na kolejnych etapach ataku. | Zbadaj dany komputer i spróbuj określić, czy istnieje uzasadniona przyczyna uruchomienia tak wielu procesów uwierzytelniania Kerberos. Są to procesy, które próbowały poznać wiele kont i nie udało im się to, ponieważ dany użytkownik nie istnieje (błąd Client_Principal_Unknown), ale co najmniej jedna próba dostępu zakończyła się sukcesem. <br></br>**Wyjątki:** ta metoda wykrywania opiera się na znalezieniu wielu nieistniejących kont oraz prób uwierzytelnienia z jednego komputera. Jeśli użytkownik popełni błąd podczas ręcznego wpisywania nazwy użytkownika lub domeny, próba uwierzytelnienia jest postrzegana jako próba zalogowania się na nieistniejące konto. Serwery terminali wymagające logowania się przez wielu użytkowników mogą rzeczywiście napotykać dużą liczbę omyłkowych prób zalogowania. |Zbadaj proces odpowiedzialny za generowanie tych żądań.  Aby uzyskać pomoc w identyfikacji procesów na podstawie portu źródłowego, zobacz artykuł [Have you ever wanted to see which Windows process sends a certain packet out to network? (Czy chcesz zobaczyć, który proces systemu Windows wysyła określony pakiet do sieci?)](https://blogs.technet.microsoft.com/nettracer/2010/08/02/have-you-ever-wanted-to-see-which-windows-process-sends-a-certain-packet-out-to-network/)|Średni|

## <a name="reconnaissance-using-directory-services-enumeration-sam-r"></a>Rekonesans przy użyciu wyliczania usług katalogowych (SAM-R)

> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
Rekonesans usług irectory to technika, używane przez osoby atakujące mapy strukturę katalogów i stosowanie uprzywilejowanych kont do wykonania kolejnych kroków ataku. Protokół Security Account Manager Remote (SAM-R) to jedna z metod używanych do wysyłania zapytań o katalog. | Dowiedz się, dlaczego dany komputer korzysta z protokołu Security Accounts Manager — Remote (MS-SAMR). Jest to proces wykonywany w nietypowy sposób i prawdopodobnie wiąże się z zapytaniami o jednostki poufne. <br></br>**Wyjątki:** ta metoda wykrywania polega na profilowaniu normalnego zachowania użytkowników wysyłających zapytania SAM-R oraz ostrzeganiu w przypadku zaobserwowania zapytania nietypowego. Użytkownicy uprzywilejowani logujący się do komputerów, które do nich nie należą, mogą spowodować wywołanie zapytania SAM-R wykrywanego jako nietypowe nawet wtedy, gdy jest to element normalnego procesu pracy. Sytuacje takie mogą spotykać często członków zespołu IT. Jeśli dany przypadek został oznaczony jako podejrzany, ale wynika z normalnego użytkowania, jest to spowodowane faktem, że dane zachowanie nie zostało wcześniej zaobserwowane przez usługę ATA. | W takiej sytuacji zaleca się zastosowanie dłuższego okresu uczenia oraz lepszego pokrycia usługi ATA w domenie, zgodnie z lasem usługi Active Directory.<br></br>[Pobierz i uruchom narzędzie „SAMRi10”](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b). Narzędzie SAMRi10 zostało opublikowane przez zespół usługi ATA i zwiększa odporność środowiska na zapytania SAM-R. | Średni|

## <a name="reconnaissance-using-dns"></a>Rekonesans przy użyciu systemu DNS


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Serwer DNS zawiera mapę wszystkich komputerów, adresów IP i usług w sieci. Te informacje są używane przez osoby atakujące do mapowania struktury sieci i interesujących komputerów docelowych do wykonania kolejnych kroków ataku. | Dowiedz się, dlaczego dany komputer wykonuje zapytanie o pełny transfer strefy (AXFR) w celu pobrania wszystkich rekordów z domeny DNS. <br></br>**Wyjątki:** ta metoda wykrywania identyfikuje serwery inne niż DNS, które wysyłają żądania transferu strefy DNS. Istnieje kilka skanerów zabezpieczeń, które są znane z przesyłania tego rodzaju żądań do serwerów DNS. <br></br>Sprawdź także, czy usługa ATA może komunikować się za pośrednictwem portu 53 z bram usługi ATA do serwerów DNS w celu uniknięcia wyników fałszywie dodatnich.| Ogranicz transfer strefy, starannie wybierając hosty, które mogą go żądać. Aby uzyskać więcej informacji, zobacz artykuły [Zabezpieczanie serwera DNS](https://technet.microsoft.com/library/cc770474(v=ws.11).aspx) i [Lista kontrolna: Zabezpieczanie serwera DNS](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx). |Średni|

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekonesans przy użyciu wyliczania sesji SMB


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Wyliczanie bloku komunikatów serwera (SMB, Server Message Block) umożliwia osobie atakującej uzyskiwanie informacji na temat adresów IP, z których niedawno logowali się użytkownicy sieci. Po uzyskaniu tych informacji osoba atakująca może użyć ich do atakowania określonych kont i poruszania się po danym poziomie sieci. | Dowiedz się, dlaczego dany komputer wykonuje wyliczenia sesji SMB.<br></br>**Wyjątki:** ta metoda wykrywania opiera się na założeniu, że wyliczanie sesji SMB nie ma uzasadnionego użytku w sieci przedsiębiorstwa, jednakże niektóre skanery zabezpieczeń (takie jak Websense) wysyłają takie żądania. | [Use the net cease tool to harden your environment (Używanie narzędzia Net Cease do wzmacniania zabezpieczeń środowiska)](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) | Średni   |

## <a name="brute-force-ldap-kerberos-ntlm"></a>Atak siłowy (LDAP, Kerberos, NTLM)


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| W przypadku ataków siłowych osoba atakująca próbuje użyć wielu różnych haseł, licząc na to, że w końcu uda jej się je odgadnąć. Osoba atakująca systematycznie sprawdza wszystkie możliwe hasła (lub duży zestaw możliwych haseł) do momentu odnalezienia prawidłowego. Po odgadnięciu poprawnego hasła osoba atakująca może zalogować się do sieci tak, jakby była normalnym użytkownikiem. Obecnie usługa ATA obsługuje poziome (wiele kont) ataki siłowe przy użyciu protokołu Kerberos lub NTLM oraz ataki poziome i pionowe (jedno konto, wiele prób podania hasła) przy użyciu prostego powiązania LDAP. | Dowiedz się, dlaczego dany komputer nie jest w stanie uwierzytelnić wielu kont użytkowników (przy mniej więcej podobnej liczbie prób uwierzytelnienia wielu użytkowników) lub dlaczego wykryto dużą liczbę zakończonych niepowodzeniem prób uwierzytelnienia jednego użytkownika. <br></br>**Wyjątki:** ta metoda wykrywania opiera się na profilowaniu normalnego zachowania kont uwierzytelnianych w wielu zasobach. W przypadku wykrycia nietypowego wzorca wywoływany jest alert. Ten wzorzec nie jest nietypowy w przypadku skryptów uwierzytelniających automatycznie, które korzystają z nieaktualnych poświadczeń (nieprawidłowe hasło lub nazwa użytkownika). | Złożone, długie hasła stanowią wymagany pierwszy poziom zabezpieczeń przed atakami siłowymi. | Średni   |

## <a name="sensitive-account-exposed-in-plain-text-authentication-and-service-exposing-accounts-in-plain-text-authentication"></a>Poufne konto uwidocznione podczas uwierzytelnienia zwykłym tekstem i usługa uwidaczniająca konta podczas uwierzytelniania zwykłym tekstem


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Niektóre usługi na komputerze wysyłają poświadczenia kont w postaci zwykłego tekstu, nawet w przypadku kont poufnych. Osoby atakujące monitorujące ruch mogą przechwycić te poświadczenia do złośliwych celów. Alert wywołują wszystkie przypadki przesłania zwykłym tekstem haseł do kont poufnych. | Odszukaj odpowiedni komputer i dowiedz się, dlaczego korzysta z prostych powiązań LDAP. | Sprawdź konfigurację komputerów źródłowych i upewnij się, że nie korzystają z prostych powiązań LDAP. Zamiast prostych powiązań LDAP użyj warstwy LDAP SALS lub protokołu LDAPS. Postępuj zgodnie z zasadami warstwowej struktury zabezpieczeń i ogranicz dostęp we wszystkich warstwach, aby zapobiec podwyższeniu poziomu uprawnień. | Niska dla uwidaczniania usług, średnia dla kont poufnych |

## <a name="honey-token-account-suspicious-activities"></a>Podejrzane działania związane z kontem wystawionym jako przynęta


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Konta wystawione jako przynęta są fikcyjnymi kontami konfigurowanymi w celu przechwytywania, identyfikowania i śledzenia złośliwych działań w sieci obejmujących te konta. Są to konta nieużywane i nieaktywne w sieci, a nieoczekiwane działania z konta wystawionego jako przynęta mogą wskazywać próbę wykorzystania tego konta przez złośliwego użytkownika. | Dowiedz się, dlaczego konto wystawione jako przynęta podejmuje próbę uwierzytelnienia z danego komputera. | Przejrzyj strony profilów usługi ATA dla innych kont poufnych (uprzywilejowanych) w środowisku, aby sprawdzić, czy występują potencjalnie podejrzane działania. | Średni   |

## <a name="unusual-protocol-implementation"></a>Implementacja nietypowego protokołu


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
|Osoby atakujące mogą wykorzystywać narzędzia stosujące protokoły SMB/Kerberos na określone sposoby umożliwiające im uzyskanie określonych możliwości w sieci. Wskazuje to zastosowanie złośliwych technik stosowanych w atakach typu Over-Pass-the-Hash i atakach siłowych. | Dowiedz się, dlaczego dany komputer korzysta z protokołu uwierzytelniania lub SMB w nietypowy sposób. <br></br>Aby określić, czy jest to atak WannaCry, wykonaj następujące działania:<br></br> 1.    Pobierz eksport podejrzanego działania w formacie programu Excel.<br></br>2.    Otwórz kartę działań sieci i przejdź do pola „Json”, aby skopiować powiązane obiekty JSON Smb1SessionSetup i Ntlm<br></br>3.   Jeśli wartość Smb1SessionSetup.OperatingSystem to „Windows 2000 2195”, wartość Smb1SessionSetup.IsEmbeddedNtlm to „true”, a wartość Ntlm.SourceAccountId to „null”, jest to atak WannaCry.<br></br><br></br>**Wyjątki:** wykrycie może nastąpić w rzadkich przypadkach, w których uprawnione narzędzia implementują protokoły w sposób niestandardowy. Tak działają na przykład niektóre aplikacja do testów penetracyjnych. | Zarejestruj ruch sieciowy i sprawdź, który proces generuje ruch z nietypową implementacją protokołu.| Średni|

## <a name="malicious-data-protection-private-information-request"></a>Złośliwe żądanie informacji prywatnych z zakresu ochrony danych


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
|Interfejs API ochrony danych (DPAPI, Data Protection API) jest używany przez różne składniki systemu Windows w celu bezpiecznego przechowywania haseł, kluczy szyfrowania i innych danych poufnych. Kontrolery domeny przechowują zapasowy klucz główny, który umożliwia odszyfrowanie wszystkich wpisów tajnych zaszyfrowanych przy użyciu interfejsu DPAPI przez maszyny z systemem Windows przyłączone do domeny. Osoby atakujące mogą użyć zapasowego klucza głównego domeny DPAPI w celu odszyfrowania wszystkich wpisów tajnych na wszystkich maszynach przyłączonych do domeny (hasła przeglądarek, zaszyfrowane pliki itp.).| Dowiedz się, dlaczego komputer wysłał żądanie przy użyciu tego nieudokumentowanego wywołania interfejsu API dla klucza głównego interfejsu DPAPI.|Dodatkowe informacje na temat interfejsu DPAPI zamieszczono w artykule [Windows Data Protection (Ochrona danych w systemie Windows)](https://msdn.microsoft.com/library/ms995355.aspx).|Wysoki|

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Podejrzenie kradzieży tożsamości na podstawie nietypowego zachowania


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Po utworzeniu modelu zachowań (utworzenie modelu zachowań wymaga co najmniej 50 aktywnych kont na przestrzeni 3 tygodni) każde nietypowe zachowanie wywołuje alert. Zachowanie, które nie pasuje do modelu utworzonego dla określonego konta użytkownika, może wskazywać na kradzież tożsamości. | Dowiedz się, dlaczego dany użytkownik może zachowywać się inaczej. <br></br>**Wyjątki:** jeśli usługa ATA zapewnia tylko częściowe pokrycie (nie wszystkie kontrolery domen są przekierowywane do bramy usługi ATA), poznawane są tylko niektóre działania danego użytkownika. Jeśli nagle po ponad 3 tygodniach usługa ATA zaczyna obejmować cały ruch sieciowy, pełnia działań użytkownika może wywołać alert. | Upewnij się, że usługa ATA została wdrożona we wszystkich kontrolerach domen. <br></br>1.  Sprawdź, czy użytkownik zmienił stanowisko w organizacji.<br></br>2.  Sprawdź, czy użytkownik jest pracownikiem sezonowym.<br></br>3.  Sprawdź, czy użytkownik właśnie wrócił po długiej nieobecności.| Średnia dla wszystkich użytkowników i wysoka dla użytkowników uprzywilejowanych |


## <a name="pass-the-ticket"></a>Ataki typu Pass-the-Ticket


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Atak typu Pass-the-Ticket to technika ruchu po danym poziomie sieci, w której osoba atakująca dokonuje kradzieży biletu Kerberos z jednego z komputerów i przy jego użyciu uzyskuje dostęp do innego komputera, podszywając się pod jednostkę w sieci. | Ta metoda wykrywania polega na identyfikacji zastosowania tych samych biletów Kerberos na co najmniej dwóch różnych komputerach. W niektórych przypadkach, jeśli adresy IP zmieniają się z dużą częstotliwością, usługa ATA może nie być w stanie określić, czy różne adresy IP są używane przez ten sam komputer, czy przez różne komputery. Jest to typowy problem w przypadku zbyt małych puli DHCP (VPN, Wi-Fi itp.) oraz współdzielonych adresów IP (urządzenia NAT). | Postępuj zgodnie z zasadami warstwowej struktury zabezpieczeń i ogranicz dostęp we wszystkich warstwach, aby zapobiec podwyższeniu poziomu uprawnień. | Wysoki     |

## <a name="pass-the-hash"></a>Ataki typu Pass-the-Hash


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| W przypadku ataku Pass-the-Hash osoba atakująca uwierzytelnia się na serwerze zdalnym lub w usłudze zdalnej przy użyciu podstawowego skrótu NTLM hasła użytkownika zamiast skojarzonego hasła w postaci zwykłego tekstu, jak to się dzieje zazwyczaj. | Sprawdź, czy konto przeprowadzało jakieś nietypowe działania w czasie zbliżonym do momentu wystąpienia alertu. | Wdróż zalecenia opisane w artykule [Pass-the-Hash](http://aka.ms/PtH). Postępuj zgodnie z zasadami warstwowej struktury zabezpieczeń i ogranicz dostęp we wszystkich warstwach, aby zapobiec podwyższeniu poziomu uprawnień. | Wysoki|

## <a name="over-pass-the-hash"></a>Ataki typu Over-Pass-the-Hash


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Atak typu Over-Pass-the-Hash wykorzystuje słabość implementacji protokołu uwierzytelniania Kerberos polegającą na tym, że skrót NTLM umożliwia utworzenie biletu Kerberos, pozwalając osobie atakującej na uwierzytelnienie w usługach w sieci bez hasła użytkownika. | Obniżenie poziomu szyfrowania: dowiedz się, dlaczego dane konto korzysta z szyfrowania RC4 protokołu Kerberos po poznaniu szyfrowania AES. <br></br>**Wyjątki:** ta metoda wykrywania opiera się na profilowaniu metod szyfrowania używanych w domenie oraz wysyłaniu alertów w przypadku wykrycia nietypowej, słabszej metody. W niektórych przypadkach stosowana jest słabsza metoda szyfrowania, a usługa ATA wykrywa ją jako nietypową, mimo że jest częścią normalnego (choć rzadkiego) procesu roboczego. Taka sytuacja może wystąpić, jeśli dane zachowanie nie zostało wcześniej zaobserwowane przez usługę ATA. Pomocne jest zapewnienie lepszego pokrycia usługi ATA w domenie. | Wdróż zalecenia opisane w artykule [Pass-the-Hash](http://aka.ms/PtH). Postępuj zgodnie z zasadami warstwowej struktury zabezpieczeń i ogranicz dostęp we wszystkich warstwach, aby zapobiec podwyższeniu poziomu uprawnień. | Wysoki     |

## <a name="privilege-escalation-using-forged-authorization-data-ms14-068-exploit-forged-pac--ms11-013-exploit-silver-pac"></a>Podwyższenie poziomu uprawnień przy użyciu sfałszowanych danych autoryzacji — luka MS14-068 (sfałszowany element PAC) / luka MS11-013 (Silver PAC)


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Znane luki w zabezpieczeniach w starszych wersjach systemu Windows Server umożliwiają osobom atakującym manipulację certyfikatem atrybutu uprawnień (PAC, Privilege Attribute Certificate), polem w bilecie Kerberos, które zawiera dane autoryzacji użytkownika (w usłudze Active Directory jest to członkostwo w grupie), i przyznanie osobie atakującej dodatkowych uprawnień. | Sprawdź, czy na danym komputerze uruchomiono usługę specjalną, która może korzystać z metody autoryzacji innej niż certyfikat PAC. <br></br>**Wyjątki:** w niektórych określonych scenariuszach zasoby implementują własny mechanizm autoryzacji i mogą wyzwalać alert w usłudze ATA. | Upewnij się, że na wszystkich kontrolerach domen z systemami operacyjnymi starszymi niż system Windows Server 2012 R2 zainstalowano poprawkę [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege), a wszystkie serwery członkowskie i kontrolery domen do wersji 2012 R2 mają zainstalowaną poprawkę KB2496930. Aby uzyskać więcej informacji, zobacz [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) i [Forged PAC (Sfałszowany element PAC)](https://technet.microsoft.com/library/security/ms14-068.aspx). | Wysoki     |

## <a name="abnormal-sensitive-group-modification"></a>Nietypowa modyfikacja grupy poufnej


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
|W fazie podwyższenia poziomu uprawnień atakujący modyfikują grupy z wysokim poziomem uprawnień w celu uzyskania dostępu do poufnych zasobów.| Sprawdź, czy zmiana grupy jest uzasadniona. <br></br>**Wyjątki:** ta metoda wykrywania polega na profilowaniu normalnego zachowania użytkowników modyfikujących grupy poufne oraz ostrzeganiu w przypadku zaobserwowania nietypowej zmiany. Uzasadnione zmiany mogą wywołać alert, jeśli dane zachowanie nie zostało wcześniej zaobserwowane przez usługę ATA. Pomocne jest zastosowanie dłuższego okresu uczenia i lepszego pokrycia usługi ATA w domenie. | Upewnij się, że zminimalizowano grupę osób uprawnionych do modyfikowania grup poufnych. Jeśli to możliwe, zastosuj uprawnienia typu „just in time”. | Średni   |

## <a name="encryption-downgrade---skeleton-key-malware"></a>Obniżenie poziomu szyfrowania — złośliwe oprogramowanie Skeleton Key


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Skeleton Key to złośliwe oprogramowanie, które działa na kontrolerach domen i umożliwia uwierzytelnianie w domenie przy użyciu dowolnego konta bez znajomości hasła. To złośliwe oprogramowanie często używa słabszych algorytmów szyfrowania w celu szyfrowania haseł użytkowników na kontrolerze domeny. | Obniżenie poziomu szyfrowania: dowiedz się, dlaczego dane konto korzysta z szyfrowania RC4 protokołu Kerberos po poznaniu szyfrowania AES. <br></br>**Wyjątki:** ta metoda wykrywania opiera się na profilowaniu metod szyfrowania stosowanych w domenie. W niektórych przypadkach stosowana jest słabsza metoda szyfrowania, a usługa ATA wykrywa ją jako nietypową, mimo że jest częścią normalnego (choć rzadkiego) procesu roboczego. | Aby sprawdzić, czy oprogramowanie Skeleton Key istnieje na kontrolerach domen, możesz skorzystać ze [skanera przygotowanego przez zespół usługi ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). | Wysoki |

## <a name="golden-ticket"></a>Sfałszowany bilet uwierzytelniania Golden Ticket


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Jeśli osoba atakująca ma uprawnienia administratora domeny, może utworzyć bilet uprawniający do przyznania biletu (TGT, ticket granting ticket) protokołu Kerberos zapewniający autoryzację do wszystkich zasobów w sieci oraz ustawiający dowolny czas ważności biletu. Pozwala to osobom atakującym na uzyskanie stałego dostępu do sieci. | Obniżenie poziomu szyfrowania: dowiedz się, dlaczego dane konto korzysta z szyfrowania RC4 protokołu Kerberos po poznaniu szyfrowania AES. <br></br>**Wyjątki:** ta metoda wykrywania opiera się na profilowaniu metod szyfrowania używanych w domenie oraz wysyłaniu alertów w przypadku wykrycia nietypowej, słabszej metody. W niektórych przypadkach stosowana jest słabsza metoda szyfrowania, a usługa ATA wykrywa ją jako nietypową, mimo że jest częścią normalnego (choć rzadkiego) procesu roboczego. Taka sytuacja może wystąpić, jeśli dane zachowanie nie zostało wcześniej zaobserwowane przez usługę ATA. Upewnij się, że usługa ATA obejmuje całą domenę. | Zapewnij jak najwyższy poziom bezpieczeństwa biletu uprawniającego do przyznania biletu protokołu Kerberos (KRBTGT, Kerberos Ticket Granting Ticket), stosując następujące metody:<br></br>1.  Zabezpieczenia fizyczne<br></br>2.  Zabezpieczenia fizyczne maszyn wirtualnych<br></br>3. Wzmocnij zabezpieczenia kontrolera domeny<br></br>4.  Izolacja/ochrona poświadczeń urzędu zabezpieczeń lokalnych (LSA, Local Security Authority)<br></br>W przypadku wykrycia sfałszowanych biletów uwierzytelniania Golden Ticket należy przeprowadzić dokładniejsze badania w celu określenia, czy wymagane jest odzyskiwanie taktyczne.<br></br>Regularnie zmieniaj bilet uprawniający do przyznania biletu protokołu Kerberos zgodnie z zaleceniami we wpisie w blogu firmy Microsoft [KRBTGT Account Password Reset Scripts now available for customers (Skrypty resetowania haseł kont KRBTGT dostępne dla klientów)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) przy użyciu narzędzia [Reset the krbtgt account password/keys (Resetowanie kluczy/haseł kont KRBTGT)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). <br></br>Zaimplementuj następujące [zalecenia dotyczące ataków typu Pass-the-Hash](http://aka.ms/PtH). | Średni   |



## <a name="remote-execution"></a>Zdalne wykonywanie kodu


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Osoby atakujące, które przejęły poświadczenia administratora, mogą wykonywać polecenia zdalne na kontrolerze domeny. Umożliwia to stały dostęp do sieci, zbieranie informacji, przeprowadzanie ataków typu „odmowa usługi” (DoS, denial of service) oraz wykonywanie innych działań. | Dowiedz się, czy dane konto ma uprawnienia do wykonywania działań zdalnych w kontrolerze domeny. <br></br>**Wyjątki:** autoryzowani użytkownicy, którzy czasami uruchamiają polecenia na kontrolerze domeny, mogą wywołać ten alert, chociaż jest to część normalnego procesu administracyjnego. Najczęściej sytuacja taka występuje w przypadku członków zespołu IT oraz kont usług, które wykonują zadania administracyjne na kontrolerach domeny. | Ogranicz zdalny dostęp do kontrolerów domen z maszyn nienależących do warstwy 0. Usuń wszystkie podejrzane, nieaktualne i niewymagane pliki oraz foldery. Zaimplementuj silne zasady kontroli konta użytkownika. Zaimplementuj [stacje robocze z dostępem uprzywilejowanym](https://technet.microsoft.com/en-us/windows-server-docs/security/securing-privileged-access/securing-privileged-access), umożliwiając łączenie się z kontrolerami domeny na potrzeby administrowania jedynie maszynom o wzmocnionych zabezpieczeniach. | Niski      |

## <a name="malicious-replication-requests"></a>Złośliwe żądania replikacji


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Replikacja usługi Active Directory to proces, w którym zmiany wprowadzone na jednym kontrolerze domeny są synchronizowane z wszystkimi innymi kontrolerami w domenie lub lesie, które przechowują kopie tych samych danych. W przypadku posiadania odpowiednich uprawnień osoba atakująca może zainicjować żądanie replikacji, tak jakby była kontrolerem domeny. Umożliwia to pobranie danych przechowywanych w usłudze Active Directory, w tym skrótów haseł. | Dowiedz się, dlaczego komputer korzysta z interfejsu API replikacji kontrolera domeny. Ta metoda wykrywania opiera się na korzystaniu przez usługę ATA z partycji konfiguracji lasu katalogu w celu rozpoznania, czy dany komputer jest kontrolerem domeny. <br></br>**Wyjątki:** narzędzie Azure AD DirSync może spowodować wywołanie tego alertu. | Zweryfikuj następujące uprawnienia: — Replikacja zmian katalogów <br></br>— Replikacja wszystkich zmian katalogów<br></br>Aby uzyskać więcej informacji, zobacz [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Przydzielanie uprawnień do usług Active Directory Domain Services dla synchronizacji profili w programie SharePoint Server 2013)](https://technet.microsoft.com/library/hh296982.aspx)<br></br>Aby określić, które osoby w domenie mają te uprawnienia, można wykorzystać [skaner list ACL usługi AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) lub utworzyć skrypt programu PowerShell. | Średni   |



## <a name="broken-trust-between-domain-and-computers"></a>Zerwanie relacji zaufania między domeną i komputerami


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Zerwanie relacji zaufania oznacza, że wymagania dotyczące zabezpieczeń usługi Active Directory mogą nie być aktywne. Taka sytuacja jest często uznawana za podstawowy błąd zabezpieczeń i zgodności oraz atrakcyjny cel dla osób atakujących. Więcej niż 5 kolejnych niepowodzeń uwierzytelniania Kerberos dla konta komputera w przeciągu 24 godzin wywołuje alert w usłudze ATA. Komputer nie komunikuje się z kontrolerem domeny, w związku z czym (1) nie ma dostępu do zaktualizowanych zasad grupy oraz (2) logowanie jest ograniczone do poświadczeń w pamięci podręcznej. | Upewnij się, że relacja zaufania między komputerem i domeną jest poprawna, sprawdzając dzienniki zdarzeń. | Jeśli to konieczne, przyłącz ponownie maszynę do domeny lub zresetuj hasło maszyny. | Niski      |

## <a name="massive-object-deletion"></a>Usunięcie dużej liczby obiektów


> [!div class="mx-tableFixed"]
|Opis|Badanie|Zalecenie|Ważność|
|------|----|------|----------|
| Usługa ATA zgłasza ten alert w przypadku usunięcia więcej niż 5% wszystkich kont. Wymaga to dostępu do odczytu do kontenera usuniętego elementu. | Dowiedz się, dlaczego nagle usunięto 5% wszystkich kont. | Usuń uprawnienia użytkowników, którzy mogą usuwać konta w usłudze Active Directory. Aby uzyskać więcej informacji, zobacz [View or Set Permissions on a Directory Object (Wyświetlanie i ustawianie uprawnień obiektu katalogu)](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx). | Niski |

## <a name="see-also"></a>Zobacz też
- [Praca z podejrzanymi działaniami](working-with-suspicious-activities.md)
- [Badanie ataków z użyciem sfałszowanego certyfikatu PAC](use-case-forged-pac.md)
- [Rozwiązywanie znanych błędów usługi ATA](troubleshooting-ata-known-errors.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
