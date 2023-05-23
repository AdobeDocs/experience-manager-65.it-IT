---
title: Configurazione della memorizzazione in cache per Forms
seo-title: Configuring caching for Forms
description: Scopri come configurare le impostazioni della cache e come creare cluster per le cache.
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

Il servizio Forms prende forma di progetti creati in Designer e li riproduce in vari formati.

La pagina Forms nella console di amministrazione contiene le impostazioni che controllano il modo in cui il servizio Forms memorizza in cache gli elementi. È possibile regolare queste impostazioni per ottimizzare le prestazioni del servizio Forms.

Il servizio Forms memorizza nella cache i seguenti elementi:

* **progettazioni moduli:** Il servizio Forms memorizza nella cache le progettazioni dei moduli che recupera dal repository o da origini HTTP. Questo caching migliora le prestazioni perché per le successive richieste di rendering, il servizio Forms recupera la progettazione del modulo dalla cache anziché dall’archivio.
* **frammenti e immagini:** Il servizio Forms può memorizzare in cache frammenti e immagini utilizzati nelle progettazioni di moduli. Quando il servizio Forms memorizza nella cache questi oggetti, migliora le prestazioni perché i frammenti e le immagini vengono letti dal repository solo alla prima richiesta.
* **moduli:** Il servizio Forms memorizza nella cache i moduli di cui esegue il rendering. Questo tipo di caching migliora le prestazioni perché il servizio Forms non deve risolvere ed eseguire il rendering dello stesso modulo nelle richieste successive.

Forms memorizza la cache in due posizioni:

* **in memoria:** Gli elementi vengono archiviati in memoria per accedervi rapidamente. La cache in memoria ha dimensioni limitate e viene eliminata al riavvio del server.
* **su disco:** Gli elementi vengono archiviati nel file system del server. La cache del disco ha una capacità maggiore della cache in memoria e viene mantenuta al riavvio del server. La posizione della cache del disco dipende dal server dell&#39;applicazione. Per informazioni sulla modifica della posizione della cache del disco, vedere [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Specifica della modalità cache {#specifying-the-cache-mode}

Forms supporta due modalità di caching:

* incondizionato
* utilizzo del punto di controllo della cache

Se passi da una modalità di cache all’altra, riavvia il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o vedere [Avviare o arrestare i servizi associati ai moduli AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

Il tempo del punto di controllo della cache viene reimpostato automaticamente quando si passa da una modalità all&#39;altra.

### Utilizzo del caching non condizionale {#using-unconditional-caching}

In questa modalità, quando il servizio Forms riceve una richiesta, convalida le risorse necessarie (progettazione dei moduli e tutte le risorse correlate, come frammenti e immagini). Il servizio Forms confronta la marca temporale delle risorse nell’archivio con la marca temporale delle risorse nella cache. Se la risorsa nella cache è meno recente, il servizio Forms la aggiorna.

Questa modalità di cache garantisce l’utilizzo delle risorse più recenti. Tuttavia, le prestazioni sono influenzate dal fatto che il servizio Forms convalida gli elementi memorizzati in cache rispetto all’archivio a ogni richiesta. Questa modalità cache è adatta per gli ambienti di sviluppo e staging in cui le risorse vengono aggiornate frequentemente e le prestazioni non rappresentano un problema primario.

**Specificare la memorizzazione in cache non condizionale**

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Impostazioni controllo cache di Forms, seleziona Incondizionatamente e fai clic su Salva.

### Utilizza il punto di controllo della cache {#use-the-cache-check-point}

In questa modalità, il servizio Forms controlla l’archivio solo per le versioni più recenti delle risorse quando la marca temporale della risorsa memorizzata in cache è precedente all’ora del punto di controllo della cache. L&#39;ora dell&#39;ultimo punto di controllo della cache viene visualizzata nella pagina Forms di Administration Console.

Utilizza questa modalità cache in ambienti di produzione ad alte prestazioni in cui le prestazioni sono un problema e le modifiche alle risorse non sono frequenti. È possibile reimpostare l’ora del punto di controllo della cache quando si desidera distribuire eventuali modifiche apportate alle risorse dell’archivio.

**Specificare l&#39;utilizzo di un punto di controllo della cache**

1. In Administration Console, fare clic su Servizi > Forms.
1. In Impostazioni controllo cache di Forms, selezionare Solo se l&#39;ultima convalida è stata eseguita prima dell&#39;ora del punto di controllo della cache e fare clic su Salva.

**Reimposta il punto di controllo della cache**

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Impostazioni controllo cache di Forms fare clic su Punto di controllo cache.

**Reimposta il contenuto della cache**

Puoi cancellare il contenuto della cache in qualsiasi momento. Dopo un ripristino della cache, la prima richiesta per ciascun modulo è più lenta perché il servizio Forms esegue un rendering completo e crea nuovo contenuto della cache.

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Impostazioni controllo cache di Forms fare clic su Reimposta cache.

## Configurazione impostazioni cache {#configuring-cache-settings}

Puoi specificare le impostazioni utilizzate da Forms per il caching, che possono ottimizzare le prestazioni dell’ambiente dei moduli AEM.

Per accedere a queste impostazioni, nella console di amministrazione fai clic su Servizi > Forms.

>[!NOTE]
>
>I requisiti del disco per la cache devono essere uguali all’archivio.

### Specifica delle impostazioni globali della cache {#specifying-global-cache-settings}

Le impostazioni in **Impostazioni cache globale** di tutti i tipi di cache. Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o vedere [Avviare o arrestare i servizi associati ai moduli AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Dimensione massima documento cache (KB):** Dimensione massima, in kilobyte, della struttura di un modulo o di un&#39;altra risorsa che può essere memorizzata in qualsiasi cache in memoria. Si tratta di un’impostazione globale applicabile a tutte le cache in memoria. Se una risorsa è più grande di questo valore, non viene memorizzata nella cache. Il valore predefinito è 1024 kilobyte. Questa impostazione non influisce sulla cache del disco.

**Cache di rendering moduli abilitata:** Per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli sottoposti a rendering vengono memorizzati nella cache per il recupero successivo. Questa impostazione migliora le prestazioni perché il servizio Forms deve eseguire il rendering di un determinato modulo una sola volta e quindi utilizza la versione memorizzata nella cache. Questa opzione funziona con la proprietà di memorizzazione in cache della struttura del modulo. Per informazioni sulla configurazione di questo valore nella progettazione del modulo, vedere la Guida in linea di Designer.

### Memorizzazione in cache delle progettazioni dei moduli {#caching-form-designs}

Quando il servizio Forms riceve una richiesta di rendering, recupera la progettazione del modulo dall’archivio e la memorizza in cache. Questo caching migliora le prestazioni perché per le successive richieste di rendering, il servizio Forms recupera la progettazione del modulo dalla cache anziché dall’archivio.

Il servizio Forms memorizza sempre nella cache le progettazioni dei moduli su disco. Se le progettazioni dei moduli sono memorizzate sul server, tali file vengono considerati cache del disco. Il servizio Forms memorizza nella cache anche le progettazioni dei moduli, in base all’impostazione nella **Nella cache dei modelli di memoria** area. Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o vedere [Avviare o arrestare i servizi associati ai moduli AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Template Configuration Cache Size:** Numero massimo di oggetti di configurazione del modello da mantenere in memoria. Il valore predefinito è 100. È consigliabile impostare questo valore su un valore maggiore o uguale al valore di Dimensione cache modello. Questa impostazione non influisce sulla cache del disco.

**Template Cache Size:** Numero massimo di oggetti contenuto modello da mantenere in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**Attivato:** Per impostazione predefinita, questa casella di controllo è selezionata, il che significa che i modelli di modulo sono memorizzati nella cache. Se questa opzione non è selezionata, i modelli di modulo vengono memorizzati nella cache solo su disco.

### Memorizzazione in cache dei moduli sottoposti a rendering {#caching-rendered-forms}

Il servizio Forms memorizza nella cache i moduli sottoposti a rendering in modo da non dover risolvere ed eseguire il rendering dello stesso modulo nelle richieste successive. I moduli sottoposti a rendering vengono memorizzati nella cache sia su disco che in memoria.

Queste impostazioni si trovano nella sezione **Nella cache di rendering dei moduli di memoria** area. Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o vedere [Avviare o arrestare i servizi associati ai moduli AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Dimensione cache:** Specifica il numero massimo di moduli sottoposti a rendering che possono risiedere nella cache in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**Attivato:** Per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli sottoposti a rendering vengono memorizzati nella cache. Se questa opzione non è selezionata, i moduli sottoposti a rendering vengono memorizzati nella cache solo su disco.

### Memorizzazione in cache di frammenti e immagini {#caching-fragments-and-images}

Il servizio Forms memorizza in cache frammenti e immagini utilizzati nelle progettazioni di moduli su disco. Ciò migliora le prestazioni perché i frammenti e le immagini vengono letti dall’archivio solo alla prima richiesta. Successivamente, nelle richieste successive, il servizio Forms legge i frammenti e le immagini dalla cache del disco. I frammenti e le immagini vengono memorizzati nella cache solo su disco e non in memoria.

È possibile utilizzare le seguenti impostazioni per controllare la memorizzazione nella cache su disco di frammenti e immagini. Queste impostazioni si trovano nella sezione **Impostazioni cache risorse modello** area:

**Memorizzazione in cache delle risorse** Selezionare una delle opzioni seguenti dall&#39;elenco:

**Attivato per frammenti e immagini:** Il servizio Forms memorizza in cache frammenti e immagini. Questa è l&#39;opzione predefinita.

**Abilitato per frammenti:** Il servizio Forms memorizza nella cache i frammenti, ma non le immagini.

**Disattivato:** Il servizio Forms non memorizza in cache frammenti o immagini.

**Intervallo pulizia (secondi):** Specifica la frequenza con cui il servizio Forms rimuove i vecchi file di cache non validi. Il servizio Forms non rimuove i file di cache validi. Se si modifica l&#39;intervallo di pulizia, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o vedere Avviare o arrestare i servizi associati ai moduli AEM Forms per le istruzioni. Il valore predefinito è 600 secondi.

## Considerazioni sul clustering per le cache {#clustering-considerations-for-caches}

In un ambiente cluster, ogni nodo mantiene la propria cache in memoria e su disco. Il contenuto della cache di ciascun nodo dipende dai moduli di cui è stato eseguito il rendering su quel nodo.

La posizione della cache deve essere identica (stesso disco e percorso) in ogni nodo del cluster. Non inserire la cache nell&#39;archiviazione condivisa.

Se utilizzi la pagina Forms nella console di amministrazione per modificare le impostazioni della cache per un particolare nodo, le impostazioni della cache sugli altri nodi vengono aggiornate quando una richiesta viene indirizzata a tale nodo. Questo comportamento si applica anche al pulsante Reimposta cache. Se fai clic sul pulsante Reimposta cache per un nodo, la cache viene rimossa immediatamente da quel nodo. La cache sugli altri nodi viene cancellata quando una richiesta viene indirizzata a quel nodo.
