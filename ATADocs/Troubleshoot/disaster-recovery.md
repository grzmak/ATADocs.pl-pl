---
title: "Odzyskiwanie po awarii w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można szybko odzyskać funkcjonalność usługi ATA po awarii"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: e315e9731fa9715c3b41b9292349ee5aca13fbce
ms.sourcegitcommit: 4f5927f30089655e3984d69623ea4439b7c36845
translationtype: HT
---
*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="ata-disaster-recovery"></a>Odzyskiwanie usługi ATA po awarii
W tym artykule opisano sposób szybkiego odzyskiwania centrum usługi ATA i przywracania funkcjonalności usługi ATA, w przypadku gdy funkcje centrum usługi ATA zostały utracone, ale nadal działają bramy usługi ATA. 

>[!NOTE]
> Przedstawiony proces nie prowadzi do odzyskania wcześniej wykrytych podejrzanych działań, ale przywraca pełną funkcjonalność centrum usługi ATA. Ponadto okres nauki wymagany dla niektórych wykryć behawioralnych będzie liczony od początku, ale większość wykryć oferowanych w usłudze ATA będzie działać po przywróceniu centrum usługi ATA. 

## <a name="back-up-your-ata-center-configuration"></a>Tworzenie kopii zapasowej konfiguracji centrum usługi ATA

1. Konfiguracja centrum usługi ATA jest zapisywana do pliku co godzinę. Znajdź najnowszą kopię zapasową konfiguracji centrum usługi ATA i zapisz ją na innym komputerze. Pełne wyjaśnienie sposobu lokalizowania tych plików można znaleźć w artykule [Eksportowanie i importowanie konfiguracji usługi ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Wyeksportuj certyfikat centrum usługi ATA.
    1. W Menedżerze certyfikatów (`certlm.msc`) przejdź do opcji **Certyfikaty (komputer lokalny)** -> **Osobiste** ->**Certyfikaty** i wybierz pozycję **Centrum usługi ATA**.
    2. Kliknij prawym przyciskiem myszy pozycję **Centrum usługi ATA** i wybierz opcję **Wszystkie zadania**, a następuje **Eksportuj**. 
     ![Certyfikat centrum usługi ATA](media/ata-center-cert.png)
    3. Postępuj zgodnie z instrukcjami, aby wyeksportować certyfikat wraz z kluczem prywatnym.
    4. Utwórz kopię zapasową pliku wyeksportowanego pliku certyfikatu na innym komputerze.

  > [!NOTE] 
  > Jeśli nie można wyeksportować klucza prywatnego, należy utworzyć nowy certyfikat i wdrożyć go w usłudze ATA, zgodnie z opisem w artykule [Zmienianie certyfikatu centrum usługi ATA](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert), a następnie wyeksportować go. 

## <a name="recover-your-ata-center"></a>Odzyskiwanie centrum usługi ATA

1. Utwórz nową maszynę systemu Windows Server przy użyciu tej samej nazwy komputera i adresu IP, które były użyte dla poprzedniej maszyny centrum usługi ATA.
4. Zaimportuj certyfikat, którego kopię zapasową wykonano w kroku powyżej, do nowego serwera.
5. Postępuj zgodnie z instrukcjami, aby [wdrożyć centrum usługi ATA](/advanced-threat-analytics/deploy-use/install-ata-step1) na nowo utworzonej maszynie systemu Windows Server. Pamiętaj, aby wybrać ten sam adres IP i port co w przypadku starego centrum. Nie ma potrzeby ponownego wdrażania bram usługi ATA. Po wyświetleniu monitu o certyfikat przedstaw certyfikat wyeksportowany podczas tworzenia kopii zapasowej konfiguracji centrum usługi ATA. 
![Przywracanie centrum usługi ATA](media/ata-center-restore.png)
6. Zaimportuj kopię konfiguracji centrum usługi ATA:
    1. Usuń dokument domyślnego profilu systemu centrum usługi ATA z bazy danych MongoDB: 
        1. Przejdź do lokalizacji **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Uruchom polecenie `mongo.exe ATA` 
        3. Uruchom następujące polecenie, aby usunąć domyślny profil systemu: `db.SystemProfile.remove({})`
    2. Uruchom polecenie: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`, używając pliku kopii zapasowej z kroku 1.</br>
    Pełne wyjaśnienie sposobu lokalizowania i importowania plików kopii zapasowej można znaleźć w artykule [Eksportowanie i importowanie konfiguracji usługi ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Po zaimportowaniu uruchom to polecenie, aby usunąć niektóre z domyślnych profilów systemu (aby je zresetować na potrzeby nowego środowiska): `db.SystemProfile.remove({$or:[{"_t":"DetectorProfile"}, "_t":"DirectoryServicesSystemProfile"}]}) `
    4. Otwórz konsolę usługi ATA. Wszystkie połączone bramy usługi ATA powinny być widoczne na karcie Konfiguracja/Bramy. 
    5. Upewnij się, że został zdefiniowany [**Użytkownik usług katalogu**](/advanced-threat-analytics/deploy-use/install-ata-step2) i wybrany [**Synchronizator kontrolera domeny**](/advanced-threat-analytics/deploy-use/install-ata-step5). 






## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
