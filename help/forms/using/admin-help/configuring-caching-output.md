---
title: Configurazione della memorizzazione nella cache per Output
seo-title: Configurazione della memorizzazione nella cache per Output
description: Il servizio Output memorizza nella cache le strutture del modulo, i frammenti e le immagini. Scoprite come configurare la memorizzazione nella cache per l'output.
seo-description: Il servizio Output memorizza nella cache le strutture del modulo, i frammenti e le immagini. Scoprite come configurare la memorizzazione nella cache per l'output.
uuid: 00bffeb5-c9c4-4a46-98b5-e14ec9f4514e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5398abd-f62c-485d-9f4b-a316c0de2b6b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---


# Configurazione della memorizzazione nella cache per l&#39;output {#configuring-caching-for-output}

Il servizio Output unisce i dati del modulo XML a una struttura del modulo creata in Designer per creare un flusso di output del documento in vari formati.

La pagina Output nella console di amministrazione contiene impostazioni che controllano il modo in cui il servizio Output memorizza gli elementi nella cache. È possibile regolare queste impostazioni per ottimizzare le prestazioni del servizio Output.

Il servizio Output memorizza nella cache i seguenti elementi:

* **strutture del modulo:** il servizio Output memorizza nella cache le strutture del modulo recuperate dall&#39;archivio o da origini HTTP. Questo caching migliora le prestazioni perché per richieste di rendering successive, il servizio Output recupera la struttura del modulo dalla cache anziché dall&#39;archivio.
* **frammenti e immagini:** Il servizio Output può memorizzare nella cache frammenti e immagini utilizzati nelle strutture del modulo. Quando il servizio Output memorizza nella cache questi oggetti, migliora le prestazioni perché i frammenti e le immagini vengono letti solo dalla directory archivio alla prima richiesta.

Output memorizza la cache in due posizioni:

* **in memoria:** Gli elementi vengono memorizzati per un accesso rapido. La cache in memoria ha dimensioni limitate e viene eliminata al riavvio del server.
* **su disco:** Gli elementi sono memorizzati nel file system del server. La cache del disco ha una capacità maggiore della cache in memoria e viene mantenuta al riavvio del server. La posizione della cache del disco dipende dal server dell’applicazione in uso. Per informazioni sulla modifica della posizione della cache del disco, vedere [Specificare le posizioni dei file per Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Specifica della modalità cache {#specifying-the-cache-mode}

Output supporta due modalità di caching:

* incondizionato
* utilizzo del punto di controllo della cache

Se si passa da una modalità cache all&#39;altra, riavviare il servizio Output per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per le istruzioni.

Il tempo del punto di controllo della cache viene reimpostato automaticamente quando si passa da una modalità all&#39;altra.

### Utilizzo della cache incondizionata {#using-unconditional-caching}

In questa modalità, quando il servizio Output riceve una richiesta, convalida le risorse necessarie (struttura del modulo ed eventuali risorse correlate, ad esempio frammenti e immagini). Il servizio Output confronta la marca temporale delle risorse nell&#39;archivio con la marca temporale delle risorse presenti nella cache. Se la risorsa nella cache è precedente, il servizio Output la aggiorna.

Questa modalità cache garantisce l’utilizzo delle risorse più recenti. Tuttavia, le prestazioni sono influenzate dal fatto che il servizio Output convalida gli elementi memorizzati nella cache rispetto al repository con ogni richiesta. Questa modalità cache è adatta per ambienti di sviluppo e gestione temporanea in cui le risorse vengono aggiornate frequentemente e le prestazioni non rappresentano un problema principale.

**Specificare la cache non condizionale**

1. Nella console di amministrazione, fate clic su Servizi > output.
1. In Impostazioni controllo cache di output, selezionare Senza condizioni e fare clic su Salva.

### Utilizzare il punto di controllo della cache {#use-the-cache-check-point}

In questa modalità, il servizio Output verifica nell&#39;archivio solo la disponibilità di nuove versioni delle risorse quando la marca temporale della risorsa memorizzata nella cache è maggiore dell&#39;ora del punto di controllo della cache. L&#39;ora dell&#39;ultimo punto di controllo della cache viene visualizzata nella pagina Output in Admin Console.

Utilizzate questa modalità cache in ambienti di produzione ad alte prestazioni in cui le prestazioni sono un problema e le modifiche alle risorse non sono frequenti. È possibile reimpostare l&#39;ora del punto di controllo della cache quando si desidera distribuire le modifiche apportate alle risorse del repository.

**Specificare l&#39;utilizzo di un punto di controllo della cache**

1. In Admin Console, fai clic su Servizi > output.
1. In Impostazioni controllo cache di output, selezionare Solo se l&#39;ultima convalida è stata eseguita prima del tempo del punto di controllo della cache e fare clic su Salva.

**Ripristino del punto di controllo della cache**

1. Nella console di amministrazione, fate clic su Servizi > output.
1. In Impostazioni controllo cache di output, fare clic su Punto di controllo cache.

### Reimpostare il contenuto della cache {#reset-the-cache-contents}

Potete cancellare il contenuto della cache in qualsiasi momento. Dopo la reimpostazione della cache, la prima richiesta per ciascun modulo è più lenta perché il servizio Output esegue un rendering completo e crea nuovo contenuto della cache.

1. Nella console di amministrazione, fate clic su Servizi > output.
1. In Impostazioni controllo cache di output, fare clic su Reimposta cache.

## Configurazione delle impostazioni della cache {#configuring-cache-settings}

È possibile specificare le impostazioni utilizzate da Output per il caching, che consentono di ottimizzare le prestazioni dell&#39;ambiente dei moduli AEM.

Per accedere a queste impostazioni, nella console di amministrazione fare clic su Servizi > output.

>[!NOTE]
>
>I requisiti del disco per la cache devono essere uguali al repository.

### Specifica delle impostazioni globali della cache {#specifying-global-cache-settings}

Le impostazioni nell&#39;area **Impostazioni cache globale** interessano tutti i tipi di cache. Se si modifica una di queste impostazioni, riavviare il servizio Output per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per le istruzioni.

**Dimensione massima documento cache (KB):** dimensione massima, in kilobyte, di una struttura del modulo o di altre risorse che è possibile memorizzare in qualsiasi cache in memoria. Si tratta di un&#39;impostazione globale che si applica a tutte le cache in memoria. Se la risorsa è maggiore di questo valore, non viene memorizzata nella cache. Il valore predefinito è 1024 kilobyte. Questa impostazione non influisce sulla cache del disco.

**Cache di rendering del modulo abilitata:** per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli sottoposti a rendering vengono memorizzati nella cache per il successivo recupero. Questa impostazione ha poco effetto sulle prestazioni del servizio Output perché non memorizza nella cache i documenti non interattivi. Questa opzione ha un effetto quando si utilizza il servizio Output per documenti non interattivi di cui viene eseguito il rendering sul client.

### Memorizzazione delle strutture del modulo nella cache {#caching-form-designs}

Quando il servizio Output riceve una richiesta di rendering, recupera la struttura del modulo dall&#39;archivio o da un&#39;origine HTTP e la memorizza nella cache. Questo caching migliora le prestazioni perché per richieste di rendering successive, il servizio Output recupera la struttura del modulo dalla cache anziché dall&#39;archivio.

Il servizio Output memorizza sempre nella cache le strutture del modulo su disco. Se le strutture del modulo sono memorizzate sul server, tali file vengono considerati cache del disco. Il servizio Output memorizza anche le strutture del modulo nella cache, in base alle impostazioni specificate nell&#39;area **In Memory Template Cache**. Se si modifica una di queste impostazioni, riavviare il servizio Output affinché la modifica abbia effetto. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per le istruzioni.

**Dimensione cache configurazione modello:** il numero massimo di oggetti di configurazione modello da tenere in memoria. Il valore predefinito è 100. È consigliabile impostare questo valore maggiore o uguale al valore Dimensione cache modello. Questa impostazione non influisce sulla cache del disco.

**Dimensione cache modello:** il numero massimo di oggetti di contenuto modello da tenere in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**Abilitato:** Per impostazione predefinita, questa casella di controllo è selezionata, il che significa che i modelli di modulo sono memorizzati nella cache. Se questa opzione non è selezionata, i modelli di modulo sono memorizzati nella cache solo sul disco.

### Memorizzazione nella cache di frammenti e immagini {#caching-fragments-and-images}

Il servizio Output memorizza nella cache frammenti e immagini utilizzati nelle strutture del modulo su disco. Ciò migliora le prestazioni perché i frammenti e le immagini vengono letti solo dalla directory archivio alla prima richiesta. Quindi, su richieste successive, il servizio Output legge frammenti e immagini dalla cache del disco. I frammenti e le immagini sono memorizzati nella cache solo su disco e non nella memoria.

Per controllare il caching su disco di frammenti e immagini è possibile utilizzare le seguenti impostazioni. Queste impostazioni si trovano nell&#39;area **Impostazioni cache delle risorse dei modelli**:

**Memorizzazione** nella cache delle risorseSelezionare una delle seguenti opzioni dall&#39;elenco:

**Abilitato per frammenti e immagini:** il servizio Output memorizza nella cache frammenti e immagini. Questa è l&#39;opzione predefinita.

**Abilitato per i frammenti:** il servizio Output memorizza nella cache i frammenti, ma non le immagini.

**Disattivato:** il servizio Output non memorizza nella cache frammenti o immagini.

**Intervallo di pulizia (secondi):** specifica la frequenza con cui il servizio Output rimuove i vecchi file cache non validi. Il servizio Output non rimuove i file di cache validi. Se si modifica l&#39;intervallo di pulizia, riavviare il servizio Output per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare Avviare o arrestare i servizi associati ai moduli AEM per istruzioni.

## Considerazioni sul clustering per le cache {#clustering-considerations-for-caches}

In un ambiente cluster, ogni nodo mantiene la propria cache in memoria e disco. Il contenuto della cache di ciascun nodo dipende da quali moduli è stato eseguito il rendering su tale nodo.

La posizione della cache deve essere identica (lo stesso disco e lo stesso percorso) su ciascun nodo del cluster. Non inserite la cache nell&#39;archivio condiviso.

Se utilizzate la pagina Output nella console di amministrazione per modificare le impostazioni della cache per un particolare nodo, le impostazioni della cache per altri nodi vengono aggiornate quando una richiesta va a tale nodo. Questo comportamento si applica anche al pulsante Ripristina cache. Se fate clic sul pulsante Ripristina cache per un nodo, la cache viene immediatamente rimossa da tale nodo. La cache degli altri nodi viene cancellata quando una richiesta arriva a tale nodo.
