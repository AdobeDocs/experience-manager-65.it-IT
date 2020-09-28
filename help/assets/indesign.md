---
title: ' [!DNL Assets] Integrate con [!DNL InDesign Server]'
description: Scopri come [!DNL Adobe Experience Manager Assets] integrarsi [!DNL Adobe InDesign Server].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 4%

---


# Integrazione [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] use:

* Un proxy per distribuire il carico di alcune attività di elaborazione. Un proxy è un&#39; [!DNL Experience Manager] istanza che comunica con un lavoratore proxy per eseguire un&#39;attività specifica e altre [!DNL Experience Manager] istanze per fornire i risultati.
* Un lavoratore proxy per definire e gestire un&#39;attività specifica.
Questi possono coprire un&#39;ampia gamma di compiti; ad esempio, l&#39;uso di un [!DNL InDesign Server] per elaborare i file.

Per caricare completamente i file in [!DNL Experience Manager Assets] cui avete creato [!DNL Adobe InDesign] un proxy, viene utilizzato. Questo utilizza un proxy worker per comunicare con il [!DNL Adobe InDesign Server], dove [gli script](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) vengono eseguiti per estrarre i metadati e generare diverse rappresentazioni per [!DNL Experience Manager Assets]. Il lavoratore proxy abilita la comunicazione bidirezionale tra le istanze [!DNL InDesign Server] e le [!DNL Experience Manager] istanze in una configurazione cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] viene offerto come due offerte separate. [app desktop Adobe InDesign](https://www.adobe.com/products/indesign.html) utilizzata per progettare layout di pagina per la stampa e la distribuzione digitale. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) consente di creare a livello di programmazione documenti automatizzati basati su ciò che è stato creato [!DNL InDesign]. Funziona come un servizio che offre un&#39;interfaccia al suo motore ExtendScript [](https://www.adobe.com/devnet/scripting.html) .Gli script sono scritti in [!DNL ExtendScript], che è simile a [!DNL JavaScript]. Per informazioni sugli [!DNL InDesign] script, vedere [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Funzionamento dell&#39;estrazione {#how-the-extraction-works}

È [!DNL Adobe InDesign Server] possibile integrare i file INDD creati con [!DNL Experience Manager Assets] cui [!DNL InDesign] possono essere caricati, generati, tutti i file multimediali estratti (ad esempio, video) e memorizzati come risorse:

>[!NOTE]
>
>Le versioni precedenti di [!DNL Experience Manager] erano in grado di estrarre XMP e la miniatura, ora tutti i supporti possono essere estratti.

1. Caricate il file INDD in [!DNL Experience Manager Assets].
1. Un framework invia script di comando [!DNL InDesign Server] tramite SOAP (Simple Object Access Protocol).
Questo script di comando:

   * Recuperate il file INDD.
   * Esegui [!DNL InDesign Server] comandi:

      * Vengono estratti la struttura, il testo e tutti i file multimediali.
      * Vengono generate rappresentazioni PDF e JPG.
      * Vengono generate rappresentazioni HTML e IDML.
   * Ripubblica i file risultanti in [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML è un formato basato su XML che esegue il rendering di tutti i contenuti del [!DNL InDesign] file. Viene memorizzato come pacchetto compresso utilizzando la compressione [ZIP](https://www.techterms.com/definition/zip) . Per ulteriori informazioni, vedere [formati di interscambio InDesign INX e IDML](http://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Se il file [!DNL InDesign Server] non è installato o non è configurato, potete comunque caricare un file INDD in [!DNL Experience Manager]. Tuttavia, le rappresentazioni generate saranno limitate a PNG e JPEG. Non sarà possibile generare rappresentazioni HTML, .idml o di pagina.

1. Dopo la generazione di estrazione e rappresentazione:

   * La struttura viene replicata in un `cq:Page` (tipo di rappresentazione).
   * Il testo e i file estratti vengono memorizzati in [!DNL Experience Manager Assets].
   * Tutte le rappresentazioni sono memorizzate nella [!DNL Experience Manager Assets], nella risorsa stessa.

## Integrare l&#39; [!DNL InDesign Server] con  Experience Manager {#integrating-the-indesign-server-with-aem}

Per integrare l&#39; [!DNL InDesign Server] utilizzo con [!DNL Experience Manager Assets] e dopo la configurazione del proxy, è necessario:

1. [Installare il InDesign Server](#installing-the-indesign-server).
1. Se necessario, [configura il flusso di lavoro](#configuring-the-aem-assets-workflow)Risorse Experience Manager .
Ciò è necessario solo se i valori predefiniti non sono appropriati per l’istanza in uso.
1. Configurare un lavoratore [proxy per il InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installa [!DNL InDesign Server] {#installing-the-indesign-server}

Per installare e avviare l’ [!DNL InDesign Server] utilizzo con [!DNL Experience Manager]:

1. Scaricate e installate il [!DNL InDesign Server].

1. Se necessario, potete personalizzare la configurazione dell’ [!DNL InDesign Server] istanza.

1. Dalla riga di comando, avviate il server:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Verrà avviato il server con il plug-in SOAP in ascolto sulla porta 8080. Tutti i messaggi e gli output del registro vengono scritti direttamente nella finestra del comando.

   >[!NOTE]
   >
   >Se si desidera salvare i messaggi di output in un file, utilizzare redirection; ad esempio, in Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurare il [!DNL Experience Manager Assets] flusso di lavoro {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispone di un flusso di lavoro preconfigurato **[!UICONTROL DAM Update Asset]**, con diversi passaggi di processo specifici per [!DNL InDesign]:

* [Estrazione file multimediali](#media-extraction)
* [Estrazione pagina](#page-extraction)

Questo flusso di lavoro è configurato con valori predefiniti che possono essere adattati per la configurazione nelle varie istanze di authoring (si tratta di un flusso di lavoro standard, per cui ulteriori informazioni sono disponibili in [Modifica di un flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se si utilizzano i valori predefiniti (inclusa la porta SOAP), non è necessaria alcuna configurazione.

Dopo l’impostazione, il caricamento di [!DNL InDesign] file in [!DNL Experience Manager Assets] (con uno dei metodi più comuni) attiva il flusso di lavoro per elaborare la risorsa e preparare le varie rappresentazioni. Verifica la configurazione caricando un file INDD in [!DNL Experience Manager Assets] modo da confermare la visualizzazione delle diverse rappresentazioni create da IDS in `<*your_asset*>.indd/Renditions`

#### Media extraction {#media-extraction}

Questo passaggio controlla l’estrazione di file multimediali dal file INDD.

Per personalizzare, puoi modificare la scheda **[!UICONTROL Arguments (Argomenti)]** del passaggio **[!UICONTROL Estrazione file multimediali]**.

![Argomenti di estrazione dei supporti e percorsi di script](assets/media_extraction_arguments_scripts.png)

Argomenti di estrazione dei supporti e percorsi di script

* **Libreria** ExtendScript : Si tratta di una semplice libreria di metodi http get/post, richiesta dagli altri script.

* **Estendi script**: Qui è possibile specificare diverse combinazioni di script. Se si desidera che gli script personalizzati siano eseguiti sul [!DNL InDesign Server]computer, salvare gli script in `/apps/settings/dam/indesign/scripts`.

Per informazioni sugli [!DNL Adobe InDesign] script, consultate la documentazione per lo sviluppo di [InDesign](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>Non modificare la libreria ExtendScript. Questa libreria fornisce la funzionalità HTTP necessaria per comunicare con Sling. Questa impostazione specifica la libreria da inviare alla libreria [!DNL InDesign Server] per utilizzarla.

Lo `ThumbnailExport.jsx` script eseguito dal passaggio del flusso di lavoro Estrazione file multimediali genera una rappresentazione in miniatura in formato JPG. Questa rappresentazione viene utilizzata dal passaggio del flusso di lavoro Miniature di processo per generare le rappresentazioni statiche richieste da [!DNL Experience Manager].

Potete configurare il passaggio del flusso di lavoro Miniature di processo per generare rappresentazioni statiche di dimensioni diverse. Assicuratevi di non rimuovere le impostazioni predefinite, perché sono richieste dall&#39; [!DNL Experience Manager Assets] interfaccia. Infine, il passaggio del flusso di lavoro Elimina anteprima immagine rimuove la rappresentazione in miniatura JPG, in quanto non è più necessaria.

#### Page extraction {#page-extraction}

Viene creata una [!DNL Experience Manager] pagina dagli elementi estratti. Un gestore di estrazione viene utilizzato per estrarre i dati da una rappresentazione (attualmente HTML o IDML). Questi dati vengono quindi utilizzati per creare una pagina con PageBuilder.

Per personalizzare, è possibile modificare la scheda **[!UICONTROL Argomenti]** del passaggio **[!UICONTROL Estrazione pagina]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestore** estrazione pagina: Dall&#39;elenco a comparsa, selezionare il gestore che si desidera utilizzare. Un gestore estrazione opera su un rendering specifico, scelto da un `RenditionPicker` correlato (consulta l’API `ExtractionHandler`). In a standard [!DNL Experience Manager] installation the following is available:
   * Maniglia estrazione esportazione IDML: Funziona sulla `IDML` rappresentazione generata nel passaggio MediaExtract.

* **Nome** pagina: Specificate il nome che desiderate assegnare alla pagina risultante. Se lasciato vuoto, il nome è &quot;page&quot; (o un derivato, se &quot;page&quot; esiste già).

* **Titolo** pagina: Specificate il titolo che desiderate assegnare alla pagina risultante.

* **Percorso** directory principale pagina: Percorso della posizione principale della pagina risultante. Se lasciato vuoto, verrà utilizzato il nodo che contiene le rappresentazioni della risorsa.

* **Modello** pagina: Modello da utilizzare per la generazione della pagina risultante.

* **Progettazione** pagina: Struttura della pagina da utilizzare per la generazione della pagina risultante.

### Configurare il lavoratore proxy per [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Il lavoratore risiede nell&#39;istanza proxy.

1. Nella console Strumenti, espandete Configurazioni **** Cloud Services nel riquadro a sinistra. Quindi espandete Configurazione **[!UICONTROL proxy]** Cloud.

1. Per aprire la configurazione, fai doppio clic su **[!UICONTROL IDS worker]**.

1. Fate clic su **[!UICONTROL Modifica]** per aprire la finestra di dialogo di configurazione e definire le impostazioni richieste:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool** IDS Gli endpoint SOAP da utilizzare per comunicare con l&#39;app [!DNL InDesign Server]. È possibile aggiungere, rimuovere e ordinare gli elementi necessari.

1. Fai clic su OK per salvare.

### Configurare Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se l&#39;applicazione [!DNL InDesign Server] e l&#39; [!DNL Experience Manager] esecuzione su host diversi o una o entrambe le applicazioni non vengono eseguite sulle porte predefinite, configurate [!UICONTROL Day CQ Link Externalizer] per impostare il nome host, la porta e il percorso del contenuto per l&#39;host [!DNL InDesign Server].

1. Accedi alla console Web all&#39;indirizzo `https://[aem_server]:[port]/system/console/configMgr`.
1. Locate the configuration **[!UICONTROL Day CQ Link Externalizer]**, and click **[!UICONTROL Edit]** to open it.
1. Specificate il nome host e il percorso contestuale per il file [!DNL Adobe InDesign Server] e fate clic su **Salva**.

   ![chlimage_1-97](assets/chlimage_1-290.png)

### Abilita elaborazione processi paralleli per [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server-s}

È ora possibile abilitare l&#39;elaborazione processi paralleli per gli ID. Determinare il numero massimo di processi paralleli (`x`) che è [!DNL InDesign Server] possibile elaborare:

* Su un singolo computer multiprocessore, il numero massimo di processi paralleli (`x`) che un utente [!DNL InDesign Server] può elaborare è inferiore di uno al numero di processori che eseguono IDS.
* Quando si esegue IDS su più computer è necessario contare il numero totale di processori disponibili (ossia su tutti i computer), quindi sottrarre il numero totale di computer.

Per configurare il numero di processi IDS paralleli:

1. Aprite la scheda **[!UICONTROL Configurazioni]** della console Felix; ad esempio: `https://[aem_server]:[port]/system/console/configMgr`.

1. Selezionare la coda di elaborazione IDS sotto `Apache Sling Job Queue Configuration`.

1. Imposta:

   * **Tipo** - `Parallel`
   * **Processi** paralleli massimi - `<*x*>` (come calcolato sopra)

1. Salvate queste modifiche.
1. Per abilitare il supporto per più sessioni per  Adobe CS6 e versioni successive, selezionate `enable.multisession.name` casella di controllo, in `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configurazione.
1. Create un [pool di lavoratori `x` IDS aggiungendo endpoint SOAP alla configurazione](#configuring-the-proxy-worker-for-indesign-server)IDS Worker.

   Se sono in esecuzione più computer [!DNL InDesign Server], aggiungere endpoint SOAP (numero di processori per computer -1) per ogni computer.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Quando si lavora con un pool di lavoratori, è possibile abilitare  elenco Bloccati di lavoratori IDS.
>
>A tal fine, abilitare la casella di controllo **[!UICONTROL enable.try.name]** , nella `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configurazione, che consente di recuperare i processi IDS.
>
>Inoltre, nella `com.day.cq.dam.ids.impl.IDSPoolImpl.name` configurazione, impostare un valore positivo per il `max.errors.to.blacklist` parametro che determina il numero di recuperi di processi prima di barrare un ID dall&#39;elenco dei gestori di processi.
>
>Per impostazione predefinita, dopo il tempo configurabile (`retry.interval.to.whitelist.name`) in minuti, il lavoro IDS viene riconvalidato. Se il lavoratore viene trovato online, viene rimosso dal elenco Bloccati .

## Abilita il supporto per la versione [!DNL InDesign Server] 10.0 o successiva {#enabling-support-for-indesign-server-or-later}

Per [!DNL InDesign Server] 10.0 o versione successiva, eseguite i seguenti passaggi per abilitare il supporto per più sessioni.

1. Aprite Configuration Manager dall&#39; [!DNL Experience Manager Assets] istanza `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificate la configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Selezionate l’opzione **[!UICONTROL ids.cc.enable]** e fate clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Per [!DNL InDesign Server] l&#39;integrazione con [!DNL Experience Manager Assets], utilizzate un processore multi-core perché la funzione di supporto delle sessioni necessaria per l&#39;integrazione non è supportata nei sistemi single core.

## Configurare [!DNL Experience Manager] le credenziali {#configure-aem-credentials}

Potete modificare le credenziali di amministratore predefinite (nome utente e password) per accedere al [!DNL InDesign Server] contenuto dalla [!DNL Experience Manager] distribuzione senza interrompere l&#39;integrazione con il [!DNL InDesign Server].

1. Passa a `/etc/cloudservices/proxy.html`.
1. Nella finestra di dialogo, specificate il nuovo nome utente e la nuova password.
1. Salvare le credenziali.

>[!MORELIKETHIS]
>
>* [Informazioni su  Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

