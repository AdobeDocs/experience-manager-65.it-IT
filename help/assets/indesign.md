---
title: Integrare [!DNL Assets] con [!DNL InDesign Server]
description: Scopri come integrare [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 4%

---

# Integrare [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilizza:

* Un proxy per distribuire il carico di alcune attività di elaborazione. Un proxy è un [!DNL Experience Manager] istanza che comunica con un proxy worker per eseguire un&#39;attività specifica e altre [!DNL Experience Manager] per fornire i risultati.
* Un processo di lavoro proxy per definire e gestire un’attività specifica.
Questi possono coprire un&#39;ampia gamma di compiti; ad esempio, utilizzando un [!DNL InDesign Server] per elaborare i file.

Per caricare completamente i file in [!DNL Experience Manager Assets] creato con [!DNL Adobe InDesign] viene utilizzato un proxy. Questo utilizza un proxy worker per comunicare con [!DNL Adobe InDesign Server], dove [script](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) vengono eseguiti per estrarre i metadati e generare diverse rappresentazioni per [!DNL Experience Manager Assets]. Il proxy worker consente la comunicazione bidirezionale tra [!DNL InDesign Server] e [!DNL Experience Manager] istanze in una configurazione cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] viene offerto come due offerte separate. [Adobe InDesign](https://www.adobe.com/products/indesign.html) app desktop utilizzata per progettare layout di pagina per la stampa e la distribuzione digitale. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) consente di creare a livello di programmazione documenti automatizzati in base a ciò che è stato creato con [!DNL InDesign]. Opera come servizio che offre un’interfaccia ai suoi [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.Gli script vengono scritti in [!DNL ExtendScript], simile a [!DNL JavaScript]. Per informazioni su [!DNL InDesign] script vedi [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Come funziona l’estrazione {#how-the-extraction-works}

La [!DNL Adobe InDesign Server] può essere integrato con [!DNL Experience Manager Assets] in modo che i file INDD creati con [!DNL InDesign] possono essere caricati, generate rappresentazioni, tutti i file multimediali estratti (ad esempio, video) e memorizzati come risorse:

>[!NOTE]
>
>Versioni precedenti di [!DNL Experience Manager] sono stati in grado di estrarre XMP e la miniatura, ora tutti i supporti possono essere estratti.

1. Carica il file INDD in [!DNL Experience Manager Assets].
1. Un framework invia script di comando al [!DNL InDesign Server] tramite SOAP (Simple Object Access Protocol).
Questo script di comando:

   * Recupera il file INDD.
   * Esegui [!DNL InDesign Server] comandi:

      * Vengono estratti la struttura, il testo e tutti i file multimediali.
      * Vengono generati rendering di PDF e JPG.
      * Vengono generati rendering HTML e IDML.
   * Ripubblicare i file risultanti in [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML è un formato basato su XML che esegue il rendering di tutti i contenuti del [!DNL InDesign] file. Viene memorizzato come pacchetto compresso utilizzando [ZIP](https://www.techterms.com/definition/zip) compressione. Per ulteriori informazioni, consulta [InDesign Interchange Formats INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Se la [!DNL InDesign Server] non è installato o non è configurato, è comunque possibile caricare un file INDD in [!DNL Experience Manager]. Tuttavia, le rappresentazioni generate saranno limitate a PNG e JPEG. Non sarà possibile generare rappresentazioni di HTML, idml o pagina.

1. Dopo la generazione di estrazione e rendering:

   * La struttura viene replicata in un `cq:Page` (tipo di rendering).
   * Il testo e i file estratti vengono memorizzati in [!DNL Experience Manager Assets].
   * Tutte le rappresentazioni sono memorizzate in [!DNL Experience Manager Assets], nella risorsa stessa.

## Integrare le [!DNL InDesign Server] con Experience Manager {#integrating-the-indesign-server-with-aem}

Per integrare [!DNL InDesign Server] per l&#39;uso con [!DNL Experience Manager Assets] e dopo aver configurato il proxy, devi:

1. [Installare InDesign Server](#installing-the-indesign-server).
1. Se necessario, [configurare il flusso di lavoro Experience Manager Assets](#configuring-the-aem-assets-workflow).
Ciò è necessario solo se i valori predefiniti non sono appropriati per l’istanza.
1. Configura un [proxy worker per InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installa il [!DNL InDesign Server] {#installing-the-indesign-server}

Per installare e avviare il [!DNL InDesign Server] per l&#39;uso con [!DNL Experience Manager]:

1. Scarica e installa la [!DNL InDesign Server].

1. Se necessario, puoi personalizzare la configurazione del [!DNL InDesign Server] istanza.

1. Dalla riga di comando, avvia il server:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Verrà avviato il server con il plug-in SOAP in ascolto sulla porta 8080. Tutti i messaggi e gli output di log vengono scritti direttamente nella finestra dei comandi.

   >[!NOTE]
   >
   >Se si desidera salvare i messaggi di output in un file, utilizzare il reindirizzamento; ad esempio, in Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configura le [!DNL Experience Manager Assets] workflow {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispone di un flusso di lavoro preconfigurato **[!UICONTROL Risorsa di aggiornamento DAM]**, che prevede diversi passaggi di processo specifici per [!DNL InDesign]:

* [Estrazione file multimediali](#media-extraction)
* [Estrazione pagina](#page-extraction)

Questo flusso di lavoro è configurato con valori predefiniti che possono essere adattati per la configurazione sulle varie istanze di authoring (si tratta di un flusso di lavoro standard, quindi ulteriori informazioni sono disponibili in [Modifica di un flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se si utilizzano i valori predefiniti (inclusa la porta SOAP), non è necessaria alcuna configurazione.

Dopo la configurazione, il caricamento [!DNL InDesign] file in [!DNL Experience Manager Assets] (con uno dei metodi consueti) attiva il flusso di lavoro per elaborare la risorsa e preparare le varie rappresentazioni. Verifica la configurazione caricando un file INDD in [!DNL Experience Manager Assets] per confermare che visualizzi le diverse rappresentazioni create da IDS in `<*your_asset*>.indd/Renditions`

#### Estrazione di file multimediali {#media-extraction}

Questo passaggio controlla l’estrazione dei file multimediali dal file INDD.

Per personalizzare, puoi modificare la scheda **[!UICONTROL Arguments (Argomenti)]** del passaggio **[!UICONTROL Estrazione file multimediali]**.

![Argomenti di estrazione file multimediali e percorsi di script](assets/media_extraction_arguments_scripts.png)

Argomenti di estrazione file multimediali e percorsi di script

* **Libreria ExtendScript**: Si tratta di una semplice libreria di metodi http get/post, necessaria per gli altri script.

* **Estendi script**: Qui è possibile specificare diverse combinazioni di script. Se desideri che gli script personalizzati vengano eseguiti nel [!DNL InDesign Server], salva gli script in `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Non modificare la libreria ExtendScript. Questa libreria fornisce la funzionalità HTTP necessaria per comunicare con Sling. Questa impostazione specifica la libreria da inviare al [!DNL InDesign Server] da usare lì.

La `ThumbnailExport.jsx` lo script eseguito dal passaggio del flusso di lavoro Estrazione file multimediali genera un rendering delle miniature in formato JPG. Questo rendering viene utilizzato dal passaggio del flusso di lavoro Elabora miniature per generare le rappresentazioni statiche richieste da [!DNL Experience Manager].

Puoi configurare il passaggio del flusso di lavoro Elabora miniature per generare rappresentazioni statiche con dimensioni diverse. Assicurati di non rimuovere i valori predefiniti, perché sono richiesti da [!DNL Experience Manager Assets] interfaccia. Infine, il passaggio del flusso di lavoro Elimina rappresentazione anteprima immagine rimuove il rendering delle miniature di JPG, in quanto non è più necessario.

#### Estrazione pagina {#page-extraction}

Questo crea un [!DNL Experience Manager] dagli elementi estratti. Un gestore estrazione viene utilizzato per estrarre dati da un rendering (attualmente HTML o IDML). Questi dati vengono quindi utilizzati per creare una pagina utilizzando PageBuilder.

Per personalizzare, è possibile modificare la scheda **[!UICONTROL Argomenti]** del passaggio **[!UICONTROL Estrazione pagina]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestore estrazione pagina**: Dall&#39;elenco a comparsa, selezionare il gestore che si desidera utilizzare. Un gestore estrazione opera su un rendering specifico, scelto da un `RenditionPicker` correlato (consulta l’API `ExtractionHandler`). In uno standard [!DNL Experience Manager] è disponibile l&#39;installazione seguente:
   * Maniglia di estrazione esportazione IDML: Opera sul `IDML` rendering generato nel passaggio MediaExtract.

* **Nome pagina**: Specifica il nome da assegnare alla pagina risultante. Se lasciato vuoto, il nome è &quot;page&quot; (o un derivato, se &quot;page&quot; esiste già).

* **Titolo pagina**: Specifica il titolo da assegnare alla pagina risultante.

* **Percorso principale pagina**: Percorso della posizione principale della pagina risultante. Se lasciato vuoto, verrà utilizzato il nodo contenente le rappresentazioni della risorsa.

* **Modello di pagina**: Modello da utilizzare per la generazione della pagina risultante.

* **Progettazione pagina**: Progettazione di pagina da utilizzare per la generazione della pagina risultante.

### Configura il proxy worker per [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Il processo di lavoro risiede nell&#39;istanza proxy.

1. Nella console Strumenti , espandi **[!UICONTROL Configurazioni Cloud Services]** nel riquadro a sinistra. Quindi espandi **[!UICONTROL Configurazione proxy cloud]**.

1. Per aprire la configurazione, fai doppio clic su **[!UICONTROL IDS worker]**.

1. Fai clic su **[!UICONTROL Modifica]** per aprire la finestra di dialogo di configurazione e definire le impostazioni richieste:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool IDS**
Endpoint SOAP da utilizzare per la comunicazione con il [!DNL InDesign Server]. È possibile aggiungere, rimuovere e ordinare gli elementi necessari.

1. Fai clic su OK per salvare.

### Configurare Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se la [!DNL InDesign Server] e [!DNL Experience Manager] su host diversi o una o entrambe le applicazioni non funzionano sulle porte predefinite, quindi configura [!UICONTROL Day CQ Link Externalizer] per impostare il nome host, la porta e il percorso del contenuto per [!DNL InDesign Server].

1. Accedere alla console Web all&#39;indirizzo `https://[aem_server]:[port]/system/console/configMgr`.
1. Individua la configurazione **[!UICONTROL Day CQ Link Externalizer]**. Fai clic su **[!UICONTROL Modifica]** per aprire.
1. Le impostazioni di Link Externalizer consentono di creare URL assoluti per [!DNL Experience Manager] e per [!DNL InDesign Server]. Utilizzo **[!UICONTROL Domini]** campo per specificare il nome host per il [!DNL Adobe InDesign Server]. Fai clic su **Salva**.

   Negli URL assoluti, utilizza `localhost` come nome host per l’istanza locale (autore) e come nome host o indirizzo IP per l’istanza di pubblicazione, come illustrato nella figura seguente.

   ![Impostazione del collegamento esternalizzatore](assets/link-externalizer-config.png)

### Abilita elaborazione processi paralleli per [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

È ora possibile abilitare l&#39;elaborazione dei processi paralleli per gli ID. Determinare il numero massimo di processi paralleli (`x`) e [!DNL InDesign Server] può elaborare:

* Su un singolo computer multiprocessore, il numero massimo di processi paralleli (`x`) che [!DNL InDesign Server] L&#39;elaborazione di can è inferiore al numero di processori che eseguono ID.
* Quando si esegue l&#39;ID su più computer è necessario contare il numero totale di processori disponibili (ossia su tutti i computer), quindi sottrarre il numero totale di macchine.

Per configurare il numero di processi IDS paralleli:

1. Apri **[!UICONTROL Configurazioni]** scheda della console Felix; ad esempio: `https://[aem_server]:[port]/system/console/configMgr`.

1. Seleziona la coda di elaborazione IDS sotto `Apache Sling Job Queue Configuration`.

1. Imposta:

   * **Tipo** - `Parallel`
   * **Processi paralleli massimi** - `<*x*>` (come calcolato in precedenza)

1. Salva queste modifiche.
1. Per abilitare il supporto per più sessioni per Adobe CS6 e versioni successive, controlla `enable.multisession.name` casella di controllo, sotto `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configurazione.
1. Crea un [piscina `x` I processi di lavoro IDS aggiungendo endpoint SOAP alla configurazione di IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Se sono in esecuzione più macchine [!DNL InDesign Server], aggiungi endpoint SOAP (numero di processori per computer -1) per ogni computer.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Quando si lavora con un pool di lavoratori, è possibile abilitare l&#39;elenco Bloccati di lavoratori IDS.
>
>Per farlo, abilita la **[!UICONTROL enable.try.name]** sotto la casella di controllo `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configurazione, che abilita il recupero del processo IDS.
>
>Inoltre, sotto `com.day.cq.dam.ids.impl.IDSPoolImpl.name` configurazione, imposta un valore positivo per `max.errors.to.blacklist` parametro che determina il numero di recuperi di processi prima di associare un ID dall&#39;elenco dei gestori di processi.
>
>Per impostazione predefinita, dopo il`retry.interval.to.whitelist.name`) in minuti il processo di lavoro IDS viene riconvalidato. Se il lavoratore viene trovato online, viene rimosso dall&#39;elenco Bloccati.

## Abilita supporto per [!DNL InDesign Server] 10.0 o versione successiva {#enabling-support-for-indesign-server-or-later}

Per [!DNL InDesign Server] 10.0 o versione successiva, esegui i seguenti passaggi per abilitare il supporto per più sessioni.

1. Apri Configuration Manager dal [!DNL Experience Manager Assets] istanza `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificare la configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Seleziona la **[!UICONTROL ids.cc.enable]** e fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Per [!DNL InDesign Server] integrazione con [!DNL Experience Manager Assets], utilizza un processore multi-core perché la funzionalità di supporto delle sessioni necessaria per l&#39;integrazione non è supportata sui sistemi single-core.

## Configura [!DNL Experience Manager] credenziali {#configure-aem-credentials}

È possibile modificare le credenziali di amministratore predefinite (nome utente e password) per accedere al [!DNL InDesign Server] dal [!DNL Experience Manager] senza interrompere l’integrazione con [!DNL InDesign Server].

1. Passa a `/etc/cloudservices/proxy.html`.
1. Nella finestra di dialogo , specifica il nuovo nome utente e la nuova password.
1. Salva le credenziali.

>[!MORELIKETHIS]
>
>* [Informazioni su Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

