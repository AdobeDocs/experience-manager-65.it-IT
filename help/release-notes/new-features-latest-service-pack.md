---
title: Novità in [!DNL Experience Manager] 6.5 Service Pack 10
description: Novità in [!DNL Experience Manager] 6.5 Service Pack 10
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 496516f7f4b0e59bbfdae4cbe061a793f28449d2
workflow-type: tm+mt
source-wordcount: '4106'
ht-degree: 1%

---

# Novità in [!DNL Adobe Experience Manager] 6.5 Service Pack 10 {#aem-whats-new-service-pack}

<!-- TBD: Downsample this image. We do not need as big an image since customers don't use as big a screen to view. Also, having a 700+ KB decorative image is bad for page load time.
-->

![Novità](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 I Service Pack forniscono nuove funzionalità, miglioramenti richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza a intervalli trimestrali. La disponibilità trimestrale semplifica l&#39;accesso e l&#39;adozione di nuove caratteristiche e innovazioni.

Questo articolo evidenzia le funzioni incluse nell&#39;ultimo Service Pack, [funzionalità chiave incluse nei Service Pack 6.5](#key-features-previous-service-packs) precedenti e nelle [versioni chiave dall&#39;ultima versione di Service Pack](#key-releases-since-last-sp).

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

* **Editor e  [!DNL Content Fragment] modelli migliorati**: È ora possibile creare modelli complessi e personalizzati per contenuti strutturati utilizzando  [!DNL Content Fragment] modelli nidificati. Le strutture di contenuto sono modularizzate in elementi di base modellati come sottoframmenti. I frammenti di livello superiore fanno riferimento a tali sottoframmenti. Ulteriori miglioramenti del tipo di dati, come le regole di convalida avanzate, migliorano ulteriormente la flessibilità nella modellazione dei contenuti con [!DNL Content Fragments]. L’editor [!DNL Experience Manager] [!DNL Content Fragment] supporta le strutture di frammenti nidificati in una sessione dell’editor comune, con miglioramenti quali la visualizzazione struttura ad albero e la navigazione a schede tramite gerarchie di frammenti.

* **API GraphQL per[!DNL Content Fragments]**: La nuova API GraphQL è il metodo standard per distribuire contenuti strutturati in formato JSON. Le query GraphQL consentono ai client di richiedere solo gli elementi di contenuto rilevanti per il rendering di un’esperienza. Tale selezione elimina la consegna dei contenuti in eccesso (possibilità con le API REST HTTP) che richiede l’analisi dei contenuti sul lato client. Gli schemi GraphQL sono derivati da modelli [!DNL Content Fragment] e le risposte API sono effettuate in formato JSON. In [!DNL Experience Manager] come [!DNL Cloud Service], [Le query GraphQL persistono](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) ed elaborano richieste di GET compatibili con la cache. Non è ancora possibile in [!DNL Experience Manager] 6.5.

* **Gestione della gerarchia e anteprima** futura: Gli utenti dispongono ora di un’interfaccia per accedere alle strutture di contenuto dei loro  [!DNL Experience Manager] lanci, inclusa la possibilità di aggiungere e rimuovere pagine in un lancio. Questa funzione migliora la flessibilità dei [!DNL Experience Manager] lanci per creare versioni di contenuti destinate a future pubblicazioni. [Le funzioni ](/help/sites-authoring/working-with-page-versions.md#timewarp) di deformazione in tempo libero consentono agli utenti di visualizzare in anteprima gli avvii come stati di contenuto futuri.

* [!DNL Experience Manager] visualizza direttamente un elenco di tutti i modelli di contenuto presenti in una cartella senza che gli autori di contenuti debbano spostarsi all’interno della struttura del file. La funzionalità ora richiede meno clic e migliora l’efficienza di authoring.

* Il campo percorso nell’ editor [!DNL Sites] consente agli autori di trascinare risorse da [!DNL Content Finder].

* Platform fornisce alcuni miglioramenti all’accessibilità. Consulta [Aggiornamenti della piattaforma](/help/release-notes/sp-release-notes.md#platform-65100).

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* [!DNL Experience Manager] estende la funzionalità Risorse collegate all’utilizzo di  [!DNL Dynamic Media] immagini nei componenti core applicabili. Consulta [Utilizzare le risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* Quando condividi singole risorse e raccolte come collegamento (utilizzando la finestra di dialogo [!UICONTROL Condivisione collegamenti] ), gli utenti possono scegliere se consentire al destinatario di scaricare le risorse originali, le relative rappresentazioni o entrambi. Consulta [Condividere le risorse tramite link](/help/assets/link-sharing.md).

   ![per consentire il download solo delle risorse originali, solo delle rappresentazioni o di entrambe](/help/release-notes/assets/share-assets-as-link.png)

* Quando gli utenti scaricano le risorse condivise con loro come collegamento, possono scegliere di scaricare le risorse originali, le rappresentazioni o entrambi.

* **Limita le risorse secondarie generate**: Gli amministratori possono limitare il numero di risorse secondarie  [!DNL Experience Manager] generate per risorse composte come file PDF, PowerPoint, InDesign e Keynote.

   ![limitare la generazione di risorse secondarie](/help/assets/assets/sub-asset-limit.png)

* È disponibile un nuovo pacchetto [!DNL Camera Raw] che supporta [!DNL Adobe Camera Raw] v10.4. Consulta [elaborare le immagini utilizzando [!DNL Camera Raw]](/help/assets/camera-raw.md).

### [!DNL Dynamic Media] {#assets-dynamic-media}

* Molti miglioramenti dell’accessibilità vengono eseguiti nel client [!DNL Dynamic Media] in modo che un assistente vocale possa presentare una descrizione più appropriata e utile dell’azione o dell’interfaccia utente. Vedere [[!DNL Dynamic Media] aggiornamenti](/help/release-notes/sp-release-notes.md#dynamic-media-65100).

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>Il pacchetto aggiuntivo di [!DNL Experience Manager Forms] viene reso disponibile una settimana dopo il rilascio pianificato di [!DNL Experience Manager] Service Pack .

* È ora possibile utilizzare il servizio Automated forms conversion per [convertire i PDF forms in francese, tedesco e spagnolo](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#language-specific-meta-model) nei moduli adattivi.

* **Messaggi di errore nel browser** Proprietà: Sono stati aggiunti messaggi di errore per ciascuna proprietà nel browser Proprietà adattive Forms. Questi messaggi consentono di comprendere i valori consentiti per un campo.

* **Supporto per utilizzare l&#39;opzione letterale per impostare il valore per una variabile** di tipo JSON: Puoi utilizzare l’opzione letterale per impostare il valore per una variabile di tipo JSON nel passaggio della variabile set di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

* [Aggiornamenti](../forms/using/aem-forms-jee-supported-platforms.md) della piattaforma:  [!DNL Adobe Experience Manager Forms] in JEE è stato aggiunto il supporto per le seguenti piattaforme:
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

* È stato aggiunto il supporto per l’ API `GuideBridge#getGuidePath` in [!DNL AEM Forms].

## Funzioni principali nei Service Pack [!DNL Experience Manager] 6.5 precedenti {#key-features-previous-service-packs}

### Possibilità di ripristinare le pagine e la struttura eliminate (6.5.9.0) {#ability-to-restore-pages-tree}

È ora possibile ripristinare le pagine eliminate e l’intera visualizzazione struttura in una pagina [!DNL Experience Manager Sites].

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Ordinare le pagine Live Copy disponibili per il rollout (6.5.8.0) {#sort-livecopy-pages}

Ora puoi ordinare le pagine Live Copy disponibili per il rollout utilizzando le proprietà [!UICONTROL Name], [!UICONTROL Last modified date] e [!UICONTROL Last rollout date] . La [!UICONTROL Data ultimo rollout] per una pagina è una nuova proprietà introdotta in questa versione.

#### Disponibilità di spostamenti di pagina e rollout MSM come operazioni asincrone (6.5.7.0) {#page-moves-msm-asynchronous}

È ora possibile eseguire gli spostamenti delle pagine e i rollout MSM come operazioni asincrone per ridurne l’impatto sulle prestazioni di runtime. Puoi pianificare le operazioni per l’esecuzione immediata o successiva. Lo stato dei processi e dei passaggi del processo associati viene visualizzato in una console, utile per monitorare i rollout MSM su larga scala.

#### Disponibilità dell’operazione Sposta pagina in modalità asincrona (6.5.6.0) {#page-move-asynchronous}

L’operazione Sposta pagina è ora disponibile in modalità asincrona. Oltre all’esecuzione immediata, puoi anche pianificare l’operazione Sposta pagina per un’esecuzione successiva.

#### Miglioramenti all’accessibilità (6.5.5.0) {#accessibility-sites}

* È stata migliorata la generazione di rapporti sugli errori grazie all’aggiunta di informazioni sul testo.

* È stata migliorata la messa a fuoco dell&#39;interfaccia utente durante la navigazione da tastiera.

* Rapporto di contrasto migliorato per vari elementi dell&#39;interfaccia utente.

* Migliorata la coerenza degli attributi alt per le immagini della pagina.

* Migliorata la coerenza delle etichette delle applicazioni Rich Internet (ARIA) accessibili.

* Funzionalità di accesso desktop non visivo (NVDA) migliorate.

* Supporto migliorato per gli assistenti vocali.

#### Altri miglioramenti chiave (6.5.5.0) {#other-enhancements-sites}

* L’accesso anonimo ad CRXDE Lite non è consentito per migliorare la sicurezza. Gli utenti vengono invece indirizzati alla schermata di accesso. Vedere [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Quando si copia o incolla una struttura di pagina, è ora possibile incollare la pagina principale o incollare la pagina principale con le pagine secondarie della struttura.

* [!DNL Adobe Experience Manager Experience Fragments] esportati nelle  [!DNL Adobe Target] aree di lavoro ora vengono visualizzati come tipi di offerta univoci e origini offerte in  [!DNL Target].

* Multi Site Manager : l’attivazione di pubblicazione ora elimina un componente dalla pagina pubblicata se un componente viene eliminato dalla pagina sorgente.

* Multi Site Manager : quando il nome di un componente locale in una [!UICONTROL Live Copy] è identico al nome di un componente nella blueprint e il componente viene rilasciato dalla blueprint, il termine `_msm_moved` viene ora aggiunto al nome del componente locale.

#### Miglioramenti al sistema di stili (6.5.4.0) {#style-system-enhancements}

È ora possibile selezionare gli stili all’interno della finestra di dialogo del componente utilizzando il sistema di stili avanzato.

#### Miglioramenti delle prestazioni in vari settori (6.5.4.0) {#performance-improvements}

* Riduzione del tempo necessario per caricare e inizializzare ContextHub all&#39;interno di un sito (`contexthub.kernel.js`). Ne risulta un caricamento più rapido delle pagine durante una visita al sito.

* È stato ridotto il tempo necessario per aggiornare una pagina dopo aver trascinato [!DNL Experience Fragments] in [!DNL Sites] Editor pagina.

* È stato ridotto il tempo di caricamento delle voci in una pagina [!DNL Sites] con più di 200 Live Copy in **[!UICONTROL Panoramica Live Copy]**.

* È stata migliorata la gestione degli URL incompleti o non validi. Tali URL possono rallentare l’Editor modelli.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}


* È stata aggiornata la denominazione delle impostazioni locali e delle regioni cinesi relative a Hong Kong, Macao e Taiwan, per renderle coerenti con le opinioni sociali e politiche cinesi (6.5.9.0).

* È stata introdotta una configurazione opzionale per modificare l’utilizzo degli ID e-mail nella risposta API ACP da [!DNL Adobe Experience Manager] (6.5.9.0).

   ![configurazione per modificare gli ID e-mail in lettere minuscole nella risposta ACP da  [!DNL Experience Manager]](assets/email-lowcase-config.png)

* Il contrasto di testo e icone sullo sfondo è migliorato per varie funzioni. Questa implementazione delle linee guida WCAG (Web Content Accessibility Guidelines) rende [!DNL Assets] più accessibile agli utenti con una visione e una percezione del colore limitate. Vedi [miglioramenti all&#39;accessibilità in [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590) (6.5.9.0).
* Quando utilizzi la funzionalità [Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md), ora puoi visualizzare un elenco di tutte le [!DNL Sites] pagine che utilizzano la risorsa. Questi riferimenti a una risorsa sono disponibili nella pagina [!UICONTROL Proprietà] di una risorsa. Questo consente agli amministratori, agli esperti di marketing e ai bibliotecari di visualizzare in modo completo l’utilizzo delle risorse, consentendo un migliore monitoraggio, gestione e coerenza del marchio (6.5.8.0).

* Quando si elimina una risorsa a cui si fa riferimento in una pagina web, in [!DNL Experience Manager] viene visualizzato un avviso. Puoi forzare l’eliminazione di una risorsa di riferimento oppure controllare e modificare i riferimenti visualizzati nella pagina [!DNL Properties] della risorsa. Facendo clic sui riferimenti vengono aperte le pagine locali e remote [!DNL Sites] (6.5.8.0).

* [!DNL Assets] e  [!DNL Dynamic Media] forniscono diversi miglioramenti dell’accessibilità. I miglioramenti riguardano la navigazione da tastiera, l’uso di assistenti vocali e miglioramenti simili per consentire l’utilizzo di tecnologie per l’accessibilità (AT). Consulta [[!DNL Assets] miglioramenti](/help/release-notes/sp-release-notes.md#assets-6570) e [[!DNL Dynamic Media] miglioramenti](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Gli utenti possono ordinare le risorse digitali nelle viste a schede e a colonne (6.5.7.0).

#### Miglioramenti all’accessibilità (6.5.6.0) {#accessibility-assets-6560}

* **Messa a fuoco migliorata dell&#39;interfaccia utente durante la navigazione** da tastiera, ad esempio per quanto riguarda:

   * `x` nella finestra di dialogo  [!UICONTROL Anteprima ] versione di una risorsa nella  [!UICONTROL Timeline].

   * Opzioni fruibili dell’interfaccia utente.

   * Campo e-mail nella finestra di dialogo [!UICONTROL Condividi collegamento] e campo per aggiungere un gruppo utenti chiuso nella scheda [!UICONTROL Autorizzazione] della cartella [!UICONTROL Proprietà].

* **Funzionalità ottimizzata tramite tasti di tastiera**

   Gli utenti possono utilizzare i tasti di tastiera per trascinare i controlli nell’editor Modulo schema metadati nella modalità Sfoglia dell’assistente vocale.

* **È stata migliorata la fruibilità per gli utenti** di assistenti vocali, a causa dei seguenti elementi:

   * Gli assistenti vocali annunciano lo scopo dei lettori video e audio.

   * Gli assistenti vocali annunciano lo scopo delle opzioni dell’interfaccia utente per rimuovere i tag selezionati utilizzando la finestra di dialogo [!UICONTROL Selezione tag] sulla risorsa [!UICONTROL Proprietà].

   * Gli assistenti vocali annunciano le intestazioni di riga e gli elementi di riga delle tabelle, in modo che gli utenti sappiano quali voci appartengono alla stessa riga.

   * Titolo descrittivo e significativo della pagina di ricerca.

   * Gli assistenti vocali annunciano le opzioni nel pannello dei filtri di ricerca come pannello a soffietto espandibile.

#### Altri miglioramenti in [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* I gruppi di utenti associati alle cartelle (private e non private) vengono ora rimossi dall&#39;archivio in [eliminazione di tali cartelle](/help/assets/private-folder.md#delete-private-folder). Tuttavia, i gruppi di utenti ridondanti, orfani, inutilizzati e generati automaticamente possono essere rimossi dall’archivio utilizzando JMX.

#### Miglioramenti all’accessibilità in [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] è ora più accessibile in conformità alle linee guida per l’accessibilità dei contenuti web (WCAG). L’accessibilità è stata migliorata a causa dei seguenti miglioramenti:

* Molti elementi, controlli, pagine e finestre di dialogo dell’interfaccia sono compatibili con gli assistenti vocali.

* Molti elementi, controlli e campi modulo di input dell’interfaccia utente sono accessibili da tastiera.

* Il colore e il contrasto di alcuni elementi dell’interfaccia utente sono stati aggiornati in modo che gli utenti con vista limitata o senza percezione del colore possano distinguere tali elementi. Ad esempio, il colore delle icone delle stelle di valutazione (come nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] nella scheda della risorsa [!UICONTROL Proprietà] o nella vista a schede) viene modificato per ottenere un contrasto adeguato.

   ![Icone di valutazione con contrasto migliorato](assets/star-rating-icons.png)

#### Gestione migliorata delle eccezioni (6.5.5.0) {#exception-handling}

[!DNL Assets] il flusso dell&#39;interfaccia utente offre una migliore gestione delle eccezioni. Se una risorsa non ha un tipo per la sua dimensione, l’eccezione osservata viene registrata nei file di registro.

#### Supporto per risorse 3D in [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

Il supporto per le immagini 3D in [!DNL Dynamic Media] consente ai clienti di pubblicare e aggiungere contenuti 3D alle pagine web e alle applicazioni. Il supporto include:

* Pubblica i formati comuni di risorse 3D e genera un URL di risorse che può essere utilizzato nelle pagine web e in altre applicazioni.

* Un visualizzatore Web 3D, basato su [!DNL Adobe Dimension], per visualizzare in modo interattivo le risorse 3D pubblicate.

* Pubblica e visualizza risorse 3D comuni sulle [!DNL Experience Manager Sites] pagine utilizzando il componente [!DNL Sites] WCM .

#### Configurare [!DNL Experience Manager Assets] con [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Il canale di autorizzazione tra [!DNL Experience Manager Assets] e [!DNL Brand Portal] viene modificato. In precedenza, [!DNL Brand Portal] era configurato nell’interfaccia classica tramite la versione precedente del gateway OAuth, che utilizza lo scambio di token JWT per ottenere un token di accesso IMS per l’autorizzazione. [!DNL Experience Manager Assets] è ora configurato con  [!DNL Brand Portal] tramite  [!DNL Adobe I/O], che fornisce un token IMS per l’autorizzazione del  [!DNL Brand Portal] tenant.

I passaggi per configurare [!DNL Experience Manager Assets] con [!DNL Brand Portal] sono diversi a seconda della versione [!DNL Experience Manager] e se si sta configurando per la prima volta o se si stanno aggiornando le configurazioni esistenti. Per ulteriori informazioni, consulta [Configurare risorse di Experience Manager con Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) .

#### Miglioramenti all’accessibilità (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] include i seguenti miglioramenti all’accessibilità:

* I tasti freccia sulla tastiera possono essere utilizzati per spostare e scorrere le aree all&#39;interno delle immagini ingrandite. Per ulteriori informazioni, consulta [visualizzare in anteprima le risorse utilizzando solo i tasti di scelta rapida](../assets/manage-assets.md#previewing-assets).

* Le caselle di controllo a stato misto (in cui, a meno che non si selezionino tutti i predicati nidificati, le caselle di controllo di primo livello non sono selezionate e sono evidenziate) nel pannello Filtri sono leggibili dagli assistenti vocali.

* Nelle etichette dei campi data vengono forniti vincoli di formato data e ora per consentire agli utenti di immettere la data nel formato corretto utilizzando la tastiera.
Esempio, `On Time (MM-DD-YYYY HH:mm)`. Qui MM è mese in formato a due cifre, AAAA è anno, GG è giorno in formato a due cifre, HH è ora in formato militare a 24 ore e mm è minuto.

* Gli assistenti vocali annunciano l’opzione per rimuovere i tag selezionati (`X` simbolo) e il numero di tag selezionati.

#### Colonna ordinabile per la data di creazione delle risorse nella vista a elenco (6.5.3.0) {#sortable-date-created-column}

Nella vista a elenco DAM e nei risultati della ricerca delle risorse nella vista a elenco viene aggiunta una nuova colonna ordinabile per la data di creazione delle risorse.

![Colonna ordinabile per la data creata](assets/asset-created-date.png)

#### Ricerca visiva per [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets]Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di In Experience Manager vengono visualizzate le immagini con tag avanzati dell’archivio DAM simili a quelle selezionate dall’utente. Vedere [Ricerca visiva](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

* [[!DNL Dynamic Media] è più ](sp-release-notes.md#assets-accessibility-6590) accessibile in termini di:

   * Facilità di utilizzo con i tasti della tastiera.
   * Contrasto (con sfondo) di testo, testo segnaposto e controlli in vari editor.
   * Accessibilità e narrazione da parte degli assistenti vocali.

* Offri immagini di alta qualità in modo efficiente su dispositivi con display ad alta risoluzione e larghezza di banda limitata, con Smart Imaging DPR (Device Pixel Ratio) e ottimizzazione della larghezza di banda della rete. Consulta [Domande frequenti sull&#39;imaging intelligente](/help/assets/imaging-faq.md) (6.5.9.0).

* [!DNL Dynamic Media] delivery (modificatore `fmt` URL) ora supporta il formato immagine AVIF (formato immagine AV1) di nuova generazione. Per ulteriori dettagli e timeline, consulta [servizio immagini e rendering API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) (6.5.9.0).

#### Annullare la validità del contenuto CDN memorizzato nella cache (6.5.6.0) {#invalidate-cdn-cached-content}

Ora puoi utilizzare l’ interfaccia utente [!DNL Dynamic Media] per annullare la validità del contenuto nella cache della rete di distribuzione dei contenuti (CDN). Di conseguenza, le risorse aggiornate sono disponibili immediatamente invece di attendere la scadenza della cache. Puoi annullare la validità della CDN:

* Creazione di un modello di invalidazione CDN: Selezione delle risorse e degli URL basati su modelli associati

* Selezione delle risorse e dei predefiniti associati tramite il selettore delle risorse

* Aggiunta di URL completi per le risorse

#### Pubblicazione selettiva delle risorse su [!DNL Experience Manager] e [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Ora puoi scegliere di pubblicare selettivamente o annullare la pubblicazione delle risorse in [!DNL Experience Manager] o [!DNL Dynamic Media] utilizzando la procedura guidata [!UICONTROL Pubblicazione rapida] o [!UICONTROL Gestisci pubblicazione]. È inoltre possibile impostare la modalità `Publish` o `Unpublish` a livello di cartella.

#### Imaging avanzato per Dynamic Media {#smart-imaging}

La funzione Smart imaging utilizza le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, garantendo prestazioni e coinvolgimento migliori. La funzione Smart imaging funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base al browser o alla velocità di connessione di rete. Consulta [Smart Imaging](../assets/imaging-faq.md).

#### Ritaglio avanzato nei profili video per Dynamic Media (6.5.3.0) {#smart-crop-video}

Il ritaglio avanzato per i video - una funzione opzionale disponibile in Profili video - utilizza Adobe Sensei per rilevare e ritagliare automaticamente il punto focale in qualsiasi video adattivo o video progressivo, indipendentemente dalle dimensioni. Consulta [informazioni sull’utilizzo del ritaglio avanzato nei profili video](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Supporto per [!DNL Azul Zulu OpenJDK] (6.5.9.0) {#support-azul-zulu}

È ora possibile sviluppare e utilizzare applicazioni con [!DNL Azul Zulu] build di [!DNL OpenJDK] per [!DNL Experience Manager Forms] nelle distribuzioni OSGi. Per ulteriori informazioni, consulta [Note sulla versione di Experience Manager 6.5 Service Pack 9](sp-release-notes.md) e [Requisiti tecnici](../sites-deploying/technical-requirements.md).

#### Possibilità di inviare un messaggio e-mail di notifica a un gruppo utilizzando [!UICONTROL Assegna attività] (6.5.9.0) {#group-notification-email}

Ora puoi inviare un messaggio e-mail di notifica a un indirizzo e-mail di gruppo utilizzando il passaggio del flusso di lavoro Assegna attività .

#### Possibilità di recuperare una bozza di comunicazione interattiva dopo aver modificato la sorgente di comunicazione interattiva (6.5.9.0) {#retrieve-draft-after-source-modifications}

È ora possibile recuperare una comunicazione interattiva salvata come bozza dopo aver modificato la comunicazione interattiva di origine.

#### Imposta il nome di dominio personalizzato per il caricamento, il rendering e la convalida del servizio reCAPTCHA (6.5.9.0) {#set-custom-domain-name-recaptcha}

Il servizio reCAPTCHA utilizza `https://www.recaptcha.net/` come dominio predefinito. Ora puoi modificare le impostazioni per impostare `https://www.google.com/` o qualsiasi nome di dominio personalizzato per caricare, eseguire il rendering e convalidare il servizio reCAPTCHA.

#### Miglioramenti dei dati di input per la fase del flusso di lavoro [!UICONTROL Invoke Form Data Model Service] (6.5.9.0) {#input-data-enhancements-fdm}

Quando si seleziona un modello di dati modulo e un servizio nel passaggio del flusso di lavoro [!UICONTROL Invoke Form Data Model Service], è possibile specificare gli argomenti del servizio per i dati di input.

Se si seleziona l&#39;opzione [!UICONTROL Relativo al payload] per allegare un file come argomento del servizio, ora è possibile specificare il percorso della cartella contenente il file invece del nome effettivo del file. La definizione del nome della cartella invece del nome dell’allegato del file consente di riutilizzare i modelli di flusso di lavoro. Non limitare il modello di flusso di lavoro a un singolo nome di file allegato.

#### Possibilità di utilizzare più pagine master in un modello Documento di record (6.5.9.0) {#use-multiple-master-pages-dor-template}

È ora possibile utilizzare più pagine master in un modello Documento di record. Di conseguenza, ora è possibile avere intestazione, piè di pagina, font, informazioni sul logo nella pagina del titolo e in altre pagine del modello.

#### Interruzioni della pagina di supporto nel documento di record (6.5.9.0) {#support-page-breaks-dor}

È ora possibile aggiungere interruzioni di pagina a un documento di record. Di conseguenza, se un pannello si interrompe all’interno delle pagine, è possibile aggiungere un’interruzione di pagina per spostare il pannello in una nuova pagina in un documento di record.

#### Mostra o nasconde il componente CAPTCHA in un modulo adattivo basato su regole (6.5.8.0) {#show-hide-captcha}

È ora possibile convalidare il CAPTCHA sia per l’invio di moduli adattivi che per l’azione dell’utente. Puoi anche aggiungere condizioni per convalidare CAPTCHA su un’azione dell’utente e mostrare o nascondere il componente CAPTCHA in un modulo adattivo in base alle regole.

#### Aggiungi servizi CAPTCHA personalizzati (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] fornisce supporto immediato per utilizzare Google reCAPTCHA (è necessaria una licenza separata per le API reCAPTCHA di Google) come servizio di convalida CAPTCHA. Puoi anche utilizzare un servizio CAPTCHA personalizzato per convalidare i CAPTCHA.

#### Altri miglioramenti (6.5.8.0) {#other-enhancements-forms-6580}

* Miglioramento dell’accessibilità del componente [!DNL Experience Manager Forms] Selettore data .

* È stato aggiunto il supporto per la generazione di una comunicazione interattiva in formato PCL tramite l’API PrintChannel.

* Quando si esegue una conversione PDFG, è ora possibile abilitare o disabilitare le modifiche del Registro di sistema [!DNL Experience Manager Forms] per la generazione di segnalibri personalizzati.

#### Miglioramenti delle prestazioni (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms migliora le prestazioni per:

* Convalida dei valori dei campi sul server quando si invia un modulo adattivo.

* Conversione di un modulo PDF in un modulo adattivo utilizzando [!DNL Automated Forms Conversion service].

#### Supporto per i gruppi di disponibilità Always On di Microsoft SQL Server 2016 per l&#39;alta disponibilità (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] ora supporta i gruppi di disponibilità Always On di  [!DNL Microsoft] SQL Server 2016 per le distribuzioni OSGi ad alta disponibilità.

#### Configurazione del client HTTP del modello dati modulo per ottimizzare le prestazioni (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] modello di dati modulo per l’integrazione con i servizi web RESTful come origine dati ora include configurazioni client HTTP per l’ottimizzazione delle prestazioni. Consulta [Configurare origini dati](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilità dell’opzione Ripristina per ciascun componente in modalità Layout (6.5.7.0) {#reset-option-layout-mode}

È ora possibile utilizzare l’opzione di reimpostazione per ciascun componente in modalità Layout di un modulo adattivo. Quando definisci un layout a più colonne per un pannello, puoi utilizzare questa funzione per reimpostare i singoli componenti all’interno del pannello. Consulta [Utilizzare la modalità di layout per ridimensionare i componenti](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Precompila un modulo adattivo sul client (6.5.6.0) {#prefill-merge-data-at-client}

Quando si precompila un modulo adattivo, il server [!DNL Experience Manager Forms] unisce i dati con un modulo adattivo e consegna il modulo compilato. Per impostazione predefinita, l’azione di unione dati viene eseguita sul server.
Ora è possibile configurare il server [!DNL Experience Manager Forms] in modo che [esegua l&#39;azione di unione dati sul client](../../help/forms/using/prepopulate-adaptive-form-fields.md) anziché sul server. Riduce notevolmente il tempo necessario per precompilare ed eseguire il rendering dei moduli adattivi.

#### Integrazione del modello dati del modulo con API RESTful su un server con implementazione SSL bidirezionale (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] Il modello dati del modulo può ora  [integrarsi con le API RESTful su un server in cui è implementato un SSL a due vie su di esso](../../help/forms/using/configure-data-sources.md).

#### È stato aggiunto il supporto per [!DNL Adobe Sign] Tag testo nel servizio Automated forms conversion (6.5.6.0) {#sign-integration-acroform-afcs}

Se un AcroForm include [!DNL Adobe Sign] Tag testo, tali campi vengono ora riconosciuti e rappresentati come campi [!DNL Adobe Sign] nel modulo adattivo convertito utilizzando [!DNL Automated Forms Conversion service]. Un firmatario può compilare tali campi durante la firma del modulo adattivo.

#### Supporto per la conversione di PDF forms colorati in moduli adattivi (6.5.6.0) {#colored-PDF-forms}

È possibile utilizzare [!DNL Automated Forms Conversion service] per convertire PDF forms colorati in moduli adattivi.

#### Supporto per i protocolli SMB 2 e SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] ora supporta i protocolli SMB 2 e SMB 3.

#### Memorizzazione in cache migliorata per le pagine dei moduli adattivi tradotte (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Ora è possibile specificare le [impostazioni internazionali come selettore nell&#39;URL del modulo adattivo invece di un argomento nell&#39;URL del modulo adattivo](../../help/forms/using/supporting-new-language-localization.md). Consente di memorizzare nella cache i moduli adattivi convertiti su [!DNL Experience Manager Dispatcher]. La memorizzazione nella cache dei moduli adattivi convertiti non era possibile nelle versioni precedenti. Per informazioni dettagliate sulla configurazione della memorizzazione in cache per l&#39;utilizzo delle impostazioni internazionali come selettore nell&#39;URL del modulo adattivo, consulta [Configurare la cache dei moduli adattivi nel dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Salvare l’output del servizio del modello dati modulo su una variabile (6.5.6.0) {#save-fdm-service-to-variable}

Il modello dati modulo consente di salvare l’output di un servizio del modello dati modulo su una variabile. [!DNL Experience Manager Forms] ora mappa automaticamente il tipo di servizio del modello dati del modulo al tipo di variabile.

#### Allegare più file per il componente File allegato (6.5.6.0) {#attach-multiple-files}

È ora possibile [allegare più file](../../help/forms/using/introduction-forms-authoring.md) al componente [!UICONTROL File allegato] dei moduli adattivi.

#### Personalizzare le colonne della Casella in entrata Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

È possibile personalizzare una [!DNL Experience Manager] casella in entrata per modificare il titolo predefinito di una colonna, riordinare la posizione di una colonna e visualizzare colonne aggiuntive in base ai dati di un flusso di lavoro. I membri del gruppo `administrators` o `workflow-administrators` possono personalizzare le colonne. Per ulteriori informazioni, consulta [Controllo amministratore](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizzare le colonne della casella in entrata di Experience Manager](assets/customize-columns.gif)

#### Possibilità di salvare le comunicazioni interattive come bozza (6.5.5.0) {#save-as-draft}

Puoi utilizzare l’interfaccia utente dell’agente per salvare una o più bozze per ogni comunicazione interattiva e recuperare la bozza in un secondo momento per continuare a lavorarci. Potete specificare un nome diverso per ogni bozza da identificare. Per ulteriori informazioni, consulta [Salvare le comunicazioni interattive come bozza](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Salva come bozza](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] supporto di application server (6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms ha aggiunto il supporto per [!DNL Oracle WebLogic 12] per Adobe Experience Manager Forms su JEE. Puoi eseguire l’aggiornamento da una versione precedente o impostare un nuovo Forms Experience Manager 6.5 sul server JEE su [!DNL Oracle WebLogic] 12.2.1.4 e versioni successive. Successivamente corrisponde alle modifiche minori, dove x in 12.2.1.x viene sostituito con un numero di versione.

#### Miglioramenti all’accessibilità (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms include i seguenti miglioramenti all’accessibilità:

* Quando un utente visualizza l&#39;anteprima di un modulo adattivo come modulo HTML, il campo [!UICONTROL Firma scarabocchio] mantiene lo stato attivo.

* I messaggi di errore visualizzati all’invio di un modulo adattivo ora contengono l’attributo `aria-describedBy` . L’attributo è associato ai campi indicati nel messaggio di errore. L&#39;attributo `aria-describedby` indica gli ID degli elementi che descrivono l&#39;oggetto. Aiuta a stabilire una relazione tra widget o gruppi e testo che li ha descritti.

* Se un modulo adattivo contiene alcuni campi obbligatori, l’attributo obbligatorio è impostato su `True` per tali campi nello schema di accessibilità ARIA.

#### Autenticazione basata su certificato X-509 per i servizi web basati su SOAP nel modello per dati modulo (6.5.5.0) {#x509-based-authentication-soap}

Il modello dati modulo supporta ora l’autenticazione basata su certificato X-509 durante l’utilizzo dei servizi web SOAP come origine dati. Per ulteriori informazioni, vedere [Configurare servizi Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Altri miglioramenti chiave (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms su JEE Document Security è ora basato su [!DNL Apache Struts 2].

* È stato aggiunto il supporto per [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Generare output stampabile nei flussi di lavoro Experience Manager Forms (6.5.4.0) {#generate-printable-output}

Il passaggio del flusso di lavoro Genera output stampabile consente di integrare un file modello di origine con un file di dati. Questa integrazione consente di stampare o salvare copie diverse del file modello. Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL. Per ulteriori informazioni su questa funzione, consulta [Flusso di lavoro incentrato su Forms su OSGi - Riferimento passo](../forms/using/aem-forms-workflow-step-reference.md).

![Genera output stampabile](assets/generate-print-output-step.gif)

#### Supporto a più colonne per moduli adattivi e comunicazioni interattive in modalità Layout (6.5.4.0) {#multi-column-adaptive-forms}

È ora possibile definire il numero di colonne per un pannello nei moduli adattivi e nelle comunicazioni interattive. Passa alla modalità di layout per utilizzare la nuova opzione a più colonne. Per ulteriori informazioni, consulta [Utilizzare la modalità Layout per ridimensionare i componenti](../forms/using/resize-using-layout-mode.md).

![Layout a più colonne](assets/multi-column-layout.gif)

#### Personalizzazioni della casella in entrata Experience Manager (6.5.4.0) {#aem-inbox}

La nuova opzione Controllo amministratore consente agli amministratori di:

* Personalizza il testo dell’intestazione e il logo.

* Controlla la visualizzazione dei collegamenti di navigazione disponibili nell’intestazione.

L’opzione Controllo amministratore è visibile solo per i membri del gruppo `administrators` o `workflow-administrators`. Per ulteriori informazioni su questa funzione, consulta [Casella in entrata](../sites-authoring/inbox.md).

#### Supporto di testo RTF nei moduli HTML5 (6.5.4.0) {#rich-text-support}

Convertire un campo di testo in un modulo XFA in un campo di testo RTF in un modulo HTML5. Per ulteriori informazioni, vedere [Progettazione di modelli di modulo per i moduli HTML5](../forms/using/designing-form-template.md).

#### Miglioramenti all’accessibilità (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms include i seguenti miglioramenti all’accessibilità:

* Gli assistenti vocali annunciano correttamente in un modulo adattivo caselle di controllo, collegamenti, selettore data e campi di immissione data .

* Ogni pagina di un modulo adattivo ora include un titolo e un’etichetta di riferimento principale.

#### Condividere e richiedere l’accesso agli elementi in entrata di un utente Experience Manager Forms (6.5.3.0) {#share-request-access}

È possibile condividere gli elementi della casella in entrata con un altro utente. Una volta che un altro utente ottiene l&#39;accesso agli elementi della casella in entrata, può richiedere e intraprendere le azioni appropriate sugli elementi condivisi. Allo stesso modo, puoi richiedere l’accesso agli elementi della casella in entrata ad altri utenti. Consulta [Condividere e richiedere l’accesso agli elementi in entrata di un utente](../forms/using/configure-shared-queues-osgi.md).

#### Configurare le impostazioni predefinite per gli elementi in entrata di un utente Forms di Experience Manager (6.5.3.0) {#configure-out-of-office}

Se si prevede di uscire dall&#39;ufficio, è possibile specificare cosa accade agli articoli che vi vengono assegnati per quel periodo.
Puoi specificare una data e un’ora di inizio e una data e un’ora di fine per rendere effettive le impostazioni fuori sede. Puoi impostare una persona predefinita a cui vengono inviati tutti gli elementi. Consultare [Configurare le impostazioni fuori sede](../forms/using/configure-out-of-office-settings.md).

#### Generare più comunicazioni interattive utilizzando l’API Batch per Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Puoi utilizzare l’API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L’API Batch combina i dati con un modello per produrre una comunicazione interattiva. L&#39;API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto della carta di credito per più clienti. Consulta [Generare più comunicazioni interattive utilizzando l&#39;API Batch](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versioni chiave da [!DNL Adobe Experience Manager] 6.5 SP9 {#key-releases-since-last-sp}

Tra il 27 maggio 2021 e il 26 agosto 2021, Adobe ha rilasciato quanto segue, oltre ai Service Pack:

* [!DNL Adobe Experience Manager] come Cloud Service  [2021.6.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-6-0.html),  [2021.7.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-7-0.html) e  [2021.8.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=en).

* [[!DNL Experience Manager] app desktop 2.1 (2.1.3.3)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experienci Manager Screens: Feature Pack 202105](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202105.html?lang=en)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Note sulla versione di disponibilità generale per [!DNL Experience Manager] 6.5](release-notes.md)
>* [Note sulla versione del Service Pack per [!DNL Experience Manager] 6.5](sp-release-notes.md)

