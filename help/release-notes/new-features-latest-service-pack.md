---
title: Novità di [!DNL Experience Manager] 6.5 Service Pack 11
description: Novità di [!DNL Experience Manager] 6.5 Service Pack 11
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 092ba82ac645539fd0d4e2085c380025201914de
workflow-type: tm+mt
source-wordcount: '4399'
ht-degree: 1%

---

# Novità di [!DNL Adobe Experience Manager] 6.5 Service Pack 11 {#aem-whats-new-service-pack}

<!-- TBD: Downsample this image. We do not need as big an image since customers don't use as big a screen to view. Also, having a 700+ KB decorative image is bad for page load time.
-->

![Novità](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 I Service Pack forniscono nuove funzionalità, miglioramenti richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza a intervalli trimestrali. La disponibilità trimestrale semplifica l&#39;accesso e l&#39;adozione di nuove caratteristiche e innovazioni.

Questo articolo evidenzia le funzioni incluse nell&#39;ultimo Service Pack, [caratteristiche principali incluse nei Service Pack 6.5 precedenti](#key-features-previous-service-packs)e [versioni chiave dall&#39;ultimo Service Pack](#key-releases-since-last-sp) rilascio.

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

* È possibile generare automaticamente la mappa del sito a scopo di SEO utilizzando [Pacchetto indice SEO](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). Supporta sitemap, URL alternativi, meta tag robot e altro ancora nel [!DNL Core Components].

* È stato aggiunto il supporto per più campi per il tipo di dati a più righe.

* È stato migliorato per informare gli utenti del processo asincrono attualmente in esecuzione in background, in modo da impedire loro di attivare più operazioni asincrone sullo stesso percorso.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* I miglioramenti dell’esperienza utente visualizzano il numero di risorse presenti in una cartella. Per più di 1000 risorse in una cartella, [!DNL Assets] visualizza oltre 1000.

   ![Numero di risorse in una cartella](/help/assets/assets/browse-folder-number-of-assets.png)

* Sono disponibili i seguenti miglioramenti dell’accessibilità:

   * Nella vista a schede [!DNL Assets] archivio, quando si utilizza `Tab` per spostare lo stato attivo sul primo elemento che apre Azioni rapide sullo stato attivo, l’assistente vocale annuncia il nome dell’elemento attivo.
   * In [!DNL Dynamic Media] [!UICONTROL Editor predefiniti visualizzatore], se colori ombreggiatura e colore bordo non sono presenti, gli input vengono disattivati utilizzando la proprietà disabilitata. Gli utenti della tastiera non sono in grado di attivare l’input e gli assistenti vocali non annunciano lo stato del controllo come disattivato.
   * In [!DNL Dynamic Media], nell’interfaccia di per creare un nuovo profilo di codifica video, la [!UICONTROL Rapporto ritaglio avanzato] l’opzione è contrassegnata come accessibile dagli assistenti vocali che l’hanno annunciata in modo appropriato.

### [!DNL Dynamic Media] {#dynamic-media}

* Ora puoi utilizzare [!DNL Dynamic Media] per configurare le Impostazioni generali anziché dover passare attraverso [!DNL Dynamic Media Classic] applicazione desktop. Vedi [Configurare le impostazioni generali di Dynamic Media](/help/assets/dm-general-settings.md).

   ![Impostazioni generali di DM](/help/assets/assets-dm/dm-general-settings.png)

* Ora puoi utilizzare [!DNL Dynamic Media] per configurare l’impostazione di pubblicazione anziché passare attraverso [!DNL Dynamic Media Classic] applicazione desktop. Vedi [Configurare l’installazione di Dynamic Media Publish](/help/assets/dm-publish-settings.md).

   ![Impostazioni di pubblicazione DM](/help/assets/assets-dm/dm-publish-setup.png)

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>* I pacchetti del componente aggiuntivo [!DNL Experience Manager Forms] vengono rilasciati una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].


## Funzioni principali precedenti [!DNL Experience Manager] 6.5 Service Pack {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Funzioni incluse nella versione 6.5.10.0 di AEM {#features-sites-65100}

* **Miglioramento [!DNL Content Fragment] Modelli ed editor**: È ora possibile creare modelli complessi e personalizzati per il contenuto strutturato utilizzando [!DNL Content Fragment] modelli. Le strutture di contenuto sono modularizzate in elementi di base modellati come sottoframmenti. I frammenti di livello superiore fanno riferimento a tali sottoframmenti. Ulteriori miglioramenti del tipo di dati, come le regole di convalida avanzate, migliorano ulteriormente la flessibilità nella modellazione dei contenuti con [!DNL Content Fragments]. La [!DNL Experience Manager] [!DNL Content Fragment] l’editor supporta le strutture di frammenti nidificati in una sessione dell’editor comune, con miglioramenti quali la visualizzazione struttura ad albero e la navigazione a schede tramite gerarchie di frammenti.

* **API GraphQL per[!DNL Content Fragments]**: La nuova API GraphQL è il metodo standard per distribuire contenuti strutturati in formato JSON. Le query GraphQL consentono ai client di richiedere solo gli elementi di contenuto rilevanti per il rendering di un’esperienza. Tale selezione elimina la consegna dei contenuti in eccesso (possibilità con le API REST HTTP) che richiede l’analisi dei contenuti lato client. Gli schemi GraphQL sono derivati da [!DNL Content Fragment] I modelli e le risposte API vengono effettuati in formato JSON. In [!DNL Experience Manager] come [!DNL Cloud Service], [Le query GraphQL persistono](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) e elabora richieste di GET compatibili con la cache. Non è ancora possibile in [!DNL Experience Manager] 6.5.

* **Gestione delle gerarchie e anteprima futura**: Gli utenti ora dispongono di un’interfaccia per accedere alle strutture dei contenuti [!DNL Experience Manager] lanci, inclusa la possibilità di aggiungere e rimuovere pagine in un lancio. Questa funzione migliora la flessibilità di [!DNL Experience Manager] lancia per creare versioni di contenuto destinate alla pubblicazione futura. [Funzione di deformazione del tempo](/help/sites-authoring/working-with-page-versions.md#timewarp) consente agli utenti di visualizzare in anteprima gli avvii come stati di contenuto futuri.

* [!DNL Experience Manager] visualizza direttamente un elenco di tutti i modelli di contenuto presenti in una cartella senza che gli autori di contenuti debbano spostarsi all’interno della struttura del file. La funzionalità ora richiede meno clic e migliora l’efficienza di authoring.

* Campo percorso in [!DNL Sites] l’editor consente agli autori di trascinare le risorse da [!DNL Content Finder].

* Platform fornisce alcuni miglioramenti all’accessibilità. Vedi [Aggiornamenti della piattaforma](/help/release-notes/sp-release-notes.md#platform-65100).

#### Possibilità di ripristinare le pagine e la struttura eliminate (6.5.9.0) {#ability-to-restore-pages-tree}

È ora possibile ripristinare le pagine eliminate e l&#39;intera visualizzazione ad albero in un [!DNL Experience Manager Sites] pagina.

#### Ordinare le pagine Live Copy disponibili per il rollout (6.5.8.0) {#sort-livecopy-pages}

Ora puoi ordinare le pagine Live Copy disponibili per il rollout utilizzando il [!UICONTROL Nome], [!UICONTROL Data ultima modifica]e [!UICONTROL Data ultimo rollout] proprietà. La [!UICONTROL Data ultimo rollout] per una pagina è stata introdotta una nuova proprietà in questa versione.

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

* L’accesso anonimo ad CRXDE Lite non è consentito per migliorare la sicurezza. Gli utenti vengono invece indirizzati alla schermata di accesso. Vedi [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Quando si copia o incolla una struttura di pagina, è ora possibile incollare la pagina principale o incollare la pagina principale con le pagine secondarie della struttura.

* [!DNL Adobe Experience Manager Experience Fragments] esportato in [!DNL Adobe Target] le aree di lavoro ora vengono visualizzate come tipi di offerta univoci e origini offerte in [!DNL Target].

* Multi Site Manager : l’attivazione di pubblicazione ora elimina un componente dalla pagina pubblicata se un componente viene eliminato dalla pagina sorgente.

* Multi Site Manager : quando il nome di un componente locale in un [!UICONTROL Live Copy] è identico al nome di un componente nella blueprint e il componente viene rilasciato dalla blueprint, quindi il termine `_msm_moved` viene ora aggiunto al nome del componente locale.

#### Miglioramenti al sistema di stili (6.5.4.0) {#style-system-enhancements}

È ora possibile selezionare gli stili all’interno della finestra di dialogo del componente utilizzando il sistema di stili avanzato.

#### Miglioramenti delle prestazioni in vari settori (6.5.4.0) {#performance-improvements}

* Riduzione del tempo necessario per caricare e inizializzare ContextHub all&#39;interno di un sito (`contexthub.kernel.js`). Ne risulta un caricamento più rapido delle pagine durante una visita al sito.

* Riduzione del tempo necessario per aggiornare una pagina dopo il trascinamento [!DNL Experience Fragments] a [!DNL Sites] Editor pagina.

* Riduzione del tempo di caricamento per le voci in un [!DNL Sites] pagina con più di 200 Live Copy in **[!UICONTROL Panoramica di Live Copy]**.

* È stata migliorata la gestione degli URL incompleti o non validi. Tali URL possono rallentare l’Editor modelli.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Funzioni incluse nella versione 6.5.10.0 di AEM {#features-assets-65100}

* [!DNL Experience Manager] estende la funzionalità Risorse collegate all’utilizzo di [!DNL Dynamic Media] immagini nei componenti core applicabili. Vedi [utilizzare Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* Quando condividi singole risorse e raccolte come collegamento (utilizzando [!UICONTROL Condivisione collegamenti] (finestra di dialogo), gli utenti possono scegliere se consentire al destinatario di scaricare le risorse originali, le loro rappresentazioni o entrambi. Vedi [Condividere le risorse tramite collegamento](/help/assets/link-sharing.md).

   ![per consentire il download solo delle risorse originali, solo delle rappresentazioni o di entrambe](/help/release-notes/assets/share-assets-as-link.png)

* Quando gli utenti scaricano le risorse condivise con loro come collegamento, possono scegliere di scaricare le risorse originali, le rappresentazioni o entrambi.

* **Limita le risorse secondarie generate**: Gli amministratori possono limitare il numero di risorse secondarie [!DNL Experience Manager] genera per risorse composte come file PDF, PowerPoint, InDesign e Keynote.

   ![limitare la generazione di risorse secondarie](/help/assets/assets/sub-asset-limit.png)

* Nuovo [!DNL Camera Raw] pacchetto disponibile che supporta [!DNL Adobe Camera Raw] v10.4. Vedi [elaborare immagini utilizzando [!DNL Camera Raw]](/help/assets/camera-raw.md).

#### Versioni precedenti {#previous-releases-assets}

* È stata aggiornata la denominazione delle impostazioni locali e delle regioni cinesi relative a Hong Kong, Macao e Taiwan, per renderle coerenti con le opinioni sociali e politiche cinesi (6.5.9.0).

* È stata introdotta una configurazione opzionale per modificare la casing negli ID e-mail nella risposta API ACP da [!DNL Adobe Experience Manager] (6.5.9.0)

   ![configurazione per modificare gli ID e-mail in lettere minuscole nella risposta ACP da [!DNL Experience Manager]](assets/email-lowcase-config.png)

* Il contrasto di testo e icone sullo sfondo è migliorato per varie funzioni. Questa implementazione delle linee guida per l’accessibilità dei contenuti web (WCAG) rende [!DNL Assets] più accessibile per gli utenti con una visione limitata e una percezione del colore. Vedi [miglioramenti dell’accessibilità in [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590) (6.5.9.0)
* Quando utilizzi [Funzionalità Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md), ora puoi visualizzare un elenco di tutti i [!DNL Sites] pagine che utilizzano la risorsa. Questi riferimenti a una risorsa sono disponibili nelle’ [!UICONTROL Proprietà] pagina. Questo consente agli amministratori, agli esperti di marketing e ai bibliotecari di visualizzare in modo completo l’utilizzo delle risorse, consentendo un migliore monitoraggio, gestione e coerenza del marchio (6.5.8.0).

* Quando si elimina una risorsa a cui si fa riferimento in una pagina web, [!DNL Experience Manager] visualizza un avviso. Puoi forzare l’eliminazione di una risorsa di riferimento oppure controllare e modificare i riferimenti visualizzati nella [!DNL Properties] della risorsa. Facendo clic sui riferimenti si apre il locale e il remoto [!DNL Sites] pagine (6.5.8.0).

* [!DNL Assets] e [!DNL Dynamic Media] forniscono diversi miglioramenti dell’accessibilità. I miglioramenti riguardano la navigazione da tastiera, l’uso di assistenti vocali e miglioramenti simili per consentire l’utilizzo di tecnologie per l’accessibilità (AT). Vedi [[!DNL Assets] miglioramenti](/help/release-notes/sp-release-notes.md#assets-6570) e [[!DNL Dynamic Media] miglioramenti](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Gli utenti possono ordinare le risorse digitali nelle viste a schede e a colonne (6.5.7.0).

#### Miglioramenti all’accessibilità (6.5.6.0) {#accessibility-assets-6560}

* **Messa a fuoco dell&#39;interfaccia utente migliorata durante la navigazione da tastiera** ad esempio:

   * `x` icona in [!UICONTROL Anteprima versione] finestra di dialogo di una risorsa in [!UICONTROL Timeline].

   * Opzioni fruibili dell’interfaccia utente.

   * Campo e-mail [!UICONTROL Condividi collegamento] finestra di dialogo e campo per aggiungere un gruppo utenti chiuso in [!UICONTROL Autorizzazione] scheda della cartella [!UICONTROL Proprietà].

* **Funzionalità ottimizzata tramite tasti di tastiera**

   Gli utenti possono utilizzare i tasti di tastiera per trascinare i controlli nell’editor Modulo schema metadati nella modalità Sfoglia dell’assistente vocale.

* **Migliore fruibilità per gli utenti degli assistenti vocali**, per i seguenti motivi:

   * Gli assistenti vocali annunciano lo scopo dei lettori video e audio.

   * Gli assistenti vocali annunciano lo scopo delle opzioni dell’interfaccia utente per rimuovere i tag selezionati utilizzando [!UICONTROL Finestra di dialogo per la selezione dei tag] su risorsa [!UICONTROL Proprietà].

   * Gli assistenti vocali annunciano le intestazioni di riga e gli elementi di riga delle tabelle, in modo che gli utenti sappiano quali voci appartengono alla stessa riga.

   * Titolo descrittivo e significativo della pagina di ricerca.

   * Gli assistenti vocali annunciano le opzioni nel pannello dei filtri di ricerca come pannello a soffietto espandibile.

#### Altri miglioramenti in [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* I gruppi di utenti associati alle cartelle (privati e non privati) ora vengono rimossi dall’archivio in [eliminazione di tali cartelle](/help/assets/private-folder.md#delete-private-folder). Tuttavia, i gruppi di utenti ridondanti, orfani, inutilizzati e generati automaticamente possono essere rimossi dall’archivio utilizzando JMX.

#### Miglioramenti all’accessibilità in [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] è ora più accessibile in conformità alle linee guida per l’accessibilità dei contenuti web (WCAG). L’accessibilità è stata migliorata a causa dei seguenti miglioramenti:

* Molti elementi, controlli, pagine e finestre di dialogo dell’interfaccia sono compatibili con gli assistenti vocali.

* Molti elementi, controlli e campi modulo di input dell’interfaccia utente sono accessibili da tastiera.

* Il colore e il contrasto di alcuni elementi dell’interfaccia utente sono stati aggiornati in modo che gli utenti con vista limitata o senza percezione del colore possano distinguere tali elementi. Ad esempio, il colore delle icone di valutazione delle stelle (ad esempio in [!UICONTROL Valutazione] sezione [!UICONTROL Avanzate] scheda nella risorsa [!UICONTROL Proprietà] o nella vista a schede) viene modificato per ottenere un contrasto adeguato.

   ![Icone di valutazione con contrasto migliorato](assets/star-rating-icons.png)

#### Gestione migliorata delle eccezioni (6.5.5.0) {#exception-handling}

[!DNL Assets] il flusso dell&#39;interfaccia utente offre una migliore gestione delle eccezioni. Se una risorsa non ha un tipo per la sua dimensione, l’eccezione osservata viene registrata nei file di registro.

#### Configura [!DNL Experience Manager Assets] con [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Il canale di autorizzazione tra [!DNL Experience Manager Assets] e [!DNL Brand Portal] viene modificato. In precedenza, [!DNL Brand Portal] è stato configurato nell’interfaccia classica tramite la versione precedente del gateway OAuth, che utilizza lo scambio di token JWT per ottenere un token di accesso IMS per l’autorizzazione. [!DNL Experience Manager Assets] è ora configurato con [!DNL Brand Portal] attraverso [!DNL Adobe I/O], che fornisce un token IMS per l’autorizzazione del tuo [!DNL Brand Portal] inquilino.

Passaggi da configurare [!DNL Experience Manager Assets] con [!DNL Brand Portal] sono diversi a seconda del [!DNL Experience Manager] e se si sta configurando per la prima volta o se si desidera aggiornare le configurazioni esistenti. Vedi [Configurare Experience Manager Assets con Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) per i dettagli.

#### Miglioramenti all’accessibilità (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] include i seguenti miglioramenti all’accessibilità:

* I tasti freccia sulla tastiera possono essere utilizzati per spostare e scorrere le aree all&#39;interno delle immagini ingrandite. Per ulteriori informazioni, consulta [visualizzare in anteprima le risorse utilizzando solo i tasti di tastiera](../assets/manage-assets.md#previewing-assets).

* Le caselle di controllo a stato misto (in cui, a meno che non si selezionino tutti i predicati nidificati, le caselle di controllo di primo livello non sono selezionate e sono evidenziate) nel pannello Filtri sono leggibili dagli assistenti vocali.

* Nelle etichette dei campi data vengono forniti vincoli di formato data e ora per consentire agli utenti di immettere la data nel formato corretto utilizzando la tastiera.
Esempio, `On Time (MM-DD-YYYY HH:mm)`. Qui MM è mese in formato a due cifre, AAAA è anno, GG è giorno in formato a due cifre, HH è ora in formato militare a 24 ore e mm è minuto.

* Gli assistenti vocali annunciano l’opzione per rimuovere i tag selezionati (`X` e il numero dei tag selezionati.

#### Colonna ordinabile per la data di creazione delle risorse nella vista a elenco (6.5.3.0) {#sortable-date-created-column}

Nella vista a elenco DAM e nei risultati della ricerca delle risorse nella vista a elenco viene aggiunta una nuova colonna ordinabile per la data di creazione delle risorse.

![Colonna ordinabile per la data creata](assets/asset-created-date.png)

#### Ricerca visiva per [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets]Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di In Experience Manager vengono visualizzate le immagini con tag avanzati dell’archivio DAM simili a quelle selezionate dall’utente. Vedi [Ricerca visiva](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

* Sono stati apportati molti miglioramenti all’accessibilità in [!DNL Dynamic Media] in modo che un assistente vocale possa presentare una descrizione più appropriata e utile dell’azione o dell’interfaccia utente. Vedi [[!DNL Dynamic Media] aggiornamenti](/help/release-notes/sp-release-notes.md#dynamic-media-65100) (6.5.10.0).

* [[!DNL Dynamic Media] è più accessibile](sp-release-notes.md#assets-accessibility-6590) in termini di:

   * Facilità di utilizzo con i tasti della tastiera.
   * Contrasto (con sfondo) di testo, testo segnaposto e controlli in vari editor.
   * Accessibilità e narrazione da parte degli assistenti vocali.

* Offri immagini di alta qualità in modo efficiente su dispositivi con display ad alta risoluzione e larghezza di banda limitata, con Smart Imaging DPR (Device Pixel Ratio) e ottimizzazione della larghezza di banda della rete. Vedi [Domande frequenti sull’imaging intelligente](/help/assets/imaging-faq.md) (6.5.9.0)

* [!DNL Dynamic Media] consegna (`fmt` Modificatore URL) ora supporta il formato immagine AVIF (formato immagine AV1) di nuova generazione. Per ulteriori dettagli e timeline, consulta [fmt API di servizio e rendering delle immagini](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) (6.5.9.0)

#### Supporto per risorse 3D in [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

Supporto per immagini 3D in [!DNL Dynamic Media] consente ai clienti di pubblicare e aggiungere contenuti 3D a pagine e applicazioni web. Il supporto include:

* Pubblica i formati comuni di risorse 3D e genera un URL di risorse che può essere utilizzato nelle pagine web e in altre applicazioni.

* Visualizzatore web 3D basato su [!DNL Adobe Dimension]per visualizzare in modo interattivo le risorse 3D pubblicate.

* Pubblicare e visualizzare risorse 3D comuni su [!DNL Experience Manager Sites] pagine che utilizzano [!DNL Sites] Componente WCM.

#### Annullare la validità del contenuto CDN memorizzato nella cache (6.5.6.0) {#invalidate-cdn-cached-content}

Ora puoi utilizzare la [!DNL Dynamic Media] Interfaccia utente per annullare la validità del contenuto nella cache della rete CDN (Content Delivery Network). Di conseguenza, le risorse aggiornate sono disponibili immediatamente invece di attendere la scadenza della cache. Puoi annullare la validità della CDN:

* Creazione di un modello di invalidazione CDN: Selezione delle risorse e degli URL basati su modelli associati

* Selezione delle risorse e dei predefiniti associati tramite il selettore delle risorse

* Aggiunta di URL completi per le risorse

#### Pubblicazione selettiva delle risorse su [!DNL Experience Manager] e [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Ora puoi scegliere di pubblicare o annullare selettivamente la pubblicazione delle risorse su [!DNL Experience Manager] o [!DNL Dynamic Media] utilizzo [!UICONTROL Pubblicazione rapida] o [!UICONTROL Gestisci pubblicazione] procedura guidata. È inoltre possibile impostare `Publish` o `Unpublish` a livello di cartella.

#### Imaging avanzato per Dynamic Media {#smart-imaging}

La funzione Smart imaging utilizza le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, garantendo prestazioni e coinvolgimento migliori. La funzione Smart imaging funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base al browser o alla velocità di connessione di rete. Consulta [Smart Imaging](../assets/imaging-faq.md).

#### Ritaglio avanzato nei profili video per Dynamic Media (6.5.3.0) {#smart-crop-video}

Il ritaglio avanzato per i video - una funzione opzionale disponibile in Profili video - utilizza Adobe Sensei per rilevare e ritagliare automaticamente il punto focale in qualsiasi video adattivo o video progressivo, indipendentemente dalle dimensioni. Vedi [informazioni sull’utilizzo del ritaglio avanzato nei profili video](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Funzioni incluse nella versione 6.5.10.0 di AEM {#features-forms-65100}

>[!NOTE]
>
>Il pacchetto aggiuntivo di [!DNL Experience Manager Forms] è reso disponibile una settimana dopo il [!DNL Experience Manager] Versione Service Pack.

* Ora puoi utilizzare il servizio Automated forms conversion per [convertire i PDF forms in francese, tedesco, spagnolo, italiano e portoghese](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) ai moduli adattivi.

* **Messaggi di errore nel browser Proprietà**: Sono stati aggiunti messaggi di errore per ciascuna proprietà nel browser Proprietà adattive Forms. Questi messaggi consentono di comprendere i valori consentiti per un campo.

* **Supporto per l’utilizzo dell’opzione letterale per impostare il valore per una variabile di tipo JSON**: Puoi utilizzare l’opzione letterale per impostare il valore per una variabile di tipo JSON nel passaggio della variabile set di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

* [Aggiornamenti alla piattaforma](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] in JEE è stato aggiunto il supporto per le seguenti piattaforme:
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

* È stato aggiunto il supporto per `GuideBridge#getGuidePath` API in [!DNL AEM Forms].

#### Supporto per [!DNL Azul Zulu OpenJDK] (6.5.9.0) {#support-azul-zulu}

È ora possibile sviluppare e utilizzare applicazioni con [!DNL Azul Zulu] build di [!DNL OpenJDK] per [!DNL Experience Manager Forms] sulle distribuzioni OSGi. Per ulteriori informazioni, consulta [Note sulla versione di Experience Manager 6.5 Service Pack 9](sp-release-notes.md) e [Requisiti tecnici](../sites-deploying/technical-requirements.md).

#### Possibilità di inviare un messaggio e-mail di notifica a un gruppo utilizzando [!UICONTROL Assegna attività] (6.5.9.0) {#group-notification-email}

Ora puoi inviare un messaggio e-mail di notifica a un indirizzo e-mail di gruppo utilizzando il passaggio del flusso di lavoro Assegna attività .

#### Possibilità di recuperare una bozza di comunicazione interattiva dopo aver modificato la sorgente di comunicazione interattiva (6.5.9.0) {#retrieve-draft-after-source-modifications}

È ora possibile recuperare una comunicazione interattiva salvata come bozza dopo aver modificato la comunicazione interattiva di origine.

#### Imposta il nome di dominio personalizzato per il caricamento, il rendering e la convalida del servizio reCAPTCHA (6.5.9.0) {#set-custom-domain-name-recaptcha}

Il servizio reCAPTCHA utilizza `https://www.recaptcha.net/` come dominio predefinito. Ora puoi modificare le impostazioni da impostare `https://www.google.com/` o qualsiasi nome di dominio personalizzato da caricare, eseguire il rendering e convalidare il servizio reCAPTCHA.

#### Miglioramenti dei dati di input per [!UICONTROL Richiama servizio modello dati modulo] passaggio del flusso di lavoro (6.5.9.0) {#input-data-enhancements-fdm}

Quando si selezionano un modello dati modulo e un servizio in [!UICONTROL Richiama servizio modello dati modulo] al passaggio del flusso di lavoro, è possibile specificare gli argomenti del servizio per i dati di input.

Se si seleziona [!UICONTROL Relativo al payload] per allegare un file come argomento del servizio, ora è possibile specificare il percorso della cartella che contiene il file invece del nome effettivo. La definizione del nome della cartella invece del nome dell’allegato del file consente di riutilizzare i modelli di flusso di lavoro. Non limitare il modello di flusso di lavoro a un singolo nome di file allegato.

#### Possibilità di utilizzare più pagine master in un modello Documento di record (6.5.9.0) {#use-multiple-master-pages-dor-template}

È ora possibile utilizzare più pagine master in un modello Documento di record. Di conseguenza, ora è possibile avere intestazione, piè di pagina, font, informazioni sul logo nella pagina del titolo e in altre pagine del modello.

#### Interruzioni della pagina di supporto nel documento di record (6.5.9.0) {#support-page-breaks-dor}

È ora possibile aggiungere interruzioni di pagina a un documento di record. Di conseguenza, se un pannello si interrompe all’interno delle pagine, è possibile aggiungere un’interruzione di pagina per spostare il pannello in una nuova pagina in un documento di record.

#### Mostra o nasconde il componente CAPTCHA in un modulo adattivo basato su regole (6.5.8.0) {#show-hide-captcha}

È ora possibile convalidare il CAPTCHA sia per l’invio di moduli adattivi che per l’azione dell’utente. Puoi anche aggiungere condizioni per convalidare CAPTCHA su un’azione dell’utente e mostrare o nascondere il componente CAPTCHA in un modulo adattivo basato su regole.

#### Aggiungi servizi CAPTCHA personalizzati (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] fornisce supporto immediato per l’utilizzo di Google reCAPTCHA (è necessaria una licenza separata per le API reCAPTCHA di Google) come servizio di convalida CAPTCHA. Puoi anche utilizzare un servizio CAPTCHA personalizzato per convalidare i CAPTCHA.

#### Altri miglioramenti (6.5.8.0) {#other-enhancements-forms-6580}

* Miglioramento dell’accessibilità dei [!DNL Experience Manager Forms] Componente Selezione data .

* È stato aggiunto il supporto per la generazione di una comunicazione interattiva in formato PCL tramite l’API PrintChannel.

* Quando si esegue una conversione PDFG, ora è possibile abilitare o disabilitare la funzione [!DNL Experience Manager Forms] modifiche del Registro di sistema per la generazione di segnalibri personalizzati.

#### Miglioramenti delle prestazioni (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms migliora le prestazioni per:

* Convalida dei valori dei campi sul server quando si invia un modulo adattivo.

* Conversione di un modulo PDF in un modulo adattivo utilizzando [!DNL Automated Forms Conversion service].

#### Supporto per i gruppi di disponibilità Microsoft SQL Server 2016 Always On per l&#39;alta disponibilità (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] ora supporta [!DNL Microsoft] Gruppi di disponibilità Always On di SQL Server 2016 per le distribuzioni OSGi ad alta disponibilità.

#### Configurazione del client HTTP del modello dati modulo per ottimizzare le prestazioni (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] modello di dati modulo per l’integrazione con i servizi web RESTful come origine dati ora include configurazioni client HTTP per l’ottimizzazione delle prestazioni. Vedi [Configurare origini dati](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilità dell’opzione Ripristina per ciascun componente in modalità Layout (6.5.7.0) {#reset-option-layout-mode}

È ora possibile utilizzare l’opzione di reimpostazione per ogni componente in modalità Layout di un modulo adattivo. Quando definisci un layout a più colonne per un pannello, puoi utilizzare questa funzione per reimpostare i singoli componenti all’interno del pannello. Vedi [Utilizzare la modalità di layout per ridimensionare i componenti](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Precompila un modulo adattivo sul client (6.5.6.0) {#prefill-merge-data-at-client}

Quando si precompila un modulo adattivo, la funzione [!DNL Experience Manager Forms] il server unisce i dati con un modulo adattivo e invia il modulo compilato all’utente. Per impostazione predefinita, l’azione di unione dati viene eseguita sul server.
Ora puoi configurare le [!DNL Experience Manager Forms] server a [eseguire l&#39;azione di unione dati sul client](../../help/forms/using/prepopulate-adaptive-form-fields.md) invece del server. Riduce notevolmente il tempo necessario per precompilare ed eseguire il rendering dei moduli adattivi.

#### Integrazione del modello dati del modulo con API RESTful su un server con implementazione SSL bidirezionale (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] il modello dati del modulo può ora [integrare con le API RESTful su un server in cui è implementato un SSL bidirezionale](../../help/forms/using/configure-data-sources.md).

#### È stato aggiunto il supporto per [!DNL Adobe Sign] Tag testo nel servizio Automated forms conversion (6.5.6.0) {#sign-integration-acroform-afcs}

Se un AcroForm include [!DNL Adobe Sign] Tag testo, questi campi vengono ora riconosciuti e rappresentati come [!DNL Adobe Sign] campi nel modulo adattivo convertiti utilizzando [!DNL Automated Forms Conversion service]. Un firmatario può compilare tali campi durante la firma del modulo adattivo.

#### Supporto per la conversione di PDF forms colorati in moduli adattivi (6.5.6.0) {#colored-PDF-forms}

È possibile utilizzare [!DNL Automated Forms Conversion service] per convertire PDF forms colorati in moduli adattivi.

#### Supporto per i protocolli SMB 2 e SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] ora supporta i protocolli SMB 2 e SMB 3.

#### Memorizzazione in cache migliorata per le pagine dei moduli adattivi tradotte (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

È ora possibile specificare [impostazioni internazionali come selettore nell’URL del modulo adattivo anziché come argomento nell’URL del modulo adattivo](../../help/forms/using/supporting-new-language-localization.md). Aiuta a memorizzare nella cache i moduli adattivi convertiti su [!DNL Experience Manager Dispatcher]. La memorizzazione nella cache dei moduli adattivi convertiti non era possibile nelle versioni precedenti. Per informazioni dettagliate sulla configurazione della memorizzazione in cache per l’utilizzo delle impostazioni internazionali come selettore nell’URL del modulo adattivo, consulta [Configurare la cache dei moduli adattivi nel dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Salvare l’output del servizio del modello dati modulo su una variabile (6.5.6.0) {#save-fdm-service-to-variable}

Il modello dati modulo consente di salvare l’output di un servizio del modello dati modulo su una variabile. [!DNL Experience Manager Forms] ora mappa automaticamente il tipo di servizio del modello dati del modulo al tipo di variabile.

#### Allegare più file per il componente File allegato (6.5.6.0) {#attach-multiple-files}

Ora puoi [allegare più file](../../help/forms/using/introduction-forms-authoring.md) al [!UICONTROL File allegato] componente dei moduli adattivi.

#### Personalizzare le colonne della Casella in entrata Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Puoi personalizzare un [!DNL Experience Manager] Casella in entrata: consente di modificare il titolo predefinito di una colonna, riordinare la posizione di una colonna e visualizzare colonne aggiuntive in base ai dati di un flusso di lavoro. Membri `administrators` o `workflow-administrators` gruppo può personalizzare le colonne. Per ulteriori informazioni, consulta [Controllo amministratore](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizzare le colonne della casella in entrata di Experience Manager](assets/customize-columns.gif)

#### Possibilità di salvare le comunicazioni interattive come bozza (6.5.5.0) {#save-as-draft}

Puoi utilizzare l’interfaccia utente dell’agente per salvare una o più bozze per ogni comunicazione interattiva e recuperare la bozza in un secondo momento per continuare a lavorarci. Potete specificare un nome diverso per ogni bozza da identificare. Per ulteriori informazioni, consulta [Salvare le comunicazioni interattive come bozza](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Salva come bozza](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] supporto di application server (6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms ha aggiunto il supporto per [!DNL Oracle WebLogic 12] per Adobe Experience Manager Forms su JEE. Puoi eseguire l’aggiornamento da una versione precedente o impostare un nuovo Forms Experience Manager 6.5 sul server JEE su [!DNL Oracle WebLogic] 12.2.1.4 e versioni successive. Successivamente corrisponde alle modifiche minori, dove x in 12.2.1.x viene sostituito con un numero di versione.

#### Miglioramenti all’accessibilità (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms include i seguenti miglioramenti all’accessibilità:

* Quando un utente visualizza in anteprima un modulo adattivo come modulo HTML, la funzione [!UICONTROL Firma scarabocchio] mantiene lo stato attivo.

* I messaggi di errore visualizzati all’invio di un modulo adattivo ora contengono `aria-describedBy` attributo. L’attributo è associato ai campi indicati nel messaggio di errore. La `aria-describedby` attribute indica gli ID degli elementi che descrivono l’oggetto. Aiuta a stabilire una relazione tra widget o gruppi e testo che li ha descritti.

* Se un modulo adattivo contiene alcuni campi obbligatori, l’attributo obbligatorio è impostato su `True` per tali campi nello schema di accessibilità ARIA.

#### Autenticazione basata su certificato X-509 per i servizi web basati su SOAP nel modello per dati modulo (6.5.5.0) {#x509-based-authentication-soap}

Il modello dati modulo supporta ora l’autenticazione basata su certificato X-509 durante l’utilizzo dei servizi web SOAP come origine dati. Per ulteriori informazioni, consulta [Configurare i servizi Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Altri miglioramenti chiave (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms su JEE Document Security è ora basato su [!DNL Apache Struts 2].

* È stato aggiunto il supporto per [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Genera output stampabile nei flussi di lavoro Experience Manager Forms (6.5.4.0) {#generate-printable-output}

Il passaggio del flusso di lavoro Genera output stampabile consente di integrare un file modello di origine con un file di dati. Questa integrazione consente di stampare o salvare copie diverse del file modello. Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL. Per ulteriori informazioni su questa funzione, consulta [Flusso di lavoro incentrato su Forms su OSGi - Riferimento dettagliato](../forms/using/aem-forms-workflow-step-reference.md).

![Genera output stampabile](assets/generate-print-output-step.gif)

#### Supporto a più colonne per moduli adattivi e comunicazioni interattive in modalità Layout (6.5.4.0) {#multi-column-adaptive-forms}

È ora possibile definire il numero di colonne per un pannello nei moduli adattivi e nelle comunicazioni interattive. Passa alla modalità di layout per utilizzare la nuova opzione a più colonne. Per ulteriori informazioni, consulta [Utilizzare la modalità Layout per ridimensionare i componenti](../forms/using/resize-using-layout-mode.md).

![Layout a più colonne](assets/multi-column-layout.gif)

#### Personalizzazioni della casella in entrata Experience Manager (6.5.4.0) {#aem-inbox}

La nuova opzione Controllo amministratore consente agli amministratori di:

* Personalizza il testo dell’intestazione e il logo.

* Controlla la visualizzazione dei collegamenti di navigazione disponibili nell’intestazione.

L’opzione Controllo amministratore è visibile solo ai membri del gruppo `administrators` o `workflow-administrators` gruppo. Per ulteriori informazioni su questa funzione, consulta [Casella in entrata](../sites-authoring/inbox.md).

#### Supporto del testo RTF in HTML5 forms (6.5.4.0) {#rich-text-support}

Convertire un campo di testo in un modulo XFA in un campo di testo RTF in un modulo HTML5. Per ulteriori informazioni, consulta [Progettazione di modelli di modulo per i moduli HTML5](../forms/using/designing-form-template.md).

#### Miglioramenti all’accessibilità (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms include i seguenti miglioramenti all’accessibilità:

* Gli assistenti vocali annunciano correttamente in un modulo adattivo caselle di controllo, collegamenti, selettore data e campi di immissione data .

* Ogni pagina di un modulo adattivo ora include un titolo e un’etichetta di riferimento principale.

#### Condividere e richiedere l’accesso agli elementi in entrata di un utente Experience Manager Forms (6.5.3.0) {#share-request-access}

È possibile condividere gli elementi della casella in entrata con un altro utente. Una volta che un altro utente ottiene l&#39;accesso agli elementi della casella in entrata, può richiedere e intraprendere le azioni appropriate sugli elementi condivisi. Allo stesso modo, puoi richiedere l’accesso agli elementi della casella in entrata ad altri utenti. Vedi [Condividere e richiedere l’accesso agli elementi della casella in entrata di un utente](../forms/using/configure-shared-queues-osgi.md).

#### Configurare le impostazioni predefinite per gli elementi in entrata di un utente Experience Manager Forms (6.5.3.0) {#configure-out-of-office}

Se si prevede di uscire dall&#39;ufficio, è possibile specificare cosa accade agli articoli che vi vengono assegnati per quel periodo.
Puoi specificare una data e un’ora di inizio e una data e un’ora di fine per rendere effettive le impostazioni fuori sede. Puoi impostare una persona predefinita a cui vengono inviati tutti gli elementi. Vedi [Configurare le impostazioni di Fuori sede](../forms/using/configure-out-of-office-settings.md).

#### Generare più comunicazioni interattive utilizzando l’API Batch per Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Puoi utilizzare l’API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L’API Batch combina i dati con un modello per produrre una comunicazione interattiva. L&#39;API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto della carta di credito per più clienti. Vedi [Generare più comunicazioni interattive utilizzando l’API Batch](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versioni principali dal [!DNL Adobe Experience Manager] 6.5 SP9 {#key-releases-since-last-sp}

Tra il 27 maggio 2021 e il 26 agosto 2021, Adobe ha rilasciato quanto segue, oltre ai Service Pack:

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.6.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-6-0.html), [2021.7.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-7-0.html)e [2021.8.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

* [[!DNL Experience Manager] app desktop 2.1 (2.1.3.3)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experienci Manager Screens: Feature Pack 202105](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202105.html)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Note generali sulla versione di disponibilità [!DNL Experience Manager] 6,5](release-notes.md)
>* [Note sulla versione del Service Pack per [!DNL Experience Manager] 6,5](sp-release-notes.md)

