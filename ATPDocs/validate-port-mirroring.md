---
title: "Weryfikowanie funkcji dublowania portów w Azure Advanced Threat Protection | Dokumentacja firmy Microsoft"
description: "Opis sposobu weryfikacji, czy funkcja dublowania portów jest prawidłowo skonfigurowane w Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7628fa491ddbe477cab7eb414409028c0f94f44d
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
*Dotyczy: Azure Advanced Threat Protection*



# <a name="validate-port-mirroring"></a>Weryfikowanie funkcji dublowania portów
> [!NOTE] 
> Ten artykuł dotyczy tylko w przypadku wdrożenia wdrażanie czujnik autonomiczny ATP Azure zamiast czujnik ATP Azure. Aby określić, czy należy użyć czujnik ATP Azure, zobacz [Wybieranie prawo czujnik wdrożenia](atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment).
 
W poniższych krokach objaśniono proces weryfikowania, czy funkcja dublowania portów jest poprawnie skonfigurowana. Dla usługi Azure ATP działało poprawnie czujnik autonomiczny Azure ATP musi mieć możliwość widoczny ruch do i z kontrolera domeny. Główne źródło danych używane przez Azure ATP to głęboka inspekcja pakietów ruchu sieciowego do i z kontrolerów domeny. Dla ATP Azure zobaczyć ruchu sieciowego funkcję dublowania portów należy skonfigurować. Funkcja dublowania portów kopiuje ruch z jednego portu (portu źródłowego) do innego portu (portu docelowego).

## <a name="validate-port-mirroring-using-net-mon"></a>Weryfikowanie funkcji dublowania portów za pomocą monitora sieci
1.  Zainstaluj [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) na ATP czujnika autonomiczny, który chcesz zweryfikować.

    > [!IMPORTANT]
    > Jeśli zamierzasz zainstalować Wireshark celu weryfikowanie funkcji dublowania portów, uruchom ponownie usługę Azure ATP autonomiczny czujnik, po weryfikacji.

2.  Otwórz program Network Monitor i utwórz nową kartę przechwytywania.

    1.  Wybierz tylko kartę sieciową **przechwytywania** lub kartę sieciową połączoną z portem przełącznika, który został skonfigurowany jako miejsce docelowe funkcji dublowania portów.

    2.  Upewnij się, że tryb P-Mode jest włączony.

    3.  Kliknij pozycję **Nowe przechwytywanie**.

        ![Obraz przedstawiający tworzenie nowej karty przechwytywania](media/atp-port-mirroring-capture.png)

3.  W oknie filtru wyświetlania wprowadź następujący filtr: **KerberosV5 LUB LDAP**, a następnie kliknij pozycję **Zastosuj**.

    ![Obraz przedstawiający stosowanie filtru KerberosV5 lub LDAP](media/atp-port-mirroring-filter-settings.png)

4.  Kliknij pozycję **Uruchom**, aby rozpocząć sesję przechwytywania. Jeśli ruch do i z kontrolera domeny nie jest widoczny, sprawdź konfigurację funkcji dublowania portów.

    ![Obraz przedstawiający uruchamianie sesji przechwytywania](media/atp-port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Upewnij się, że jest widoczny ruch zarówno do, jak i z kontrolerów domeny.
    

5.  Jeśli jest widoczny ruch tylko w jednym kierunku, współpracować z zespołów sieci lub wirtualizacji, aby ułatwić rozwiązywanie problemów z konfiguracją funkcji dublowania portów.

## <a name="see-also"></a>Zobacz też

- [Konfigurowanie funkcji przekazywania zdarzeń](configure-event-forwarding.md)
- [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md)
- [Zapoznaj się z forum ATP!](https://aka.ms/azureatpcommunity)
