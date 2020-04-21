---
title: Migrazione da Dynamic Media - Modalità ibrida a Dynamic Media - Modalità S7
description: Scopri come trasferire la tua istanza di Dynamic Media - Modalità ibrida a Dynamic Media - modalità S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: f466193a259d9e8869d7f79eafda1be20869e4af

---


# Passaggio da elemento multimediale dinamico-ibrido a elemento multimediale dinamico-Scene7 {#about-migrating}

Dynamic Media-Hybrid è una versione precedente dell’integrazione Dynamic Media con Adobe Experience Manager. La versione ibrida è stata introdotta per la prima volta in AEM (Adobe Experience Manager) 6.1. Adobe continua a supportare la modalità ibrida, ma non la modalità preferita (la modalità preferita è Dynamic Media-Scene7). Non supporta inoltre nuove funzioni quali Smart Crop e immagini panoramiche. mentre per gli elementi multimediali dinamici di Scene7.

Ulteriori differenze chiave tra Dynamic Media-Hybrid e Dynamic Media-Scene7 sono:

* Struttura degli URL.
* Ingestione dei video.
* Creazione e memorizzazione di rappresentazioni di immagini.
* Configurazione e credenziali cloud (provisioning).

Quando passate da Dynamic Media-Hybrid a Dynamic Media-Scene7, sono disponibili due opzioni. La prima opzione consiste nel fornire semplicemente una nuova istanza di Dynamic Media-Scene7 su AEM. La seconda opzione consiste nel migrare l’istanza esistente di elemento multimediale dinamico ibrido in elemento multimediale dinamico-Scene7. Questa opzione mostra il modulo di tabella riportato di seguito, sotto i passaggi e le considerazioni da effettuare durante lo spostamento.

>[!IMPORTANT]
>
>Adobe consiglia di non migrare un’implementazione Dynamic Media-Hybrid in Dynamic Media-Scene7 su istanze di produzione live.

## Opzione 1 - Provisioning di una nuova istanza di Dynamic Media-Scene7 su AEM {#provision-new-dms7}

È consigliabile iniziare semplicemente da zero con una nuova istanza di Dynamic Media-Scene7 su Adobe Experience Manager. Oltre all’assimilazione e all’elaborazione delle risorse tramite Dynamic Media Cloud Service, si consiglia vivamente di effettuare un controllo Adobe sull’utilizzo delle risorse, sui flussi di lavoro e sui componenti. In molti casi, i componenti e i flussi di lavoro personalizzati possono essere sostituiti da nuove funzioni pronte all&#39;uso.

## Opzione 2 - Migrazione dell’istanza esistente di elemento multimediale dinamico ibrido a elemento multimediale dinamico-Scene7 {#process-for-migrating}

| Incremento | Attività | Considerazioni |
|---|---|---|
| 1 | Clona l’istanza Dynamic Media-Hybrid Author. | È necessario mantenere l&#39;istanza esistente di Dynamic Media-Hybrid Author a scopo di fallback fino al completamento dei passaggi rimanenti del processo di migrazione. |
| 2 | Avviate l’istanza Author clonata in modalità Dynamic Media-Scene7. |  |
| 3 | In Adobe Experience Manager Cloud Services, configura Dynamic Media con le credenziali Dynamic Media-Scene7. | Adobe deve approvare il provisioning Dynamic Media-Scene7. Gli ambienti Dynamic MediaM-Hybrid e Dynamic Media-Scene7 saranno supportati per un periodo di tempo limitato. |
| 4 | Create il bundle di migrazione per acquisire le risorse in base alle esigenze.<br>Eliminate i file PTIFF locali creati durante l’assimilazione iniziale in Dynamic Media-Hybrid. | Se tutte le risorse sono attualmente disponibili nell’istanza Dynamic Media-Hybrid, un clone di tale risorsa le include già tutte. Pertanto, non è necessario alcun bundle. |
| 5 | Eseguite il flusso di lavoro di aggiornamento delle risorse per sincronizzare le risorse a Dynamic Media Cloud Service. | Adobe consiglia di eseguire il flusso di lavoro di aggiornamento in batch per consentire la compattazione. |
| 6 | Migrare i predefiniti per visualizzatori, immagini e video. |  |
| 7 | Scorrete tutte le risorse di riferimento per la gestione dei contenuti Web e aggiornate i relativi URL. |  |
| 8 | Migrate eventuali flussi di lavoro personalizzati per supportare la nuova modalità Dynamic Media-Scene7 (aggiornamenti manuali). |  |
| 9 | Verificate il caricamento e la configurazione della gestione dei contenuti Web. |  |
| 10 | Dopo la verifica, ottieni un’approvazione per disabilitare l’autore ibrido per file multimediali dinamici (mantieni come fall back). |  |
| 11 | Eliminate l’istanza di authoring per file multimediali dinamici ibridi dopo circa un mese dall’utilizzo di Dynamic Media-Scene7. |  |
