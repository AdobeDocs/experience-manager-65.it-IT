---
title: Configurazione della memorizzazione in cache per Forms
seo-title: Configuring caching for Forms
description: Scopri come configurare le impostazioni della cache e come eseguire il cluster di considerazioni per le cache.
seo-description: Learn how to configure cache settings and how to cluster considerations for caches.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 0%

---

# Configurazione della memorizzazione in cache per Forms{#configuring-caching-for-forms}

Il servizio Forms adotta le strutture del modulo create in Designer ed effettua il rendering in vari formati.

La pagina Forms nella console di amministrazione contiene impostazioni che controllano il modo in cui il servizio Forms memorizza in cache gli elementi. È possibile regolare queste impostazioni per ottimizzare le prestazioni del servizio Forms.

Il servizio Forms memorizza in cache i seguenti elementi:

* **strutture del modulo:** Il servizio Forms memorizza in cache le strutture dei moduli recuperate dall’archivio o da origini HTTP. Questo caching migliora le prestazioni perché per le richieste di rendering successive, il servizio Forms recupera la struttura del modulo dalla cache anziché dall’archivio.
* **frammenti e immagini:** Il servizio Forms può memorizzare nella cache frammenti e immagini utilizzati nelle strutture del modulo. Quando il servizio Forms memorizza in cache questi oggetti, migliora le prestazioni perché i frammenti e le immagini vengono letti dall’archivio solo alla prima richiesta.
* **moduli:** Il servizio Forms memorizza in cache i moduli di cui esegue il rendering. Questo tipo di caching migliora le prestazioni perché il servizio Forms non deve risolvere ed eseguire il rendering dello stesso modulo nelle richieste successive.

Forms memorizza la cache in due posizioni:

* **in memoria:** Gli elementi vengono memorizzati in memoria per un accesso rapido. La cache in memoria ha una dimensione limitata e viene eliminata al riavvio del server.
* **su disco:** Gli elementi vengono memorizzati nel file system del server. La cache del disco ha una capacità maggiore della cache in memoria e viene mantenuta al riavvio del server. La posizione della cache del disco dipende dal server dell&#39;applicazione. Per informazioni sulla modifica della posizione della cache del disco, vedi [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Specifica della modalità cache {#specifying-the-cache-mode}

Forms supporta due modalità di caching:

* incondizionato
* utilizzo del punto di controllo della cache

Se si passa da una modalità di cache all’altra, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

Il tempo del punto di controllo della cache viene reimpostato automaticamente quando si passa da una modalità all&#39;altra.

### Utilizzo della memorizzazione in cache incondizionata {#using-unconditional-caching}

In questa modalità, quando il servizio Forms riceve una richiesta, convalida le risorse necessarie (struttura del modulo e tutte le risorse correlate, come frammenti e immagini). Il servizio Forms confronta la marca temporale delle risorse nell’archivio con la marca temporale delle risorse nella cache. Se la risorsa nella cache è precedente, il servizio Forms la aggiorna.

Questa modalità cache garantisce l’utilizzo delle risorse più recenti. Tuttavia, le prestazioni sono influenzate dal fatto che il servizio Forms convalida gli elementi memorizzati nella cache rispetto all’archivio con ogni richiesta. Questa modalità cache è adatta per ambienti di sviluppo e staging in cui le risorse vengono aggiornate frequentemente e le prestazioni non rappresentano un problema primario.

**Specificare la memorizzazione in cache incondizionata**

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Impostazioni controllo cache Forms, selezionare Senza condizioni e fare clic su Salva.

### Utilizza il punto di controllo della cache {#use-the-cache-check-point}

In questa modalità, il servizio Forms controlla nell’archivio solo la disponibilità di versioni più recenti delle risorse quando la marca temporale della risorsa memorizzata nella cache è maggiore del tempo del punto di controllo della cache. L’ora dell’ultimo punto di controllo della cache viene visualizzata nella pagina Forms in Admin Console.

Utilizza questa modalità cache in ambienti di produzione ad alte prestazioni in cui le prestazioni rappresentano un problema e le modifiche alle risorse non sono frequenti. È possibile reimpostare il momento del controllo della cache quando si desidera distribuire eventuali modifiche apportate alle risorse del repository.

**Specificare l&#39;utilizzo di un punto di controllo della cache**

1. In Console di amministrazione, fai clic su Servizi > Forms.
1. In Impostazioni controllo cache di Forms, selezionare Solo se l&#39;ultima convalida è stata eseguita prima dell&#39;ora del punto di controllo della cache e fare clic su Salva.

**Reimposta il punto di controllo della cache**

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Impostazioni controllo cache Forms, fare clic su Punto di controllo cache.

**Reimpostare il contenuto della cache**

Puoi cancellare il contenuto della cache in qualsiasi momento. Dopo una reimpostazione della cache, la prima richiesta per ciascun modulo è più lenta perché il servizio Forms esegue un rendering completo e crea nuovo contenuto della cache.

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Impostazioni controllo cache Forms, fai clic su Ripristina cache.

## Configurazione delle impostazioni della cache {#configuring-cache-settings}

È possibile specificare le impostazioni utilizzate da Forms per la memorizzazione in cache, che possono ottimizzare le prestazioni dell’ambiente dei moduli AEM.

Per accedere a queste impostazioni, nella console di amministrazione fai clic su Servizi > Forms.

>[!NOTE]
>
>I requisiti del disco per la cache devono essere uguali all’archivio.

### Specifica delle impostazioni della cache globale {#specifying-global-cache-settings}

Le impostazioni nel **Impostazioni della cache globale** l’area interessa tutti i tipi di cache. Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Dimensione massima documento cache (KB):** Dimensione massima, in kilobyte, di una struttura del modulo o di un’altra risorsa memorizzabile in qualsiasi cache in memoria. Si tratta di un’impostazione globale che si applica a tutte le cache in memoria. Se una risorsa è più grande di questo valore, non viene memorizzata nella cache. Il valore predefinito è 1024 kilobyte. Questa impostazione non influisce sulla cache del disco.

**Cache di rendering del modulo abilitata:** Per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli di cui è stato effettuato il rendering vengono memorizzati nella cache per il successivo recupero. Questa impostazione migliora le prestazioni perché il servizio Forms deve eseguire il rendering di un modulo specifico una sola volta e quindi utilizza la versione cache. Questa opzione funziona con la proprietà di memorizzazione in cache della struttura del modulo. Per informazioni sulla configurazione di questo valore nella struttura del modulo, vedere la Guida di Designer.

### Schede del modulo di memorizzazione nella cache {#caching-form-designs}

Quando il servizio Forms riceve una richiesta di rendering, recupera la struttura del modulo dall’archivio e la memorizza in cache. Questo caching migliora le prestazioni perché per le richieste di rendering successive, il servizio Forms recupera la struttura del modulo dalla cache anziché dall’archivio.

Il servizio Forms memorizza sempre in cache le strutture dei moduli su disco. Se le strutture del modulo sono memorizzate sul server, tali file vengono considerati come cache del disco. Il servizio Forms memorizza anche le strutture del modulo nella cache, in base alle impostazioni in **Nella cache del modello di memoria** area. Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Dimensione cache configurazione modello:** Il numero massimo di oggetti di configurazione del modello da tenere in memoria. Il valore predefinito è 100. È consigliabile impostare questo valore maggiore o uguale al valore Dimensione cache modello. Questa impostazione non influisce sulla cache del disco.

**Dimensione cache modello:** Il numero massimo di oggetti di contenuto del modello da tenere in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**Abilitato:** Per impostazione predefinita, questa casella di controllo è selezionata, il che significa che i modelli di modulo sono memorizzati nella cache. Se questa opzione non è selezionata, i modelli di modulo vengono memorizzati nella cache solo su disco.

### Memorizzazione in cache dei moduli di cui è stato eseguito il rendering {#caching-rendered-forms}

Il servizio Forms memorizza in cache i moduli di cui è stato eseguito il rendering in modo da non dover risolvere ed eseguire il rendering dello stesso modulo nelle richieste successive. I moduli sottoposti a rendering vengono memorizzati nella cache sia su disco che in memoria.

Queste impostazioni si trovano nella **Nella cache di rendering dei moduli di memoria** area. Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Dimensione cache:** Specifica il numero massimo di moduli di cui è stato eseguito il rendering che possono trovarsi nella cache in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**Abilitato:** Per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli di cui è stato eseguito il rendering sono memorizzati nella cache. Se questa opzione non è selezionata, i moduli di cui è stato eseguito il rendering vengono memorizzati nella cache solo su disco.

### Memorizzazione in cache di frammenti e immagini {#caching-fragments-and-images}

Il servizio Forms memorizza in cache frammenti e immagini utilizzati nelle strutture del modulo su disco. Ciò migliora le prestazioni perché i frammenti e le immagini vengono letti dall’archivio solo alla prima richiesta. Successivamente, nelle richieste successive, il servizio Forms legge frammenti e immagini dalla cache del disco. I frammenti e le immagini sono memorizzati nella cache solo su disco e non in memoria.

È possibile utilizzare le seguenti impostazioni per controllare la memorizzazione in cache su disco di frammenti e immagini. Queste impostazioni si trovano nella **Impostazioni della cache delle risorse di modello** area:

**Memorizzazione in cache delle risorse** Selezionare una delle seguenti opzioni dall’elenco:

**Abilitato per frammenti e immagini:** Il servizio Forms memorizza in cache frammenti e immagini. Questa è l’opzione predefinita.

**Abilitato per i frammenti:** Il servizio Forms memorizza in cache frammenti, ma non immagini.

**Disabilitata:** Il servizio Forms non memorizza in cache frammenti o immagini.

**Intervallo di pulizia (secondi):** Specifica la frequenza con cui il servizio Forms rimuove i vecchi file di cache non validi. Il servizio Forms non rimuove i file di cache validi. Se si modifica l&#39;intervallo di pulizia, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare Avviare o arrestare i servizi associati ai moduli AEM per le istruzioni. Il valore predefinito è 600 secondi.

## Considerazioni sul clustering per le cache {#clustering-considerations-for-caches}

In un ambiente cluster, ogni nodo mantiene la propria cache in memoria e disco. Il contenuto della cache di ciascun nodo dipende da quali moduli sono stati sottoposti a rendering su quel nodo.

La posizione della cache deve essere identica (stesso disco e percorso) su ciascun nodo del cluster. Non inserire la cache nell&#39;archiviazione condivisa.

Se utilizzi la pagina Forms nella console di amministrazione per modificare le impostazioni della cache per un particolare nodo, le impostazioni della cache su altri nodi vengono aggiornate quando una richiesta passa a quel nodo. Questo comportamento si applica anche al pulsante Ripristina cache . Se fai clic sul pulsante Ripristina cache per un nodo, la cache viene immediatamente rimossa da quel nodo. La cache su altri nodi viene cancellata quando una richiesta arriva a quel nodo.
