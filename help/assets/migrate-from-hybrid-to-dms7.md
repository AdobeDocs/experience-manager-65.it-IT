---
title: Migrazione da Dynamic Medie - Modalità ibrida a Dynamic Medie - Modalità S7
description: Scopri come migrare l’istanza di Dynamic Medie in modalità ibrida a Dynamic Medie in modalità S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 2%

---

# Informazioni sul passaggio da Dynamic Medie-Hybrid a Dynamic Medie-Scene7 {#about-migrating}

Dynamic Medie-Hybrid è una versione precedente dell&#39;integrazione di Dynamic Medie con Adobe Experience Manager. La versione ibrida è stata introdotta in Adobe Experience Manager 6.1. Adobe continua a supportare la modalità ibrida, ma non è la modalità preferita; Dynamic Medie-Scene7 è la modalità preferita da utilizzare. La modalità ibrida non supporta inoltre nuove funzioni come Ritaglio avanzato e immagini panoramiche, mentre Dynamic Medie-Scene7 le supporta.

Ulteriori differenze chiave tra Dynamic Medie-Hybrid e Dynamic Medie-Scene7 includono:

* Struttura degli URL.
* Acquisizione di video.
* Creazione e archiviazione di rappresentazioni di immagini.
* Configurazione cloud e credenziali (provisioning).

Quando si passa da Dynamic Medie-Hybrid a Dynamic Medie-Scene7 sono disponibili due opzioni. La prima opzione consiste semplicemente nel provisioning di una nuova istanza di Dynamic Medie-Scene7 su Experience Manager. La seconda opzione consiste nel migrare l’istanza esistente di Dynamic Medie-Hybrid a Dynamic Medie-Scene7. Questa opzione delinea sotto forma di tabella i passaggi e le considerazioni da effettuare durante lo spostamento.

>[!IMPORTANT]
>
>L’Adobe consiglia di non migrare un’implementazione ibrida di Dynamic Medie a Dynamic Medie-Scene7 nelle istanze di produzione live.

## Opzione 1 - Eseguire il provisioning di una nuova istanza di Dynamic Medie-Scene7 su Experience Manager {#provision-new-dms7}

È sufficiente iniziare da capo con una nuova istanza predisposta di Dynamic Medie-Scene7 su Adobe Experience Manager. Oltre all’acquisizione e all’elaborazione delle risorse tramite il Cloud Service Dynamic Medie, si consiglia vivamente di eseguire un audit di Adobe sull’utilizzo delle risorse, i flussi di lavoro e i componenti. Spesso è possibile sostituire componenti e flussi di lavoro personalizzati utilizzando funzionalità più recenti e pronte all’uso.

## Opzione 2: migrazione dell&#39;istanza esistente di Dynamic Medie-Hybrid a Dynamic Medie-Scene7 {#process-for-migrating}

| Passaggio | Attività | Considerazioni |
|---|---|---|
| 1 | Clona l’istanza Dynamic Medie-Hybrid Author. | Gestisci l’istanza esistente di Dynamic Medie-Hybrid Author a scopo di fallback fino al completamento dei passaggi rimanenti di questo processo di migrazione. |
| 2 | Avvia l’istanza di authoring clonata in modalità Dynamic Medie-Scene7. |  |
| 3 | Nei Cloud Service Adobe Experience Manager, configura Dynamic Medie con le credenziali Dynamic Medie-Scene7. | L’Adobe deve approvare il provisioning di Dynamic Medie-Scene7. In questo modo, gli ambienti Dynamic MediaM-Hybrid e Dynamic Medie-Scene7 simultanei sono supportati da Adobe, ma solo per un periodo di tempo limitato. |
| 4 | Crea un bundle di migrazione per acquisire le risorse in base alle esigenze.<br>Elimina i file PTIFF locali creati durante l’acquisizione iniziale in Dynamic Medie-Hybrid. | Se tutte le risorse sono attualmente disponibili nell’istanza Dynamic Medie-Hybrid, un clone di che le include già tutte. Pertanto, non è necessario alcun bundle. |
| 5 | Esegui il flusso di lavoro di aggiornamento delle risorse per sincronizzarle con il Cloud Service Dynamic Medie. | L’Adobe consiglia di eseguire il flusso di lavoro di aggiornamento in batch per consentire la compattazione. |
| 6 | Migra i predefiniti visualizzatore, immagine e video. |  |
| 7 | Esaminare ogni risorsa di riferimento per la gestione dei contenuti web e aggiornare gli URL associati. |  |
| 8 | Migra i flussi di lavoro personalizzati che desideri supportare nella nuova modalità Dynamic Medie-Scene7 (aggiornamenti manuali). |  |
| 9 | Verifica il caricamento e la configurazione di Gestione contenuto Web. |  |
| 10 | Dopo la verifica, ottieni un’approvazione per disabilitare Dynamic Medie-Hybrid Author (mantieni come fallback). |  |
| 11 | Elimina l’istanza Dynamic Medie-Hybrid Author dopo circa un mese di utilizzo riuscito di Dynamic Medie-Scene7. |  |
