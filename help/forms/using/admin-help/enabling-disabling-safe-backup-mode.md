---
title: Attivazione e disattivazione della modalità di backup sicuro
description: Nella pagina Impostazioni di backup è possibile utilizzare i moduli AEM in modalità di backup sicura in modo da poter eseguire il backup affidabile del database e della directory GDS (Global Document Storage). Scopri come abilitare e disabilitare la modalità di backup sicuro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Attivazione e disattivazione della modalità di backup sicuro {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Nella pagina Impostazioni di backup è possibile utilizzare i moduli AEM in modalità di backup sicura in modo da poter eseguire il backup affidabile del database e della directory GDS (Global Document Storage).

Mentre AEM forms è in modalità di backup sicuro, funziona normalmente, tranne per il fatto che non rimuove attivamente i file dalla directory GDS.

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
