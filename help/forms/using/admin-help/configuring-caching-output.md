---
title: Configurazione della memorizzazione in cache per l’output
description: Il servizio di output memorizza nella cache le progettazioni, i frammenti e le immagini dei moduli. Scopri come configurare la memorizzazione in cache per l’output.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1454'
ht-degree: 100%

---

# Configurazione della memorizzazione in cache per l’output  {#configuring-caching-for-output}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il servizio di output unisce i dati del modulo XML con una progettazione del modulo creata nel designer per creare un flusso di output di documenti in vari formati.

La pagina Output nella console di amministrazione contiene le impostazioni che controllano il modo in cui il servizio di output memorizza gli elementi nella cache. Puoi regolare queste impostazioni per ottimizzare le prestazioni del servizio di output.

Il servizio di output memorizza nella cache i seguenti elementi:

* **progettazioni moduli:** il servizio di output memorizza nella cache le progettazioni dei moduli recuperate dall’archivio o dalle origini HTTP. Questa memorizzazione in cache migliora le prestazioni perché, per le successive richieste di rendering, il servizio di output recupera la progettazione del modulo dalla cache anziché dall’archivio.
* **frammenti e immagini:** il servizio di output può memorizzare nella cache frammenti e immagini utilizzati nelle progettazioni di moduli. Quando il servizio di output memorizza nella cache questi oggetti, migliora le prestazioni perché i frammenti e le immagini vengono letti dall’archivio solo alla prima richiesta.

L’output memorizza la cache in due posizioni:

* **in memoria:** gli elementi sono archiviati nella memoria per l’accesso rapido. La cache in memoria ha dimensioni limitate e viene eliminata al riavvio del server.
* **su disco:** gli elementi sono archiviati nel file system del server. La cache del disco ha una capacità maggiore della cache in memoria e viene mantenuta al riavvio del server. La posizione della cache del disco dipende dal server applicazioni. Per informazioni sulla modifica del percorso della cache del disco, comsulta [Specificare le posizioni dei file per l’output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Specifica della modalità cache {#specifying-the-cache-mode}

L&#39;output supporta due modalità di memorizzazione nella cache:

* incondizionato
* utilizzo del punto di controllo della cache

Se passi da una modalità di memorizzazione nella cache all’altra, riavvia il servizio di output per rendere effettiva la modifica. Per riavviare il servizio, utilizza Workbench o consulta [Avviare o arrestare i servizi associati ai moduli di AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) per le istruzioni.

L’orario del punto di controllo della cache viene reimpostato automaticamente quando si passa da una modalità all’altra.

### Utilizzo della memorizzazione nella cache incondizionata {#using-unconditional-caching}

In questa modalità, quando il servizio di output riceve una richiesta, convalida le risorse necessarie (progettazione del modulo ed eventuali risorse correlate, come frammenti e immagini). Il servizio di output confronta la marca temporale delle risorse nell’archivio con la marca temporale delle risorse nella cache. Se la risorsa nella cache è meno recente, il servizio di output la aggiorna.

Questa modalità di memorizzazione nella cache garantisce l’utilizzo delle risorse più recenti. Tuttavia, le prestazioni sono influenzate dal fatto che il servizio di output convalida gli elementi memorizzati in cache rispetto all’archivio con ogni richiesta. Questa modalità di memorizzazione nella cache è adatta per gli ambienti di sviluppo e staging in cui le risorse vengono aggiornate frequentemente e le prestazioni non rappresentano un problema primario.

**Specificare la memorizzazione nella cache incondizionata**

1. Nella Console di amministrazione, fai clic su Servizi > Output.
1. In Impostazioni controllo cache di output, seleziona Incondizionatamente e fai clic su Salva.

### Utilizzare il punto di controllo della cache {#use-the-cache-check-point}

In questa modalità, il servizio di output controlla l’archivio solo per le versioni più recenti delle risorse quando la marca temporale della risorsa memorizzata in cache è precedente all’ora del punto di controllo della cache. L’ora dell’ultimo punto di controllo della cache viene visualizzata nella pagina Output della console di amministrazione.

Utilizza questa modalità cache in ambienti di produzione ad alte prestazioni in cui le prestazioni sono un problema e le modifiche alle risorse non sono frequenti. Puoi reimpostare l’ora del punto di controllo della cache quando desideri distribuire eventuali modifiche apportate alle risorse dell’archivio.

**Specificare l’utilizzo di un punto di controllo della cache**

1. Nella console di amministrazione, fai clic su Servizi > Output.
1. In Impostazioni controllo cache di output, seleziona Solo se l’ultima convalida è stata eseguita prima dell’ora del punto di controllo della cache e fai clic su Salva.

**Reimpostare il punto di controllo della cache**

1. Nella Console di amministrazione, fai clic su Servizi > Output.
1. In Impostazioni controllo cache di output, fai clic su Punto di controllo cache.

### Reimpostare i contenuti della cache {#reset-the-cache-contents}

Puoi cancellare i contenuti della cache in qualsiasi momento. Dopo un ripristino della cache, la prima richiesta per ciascun modulo è più lenta perché il servizio di output esegue un rendering completo e crea nuovo contenuto per la cache.

1. Nella Console di amministrazione, fai clic su Servizi > Output.
1. In Impostazioni di controllo della cache di output fai clic su Reimposta cache.

## Configurazione delle impostazioni della cache {#configuring-cache-settings}

Puoi specificare le impostazioni utilizzate da Output per la memorizzazione in cache, in modo da ottimizzare le prestazioni dell’ambiente AEM Forms.

Per accedere a queste impostazioni, nella console di amministrazione fai clic su Servizi > Output.

>[!NOTE]
>
>I requisiti del disco per la cache devono essere uguali all’archivio.

### Specifica delle impostazioni globali della cache {#specifying-global-cache-settings}

Le impostazioni nell’area **Impostazioni globali della cache** interessano tutti i tipi di cache. Se modifichi una di queste impostazioni, riavvia il servizio di output per rendere effettiva la modifica. Per riavviare il servizio, utilizza Workbench o consulta le istruzioni in [Avviare o arrestare i servizi associati ai moduli di AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules).

**Dimensione massima del documento nella cache (KB):** dimensione massima, in kilobyte, della progettazione di un modulo o di un’altra risorsa che può essere archiviata in qualsiasi cache in memoria. Si tratta di un’impostazione globale applicabile a tutte le cache in memoria. Se la risorsa è maggiore di questo valore, non viene memorizzata nella cache. Il valore predefinito è 1024 kilobyte. Questa impostazione non influisce sulla cache del disco.

**Cache di rendering dei moduli abilitata:** per impostazione predefinita, questa opzione è selezionata, pertanto i moduli sottoposti a rendering vengono memorizzati nella cache per il recupero successivo. Questa impostazione ha scarso effetto sulle prestazioni del servizio di output perché non memorizza in cache i documenti non interattivi. Questa opzione ha effetto quando utilizzi il servizio di output per i documenti non interattivi sottoposti a rendering sul client.

### Memorizzazione in cache delle progettazioni dei moduli {#caching-form-designs}

Quando il servizio di output riceve una richiesta di rendering, recupera la progettazione del modulo dall’archivio o da un’origine HTTP e la memorizza nella cache. Questa memorizzazione in cache migliora le prestazioni perché, per le successive richieste di rendering, il servizio di output recupera la progettazione del modulo dalla cache anziché dall’archivio.

Il servizio di output memorizza sempre nella cache le progettazioni dei moduli sul disco. Se le progettazioni dei moduli sono memorizzate sul server, tali file vengono considerati come cache del disco. Il servizio di output memorizza nella cache anche le progettazioni dei moduli in memoria, in base all’impostazione nell’area **Cache dei modelli di memoria**. Se modifichi una di queste impostazioni, riavvia il servizio di output per rendere effettiva la modifica. Per riavviare il servizio, utilizza Workbench o consulta le istruzioni in [Avviare o arrestare i servizi associati ai moduli di AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules).

**Dimensioni della cache per la configurazione del modello:** numero massimo di oggetti configurazione del modello da conservare in memoria. Il valore predefinito è 100. È consigliabile impostarlo su un valore maggiore o uguale al valore della dimensione della cache del modello. Questa impostazione non influisce sulla cache del disco.

**Dimensione della cache del modello:** numero massimo di oggetti contenuto del modello da conservare in memoria. Il valore predefinito è 100. Questa impostazione non influisce sulla cache del disco.

**Abilitato:** questa casella di controllo è selezionata per impostazione predefinita, pertanto i modelli dei moduli sono memorizzati nella cache in memoria. Se questa opzione non è selezionata, i modelli dei moduli vengono memorizzati nella cache solo su disco.

### Memorizzazione in cache di frammenti e immagini {#caching-fragments-and-images}

Il servizio di output memorizza nella cache frammenti e immagini utilizzati nelle progettazioni dei moduli su disco. Questa operazione migliora le prestazioni perché i frammenti e le immagini vengono letti dall’archivio solo alla prima richiesta. Nelle richieste successive, il servizio di output legge i frammenti e le immagini dalla cache del disco. I frammenti e le immagini vengono memorizzati nella cache solo su disco e non in memoria.

Puoi utilizzare le seguenti impostazioni per controllare la memorizzazione nella cache su disco di frammenti e immagini. Queste impostazioni si trovano nell’area **Impostazioni della cache per le risorse del modello**:

**Memorizzazione in cache delle risorse** Seleziona una delle opzioni seguenti dall’elenco:

**Abilitato per frammenti e immagini:** il servizio di output memorizza nella cache frammenti e immagini. Questa è l’opzione predefinita.

**Abilitato per frammenti:** il servizio di output memorizza nella cache i frammenti, ma non le immagini.

**Disabilitato:** il servizio di output non memorizza nella cache frammenti o immagini.

**Intervallo di pulizia (secondi):** specifica la frequenza con cui il servizio di output rimuove i vecchi file della cache non validi. Il servizio di output non rimuove i file di cache validi. Se modifichi l’intervallo di pulizia, riavvia il servizio di output per rendere effettiva la modifica. Per riavviare il servizio, utilizza Workbench o consulta la sezione Avviare o interrompere i servizi associati ai moduli di AEM Forms per istruzioni.

## Considerazioni sul clustering per le cache {#clustering-considerations-for-caches}

In un ambiente cluster, ogni nodo gestisce la propria cache in memoria e su disco. Il contenuto della cache su ciascun nodo dipende dai moduli di cui è stato eseguito il rendering su tale nodo.

La posizione della cache deve essere identica (stesso disco e percorso) in ciascun nodo del cluster. Non posizionare la cache nell’archiviazione condivisa.

Se utilizzi la pagina Output nella console di amministrazione per modificare le impostazioni della cache per un nodo specifico, quando una richiesta viene indirizzata a tale nodo le impostazioni della cache sugli altri nodi vengono aggiornate. Questo comportamento si applica anche al pulsante Reimposta cache. Se fai clic sul pulsante Reimposta cache per un nodo, la cache viene rimossa immediatamente da quel nodo. La cache sugli altri nodi viene cancellata quando una richiesta viene indirizzata a quel nodo.
