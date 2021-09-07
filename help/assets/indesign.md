---
title: Integrare [!DNL Assets] con [!DNL InDesign Server]
description: Scopri come integrare [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: f74190692d718da6074affa87d283f326eca7faa
workflow-type: tm+mt
source-wordcount: '1577'
ht-degree: 4%

---

# Integrare [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilizza:

* Un proxy per distribuire il carico di alcune attività di elaborazione. Un proxy è un&#39;istanza [!DNL Experience Manager] che comunica con un proxy worker per eseguire un&#39;attività specifica e altre istanze [!DNL Experience Manager] per fornire i risultati.
* Un processo di lavoro proxy per definire e gestire un’attività specifica.
Questi possono coprire un&#39;ampia gamma di compiti; ad esempio, utilizzando un tag [!DNL InDesign Server] per elaborare i file.

Per caricare completamente i file in [!DNL Experience Manager Assets] creati con [!DNL Adobe InDesign] viene utilizzato un proxy. Questo utilizza un processo di lavoro proxy per comunicare con [!DNL Adobe InDesign Server], dove [gli script](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) vengono eseguiti per estrarre i metadati e generare diverse rappresentazioni per [!DNL Experience Manager Assets]. Il proxy worker abilita la comunicazione bidirezionale tra le istanze [!DNL InDesign Server] e [!DNL Experience Manager] in una configurazione cloud.

>[!NOTE]
>
>[!DNL Adobe InDesign] viene offerto come due offerte separate. [Adobe app desktop ](https://www.adobe.com/products/indesign.html) InDesigndesktop utilizzata per progettare layout di pagina per la stampa e la distribuzione digitale. [Adobe InDesign ](https://www.adobe.com/products/indesignserver.html) Server consente di creare in modo programmatico documenti automatizzati in base a ciò che hai creato con  [!DNL InDesign]. Funziona come un servizio che offre un&#39;interfaccia al suo motore [ExtendScript](https://www.adobe.com/devnet/scripting.html).Gli script sono scritti in [!DNL ExtendScript], che è simile a [!DNL JavaScript]. Per informazioni sugli script [!DNL InDesign], consulta [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Come funziona l’estrazione {#how-the-extraction-works}

È possibile integrare [!DNL Adobe InDesign Server] con [!DNL Experience Manager Assets] in modo che i file INDD creati con [!DNL InDesign] possano essere caricati, generati rendering, tutti i file multimediali estratti (ad esempio, video) e memorizzati come risorse:

>[!NOTE]
>
>Le versioni precedenti di [!DNL Experience Manager] erano in grado di estrarre XMP e la miniatura, ora è possibile estrarre tutti i file multimediali.

1. Carica il file INDD in [!DNL Experience Manager Assets].
1. Un framework invia script di comando a [!DNL InDesign Server] tramite SOAP (Simple Object Access Protocol).
Questo script di comando:

   * Recupera il file INDD.
   * Esegui i comandi [!DNL InDesign Server]:

      * Vengono estratti la struttura, il testo e tutti i file multimediali.
      * Vengono generate rappresentazioni PDF e JPG.
      * Vengono generati rendering HTML e IDML.
   * Ripubblicare i file risultanti su [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML è un formato basato su XML che esegue il rendering di tutti i contenuti del file [!DNL InDesign]. Viene memorizzato come pacchetto compresso utilizzando la compressione [ZIP](https://www.techterms.com/definition/zip). Per ulteriori informazioni, consulta [Formati di interscambio InDesign INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Se [!DNL InDesign Server] non è installato o non è configurato, puoi comunque caricare un file INDD in [!DNL Experience Manager]. Tuttavia, le rappresentazioni generate saranno limitate a PNG e JPEG. Non sarà possibile generare rappresentazioni HTML, idml o pagina.

1. Dopo la generazione di estrazione e rendering:

   * La struttura viene replicata in un `cq:Page` (tipo di rendering).
   * Il testo e i file estratti vengono memorizzati in [!DNL Experience Manager Assets].
   * Tutte le rappresentazioni sono memorizzate in [!DNL Experience Manager Assets], nella risorsa stessa.

## Integra il [!DNL InDesign Server] con l’Experience Manager {#integrating-the-indesign-server-with-aem}

Per integrare [!DNL InDesign Server] da utilizzare con [!DNL Experience Manager Assets] e dopo aver configurato il proxy, è necessario:

1. [Installa InDesign Server](#installing-the-indesign-server).
1. Se necessario, [configura il flusso di lavoro Risorse di Experience Manager](#configuring-the-aem-assets-workflow).
Ciò è necessario solo se i valori predefiniti non sono appropriati per l’istanza.
1. Configura un processo di lavoro proxy [per InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installa il [!DNL InDesign Server] {#installing-the-indesign-server}

Per installare e avviare [!DNL InDesign Server] per l&#39;utilizzo con [!DNL Experience Manager]:

1. Scarica e installa il [!DNL InDesign Server].

1. Se necessario, puoi personalizzare la configurazione dell’istanza [!DNL InDesign Server].

1. Dalla riga di comando, avvia il server:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Verrà avviato il server con il plug-in SOAP in ascolto sulla porta 8080. Tutti i messaggi e gli output di log vengono scritti direttamente nella finestra dei comandi.

   >[!NOTE]
   >
   >Se si desidera salvare i messaggi di output in un file, utilizzare il reindirizzamento; ad esempio, in Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurare il flusso di lavoro [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] dispone di un flusso di lavoro preconfigurato  **[!UICONTROL DAM Update Asset]**, con diversi passaggi di processo specifici per  [!DNL InDesign]:

* [Estrazione file multimediali](#media-extraction)
* [Estrazione pagina](#page-extraction)

Questo flusso di lavoro è configurato con valori predefiniti che possono essere adattati per la configurazione sulle varie istanze di authoring (si tratta di un flusso di lavoro standard, quindi ulteriori informazioni sono disponibili in [Modifica di un flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se si utilizzano i valori predefiniti (inclusa la porta SOAP), non è necessaria alcuna configurazione.

Dopo la configurazione, il caricamento di file [!DNL InDesign] in [!DNL Experience Manager Assets] (con uno dei metodi consueti) attiva il flusso di lavoro per elaborare la risorsa e preparare le varie rappresentazioni. Verifica la configurazione caricando un file INDD in [!DNL Experience Manager Assets] per confermare che sono presenti diverse rappresentazioni create da IDS in `<*your_asset*>.indd/Renditions`

#### Estrazione di file multimediali {#media-extraction}

Questo passaggio controlla l’estrazione dei file multimediali dal file INDD.

Per personalizzare, puoi modificare la scheda **[!UICONTROL Arguments (Argomenti)]** del passaggio **[!UICONTROL Estrazione file multimediali]**.

![Argomenti di estrazione file multimediali e percorsi di script](assets/media_extraction_arguments_scripts.png)

Argomenti di estrazione file multimediali e percorsi di script

* **Libreria** ExtendScript: Si tratta di una semplice libreria di metodi http get/post, necessaria per gli altri script.

* **Estendi script**: Qui è possibile specificare diverse combinazioni di script. Se si desidera che gli script personalizzati vengano eseguiti su [!DNL InDesign Server], salvare gli script in `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Non modificare la libreria ExtendScript. Questa libreria fornisce la funzionalità HTTP necessaria per comunicare con Sling. Questa impostazione specifica la libreria da inviare al [!DNL InDesign Server] per l&#39;utilizzo in tale ambiente.

Lo script `ThumbnailExport.jsx` eseguito dal passaggio del flusso di lavoro Estrazione file multimediali genera un rendering delle miniature in formato JPG. Questo rendering viene utilizzato dal passaggio del flusso di lavoro Elabora miniature per generare le rappresentazioni statiche richieste da [!DNL Experience Manager].

Puoi configurare il passaggio del flusso di lavoro Elabora miniature per generare rappresentazioni statiche con dimensioni diverse. Assicurati di non rimuovere i valori predefiniti, in quanto sono richiesti dall&#39;interfaccia [!DNL Experience Manager Assets]. Infine, il passaggio del flusso di lavoro Elimina anteprima immagine rimuove il rendering delle miniature JPG, in quanto non è più necessario.

#### Estrazione pagina {#page-extraction}

Viene creata una pagina [!DNL Experience Manager] dagli elementi estratti. Un gestore estrazione viene utilizzato per estrarre dati da un rendering (attualmente HTML o IDML). Questi dati vengono quindi utilizzati per creare una pagina utilizzando PageBuilder.

Per personalizzare, è possibile modificare la scheda **[!UICONTROL Argomenti]** del passaggio **[!UICONTROL Estrazione pagina]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Gestore** estrazione pagina: Dall&#39;elenco a comparsa, selezionare il gestore che si desidera utilizzare. Un gestore estrazione opera su un rendering specifico, scelto da un `RenditionPicker` correlato (consulta l’API `ExtractionHandler`). In un&#39;installazione standard [!DNL Experience Manager] è disponibile quanto segue:
   * Maniglia di estrazione esportazione IDML: Funziona sul rendering `IDML` generato nel passaggio MediaExtract.

* **Nome** pagina: Specifica il nome da assegnare alla pagina risultante. Se lasciato vuoto, il nome è &quot;page&quot; (o un derivato, se &quot;page&quot; esiste già).

* **Titolo** pagina: Specifica il titolo da assegnare alla pagina risultante.

* **Percorso** principale pagina: Percorso della posizione principale della pagina risultante. Se lasciato vuoto, verrà utilizzato il nodo contenente le rappresentazioni della risorsa.

* **Modello** pagina: Modello da utilizzare per la generazione della pagina risultante.

* **Progettazione** pagina: Progettazione di pagina da utilizzare per la generazione della pagina risultante.

### Configura il processo di lavoro proxy per [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Il processo di lavoro risiede nell&#39;istanza proxy.

1. Nella console Strumenti , espandi **[!UICONTROL Configurazioni Cloud Services]** nel riquadro a sinistra. Quindi espandi **[!UICONTROL Cloud Proxy Configuration]**.

1. Per aprire la configurazione, fai doppio clic su **[!UICONTROL IDS worker]**.

1. Fai clic su **[!UICONTROL Modifica]** per aprire la finestra di dialogo di configurazione e definire le impostazioni richieste:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**
PoolEndpoint SOAP da utilizzare per la comunicazione con  [!DNL InDesign Server]. È possibile aggiungere, rimuovere e ordinare gli elementi necessari.

1. Fai clic su OK per salvare.

### Configurare Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se le [!DNL InDesign Server] e [!DNL Experience Manager] si trovano su host diversi o se una o entrambe le applicazioni non funzionano sulle porte predefinite, configura [!UICONTROL Day CQ Link Externalizer] per impostare il nome host, la porta e il percorso del contenuto per [!DNL InDesign Server].

1. Accedi alla console Web all&#39;indirizzo `https://[aem_server]:[port]/system/console/configMgr`.
1. Individua la configurazione **[!UICONTROL Day CQ Link Externalizer]**. Fai clic su **[!UICONTROL Modifica]** per aprire.
1. Le impostazioni di Link Externalizer consentono di creare URL assoluti per la distribuzione [!DNL Experience Manager] e per la [!DNL InDesign Server]. Utilizza il campo **[!UICONTROL Domains]** per specificare il nome host per il [!DNL Adobe InDesign Server]. Fai clic su **Salva**.

   Quando crei URL assoluti, devi utilizzare il nome host `localhost` per le istanze locali, di authoring e di pubblicazione.

   ![Impostazione del collegamento esternalizzatore](assets/link-externalizer-config.png)

### Abilita elaborazione processi paralleli per [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

È ora possibile abilitare l&#39;elaborazione dei processi paralleli per gli ID. Determinare il numero massimo di processi paralleli (`x`) che possono essere elaborati da [!DNL InDesign Server]:

* Su un singolo computer multiprocessore, il numero massimo di processi paralleli (`x`) che un [!DNL InDesign Server] può elaborare è inferiore di uno al numero di processori che eseguono ID.
* Quando si esegue l&#39;ID su più computer è necessario contare il numero totale di processori disponibili (ossia su tutti i computer), quindi sottrarre il numero totale di macchine.

Per configurare il numero di processi IDS paralleli:

1. Apri la scheda **[!UICONTROL Configurazioni]** della console Felix; ad esempio: `https://[aem_server]:[port]/system/console/configMgr`.

1. Seleziona la coda di elaborazione IDS in `Apache Sling Job Queue Configuration`.

1. Imposta:

   * **Tipo** - `Parallel`
   * **Processi**  paralleli massimi -  `<*x*>` (come calcolato sopra)

1. Salva queste modifiche.
1. Per abilitare il supporto per più sessioni per Adobe CS6 e versioni successive, seleziona la casella di controllo `enable.multisession.name` nella configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Crea un [pool di processi di lavoro `x` IDS aggiungendo endpoint SOAP alla configurazione IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Se sono presenti più computer in esecuzione [!DNL InDesign Server], aggiungere endpoint SOAP (numero di processori per computer -1) per ogni computer.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Quando si lavora con un pool di lavoratori, è possibile abilitare l&#39;elenco Bloccati di lavoratori IDS.
>
>Per farlo, abilita la casella di controllo **[!UICONTROL enable.try.name]**, nella configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, che abilita i recuperi dei processi IDS.
>
>Inoltre, nella configurazione `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, imposta un valore positivo per il parametro `max.errors.to.blacklist` che determina il numero di recuperi di processi prima di assegnare un ID dall&#39;elenco dei gestori di processi.
>
>Per impostazione predefinita, dopo il tempo configurabile (`retry.interval.to.whitelist.name`) in minuti, il processo di lavoro IDS viene riconvalidato. Se il lavoratore viene trovato online, viene rimosso dall&#39;elenco Bloccati.

## Abilita il supporto per [!DNL InDesign Server] 10.0 o versione successiva {#enabling-support-for-indesign-server-or-later}

Per [!DNL InDesign Server] 10.0 o versioni successive, esegui i seguenti passaggi per abilitare il supporto per più sessioni.

1. Apri Configuration Manager dall&#39;istanza [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifica la configurazione `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Seleziona l&#39;opzione **[!UICONTROL ids.cc.enable]** e fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Per l&#39;integrazione di [!DNL InDesign Server] con [!DNL Experience Manager Assets], utilizza un processore multi-core perché la funzionalità di supporto della sessione necessaria per l&#39;integrazione non è supportata sui sistemi single-core.

## Configurare le credenziali [!DNL Experience Manager] {#configure-aem-credentials}

È possibile modificare le credenziali di amministratore predefinite (nome utente e password) per accedere a [!DNL InDesign Server] dalla distribuzione [!DNL Experience Manager] senza interrompere l&#39;integrazione con [!DNL InDesign Server].

1. Passa a `/etc/cloudservices/proxy.html`.
1. Nella finestra di dialogo , specifica il nuovo nome utente e la nuova password.
1. Salva le credenziali.

>[!MORELIKETHIS]
>
>* [Informazioni su Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

