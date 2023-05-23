---
title: Attivazione e disattivazione della modalità di backup sicuro
seo-title: Enabling and disabling safe backup mode
description: Nella pagina Impostazioni di backup è possibile utilizzare i moduli AEM in modalità di backup sicura in modo da poter eseguire il backup affidabile del database e della directory GDS (Global Document Storage). Scopri come abilitare e disabilitare la modalità di backup sicuro.
seo-description: On the Backup Settings page, you can operate AEM forms in safe backup mode so that you can reliably back up your database and Global Document Storage (GDS) (GDS) directory. Learn how to enable and disable safe backup mode.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Attivazione e disattivazione della modalità di backup sicuro {#enabling-and-disabling-safe-backup-mode}

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
