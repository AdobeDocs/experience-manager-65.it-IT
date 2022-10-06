---
title: Configurazione della memorizzazione in cache per l’output
seo-title: Configuring caching for Output
description: Il servizio Output memorizza in cache le strutture del modulo, i frammenti e le immagini. Scopri come configurare la memorizzazione in cache per l’output.
seo-description: The Output service caches the form designs, fragments and images. Learn how to configure the caching for output.
uuid: 00bffeb5-c9c4-4a46-98b5-e14ec9f4514e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5398abd-f62c-485d-9f4b-a316c0de2b6b
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---

# Configurazione della memorizzazione in cache per l’output  {#configuring-caching-for-output}

Il servizio Output unisce i dati del modulo XML a una struttura del modulo creata in Designer per creare un flusso di output del documento in vari formati.

La pagina Output nella console di amministrazione contiene impostazioni che controllano il modo in cui il servizio Output memorizza in cache gli elementi. È possibile regolare queste impostazioni per ottimizzare le prestazioni del servizio Output.

Il servizio Output memorizza in cache i seguenti elementi:

* **strutture del modulo:** Il servizio Output memorizza in cache le strutture del modulo recuperate dall&#39;archivio o da origini HTTP. Questo caching migliora le prestazioni perché per le richieste di rendering successive, il servizio Output recupera la struttura del modulo dalla cache anziché dall’archivio.
* **frammenti e immagini:** Il servizio Output può memorizzare nella cache frammenti e immagini utilizzati nelle strutture del modulo. Quando il servizio Output memorizza in cache questi oggetti, migliora le prestazioni perché i frammenti e le immagini vengono letti dall&#39;archivio solo alla prima richiesta.

Output memorizza la cache in due posizioni:

* **in memoria:** Gli elementi vengono memorizzati in memoria per un accesso rapido. La cache in memoria ha una dimensione limitata e viene eliminata al riavvio del server.
* **su disco:** Gli elementi vengono memorizzati nel file system del server. La cache del disco ha una capacità maggiore della cache in memoria e viene mantenuta al riavvio del server. La posizione della cache del disco dipende dal server dell&#39;applicazione. Per informazioni sulla modifica della posizione della cache del disco, vedi [Specificare le posizioni dei file per l&#39;output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Specifica della modalità cache {#specifying-the-cache-mode}

L&#39;output supporta due modalità di memorizzazione in cache:

* incondizionato
* utilizzo del punto di controllo della cache

Se si passa da una modalità cache all&#39;altra, riavviare il servizio Output per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

Il tempo del punto di controllo della cache viene reimpostato automaticamente quando si passa da una modalità all&#39;altra.

### Utilizzo della memorizzazione in cache incondizionata {#using-unconditional-caching}

In questa modalità, quando il servizio Output riceve una richiesta, convalida le risorse necessarie (struttura del modulo e tutte le risorse correlate, come frammenti e immagini). Il servizio Output confronta la marca temporale delle risorse nell’archivio con la marca temporale delle risorse nella cache. Se la risorsa nella cache è precedente, il servizio Output la aggiorna.

Questa modalità cache garantisce l’utilizzo delle risorse più recenti. Tuttavia, le prestazioni sono influenzate dal fatto che il servizio Output convalida gli elementi memorizzati nella cache rispetto al repository con ogni richiesta. Questa modalità cache è adatta per ambienti di sviluppo e staging in cui le risorse vengono aggiornate frequentemente e le prestazioni non rappresentano un problema primario.

**Specificare la memorizzazione in cache incondizionata**

1. Nella console di amministrazione, fai clic su Servizi > output.
1. In Impostazioni controllo cache di output, selezionare Senza condizioni e fare clic su Salva.

### Utilizza il punto di controllo della cache {#use-the-cache-check-point}

In questa modalità, il servizio di output controlla nell’archivio solo la disponibilità di versioni più recenti delle risorse quando la marca temporale della risorsa memorizzata nella cache è maggiore del tempo del punto di controllo della cache. L’ora dell’ultimo punto di controllo della cache viene visualizzata nella pagina Output in Admin Console.

Utilizza questa modalità cache in ambienti di produzione ad alte prestazioni in cui le prestazioni rappresentano un problema e le modifiche alle risorse non sono frequenti. È possibile reimpostare il momento del controllo della cache quando si desidera distribuire eventuali modifiche apportate alle risorse del repository.

**Specificare l&#39;utilizzo di un punto di controllo della cache**

1. In Console di amministrazione, fai clic su Servizi > output.
1. In Impostazioni controllo cache di output, selezionare Solo se l&#39;ultima convalida è stata eseguita prima dell&#39;ora del punto di controllo della cache e fare clic su Salva.

**Reimposta il punto di controllo della cache**

1. Nella console di amministrazione, fai clic su Servizi > output.
1. In Impostazioni controllo cache di output fare clic su Punto di controllo cache.

### Reimpostare il contenuto della cache {#reset-the-cache-contents}

Puoi cancellare il contenuto della cache in qualsiasi momento. Dopo una reimpostazione della cache, la prima richiesta per ciascun modulo è più lenta perché il servizio Output esegue un rendering completo e crea nuovo contenuto della cache.

1. Nella console di amministrazione, fai clic su Servizi > output.
1. In Impostazioni controllo cache di output, fare clic su Ripristina cache.

## Configurazione delle impostazioni della cache {#configuring-cache-settings}

È possibile specificare le impostazioni utilizzate da Output per la memorizzazione in cache, che possono ottimizzare le prestazioni dell’ambiente dei moduli AEM.

Per accedere a queste impostazioni, nella console di amministrazione, fai clic su Servizi > output.

>[!NOTE]
>
>I requisiti del disco per la cache devono essere uguali all’archivio.

### Specifica delle impostazioni della cache globale {#specifying-global-cache-settings}

Le impostazioni nel **Impostazioni della cache globale** l’area interessa tutti i tipi di cache. Se si modifica una di queste impostazioni, riavviare il servizio Output per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Dimensione massima documento cache (KB):** Dimensione massima, in kilobyte, di una struttura del modulo o di un’altra risorsa memorizzabile in qualsiasi cache in memoria. Si tratta di un’impostazione globale che si applica a tutte le cache in memoria. Se la risorsa è maggiore di questo valore, non viene memorizzata nella cache. Il valore predefinito è 1024 kilobyte. Questa impostazione non influisce sulla cache del disco.

**Cache di rendering del modulo abilitata:** Per impostazione predefinita, questa opzione è selezionata, il che significa che i moduli di cui è stato effettuato il rendering vengono memorizzati nella cache per il successivo recupero. Questa impostazione ha un effetto minimo sulle prestazioni del servizio Output perché non memorizza in cache i documenti non interattivi. Questa opzione ha un effetto quando si utilizza il servizio Output per documenti non interattivi di cui è stato eseguito il rendering sul client.

### Schede del modulo di memorizzazione nella cache {#caching-form-designs}

Quando il servizio Output riceve una richiesta di rendering, recupera la struttura del modulo dall’archivio o da un’origine HTTP e la memorizza nella cache. Questo caching migliora le prestazioni perché per le richieste di rendering successive, il servizio Output recupera la struttura del modulo dalla cache anziché dall’archivio.

Il servizio Output memorizza sempre in cache le strutture del modulo su disco. Se le strutture del modulo sono memorizzate sul server, tali file vengono considerati come cache del disco. Il servizio Output memorizza anche le strutture del modulo nella cache, in base all&#39;impostazione in **Nella cache del modello di memoria** area. Se si modifica una di queste impostazioni, riavviare il servizio Output per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare [Avviare o arrestare i servizi associati ai moduli AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per istruzioni.

**Dimensione cache configurazione modello:** Il numero massimo di oggetti di configurazione del modello da tenere in memoria. Il valore predefinito è 100. È consigliabile impostare questo valore maggiore o uguale al valore Dimensione cache modello. Questa impostazione non influisce sulla cache del disco.

**Dimensione cache modello:** Il numero massimo di oggetti di contenuto del modello da tenere in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**Abilitato:** Per impostazione predefinita, questa casella di controllo è selezionata, il che significa che i modelli di modulo sono memorizzati nella cache. Se questa opzione non è selezionata, i modelli di modulo vengono memorizzati nella cache solo su disco.

### Memorizzazione in cache di frammenti e immagini {#caching-fragments-and-images}

Il servizio Output memorizza in cache frammenti e immagini utilizzati nelle strutture del modulo su disco. Ciò migliora le prestazioni perché i frammenti e le immagini vengono letti dall’archivio solo alla prima richiesta. Successivamente, nelle richieste successive, il servizio Output legge frammenti e immagini dalla cache del disco. I frammenti e le immagini sono memorizzati nella cache solo su disco e non in memoria.

È possibile utilizzare le seguenti impostazioni per controllare la memorizzazione in cache su disco di frammenti e immagini. Queste impostazioni si trovano nella **Impostazioni della cache delle risorse di modello** area:

**Memorizzazione in cache delle risorse** Selezionare una delle seguenti opzioni dall’elenco:

**Abilitato per frammenti e immagini:** Il servizio Output memorizza in cache frammenti e immagini. Questa è l’opzione predefinita.

**Abilitato per i frammenti:** Il servizio Output memorizza in cache frammenti, ma non immagini.

**Disabilitata:** Il servizio Output non memorizza in cache frammenti o immagini.

**Intervallo di pulizia (secondi):** Specifica la frequenza con cui il servizio Output rimuove i vecchi file di cache non validi. Il servizio di output non rimuove i file di cache validi. Se si modifica l&#39;intervallo di pulizia, riavviare il servizio Output per rendere effettiva la modifica. Per riavviare il servizio, utilizzare Workbench o consultare Avviare o arrestare i servizi associati ai moduli AEM per le istruzioni.

## Considerazioni sul clustering per le cache {#clustering-considerations-for-caches}

In un ambiente cluster, ogni nodo mantiene la propria cache in memoria e disco. Il contenuto della cache di ciascun nodo dipende da quali moduli sono stati sottoposti a rendering su quel nodo.

La posizione della cache deve essere identica (stesso disco e percorso) su ciascun nodo del cluster. Non inserire la cache nell&#39;archiviazione condivisa.

Se utilizzi la pagina Output nella console di amministrazione per modificare le impostazioni della cache per un particolare nodo, le impostazioni della cache su altri nodi vengono aggiornate quando una richiesta passa a quel nodo. Questo comportamento si applica anche al pulsante Ripristina cache . Se fai clic sul pulsante Ripristina cache per un nodo, la cache viene immediatamente rimossa da quel nodo. La cache su altri nodi viene cancellata quando una richiesta arriva a quel nodo.
