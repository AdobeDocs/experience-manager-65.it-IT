---
title: Migrazione da Dynamic Media - Modalità ibrida a Dynamic Media - Modalità S7
description: Scopri come migrare la tua istanza di Dynamic Media - Modalità ibrida a Dynamic Media - Modalità S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
feature: Modalità Scene7, Modalità ibrida
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
translation-type: tm+mt
source-git-commit: 61e703e73b831a9b4e7045e5d5fffeef5be7ed6d
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# Informazioni sul passaggio da Dynamic Media-Hybrid a Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid è una versione precedente dell’integrazione Dynamic Media con Adobe Experience Manager. La versione ibrida è stata introdotta in AEM (Adobe Experience Manager) 6.1. Anche se Adobe continua a supportare la modalità ibrida, non è la modalità preferita (Dynamic Media-Scene7 è la modalità preferita). Inoltre, non supporta nuove funzioni come Ritaglio avanzato e immagini panoramiche. Dynamic Media-Scene7 invece sì.

Ulteriori differenze chiave tra Dynamic Media-Hybrid e Dynamic Media-Scene7 includono:

* Struttura degli URL.
* Acquisizione di video.
* Creazione e archiviazione di rappresentazioni delle immagini.
* Configurazione e credenziali del cloud (provisioning).

Quando si passa da Dynamic Media-Hybrid a Dynamic Media-Scene7 sono disponibili due opzioni: La prima opzione è semplicemente quella di fornire una nuova istanza di Dynamic Media-Scene7 su AEM. La seconda opzione è la migrazione dell’istanza esistente di Dynamic Media-Hybrid a Dynamic Media-Scene7. Questa opzione delinea il modulo di tabella sotto i passaggi e le considerazioni da eseguire durante lo spostamento.

>[!IMPORTANT]
>
>L’Adobe consiglia di non migrare un’implementazione ibrida di Dynamic Media a Dynamic Media-Scene7 su istanze di produzione live.

## Opzione 1 - Provisioning di una nuova istanza di Dynamic Media-Scene7 su AEM {#provision-new-dms7}

È consigliabile iniziare da zero con una nuova istanza di Dynamic Media-Scene7 su Adobe Experience Manager. Oltre all’acquisizione e all’elaborazione delle risorse tramite il Cloud Service Dynamic Media, è vivamente consigliato un controllo Adobe dell’utilizzo delle risorse, dei flussi di lavoro e dei componenti. In molti casi, i componenti e i flussi di lavoro personalizzati possono essere sostituiti da nuove funzioni pronte all’uso.

## Opzione 2 - Migrazione dell&#39;istanza esistente di Dynamic Media-Hybrid a Dynamic Media-Scene7 {#process-for-migrating}

| Incremento | Attività | Considerazioni |
|---|---|---|
| 1 | Clona l’istanza di authoring Dynamic Media-Hybrid. | È necessario mantenere l’istanza esistente di Dynamic Media-Hybrid Author a scopo di fallback fino a quando i passaggi rimanenti in questo processo di migrazione non vengono completati correttamente. |
| 2 | Avvia l&#39;istanza Author clonata in modalità Dynamic Media-Scene7. |  |
| 3 | Nei Cloud Services Adobe Experience Manager, configura Dynamic Media con le credenziali Dynamic Media-Scene7. | Adobe deve approvare il provisioning Dynamic Media-Scene7. Gli ambienti Dynamic MediaM-Hybrid e Dynamic Media-Scene7 simultanei saranno supportati per un periodo di tempo limitato. |
| 4 | Crea il bundle di migrazione per acquisire le risorse in base alle esigenze.<br>Elimina i PTIFF locali creati durante l’acquisizione iniziale in Dynamic Media-Hybrid. | Se tutte le risorse sono attualmente disponibili nell’istanza Dynamic Media-Hybrid, un clone di che le include già tutte. Pertanto, non è necessario alcun bundle. |
| 5 | Esegui il flusso di lavoro di aggiornamento delle risorse per sincronizzare le risorse al Cloud Service Dynamic Media. | L’Adobe consiglia di eseguire il flusso di lavoro di aggiornamento in batch per consentire la compattazione. |
| 6 | Migrare predefiniti per visualizzatori, immagini e video. |  |
| 7 | Scorri tutte le risorse a cui si fa riferimento in Gestione dei contenuti web e aggiorna gli URL associati. |  |
| 8 | Esegui la migrazione di tutti i flussi di lavoro personalizzati per supportare la nuova modalità Dynamic Media-Scene7 (aggiornamenti manuali). |  |
| 9 | Verifica il caricamento e la configurazione della gestione dei contenuti web. |  |
| 10 | Dopo la verifica, ottieni un&#39;approvazione per disabilitare l&#39;autore ibrido di Dynamic Media (mantieni come fallback). |  |
| 11 | Elimina l’istanza di authoring Dynamic Media-Hybrid dopo circa un mese di utilizzo corretto di Dynamic Media-Scene7. |  |
