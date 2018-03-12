---
title: "Azure instalacji Advanced Threat Protection — krok 1 | Dokumentacja firmy Microsoft"
description: "Pierwszy krok w celu zainstalowania Azure ATP obejmuje tworzenie obszaru roboczego dla danego wdrożenia Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5eabf4fc3965e8745b7e2c0fbae4973deb358814
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2018
---
*Dotyczy: Azure Advanced Threat Protection*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Tworzenie obszaru roboczego w portalu zarządzania Azure ATP roboczym — krok 1

>[!div class="step-by-step"]
[Krok 2 »](install-atp-step2.md)

Ta procedura instalacji zawiera instrukcje dotyczące tworzenia i zarządzania obszaru roboczego w portalu zarządzania Azure ATP obszaru roboczego. Aby uzyskać informacje dotyczące architektury Azure ATP, zobacz [architektura Azure ATP](atp-architecture.md).

ATP Azure masz możliwość zarządzania i monitorowania wiele obszarów roboczych. Jest to szczególnie przydatne, jeśli chcesz utworzyć pokaz obszar roboczy oraz obszaru roboczego testu, który umożliwia ATP Azure fazy weryfikacji Koncepcji przed udostępnieniem jej do całej organizacji. Jest to również wymagane do obsługi wdrożeń z wieloma lasami. Jednego obszaru roboczego można monitorować tylko wielu domen pochodzących z jednego lasu. 

> [!NOTE]
> Może mieć co najwyżej dwa active obszarów roboczych. Po usunięciu obszaru roboczego można się z pomocą techniczną, aby uaktywnić go ponownie. Możesz mieć mazimum trzy usunięto obszarów roboczych. Aby zwiększyć liczbę zapisanych, usunięto obszary robocze, skontaktuj się z obsługą Azure ATP.

## <a name="step-1-enter-the-workspace-management-portal"></a>Krok 1. Przejście do portalu zarządzania obszaru roboczego

Po upewnieniu się, że sieć spełnia wymagania czujnika, można przystąpić do tworzenia obszaru roboczego Azure ATP.

> [!NOTE]
>Aby uzyskać dostęp do portalu zarządzania obszaru roboczego, musisz być administratorem globalnym lub administratorem zabezpieczeń na tę dzierżawę.


1.  Wprowadź [portalu obszaru roboczego Azure ATP](https://portal.atp.azure.com).

2.  Zaloguj się przy użyciu swojego konta użytkownika usługi Azure Active Directory lokalnego ma co najmniej dostęp do odczytu wszystkich obiektów w monitorowanej domeny.

## <a name="step-2-create-a-workspace"></a>Krok 2. Tworzenie obszaru roboczego

1. Kliknij przycisk **Utwórz obszar roboczy**.

2. W **Utwórz nowy obszar roboczy** okna dialogowego, nazwa obszaru roboczego, zdecydować, czy z podstawowym obszarem roboczym lub nie, a następnie wybierz **Geolokalizacja** dla centrum danych. Tylko jeden obszar roboczy, może być ustawiony jako podstawowy. Ustawienia obszaru roboczego, ponieważ podstawowy ma wpływ na integracji — Azure ATP można tylko zintegrować z Windows Defender ATP obszaru roboczego podstawowego. Można zmienić, które obszaru roboczego jest podstawowym później, ale aby zrobić, należy usunąć wszystkie integracji został już ustawiony dla podstawowym obszarem roboczym.
 > [!NOTE]
 > Po wybraniu używanie funkcji Geolokalizacji, nie można go modyfikować.
    ![Azure ATP obszaru roboczego](media/create-workspace.png)

3. Możesz kliknąć **ról użytkownika zarządzania ATP Azure** link bezpośredni dostęp do [Centrum administracyjnego usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) i zarządzanie grupami roli.

 > [!NOTE]
 > Pomyślnie zalogować się do usługi Azure ATP, należy zalogować się użytkownik, który został przypisany do roli Azure ATP właściwy dostęp do portalu Azure ATP obszaru roboczego. Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) w Azure ATP, zobacz [Praca z grupami roli Azure ATP](atp-role-groups.md).

4. Kliknij nazwę nowego obszaru roboczego dostępu portalu Azure ATP obszaru roboczego dla tego obszaru roboczego.

    ![Azure ATP obszary robocze](media/atp-workspaces.png)

- Można edytować tylko podstawowym obszarem roboczym. Aby wprowadzić zmiany dotyczące innych obszarów roboczych, można je usunąć i dodać je ponownie. Jeśli chcesz usunąć podstawowym obszarem roboczym, najpierw musisz wyłączyć integracji i ustaw obszar roboczy, aby nie może być **głównej** będzie on mógł zostać usunięty.
- Edytuj podstawowym obszarem roboczym, możesz wyłączyć integracji istniejących w obszarze roboczym.

- Przechowywanie danych — usunięto obszary robocze nie są wyświetlane w Interfejsie użytkownika, jednak ich dane są przechowywane zgodnie z [zasady przechowywania danych firmy Microsoft](https://www.microsoft.com/trustcenter/privacy/you-own-your-data).


>[!div class="step-by-step"]
[« Przed rozpoczęciem instalacji](configure-port-mirroring.md)
[Krok 2 »](install-atp-step2.md)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
