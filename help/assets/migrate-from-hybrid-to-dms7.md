---
title: Migrazione da Dynamic Media - Modalità ibrida a Dynamic Media - Modalità S7
description: Scopri come migrare l’istanza di Dynamic Media - Modalità ibrida a Dynamic Media - Modalità S7
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
source-wordcount: '564'
ht-degree: 2%

---

# Informazioni sul passaggio da Dynamic Media-Hybrid a Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid è una versione precedente dell’integrazione Dynamic Media con Adobe Experience Manager. La versione ibrida è stata introdotta in Adobe Experience Manager 6.1. Anche se Adobe continua a supportare la modalità ibrida, non è la modalità preferita; Dynamic Media-Scene7 è la modalità preferita da utilizzare. La modalità ibrida non supporta nuove funzioni, come Ritaglio avanzato e immagini panoramiche, mentre Dynamic Media-Scene7 le supporta.

Ulteriori differenze chiave tra Dynamic Media-Hybrid e Dynamic Media-Scene7 includono:

* Struttura degli URL.
* Acquisizione di video.
* Creazione e archiviazione di rappresentazioni di immagini.
* Configurazione cloud e credenziali (provisioning).

Quando passi da Dynamic Media-Hybrid a Dynamic Media-Scene7, sono disponibili due opzioni. La prima opzione consiste semplicemente nel provisioning di una nuova istanza di Dynamic Media-Scene7 su Experience Manager. La seconda opzione consiste nel migrare l’istanza esistente di Dynamic Media-Hybrid a Dynamic Media-Scene7. Questa opzione delinea sotto forma di tabella i passaggi e le considerazioni da effettuare durante lo spostamento.

>[!IMPORTANT]
>
>Adobe consiglia di non migrare un’implementazione ibrida di Dynamic Media a Dynamic Media-Scene7 sulle istanze di produzione live.

## Opzione 1 - Provisioning di una nuova istanza di Dynamic Media-Scene7 su Experience Manager {#provision-new-dms7}

È sufficiente iniziare da capo con una nuova istanza predisposta di Dynamic Media-Scene7 su Adobe Experience Manager. Oltre all’acquisizione e all’elaborazione delle risorse tramite Dynamic Media Cloud Service, si consiglia vivamente di eseguire un controllo di Adobe sull’utilizzo delle risorse, i flussi di lavoro e i componenti. Spesso è possibile sostituire componenti e flussi di lavoro personalizzati utilizzando funzionalità più recenti e pronte all’uso.

## Opzione 2: migrazione dell&#39;istanza esistente di Dynamic Media-Hybrid a Dynamic Media-Scene7 {#process-for-migrating}

| Passaggio | Attività | Considerazioni |
|---|---|---|
| 1 | Clona l’istanza di authoring ibrido Dynamic Media. | Gestisci l’istanza esistente di Dynamic Media-Hybrid Author a scopo di fallback fino al completamento dei passaggi rimanenti di questo processo di migrazione. |
| 2 | Avvia l’istanza di authoring clonata in modalità Dynamic Media-Scene7. |  |
| 3 | In Adobe Experience Manager Cloud Services, configura Dynamic Media con le credenziali Dynamic Media-Scene7. | Adobe deve approvare il provisioning Dynamic Media-Scene7. In questo modo, puoi contare su ambienti Dynamic MediaM-Hybrid e Dynamic Media-Scene7 simultanei supportati da Adobe, ma solo per un periodo di tempo limitato. |
| 4 | Crea un bundle di migrazione per acquisire le risorse in base alle esigenze.<br>Eliminare i file PTIFF locali creati durante l&#39;acquisizione iniziale in Dynamic Media-Hybrid. | Se tutte le risorse sono attualmente disponibili nell’istanza ibrida di Dynamic Media, un clone di che le include già tutte. Pertanto, non è necessario alcun bundle. |
| 5 | Esegui il flusso di lavoro di aggiornamento delle risorse per sincronizzare le risorse con Dynamic Media Cloud Service. | Adobe consiglia di eseguire il flusso di lavoro di aggiornamento in batch per consentire la compattazione. |
| 6 | Migra i predefiniti visualizzatore, immagine e video. |  |
| 7 | Esaminare ogni risorsa di riferimento per la gestione dei contenuti web e aggiornare gli URL associati. |  |
| 8 | Migra i flussi di lavoro personalizzati che desideri supportare nella nuova modalità Dynamic Media-Scene7 (aggiornamenti manuali). |  |
| 9 | Verifica il caricamento e la configurazione di Gestione contenuto Web. |  |
| 10 | Dopo la verifica, ottieni un’approvazione per disabilitare Dynamic Media-Hybrid Author (mantieni come fallback). |  |
| 11 | Elimina l’istanza di authoring ibrido di Dynamic Media dopo circa un mese di utilizzo riuscito di Dynamic Media-Scene7. |  |
