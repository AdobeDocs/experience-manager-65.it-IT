---
title: Configurazione dell'utilità di pianificazione della sincronizzazione
description: Scopri come migrare e sincronizzare le risorse, configurare l’utilità di pianificazione della sincronizzazione e utilizzare le cartelle per organizzare le risorse.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
solution: Experience Manager, Experience Manager Forms
feature: Workbench,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Configurazione dell&#39;utilità di pianificazione della sincronizzazione {#configuring-the-synchronization-scheduler}

Per impostazione predefinita, la pianificazione della sincronizzazione viene eseguita ogni 3 minuti per sincronizzare tutte le risorse modificate e aggiornate nell’archivio tramite LiveCycle Workbench 11. Le applicazioni contenenti moduli e risorse sono visibili nell’interfaccia utente di AEM Forms al termine del processo di sincronizzazione.

## Intervallo di modifica dell&#39;utilità di pianificazione della sincronizzazione {#change-interval-of-the-synchronization-scheduler}

Per modificare l&#39;intervallo dell&#39;utilità di pianificazione della sincronizzazione, effettuare le operazioni riportate di seguito.

1. Accedere a Gestione configurazione AEM. URL di Configuration Manager: `https://'[server]:[port]'/lc/system/console/configMgr`

1. Individua e apri il bundle **FormsManagerConfiguration**.

1. Specificare un nuovo valore per l&#39;opzione **Frequenza utilità di pianificazione sincronizzazione**.

   L&#39;unità della frequenza è minuti. Ad esempio, per configurare la pianificazione in modo che venga eseguita dopo ogni 60 minuti, specificare 60.

## Sincronizzazione delle risorse {#synchronizing-assets}

È possibile utilizzare l&#39;opzione **Sincronizza Assets dall&#39;archivio** per sincronizzare manualmente le risorse. Per sincronizzare manualmente le risorse, effettua le seguenti operazioni:

1. Accedi ad AEM Forms. URL predefinito: `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interfaccia utente di AEM Forms](assets/aem_forms_ui.png)

   **Figura:** *Interfaccia utente di AEM Forms*

1. Fai clic sull&#39;icona ![aem6forms_sync](assets/aem6forms_sync.png) nella barra degli strumenti. Se non disponi di alcuna risorsa nell’ultimo percorso configurato, seleziona la finestra di dialogo come mostrato di seguito. Fare clic su **Inizio** per avviare la sincronizzazione.

   ![Finestra di dialogo di sincronizzazione](assets/migrate-and-syncronize.png)

   **Figura:** *Finestra di dialogo di sincronizzazione*

## Risoluzione dei problemi di sincronizzazione {#troubleshooting-synchronization-error}

È possibile creare nuove applicazioni nel designer flusso di lavoro (LiveCycle Workbench).

Se l&#39;applicazione appena creata e una cartella in /content/dam/formsanddocuments hanno lo stesso nome, a livello principale esiste già un errore &quot;*Una risorsa con lo stesso nome di questa applicazione.*&quot; è registrato.

Per risolvere il conflitto, rinomina l’applicazione e sincronizza manualmente le risorse.

![Conflitti nella finestra di dialogo di sincronizzazione risorse](assets/sync-conflict.png)

**Figura:** *Conflitti nella finestra di dialogo di sincronizzazione risorse*
