---
title: Configurazione dell'utilità di pianificazione della sincronizzazione
seo-title: Configuring the synchronization scheduler
description: Scopri come migrare e sincronizzare le risorse, configurare l’utilità di pianificazione della sincronizzazione e utilizzare le cartelle per organizzare le risorse.
seo-description: Learn how to migrate and sync assets, configure sync scheduler, and use folders to arrange assets.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Configurazione dell&#39;utilità di pianificazione della sincronizzazione {#configuring-the-synchronization-scheduler}

Per impostazione predefinita, la pianificazione della sincronizzazione viene eseguita ogni 3 minuti per sincronizzare tutte le risorse modificate e aggiornate nell’archivio tramite LiveCycle Workbench 11. Le applicazioni contenenti moduli e risorse sono visibili nell’interfaccia utente di AEM Forms al termine del processo di sincronizzazione.

## Intervallo di modifica dell&#39;utilità di pianificazione della sincronizzazione {#change-interval-of-the-synchronization-scheduler}

Per modificare l&#39;intervallo dell&#39;utilità di pianificazione della sincronizzazione, effettuare le operazioni riportate di seguito.

1. Accedere a Gestione configurazione AEM. L’URL di Configuration Manager è `https://'[server]:[port]'/lc/system/console/configMgr`

1. Individuare e aprire **FormsManagerConfiguration** pacchetto.

1. Specifica un nuovo valore per **Frequenza utilità di pianificazione sincronizzazione** opzione.

   L&#39;unità della frequenza è minuti. Ad esempio, per configurare la pianificazione in modo che venga eseguita dopo ogni 60 minuti, specificare 60.

## Sincronizzazione delle risorse {#synchronizing-assets}

È possibile utilizzare **Sincronizzare le risorse dall’archivio** per sincronizzare manualmente le risorse. Per sincronizzare manualmente le risorse, effettua le seguenti operazioni:

1. Accedi ad AEM Forms. L’URL predefinito è `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interfaccia utente di AEM Forms](assets/aem_forms_ui.png)

   **Figura:** *Interfaccia utente di AEM Forms*

1. Fai clic su ![aem6forms_sync](assets/aem6forms_sync.png) nella barra degli strumenti. Se non disponi di alcuna risorsa nell’ultimo percorso configurato, seleziona la finestra di dialogo come mostrato di seguito. Clic **Inizio** per avviare la sincronizzazione.

   ![Finestra di dialogo Sincronizzazione](assets/migrate-and-syncronize.png)

   **Figura:** *Finestra di dialogo Sincronizzazione*

## Risoluzione dei problemi di sincronizzazione {#troubleshooting-synchronization-error}

È possibile creare nuove applicazioni nel designer flusso di lavoro (LiveCycle Workbench).

Se l’applicazione appena creata e una cartella in /content/dam/formsanddocuments hanno lo stesso nome, viene visualizzato un errore &quot;*A livello principale esiste già una risorsa con lo stesso nome di questa applicazione.*&quot; è registrato.

Per risolvere il conflitto, rinomina l’applicazione e sincronizza manualmente le risorse.

![Conflitti nella finestra di dialogo Sincronizzazione risorse](assets/sync-conflict.png)

**Figura:** *Conflitti nella finestra di dialogo Sincronizzazione risorse*
