---
title: "Odzyskiwanie po awarii w usłudze Advanced Threat Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można szybko odzyskać funkcjonalność usługi ATA po awarii"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3f763f7c1cce6c451a1cc969771b73543c76673
ms.openlocfilehash: 0669ccb78207dde1ede06a229af896bed0b19d28


---

*Dotyczy: Advanced Threat Analytics, wersja 1.7*



# <a name="ata-disaster-recovery"></a>Odzyskiwanie usługi ATA po awarii
W tym artykule opisano sposób szybkiego odzyskiwania centrum usługi ATA i przywracania funkcjonalności usługi ATA, w przypadku gdy funkcje centrum usługi ATA zostały utracone, ale nadal działają bramy usługi ATA. 

>[!NOTE]
> Przedstawiony proces nie prowadzi do odzyskania wcześniej wykrytych podejrzanych działań, ale przywraca pełną funkcjonalność centrum usługi ATA. Ponadto okres nauki wymagany dla niektórych wykryć behawioralnych będzie liczony od początku, ale większość wykryć oferowanych w usłudze ATA będzie działać po przywróceniu centrum usługi ATA. 

## <a name="how-to-recover-your-ata-center-after-a-disaster"></a>Jak odzyskać centrum usługi ATA po awarii

1. Konfiguracja centrum usługi ATA jest zapisywana do pliku co godzinę. Znajdź najnowszą kopię zapasową konfiguracji centrum usługi ATA i zapisz ją na innym komputerze. Pełne wyjaśnienie sposobu lokalizowania tych plików można znaleźć w artykule [Eksportowanie i importowanie konfiguracji usługi ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Wyeksportuj certyfikat centrum usługi ATA.
    1. W Menedżerze certyfikatów przejdź do opcji **Certyfikaty (komputer lokalny)** -> **Osobiste** ->**Certyfikaty** i wybierz pozycję **Centrum usługi ATA**.
    2. Kliknij prawym przyciskiem myszy pozycję **Centrum usługi ATA** i wybierz opcję **Wszystkie zadania**, a następuje **Eksportuj**. 
     ![Certyfikat centrum usługi ATA](media/ata-center-cert.png)
    3. Postępuj zgodnie z instrukcjami, aby wyeksportować certyfikat wraz z kluczem prywatnym.

    > [!NOTE] 
    > Jeśli nie można wyeksportować klucza prywatnego, należy utworzyć nowy certyfikat i wdrożyć go w usłudze ATA, zgodnie z opisem w artykule [Zmienianie certyfikatu centrum usługi ATA](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert), a następnie wyeksportować go. 

    4. Utwórz kopię zapasową pliku wyeksportowanego pliku certyfikatu na innym komputerze.
3. Utwórz nową maszynę systemu Windows Server przy użyciu tej samej nazwy komputera i adresu IP, które były użyte dla poprzedniej maszyny centrum usługi ATA.
4. Zaimportuj certyfikat, którego kopię zapasową wykonano w kroku 2, do nowego serwera.
5. Postępuj zgodnie z instrukcjami, aby [wdrożyć centrum usługi ATA](/advanced-threat-analytics/deploy-use/install-ata-step1) na nowo utworzonej maszynie systemu Windows Server. Nie ma potrzeby ponownego wdrażania bram usługi ATA. Gdy zostanie wyświetlony monit o certyfikat, podaj certyfikat z kroku 2. 
![Przywracanie centrum usługi ATA](media/ata-center-restore.png)
6. Zaimportuj kopię konfiguracji centrum usługi ATA:
    1. Usuń dokument domyślnego profilu systemu centrum usługi ATA z bazy danych MongoDB: 
        1. Przejdź do lokalizacji **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Uruchom polecenie `mongo.exe` 
        3. Uruchom następujące polecenie, aby usunąć domyślny profil systemu: `db.SystemProfile.remove({})`
    2. Uruchom polecenie: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`, używając pliku kopii zapasowej z kroku 1.</br>
    Pełne wyjaśnienie sposobu lokalizowania i importowania plików kopii zapasowej można znaleźć w artykule [Eksportowanie i importowanie konfiguracji usługi ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Po zaimportowaniu uruchom to polecenie, aby usunąć niektóre z domyślnych detektorów i profilerów (aby je zresetować dla nowego środowiska):`db.SystemProfile.remove({$or:[{"_t":"DetectorProfile"}, "_t":"DirectoryServicesSystemProfile"}]}) `
    4. Otwórz konsolę usługi ATA. Wszystkie połączone bramy usługi ATA powinny być widoczne na karcie Konfiguracja/Bramy. 
    5. Upewnij się, że został zdefiniowany **Użytkownik usług katalogu** i wybrany **Synchronizator kontrolera domeny**. 






## <a name="see-also"></a>Zobacz też
- [Wymagania wstępne usługi ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planowanie pojemności usługi ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurowanie zbierania zdarzeń](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurowanie funkcji przekazywania zdarzeń systemu Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Forum usługi ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO3-->


