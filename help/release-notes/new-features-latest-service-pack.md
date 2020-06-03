---
title: Novità in Adobe Experience Manager 6.5 Service Pack 5
description: Novità in Adobe Experience Manager 6.5 Service Pack 5
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 4%

---


# Novità in AEM 6.5 Service Pack 5 {#aem-whats-new-service-pack-5}

I service pack di Adobe Experience Manager 6.5 offrono nuove funzioni, miglioramenti richiesti dai clienti, prestazioni e miglioramenti relativi alla stabilità a intervalli trimestrali. Il modello di consegna trimestrale semplifica l&#39;accesso e l&#39;adozione di nuove caratteristiche e innovazioni.

In questo articolo vengono evidenziate le funzioni incluse nell&#39;ultimo Service Pack 6.5, le funzioni [chiave incluse nei Service Pack](#key-features-previous-service-packs)6.5 precedenti e alcune delle release [chiave dalla release di Experience Manager 6.5.4.0](#key-features-sice-sp3) .

## AEM Sites {#aem-sites}

### Miglioramenti all&#39;accessibilità {#accessibility-sites}

* È stata migliorata la generazione di rapporti sugli errori mediante l’aggiunta di informazioni sul testo

* È stata migliorata l&#39;interfaccia utente attiva durante la navigazione da tastiera

* Contrasto del testo migliorato (rapporto di luminosità)

* Miglioramento della coerenza degli attributi alt per le immagini di pagina

* Miglioramento della coerenza delle etichette delle applicazioni Rich Internet (ARIA) accessibili

* Funzionalità non visive Desktop Access (NVDA) migliorate

* Supporto migliorato per gli assistenti vocali

### Altri miglioramenti chiave {#other-enhancements-sites}

* Quando si copia o incolla una struttura ad albero di pagina, è ora possibile incollare la pagina principale o incollare la pagina principale con le relative sottopagine.

* AEM Experience Fragments exported to Adobe Target workspaces now appear as unique offer types and offer sources in [!DNL Target].

* Multi Site Manager - L&#39;attivazione della pubblicazione ora elimina correttamente un componente dalla pagina pubblicata se un componente viene eliminato dalla pagina di origine.

* Multi Site Manager - Se il nome di un componente locale in LiveCopy è identico al nome di un componente nel blueprint e il componente viene implementato dal blueprint, il termine _msm_move viene ora aggiunto correttamente al nome del componente locale.

## AEM Assets {#aem-assets}

### Miglioramenti dell’accessibilità in Risorse {#assets-accessibility}

[!DNL Adobe Experience Manager] Le funzionalità delle risorse ora sono più accessibili in conformità alle linee guida WCAG (Web Content Accessibility Guidelines). L&#39;accessibilità è stata migliorata nelle seguenti aree:

* Gli elementi dell&#39;interfaccia utente, i controlli, le pagine e le finestre di dialogo sono intuitivi per gli assistenti vocali.

* Gli elementi dell&#39;interfaccia utente, i controlli e i campi dei moduli di input sono accessibili tramite tastiera.

* Modifica del colore e del contrasto di alcuni elementi grafici per essere distinguibili dagli utenti con visione limitata e senza percezione del colore. Ad esempio, il colore delle icone di valutazione a stella (ad esempio nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] in [!UICONTROL Proprietà] risorsa o nella vista a schede) viene modificato per il contrasto appropriato.

![colore delle icone di valutazione a stella modificate per migliorare il contrasto](assets/star-rating-icons.png)

### Gestione delle eccezioni migliorata {#exception-handling}

Il flusso dell’interfaccia utente Assets offre una migliore gestione delle eccezioni. Precedentemente, se una risorsa non aveva il tipo appropriato per la sua dimensione, veniva rilevata un’eccezione catturata in modo invisibile, senza traccia nei registri. Questo comportamento è cambiato e tutte le eccezioni sono rilevate nei registri.

## [!DNL Dynamic Media] {#dynamic-media}

### Supporto 3D in [!DNL Dynamic Media] {#support-for-3d}

Il supporto 3D in [!DNL Dynamic Media] ora consente ai clienti di pubblicare e aggiungere contenuto 3D a pagine Web e applicazioni. Include:

* Pubblicazione di formati di risorse 3D comuni per generare un URL di risorsa.

* Visualizzazione interattiva delle risorse 3D pubblicate tramite un nuovo visualizzatore Web 3D disponibile nella libreria del [!DNL Dynamic Media] visualizzatore, basato su Adobe Dimension.

* Pubblicazione e visualizzazione in 3D sulla [!DNL Experience Manager Sites] pagina mediante il componente [!DNL Sites] WCM.

## AEM Forms {#aem-forms}

### Personalizzare le colonne Inbox di AEM {#customize-aem-inbox-columns}

Potete personalizzare una Casella in entrata AEM per modificare il titolo predefinito di una colonna, riordinare la posizione di una colonna e visualizzare ulteriori colonne in base ai dati di un flusso di lavoro. È membro `administrators` o `workflow-administrators` gruppo per personalizzare le colonne.

![Personalizzare le colonne Inbox di AEM](assets/customize-columns.gif)

### Salva le comunicazioni interattive come bozza {#save-as-draft}

È possibile utilizzare l&#39;interfaccia utente agente per salvare una o più bozze per ogni comunicazione interattiva e recuperare la bozza in un secondo momento per continuare a lavorarci. È possibile specificare un nome diverso per ciascuna bozza per facilitarne l&#39;identificazione.

![Salva come bozza](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] supporto del server applicazioni {#weblogic-support}

AEM Forms ha aggiunto il supporto per AEM Forms su JEE. [!DNL Oracle WebLogic 12] È possibile effettuare l’aggiornamento da una versione precedente o impostare un nuovo AEM 6.5 Forms sul server JEE sulla versione [!DNL Oracle WebLogic] 12.2.1.4 e versioni successive. Successivamente corrisponde alle modifiche minori, dove x in 12.2.1.x viene sostituito con un numero di versione.

### Miglioramenti all&#39;accessibilità {#accessibility-improvements}

AEM Forms include i seguenti miglioramenti a livello di accessibilità:

* Quando un utente visualizza l&#39;anteprima di un modulo adattivo come modulo HTML, il campo Firma  scarabocchio mantiene lo stato attivo.

* I messaggi di errore visualizzati durante l&#39;invio di un modulo adattivo ora contengono l&#39; `aria-describedBy` attributo. L&#39;attributo è associato ai campi indicati nel messaggio di errore. L&#39; `aria-describedby` attributo indica gli ID degli elementi che descrivono l&#39;oggetto. Consente di stabilire una relazione tra widget o gruppi e testo che li descrive.

* Se in un modulo adattivo sono presenti alcuni campi obbligatori, l&#39;attributo obbligatorio è impostato `True` per tali campi nello schema di accessibilità ARIA.

### Autenticazione basata su certificato X-509 per i servizi Web basati su SOAP nel modello dati del modulo {#x509-based-authentication-soap}

Il modello di dati del modulo ora supporta l&#39;autenticazione basata sui certificati X-509 quando si utilizzano i servizi Web SOAP come origine dati.

### Altri miglioramenti chiave {#other-improvements}

* AEM 6.5 Forms su JEE Document Security ora è basato su [!DNL Apache Struts 2].

* È stato aggiunto il supporto per [!DNL Oracle Real Applications Cluster (RAC) 19c].

## Funzioni principali nei precedenti Service Pack di AEM 6.5 {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### Miglioramenti di Style System (6.5.4.0) {#style-system-enhancements}

È ora possibile selezionare gli stili nella finestra di dialogo del componente utilizzando il sistema di stile avanzato.

#### Miglioramenti delle prestazioni in varie aree (6.5.4.0) {#performance-improvements}

* È stato ridotto il tempo necessario per caricare e inizializzare ContextHub in un sito (`contexthub.kernel.js`). Ne risulta un caricamento più rapido delle pagine durante una visita del sito.

* È stato ridotto il tempo necessario per aggiornare una pagina dopo aver trascinato i frammenti esperienza nell’Editor pagina Siti.

* È stato ridotto il tempo di caricamento delle voci in una pagina Siti con più di 200 copie dal vivo in Panoramica **** Live Copy.

* Gestione migliorata degli URL incompleti o non validi. Tali URL possono rallentare l’Editor modelli.

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

Il canale di autorizzazione tra Risorse AEM e Portale marchio viene modificato. Precedentemente, Brand Portal era stato configurato nell’interfaccia classica tramite il gateway OAuth legacy, che utilizza lo scambio di token JWT per ottenere un token di accesso IMS per l’autorizzazione. AEM Assets è ora configurato con Brand Portal tramite Adobe I/O, che fornisce un token IMS per l&#39;autorizzazione del tenant del Brand Portal.

I passaggi per configurare Risorse AEM con Portale marchio variano a seconda della versione di AEM in uso e se si sta configurando per la prima volta o si stanno aggiornando le configurazioni esistenti. Per informazioni dettagliate, consultate [Configurare AEM Assets con il Portale](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) marchio.

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

Experience Manager Assets include i seguenti miglioramenti a livello di accessibilità:

* I tasti freccia sulla tastiera possono essere utilizzati per spostare e scorrere le aree all&#39;interno delle immagini ingrandite. Per ulteriori informazioni, consultate [Anteprima delle risorse solo](../assets/managing-assets-touch-ui.md#previewing-assets)con i tasti di scelta rapida.

* Le caselle di controllo dello stato misto (in cui, a meno che non si selezionino tutti i predicati nidificati, le caselle di controllo di primo livello non vengono selezionate e vengono evidenziate) nel pannello Filtri sono leggibili dagli assistenti vocali.

* Le limitazioni relative al formato di data e ora sono fornite nelle etichette dei campi data, per consentire agli utenti di immettere la data nel formato corretto utilizzando la tastiera.

   Esempio, `On Time (MM-DD-YYYY HH:mm)`. Qui MM è mese in formato a due cifre, AAAA è anno, GG è giorno in formato a due cifre, HH è ora in formato militare a 24 ore e mm è minuto.

* Il `X` simbolo sul pulsante per rimuovere i tag attualmente selezionati viene ora annunciato dagli assistenti vocali insieme al numero di tag selezionati.

#### Ricerca visiva di Risorse AEM (6.5.2.0) {#visual-search}

Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. Dall’archivio DAM, AEM visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Immagini intelligenti per contenuti multimediali dinamici {#smart-imaging}

Le immagini intelligenti utilizzano le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento. La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser. Consultate [Smart Imaging](../assets/imaging-faq.md).

#### Ritaglio avanzato nei profili video per contenuti multimediali dinamici (6.5.3.0) {#smart-crop-video}

La funzione di ritaglio avanzato per i video, una funzione opzionale disponibile nei profili video, è uno strumento che utilizza l&#39;intelligenza artificiale di Adobe Sensei per rilevare e ritagliare automaticamente il punto focale in qualsiasi video adattivo o progressivo caricato, indipendentemente dalle dimensioni. Consultate [Utilizzo del ritaglio avanzato nei profili](../assets/video-profiles.md)video.

### AEM Forms {#aem-forms-previous-service-packs}

#### Genera output stampabile nei flussi di lavoro AEM Forms (6.5.4.0) {#generate-printable-output}

Il passaggio del flusso di lavoro Genera output stampabile consente di integrare un file modello sorgente con un file di dati. Questa integrazione consente di stampare o salvare copie diverse del file modello. Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL. Per ulteriori informazioni su questa funzione, vedere [Flusso di lavoro incentrato sui moduli in OSGi - Riferimento](../forms/using/aem-forms-workflow-step-reference.md)passo.

![Genera output stampabile](assets/generate-print-output-step.gif)

#### Supporto di più colonne per moduli adattivi e comunicazioni interattive in modalità Layout (6.5.4.0) {#multi-column-adaptive-forms}

È ora possibile definire il numero di colonne per un pannello nei moduli adattivi e nelle comunicazioni interattive. Passate alla modalità di layout per utilizzare la nuova opzione a più colonne. Per ulteriori informazioni, vedere [Uso della modalità Layout per ridimensionare i componenti](../forms/using/resize-using-layout-mode.md).

![Layout a più colonne](assets/multi-column-layout.gif)

#### Personalizzazioni della inbox AEM (6.5.4.0) {#aem-inbox}

La nuova opzione Controllo amministratore consente agli amministratori di:

* Personalizzare il testo dell’intestazione e il logo

* Controllare la visualizzazione dei collegamenti di navigazione disponibili nell&#39;intestazione

L’opzione Controllo amministratore è visibile solo ai membri del gruppo Amministratori o Amministratori di workflow. Per ulteriori informazioni su questa funzione, vedere [Casella in entrata](../sites-authoring/inbox.md).

#### Supporto di testo RTF nei moduli HTML5 (6.5.4.0) {#rich-text-support}

Convertire un campo di testo in un modulo XFA in un campo di testo RTF in un modulo HTML5. Per ulteriori informazioni, vedere [Progettazione di modelli di modulo per moduli](../forms/using/designing-form-template.md)HTML5.

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms include i seguenti miglioramenti a livello di accessibilità:

* Gli assistenti vocali annunciano le caselle di controllo, i collegamenti, il selettore data e i campi di immissione data correttamente in un modulo adattivo.

* Ogni pagina di un modulo adattivo ora include un titolo e un’etichetta con il punto di riferimento principale.

#### Condivisione e richiesta dell&#39;accesso agli elementi in entrata di un utente AEM Forms (6.5.3.0) {#share-request-access}

È possibile condividere gli elementi Inbox con un altro utente. Quando un altro utente accede agli elementi della Casella in entrata, può richiedere e intervenire sugli elementi condivisi. Allo stesso modo, potete richiedere l’accesso agli elementi della casella in entrata ad altri utenti. Consultate [Condividere e richiedere l’accesso agli elementi in entrata di un utente](../forms/using/configure-shared-queues-osgi.md).

#### Configurare le impostazioni predefinite per gli elementi in entrata di un utente AEM Forms (6.5.3.0) {#configure-out-of-office}

Se prevedete di uscire dall&#39;ufficio, potete specificare cosa accade agli elementi assegnati a quel periodo.
È possibile specificare una data e un&#39;ora di inizio e una data e un&#39;ora di fine affinché le impostazioni fuori sede siano attive. Potete impostare una persona predefinita a cui vengono inviati tutti gli elementi. Consultate [Configurare le impostazioni](../forms/using/configure-out-of-office-settings.md)Fuori sede.

#### Generazione di più comunicazioni interattive mediante l&#39;API Batch per AEM Forms (6.5.3.0) {#generate-multiple-ic}

Potete utilizzare l&#39;API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L&#39;API Batch combina i dati con un modello per produrre una comunicazione interattiva. L&#39;API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto della carta di credito per più clienti. Consultate [Generare più comunicazioni interattive utilizzando l&#39;API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

## Versioni principali da AEM 6.5 SP4 {#key-releases-since-last-sp}

Tra il 5 marzo 2020 e il 4 giugno 2020, Adobe ha rilasciato le seguenti funzionalità che non rientrano nel risultato finale di AEM:

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)e [2020.5.0](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* [Risorse AEM: Desktop App 2.0.2.0](https://docs.adobe.com/content/help/it-IT/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens: Feature Pack 202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## Risorse utili

* [Guide utente di AEM 6.5](../user-guide/home.md)

* [Note generali sulla versione per Adobe Experience Manager 6.5](release-notes.md)

* [Note sulla versione di Service Pack per Adobe Experience Manager 6.5](sp-release-notes.md)
