---
title: Integrare  [!DNL Assets] con [!DNL InDesign Server]
description: Scopri come integrare  [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server].
contentOwner: AG
translation-type: tm+mt
source-git-commit: a31fa2712e541dfdc7a5b08ee9b33782f190f00b
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 4%

---


# Integrare [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] use:

* Un proxy per distribuire il carico di alcune attività di elaborazione. Un proxy è un&#39;istanza [!DNL Experience Manager] che comunica con un lavoratore proxy per eseguire un&#39;attività specifica, e con altre istanze [!DNL Experience Manager] per fornire i risultati.
* Un lavoratore proxy per definire e gestire un&#39;attività specifica.
Questi possono coprire un&#39;ampia gamma di compiti; ad esempio, l&#39;utilizzo di un [!DNL InDesign Server] per elaborare i file.

Per caricare completamente i file in [!DNL Experience Manager Assets] creati con [!DNL Adobe InDesign] viene utilizzato un proxy. Questo utilizza un proxy worker per comunicare con [!DNL Adobe InDesign Server], dove [gli script](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) vengono eseguiti per estrarre i metadati e generare diverse rappresentazioni per [!DNL Experience Manager Assets]. Il lavoratore proxy abilita la comunicazione bidirezionale tra le istanze [!DNL InDesign Server] e [!DNL Experience Manager] in una configurazione cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] viene offerto come due offerte separate. [&#39;app desktop ](https://www.adobe.com/products/indesign.html) InDesign di Adobe utilizzata per progettare layout di pagina per la stampa e la distribuzione digitale. [ Adobe InDesign ](https://www.adobe.com/products/indesignserver.html) Server consente di creare a livello di programmazione documenti automatizzati basati su ciò che è stato creato con  [!DNL InDesign]. Funziona come un servizio che offre un&#39;interfaccia al suo motore [ ExtendScript](https://www.adobe.com/devnet/scripting.html).Gli script sono scritti in [!DNL ExtendScript], che è simile a [!DNL JavaScript]. Per informazioni sugli script [!DNL InDesign], vedere [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Funzionamento dell&#39;estrazione {#how-the-extraction-works}

È possibile integrare [!DNL Adobe InDesign Server] con [!DNL Experience Manager Assets] per caricare i file INDD creati con [!DNL InDesign], generare le rappresentazioni, estrarre tutti i file multimediali (ad esempio, video) e memorizzarli come risorse:

>[!NOTE]
>
>Le versioni precedenti di [!DNL Experience Manager] erano in grado di estrarre XMP e la miniatura, ora è possibile estrarre tutti i supporti.

1. Caricate il file INDD in [!DNL Experience Manager Assets].
1. Un framework invia script di comando a [!DNL InDesign Server] tramite SOAP (Simple Object Access Protocol).
Questo script di comando:

   * Recuperate il file INDD.
   * Esegui comandi [!DNL InDesign Server]:

      * Vengono estratti la struttura, il testo e tutti i file multimediali.
      * Vengono generate rappresentazioni PDF e JPG.
      * Vengono generate rappresentazioni HTML e IDML.
   * Riportare i file risultanti su [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML è un formato basato su XML che esegue il rendering di tutti i contenuti del file [!DNL InDesign]. Viene memorizzato come pacchetto compresso utilizzando la compressione [ZIP](https://www.techterms.com/definition/zip). Per ulteriori informazioni, vedere [ formati di interscambio InDesign INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Se [!DNL InDesign Server] non è installato o non è configurato, è comunque possibile caricare un file INDD in [!DNL Experience Manager]. Tuttavia, le rappresentazioni generate saranno limitate a PNG e JPEG. Non sarà possibile generare rappresentazioni HTML, .idml o di pagina.

1. Dopo la generazione di estrazione e rappresentazione:

   * La struttura viene replicata in un `cq:Page` (tipo di rappresentazione).
   * Il testo e i file estratti sono memorizzati in [!DNL Experience Manager Assets].
   * Tutte le rappresentazioni sono memorizzate in [!DNL Experience Manager Assets], nella risorsa stessa.

## Integrare il [!DNL InDesign Server] con  Experience Manager {#integrating-the-indesign-server-with-aem}

Per integrare [!DNL InDesign Server] per l&#39;utilizzo con [!DNL Experience Manager Assets] e dopo aver configurato il proxy, è necessario:

1. [Installare il InDesign Server](#installing-the-indesign-server) .
1. Se necessario, [configura il flusso di lavoro risorse del Experience Manager ](#configuring-the-aem-assets-workflow).
Ciò è necessario solo se i valori predefiniti non sono appropriati per l’istanza in uso.
1. Configurare un lavoratore proxy [per il  InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installare [!DNL InDesign Server] {#installing-the-indesign-server}

Per installare e avviare [!DNL InDesign Server] per l&#39;utilizzo con [!DNL Experience Manager]:

1. Scaricate e installate il [!DNL InDesign Server].

1. Se necessario, potete personalizzare la configurazione dell&#39;istanza [!DNL InDesign Server].

1. Dalla riga di comando, avviate il server:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Verrà avviato il server con il plug-in SOAP in ascolto sulla porta 8080. Tutti i messaggi e gli output del registro vengono scritti direttamente nella finestra del comando.

   >[!NOTE]
   >
   >Se si desidera salvare i messaggi di output in un file, utilizzare redirection; ad esempio, in Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurare il flusso di lavoro [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispone di un flusso di lavoro preconfigurato  **[!UICONTROL DAM Update Asset]**, con diversi passaggi di processo specifici per  [!DNL InDesign]:

* [Estrazione file multimediali](#media-extraction)
* [Estrazione pagina](#page-extraction)

Questo flusso di lavoro è configurato con valori predefiniti che possono essere adattati per la configurazione nelle varie istanze di authoring (si tratta di un flusso di lavoro standard, per cui ulteriori informazioni sono disponibili in [Modifica di un flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se si utilizzano i valori predefiniti (inclusa la porta SOAP), non è necessaria alcuna configurazione.

Dopo l’impostazione, il caricamento di [!DNL InDesign] file in [!DNL Experience Manager Assets] (con uno dei metodi consueti) attiva il flusso di lavoro per elaborare la risorsa e preparare le varie rappresentazioni. Verificare la configurazione caricando un file INDD in [!DNL Experience Manager Assets] per confermare che vengono visualizzate le diverse rappresentazioni create da IDS in `<*your_asset*>.indd/Renditions`

#### Estrazione file multimediali {#media-extraction}

Questo passaggio controlla l’estrazione di file multimediali dal file INDD.

Per personalizzare, puoi modificare la scheda **[!UICONTROL Arguments (Argomenti)]** del passaggio **[!UICONTROL Estrazione file multimediali]**.

![Argomenti di estrazione dei supporti e percorsi di script](assets/media_extraction_arguments_scripts.png)

Argomenti di estrazione dei supporti e percorsi di script

* **Libreria** ExtendScript : Si tratta di una semplice libreria di metodi http get/post, richiesta dagli altri script.

* **Estendi script**: Qui è possibile specificare diverse combinazioni di script. Se si desidera che gli script personalizzati siano eseguiti sul [!DNL InDesign Server], salvare gli script in `/apps/settings/dam/indesign/scripts`.

Per informazioni sugli script [!DNL Adobe InDesign], vedere la [documentazione per lo sviluppo di InDesign ](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>Non modificare la libreria ExtendScript. Questa libreria fornisce la funzionalità HTTP necessaria per comunicare con Sling. Questa impostazione specifica la libreria da inviare a [!DNL InDesign Server] per l&#39;utilizzo in tale libreria.

Lo script `ThumbnailExport.jsx` eseguito dal passaggio del flusso di lavoro Media Extraction genera una rappresentazione in miniatura in formato JPG. Questa rappresentazione viene utilizzata dal passaggio del flusso di lavoro Miniature di processo per generare le rappresentazioni statiche richieste da [!DNL Experience Manager].

Potete configurare il passaggio del flusso di lavoro Miniature di processo per generare rappresentazioni statiche di dimensioni diverse. Assicurarsi di non rimuovere i valori predefiniti, perché sono richiesti dall&#39;interfaccia [!DNL Experience Manager Assets]. Infine, il passaggio del flusso di lavoro Elimina anteprima immagine rimuove la rappresentazione in miniatura JPG, in quanto non è più necessaria.

#### Estrazione pagina {#page-extraction}

Viene creata una pagina [!DNL Experience Manager] dagli elementi estratti. Un gestore di estrazione viene utilizzato per estrarre i dati da una rappresentazione (attualmente HTML o IDML). Questi dati vengono quindi utilizzati per creare una pagina con PageBuilder.

Per personalizzare, è possibile modificare la scheda **[!UICONTROL Argomenti]** del passaggio **[!UICONTROL Estrazione pagina]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestore** estrazione pagina: Dall&#39;elenco a comparsa, selezionare il gestore che si desidera utilizzare. Un gestore estrazione opera su un rendering specifico, scelto da un `RenditionPicker` correlato (consulta l’API `ExtractionHandler`). In un&#39;installazione [!DNL Experience Manager] standard è disponibile quanto segue:
   * Maniglia estrazione esportazione IDML: Funziona sulla rappresentazione `IDML` generata nel passaggio MediaExtract.

* **Nome** pagina: Specificate il nome che desiderate assegnare alla pagina risultante. Se lasciato vuoto, il nome è &quot;page&quot; (o un derivato, se &quot;page&quot; esiste già).

* **Titolo** pagina: Specificate il titolo che desiderate assegnare alla pagina risultante.

* **Percorso** directory principale pagina: Percorso della posizione principale della pagina risultante. Se lasciato vuoto, verrà utilizzato il nodo che contiene le rappresentazioni della risorsa.

* **Modello** pagina: Modello da utilizzare per la generazione della pagina risultante.

* **Progettazione** pagina: Struttura della pagina da utilizzare per la generazione della pagina risultante.

### Configurare il proxy per [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Il lavoratore risiede nell&#39;istanza proxy.

1. Nella console Strumenti, espandere **[!UICONTROL Configurazioni Cloud Services]** nel riquadro a sinistra. Quindi espandere **[!UICONTROL Configurazione proxy cloud]**.

1. Per aprire la configurazione, fai doppio clic su **[!UICONTROL IDS worker]**.

1. Fare clic su **[!UICONTROL Modifica]** per aprire la finestra di dialogo di configurazione e definire le impostazioni richieste:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**
PoolGli endpoint SOAP da utilizzare per comunicare con l&#39; [!DNL InDesign Server]. È possibile aggiungere, rimuovere e ordinare gli elementi necessari.

1. Fai clic su OK per salvare.

### Configurare Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se le [!DNL InDesign Server] e [!DNL Experience Manager] si trovano su host diversi o se una di queste applicazioni non funziona sulle porte predefinite, configurare [!UICONTROL Day CQ Link Externalizer] per impostare il nome host, la porta e il percorso del contenuto per [!DNL InDesign Server].

1. Accedi alla console Web all&#39;indirizzo `https://[aem_server]:[port]/system/console/configMgr`.
1. Individuare la configurazione **[!UICONTROL Day CQ Link Externalizer]**. Fare clic su **[!UICONTROL Modifica]** per aprire.
1. Le impostazioni di Link Externalizer consentono di creare URL assoluti per la [!DNL Experience Manager] distribuzione e per [!DNL InDesign Server]. Utilizzare il campo **[!UICONTROL Domains]** per specificare il nome host e il percorso contestuale per [!DNL Adobe InDesign Server]. Fai clic su **Salva**.

   ![Impostazione del collegamento esternalizzatore](assets/link-externalizer-config.png)

### Abilita elaborazione processi paralleli per [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

È ora possibile abilitare l&#39;elaborazione processi paralleli per gli ID. Determinare il numero massimo di processi paralleli (`x`) che possono essere elaborati da [!DNL InDesign Server]:

* Su un singolo computer multiprocessore, il numero massimo di processi paralleli (`x`) che un processo [!DNL InDesign Server] può elaborare è inferiore di uno al numero di processori che eseguono IDS.
* Quando si esegue IDS su più computer è necessario contare il numero totale di processori disponibili (ossia su tutti i computer), quindi sottrarre il numero totale di computer.

Per configurare il numero di processi IDS paralleli:

1. Aprite la scheda **[!UICONTROL Configurazioni]** della console Felix; ad esempio: `https://[aem_server]:[port]/system/console/configMgr`.

1. Selezionare la coda di elaborazione IDS in `Apache Sling Job Queue Configuration`.

1. Imposta:

   * **Tipo** - `Parallel`
   * **Numero massimo di processi**  paralleli-  `<*x*>` (come calcolato sopra)

1. Salvate queste modifiche.
1. Per abilitare il supporto per più sessioni per  Adobe CS6 e versioni successive, selezionate la casella di controllo `enable.multisession.name`, in `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configurazione.
1. Create un [pool di `x` lavoratori IDS aggiungendo endpoint SOAP alla configurazione di IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Se sono presenti più computer con [!DNL InDesign Server], aggiungere endpoint SOAP (numero di processori per computer -1) per ogni computer.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Quando si lavora con un pool di lavoratori, è possibile abilitare  elenco Bloccati di lavoratori IDS.
>
>A tal fine, abilitare la casella di controllo **[!UICONTROL enable.try.name]**, nella configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, che consente di recuperare i processi IDS.
>
>Inoltre, nella configurazione `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, impostare un valore positivo per il parametro `max.errors.to.blacklist` che determina il numero di recuperi di processi prima di barrare un ID dall&#39;elenco dei gestori di processi.
>
>Per impostazione predefinita, dopo l&#39;ora configurabile (`retry.interval.to.whitelist.name`) in minuti, il lavoro IDS viene nuovamente convalidato. Se il lavoratore viene trovato online, viene rimosso dal elenco Bloccati .

## Abilita il supporto per [!DNL InDesign Server] 10.0 o versione successiva {#enabling-support-for-indesign-server-or-later}

Per [!DNL InDesign Server] 10.0 o versione successiva, eseguite i seguenti passaggi per abilitare il supporto per più sessioni.

1. Aprire Configuration Manager dall&#39;istanza [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificare la configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Selezionare l&#39;opzione **[!UICONTROL ids.cc.enable]**, quindi fare clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Per l&#39;integrazione di [!DNL InDesign Server] con [!DNL Experience Manager Assets], utilizzate un processore multi-core perché la funzione di supporto delle sessioni necessaria per l&#39;integrazione non è supportata nei sistemi single core.

## Configurare le credenziali [!DNL Experience Manager] {#configure-aem-credentials}

Potete modificare le credenziali di amministratore predefinite (nome utente e password) per accedere alla [!DNL InDesign Server] dalla distribuzione [!DNL Experience Manager] senza interrompere l&#39;integrazione con la [!DNL InDesign Server].

1. Passa a `/etc/cloudservices/proxy.html`.
1. Nella finestra di dialogo, specificate il nuovo nome utente e la nuova password.
1. Salvare le credenziali.

>[!MORELIKETHIS]
>
>* [Informazioni su  Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

