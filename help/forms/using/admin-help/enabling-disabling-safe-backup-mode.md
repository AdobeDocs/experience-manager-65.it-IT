---
title: Abilitazione e disabilitazione della modalità backup sicuro
description: Nella pagina Impostazioni di backup è possibile utilizzare AEM Forms in modalità di backup sicura in modo da poter eseguire il backup affidabile del database e della directory GDS (Global Document Storage). Scopri come abilitare e disabilitare la modalità di backup sicuro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 11%
---
# Abilitazione e disabilitazione della modalità backup sicuro {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Nella pagina Impostazioni di backup è possibile utilizzare AEM Forms in modalità di backup sicura in modo da poter eseguire il backup affidabile del database e della directory GDS (Global Document Storage).

AEM Forms è in modalità di backup sicura ma funziona normalmente, tranne per il fatto che non rimuove attivamente i file dalla directory GDS.

>[!NOTE]
>
>L&#39;impostazione di questa opzione non esegue il backup del sistema, ma prepara il sistema per il backup.

## Abilita modalità di backup sicura {#enable-safe-backup-mode}

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistemi core > Impostazioni di backup.
1. Nella pagina Impostazioni di backup, selezionare Esegui in modalità di backup sicuro e fare clic su OK.

>[!NOTE]
>
>Se il sistema è già in esecuzione in modalità di backup sicuro, non verrà creata una nuova prenotazione quando si fa clic su OK.

## Disattiva modalità di backup sicuro {#disable-safe-backup-mode}

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistemi core > Impostazioni di backup.
1. Nella pagina Impostazioni di backup deselezionare Esegui in modalità di backup sicuro e fare clic su OK.
