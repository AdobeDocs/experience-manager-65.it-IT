---
title: Novità in Adobe Experience Manager 6.5 Service Pack 7
description: Novità in Adobe Experience Manager 6.5 Service Pack 7
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: e056d25cf16d79e8eadc80b9cb17b60b2ba8d7e1
workflow-type: tm+mt
source-wordcount: '2704'
ht-degree: 1%

---


# Novità in Adobe Experience Manager 6.5 Service Pack 7 {#aem-whats-new-service-pack}

![Novità](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Service Pack forniscono nuove funzioni, miglioramenti richiesti dai clienti e miglioramenti a prestazioni, stabilità e sicurezza a intervalli trimestrali. La disponibilità trimestrale semplifica l&#39;accesso e l&#39;adozione di nuove caratteristiche e innovazioni.

In questo articolo vengono evidenziate le funzionalità incluse nell&#39;ultimo Service Pack 6.5, le [funzionalità chiave incluse nei Service Pack 6.5](#key-features-previous-service-packs) precedenti, e le [principali AEM rilasciate dall&#39;ultima versione del Service Pack](#key-releases-since-last-sp).

## Adobe [!DNL Experience Manager Sites] {#aem-sites}

### Ordinare le pagine Live Copy disponibili per il rollout {#sort-livecopy-pages}

È ora possibile ordinare le pagine Live Copy disponibili per l&#39;implementazione utilizzando le proprietà [!UICONTROL Name], [!UICONTROL Last modified date] e [!UICONTROL Last rollout date]. La [!UICONTROL Data ultimo rollout] per una pagina è una nuova proprietà introdotta in questa versione.

### Disponibilità di spostamenti di pagina e rollout MSM come operazioni asincrone {#page-moves-msm-asynchronous}

È ora possibile eseguire gli spostamenti di pagina e i rollout MSM come operazioni asincrone per ridurne l&#39;impatto sulle prestazioni del runtime. È possibile pianificare le operazioni per l&#39;esecuzione immediata o successiva. Lo stato dei processi e dei passaggi di processo associati viene visualizzato in una console, utile per monitorare i rollout MSM su larga scala.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* [!DNL Assets] e  [!DNL Dynamic Media] fornire diversi miglioramenti a livello di accessibilità. I miglioramenti riguardano la navigazione tramite tastiera, l&#39;uso di assistenti vocali, miglioramenti simili per consentire l&#39;uso di tecnologie di assistenza (AT). Vedere [[!DNL Assets] miglioramenti](/help/release-notes/sp-release-notes.md#assets-6570) e [[!DNL Dynamic Media] miglioramenti](/help/release-notes/sp-release-notes.md#dynamic-media-6570).

* Gli utenti possono ordinare le risorse digitali nelle viste a schede e a colonne.

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>[!DNL Experience Manager Forms] i pacchetti aggiuntivi sono disponibili una settimana dopo il rilascio pianificato di  [!DNL Experience Manager] Service Pack. [!DNL Experience Manager] 6.5 Service Pack 7 (6.5.7.0) è previsto per il 26 novembre 2020.

## Funzioni principali nei precedenti [!DNL Experience Manager] Service Pack 6.5 {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Disponibilità dell&#39;operazione Page Move in modalità asincrona (6.5.6.0) {#page-move-asynchronous}

L&#39;operazione Page Move (Sposta pagina) è ora disponibile in modalità asincrona. Oltre all&#39;esecuzione immediata, potete anche pianificare l&#39;operazione Page Move per un&#39;esecuzione successiva.

#### Miglioramenti all&#39;accessibilità (6.5.5.0) {#accessibility-sites}

* È stata migliorata la generazione di rapporti sugli errori mediante l’aggiunta di informazioni di testo.

* È stato migliorato lo stato attivo dell&#39;interfaccia utente durante la navigazione tramite tastiera.

* Rapporto di contrasto migliorato per vari elementi dell&#39;interfaccia utente.

* Miglioramento della coerenza degli attributi alt per le immagini della pagina.

* Miglioramento della coerenza delle etichette delle applicazioni Rich Internet (ARIA) accessibili.

* Funzionalità non visive Desktop Access (NVDA) migliorate.

* Supporto migliorato per gli assistenti vocali.

#### Altri miglioramenti chiave (6.5.5.0) {#other-enhancements-sites}

* L&#39;accesso anonimo ai CRXDE Lite non è consentito per migliorare la sicurezza. Al contrario, gli utenti vengono indirizzati alla schermata di accesso. Vedere [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Quando si copia o incolla una struttura ad albero di pagina, è ora possibile incollare la pagina principale o incollare la pagina principale con le relative sottopagine.

* [!DNL Adobe Experience Manager Experience Fragments] esportati in  [!DNL Adobe Target] aree di lavoro ora vengono visualizzati come tipi di offerta univoci e origini di offerta in  [!DNL Target].

* Multi Site Manager - L&#39;attivazione della pubblicazione ora elimina un componente dalla pagina pubblicata se un componente viene eliminato dalla pagina di origine.

* Multi Site Manager - Quando il nome di un componente locale in una [!UICONTROL Live Copy] è identico al nome di un componente nel blueprint e il componente viene implementato dal blueprint, il termine `_msm_moved` viene ora aggiunto al nome del componente locale.

#### Miglioramenti di Style System (6.5.4.0) {#style-system-enhancements}

È ora possibile selezionare gli stili nella finestra di dialogo del componente utilizzando il sistema di stile avanzato.

#### Miglioramenti delle prestazioni in varie aree (6.5.4.0) {#performance-improvements}

* Riduzione del tempo necessario per caricare e inizializzare ContextHub in un sito (`contexthub.kernel.js`). Ne risulta un caricamento più rapido delle pagine durante una visita del sito.

* È stato ridotto il tempo necessario per aggiornare una pagina dopo il trascinamento di [!DNL Experience Fragments] in [!DNL Sites] Editor pagina.

* È stato ridotto il tempo di caricamento delle voci in una pagina [!DNL Sites] con più di 200 copie live in **[!UICONTROL Live Copy Overview]**.

* Gestione migliorata degli URL incompleti o non validi. Tali URL possono rallentare l&#39;Editor modelli.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Miglioramenti dell&#39;accessibilità (6.5.6.0) {#accessibility-assets-6560}

* **Ottimizzazione dell&#39;interfaccia utente durante la navigazione** da tastiera, ad esempio per quanto riguarda:

   * `x` nella finestra di dialogo  [!UICONTROL Anteprima ] versione di una risorsa nella  [!UICONTROL timeline].

   * Opzioni di interfaccia utente fruibili.

   * Campo e-mail nella finestra di dialogo [!UICONTROL Condividi collegamento] e campo per aggiungere un gruppo di utenti chiuso nella scheda [!UICONTROL Autorizzazioni] della cartella [!UICONTROL Proprietà].

* **Funzionalità ottimizzata mediante i tasti della tastiera**

   Gli utenti possono utilizzare i tasti di scelta rapida per trascinare i controlli nell&#39;editor Modulo schema metadati nella modalità Sfoglia dell&#39;assistente vocale.

* **Maggiore usabilità per gli utenti** di utilità di lettura dello schermo, grazie alle seguenti caratteristiche:

   * Gli assistenti vocali annunciano lo scopo dei lettori video e audio.

   * Gli assistenti vocali annunciano lo scopo delle opzioni dell&#39;interfaccia utente per rimuovere i tag selezionati utilizzando la finestra di dialogo di selezione dei tag [!UICONTROL a1/> sulla risorsa [!UICONTROL Proprietà].]

   * Gli assistenti vocali annunciano le intestazioni di riga e gli elementi di riga delle tabelle, in modo che gli utenti sappiano quali voci appartengono alla stessa riga.

   * Titolo della pagina descrittivo e significativo della pagina di ricerca.

   * Gli assistenti vocali annunciano le opzioni nel pannello dei filtri di ricerca come fisarmoniche espandibili.

#### Altri miglioramenti in [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* I gruppi di utenti associati alle cartelle (privati e non privati) ora vengono rimossi dall&#39;archivio in [eliminazione di tali cartelle](/help/assets/private-folder.md#delete-private-folder). Tuttavia, i gruppi di utenti ridondanti, orfani, inutilizzati e generati automaticamente possono essere rimossi dall&#39;archivio tramite JMX.

#### Miglioramenti dell&#39;accessibilità in [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] è ora più accessibile in conformità con le linee guida WCAG (Web Content Accessibility Guidelines). L&#39;accessibilità è migliorata grazie ai seguenti miglioramenti:

* Molti elementi dell&#39;interfaccia utente, controlli, pagine e finestre di dialogo sono intuitivi per gli assistenti vocali.

* Molti elementi, controlli e campi modulo di input dell&#39;interfaccia utente sono accessibili tramite tastiera.

* Il colore e il contrasto di alcuni elementi dell’interfaccia utente sono stati aggiornati in modo che gli utenti con vista limitata o senza percezione del colore possano distinguere tali elementi. Ad esempio, il colore delle icone di valutazione a stella (come nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] nella risorsa [!UICONTROL Proprietà] o nella vista a schede) viene modificato per il contrasto appropriato.

   ![Icone di valutazione con contrasto migliorato](assets/star-rating-icons.png)

#### Gestione delle eccezioni migliorata (6.5.5.0) {#exception-handling}

[!DNL Assets] il flusso dell&#39;interfaccia utente offre una migliore gestione delle eccezioni. Se una risorsa non ha un tipo per la sua dimensione, l&#39;eccezione osservata viene registrata nei file di registro.

#### Supporto delle risorse 3D in [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

Il supporto per le immagini 3D in [!DNL Dynamic Media] consente ai clienti di pubblicare e aggiungere contenuti 3D a pagine Web e applicazioni. Il supporto include:

* Pubblicate i formati di risorse 3D più comuni e generate un URL di risorse che può essere utilizzato nelle pagine Web e in altre applicazioni.

* Visualizzatore Web 3D, basato su [!DNL Adobe Dimension], per visualizzare in modo interattivo le risorse 3D pubblicate.

* Pubblicate e visualizzate le risorse 3D comuni su [!DNL Experience Manager Sites] pagine utilizzando il componente [!DNL Sites] WCM.

#### Configurare [!DNL Experience Manager Assets] con [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Viene modificato il canale di autorizzazione tra [!DNL Experience Manager Assets] e [!DNL Brand Portal]. In precedenza, [!DNL Brand Portal] era stato configurato nell&#39;interfaccia classica tramite il gateway OAuth legacy, che utilizza lo scambio di token JWT per ottenere un token di accesso IMS per l&#39;autorizzazione. [!DNL Experience Manager Assets] è ora configurato con  [!DNL Brand Portal] tramite  Adobe I/O, che fornisce un token IMS per l&#39;autorizzazione del  [!DNL Brand Portal] tenant.

I passaggi per configurare [!DNL Experience Manager Assets] con [!DNL Brand Portal] sono diversi a seconda della versione [!DNL Experience Manager] in uso e se si sta configurando per la prima volta, oppure aggiornando le configurazioni esistenti. Per informazioni, consultate [Configurare  risorse Experience Manager con il portale dei marchi](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html).

#### Miglioramenti dell&#39;accessibilità (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] include i seguenti miglioramenti dell&#39;accessibilità:

* I tasti freccia sulla tastiera possono essere utilizzati per spostare e scorrere le aree all&#39;interno delle immagini ingrandite. Per ulteriori informazioni, vedere [visualizzare in anteprima le risorse utilizzando solo i tasti di scelta rapida](../assets/manage-assets.md#previewing-assets).

* Le caselle di controllo dello stato misto (in cui, a meno che non si selezionino tutti i predicati nidificati, le caselle di controllo di primo livello non vengono selezionate e vengono evidenziate) nel pannello Filtri sono leggibili dagli assistenti vocali.

* Le limitazioni relative al formato di data e ora sono fornite nelle etichette dei campi data, per consentire agli utenti di immettere la data nel formato corretto utilizzando la tastiera.
Esempio, `On Time (MM-DD-YYYY HH:mm)`. Qui MM è mese in formato a due cifre, AAAA è anno, GG è giorno in formato a due cifre, HH è ora in formato militare a 24 ore e mm è minuto.

* Gli assistenti vocali annunciano la possibilità di rimuovere i tag selezionati (`X` simbolo) e il numero dei tag selezionati.

#### Colonna ordinabile per la data di creazione delle risorse nella vista a elenco (6.5.3.0) {#sortable-date-created-column}

Nella visualizzazione a elenco di DAM e nei risultati della ricerca di risorse nella visualizzazione a elenco viene aggiunta una nuova colonna ordinabile per la data di creazione delle risorse.

![Colonna ordinabile per la data di creazione](assets/asset-created-date.png)

#### Ricerca visiva per [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets]Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di  Experience Manager visualizza le immagini con tag avanzati dall&#39;archivio DAM, simili a quelle selezionate dall&#39;utente. Vedere [Ricerca visiva](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Annullamento della validità del contenuto cache CDN (6.5.6.0) {#invalidate-cdn-cached-content}

Ora potete utilizzare l&#39;interfaccia utente [!DNL Dynamic Media] per annullare la validità del contenuto nella cache della rete di distribuzione dei contenuti (CDN). Di conseguenza, le risorse aggiornate sono disponibili all’istante invece di attendere la scadenza della cache. Potete annullare la validità della CDN:

* Creazione di un modello di annullamento validità CDN: Selezione delle risorse e degli URL basati su modelli associati

* Selezione delle risorse e dei predefiniti associati tramite il selettore delle risorse

* Aggiunta di URL di risorse completi

#### Pubblicazione selettiva delle risorse su [!DNL Experience Manager] e [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Ora potete scegliere di pubblicare o annullare la pubblicazione selettiva delle risorse in [!DNL Experience Manager] o [!DNL Dynamic Media] utilizzando la procedura guidata [!UICONTROL Pubblicazione rapida] o [!UICONTROL Gestisci pubblicazione]. È inoltre possibile impostare la modalità `Publish` o `Unpublish` a livello di cartella.

#### Immagini intelligenti per contenuti multimediali dinamici {#smart-imaging}

Le immagini intelligenti utilizzano le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento. La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser. Vedere [Immagini intelligenti](../assets/imaging-faq.md).

#### Ritaglio avanzato nei profili video per contenuti multimediali dinamici (6.5.3.0) {#smart-crop-video}

La funzione di ritaglio avanzato per i video - una funzione opzionale disponibile nei profili video - è uno strumento che utilizza l&#39;intelligenza artificiale di  Adobe Sensei per rilevare e ritagliare automaticamente il punto focale in qualsiasi video adattivo o progressivo caricato, indipendentemente dalle dimensioni. Consultate [L&#39;utilizzo del ritaglio avanzato nei profili video](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Precompilare un modulo adattivo sul client (6.5.6.0) {#prefill-merge-data-at-client}

Quando si precompila un modulo adattivo, il server [!DNL Experience Manager Forms] unisce i dati a un modulo adattivo e invia il modulo compilato. Per impostazione predefinita, l&#39;azione di unione dei dati viene eseguita sul server.
Ora è possibile configurare il server [!DNL Experience Manager Forms] in modo che [esegua l&#39;azione di unione dati sul client](../../help/forms/using/prepopulate-adaptive-form-fields.md) anziché sul server. Riduce notevolmente il tempo necessario per precompilare ed eseguire il rendering dei moduli adattivi.

#### Integrazione del modello di dati del modulo con le API RESTful su un server con implementazione SSL bidirezionale (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] il modello di dati modulo ora può  [integrarsi con le API RESTful su un server in cui è implementato](../../help/forms/using/configure-data-sources.md) un SSL bidirezionale.

#### È stato aggiunto il supporto per [!DNL Adobe Sign] Tag di testo nel servizio Automated forms conversion (6.5.6.0) {#sign-integration-acroform-afcs}

Se un AcroForm include tag di testo [!DNL Adobe Sign], questi campi vengono ora riconosciuti e rappresentati come campi [!DNL Adobe Sign] nel modulo adattivo convertito utilizzando [!DNL Automated Forms Conversion service]. Un firmatario può compilare tali campi durante la firma del modulo adattivo.

#### Supporto per la conversione di PDF forms colorati in moduli adattivi (6.5.6.0) {#colored-PDF-forms}

È possibile utilizzare [!DNL Automated Forms Conversion service] per convertire PDF forms colorati in moduli adattivi.

#### Supporto dei protocolli SMB 2 e SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] ora supporta i protocolli SMB 2 e SMB 3.

#### Caching migliorato per le pagine dei moduli adattivi tradotti (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Ora è possibile specificare le [impostazioni internazionali come selettore nell&#39;URL del modulo adattivo invece di un argomento nell&#39;URL del modulo adattivo](../../help/forms/using/supporting-new-language-localization.md). Consente di memorizzare i moduli adattivi tradotti nella cache su [!DNL Experience Manager Dispatcher]. La memorizzazione nella cache del modulo adattivo convertito non era possibile nelle versioni precedenti. Per informazioni dettagliate sulla configurazione del caching per l&#39;utilizzo delle impostazioni internazionali come selettore nell&#39;URL del modulo adattivo, vedere [Configurare la cache del modulo adattivo nel dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Salva l&#39;output del servizio del modello dati modulo su una variabile (6.5.6.0) {#save-fdm-service-to-variable}

Il modello dati modulo consente di salvare l&#39;output di un servizio del modello dati modulo su una variabile. [!DNL Experience Manager Forms] ora esegue automaticamente il mapping del tipo di servizio del modello dati del modulo con il tipo di variabile.

#### Allega più file per il componente Allegato file (6.5.6.0) {#attach-multiple-files}

È ora possibile allegare più file](../../help/forms/using/introduction-forms-authoring.md) al componente [!UICONTROL File Attachment] dei moduli adattivi.[

#### Personalizzare le colonne Adobe Experience Manager Inbox (6.5.5.0) {#customize-aem-inbox-columns}

È possibile personalizzare una [!DNL Experience Manager] Casella in entrata per modificare il titolo predefinito di una colonna, riordinare la posizione di una colonna e visualizzare colonne aggiuntive in base ai dati di un flusso di lavoro. I membri del gruppo `administrators` o `workflow-administrators` possono personalizzare le colonne. Per ulteriori informazioni, vedere [Controllo amministratore](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizzare  colonne Casella in entrata Experience Manager](assets/customize-columns.gif)

#### Salva le comunicazioni interattive come bozza (6.5.5.0) {#save-as-draft}

È possibile utilizzare l&#39;interfaccia utente agente per salvare una o più bozze per ogni comunicazione interattiva e recuperare la bozza in un secondo momento per continuare a lavorarci. È possibile specificare un nome diverso per ciascuna bozza per identificarla. Per ulteriori informazioni, vedere [Salva le comunicazioni interattive come bozza](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Salva come bozza](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] supporto del server applicazioni (6.5.5.0)  {#weblogic-support}

 Adobe Experience Manager Forms ha aggiunto il supporto per [!DNL Oracle WebLogic 12]  Adobe Experience Manager Forms su JEE. È possibile effettuare l&#39;aggiornamento da una versione precedente o impostare un nuovo Forms  Experience Manager 6.5 sul server JEE su [!DNL Oracle WebLogic] 12.2.1.4 e versioni successive. Successivamente corrisponde alle modifiche minori, dove x in 12.2.1.x viene sostituito con un numero di versione.

#### Miglioramenti all&#39;accessibilità (6.5.5.0) {#accessibility-improvements}

 Adobe Experience Manager Forms include i seguenti miglioramenti a livello di accessibilità:

* Quando un utente visualizza l&#39;anteprima di un modulo adattivo come modulo HTML, il campo [!UICONTROL Firma scarabocchio] mantiene lo stato attivo.

* I messaggi di errore visualizzati durante l&#39;invio di un modulo adattivo ora contengono l&#39;attributo `aria-describedBy`. L&#39;attributo è associato ai campi indicati nel messaggio di errore. L&#39;attributo `aria-describedby` indica gli ID degli elementi che descrivono l&#39;oggetto. Consente di stabilire una relazione tra widget o gruppi e testo che li descrive.

* Se in un modulo adattivo sono presenti alcuni campi obbligatori, l&#39;attributo obbligatorio è impostato su `True` per tali campi nello schema di accessibilità ARIA.

#### Autenticazione basata su certificato X-509 per i servizi Web basati su SOAP nel modello dati del modulo (6.5.5.0) {#x509-based-authentication-soap}

Il modello di dati del modulo ora supporta l&#39;autenticazione basata sui certificati X-509 quando si utilizzano i servizi Web SOAP come origine dati. Per ulteriori informazioni, vedere [Configurare i servizi Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Altri miglioramenti chiave (6.5.5.0) {#other-improvements}

*  Experience Manager 6.5 Forms su JEE Document Security è ora basato su [!DNL Apache Struts 2].

* È stato aggiunto il supporto per [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Genera output stampabile nei flussi di lavoro Forms  Experience Manager (6.5.4.0) {#generate-printable-output}

Il passaggio del flusso di lavoro Genera output stampabile consente di integrare un file modello sorgente con un file di dati. Questa integrazione consente di stampare o salvare copie diverse del file modello. Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL. Per ulteriori informazioni su questa funzione, vedere [Flusso di lavoro Forms-centric su OSGi - Step Reference](../forms/using/aem-forms-workflow-step-reference.md).

![Genera output stampabile](assets/generate-print-output-step.gif)

#### Supporto a più colonne per moduli adattivi e comunicazioni interattive in modalità Layout (6.5.4.0) {#multi-column-adaptive-forms}

È ora possibile definire il numero di colonne per un pannello nei moduli adattivi e nelle comunicazioni interattive. Passate alla modalità di layout per utilizzare la nuova opzione a più colonne. Per ulteriori informazioni, vedere [Utilizzare la modalità Layout per ridimensionare i componenti](../forms/using/resize-using-layout-mode.md).

![Layout a più colonne](assets/multi-column-layout.gif)

#### Personalizzazioni della Casella in entrata  Experience Manager (6.5.4.0) {#aem-inbox}

La nuova opzione Controllo amministratore consente agli amministratori di:

* Personalizzare il testo dell’intestazione e il logo.

* Controllare la visualizzazione dei collegamenti di navigazione disponibili nell&#39;intestazione.

L&#39;opzione Controllo amministratore è visibile solo ai membri del gruppo `administrators` o `workflow-administrators`. Per ulteriori informazioni su questa funzione, vedere [Casella in entrata](../sites-authoring/inbox.md).

#### Supporto di testo RTF nei moduli HTML5 (6.5.4.0) {#rich-text-support}

Convertire un campo di testo in un modulo XFA in un campo di testo RTF in un modulo HTML5. Per ulteriori informazioni, vedere [Progettazione di modelli di modulo per moduli HTML5](../forms/using/designing-form-template.md).

#### Miglioramenti dell&#39;accessibilità (6.5.4.0) {#forms-accessibility-enhancements-6540}

 Experience Manager Forms include i seguenti miglioramenti a livello di accessibilità:

* Gli assistenti vocali annunciano le caselle di controllo, i collegamenti, il selettore data e i campi di immissione data correttamente in un modulo adattivo.

* Ogni pagina di un modulo adattivo ora include un titolo e un’etichetta con il punto di riferimento principale.

#### Condivisione e richiesta dell&#39;accesso agli elementi Inbox di un utente Forms di un Experience Manager  (6.5.3.0) {#share-request-access}

È possibile condividere gli elementi Inbox con un altro utente. Quando un altro utente accede agli elementi della Casella in entrata, può richiedere e intervenire sugli elementi condivisi. Allo stesso modo, potete richiedere l’accesso agli elementi della casella in entrata ad altri utenti. Vedere [Condividere e richiedere l&#39;accesso agli elementi in entrata di un utente](../forms/using/configure-shared-queues-osgi.md).

#### Configurare le impostazioni predefinite per gli elementi Inbox di un utente Forms di Experience Manager  (6.5.3.0) {#configure-out-of-office}

Se prevedete di uscire dall&#39;ufficio, potete specificare cosa accade agli elementi assegnati a quel periodo.
È possibile specificare una data e un&#39;ora di inizio e una data e un&#39;ora di fine affinché le impostazioni fuori sede siano attive. Potete impostare una persona predefinita a cui vengono inviati tutti gli elementi. Vedere [Configurare le impostazioni fuori sede](../forms/using/configure-out-of-office-settings.md).

#### Generare più comunicazioni interattive utilizzando l&#39;API Batch per  Forms Experience Manager (6.5.3.0) {#generate-multiple-ic}

Potete utilizzare l&#39;API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L&#39;API Batch combina i dati con un modello per produrre una comunicazione interattiva. L&#39;API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto della carta di credito per più clienti. Consultate [Generare più comunicazioni interattive utilizzando l&#39;API Batch](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

## Versioni principali da Adobe Experience Manager 6.5 SP6 {#key-releases-since-last-sp}

Tra il 30 settembre 2020 e il 26 novembre 2020,  Adobe ha rilasciato quanto segue, oltre ai Service Pack e ai fix pack cumulativi:

* [!DNL Adobe Experience Manager] come Cloud Service  [2020.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-9-0.html?lang=en#release-notes) e  [2020.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-10-0.html?lang=en#release-notes).

* [[!DNL Experience Manager] app desktop 2.0 (2.0.3.2)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Sito di riferimento WKND - 0.0.6](https://github.com/adobe/aem-guides-wknd/releases/tag/aem-guides-wknd-0.0.6)

* [Experienci Manager Screens: Feature Pack 202008](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202008.html)

* [ collegamento risorsa Adobe v2.2](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5 documentazione](../user-guide/home.md)
>* [Note generali sulla versione per [!DNL Adobe Experience Manager]  6.5](release-notes.md)
>* [Note sulla versione del Service Pack per [!DNL Adobe Experience Manager]  6.5](sp-release-notes.md)

