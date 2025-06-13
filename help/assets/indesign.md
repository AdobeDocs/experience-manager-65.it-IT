---
title: Integra [!DNL Assets] con [!DNL InDesign Server]
description: Scopri come integrare  [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 75c15b0f0e4de2ea7fff339ae46b88ce8f6af83f
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 2%

---

# Integra [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilizza:

* Proxy per distribuire il carico di determinate attività di elaborazione. Un proxy è un&#39;istanza [!DNL Experience Manager] che comunica con un lavoratore proxy per eseguire un&#39;attività specifica e altre istanze [!DNL Experience Manager] per fornire i risultati.
* Un lavoratore proxy per definire e gestire un&#39;attività specifica.
Questi possono coprire un&#39;ampia gamma di attività, ad esempio l&#39;utilizzo di [!DNL InDesign Server] per l&#39;elaborazione dei file.

Per caricare completamente i file in [!DNL Experience Manager Assets] che hai creato con [!DNL Adobe InDesign], viene utilizzato un proxy. Viene utilizzato un processo di lavoro proxy per comunicare con [!DNL Adobe InDesign Server], in cui vengono eseguiti script per estrarre i metadati e generare varie rappresentazioni per [!DNL Experience Manager Assets]. Il processo di lavoro proxy abilita la comunicazione bidirezionale tra le istanze [!DNL InDesign Server] e [!DNL Experience Manager] in una configurazione cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] è offerto come due offerte separate. [app desktop Adobe InDesign](https://www.adobe.com/products/indesign.html) utilizzata per progettare layout di pagina per la stampa e la distribuzione digitale. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) consente di creare in modo programmatico documenti automatizzati in base a ciò che hai creato con [!DNL InDesign]. Funziona come un servizio che offre un’interfaccia al suo motore ExtendScript. Gli script sono scritti in [!DNL ExtendScript], simile a [!DNL JavaScript].

## Come funziona l’estrazione {#how-the-extraction-works}

[!DNL Adobe InDesign Server] può essere integrato con [!DNL Experience Manager Assets] in modo che i file INDD creati con [!DNL InDesign] possano essere caricati, generati, tutti i file multimediali estratti (ad esempio, video) e memorizzati come risorse:

>[!NOTE]
>
>Nelle versioni precedenti di [!DNL Experience Manager] è stato possibile estrarre XMP e la miniatura. Ora è possibile estrarre tutti i file multimediali.

1. Carica il file INDD in [!DNL Experience Manager Assets].
1. Un framework invia script di comandi a [!DNL InDesign Server] tramite SOAP (Simple Object Access Protocol).
Questo script di comandi:

   * Recuperate il file INDD.
   * Esegui [!DNL InDesign Server] comandi:

      * Vengono estratti la struttura, il testo ed eventuali file multimediali.
      * Vengono generate le rappresentazioni di PDF e JPG.
      * Vengono generate le rappresentazioni HTML e IDML.

   * Ripubblica i file risultanti in [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML è un formato basato su XML che esegue il rendering di tutto il contenuto del file [!DNL InDesign]. Viene archiviato come pacchetto compresso utilizzando la compressione [ZIP](https://techterms.com/definition/zip). Per ulteriori informazioni, vedere [Formati di interscambio InDesign INX e IDML](https://www.peachpit.com/promotions/adobe-creative-cloud-2024-release-books-ebooks-and-142536).

   >[!CAUTION]
   >
   >Se [!DNL InDesign Server] non è installato o non è configurato, è comunque possibile caricare un file INDD in [!DNL Experience Manager]. Tuttavia, le rappresentazioni generate sono limitate a PNG e JPEG. Non sarà possibile generare HTML, `.idml` o le rappresentazioni delle pagine.

1. Dopo la generazione dell’estrazione e della rappresentazione:

   * La struttura viene replicata in un `cq:Page` (tipo di rappresentazione).
   * Il testo e i file estratti sono archiviati in [!DNL Experience Manager Assets].
   * Tutte le rappresentazioni sono archiviate in [!DNL Experience Manager Assets], nella risorsa stessa.

## Integra [!DNL InDesign Server] con Experience Manager {#integrating-the-indesign-server-with-aem}

Per integrare [!DNL InDesign Server] per l&#39;utilizzo con [!DNL Experience Manager Assets] e dopo aver configurato il proxy, è necessario:

1. [Installa InDesign Server](#installing-the-indesign-server).
1. Se necessario, [configurare il flusso di lavoro di Experience Manager Assets](#configuring-the-aem-assets-workflow).
Questa operazione è necessaria solo se i valori predefiniti non sono appropriati per l’istanza.
1. Configura un [lavoratore proxy per InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installa [!DNL InDesign Server] {#installing-the-indesign-server}

Per installare e avviare [!DNL InDesign Server] per l&#39;utilizzo con [!DNL Experience Manager]:

1. Scaricare e installare [!DNL InDesign Server].

1. Se necessario, è possibile personalizzare la configurazione dell&#39;istanza [!DNL InDesign Server].

1. Dalla riga di comando, avvia il server:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Il server viene avviato con il plug-in SOAP in ascolto sulla porta 8080. Tutti i messaggi di log e l&#39;output vengono scritti direttamente nella finestra di comando.

   >[!NOTE]
   >
   >Se si desidera salvare i messaggi di output in un file, utilizzare il reindirizzamento, ad esempio in Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configura il flusso di lavoro [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] ha un flusso di lavoro preconfigurato **[!UICONTROL Risorsa di aggiornamento DAM]**, con diversi passaggi di processo specifici per [!DNL InDesign]:

* [Estrazione file multimediali](#media-extraction)
* [Estrazione pagina](#page-extraction)

Questo flusso di lavoro è configurato con valori predefiniti che possono essere adattati per la tua configurazione nelle varie istanze di authoring (si tratta di un flusso di lavoro standard, quindi ulteriori informazioni sono disponibili in [Modifica di un flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se utilizzi i valori predefiniti (inclusa la porta SOAP), non è necessaria alcuna configurazione.

Dopo l&#39;installazione, il caricamento di [!DNL InDesign] file in [!DNL Experience Manager Assets] (secondo uno dei metodi usuali) attiva il flusso di lavoro per elaborare la risorsa e preparare le varie rappresentazioni. Verifica la configurazione caricando un file INDD in [!DNL Experience Manager Assets] per confermare di visualizzare le diverse rappresentazioni create da IDS in `<*your_asset*>.indd/Renditions`

#### Estrazione file multimediali {#media-extraction}

Questo passaggio controlla l&#39;estrazione dei file multimediali dal file INDD.

Per personalizzare, è possibile modificare la scheda **[!UICONTROL Argomenti]** del passaggio **[!UICONTROL Estrazione file multimediali]**.

![Argomenti di estrazione file multimediali e percorsi script](assets/media_extraction_arguments_scripts.png)

Argomenti di estrazione dei contenuti multimediali e percorsi di script

* **Libreria ExtendScript**: si tratta di una semplice libreria http get/post, richiesta dagli altri script.

* **Estendi script**: qui è possibile specificare combinazioni di script diverse. Se si desidera eseguire script personalizzati in [!DNL InDesign Server], salvare gli script in `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Non modificare la libreria ExtendScript. Questa libreria fornisce la funzionalità HTTP necessaria per comunicare con Sling. Questa impostazione specifica la libreria da inviare a [!DNL InDesign Server] per l&#39;utilizzo.

Lo script `ThumbnailExport.jsx` eseguito dal passaggio del flusso di lavoro Estrazione file multimediali genera una rappresentazione di miniature in formato JPG. Questo rendering viene utilizzato dal passaggio del flusso di lavoro Elabora miniature per generare i rendering statici richiesti da [!DNL Experience Manager].

Puoi configurare il passaggio del flusso di lavoro Elabora miniature per generare rappresentazioni statiche a dimensioni diverse. Assicurarsi di non rimuovere i valori predefiniti perché sono richiesti dall&#39;interfaccia [!DNL Experience Manager Assets]. Infine, il passaggio del flusso di lavoro Elimina rappresentazione anteprima immagine rimuove la rappresentazione delle miniature di JPG, in quanto non è più necessaria.

#### Estrazione pagina {#page-extraction}

Verrà creata una pagina [!DNL Experience Manager] dagli elementi estratti. Un gestore estrazione viene utilizzato per estrarre i dati da una rappresentazione (attualmente HTML o IDML). Questi dati vengono quindi utilizzati per creare una pagina utilizzando Page Builder.

Per personalizzare, è possibile modificare la scheda **[!UICONTROL Argomenti]** del passaggio **[!UICONTROL Estrazione pagina]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestore estrazione pagina**: dall&#39;elenco a comparsa, selezionare il gestore che si desidera utilizzare. Un gestore estrazione opera su un rendering specifico, scelto da un `RenditionPicker` correlato (vedi l&#39;API `ExtractionHandler`). In un&#39;installazione standard di [!DNL Experience Manager] è disponibile quanto segue:
   * IDML Export Extraction Handle (Handle di estrazione esportazione IDML): opera sulla rappresentazione `IDML` generata nel passaggio MediaExtract.

* **Nome pagina**: specificare il nome che si desidera assegnare alla pagina risultante. Se lasciato vuoto, il nome sarà &quot;page&quot; (o una derivata se &quot;page&quot; esiste già).

* **Titolo pagina**: specifica il titolo da assegnare alla pagina risultante.

* **Percorso principale pagina**: il percorso della posizione principale della pagina risultante. Se questo campo viene lasciato vuoto, viene utilizzato il nodo che contiene le rappresentazioni della risorsa.

* **Modello pagina**: modello da utilizzare per generare la pagina risultante.

* **Progettazione pagina**: progettazione della pagina da utilizzare per generare la pagina risultante.

### Configura il processo di lavoro proxy per [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Il lavoratore risiede nell&#39;istanza proxy.

1. Nella console Strumenti, espandi **[!UICONTROL Configurazioni servizi cloud]** nel riquadro a sinistra. Quindi espandi **[!UICONTROL Configurazione proxy cloud]**.

1. Per aprire la configurazione, fai doppio clic su **[!UICONTROL IDS worker]**.

1. Fai clic su **[!UICONTROL Modifica]** per aprire la finestra di dialogo di configurazione e definire le impostazioni richieste:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool IDS**
Gli endpoint SOAP utilizzati per comunicare con [!DNL InDesign Server]. È possibile aggiungere, rimuovere e ordinare gli elementi necessari.

1. Fare clic su OK per salvare.

### Configurare Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se [!DNL InDesign Server] e [!DNL Experience Manager] si trovano su host diversi o se una o entrambe queste applicazioni non funzionano sulle porte predefinite, configurare [!UICONTROL Day CQ Link Externalizer] per impostare il nome host, la porta e il percorso del contenuto per [!DNL InDesign Server].

1. Accedere alla console Web in `https://[aem_server]:[port]/system/console/configMgr`.
1. Individua la configurazione **[!UICONTROL Day CQ Link Externalizer]**. Fai clic su **[!UICONTROL Modifica]** per aprire.
1. Le impostazioni di Link Externalizer consentono di creare URL assoluti per la distribuzione di [!DNL Experience Manager] e per [!DNL InDesign Server]. Utilizzare il campo **[!UICONTROL Domini]** per specificare il nome host per [!DNL Adobe InDesign Server]. Fai clic su **Salva**.

   Negli URL assoluti, utilizzare `localhost` come nome host per l&#39;istanza locale (di authoring) e come nome host o indirizzo IP per l&#39;istanza di pubblicazione, come illustrato nella figura seguente.

   ![Impostazione Link Externalizer](assets/link-externalizer-config.png)

### Abilita elaborazione processi paralleli per [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Ora puoi abilitare l’elaborazione di processi paralleli per gli ID. Determinare il numero massimo di processi paralleli (`x`) che [!DNL InDesign Server] può elaborare:

* In un singolo computer multiprocessore, il numero massimo di processi paralleli (`x`) che un [!DNL InDesign Server] può elaborare è inferiore di uno al numero di processori che eseguono IDS.
* Quando si eseguono gli ID su più computer, è necessario contare il numero totale di processori disponibili (ovvero su tutti i computer) e quindi sottrarre il numero totale di computer.

Per configurare il numero di processi IDS paralleli:

1. Apri la scheda **[!UICONTROL Configurazioni]** della console Felix, ad esempio: `https://[aem_server]:[port]/system/console/configMgr`.

1. Selezionare la coda di elaborazione IDS in `Apache Sling Job Queue Configuration`.

1. Imposta:

   * **Tipo** - `Parallel`
   * **Numero massimo processi paralleli** - `<*x*>` (come calcolato sopra)

1. Salva queste modifiche.
1. Per abilitare il supporto multisessione per Adobe CS6 e versioni successive, selezionare la casella di controllo `enable.multisession.name` nella configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Creare un [pool di `x` processi di lavoro IDS aggiungendo endpoint SOAP alla configurazione di lavoro IDS](#configuring-the-proxy-worker-for-indesign-server).

   Se sono presenti più computer che eseguono [!DNL InDesign Server], aggiungere endpoint SOAP (numero di processori per computer -1) per ogni computer.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Quando si lavora con un pool di lavoratori, è possibile abilitare un elenco Bloccati di lavoratori IDS.
>
>Per eseguire questa operazione, abilitare la casella di controllo **[!UICONTROL enable.retry.name]** nella configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, che abilita le versioni di processo IDS.
>
>Inoltre, nella configurazione `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, impostare un valore positivo per il parametro `max.errors.to.blacklist` che determina il numero di tentativi del processo prima di bloccare un ID dall&#39;elenco dei gestori di processi.
>
>Per impostazione predefinita, dopo il tempo configurabile (`retry.interval.to.whitelist.name`) in minuti, il processo di lavoro IDS viene riconvalidato. Se il lavoratore viene trovato online, viene rimosso dall&#39;elenco Bloccati.

## Abilita supporto per [!DNL InDesign Server] versione 10.0 o successiva {#enabling-support-for-indesign-server-or-later}

Per [!DNL InDesign Server] 10.0 o versione successiva, eseguire la procedura seguente per abilitare il supporto per più sessioni.

1. Aprire Configuration Manager dall&#39;istanza `https://[aem_server]:[port]/system/console/configMgr` di [!DNL Experience Manager Assets].
1. Modificare la configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Selezionare l&#39;opzione **[!UICONTROL ids.cc.enable]** e fare clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Per l&#39;integrazione di [!DNL InDesign Server] con [!DNL Experience Manager Assets], utilizzare un processore multi-core perché la funzionalità di supporto delle sessioni necessaria per l&#39;integrazione non è supportata nei sistemi single-core.

## Configura credenziali [!DNL Experience Manager] {#configure-aem-credentials}

È possibile modificare le credenziali di amministratore predefinite (nome utente e password) per accedere a [!DNL InDesign Server] dalla distribuzione di [!DNL Experience Manager] senza interrompere l&#39;integrazione con [!DNL InDesign Server].

1. Passa a `/etc/cloudservices/proxy.html`.
1. Nella finestra di dialogo, specifica il nuovo nome utente e la nuova password.
1. Salva le credenziali.

>[!MORELIKETHIS]
>
>* [Informazioni su Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)
