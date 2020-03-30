---
title: Configurazione dell'utilità di pianificazione della sincronizzazione
seo-title: Configurazione dell'utilità di pianificazione della sincronizzazione
description: Scoprite come migrare e sincronizzare le risorse, configurare l’utilità di pianificazione della sincronizzazione e utilizzare le cartelle per disporre le risorse.
seo-description: Scoprite come migrare e sincronizzare le risorse, configurare l’utilità di pianificazione della sincronizzazione e utilizzare le cartelle per disporre le risorse.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configurazione dell&#39;utilità di pianificazione della sincronizzazione {#configuring-the-synchronization-scheduler}

Per impostazione predefinita, la funzione di pianificazione della sincronizzazione viene eseguita dopo ogni 3 minuti per sincronizzare tutte le risorse modificate e aggiornate nell&#39;archivio tramite LiveCycle Workbench 11. Le applicazioni contenenti moduli e risorse sono visibili nell’interfaccia utente di AEM Forms al termine del processo di sincronizzazione.

## Modifica dell&#39;intervallo del programma di sincronizzazione {#change-interval-of-the-synchronization-scheduler}

Per modificare l&#39;intervallo del programma di sincronizzazione, effettuate le seguenti operazioni:

1. Effettuate l&#39;accesso ad AEM Configuration Manager. L&#39;URL di Configuration Manager è `https://'[server]:[port]'/lc/system/console/configMgr`

1. Individuare e aprire il bundle **FormsManagerConfiguration** .

1. Specificate un nuovo valore per l&#39;opzione Frequenza **pianificazione** sincronizzazione.

   L&#39;unità della frequenza è di minuti. Ad esempio, per configurare l&#39;utilità di pianificazione in modo che venga eseguita dopo 60 minuti, specificate 60.

## Sincronizzazione delle risorse {#synchronizing-assets}

Potete usare l’opzione **Sincronizza risorse dall’archivio** per sincronizzare manualmente le risorse. Per sincronizzare manualmente le risorse, effettuate le seguenti operazioni:

1. Effettuate l&#39;accesso ad AEM Forms. L’URL predefinito è `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interfaccia utente di AEM Forms](assets/aem_forms_ui.png)

   **Figura:** Interfaccia utente di *AEM Forms*

1. Fate clic sull’icona ![aem6forms_sync](assets/aem6forms_sync.png) nella barra degli strumenti. Se non disponete di risorse all’ultimo percorso configurato, la finestra di dialogo viene visualizzata come illustrato di seguito. Fate clic su **Avvia** per avviare la sincronizzazione.

   ![Finestra di dialogo Sincronizzazione](assets/migrate-and-syncronize.png)

   **Figura:** Finestra di dialogo *Sincronizzazione*

## Risoluzione dei problemi di errore di sincronizzazione {#troubleshooting-synchronization-error}

È possibile creare nuove applicazioni nella finestra di progettazione del flusso di lavoro (LiveCycle Workbench).

Se l’applicazione appena creata e una cartella in /content/dam/formsanddocuments hanno lo stesso nome, viene visualizzato un errore &quot;*Una risorsa con lo stesso nome dell’applicazione esiste già a livello principale.*&quot; è registrato.

Per risolvere il conflitto, rinominare l’applicazione e sincronizzare manualmente le risorse.

![Conflitti nella finestra di dialogo di sincronizzazione delle risorse](assets/sync-conflict.png)

**Figura:** Conflitti *nella finestra di dialogo di sincronizzazione delle risorse*
