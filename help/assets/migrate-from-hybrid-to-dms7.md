---
title: Migrazione da Dynamic Media - Modalità ibrida a Dynamic Media - Modalità S7
description: Scopri come migrare la tua istanza di Dynamic Media - Modalità ibrida a Dynamic Media - Modalità S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Modalità Scene7, Modalità ibrida
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 2%

---

# Informazioni sul passaggio da Dynamic Media-Hybrid a Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid è una versione precedente dell’integrazione Dynamic Media con Adobe Experience Manager. La versione ibrida è stata introdotta in Adobe Experience Manager 6.1. Anche se Adobe continua a supportare la modalità ibrida, non è la modalità preferita; Dynamic Media-Scene7 è la modalità preferita da utilizzare. La modalità ibrida non supporta inoltre nuove funzioni come Ritaglio avanzato e immagini panoramiche, mentre Dynamic Media-Scene7 le supporta.

Ulteriori differenze chiave tra Dynamic Media-Hybrid e Dynamic Media-Scene7 includono:

* Struttura degli URL.
* Acquisizione di video.
* Creazione e archiviazione di rappresentazioni delle immagini.
* Configurazione e credenziali del cloud (provisioning).

Quando si passa da Dynamic Media-Hybrid a Dynamic Media-Scene7 sono disponibili due opzioni: La prima opzione è semplicemente quella di fornire una nuova istanza di Dynamic Media-Scene7 su Experience Manager. La seconda opzione è la migrazione dell’istanza esistente di Dynamic Media-Hybrid a Dynamic Media-Scene7. Questa opzione delinea il modulo di tabella sotto i passaggi e le considerazioni da eseguire durante lo spostamento.

>[!IMPORTANT]
>
>L’Adobe consiglia di non migrare un’implementazione Dynamic Media-Hybrid a Dynamic Media-Scene7 su istanze di produzione live.

## Opzione 1 - Provisioning di una nuova istanza di Dynamic Media-Scene7 sull&#39;Experience Manager {#provision-new-dms7}

È consigliabile iniziare da zero con una nuova istanza di Dynamic Media-Scene7 su Adobe Experience Manager, dotata di provisioning. Oltre all’acquisizione e all’elaborazione delle risorse tramite il Cloud Service Dynamic Media, è vivamente consigliato un controllo Adobe dell’utilizzo delle risorse, dei flussi di lavoro e dei componenti. Spesso è possibile sostituire i componenti e i flussi di lavoro personalizzati utilizzando funzioni sempre più recenti.

## Opzione 2: migrazione dell&#39;istanza esistente di Dynamic Media-Hybrid a Dynamic Media-Scene7 {#process-for-migrating}

| Incremento | Attività | Considerazioni |
|---|---|---|
| 1 | Clona l’istanza di authoring Dynamic Media-Hybrid. | Mantieni l’istanza esistente di Dynamic Media-Hybrid Author a scopo di fallback fino a quando i passaggi rimanenti in questo processo di migrazione non vengono completati correttamente. |
| 2 | Avvia l&#39;istanza Author clonata in modalità Dynamic Media-Scene7. |  |
| 3 | In Cloud Services Adobe Experience Manager, configura Dynamic Media con le credenziali Dynamic Media-Scene7. | Adobe deve approvare il provisioning Dynamic Media-Scene7. Di conseguenza, gli ambienti Dynamic MediaM-Hybrid e Dynamic Media-Scene7 simultanei sono supportati da Adobe, ma solo per un periodo di tempo limitato. |
| 4 | Crea un bundle di migrazione per acquisire le risorse in base alle esigenze.<br>Elimina i PTIFF locali creati durante l’acquisizione iniziale in Dynamic Media-Hybrid. | Se tutte le risorse sono attualmente disponibili nell’istanza Dynamic Media-Hybrid, un clone di che le include già tutte. Pertanto, non è necessario alcun bundle. |
| 5 | Esegui il flusso di lavoro di aggiornamento delle risorse per sincronizzare le risorse al Cloud Service Dynamic Media. | Adobe consiglia di eseguire il flusso di lavoro di aggiornamento in batch per consentire la compattazione. |
| 6 | Migrare predefiniti per visualizzatori, immagini e video. |  |
| 7 | Scorri tutte le risorse a cui si fa riferimento in Gestione dei contenuti web e aggiorna gli URL associati. |  |
| 8 | Esegui la migrazione dei flussi di lavoro personalizzati che desideri supportare la nuova modalità Dynamic Media-Scene7 (aggiornamenti manuali). |  |
| 9 | Verifica il caricamento e la configurazione della gestione dei contenuti web. |  |
| 10 | Dopo la verifica, ottieni un’approvazione per disabilitare l’authoring Dynamic Media-Hybrid (mantieni come fallback). |  |
| 11 | Elimina l’istanza di authoring Dynamic Media-Hybrid dopo circa un mese di utilizzo corretto di Dynamic Media-Scene7. |  |
