---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: '"[!DNL Adobe Experience Manager] Note 6.5 che descrivono le informazioni sulla versione, le novità, le modalità di installazione e gli elenchi dettagliati delle modifiche."'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '2630'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.12.0 |
| Tipo | Versione Service Pack |
| Data | 24 febbraio 2022 |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip) |

## Cosa è incluso in [!DNL Adobe Experience Manager] 6.5.12.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.12.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 di aprile 2019. Il service pack è installato in [!DNL Adobe Experience Manager] 6.5.

Funzioni chiave e miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.12.0:

* Dopo aver configurato una connessione tra le implementazioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell’implementazione di Sites. È ora possibile aggiornare, eliminare, ridenominare e spostare le risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nella distribuzione di Sites (NPR-37816).

* Per impostazione predefinita, è ora possibile eseguire il rollout di un’origine Live Copy in più Live Copy senza richiedere una configurazione blueprint (CQ-4259951).
* Lo stato delle operazioni asincrone in corso viene ora mostrato nell’interfaccia utente per impedire agli utenti di attivare accidentalmente più operazioni asincrone sullo stesso percorso (NPR-37611).
* È disponibile il supporto per l’autenticazione basata su IMS per le API di Analytics 2.0 (CQ-4285474, NPR-37803, NPR-37701, NPR-37702, NPR-37703).
* Supporto API per il frammento esperienza di tipo offerta JSON (NPR-37796).
* È ora disponibile una richiesta di offerta per l’opzione Elimina offerta (API frammento esperienza) in IMS (NPR-37668).
* L’archivio incorporato (Apache Jackrabbit Oak) rimane ancora a 1.22.9.

Di seguito è riportato l’elenco delle correzioni fornite in [!DNL Experience Manager] Versione 6.5.12.0.

### [!DNL Sites] {#sites-65120}

I seguenti problemi sono risolti in [!DNL Sites]:

* Il layout delle proprietà del frammento di contenuto viene interrotto in quanto le schede Base e Avanzate non hanno margini a sinistra (SITES-4484).
* L’opzione per chiudere il banner sui frammenti di contenuto, a cui si fa riferimento in varie pagine di siti, non funziona. Questo banner informa gli utenti che il frammento di contenuto è menzionato in una o più pagine (SITES-4173).
* Le caselle di controllo non sono allineate nella finestra di dialogo Ripristina ereditarietà (SITES-3514).
* La pagina del modello sui siti web-retail e wknd è interrotta, in quanto i componenti non vengono caricati e l’opzione di struttura non è disponibile, in quanto il servlet pageinfo.json è bloccato su LaunchManagerImpl.getLaunchStream (SITES-3489).
* La pubblicazione del nodo utente dall&#39;ambiente Author a Publish non funziona (NPR-38005).
* Il tentativo di creare un frammento di esperienza utilizzando un modello modificato non mostra le modifiche apportate alle proprietà della pagina iniziale (NPR-37962).
* L&#39;operazione di spostamento della pagina all&#39;Experience Manager è lenta (NPR-37961).
* La traduzione dei frammenti di esperienza non aggiorna i riferimenti ai percorsi di copia della lingua (NPR-37953).
* Gli utenti senza autorizzazioni di replica non sono in grado di eliminare o spostare le pagine, anche se le pagine non sono attivate (NPR-37936).
* Gli errori di tipo org.apache.felix.metype casuali vengono osservati sul server (NPR-37935).
* I riferimenti nell’interfaccia utente touch dell’amministratore di Sites non visualizzano correttamente i collegamenti in ingresso (NPR-37934).
* Il percorso di avvio per aggiungere nuove pagine o risorse non è disponibile quando si selezionano le pagine in un processo di traduzione (NPR-37912).
* Le pagine di riferimento in un componente elenco aggiunto nei frammenti esperienza non vengono aggiornate alla pagina di destinazione durante la promozione del lancio (NPR-37886).
* L’ambiente di authoring presenta problemi di interfaccia utente, ad esempio il titolo della pagina in modalità di modifica non è centrato e il selettore dei componenti consentiti nell’editor dei criteri: la casella di controllo del gruppo occupa l&#39;intera larghezza del contenitore, in modo che l&#39;etichetta venga riprodotta nella riga successiva (NPR-37878).
* [Piattaforma] Il numero di versione di xmlns:metype nel file metype.xml di commons-httpclient è &quot;http://www.osgi.org/xmlns/metatype/v1.0.0&quot; invece di &quot;http://www.osgi.org/xmlns/metatype/v1.2.0&quot; (NPR-37865).
* Gli errori vengono osservati e le pagine non si spostano quando si tenta di passare a una pagina (NPR-37864).
* [Editor Rich Text] L’immagine non viene resa nell’interfaccia classica quando si aggiunge l’immagine come voce di elenco nell’Editor Rich Text (NPR-37835).
* Gli autori possono applicare tag esterni al percorso principale configurato quando utilizzano un campo tag in una finestra di dialogo (NPR-37834).
* Multifield non esegue il rendering corretto nel contenitore di layout e restituisce un errore (NPR-37811).
* Il tentativo di ridimensionare il layout del componente nell’editor di pagine non funziona nel layout mobile (NPR-37805).
* La traduzione dei frammenti esperienza non aggiorna i riferimenti ciclici ai percorsi di copia della lingua (NPR-37745).
* L’utilizzo di un campo RTF cq-msm-lockable nelle proprietà della pagina non disattiva il campo durante il rollout della pagina e può essere modificato dagli autori (NPR-37714).
* Quando si attiva un frammento di esperienza, l’editore invia molte richieste di attivazione a Dispatcher (NPR-37707).
* Alla modifica della topologia, il processo Sling per l’elaborazione delle risorse viene reimpostato e i processi in corso al momento della modifica della topologia vengono ignorati (NPR-37706).
* I contrassegni, i punti incrociati e i trattini non vengono esportati in CSV quando gli utenti di MacOS esportano siti e URL di risorse (NPR-37698).
* Il contenitore di layout nel modello di pagina SPA non è in grado di registrare le classi CSS personalizzate definite nel criterio del modello quando si eseguono le risposte SPA pagine (NPR-37697).
* L&#39;immagine di sfondo non è visibile quando l&#39;utente seleziona il targeting di un frammento di esperienza con sfondo nel contenitore (NPR-37662).
* Il lavoro di traduzione in un frammento di esperienza non traduce tutti i componenti in quel frammento di esperienza (NPR-37660).
* La traduzione dei frammenti di esperienza e la pagina contenente il frammento di esperienza non aggiorna il percorso di lancio nel collegamento al frammento di esperienza (NPR-37659).
* Il widget Caricamento file non mostra il nome del file, quando un file viene caricato e la finestra di dialogo viene salvata (NPR-37634).
* L’attivazione pianificata (pubblicazione) della risorsa non si attiva all’ora pianificata se la cartella contenente la risorsa viene spostata (NPR-37621).
* [Piattaforma] Il dashboard per il controllo dei collegamenti esterni non riesce a riprodurre i risultati in [!DNL Adobe Experience Manager] WCM (NPR-37614).
* L’editor dei frammenti di contenuto non funziona correttamente se vengono utilizzate lettere maiuscole nei nomi dei tag durante la modifica dei tag nell’editor (NPR-37601).
* L&#39;editor dell&#39;interfaccia utente classica non mostra la registrazione come nella visualizzazione dell&#39;interfaccia utente touch (NPR-37588).
* Errore intermittente 500 durante l’aggiunta di un frammento di esperienza ai processi di traduzione (NPR-37587).
* Gli autori possono selezionare e utilizzare la data del selettore data anche nel selettore data disabilitato (NPR-37583).
* [Foundation] Gli autori non possono immettere alcuni valori decimali nel tipo di risorsa campo numerico in una struttura di dialogo dei componenti per l’interfaccia utente touch (NPR-37059).
* I percorsi nella cartella libs vengono eliminati durante l&#39;installazione dei service pack precedenti (NPR-36815).
* [Commerce] La disattivazione di una cartella principale non modifica lo stato di disattivazione dei prodotti secondari in [!DNL Experience Manager Commerce] console; inoltre, il numero di cartelle figlie di una cartella principale al momento della disattivazione non viene visualizzato correttamente nell&#39;interfaccia utente (CQ-4338261).
* [Flusso di lavoro di localizzazione] Il contenuto per la personalizzazione delle colonne e del branding non è localizzato nella finestra di dialogo Admin Control (Controllo amministrazione), quando si seleziona l’icona sotto l’icona del profilo in [!DNL Adobe Experience Manager] inbox (CQ-4334864).
* [Community] Non è possibile fare clic sul contenuto all’interno della tabella per i membri del gruppo (CQ-4334404).
* [Oak] Il processo di sincronizzazione in standby a freddo non funziona e si verifica un errore di registrazione (CQ-433868).
* [Interfaccia utente di Platform Foundation] [!DNL Experience Manager] la pagina iniziale viene visualizzata nuovamente quando l&#39;utente seleziona [!DNL Adobe Experience Manager] icona già presente nella pagina iniziale (CQ-4317409).

### [!DNL Assets] {#assets-65120}

<!--
The following accessibility enhancements are available in [!DNL Assets]:

* enhancement 1
-->

I seguenti problemi sono risolti in [!DNL Assets]:

* Quando si aggiunge una risorsa o una cartella (contenente `single quote` nel nome) in Risorse collegate, il percorso di riferimento non riesce e si verifica come eccezione (NPR-37712).
* Quando si aggiunge una filigrana a una risorsa, la filigrana viene sempre visualizzata in nero, indipendentemente dal colore definito dall’utente (NPR-37720).
* Quando si utilizzano le risorse collegate, un utente non amministratore è in grado di cercare una risorsa anche quando gli utenti non amministratori sono limitati ad accedere all’archivio DAM (NPR-37644).
* Quando si aggiornano i metadati delle risorse mediante la modifica collettiva, le modifiche applicate ai campi a discesa non vengono salvate e reimpostate sui valori predefiniti (NPR-37345).
* L&#39;eliminazione di una cartella richiede troppo tempo e influisce sulle prestazioni complessive (NPR-37107).
* Quando si applicano regole nello schema metadati, l&#39;utente non è in grado di visualizzare il valore completo del menu a discesa `Field Value` e `Field Choices` se il valore è maggiore della casella di testo (CQ-4338074).
* Dopo l’aggiornamento alla versione 6.5.10.0, la pagina delle proprietà della risorsa riflette un messaggio di rendering HTML non necessario (CQ-4336994).
* Ordinamento delle risorse in `List View` non funziona in modo efficace (CQ-4335298).
* Quando condividi le risorse utilizzando il collegamento di condivisione, le risorse vengono scaricate in cartelle separate (CQ-4335000).
* Quando si verifica il [!DNL Experience Manager] `Inbox` le impostazioni `Share` e `Out of office` le schede riflettono il contenuto non tradotto (CQ-4334858).

* Le seguenti correzioni sono relative ai metadati a cascata nelle proprietà delle risorse.
   * Un elenco a discesa obbligatorio riflette più messaggi di errore per ogni selezione nel campo multivalore (NPR-37859).
   * Solo l’ultima selezione del campo padre viene salvata per il campo non modificabile dipendente (NPR-37858).
   * Il menu a discesa dipendente (campo multivalore) riflette il valore predefinito a intermittenza per il menu a discesa principale selezionato (NPR-37791).


### [!DNL Dynamic Media] {#dynamic-media-65120}

I seguenti problemi sono risolti in [!DNL Dynamic Media]:

* Le risorse di una cartella contenente `renditions` nel nome della cartella non vengono sincronizzati in `Dynamic Media` (CQ-4338428).
* Quando crei un predefinito per immagini in `tiff` viene creato il predefinito, ma il formato cambia in `jpeg` (CQ-4335985)
* Quando modifichi la `Progressive JPEG Scan` nell’Editor predefiniti per immagini, il valore a discesa reimposta sempre su `auto`(CQ-4335971).
* I metadati video non sono visibili per il `mxf` video sulla pagina delle proprietà della risorsa (CQ-4335499).
* Durante la rielaborazione delle risorse video, le rappresentazioni AVS (Adaptive Video Set) e video vengono annullate dalla pubblicazione dal server Publish (CQ-4335461).
* Le miniature di PDF generate sono diverse dalla prima pagina dell’effettivo PDF. Alcune parti dell&#39;immagine sono mancanti nella miniatura (CQ-4315554).
* L’annullamento della validità della CDN non riesce con una risposta URL errata se `companyName` e `companyRoot` sono diversi (CQ-4339896).

### Flussi di lavoro {#workflows-65120}

* Lo scorrimento non funziona come previsto se si applica un filtro agli elementi della casella in entrata (CQ-4333594).


### [!DNL Forms] {#forms-65120}


>[!NOTE]
>
>* I pacchetti del componente aggiuntivo [!DNL Experience Manager Forms] vengono rilasciati una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].


<!--

**Adaptive Forms**

* Accessibility – When you set the `Wizard` layout for a panel in an adaptive form, the navigation buttons do not have Aria labels and role (NPR-37613).

* Validations on a date field in an adaptive form does not work, as expected (NPR-37556).

* When the label text for the Checkbox and Radio Button components is long, the text does not fit appropriately (NPR-37294).

* When you apply styling changes to the Thank You message of the AEM Forms Container component, the changes do not replicate in the source adaptive form (NPR-37284).

* Differences in the value of the `Switch` component on the user interface and in the backend (NPR-37268).

* When you use the keyboard keys to navigate to the `Submit` option and press the `Enter` key, you can submit the adaptive form multiple times (CQ-4333993).

* The Remove operation for the File Attachment component does not work, as expected (NPR-37376).

* When a label for a field exceeds 1000 characters in an adaptive form that translates to various languages, the dictionary fails to retrieve the translation of the label (CQ-4329290).

**Document Services**

* An error displays while using the Assembler service (NPR-37606):

  ```TXT
    500 Internal Server Error
  ```

* When the document attachments are passed to the Assembler service, the following exception displays (NPR-37582):

  ```TXT
    com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
  ```

* Missing closing parenthesis from data after converting a PDF document to a PDF-A/1B PDF document (NPR-37608).

**HTML5 Forms**

* When you install AEM 6.5.10.0, the HTML preview for an XDP form does not work (NPR-37503, CQ-4331926).

* Text overlapping issues while migrating the PDF forms to HTML 5 forms in various languages (NPR-37173).

**Letters**

* When you submit a letter and reopen it in HTML view, the position of text document fragments does not remain the same (NPR-37307).

**Forms Workflow**

* In case of embedded container workflow, you get multiple workflow completion emails even after selecting the `Notify on Complete of Container Workflow` option (NPR-37280).

**Foundation JEE**

* After installing AEM 6.5 Forms Service Pack 9, the CRX repository URLs are no longer available (NPR-37592).

**Issues fixed in AEM Forms 6.5.11.1**

>[!NOTE]
>
>If you have not upgraded to AEM 6.5.11.0 Forms, install the AEM Forms 6.5.11.1 add-on package directly. If you have installed AEM 6.5.11.0 Forms, Adobe recommends to upgrade to AEM 6.5.11.1 Forms.

* Submit actions, Send Email and Invoke an AEM Workflow stop working after installing the Forms 6.5.11.0 add-on package.
* CreatePDF operation stops converting Microsoft Word documents to PDF documents after installing the Forms 6.5.11.0 add-on package.
* (JEE Only) Critical security vulnerabilities (CVE-2021-44228 and CVE-2021-45046) reported for Apache Log4j2.
* (JEE only) Assembler DSC in 6.5.11.0 patch contains incorrect metainfo like specification version and impl version.

-->


Per informazioni sugli aggiornamenti di sicurezza, consulta [[!DNL Experience Manager] pagina dei bollettini sulla sicurezza](https://helpx.adobe.com/security/products/experience-manager.html).

## Installare la versione 6.5.12.0 {#install}

**Requisiti di configurazione e ulteriori informazioni**

* Experience Manager 6.5.12.0 richiede Experience Manager 6.5. Vedi [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate.
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).
* In una distribuzione con MongoDB e più istanze, installa Experience Manager 6.5.12.0 in una delle istanze Autore utilizzando Gestione pacchetti.

>[!NOTE]
>
>Adobe sconsiglia di rimuovere o disinstallare il [!DNL Adobe Experience Manager] pacchetto 6.5.12.0.

### Installare il service pack {#install-service-pack}

Per installare il service pack su un [!DNL Adobe Experience Manager] 6.5 istanza, segui questi passaggi:

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia un riavvio se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di installare, scegli uno snapshot o un nuovo backup del tuo [!DNL Experience Manager] istanza.

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip).

1. Apri Gestione pacchetti e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l&#39;istanza dopo l&#39;installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l&#39;istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude durante l’installazione del service pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere, questo problema si verifica in [!DNL Safari] browser ma può verificarsi a intermittenza su qualsiasi browser.

**Installazione automatica**

Sono disponibili due modi per installare automaticamente [!DNL Experience Manager] 6.5.12.0 su un&#39;istanza funzionante:

A. Inserire il pacchetto in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Utilizza il [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzo `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>Adobe Experience Manager 6.5.12.0 non supporta l’installazione di Bootstrap.

**Convalida l&#39;installazione**

1. La pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa di versione aggiornata `Adobe Experience Manager (6.5.12.0)` sotto [!UICONTROL Prodotti installati].

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (Usa console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.2.2.3 o successiva (Utilizzare la console Web: `/system/console/bundles`).

Per informazioni sulle piattaforme certificate per l’utilizzo con questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

UberJar per Experience Manager 6.5.12.0 è disponibile nella variabile [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.12/).

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includere nel POM del progetto la seguente dipendenza:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.12</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece dell’archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Quindi, non c&#39;è `classifier`con `apis` come valore, per `dependency` tag .

## Funzioni obsolete {#removed-deprecated-features}

Di seguito è riportato un elenco di funzioni e funzionalità contrassegnate come obsolete con [!DNL Experience Manager] 6.5.7.0. Le funzioni sono inizialmente dichiarate obsolete e successivamente rimosse in una versione futura. È disponibile un’opzione alternativa.

Controlla se utilizzi una funzione o una funzionalità in una distribuzione. Inoltre, pianifica di modificare l’implementazione in modo da utilizzare un’opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrazioni | La **[!UICONTROL Opt-in di AEM Cloud Services]** la schermata è obsoleta poiché la [!DNL Experience Manager] e [!DNL Adobe Target] L’integrazione viene aggiornata in Experience Manager 6.5. L’integrazione supporta l’API Adobe Target Standard. L’API utilizza l’autenticazione tramite Adobe IMS e [!DNL Adobe I/O] e sostiene il ruolo crescente di Launch Adobe per lo strumento [!DNL Experience Manager] nelle pagine di analisi e personalizzazione, la procedura guidata di consenso è funzionalmente irrilevante. | Configura le connessioni di sistema, l’autenticazione Adobe IMS e [!DNL Adobe I/O] integrazioni tramite le rispettive [!DNL Experience Manager] servizi cloud. |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto, ad Experience Manager 6.5. | N/D |

## Problemi noti {#known-issues}

* Quando installi AEM 6.5 Service Pack 11 e provi a scaricare il file ZIP di stato, Experience Manager scarica un file corrotto. Scarica e installa [Pacchetto indice SEO di AEM Sites](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) sulla tua istanza AEM prima di scaricare il file ZIP per risolvere il problema.

* Come [!DNL Microsoft Windows Server 2019] non supporta [!DNL MySQL 5.7] e [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] non supporta installazioni chiavi in mano per [!DNL AEM Forms 6.5.10.0].

* Se stai aggiornando il tuo [!DNL Experience Manager] istanza dalla versione 6.5 alla versione 6.5.10.0, puoi visualizzare `RRD4JReporter` eccezioni `error.log` file. Per risolvere il problema, riavvia l&#39;istanza.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 10 o un service pack precedente su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminato.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Gli utenti possono rinominare una cartella in una gerarchia [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Durante l’installazione di Experience Manager 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l’integrazione di Adobe Target è configurata in Experience Manager utilizzando l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti di esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

* Quando si tenta di spostare/eliminare/pubblicare frammenti di contenuto o siti/pagine, si verifica un problema quando i riferimenti ai frammenti di contenuto vengono recuperati, in seguito a un errore della query in background; ovvero la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell&#39;indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.12.0:

* [Elenco dei bundle OSGi inclusi nell’Experience Manager 6.5.12.0](assets/65120_bundles.txt)

* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.12.0](assets/65120_packages.txt)

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* Vedi [come contattare l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina di prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

