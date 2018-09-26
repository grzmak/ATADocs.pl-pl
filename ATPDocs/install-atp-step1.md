---
title: Install Azure Zaawansowana ochrona przed zagrożeniami — krok 1 | Dokumentacja firmy Microsoft
description: Pierwszym krokiem do zainstalowania narzędzia Azure ATP obejmuje utworzenie wystąpienia dla danego wdrożenia usługi Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6874c8a23372950dacdf328b1e885b7d039c8433
ms.sourcegitcommit: 5ff50807f855db1051b977a64eb6e90487ea196c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750507"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Tworzenie obszaru roboczego w portalu zarządzania obszarami roboczymi usługi Azure ATP — krok 1

>[!div class="step-by-step"]
[Krok 2 »](install-atp-step2.md)

Ta procedura instalacji zawiera instrukcje dotyczące tworzenia i zarządzania nimi swojego wystąpienia usługi Azure ATP. Aby uzyskać informacje dotyczące architektury usługi Azure ATP, zobacz [architektury usługi Azure ATP](atp-architecture.md).

W przypadku narzędzia Azure ATP będziesz mieć jeden obszar roboczy lub wystąpienie, aby umożliwić zarządzanie wielu lasów z jedną taflę szkła. 

> [!NOTE]
> Obecnie narzędzia Azure ATP centra danych są wdrażane w Europie oraz Azja i Ameryka Ameryka Północna/środkowa/Karaiby.

## <a name="step-1-enter-the-management-portal"></a>Krok 1. Wprowadź w portalu zarządzania

Po upewnieniu się, że sieć spełnia wymagania czujnika, możesz kontynuować tworzenie obszaru roboczego usługi Azure ATP.

> [!NOTE]
>Aby uzyskać dostęp do portalu zarządzania, musisz być administratorem globalnym lub administratorem zabezpieczeń tej dzierżawy.


1.  Wprowadź [portalu usługi Azure ATP](https://portal.atp.azure.com).

2.  Zaloguj się przy użyciu konta użytkownika usługi Azure Active Directory.

## <a name="step-2-create-your-workspace"></a>Krok 2. Tworzenie obszaru roboczego

1. Kliknij przycisk **Utwórz obszar roboczy**.

2. W **Utwórz nowy obszar roboczy** okno dialogowe, nazwij obszar roboczy, a następnie wybierz pozycję **Geolokalizacja** dla centrum danych. Jeden obszar roboczy można ustawić jako podstawowy. Ustawienia obszaru roboczego, ponieważ podstawowy ma wpływ na integracji — narzędzia Azure ATP można tylko zintegrować z usługą Windows Defender ATP, aby podstawowego obszaru roboczego. Można zmienić, który obszar roboczy jest podstawową później, ale aby można było zrobić, należy usunąć wszystkie integracje skonfigurowane dla bieżącego podstawowym obszarem roboczym.
 > [!NOTE]
 > Po wybraniu Geolokalizacji, nie można go modyfikować.
    ![Usługa Azure ATP obszaru roboczego](media/create-workspace.png)

3. Możesz kliknąć pozycję **role użytkownika usługi Azure ATP zarządzanie** link bezpośredni dostęp [Centrum administracyjne usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) i zarządzanie grupami roli.

 > [!NOTE]
 > Pomyślnie zalogować się do usługi Azure ATP, musisz zalogować się jako użytkownik, który został przypisany do właściwej roli usługi Azure ATP dostęp do portalu obszaru roboczego usługi Azure ATP. Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) w usłudze Azure ATP zobacz [Praca z grupami ról usługi Azure ATP](atp-role-groups.md).

4. Kliknij nazwę nowego obszaru roboczego do korzystania z portalu obszaru roboczego usługi Azure ATP dla danego obszaru roboczego.

    ![Usługa Azure ATP obszarów roboczych.](media/atp-workspaces.png)

- Można edytować tylko podstawowy obszar roboczy. Jeśli chcesz usunąć podstawowym obszarem roboczym, najpierw należy wyłączyć integracje i ustaw obszar roboczy, aby nie może być **głównej** będzie on mógł zostać usunięty.
- Edytowanie podstawowego obszaru roboczego, należy wyłączyć integracje istniejących w obszarze roboczym.

- Przechowywanie danych — usunięto obszarów roboczych nie są wyświetlane w interfejsie użytkownika. Aby uzyskać więcej informacji na temat przechowywania danych usługi Azure ATP, zobacz [Azure zaawansowanej ochrony przed zagrożeniami bezpieczeństwa danych i prywatności](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Przed rozpoczęciem instalacji](configure-port-mirroring.md)
[Krok 2 »](install-atp-step2.md)


## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum zaawansowanej ochrony przed zagrożeniami](https://aka.ms/azureatpcommunity)
