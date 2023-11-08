---
title: Integrare [!DNL Assets] con [!DNL InDesign Server]
description: Scopri come integrare [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 4%

---

# Integrare [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilizza:

* Proxy per distribuire il carico di determinate attività di elaborazione. Un proxy è un [!DNL Experience Manager] istanza che comunica con un lavoratore proxy per eseguire un&#39;attività specifica e altre [!DNL Experience Manager] per fornire i risultati.
* Un lavoratore proxy per definire e gestire un&#39;attività specifica.
Questi possono coprire un&#39;ampia gamma di attività; ad esempio, utilizzando un [!DNL InDesign Server] per elaborare i file.

Per caricare completamente i file in [!DNL Experience Manager Assets] creato con [!DNL Adobe InDesign] viene utilizzato un proxy. Questo utilizza un processo di lavoro proxy per comunicare con [!DNL Adobe InDesign Server], dove [script](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) vengono eseguiti per estrarre metadati e generare varie rappresentazioni per [!DNL Experience Manager Assets]. Il proxy worker consente la comunicazione bidirezionale tra [!DNL InDesign Server] e [!DNL Experience Manager] istanze in una configurazione cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] è offerto come due offerte separate. [Adobe InDesign](https://www.adobe.com/products/indesign.html) app desktop utilizzata per progettare layout di pagina per la stampa e la distribuzione digitale. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) consente di creare in modo programmatico documenti automatizzati in base a ciò che è stato creato con [!DNL InDesign]. Funziona come un servizio che offre un’interfaccia ai suoi [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.Gli script sono scritti in [!DNL ExtendScript], che è simile a [!DNL JavaScript]. Per informazioni su [!DNL InDesign] script vedi [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Come funziona l’estrazione {#how-the-extraction-works}

Il [!DNL Adobe InDesign Server] può essere integrato con [!DNL Experience Manager Assets] in modo che i file INDD creati con [!DNL InDesign] possono essere caricati, generati, estratti di tutti i file multimediali (ad esempio, video) e memorizzati come risorse:

>[!NOTE]
>
>Versioni precedenti di [!DNL Experience Manager] sono stati in grado di estrarre l’XMP e la miniatura, ora è possibile estrarre tutti i file multimediali.

1. Carica il file INDD in [!DNL Experience Manager Assets].
1. Un framework invia script di comandi al [!DNL InDesign Server] tramite SOAP (Simple Object Access Protocol).
Questo script di comandi:

   * Recuperate il file INDD.
   * Esegui [!DNL InDesign Server] comandi:

      * Vengono estratti la struttura, il testo ed eventuali file multimediali.
      * Vengono generate le rappresentazioni di PDF e JPG.
      * Vengono generate le rappresentazioni HTML e IDML.

   * Pubblica di nuovo i file risultanti in [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML è un formato basato su XML che esegue il rendering di tutto il contenuto del [!DNL InDesign] file. Viene memorizzato come pacchetto compresso utilizzando [ZIP](https://www.techterms.com/definition/zip) compressione. Per ulteriori informazioni, consulta [Formati di interscambio InDesign INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Se il [!DNL InDesign Server] non è installato o non è configurato, puoi comunque caricare un file INDD in [!DNL Experience Manager]. Tuttavia, le rappresentazioni generate sono limitate a PNG e JPEG. Non sarà possibile generare rappresentazioni HTML, .idml o della pagina.

1. Dopo la generazione dell’estrazione e della rappresentazione:

   * La struttura viene replicata in un `cq:Page` (tipo di rappresentazione).
   * Il testo e i file estratti vengono memorizzati in [!DNL Experience Manager Assets].
   * Tutte le rappresentazioni sono memorizzate in [!DNL Experience Manager Assets], nella risorsa stessa.

## Integrare [!DNL InDesign Server] con Experience Manager {#integrating-the-indesign-server-with-aem}

Per integrare [!DNL InDesign Server] per l&#39;utilizzo con [!DNL Experience Manager Assets] e dopo aver configurato il proxy, è necessario:

1. [Installare l’InDesign Server](#installing-the-indesign-server).
1. Se necessario, [configurare Experience Manager Assets Workflow](#configuring-the-aem-assets-workflow).
Questa operazione è necessaria solo se i valori predefiniti non sono appropriati per l’istanza.
1. Configurare un [lavoratore proxy per InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installare [!DNL InDesign Server] {#installing-the-indesign-server}

Per installare e avviare [!DNL InDesign Server] per l&#39;utilizzo con [!DNL Experience Manager]:

1. Scarica e installa [!DNL InDesign Server].

1. Se necessario, puoi personalizzare la configurazione del [!DNL InDesign Server] dell&#39;istanza.

1. Dalla riga di comando, avvia il server:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Il server verrà avviato con il plug-in SOAP in ascolto sulla porta 8080. Tutti i messaggi di log e l&#39;output vengono scritti direttamente nella finestra di comando.

   >[!NOTE]
   >
   >Se si desidera salvare i messaggi di output in un file, utilizzare il reindirizzamento, ad esempio in Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurare [!DNL Experience Manager Assets] workflow {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispone di un flusso di lavoro preconfigurato **[!UICONTROL Aggiorna risorsa DAM]**, che prevede diversi passaggi di processo specifici per [!DNL InDesign]:

* [Estrazione file multimediali](#media-extraction)
* [Estrazione pagina](#page-extraction)

Questo flusso di lavoro è configurato con valori predefiniti che possono essere adattati per la configurazione nelle varie istanze di authoring (si tratta di un flusso di lavoro standard, per cui ulteriori informazioni sono disponibili in [Modifica di un flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se si utilizzano i valori predefiniti (inclusa la porta SOAP), non è necessaria alcuna configurazione.

Dopo la configurazione, caricamento [!DNL InDesign] file in [!DNL Experience Manager Assets] (secondo uno dei metodi usuali) attiva il flusso di lavoro per elaborare la risorsa e preparare le varie rappresentazioni. Verifica la configurazione caricando un file INDD in [!DNL Experience Manager Assets] per confermare di visualizzare le diverse rappresentazioni create da IDS in `<*your_asset*>.indd/Renditions`

#### Estrazione file multimediali {#media-extraction}

Questo passaggio controlla l&#39;estrazione dei file multimediali dal file INDD.

Per personalizzare, puoi modificare la scheda **[!UICONTROL Arguments (Argomenti)]** del passaggio **[!UICONTROL Estrazione file multimediali]**.

![Argomenti di estrazione dei contenuti multimediali e percorsi di script](assets/media_extraction_arguments_scripts.png)

Argomenti di estrazione dei contenuti multimediali e percorsi di script

* **Libreria ExtendScript**: si tratta di una semplice libreria di metodi http get/post, richiesta dagli altri script.

* **Estendi script**: qui puoi specificare diverse combinazioni di script. Se desideri che gli script vengano eseguiti su [!DNL InDesign Server], salva gli script in `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Non modificare la libreria ExtendScript. Questa libreria fornisce la funzionalità HTTP necessaria per comunicare con Sling. Questa impostazione specifica la libreria da inviare al [!DNL InDesign Server] da utilizzare in tali aree.

Il `ThumbnailExport.jsx` Lo script eseguito dal passaggio del flusso di lavoro Estrazione file multimediali genera una rappresentazione di miniature in formato JPG. Questa rappresentazione viene utilizzata dal passaggio del flusso di lavoro Elabora miniature per generare le rappresentazioni statiche richieste da [!DNL Experience Manager].

Puoi configurare il passaggio del flusso di lavoro Elabora miniature per generare rappresentazioni statiche a dimensioni diverse. Assicurati di non rimuovere i valori predefiniti, perché sono richiesti da [!DNL Experience Manager Assets] di rete. Infine, il passaggio del flusso di lavoro Elimina rappresentazione anteprima immagine rimuove la rappresentazione JPG delle miniature, in quanto non è più necessaria.

#### Estrazione pagina {#page-extraction}

Questo crea un [!DNL Experience Manager] dagli elementi estratti. Un gestore estrazione viene utilizzato per estrarre i dati da una rappresentazione (attualmente HTML o IDML). Questi dati vengono quindi utilizzati per creare una pagina utilizzando PageBuilder.

Per personalizzare, è possibile modificare la scheda **[!UICONTROL Argomenti]** del passaggio **[!UICONTROL Estrazione pagina]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestore estrazione pagina**: dall’elenco a comparsa, seleziona il gestore da utilizzare. Un gestore estrazione opera su un rendering specifico, scelto da un `RenditionPicker` correlato (consulta l’API `ExtractionHandler`). In uno standard [!DNL Experience Manager] installazione è disponibile quanto segue:
   * IDML Export Extraction Handle (Handle di estrazione esportazione IDML): funziona sul `IDML` rendering generato nel passaggio MediaExtract.

* **Nome pagina**: specifica il nome da assegnare alla pagina risultante. Se lasciato vuoto, il nome sarà &quot;page&quot; (o una derivata se &quot;page&quot; esiste già).

* **Titolo pagina**: specifica il titolo da assegnare alla pagina risultante.

* **Percorso principale pagina**: percorso della posizione principale della pagina risultante. Se questo campo viene lasciato vuoto, viene utilizzato il nodo che contiene le rappresentazioni della risorsa.

* **Modello pagina**: modello da utilizzare per generare la pagina risultante.

* **Progettazione pagina**: progettazione della pagina da utilizzare per generare la pagina risultante.

### Configurare il processo di lavoro proxy per [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Il lavoratore risiede nell&#39;istanza proxy.

1. Nella console Strumenti, espandi **[!UICONTROL Configurazioni Cloud Service]** nel riquadro a sinistra. Quindi espandi **[!UICONTROL Configurazione proxy cloud]**.

1. Per aprire la configurazione, fai doppio clic su **[!UICONTROL IDS worker]**.

1. Clic **[!UICONTROL Modifica]** per aprire la finestra di dialogo di configurazione e definire le impostazioni richieste:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool IDS**
Endpoint SOAP da utilizzare per la comunicazione con [!DNL InDesign Server]. È possibile aggiungere, rimuovere e ordinare gli elementi necessari.

1. Fare clic su OK per salvare.

### Configurare Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se il [!DNL InDesign Server] e [!DNL Experience Manager] si trovano su host diversi o una o entrambe queste applicazioni non funzionano sulle porte predefinite, quindi configura [!UICONTROL Day CQ Link Externalizer] per impostare il nome host, la porta e il percorso contenuto per [!DNL InDesign Server].

1. Accedi alla console web all’indirizzo `https://[aem_server]:[port]/system/console/configMgr`.
1. Individua la configurazione **[!UICONTROL Day CQ Link Externalizer]**. Clic **[!UICONTROL Modifica]** per aprire.
1. Le impostazioni di Link Externalizer aiutano a creare URL assoluti per [!DNL Experience Manager] e per [!DNL InDesign Server]. Utilizzare **[!UICONTROL Domini]** per specificare il nome host per [!DNL Adobe InDesign Server]. Fai clic su **Salva**.

   Negli URL assoluti, utilizza `localhost` come nome host per l’istanza locale (di authoring) e come nome host o indirizzo IP per l’istanza di pubblicazione, come illustrato nella figura seguente.

   ![Impostazione Link Externalizer](assets/link-externalizer-config.png)

### Abilita elaborazione parallela processi per [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Ora puoi abilitare l’elaborazione di processi paralleli per gli ID. Determinare il numero massimo di processi paralleli (`x`) un [!DNL InDesign Server] può elaborare:

* Su un singolo computer multiprocessore, il numero massimo di processi paralleli (`x`) che un [!DNL InDesign Server] può elaborare è inferiore di uno al numero di processori che eseguono IDS.
* Quando si eseguono gli ID su più computer, è necessario contare il numero totale di processori disponibili (ossia su tutti i computer) e quindi sottrarre il numero totale di computer.

Per configurare il numero di processi IDS paralleli:

1. Apri **[!UICONTROL Configurazioni]** della console Felix; ad esempio: `https://[aem_server]:[port]/system/console/configMgr`.

1. Seleziona la coda di elaborazione IDS in `Apache Sling Job Queue Configuration`.

1. Imposta:

   * **Tipo** - `Parallel`
   * **Numero massimo processi paralleli** - `<*x*>` (come calcolato sopra)

1. Salva queste modifiche.
1. Per abilitare il supporto di più sessioni per Adobe CS6 e versioni successive, selezionare `enable.multisession.name` casella di controllo, in `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configurazione.
1. Creare un [pool di `x` processi di lavoro IDS mediante l&#39;aggiunta di endpoint SOAP alla configurazione di IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Se sono presenti più computer in esecuzione [!DNL InDesign Server], aggiungere endpoint SOAP (numero di processori per computer -1) per ogni computer.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Quando si lavora con un pool di lavoratori, è possibile abilitare l&#39;elenco Bloccati dei lavoratori IDS.
>
>Per farlo, abilita **[!UICONTROL enable.retry.name]** casella di controllo, sotto `com.day.cq.dam.ids.impl.IDSJobProcessor.name` che abilita i processi di recupero degli IDS.
>
>Inoltre, sotto `com.day.cq.dam.ids.impl.IDSPoolImpl.name` , imposta un valore positivo per `max.errors.to.blacklist` parametro che determina il numero di tentativi del processo prima di bloccare un ID dall&#39;elenco dei gestori di processi.
>
>Per impostazione predefinita, dopo il file configurabile (`retry.interval.to.whitelist.name`) ora in minuti in cui il processo di lavoro IDS viene riconvalidato. Se il lavoratore viene trovato online, viene rimosso dall&#39;elenco Bloccati.

## Abilita supporto per [!DNL InDesign Server] 10.0 o successiva {#enabling-support-for-indesign-server-or-later}

Per [!DNL InDesign Server] versione 10.0 o successiva, effettuare le seguenti operazioni per abilitare il supporto per più sessioni.

1. Apri Configuration Manager dal tuo [!DNL Experience Manager Assets] istanza `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificare la configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Seleziona la **[!UICONTROL ids.cc.enable]** e fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Per [!DNL InDesign Server] integrazione con [!DNL Experience Manager Assets], utilizza un processore multi-core perché la funzione di supporto della sessione necessaria per l&#39;integrazione non è supportata sui sistemi single-core.

## Configura [!DNL Experience Manager] credenziali {#configure-aem-credentials}

È possibile modificare le credenziali di amministratore predefinite (nome utente e password) per accedere al [!DNL InDesign Server] dal tuo [!DNL Experience Manager] senza interrompere l&#39;integrazione con [!DNL InDesign Server].

1. Passa a `/etc/cloudservices/proxy.html`.
1. Nella finestra di dialogo, specifica il nuovo nome utente e la nuova password.
1. Salva le credenziali.

>[!MORELIKETHIS]
>
>* [Informazioni su Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)
