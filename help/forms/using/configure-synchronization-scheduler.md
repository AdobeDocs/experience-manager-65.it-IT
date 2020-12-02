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
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Configurazione del programma di sincronizzazione {#configuring-the-synchronization-scheduler}

Per impostazione predefinita, la funzione di pianificazione della sincronizzazione viene eseguita dopo ogni 3 minuti per sincronizzare tutte le risorse modificate e aggiornate nella directory archivio tramite LiveCycle Workbench 11. Le applicazioni che contengono moduli e risorse sono visibili nell&#39;interfaccia utente  di AEM Forms al termine del processo di sincronizzazione.

## Modifica dell&#39;intervallo del programma di sincronizzazione {#change-interval-of-the-synchronization-scheduler}

Per modificare l&#39;intervallo del programma di sincronizzazione, effettuate le seguenti operazioni:

1. Accedete a AEM Configuration Manager. L&#39;URL di Configuration Manager è `https://'[server]:[port]'/lc/system/console/configMgr`

1. Individuare e aprire il pacchetto **FormsManagerConfiguration**.

1. Specificate un nuovo valore per l&#39;opzione **Frequenza pianificazione sincronizzazione**.

   L&#39;unità della frequenza è di minuti. Ad esempio, per configurare l&#39;utilità di pianificazione in modo che venga eseguita dopo 60 minuti, specificate 60.

## Sincronizzazione delle risorse {#synchronizing-assets}

Potete utilizzare l&#39;opzione **Sincronizza risorse da repository** per sincronizzare manualmente le risorse. Per sincronizzare manualmente le risorse, effettuate le seguenti operazioni:

1. Effettuate l&#39;accesso a  AEM Forms. L&#39;URL predefinito è `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interfaccia utente  AEM Forms](assets/aem_forms_ui.png)

   **Figura:** *interfaccia utente AEM Forms*

1. Fare clic sull&#39;icona ![aem6forms_sync](assets/aem6forms_sync.png) nella barra degli strumenti. Se non disponete di risorse all’ultimo percorso configurato, la finestra di dialogo viene visualizzata come illustrato di seguito. Fare clic su **Start** per avviare la sincronizzazione.

   ![Finestra di dialogo Sincronizzazione](assets/migrate-and-syncronize.png)

   **Figura:** *Sincronizzazione, finestra di dialogo*

## Risoluzione dei problemi di errore di sincronizzazione {#troubleshooting-synchronization-error}

È possibile creare nuove applicazioni nella finestra di progettazione dei flussi di lavoro (Workbench LiveCycle).

Se l&#39;applicazione appena creata e una cartella in /content/dam/formsanddocuments hanno lo stesso nome, viene visualizzato un errore &quot;*Una risorsa con lo stesso nome dell&#39;applicazione esiste già a livello principale.*&quot; è registrato.

Per risolvere il conflitto, rinominare l’applicazione e sincronizzare manualmente le risorse.

![Conflitti nella finestra di dialogo di sincronizzazione delle risorse](assets/sync-conflict.png)

**Figura:** *Conflitti nella finestra di dialogo di sincronizzazione delle risorse*
