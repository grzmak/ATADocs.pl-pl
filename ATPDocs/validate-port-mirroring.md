---
title: Weryfikowanie funkcji dublowania portów w usłudze Azure Advanced Threat Protection | Dokumentacja firmy Microsoft
description: Opisuje sposób sprawdzić, czy funkcja dublowania portów jest poprawnie skonfigurowana w usłudze Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.service: ''
ms.technology: ''
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0d9e2bcbbe2635765f1bcce9ee1367c1d3895080
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783444"
---
*Dotyczy: Azure Zaawansowana ochrona przed zagrożeniami*



# <a name="validate-port-mirroring"></a>Weryfikowanie funkcji dublowania portów
> [!NOTE] 
> Ten artykuł dotyczy tylko w przypadku wdrożenia wdrażanie czujnik autonomiczny zaawansowanej ochrony przed zagrożeniami Azure zamiast czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure. Aby określić, jeśli musisz użyć czujnika zaawansowanej ochrony przed zagrożeniami w usłudze Azure, zobacz [czujnika odpowiednie dla danego wdrożenia wybór](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
W poniższych krokach objaśniono proces weryfikowania, czy funkcja dublowania portów jest poprawnie skonfigurowana. Dla usługi Azure ATP działało poprawnie czujnik autonomiczny narzędzia Azure ATP musi umożliwiać ruch do i z kontrolera domeny. Główne źródło danych używane przez usługi Azure ATP to głęboka inspekcja pakietów ruchu sieciowego do i z kontrolerów domeny. Dla usługi Azure ATP się ruchu sieciowego funkcję dublowania portów należy skonfigurować. Funkcja dublowania portów kopiuje ruch z jednego portu (portu źródłowego) do innego portu (portu docelowego).

## <a name="validate-port-mirroring-using-net-mon"></a>Weryfikowanie funkcji dublowania portów za pomocą monitora sieci
1.  Zainstaluj [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) na czujnik autonomiczny zaawansowanej ochrony przed zagrożeniami, chcesz zweryfikować.

    > [!IMPORTANT]
    > Jeśli zdecydujesz się zainstalować program Wireshark celu weryfikowanie funkcji dublowania portów, należy ponownie uruchomić usługi czujnika autonomicznego narzędzia Azure ATP po weryfikacji.

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
    

5.  Jeśli widoczny ruch tylko w jednym kierunku, Współpracuj z zespołom sieci lub wirtualizacji, aby ułatwić rozwiązywanie problemów z konfiguracją funkcji dublowania portów.

## <a name="see-also"></a>Zobacz też

- [Konfigurowanie składnika przesyłanie dalej zdarzeń](configure-event-forwarding.md)
- [Konfigurowanie funkcji dublowania portów](configure-port-mirroring.md)
- [Skorzystaj z forum usługi Azure ATP](https://aka.ms/azureatpcommunity)
