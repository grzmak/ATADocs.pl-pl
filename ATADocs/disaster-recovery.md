---
title: Odzyskiwanie po awarii w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak można szybko odzyskać funkcjonalność usługi ATA po awarii
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 72598380f574e0475e4796887f44131009911be2
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009557"
---
*Dotyczy: Advanced Threat Analytics wersji 1.9*



# <a name="ata-disaster-recovery"></a>Odzyskiwanie usługi ATA po awarii
W tym artykule opisano sposób szybkiego odzyskiwania centrum usługi ATA i przywracania funkcjonalności usługi ATA, w przypadku gdy funkcje centrum usługi ATA zostały utracone, ale nadal działają bramy usługi ATA. 

>[!NOTE]
> Przedstawiony proces nie prowadzi do odzyskania wcześniej wykrytych podejrzanych działań, ale przywraca pełną funkcjonalność centrum usługi ATA. Ponadto okres nauki wymagany dla niektórych wykryć behawioralnych będzie liczony od początku, ale większość wykryć oferowanych w usłudze ATA będzie działać po przywróceniu centrum usługi ATA. 

## <a name="back-up-your-ata-center-configuration"></a>Tworzenie kopii zapasowej konfiguracji centrum usługi ATA

1. Konfiguracja centrum usługi ATA jest zapisywana do pliku co godzinę. Znajdź najnowszą kopię zapasową konfiguracji centrum usługi ATA i zapisz ją na innym komputerze. Pełne wyjaśnienie sposobu lokalizowania tych plików można znaleźć w artykule [Eksportowanie i importowanie konfiguracji usługi ATA](ata-configuration-file.md). 
2. Wyeksportuj certyfikat centrum usługi ATA.
    1. W Menedżerze certyfikatów przejdź do opcji **Certyfikaty (komputer lokalny)** -> **Osobiste** ->**Certyfikaty** i wybierz pozycję **Centrum usługi ATA**.
    2. Kliknij prawym przyciskiem myszy **Centrum usługi ATA** i wybierz **wszystkie zadania** następuje **wyeksportować**. 
     ![Certyfikat centrum usługi ATA](media/ata-center-cert.png)
    3. Postępuj zgodnie z instrukcjami, aby wyeksportować certyfikat wraz z kluczem prywatnym.
    4. Utwórz kopię zapasową pliku wyeksportowanego pliku certyfikatu na innym komputerze.

  > [!NOTE] 
  > Jeśli nie można wyeksportować klucza prywatnego, należy utworzyć nowy certyfikat i wdrożyć go w usłudze ATA, zgodnie z opisem w artykule [Zmienianie certyfikatu centrum usługi ATA](modifying-ata-center-configuration.md), a następnie wyeksportować go. 

## <a name="recover-your-ata-center"></a>Odzyskiwanie centrum usługi ATA

1. Utwórz nową maszynę systemu Windows Server przy użyciu tej samej nazwy komputera i adresu IP, które były użyte dla poprzedniej maszyny centrum usługi ATA.
2. Importuj certyfikat, którego kopia zapasowa została utworzona wcześniej, do nowego serwera.
3. Postępuj zgodnie z instrukcjami, aby [wdrożyć centrum usługi ATA](install-ata-step1.md) na nowo utworzonej maszynie systemu Windows Server. Nie ma potrzeby ponownego wdrażania bram usługi ATA. Po wyświetleniu monitu o certyfikat przedstaw certyfikat wyeksportowany podczas tworzenia kopii zapasowej konfiguracji centrum usługi ATA. 
![Przywracanie centrum usługi ATA](media/disaster-recovery-deploymentss.png)
4. Zatrzymaj usługę Centrum usługi ATA.
5. Importowanie konfiguracji kopii zapasowej Centrum usługi ATA:
    1. Usuń dokument domyślnego profilu systemu centrum usługi ATA z bazy danych MongoDB: 
        1. Przejdź do lokalizacji **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Uruchom `mongo.exe ATA` 
        3. Uruchom usługę Centrum usługi ATA.
        4. Uruchom następujące polecenie, aby usunąć domyślny profil systemu: `db.SystemProfile.remove({})`
    2. Uruchom polecenie: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`, używając pliku kopii zapasowej z kroku 1.</br>
    Pełne wyjaśnienie sposobu lokalizowania i importowania plików kopii zapasowej można znaleźć w artykule [Eksportowanie i importowanie konfiguracji usługi ATA](ata-configuration-file.md). 
    3. Otwórz konsolę usługi ATA. Wszystkie połączone bramy usługi ATA powinny być widoczne na karcie Konfiguracja/Bramy. 
    4. Upewnij się, że został zdefiniowany [**Użytkownik usług katalogu**](install-ata-step2.md) i wybrany [**Synchronizator kontrolera domeny**](install-ata-step5.md). 






## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](ata-prerequisites.md)
- [Planowanie pojemności usługi ATA](ata-capacity-planning.md)
- [Konfigurowanie zbierania zdarzeń](install-ata-step6.md)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](configure-event-collection.md)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
