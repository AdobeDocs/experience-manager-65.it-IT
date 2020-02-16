---
title: Configurazione della memorizzazione nella cache per Forms
seo-title: Configurazione della memorizzazione nella cache per Forms
description: Scoprite come configurare le impostazioni della cache e come raggruppare le considerazioni per le cache.
seo-description: Scoprite come configurare le impostazioni della cache e come raggruppare le considerazioni per le cache.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurazione della memorizzazione nella cache per Forms{#configuring-caching-for-forms}

Il servizio Forms utilizza le strutture del modulo create in Designer ed eseguirà il rendering in vari formati.

La pagina Moduli nella console di amministrazione contiene impostazioni che controllano il modo in cui il servizio Forms memorizza gli elementi nella cache. È possibile regolare queste impostazioni per ottimizzare le prestazioni del servizio Forms.

Il servizio Forms memorizza nella cache gli elementi seguenti:

* **** strutture del modulo: Il servizio Forms memorizza nella cache le strutture del modulo recuperate dall&#39;archivio o da origini HTTP. Questo caching migliora le prestazioni perché per le richieste di rendering successive, il servizio Forms recupera la struttura del modulo dalla cache anziché dall&#39;archivio.
* **** frammenti e immagini: Il servizio Forms consente di memorizzare nella cache frammenti e immagini utilizzati nelle strutture del modulo. Quando il servizio Forms memorizza nella cache tali oggetti, migliora le prestazioni in quanto i frammenti e le immagini vengono letti dall&#39;archivio solo alla prima richiesta.
* **** moduli: Il servizio Forms memorizza nella cache i moduli che esegue il rendering. Questo tipo di caching migliora le prestazioni perché il servizio Forms non deve risolvere ed eseguire il rendering dello stesso modulo nelle richieste successive.

Forms memorizza la cache in due posizioni:

* **** in memoria: Gli elementi vengono memorizzati per un accesso rapido. La cache in memoria ha dimensioni limitate e viene eliminata al riavvio del server.
* **** su disco: Gli elementi vengono memorizzati nel file system del server. La cache del disco ha una capacità maggiore della cache in memoria e viene mantenuta al riavvio del server. La posizione della cache del disco dipende dal server dell’applicazione. Per informazioni sulla modifica della posizione della cache del disco, vedere [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Specifica della modalità cache {#specifying-the-cache-mode}

Forms supporta due modalità di caching:

* incondizionato
* utilizzo del punto di controllo della cache

Se si passa da una modalità cache all&#39;altra, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) AEM per le istruzioni.

Il tempo del punto di controllo della cache viene reimpostato automaticamente quando si passa da una modalità all&#39;altra.

### Utilizzo della cache non condizionale {#using-unconditional-caching}

In questa modalità, quando il servizio Forms riceve una richiesta, convalida le risorse necessarie (struttura del modulo ed eventuali risorse correlate, ad esempio frammenti e immagini). Il servizio Forms confronta la marca temporale delle risorse presenti nell&#39;archivio con la marca temporale delle risorse presenti nella cache. Se la risorsa nella cache è precedente, il servizio Forms la aggiorna.

Questa modalità cache garantisce l’utilizzo delle risorse più recenti. Tuttavia, le prestazioni sono influenzate dal fatto che il servizio Forms convalida gli elementi memorizzati nella cache rispetto all&#39;archivio con ciascuna richiesta. Questa modalità cache è adatta per ambienti di sviluppo e gestione temporanea in cui le risorse vengono aggiornate frequentemente e le prestazioni non rappresentano un problema principale.

**Specificare la cache non condizionale**

1. Nella console di amministrazione, fare clic su Servizi > Moduli.
1. In Impostazioni controllo cache moduli, selezionare Senza condizioni e fare clic su Salva.

### Utilizzare il punto di controllo della cache {#use-the-cache-check-point}

In questa modalità, il servizio Forms controlla nell&#39;archivio solo la disponibilità di nuove versioni delle risorse quando la marca temporale della risorsa memorizzata nella cache è maggiore dell&#39;ora del punto di controllo della cache. L&#39;ora dell&#39;ultimo punto di controllo della cache viene visualizzata nella pagina Moduli in Admin Console.

Utilizzate questa modalità cache in ambienti di produzione ad alte prestazioni in cui le prestazioni sono un problema e le modifiche alle risorse non sono frequenti. È possibile reimpostare l&#39;ora del punto di controllo della cache quando si desidera distribuire le modifiche apportate alle risorse del repository.

**Specificare l&#39;utilizzo di un punto di controllo della cache**

1. In Admin Console, fai clic su Servizi > Moduli.
1. In Impostazioni controllo cache moduli, selezionare Solo se l&#39;ultima convalida è stata eseguita prima dell&#39;ora del punto di controllo della cache e fare clic su Salva.

**Ripristino del punto di controllo della cache**

1. Nella console di amministrazione, fare clic su Servizi > Moduli.
1. In Impostazioni controllo cache moduli fare clic su Punto di controllo cache.

**Reimpostare il contenuto della cache**

Potete cancellare il contenuto della cache in qualsiasi momento. Dopo la reimpostazione della cache, la prima richiesta per ciascun modulo è più lenta perché il servizio Forms esegue un rendering completo e crea nuovo contenuto della cache.

1. Nella console di amministrazione, fare clic su Servizi > Moduli.
1. In Impostazioni controllo cache moduli fare clic su Reimposta cache.

## Configurazione delle impostazioni della cache {#configuring-cache-settings}

È possibile specificare le impostazioni utilizzate da Forms per il caching, al fine di ottimizzare le prestazioni dell&#39;ambiente dei moduli AEM.

Per accedere a queste impostazioni, nella console di amministrazione fare clic su Servizi > Moduli.

>[!NOTE]
>
>I requisiti del disco per la cache devono essere uguali al repository.

### Specifica delle impostazioni della cache globale {#specifying-global-cache-settings}

Le impostazioni nell&#39;area Impostazioni **cache** globale interessano tutti i tipi di cache. Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) AEM per le istruzioni.

**** Dimensione massima documento cache (KB): La dimensione massima, in kilobyte, di una struttura del modulo o di altre risorse che è possibile memorizzare nella cache in qualsiasi memoria. Si tratta di un&#39;impostazione globale che si applica a tutte le cache in memoria. Se una risorsa è più grande di questo valore, non viene memorizzata nella cache. Il valore predefinito è 1024 kilobyte. Questa impostazione non influisce sulla cache del disco.

**** Cache di rendering del modulo abilitata: Per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli sottoposti a rendering vengono memorizzati nella cache per il successivo recupero. Questa impostazione migliora le prestazioni perché il servizio Forms deve eseguire il rendering di un modulo specifico solo una volta e quindi utilizza la versione memorizzata nella cache. Questa opzione funziona con la proprietà caching della struttura del modulo. Per informazioni sulla configurazione di questo valore nella struttura del modulo, vedere la Guida di Designer.

### Memorizzazione delle strutture del modulo nella cache {#caching-form-designs}

Quando il servizio Forms riceve una richiesta di rendering, recupera la struttura del modulo dall&#39;archivio e la memorizza nella cache. Questo caching migliora le prestazioni perché per le richieste di rendering successive, il servizio Forms recupera la struttura del modulo dalla cache anziché dall&#39;archivio.

Il servizio Forms memorizza sempre nella cache le strutture del modulo sul disco. Se le strutture del modulo sono memorizzate sul server, tali file vengono considerati cache del disco. Il servizio Forms memorizza anche le strutture del modulo nella cache, in base alle impostazioni specificate nell&#39;area **In Memory Template Cache** . Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) AEM per le istruzioni.

**** Dimensione cache configurazione modello: Il numero massimo di oggetti di configurazione del modello da tenere in memoria. Il valore predefinito è 100. È consigliabile impostare questo valore maggiore o uguale al valore Dimensione cache modello. Questa impostazione non influisce sulla cache del disco.

**** Dimensione cache modello: Il numero massimo di oggetti di contenuto modello da tenere in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**** Abilitato: Per impostazione predefinita, questa casella di controllo è selezionata, il che significa che i modelli di modulo sono memorizzati nella cache. Se questa opzione non è selezionata, i modelli di modulo sono memorizzati nella cache solo sul disco.

### Memorizzazione dei moduli di cui è stato effettuato il rendering nella cache {#caching-rendered-forms}

Il servizio Forms memorizza nella cache i moduli di cui è stato eseguito il rendering in modo che non sia necessario risolvere ed eseguire il rendering dello stesso modulo nelle richieste successive. I moduli di cui è stato effettuato il rendering sono memorizzati nella cache sia su disco che in memoria.

Queste impostazioni si trovano nell&#39;area **In Memory Form Rendering Cache** . Se si modifica una di queste impostazioni, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) AEM per le istruzioni.

**** Dimensione cache: Specifica il numero massimo di moduli sottoposti a rendering che possono risiedere nella cache in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**** Abilitato: Per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli di cui è stato effettuato il rendering sono memorizzati nella cache. Se questa opzione non è selezionata, i moduli di cui è stato eseguito il rendering vengono memorizzati nella cache solo sul disco.

### Memorizzazione nella cache di frammenti e immagini {#caching-fragments-and-images}

Il servizio Forms memorizza nella cache frammenti e immagini utilizzati nelle strutture del modulo su disco. Ciò migliora le prestazioni perché i frammenti e le immagini vengono letti solo dalla directory archivio alla prima richiesta. Quindi, su richieste successive, il servizio Forms legge frammenti e immagini dalla cache del disco. I frammenti e le immagini sono memorizzati nella cache solo su disco e non nella memoria.

Per controllare il caching su disco di frammenti e immagini è possibile utilizzare le seguenti impostazioni. Queste impostazioni si trovano nell&#39;area **Template Resource Cache Settings** (Impostazioni cache risorse modello):

**Memorizzazione nella cache** delle risorse Selezionare una delle seguenti opzioni dall&#39;elenco:

**** Abilitata per frammenti e immagini: Il servizio Forms memorizza nella cache frammenti e immagini. Questa è l&#39;opzione predefinita.

**** Abilitato per i frammenti: Il servizio Forms memorizza nella cache i frammenti, ma non le immagini.

**** Disattivato: Il servizio Forms non memorizza nella cache frammenti o immagini.

**** Intervallo pulizia (secondi): Specifica la frequenza con cui il servizio Forms rimuove i vecchi file cache non validi. Il servizio Forms non rimuove i file di cache validi. Se si modifica l&#39;intervallo di pulizia, riavviare il servizio Forms per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare Avviare o arrestare i servizi associati ai moduli AEM per le istruzioni. Il valore predefinito è 600 secondi.

## Considerazioni sul clustering per le cache {#clustering-considerations-for-caches}

In un ambiente cluster, ogni nodo mantiene la propria cache in memoria e disco. Il contenuto della cache di ciascun nodo dipende da quali moduli è stato eseguito il rendering su tale nodo.

La posizione della cache deve essere identica (lo stesso disco e lo stesso percorso) su ciascun nodo del cluster. Non inserite la cache nell&#39;archivio condiviso.

Se si utilizza la pagina Moduli nella console di amministrazione per modificare le impostazioni della cache per un particolare nodo, le impostazioni della cache per altri nodi vengono aggiornate quando una richiesta va a tale nodo. Questo comportamento si applica anche al pulsante Ripristina cache. Se fate clic sul pulsante Ripristina cache per un nodo, la cache viene immediatamente rimossa da tale nodo. La cache degli altri nodi viene cancellata quando una richiesta arriva a tale nodo.
