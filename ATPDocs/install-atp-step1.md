---
title: Zainstaluj usługi Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Pierwszym krokiem do zainstalowania narzędzia Azure ATP obejmuje utworzenie wystąpienia dla danego wdrożenia usługi Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 97cce3de3a1cbe049523c54901ecbc9228aaee53
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783019"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*


# <a name="creating-your-azure-atp-instance-in-the-portal---step-1"></a>Tworzenie wystąpienia usługi Azure ATP w portalu — krok 1

> [!div class="step-by-step"]
> [Krok 2 »](install-atp-step2.md)

Ta procedura instalacji zawiera instrukcje dotyczące tworzenia i zarządzania nimi z wystąpienia usługi Azure ATP lub obszaru roboczego. Aby uzyskać informacje dotyczące architektury usługi Azure ATP, zobacz [architektury usługi Azure ATP](atp-architecture.md).

W przypadku narzędzia Azure ATP będziesz mieć jedno wystąpienie lub obszaru roboczego, dzięki któremu można zarządzać wieloma lasami z jedną taflę szkła. 

> [!NOTE]
> Obecnie narzędzia Azure ATP centra danych są wdrażane w Europie oraz Azja i Ameryka Ameryka Północna/środkowa/Karaiby.

## <a name="step-1-enter-the-azure-atp-portal"></a>Krok 1. Wprowadź portalu usługi Azure ATP

Po upewnieniu się, że sieć spełnia wymagania czujnika, możesz kontynuować tworzenie obszaru roboczego usługi Azure ATP.

> [!NOTE]
>Aby uzyskać dostęp do portalu zarządzania, musisz być administratorem globalnym lub administratorem zabezpieczeń tej dzierżawy.


1.  Wprowadź [portalu usługi Azure ATP](https://portal.atp.azure.com).

2.  Zaloguj się przy użyciu konta użytkownika usługi Azure Active Directory.

## <a name="step-2-create-your-workspace"></a>Krok 2. Tworzenie obszaru roboczego

1. Kliknij przycisk **Utwórz obszar roboczy**.

2. W **Utwórz nowy obszar roboczy** okno dialogowe, nazwij obszar roboczy, a następnie wybierz pozycję **Geolokalizacja** dla centrum danych. Twój obszar roboczy jest **głównej** domyślnie. 
 > [!NOTE]
 > Po wybraniu Geolokalizacji, nie można go modyfikować.
    ![Usługa Azure ATP obszaru roboczego](media/create-workspace.png)

3. Możesz kliknąć pozycję **role użytkownika usługi Azure ATP zarządzanie** link bezpośredni dostęp [Centrum administracyjne usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) i zarządzanie grupami roli.

 > [!NOTE]
 > Pomyślnie zalogować się do usługi Azure ATP, musisz zalogować się jako użytkownik, który został przypisany do właściwej roli usługi Azure ATP dostęp do portalu usługi Azure ATP. Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) w usłudze Azure ATP zobacz [Praca z grupami ról usługi Azure ATP](atp-role-groups.md).

4. Kliknij nazwę obszaru roboczego, aby uzyskać dostęp do portalu usługi Azure ATP.

    ![Usługa Azure ATP obszarów roboczych.](media/atp-workspaces.png)

- Można edytować tylko podstawowy obszar roboczy. Jeśli chcesz usunąć podstawowego obszaru roboczego, należy najpierw wyłączyć integracje będzie on mógł zostać usunięty.

- Przechowywanie danych — wcześniej usuniętych obszarów roboczych nie są wyświetlane w interfejsie użytkownika. Aby uzyskać więcej informacji na temat przechowywania danych usługi Azure ATP, zobacz [Azure zaawansowanej ochrony przed zagrożeniami bezpieczeństwa danych i prywatności](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Przed rozpoczęciem instalacji](atp-prerequisites.md)
[Krok 2 »](install-atp-step2.md)



## <a name="see-also"></a>Zobacz też
- [Narzędzia do określania rozmiaru usługi Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurowanie zbierania zdarzeń](configure-event-collection.md)
- [Wymagania wstępne Zaawansowanej ochrony przed zagrożeniami na platformie Azure](atp-prerequisites.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
