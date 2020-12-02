---
title: '[!DNL Adobe Experience Manager] 6.5 Note sulla versione del Service Pack precedente.'
description: Note sulla versione per i Service Pack  [!DNL Adobe Experience Manager] 6.5.
contentOwner: AK
translation-type: tm+mt
source-git-commit: 22112319b31576d542d04bdc3519795b02db356c
workflow-type: tm+mt
source-wordcount: '14804'
ht-degree: 20%

---


# Hotfix e Feature Pack inclusi nei Service Pack precedenti {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.6.0  {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0 è un aggiornamento importante che include nuove funzioni, miglioramenti fondamentali richiesti dai clienti, nonché miglioramenti a prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 rilasciata a partire da **aprile 2019**. Può essere installato sulla parte superiore di Adobe Experience Manager 6.5.

Le funzioni chiave e i miglioramenti introdotti in Adobe Experience Manager 6.5.6.0 includono:

* Pubblicare o annullare la pubblicazione delle risorse in modo selettivo su [!DNL Experience Manager] o [!DNL Dynamic Media] utilizzando la procedura guidata [!UICONTROL Pubblicazione rapida] o [!UICONTROL Gestisci pubblicazione].

* Utilizzate l&#39;interfaccia utente [!DNL Dynamic Media] per annullare la validità del contenuto nella cache CDN (Content Delivery Network).

* La pubblicazione delle cartelle contributi risorse da Brand Portal a  risorse Experienci Manager ora è supportata anche tramite il server proxy.

* I gruppi di cartelle private generati automaticamente vengono ora ripuliti al momento dell&#39;eliminazione della cartella privata in [!DNL Experience Manager Assets].

* Le descrizioni dei modificatori nell&#39;editor [!UICONTROL Viewer] predefinito video sono state aggiornate in [!DNL Dynamic Media].

* Viene fornita una nuova impostazione aziendale per riflettere lo stato del connettore [!DNL Dynamic Media].

* Le opzioni predefinite per `test` e `aiprocess` vengono aggiornate su `Thumbnail`, da `Rasterize` in precedenza in Contenuti multimediali dinamici, per garantire che gli utenti debbano creare solo una miniatura e ignorare l&#39;estrazione della pagina e l&#39;estrazione delle parole chiave.

* [Precompilare un modulo adattivo presso il client](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [Integrazione del modello dati del modulo con le API RESTful su un server con implementazione](../../help/forms/using/configure-data-sources.md) SSL bidirezionale.

* [È stata migliorata la memorizzazione nella cache per le pagine](../../help/forms/using/configure-adaptive-forms-cache.md) di moduli adattivi convertite.

* Supporto per [ tag di testo Adobe Sign nel servizio Automated forms conversion](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* Supporto per [convertire moduli colorati in moduli adattivi](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) utilizzando [!DNL Automated Forms Conversion service].

* Supporto per i protocolli SMB 2 e SMB 3.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.4.

Per un elenco completo delle funzioni e dei miglioramenti introdotti  Experience Manager 6.5.6.0, vedere [Novità in Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md).

Di seguito è riportato l&#39;elenco delle correzioni fornite nella release [!DNL Experience Manager] 6.5.6.0.

### [!DNL Sites] {#sites-6560}

* In [!DNL Sites] o [!DNL Screens], selezionare un progetto e fare clic su [!UICONTROL Management Publications]. Gli utenti non possono avanzare nella procedura guidata [!UICONTROL Gestisci pubblicazione] a causa di errori nell&#39;interfaccia utente. In particolare, l&#39;opzione [!UICONTROL Pubblica] non funziona (NPR-34099).
* Dopo aver deselezionato le opzioni [!UICONTROL Annulla ereditarietà] o [!UICONTROL Disattiva ereditarietà] (NPR-34097), la posizione di iParsys (sistema paragrafo ereditato) non viene ripristinata alla posizione predefinita originale.
* Se `RolloutConfigManagerFactoryImpl` non è in grado di caricare una configurazione di rollout, non tenta di caricare le configurazioni mancanti. Restituisce le configurazioni memorizzate nella cache (NPR-34092).
* Nel componente di base Testo, dopo aver utilizzato l&#39;opzione di modifica HTML di origine, la classe dal tag `em` viene rimossa (NPR-34081).
* Dopo l&#39;aggiornamento  Experience Manager 6.3.3 a  Experience Manager 6.5.3, il processo di implementazione richiede molto più tempo e il rollout non riesce con un errore di timeout (NPR-34049).
* La `htmlwriter` non codifica i valori degli attributi. La marcatura presente nella marcatura XF viene esportata con valori attributo decodificati (ovvero `"` anziché `&#34`). Causa problemi sul lato Target con Visual Experience Composer (Compositore esperienza visivo) che utilizza il file XF esportato (NPR-34048).
* Quando si spostano le pagine in [!DNL Experience Manager Sites], è necessario migliorare la registrazione per acquisire l&#39;errore di creazione della versione con un motivo (NPR-34014).
* In [!DNL Rich Text Editor] se viene rimosso tutto il testo, viene rimosso anche il tag paragrafo (NPR-33976).
* Quando la pagina `siteadmin` (nell&#39;interfaccia classica) viene aperta o aggiornata, le opzioni nel menu `New` sono disattivate (NPR-33949).

   ![Screenshot per illustrare il problema dei menu mancanti nell’interfaccia classica](assets/33949_missing_menu.png)

* Non è possibile utilizzare un elemento [!DNL Content Fragment] come `TemplatedResource` poiché non funziona in `ContentFragmentUsePojo` (NPR-33911).
* Le operazioni di spostamento sincrone e asincrone possono causare errori a causa di trasferimenti simultanei. Le operazioni di spostamento delle pagine sono limitate allo spostamento sincrono. Consente lo spostamento simultaneo di pagine (NPR-33875).
* [!UICONTROL L&#39;operazione Gestisci ] pubblicazione per replicare il contenuto dall&#39;istanza Author a Publish non riesce e genera un errore JavaScript (NPR-33872).
* Quando per creare versioni sono selezionate più pagine o risorse, la nuova versione viene creata solo per l’ultima pagina o risorsa selezionata (NPR-33866).
* Spostate una pagina di blueprint con copie in tempo reale in un’altra cartella. Quando si sposta nella cartella originale, l&#39;operazione di spostamento non riesce senza errori (NPR-33864).
* Quando si utilizza l&#39;azione Sposta per rinominare una pagina Web nella console [!DNL Sites], all&#39;ultimo passaggio della procedura guidata vengono visualizzate due finestre di dialogo sovrapposte (NPR-33831).

   ![Screenshot per illustrare il problema NPR-33831 della sovrapposizione della finestra di dialogo di spostamento](assets/33831_rename_dialog.png)

* Le proprietà `cq:acLinks` e `cq:acUUID` della copia [!DNL Adobe Campaign] vengono rimosse durante l&#39;operazione di copia e incolla (NPR-33794).
* Quando si tenta di eseguire il rollout su una pagina figlia di una Live Copy principale indipendente, [!DNL Experience Manager] genera un&#39;eccezione di puntatore null (NPR-33676).
* I componenti [!DNL RTE] in un Contenitore di layout non sono visibili quando il Contenitore di layout viene copiato e incollato nuovamente sulla pagina. I componenti [!DNL RTE] non sono modificabili ma vengono visualizzati all&#39;aggiornamento della pagina (NPR-33662).
* Quando si ridimensiona un componente di layout per diversi punti di interruzione (medio e grande), il layout non funziona come previsto (NPR-33608).
* In modalità di modifica in linea in [!DNL RTE], il trascinamento di un&#39;immagine non funziona per il componente Testo (NPR-33602).
* È possibile creare un componente in una pagina blueprint con lo stesso nome del nome della pagina. Durante il rollout, `_msm_moved` viene aggiunto il suffisso per rinominare il componente. Il componente viene spostato alla fine del [!UICONTROL Sistema paragrafo] (NPR-33535).
* Se offTime o onTime è impostato su molte pagine o risorse, il sistema richiede molte risorse e rallenta l&#39;avvio e l&#39;arresto (NPR-33482).
* Un utente con autorizzazioni CRUD su `/content/experience-fragment` non è in grado di eliminare una cartella (NPR-33436).
* Potete selezionare [!UICONTROL HTML &amp; JSON] come opzione per [!UICONTROL  formato di esportazione Adobe Target] in una cartella principale nella sezione [!DNL Experience Fragments]. Le stesse proprietà vengono visualizzate nell’interfaccia touch per le sottocartelle di questa cartella principale. Tuttavia, in CRXDE, per `cq:adobeTargetExportFormat` viene visualizzato solo HTML invece di visualizzare `html,json` (NPR-33423).
* La pubblicazione o l&#39;annullamento della pubblicazione da un Alias pagina non è supportata. Rimuovere l&#39;opzione che sembra presentare un&#39;altra richiesta (NPR-33415).
* Un tag specifico può essere spostato da una posizione all&#39;altra in [!DNL Experience Manager]. Può essere applicato anche a pagine diverse prima e dopo lo spostamento. Quando si modificano le proprietà delle pagine, il tag non viene visualizzato per la modifica anche se il tag è lo stesso (NPR-33353).
* Il rendering di un modello di pagina non viene eseguito correttamente quando un Contenitore di layout viene eliminato da un modello che contiene più contenitori di layout (NPR-33347).
* Nell&#39;editor modelli, provare a eliminare un modello utilizzato da più di 100000 pagine in `/content/`. Viene visualizzato un errore senza alcun messaggio di errore (NPR-33312).
* Il reindirizzamento a [!DNL Experience Manager] pagina con ancoraggio non funziona sull&#39;istanza Author come `PageRedirectServlets` inserisce una stringa di query dopo un frammento URL o un ancoraggio (NPR-34288).
* La creazione di un marchio in `/content/campaign` determina una struttura che non consente di creare campagne. [!UICONTROL Create ] Brandoption lascia il marchio appena creato senza la possibilità di creare  [!UICONTROL Offerte e ] Attività, in quanto non è disponibile l&#39;opzione   Createoption (NPR-34113).
* È possibile sospendere la [!DNL Live Copy] di una pagina e l&#39;ereditarietà viene interrotta come mostrato in modalità Editor. Nelle proprietà della pagina, l&#39;icona che rappresenta l&#39;ereditarietà indica erroneamente che l&#39;ereditarietà esiste e non è interrotta (NPR-34017).
* Le pagine con molti riferimenti non possono essere spostate in modo asincrono e talvolta l&#39;operazione di spostamento non riesce (CQ-4297969).
* Una pagina Web con il carattere `/` nell’URL non risponde durante la creazione. Quando un componente viene aggiunto durante l’authoring, l’utilizzo della CPU aumenta e il browser smette di rispondere (CQ-4295749).
* In modalità Sfoglia, NVDA non narra un valore selezionato dall&#39;opzione di menu Tipo/Dimensione. L&#39;elemento visivo non è attivo sull&#39;elemento selezionato. Gli utenti che si affidano a un assistente vocale non possono utilizzare la modalità Sfoglia (CQ-4294993).
* Quando si crea una pagina Web, gli utenti possono selezionare il modello [!UICONTROL Pagina contenuto]. Nella scheda [!UICONTROL Social Media], gli utenti possono selezionare una [!UICONTROL variante XF preferita]. Per selezionare un frammento esperienza in modalità di ricerca NVDA, gli utenti non possono utilizzare i tasti di scelta rapida (CQ-4292669).
* Aggiornamento della libreria handlebars alla versione più sicura v4.7.3 (NPR-34484).

### [!DNL Assets] {#assets-6560}

**Miglioramenti dell&#39;accessibilità in  risorse Experience Manager**

* Utilizzando i tasti di tastiera, gli utenti possono ora accedere alle opzioni dell&#39;interfaccia utente interattiva nell&#39;elenco [!UICONTROL Riferimenti] delle risorse (NPR-34115).

* L&#39;assistente vocale ora annuncia l&#39;azione prevista dei predicati nella pagina di ricerca (NPR-34104).

* La pagina di ricerca e i risultati della ricerca ora dispongono di titoli più informativi per una migliore comprensione degli utenti degli assistenti vocali (NPR-34093).

* Gli assistenti vocali annunciano ora le opzioni per eliminare i tag selezionati nella scheda [!UICONTROL Base] della risorsa [!UICONTROL Proprietà] (NPR-33972).

* Gli elementi di ciascuna riga nella vista a elenco vengono ora annunciati come elementi della stessa riga dagli assistenti vocali (NPR-33932).

* Lo stato attivo durante la navigazione con il tasto `Tab` ora si sposta sull&#39;opzione di chiusura nell&#39;anteprima della versione (NPR-33863).

* Lo stato attivo ora si sposta sull&#39;icona di ricerca dopo la chiusura di Omnisearch (NPR-33705).

* Le opzioni dell&#39;interfaccia utente attivabili ora sono più visibili e con maggior contrasto quando si naviga utilizzando i tasti della tastiera. Gli utenti della tastiera possono identificare le aree interessate (NPR-33542).

* La funzionalità di trascinamento mediante la tastiera ora funziona in [!UICONTROL Editor schema metadati] in modalità Sfoglia dell&#39;assistente vocale (CQ-4296326).

* Nella finestra di dialogo di condivisione dei collegamenti, quando si naviga in modalità Sfoglia, un assistente vocale,

   * Non narra le informazioni della tabella non appena la finestra di dialogo viene caricata.

   * È possibile accedere a tutti i suggerimenti automatici elencati.

   * Racconta i suggerimenti automatici visualizzati per [!UICONTROL Aggiungi indirizzo e-mail/Ricerca] (CQ-4294232).

* L&#39;utilizzo del tasto `Esc` per rimuovere le icone delle azioni rapide dalla vista a schede non rimuove più lo stato attivo dall&#39;ultimo elemento attivo (CQ-4293554).

* Per le opzioni interattive nell&#39;interfaccia utente, l&#39;assistente vocale ne annuncia lo scopo invece dei nomi letterali delle icone (CQ-4272943).

* Lo stato attivo della tastiera ora si sposta correttamente su [!UICONTROL Flyout], [!UICONTROL InlineZoom], [!UICONTROL Shoppable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL ZoomVertical_dark&lt;a1/> e [!UICONTROL Opzioni ZoomVertical_light] durante la navigazione mediante il tasto Tab della tastiera nei dettagli delle risorse [!UICONTROL Visualizzatori] in [!DNL Dynamic Media] (CQ-4290605).]

* [!UICONTROL È ora possibile accedere all&#39;opzione Salva e ] chiudi nella   pagina Proprietà risorsa tramite i tasti di scelta rapida (NPR-34107).

* I messaggi di errore a causa di combinazioni di nome utente e password errate nella pagina di login vengono ora annunciati dagli assistenti vocali ogni volta che si verifica l&#39;errore (NPR-33722).

* Nella sezione di intestazione [!DNL Experience Manager], quando si naviga in modalità Sfoglia, l&#39;assistente vocale ora annuncia,

   * Modificate automaticamente i suggerimenti in [!UICONTROL Digitare per effettuare ricerche] in Omnisearch.

   * Lo stato è espanso o compresso per le opzioni [!UICONTROL Solutions], [!UICONTROL Help], [!UICONTROL Inbox] e [!UICONTROL User].

   * Il messaggio di stato [!UICONTROL Guida di ricerca] visualizzato quando l&#39;utente immette una stringa di ricerca nel campo [!UICONTROL Cerca aiuto] in [!UICONTROL Guida].

   ![Menu Aiuto nell&#39;intestazione](assets/Help_aem_header.png)

   *Figura:  [!UICONTROL Cercare ] Help   Helpmenu.*

   * Il messaggio di errore se il valore errato viene immesso nel campo [!UICONTROL Impersona come] in [!UICONTROL Utente] e lo stato attivo si sposta correttamente nel campo di testo (NPR-33804).

   ![Menu utente nell’intestazione](assets/User_aem_header.png)

   *Figura:  [!UICONTROL Impersona ] un campo nel menu   Utente nell’intestazione.*

* L&#39;utente ora può cambiare lo stato attivo utilizzando la tastiera all&#39;interno di:

   * [!UICONTROL Cerca/aggiungi ] indirizzo e-mail nella finestra di dialogo  [!UICONTROL Condivisione ] collegamento.

   * [!UICONTROL Aggiungi utente o ] campo gruppo in  [!UICONTROL Gruppo utenti chiuso ] nella scheda   Autorizzazioni di  [!UICONTROL proprietà]  della cartella (NPR-34452).

**Problemi risolti in Risorse  Experience Manager**

[!DNL Adobe Experience Manager] 6.5.6.0  [!DNL Assets] risolve i seguenti problemi:

* Le annotazioni non sono evidenziate se selezionate dalla timeline della risorsa (CQ-4302422).

* L&#39;anteprima delle risorse collaterali di marketing (come Brochure, Volantino e Biglietto da visita) create utilizzando il modello [!DNL Adobe InDesign] non visualizza interruzioni di riga e interruzioni di paragrafo (NPR-34268).

* L&#39;estrazione del testo e quindi la ricerca full-text per i file PDF caricati non funziona (NPR-34164). Per risolvere il problema, riavviate la distribuzione [!DNL sAdobe Experience Manager] dopo l&#39;installazione di Service Pack 6.

* Nella timeline di risorse con più pagine vengono visualizzate le annotazioni applicate a tutte le risorse secondarie quando si sfoglia la risorsa nella visualizzazione Timeline, invece di visualizzare le annotazioni specifiche per le risorse secondarie specifiche (NPR-34100).

* Le cartelle delle risorse non vengono pubblicate utilizzando l&#39;opzione [!UICONTROL Gestisci pubblicazione] se le cartelle contengono risorse nei formati di file JavaScript, CSS o JSON (NPR-34090).

* Deselezionando o rimuovendo i tag o i filtri applicati in Omnisearch la query di ricerca viene eseguita più volte, con conseguente aumento del tempo di ricerca (NPR-34078).

* Nella vista a schede, quando un flusso di lavoro (su una risorsa in una cartella) è in corso o in sospeso, la pagina viene ricaricata finché il flusso di lavoro non viene completato o terminato. Pertanto, gli autori non possono lavorare sulle risorse nella cartella per la quale devono scorrere verso il basso (NPR-33986).

* Se l&#39;utente sposta una risorsa pubblicata in una nuova posizione, la risorsa viene ripubblicata anche se l&#39;opzione [!UICONTROL Ripubblica] è deselezionata. Questo porta a molte risorse orfane che si trovano nell’istanza di pubblicazione. Il comportamento predefinito, tuttavia, consiste nel fatto che l’operazione di spostamento su una risorsa pubblicata la annulla automaticamente; questa risorsa viene ripubblicata se l&#39;autore seleziona l&#39;opzione [!UICONTROL Ripubblica] quando sposta la risorsa (NPR-33934).

* La pagina [!UICONTROL Sposta risorse] per le risorse nelle raccolte non carica tutto il contenuto HTML, ad esempio l&#39;opzione [!UICONTROL Regola/Ripubblica]. Pertanto, gli utenti non possono completare l&#39;operazione di spostamento (NPR-33860).

* Se spostate una risorsa e aggiungete caratteri speciali nel nome e nel titolo delle risorse spostate, viene creata una cartella aggiuntiva (con lo stesso nome) nella nuova posizione della risorsa (NPR-33826).

* [!UICONTROL Il pulsante ] Scarica di una risorsa viene disattivato quando l&#39;opzione   E-mail è selezionata nella finestra di dialogo   Download (NPR-33730).

* L&#39;errore &quot;Request-URI too long&quot; viene rilevato durante l&#39;esecuzione di operazioni in massa sulle risorse, come la modifica in massa dei metadati (NPR-33723).

* Viene rilevato un errore JavaScript e gli utenti non possono selezionare o eliminare le scelte generate nel campo [!UICONTROL Dropdown] da [!UICONTROL Add through JSON path] nella funzionalità [!UICONTROL Folder Metadata Schema Form Editor], se il file JSON caricato ha spazio o caratteri speciali nel valore (NPR-33712).

* Le rappresentazioni statiche delle risorse non vengono aggiornate quando la risorsa viene aggiornata utilizzando l&#39;opzione [!UICONTROL Open] in [!DNL desktop app] o [!DNL Adobe Asset Link] e vengono sincronizzate di nuovo in [!DNL Adobe Experience Manager] (CQ-4296279).

* Nella vista a colonne, l&#39;operazione di spostamento su un set di risorse consente inoltre di spostare le risorse selezionate prima di utilizzare l&#39;opzione [!UICONTROL Filtro]. Tenere presente che l&#39;utilizzo dell&#39;opzione [!UICONTROL Filter] deseleziona la selezione precedente (NPR-34018).

* Le barre rovesciate vengono aggiunte prima dei caratteri speciali nei suggerimenti per la ricerca di risorse, che contengono caratteri speciali nel nome (NPR-33834).

* Durante la creazione di regole per l&#39;elenco a discesa in [!UICONTROL Schema metadati cartella Form], l&#39;utente non può selezionare valori dalla colonna [!UICONTROL Opzioni campo] (CQ-4297530).

* La copia in fase di esecuzione del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata quando si installa [!DNL Experience Manager] 6.5 Service Pack 5 o una versione precedente su [!DNL Experience Manager] 6.5 (NPR-34532). Per recuperare la copia in fase di esecuzione, sincronizzate la copia in fase di progettazione del modello di workflow con la copia in fase di esecuzione mediante l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

**Problemi risolti in Contenuti multimediali dinamici**

* Se l’utente definisce le impostazioni di codifica nelle modifiche dopo la creazione del profilo video, le impostazioni di ritaglio avanzato vengono rimosse dai profili video (CQ-4299177).

* Le risorse lampeggiano durante il caricamento della pagina quando l&#39;utente passa dalle opzioni della barra laterale (ad esempio, [!UICONTROL Panoramica], [!UICONTROL Timeline], [!UICONTROL Visualizzatori]) alla pagina dei dettagli delle risorse (NPR-34235).

* Durante il processo di rielaborazione vengono osservati i seguenti problemi:

   * ID processo mancante nell&#39;handle del processo restituito dal processo di rielaborazione.

   * Rielaborare il processo per i registri video solo il nome del file e non il percorso completo.

   * Il processo di rielaborazione non dispone dell&#39;opzione per impostare il tipo di risorsa come statico.

   * `ExcludeFromAVS` non è disponibile (CQ-4298401).

* La funzionalità Smart Crop non riesce con un errore quando il profilo immagine viene aggiunto a una cartella con più proporzioni (ad esempio, 11) (NPR-34082).

* Il flusso di lavoro delle risorse di aggiornamento DAM viene attivato quando l&#39;utente scorre verso il basso nella pagina [!UICONTROL Workflow Archive] in [!UICONTROL Workflow] nella scheda [!UICONTROL Tools] in [!DNL Adobe Experience Manager] configurata con Dynamic Media Scene7 (CQ-4299727).

* I simboli nella scheda [!UICONTROL Behavior] di [!UICONTROL Viewer Preset Editor] non sono localizzati (CQ-4299026).

* Se il visualizzatore è in modalità reattiva (CQ-4298293), la vista principale visualizza l&#39;immagine con un layout non corretto e non è disponibile nel visualizzatore.

* Le modifiche ai predefiniti per immagini in [!UICONTROL Adobe Experience Manager] non si sincronizzano con Scene7 Publishing System (CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* I collegamenti alle risorse dei prodotti non vengono modificati quando le risorse vengono spostate (NPR-34098).

### Platform {#platform-6560}

* Impossibile scaricare i registri utilizzando lo strumento Diagnosi in un&#39;istanza di Experience Manager  aggiornata (NPR-34336).
* L&#39;aggiornamento non riesce con un errore a causa delle dipendenze da una versione specifica del pacchetto di base `cq-wcm-api` (CQ-4300520).
* I valori predefiniti per le impostazioni **[!UICONTROL Timeout connessione]** e **[!UICONTROL Timeout socket]** per la configurazione Agente predefinito (pubblicazione) non sono specificati (NPR-33707).
* Gli aggiornamenti alla configurazione della mappatura in `/etc/map.publish` non si riflettono sulle pagine del sito (NPR-34015).
* [La ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) documentazione di riferimento API non include la documentazione per il  `com.day.cq.tagging` pacchetto (CQ-4295864).

### Interfaccia utente {#ui-6560}

* L&#39;interfaccia del browser di offload non visualizza tutti gli argomenti del processo (NPR-34308).
* L&#39;interfaccia [Configuration Browser](/help/sites-administering/configurations.md) non visualizza tutte le configurazioni (NPR-33644).
* Premendo il tasto `Esc` durante la ricerca di utenti da impersonare, la finestra di dialogo **[!UICONTROL Utente]** si chiude invece dell&#39;elenco di utenti (NPR-34084).

### Integrations (Integrazioni){#integrations-6560}

* Le attività con nomi lunghi non vengono sincronizzate con [!DNL Adobe Target] (NPR-34254).

* Quando si seleziona una proprietà durante la creazione di una nuova configurazione di avvio  Adobe, viene visualizzato il seguente messaggio di errore (NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### Progetti traduzione {#translation-6560}

* Un progetto di traduzione non viene creato se l&#39;elemento `authorizableID` dell&#39;utente include caratteri speciali (NPR-33828).

### Sling {#sling-6560}

* La funzione di verifica dello stato e di rilevamento dei pattern sono sovrapposte. Di conseguenza, il controllo dello stato viene rimosso dal prodotto (NPR-33928).

### WCM {#wcm-6560}

* Componenti di base - Quando si aggiunge un componente immagine di base a una pagina e si fa riferimento a un&#39;immagine, l&#39;operazione `Undo` non funziona (NPR-34516).

* Impossibile utilizzare l&#39;operazione Page Move (CQ-4303028).

### [!DNL Communities] {#communities-6560}

* La condivisione di un post sui social media mostra un&#39;opzione obsoleta Google+ (NPR-33877).

* Il membro della community non è in grado di modificare il modello di gruppo o altre impostazioni della funzione di gruppo (NPR-33530).

* I tag collegamento ipertestuale sulle immagini non vengono generati correttamente in un post del forum (NPR-33464).

* Gli errori di accessibilità sono identificati nella funzione Assegnazione community (NPR-33442).

* Gli utenti esistenti di un gruppo di community aggiunto tramite Admin Console vengono rimossi dall&#39;elenco di utenti in caso di modifiche nella console del gruppo di community (NPR-34315).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per  [!DNL Forms]. Vengono distribuite utilizzando un pacchetto aggiuntivo [!DNL Forms] separato. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per [!DNL Experience Manager Forms] su JEE. Per ulteriori informazioni, vedere [Installare  componente aggiuntivo AEM Forms](#install-aem-forms-add-on-package) e [Installare  AEM Forms su JEE](#install-aem-forms-jee-installer).

Dopo l&#39;installazione del pacchetto del componente aggiuntivo [!DNL Experience Manager Forms] 6.5.6.0:

* Arrestate l&#39;istanza [!DNL Experience Manager Forms].

* Eliminare i file `bcpkix-1.51`, `bcmail-1.51` e `bcprov-1.51` JAR dalla directory `crx-repository\launchpad\ext`.

* Elimina` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` proprietà dal file `sling.properties`.

* Riavviate l&#39;istanza [!DNL Experience Manager Forms].

**Moduli adattivi**

* In presenza di un frammento di modulo adattivo mancante, il rendering del modulo adattivo non riesce (NPR-34302).

* La descrizione del contenuto della Guida relativa a un campo modulo adattivo visualizza un tag HTML paragrafo (NPR-34116).

* Quando si seleziona la proprietà **[!UICONTROL Revoca sul server]**, il modulo adattivo non viene inviato (NPR-33876).

* L&#39;azione di invio **[!UICONTROL Invia all&#39;endpoint REST]** non funziona per un modulo adattivo (CQ-4299044).

* Accessibilità: Quando si tenta di inviare un modulo adattivo senza caricare un allegato per un campo obbligatorio, lo stato attivo non si sposta automaticamente sul campo allegato (CQ-4298065).

* Quando si aggiungono righe a una tabella di un modulo adattivo, le opzioni **[!UICONTROL Aggiungi all&#39;inizio]** e **[!UICONTROL Aggiungi al basso]** non visualizzano i risultati appropriati (CQ-4297511).

* Lo script [!UICONTROL Value Commit] viene attivato in modo non corretto, con conseguente perdita di dati in un modulo adattivo (CQ-4296874).

* Il selettore data non funziona correttamente per i moduli adattivi localizzati (NPR-34333).

* Se il nome del file contiene un carattere di sottolineatura o uno spazio, non è possibile allegare il file a un modulo adattivo (CQ-4301001).

* Quando un pannello ripetibile nidificato ha più occorrenze del relativo elemento padre, tutte le occorrenze di tale pannello ripetibile nidificato non vengono precompilate (NPR-33666).

* Nei moduli adattivi sono presenti alcuni risolutori di risorse aperti. Ciò comporta errori di invio. Il problema si verifica in modo intermittente (CQ-4299407).

* Quando si apre la configurazione del campo per la prima volta, l&#39;icona delle proprietà non viene visualizzata (CQ-4296284).

* Durante l&#39;invio di un modulo adattivo, gli utenti possono modificare i metadati di invio, ad esempio `afPath`, `afSubmissionTime` e `signers`. Per risolvere il problema, i valori dei metadati vengono rimossi dai dati di invio del modulo sul lato client. Gli utenti possono utilizzare l&#39;oggetto `FormSubmitInfo` per recuperare questi valori dal server (NPR-33654).

**Flusso di lavoro**

* Quando un approvatore di workflow carica un allegato, l&#39;allegato viene rinominato in `undefined` (NPR-33699).

* [!DNL Experience Manager] L&#39;operazione di eliminazione del flusso di lavoro non riesce e visualizza il seguente messaggio di errore (NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] dopo l&#39;invio di un modulo (NPR-34409), l&#39;app  [!DNL Windows] non risponde più.

* Quando installate AEM Service Pack, l&#39;elenco **Da fare** di elementi non viene visualizzato come collegamenti. Il testo per gli elementi **Da fare** include tag HTML (NPR-34317).

**Comunicazione interattiva**

* Se si include un frammento di documento di testo con componenti ripetibili nidificati, la comunicazione interattiva non riesce a salvare (NPR-34095).

**Gestione della corrispondenza**

* Quando si modifica un frammento di documento di testo che include i valori del dizionario dati, l&#39;interfaccia utente dell&#39;agente non risponde più (NPR-33930).

* Copiare il contenuto da un documento [!DNL Microsoft Word] a un frammento di documento di testo in una lettera provoca problemi di formattazione (NPR-33536).

**Servizi basati su documenti**

* Quando si genera un file PDF da un file XDP utilizzando i servizi Output e Forms, il testo risulta mancante e sovrapposto (NPR-34237, CQ-4299331).

* Quando convertite un file HTML in PDF, l&#39;attributo `MaxReuseCount` non è configurabile (NPR-33470).

* Quando scaricate un file PDF che include funzioni interattive Estensioni di Reader, non potete aggiungere un allegato al file PDF utilizzando [!DNL Adobe Reader] (NPR-33729).

**Sicurezza dei documenti**

* Impossibile eseguire l&#39;operazione Sign con certificati basati su HSM in un file PDF dopo l&#39;installazione di [!DNL Experience Manager] Service Pack (NPR-34310).

**Designer**

* Impossibile aprire XForms in Designer versione 6.5.x (CQ-4295322).

* Quando si apre Designer, nella schermata introduttiva viene visualizzato un anno non corretto (CQ-4295289).

* Quando si installa [!DNL Acrobat DC] sul server, l&#39;opzione **[!UICONTROL Distribuisci modulo]** è inattiva (CQ-4296304).

Per informazioni sugli aggiornamenti della sicurezza, vedere [ pagina dei bollettini sulla sicurezza degli Experienci Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.5.0  {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0 è un aggiornamento importante che include nuove funzioni, miglioramenti fondamentali richiesti dai clienti, nonché miglioramenti a prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 rilasciata a partire da **aprile 2019**. Può essere installato sulla parte superiore di Adobe Experience Manager 6.5.

Alcune funzioni chiave e miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.5.0 includono:

* L&#39;accesso anonimo al CRXDE Lite non è consentito. Al contrario, gli utenti vengono indirizzati alla schermata di accesso. Vedere [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Personalizzare i nomi delle colonne visualizzati in [!DNL Adobe Experience Manager] Inbox.

* È stata migliorata l&#39;accessibilità in varie aree in  Web Content Management (WCM) di Experience Manager, come Editor pagina, Componenti di base, Editor Rich Text e l&#39;interfaccia utente Amministratore.

* Salvare un elemento [!DNL Interactive Communication] come bozza.

* Supporto per [!DNL Oracle WebLogic 12] per Forms  Experience Manager su JEE.

* È stata migliorata la gestione delle eccezioni nel flusso dell&#39;interfaccia utente [!DNL Adobe Experience Manager Assets].

* Per ottenere l’URL di pubblicazione per Scene7 multimediale dinamico, all’interfaccia `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` viene aggiunto un nuovo metodo `getRemoteAssetPublishURL`.

* [Miglioramenti ](#assets-6550) dell&#39;accessibilità  [!DNL Adobe Experience Manager Assets] in conformità alle linee guida WCAG (Web Content Accessibility Guidelines).

* È stata rimossa l&#39;integrazione di Package Share da Adobe Experience Manager.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.3.

Per un elenco completo delle funzioni, degli elementi di rilievo e delle funzioni chiave introdotte  service pack 5 dell&#39;Experience Manager 6.5, vedere [Novità in Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Di seguito è riportato l&#39;elenco delle correzioni fornite nella release [!DNL Experience Manager] 6.5.5.0.

### [!DNL Sites] {#sites-6550}

*  Siti Experience Manager offre l’opzione per pubblicare o annullare la pubblicazione di una pagina dal relativo alias. L&#39;opzione non funziona (NPR-33415).
* Quando un Contenitore di layout viene eliminato da un modello contenente più modelli, il rendering del modello non viene eseguito correttamente (NPR-33347).
* Quando una pagina di siti di Experience Manager  fa parte di un set di contenuti di grandi dimensioni con più Live Copy, l&#39;anteprima della cronologia delle versioni della pagina non viene caricata (NPR-33311).
* Quando si utilizza il comando Sposta per rinominare una pagina di siti di Experience Manager , il titolo della pagina non viene aggiornato (NPR-33264).
* Quando si spostano le pagine nella vista a colonne, le colonne scompaiono (NPR-33216).
* Quando il nome di un componente locale in una copia per lingua è identico al nome di un componente nel blueprint e il componente viene implementato dal blueprint, il termine `_msm_moved` non viene aggiunto al nome del componente locale (NPR-33208).
* Il servlet Page Redirect aggiunge .html a un URL di siti di  Experience Manager in cui ResourceType non è `cq:Page` (NPR-33176).
* Quando incollate una sottostruttura, non è possibile stabilire se le relative sottopagine devono essere incollate o meno (NPR-33149).
* Il numero di risultati negli usi live di un componente è limitato al numero 49 (NPR-33058).
* Se si basa un frammento di contenuto su uno schema e questo contiene un&#39;area di testo obbligatoria o un campo percorso, il frammento di contenuto non viene salvato (NPR-33007).
* Quando create un componente personalizzato utilizzando il componente Frammento esperienza predefinito e lo utilizzate  pagine Siti Experience Manager,  Experience Manager non visualizza riferimenti (utilizzo) per il componente personalizzato (NPR-32852).
* Quando rinominate una cartella con numerosi riferimenti, molti riferimenti alla cartella non vengono aggiornati (NPR-32765).
* Quando abilitate l&#39;opzione di modifica sorgente, questa diventa disponibile per le opzioni di visualizzazione a schermo intero in linea ma non per la finestra di dialogo di modifica e le opzioni a schermo intero dell&#39;editor Rich Text (NPR-32763).
* Se disponete di un campo multiplo e contiene un campo obbligatorio (ad esempio un menu a discesa o un campo percorso) nelle proprietà della pagina di un blueprint, quando viene implementata una pagina contenente tale campo multiplo, le proprietà della pagina della Live Copy non vengono salvate (NPR-32751).
* Gli assistenti vocali non possono utilizzare la struttura dell&#39;intestazione per navigare nella pagina. Inoltre, nella scheda Componenti è presente un&#39;etichetta errata (NPR-32648).
* All&#39;avvio dell&#39;impaginazione, il Selettore frammenti esperienza non carica tutti gli elementi (NPR-32605).
* Le autorizzazioni di lettura, modifica, creazione ed eliminazione delle copie in diretta vengono revocate. Ogni autore doveva fornire esplicitamente le autorizzazioni di lettura e modifica per spostare le pagine all&#39;interno di una Blueprint (NPR-32550).
* Gli autori dei contenuti non riescono a creare Launch per una pagina che dispone di un&#39;integrazione con  Adobe Analytics (NPR-32548).
* Quando un utente riprende l&#39;ereditarietà con la sincronizzazione, la live copy della pagina padre non si sincronizza con il blueprint e visualizza uno stato non corretto (NPR-32500).
*  pagina dell&#39;editor di siti di Experience Manager richiede più di 15 secondi di caricamento (NPR-32413).
* Alcuni campi non visualizzano l&#39;opzione Annulla ereditarietà (NPR-32362).
* Quando selezionate un percorso per un componente Frammento esperienza e la casella di controllo Apri finestra di dialogo di selezione, non viene visualizzato nel browser Percorso (NPR-32308).
* Quando eseguite l&#39;aggiornamento  Experience Manager 6.2 a  Experience Manager 6.5, il componente Parsys dei modelli statici non viene visualizzato correttamente. L&#39;altezza del componente Parsys è impostata su 0 e i componenti al suo interno non sono visibili (NPR-33663).
* Quando un utente copia e incolla un Contenitore di layout sulla stessa pagina, i componenti in un Contenitore di layout non vengono visualizzati (NPR-33648).
* Il controllo dello stato del dispatcher visualizza il messaggio di avviso `Invalid cookie header` nei file di registro (NPR-33629).
* XSS riflesso in PreferencesServlet (NPR-33438).
* Gli utenti anonimi possono accedere alle funzioni CRXDE Lite (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>Agli utenti Windows di [!DNL Experience Manager desktop app] viene consigliato di eseguire l&#39;aggiornamento alla [versione dell&#39;app desktop 2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added) per accedere all&#39;archivio DAM nell&#39;istanza [!DNL Adobe Experience Manager 6.5.5.0]. In quanto possono rilevare problemi durante l&#39;accesso all&#39;archivio DAM nell&#39;istanza [!DNL Adobe Experience Manager] 6.5.5.0 utilizzando l&#39;app desktop versione 2.0.2.

**Miglioramenti dell&#39;accessibilità in  risorse Experience Manager**

* È ora possibile attivare la tastiera nell&#39;elenco [!UICONTROL Commenti] e selezionare l&#39;opzione per [!UICONTROL Creare ] commenti sulla versione in [!UICONTROL Creare una nuova versione] nel pannello delle risorse [!UICONTROL Timeline] (NPR-33424).

* Ora è possibile accedere all&#39;opzione [!UICONTROL Visualizza impostazioni] per le risorse e modificare le impostazioni nella finestra di dialogo [!UICONTROL Visualizza impostazioni] utilizzando i tasti della tastiera (NPR-33420).

* La casella di riepilogo a comparsa della casella combinata (in vari campi su pagine diverse) ora mostra le voci come un elenco di opzioni che possono essere annunciate dagli assistenti vocali (NPR-33516).

* La funzionalità di ordinamento delle intestazioni ordinabili (nella vista a elenco, nella vista [!UICONTROL Timeline] e nella pagina [!UICONTROL Gestisci pubblicazione]) ora è annunciata dagli assistenti vocali e i controlli di ordinamento sulle intestazioni delle colonne sono accessibili tramite tastiera (NPR-32979).

* Gli elementi su cui è possibile fare clic, come schede per commenti, aggiornamenti delle versioni, caselle combinate e icone chevron dei menu, ora possono essere attivati e interagire con l&#39;utilizzo di una tastiera (NPR-33514).

* Funzionalità (o scopo dell&#39;azione) delle icone delle informazioni (per uso, impression e clic) su [!UICONTROL Insights View] sono ora annunciate correttamente dagli assistenti vocali (NPR-33513).

* I campi modulo di sola lettura (ad esempio i campi disabilitati in [!UICONTROL scheda Base] della risorsa [!UICONTROL Properties]) sono ora attivabili mediante la tastiera (NPR-33493, CQ-4273031).

* Le etichette in vari campi di input sono ora etichette permanenti (quindi accessibili) e non solo etichette segnaposto, scomparse al momento dell&#39;immissione del testo (NPR-33475).

* Diversi livelli di intestazione (come titoli di pagina e intestazioni di sezione) vengono ora percepiti come titoli con livelli diversi per gli utenti degli assistenti vocali (NPR-33471).

* Gli elementi interattivi dell&#39;interfaccia utente, come i collegamenti e le opzioni (nelle opzioni di intestazione e zoom della pagina delle risorse, nella navigazione delle cartelle), sono ora accessibili tramite una tastiera (NPR-33468, CQ-4271412).

* Gli indicatori di avanzamento di [!UICONTROL Opzioni], [!UICONTROL Ambito] e [!UICONTROL Flussi di lavoro] nella pagina [!UICONTROL Gestisci pubblicazione] vengono ora correttamente letti dagli assistenti vocali come indicatori di avanzamento, anziché come schede (NPR-33416).

* Il colore delle icone di valutazione a stella (ad esempio nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] nella risorsa [!UICONTROL Proprietà] o nella vista a schede) viene modificato per consentire agli utenti con una visione limitata e senza percezione del colore un contrasto adeguato (NPR-33414).

* È ora possibile accedere alla freccia verso l&#39;alto accanto al campo [!UICONTROL Commento] nella pagina dei dettagli delle risorse utilizzando i tasti di scelta rapida (NPR-33397).

* Gli stati espansi e ridotti della finestra di dialogo [!UICONTROL Tag] sulla risorsa [!UICONTROL Proprietà] e la navigazione a sinistra (sull&#39;interfaccia utente delle risorse) ora vengono annunciati correttamente dagli assistenti vocali (NPR-33396).

* I titoli di tutte le pagine visualizzate su [!DNL Adobe Experience Manager] Risorse ora sono univoci (NPR-33343).

* Quando si naviga nella struttura ad albero, diversi elementi del controllo della visualizzazione ad albero vengono ora correttamente annunciati dagli assistenti vocali (NPR-33304).

* Diverse versioni delle risorse nella vista [!UICONTROL Timeline] nella pagina dei dettagli delle risorse sono ora accessibili tramite i tasti di scelta rapida (NPR-33283).

* I nomi dei suggerimenti di ricerca visualizzati nella casella combinata Omnisearch ora sono annunciati dagli assistenti vocali quando si utilizza la funzionalità di ricerca (NPR-33280).

* Gli elementi su cui è possibile fare clic e [!UICONTROL Vai al collegamento] in [!UICONTROL Barra dei riferimenti] sono ora annunciati dagli assistenti vocali come elementi selezionabili (NPR-33278).

* Le informazioni sulla struttura della tabella (come riga 1, cella 1, tabella) della finestra di dialogo [!UICONTROL Condividi collegamento] non vengono più annunciate dagli assistenti vocali quando si apre la finestra di dialogo (NPR-33268).

* Lo scopo di vari elementi della casella combinata (ad esempio il campo Percorso e l&#39;opzione per aprire la finestra di dialogo di selezione nella scheda Base delle proprietà della risorsa) ora viene annunciato correttamente dagli assistenti vocali (NPR-33235).

* Le informazioni che le righe nella tabella di visualizzazione a elenco sono selezionabili vengono ora comunicate agli utenti dell&#39;assistente vocale quando sono attivate dalla tastiera. Quando un puntatore passa sulle righe, gli assistenti vocali annunciano le informazioni (NPR-33234).

* Le opzioni (con [!UICONTROL x]) per rimuovere ciascuno dei tag selezionati sotto il campo [!UICONTROL Tags] nella scheda [!UICONTROL Basic] della scheda [!UICONTROL Properties] sono ora accessibili agli assistenti vocali (NPR-33206).

* Il selettore della data del calendario è ora attivabile e utilizzabile tramite la tastiera da parte degli utenti di utilità di lettura dello schermo e degli utenti di tastiera con vista (NPR-33200).

* L&#39;interruttore per passare dalla visualizzazione a elenco a quella a schede ora espone correttamente la sua funzionalità (di regolazione delle viste) all&#39;assistente vocale (NPR-33069).

* Il menu nella barra a sinistra è ora accessibile. Funzionalità e scopo dell&#39;espansione del menu sono annunciati dagli assistenti vocali (NPR-33068).

* Le caselle di riepilogo e molti altri elementi dell&#39;interfaccia utente sono ora accessibili agli utenti di utilità di lettura dello schermo senza vista e le seguenti informazioni sono fornite dagli assistenti vocali (NPR-33040):

   * se l&#39;input dell&#39;utente è richiesto su un elemento prima dell&#39;invio del modulo.
   * se un elemento non è modificabile.
   * se un widget è selezionato o meno.

* È ora possibile accedere all&#39;opzione di apertura della barra laterale del filtro tramite la tastiera (NPR-32842, CQ-4273018).

* Il controllo casella di controllo nell&#39;intestazione della colonna della vista a elenco è ora accessibile e lo scopo di utilizzare il controllo è annunciato dagli assistenti vocali (NPR-32722, NPR-33005).

* Le etichette per i campi delle ore (HH) e dei minuti (mm) nel selettore della data del calendario ora sono etichette permanenti invece delle etichette dei segnaposto e non scompaiono quando l&#39;utente immette del testo in questi campi (NPR-32720).

* Il testo dei collegamenti delle notifiche (che appaiono dopo aver fatto clic sull&#39;icona della campana) viene ora annunciato agli utenti dell&#39;assistente vocale che utilizzano la scheda per accedere a ciascun collegamento (NPR-32645).

* [!UICONTROL Seleziona],  [!UICONTROL Scarica],  [!UICONTROL Proprietà] e  [!UICONTROL Altre ] azioni sulle schede delle risorse in  [!UICONTROL Insights ] Vieware sono ora accessibili tramite tastiera (NPR-32609).

* I contenuti visivamente nascosti (ad esempio, contenuti della barra di intestazione sui risultati della ricerca) non vengono più annunciati dagli assistenti vocali quando vi si accede utilizzando la tastiera (NPR-32606).

* Lo scopo delle etichette sui controlli per passare ai mesi successivi e precedenti nel selettore della data del calendario è ora annunciato dagli assistenti vocali (NPR-32604).

* Le icone di valutazione a stella sono ora attivabili e utilizzabili tramite tasti della tastiera (NPR-32513).

* La funzionalità di controllo del volume video è ora accessibile tramite scheda (per concentrarsi sul cursore del volume) e tasti freccia (per regolare il volume) sulla tastiera (NPR-32065).

* Lo scopo dei campi di input associati inferiore ([!UICONTROL Da]) e associati superiore ([!UICONTROL A]) del filtro Dimensione file è ora annunciato agli utenti di utilità di lettura dello schermo non vedenti (NPR-32064).

* Il menu [!UICONTROL Languages] nel modulo [!UICONTROL Create and Translate] è ora accessibile agli assistenti vocali in modalità Sfoglia (CQ-4293906).

* Il pannello [!UICONTROL Riferimenti] è ora accessibile con i seguenti miglioramenti (NPR-33261, CQ-4293798):

   * In modalità Sfoglia, l&#39;assistente vocale non si sposta più sui campi di modifica multiriga nascosti nelle sezioni [!UICONTROL Riferimenti del sito], [!UICONTROL Riferimenti risorsa], [!UICONTROL Copie] e [!UICONTROL Riferimenti del modulo].

   * Gli assistenti vocali annunciano ora il ruolo degli elementi [!UICONTROL Site References] e [!UICONTROL Language Copy].

   * Lo stato attivo degli assistenti vocali in modalità Sfoglia si sposta in una sequenza significativa a vari elementi.

* [!UICONTROL La pagina ] Editor schema metadati e i relativi elementi sono ora accessibili mediante la tastiera e sono compatibili con gli assistenti vocali (CQ-4290962, CQ-4272953).

* Lo scopo del simbolo `X` per rimuovere i tag selezionati viene ora annunciato dagli assistenti vocali insieme al numero di tag selezionati (CQ-4273017).

* Per evitare confusione negli utenti non vedenti che utilizzano l&#39;assistente vocale, le icone decorative e le immagini vengono ora ignorate dagli assistenti vocali (CQ-4272944).

**Problemi risolti in Risorse  Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets risolve i seguenti problemi:

* [!UICONTROL L&#39;opzione ] Start in  [!UICONTROL Crea finestra di dialogo ] flusso di lavoro per le risorse di una raccolta è disabilitata, impedendo l&#39;attivazione del flusso di lavoro (NPR-32471).

* Quando si utilizza la finestra a comparsa a cascata negli schemi di metadati, quando si seleziona e si salva un&#39;opzione a discesa contenente un apostrofo (dall&#39;elenco a discesa figlio) l&#39;opzione dell&#39;apostrofo selezionato scompare dopo la riapertura della risorsa [!UICONTROL Proprietà] (NPR-32649).

* [!UICONTROL Asset Insights Sincronizza ] Jobstop e non riesce se rileva voci non valide (sul lato Analytics) invece di passare alla voce successiva (NPR-32674).

* Il giroscopio non funziona perché i sensori di movimento sono disattivati per impostazione predefinita sui browser mobili nel visualizzatore panoramico (CQ-4272937).

* [!UICONTROL La procedura guidata ] di configurazione delle risorse collegate non funziona con l&#39;errore 404, quando si installa 6.5.3 in 6.5.1 (NPR-32730).

* Durante il processo di XMP writeback, tutte le proprietà di metadati dello spazio dei nomi personalizzate modificano il prefisso dello spazio dei nomi personalizzato in ns2 invece del prefisso dello spazio dei nomi configurato (NPR-32748).

* Il caricamento lento non viene attivato e solo 100 risorse vengono visualizzate quando si seleziona per controllare le attività dalla inbox delle notifiche (NPR-32750).

* `NullPointerException` è stato osservato a causa di preferenze di nodo mancanti nel profilo utente appena creato (SAML/SSO). Questo errore impedisce agli utenti che hanno effettuato l&#39;accesso di utilizzare l&#39;integrazione [!DNL Adobe Experience Manager Stock] (NPR-32777).

* Gli avvisi relativi alle transizioni sono riportati nei registri relativi all&#39;apertura di una raccolta intelligente contenente più di 10.000 risorse (NPR-32980).

* I nomi delle risorse vengono modificati in lettere minuscole quando si spostano le risorse da una cartella all&#39;altra in [!DNL Adobe Experience Manager] utilizzando la modalità di esecuzione di Dynamic Media Scene7 (NPR-32995).

* Una risorsa ricercata non può essere eliminata dopo aver navigato nelle sue proprietà dai risultati della ricerca e poi essere tornata ai risultati della ricerca per eliminarla (NPR-32998).

* [!UICONTROL L&#39;opzione ] Nextoption rimane disabilitata quando si seleziona la cartella di destinazione nell&#39;interfaccia  [!UICONTROL Sposta ] risorse (NPR-33356).

* [!UICONTROL L&#39;opzione ] Nextoption non è abilitata quando si seleziona il nodo padre (dove è visibile una singola cartella figlio) e si seleziona la cartella figlio (NPR-33275).

* Le autorizzazioni di Check-in e check-out sono disattivate in  Adobe Asset Link (AAL) per gli utenti con autorizzazione di eliminazione, anche se sono concesse altre autorizzazioni come lettura, creazione o modifica (NPR-33272).

* Le rappresentazioni SmartCrop non sono disponibili nella finestra di dialogo di download delle risorse (NPR-33167).

* Eccezione nei registri relativi all&#39;apertura della barra delle rappresentazioni per un PDF in una cartella con profilo di ritaglio avanzato (CQ-4294201).

* I predefiniti per immagini non vengono pubblicati se la modalità di sincronizzazione di [!UICONTROL elementi multimediali dinamici] è disattivata per impostazione predefinita  Experience Manager con la modalità di esecuzione di Scene7 per contenuti multimediali dinamici (CQ-4294200).

* L&#39;elaborazione delle risorse durante il caricamento in blocco si blocca e l&#39;istanza del flusso di lavoro mostra le istanze bloccate della risorsa di aggiornamento DAM (CQ-4293916).

* La creazione di una configurazione per file multimediali dinamici su  Experience Manager funziona, ma nell’interfaccia utente non accade nulla se si seleziona Salva (CQ-4292442).

* L&#39;anteprima delle risorse video F4V non funziona nella riproduzione progressiva su Safari/Mac (CQ-4289844).

* Al ritaglio avanzato di una risorsa che si trova all’interno di una cartella principale con il carattere punto `.` nel nome (CQ-4289337) viene creata una cartella aggiuntiva.

* La miniatura è rotta e il banner di elaborazione video non viene visualizzato quando un video viene copiato (CQ-4284125).

* Il visualizzatore dimensionale visualizza erroneamente le miniature vuote in Firefox per alcuni modelli con viste fotocamera vuote (CQ-4283447).

* I problemi di prestazioni risolti in 6.5.5.0 sono (CQ-4279206):

   * Il caricamento di file binari di grandi dimensioni sui server di elaborazione immagini per file multimediali dinamici richiede troppo tempo.

   * Il tempo di generazione delle miniature  Experience Manager aumenta a causa dell’architettura Dynamic Media Scene7.

* I problemi di migrazione di Dynamic Media Scene7 non riescono per i clienti con un numero elevato di risorse (CQ-4279206).

* Il layout del visualizzatore video 360 viene interrotto se si utilizza `setVideo` e il video si sposta verso il basso utilizzando `video= modifier` (CQ-4263201).

* Viene visualizzato un messaggio di errore durante l&#39;installazione del pacchetto SDL del Experience Manager  (NPR-33175).

* Vulnerabilità SSRF nel Experience Manager  (NPR-33435).

### Piattaforma {#platform-6550}

* Il filtro [!DNL Sling] non viene chiamato se la voce di mapping `sling:match` viene creata in `/etc/maps` (NPR-33362).
*  Experience Manager si arresta in modo anomalo a causa di un errore di segmentazione con [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] pacchetto di base mancante  file uberjar di Experience Manager (NPR-32848).
* Il CRXDE Lite non carica il contenuto per gli utenti senza l&#39;autorizzazione di lettura sulla proprietà `jcr:primaryType` di un nodo (NPR-32611).
* [!DNL Granite] la pianificazione delle attività di manutenzione viene inizializzata troppo spesso durante  distribuzioni di Experienci Manager (CQ-4294627).
* Quando una query SQL viene eseguita per un periodo di tempo prolungato, ad esempio 7 ore,  Experience Manager smette di rispondere (NPR-33044).

### Interfaccia utente {#ui-6550}

* La selezione del pulsante di scelta non persiste in un campo multiplo (NPR-33309).
* Il limite di caricamento non funziona per la visualizzazione elenco (NPR-33124).
* Nella pagina dei risultati della ricerca omnisearch non viene visualizzato un messaggio in assenza di corrispondenze (NPR-32974).
* Il filtro Omnisearch restituisce tutte le corrispondenze sotto il nodo `/content` ignorando la posizione selezionata (NPR-32849).

### Integrations (Integrazioni){#integrations-6550}

* La cache interna viene cancellata quando viene pubblicata una pagina con un componente Adobe Target  (NPR-33162).
* L&#39;integrazione con  Adobe Target non funziona su [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Durante la configurazione  Adobe Target, i campi [!UICONTROL Company] e [!UICONTROL Report Suite] non vengono visualizzati quando si seleziona un&#39;origine di reporting (NPR-32502).
* Quando si esporta [!DNL Experience Fragments] utilizzando  Adobe I/O, i metadati come Prodotto di origine non vengono esportati  Adobe Target (NPR-32159).
* Gli utenti IMS autorizzati nel gruppo di amministrazione  Experience Manager locale non possono creare o modificare configurazioni IMS (NPR-33045).
*  pagina Configurazioni lancio Adobe non visualizza tutti i record (NPR-33011).
* Gli utenti del gruppo di autori di contenuti non possono modificare le proprietà di un componente Adobe Target  a causa di un errore JavaScript (NPR-32996).
* Script tra siti per JSON (NPR-32744).

### Progetti traduzione {#translation-6550}

* I tag convertiti non vengono importati in  Experience Manager da servizi di traduzione di terze parti (NPR-33154).
* Nella pagina di configurazione della traduzione viene visualizzato un provider di traduzione non corretto rispetto a quello utilizzato per la traduzione (NPR-32971).
* Se si aggiunge una cartella di frammenti esperienza a un progetto di traduzione esistente, viene creato un nuovo progetto (NPR-32843).
* Nei registri viene visualizzato un errore `NullPointerException` durante l&#39;esecuzione di un processo di traduzione (NPR-32628).

### WCM {#wcm-6550}

* Editor pagina - L&#39; [!DNL Sites] Editor pagina non consente agli utenti che utilizzano solo la tastiera di passare al contenuto principale invece di spostare lo stato attivo tramite tutte le opzioni disponibili nell&#39;intestazione (CQ-4293883).
* Editor pagina - I pannelli che utilizzano il componente Bene e includono i dati salvati non vengono visualizzati a causa degli aggiornamenti nelle versioni [!DNL Chrome] e [!DNL Firefox] (CQ-4292995).
* MSM - Se si elimina un componente dalla pagina, il componente non viene eliminato dalla versione pubblicata della pagina (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Se si rimuove uno schema di metadati pubblicato da [!DNL Brand Portal] si verifica un errore (CQ-4292063).
* Se un amministratore configura [!DNL Experience Manager Assets] 6.5.4 con Portale marchio tramite  Console Sviluppatori di Adobe, l&#39; [!DNL Brand Portal] utente non è in grado di pubblicare la risorsa di una cartella di contributi da [!DNL Brand Portal] a [!DNL Experience Manager] (NPR-33046).
* Replica duplicata delle cartelle principali che causano conflitti (NPR-33001).

### [!DNL Communities] {#communities-6550}

* Non è possibile eliminare una scheda nella console di moderazione utilizzando l&#39;opzione di menu di modifica rapida (NPR-33117).
* Errore durante l&#39;accesso alla pagina [!UICONTROL Activity Stream] (NPR-33146).
* I gruppi eliminati nell’istanza di creazione non vengono rimossi da tutte le istanze di pubblicazione (NPR-33199).
* Dopo aver creato un nuovo gruppo, gli autori non vengono reindirizzati alla sezione [!UICONTROL Gruppo community] su [!DNL Internet Explorer] 11 (NPR-33205).
* L&#39;accesso a un messaggio in  Casella in entrata Experience Manager non modifica lo stato del messaggio in Lettura (NPR-32764).
* Se si modifica un gruppo [!DNL Communities] e si modifica l&#39;immagine in miniatura, l&#39;immagine del gruppo non viene aggiornata (NPR-32599).
* Un utente non è in grado di inviare un&#39;e-mail a un altro utente in una community (NPR-32598).
* Un blog inviato non viene visualizzato finché l&#39;utente non aggiorna la pagina (NPR-32391).
* Durante la creazione di una versione di notifiche e sottoscrizioni di contenuti generati dall&#39;utente (UGC), viene memorizzato un ID errato della pagina di origine (CQ-4279355, CQ-4289703).
* Problema di scripting tra siti (NPR-33203).

### Flusso di lavoro {#workflow-6550}

* Il caricamento dell&#39;opzione [!UICONTROL Timeline] nella barra a sinistra richiede più tempo del previsto (NPR-32851).
* Dopo il riavvio di un&#39;istanza di Experience Manager , l&#39;e-mail per l&#39;attività di revisione per una raccolta include un collegamento di payload non corretto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
> Experience Manager Service Pack non include correzioni per [!DNL Forms]. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per  AEM Forms su JEE. Per ulteriori informazioni, vedere [Installare  Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare  Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gestione corrispondenza: L&#39;ordine delle risorse in un&#39;area di destinazione viene visualizzato dopo l&#39;invio di una lettera (NPR-33359, NPR-33153).
* Forms adattivo: Quando un utente modifica un modulo adattivo, l&#39;opzione [!UICONTROL Avvia flusso di lavoro] disponibile nel menu [!UICONTROL Informazioni pagina] non funziona (NPR-33004).
* Forms adattivo: L&#39;utente non è in grado di salvare un modulo adattivo con più allegati (NPR-32997).
* Forms adattivo: La modifica del layout del pannello in un modulo adattivo genera un errore (CQ-4293880).
* Forms adattivo: Una nuova riga di una stringa in un dizionario di moduli adattivi aggiunge caratteri `&#xa;` al dizionario (NPR-33266).
* Accessibilità Forms adattiva: Quando un utente visualizza l&#39;anteprima di un modulo adattivo come modulo HTML, il campo [!UICONTROL Firma scarabocchio] non è in grado di mantenere lo stato attivo (NPR-33159).
* Accessibilità Forms adattiva: I messaggi di errore visualizzati durante l&#39;invio di un modulo adattivo non sono collegati a un attributo `aria-describedBy` (NPR-33071).
* Accessibilità Forms adattiva: I campi contrassegnati come obbligatori in un modulo adattivo non hanno l&#39;attributo obbligatorio impostato su True nello schema di accessibilità ARIA (NPR-33070).
* Servizio PDFG: Quando un utente converte un file di testo in un PDF, i caratteri giapponesi non vengono rappresentati correttamente (NPR-33238).
* Servizio PDFG: L&#39;operazione `CreatePDF` non riesce a convertire un file PDF in formato OCR PDF (NPR-32994).
* Servizio PDFG: La conversione PDF non riesce per la 200a istanza di un documento [!DNL OpenOffice] (NPR-32766).
* BackendIntegration: Le richieste del modello dati del modulo non vanno a buon fine perché il token di aggiornamento scade a causa di uno stato inattivo non corretto (NPR-33169).
* Designer: Gli assistenti vocali eseguono l&#39;ordine di tabulazione in base all&#39;ordine geografico predefinito anziché all&#39;ordine di tabulazione personalizzato definito nel file XDP (NPR-32160).
* Designer: Se l&#39;opzione relativa ai tag è abilitata, il bordo del sottomodulo scompare nell&#39;output PDF generato (NPR-32778).
* Memorizzato XSS con GuideSOMProviderServlet (NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 è un aggiornamento importante che include nuove funzioni, miglioramenti e prestazioni richiesti dai clienti chiave, stabilità, miglioramenti a livello di sicurezza, rilasciati a partire dalla versione 6.5 rilasciata a **aprile 2019**. Può essere installato sulla parte superiore di Adobe Experience Manager 6.5.

Alcune funzioni chiave e miglioramenti introdotti in Adobe Experience Manager 6.5.4.0 includono:

* Adobe Experience Manager Assets è ora configurato con Brand Portal tramite  Adobe I/O Console.

* È ora disponibile un nuovo passaggio [Genera output stampabile](../forms/using/aem-forms-workflow-step-reference.md) per  flussi di lavoro Adobe Experience Manager Forms.

* [Supporto per più colonne ](../forms/using/resize-using-layout-mode.md) per la modalità di layout per moduli adattivi e comunicazioni interattive.

* Supporto per [Rich Text](../forms/using/designing-form-template.md) nei moduli HTML5.

* [Miglioramenti ](new-features-latest-service-pack.md#accessibility-enhancements) dell’accessibilità in  risorse di Experience Manager.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.8.

* Ora è possibile sincronizzare le sottostrutture per contenuti selettivi su *Contenuti multimediali dinamici - Modalità Scene7* invece di tutti i contenuti disponibili in `content/dam`.

* L&#39;integrazione del modello dati del modulo con il servizio Web SOAP ora supporta i gruppi di scelta o gli attributi sugli elementi.

* Le strutture di input o output SOAP e i dati complessi ora supportano la sostituzione di gruppi dinamici.

Per un elenco completo delle funzioni e delle caratteristiche principali introdotte nei Service Pack più recenti, vedere [Novità nei Service Pack di Adobe Experience Manager 6.5](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Quando un URL di una pagina Adobe Experience Manager Sites  contiene due punti (`:`) o un simbolo percentuale (`%`), il browser smette di rispondere e i picchi di utilizzo della CPU (NPR-32369, NPR-31918).

* Quando si apre una pagina di siti di Experience Manager  per la modifica e si copia un componente, l&#39;azione Incolla non è disponibile per alcuni segnaposto (NPR-32317).

* Quando si apre la procedura guidata Gestisci pubblicazione, un frammento esperienza collegato a un componente core non viene visualizzato negli elenchi dei riferimenti pubblicati (NPR-32233).

* Il rendering della panoramica della Live Copy nell&#39;interfaccia touch richiede molto più tempo dell&#39;interfaccia classica (NPR-32149).

* Quando il server-time e il computer-time si trovano in fusi orari diversi, l&#39;ora di pubblicazione pianificata mostra l&#39;ora del server nell&#39;interfaccia utente touch, mentre nell&#39;interfaccia classica l&#39;ora del computer viene visualizzata (NPR-32077).

*  Siti di Experience Manager non riesce ad aprire una pagina con un suffisso nell’URL (NPR-32072).

* Quando un utente modifica un frammento di contenuto, viene ripristinata una variante eliminata del frammento di contenuto (NPR-32062).

* Gli utenti possono salvare un frammento di contenuto senza fornire informazioni nei campi richiesti (NPR-31988).

* kernel.js e ui.js non sono precompilati o memorizzati nella cache. Ciò comporta un ulteriore tempo per il rendering delle pagine (NPR-31891).

* Quando PageEventAuditListener è abilitato, la lunghezza della coda di commit aumenta. Incide sulle prestazioni di molte operazioni, come la pubblicazione in blocco, la navigazione e lo spostamento di risorse in massa (NPR-31890).

* Quando si trascinano i frammenti esperienza, viene osservato un tempo di risposta elevato (NPR-31878).

* Quando selezionate l’opzione Trascinate qui il componente nel segnaposto di una griglia reattiva, viene inviata una richiesta di GET e la richiesta genera un errore HTTP 403 (NPR-31845).

* Quando si sposta il contenuto all&#39;interno della stessa cartella, l&#39;opzione di spostamento della pagina è disabilitata (NPR-31840).

* In modalità struttura modelli modificabili, l&#39;elenco dei componenti consentiti nel contenitore di layout presenta risultati non corretti. Nel contenitore di layout (NPR-31816) vengono visualizzati solo i componenti con finestra di dialogo di progettazione.

* Quando una pagina dispone di autorizzazioni di sola lettura per un utente, l&#39;opzione Apri proprietà è visibile in sites.html ma non in editor.html (NPR-31770).

* Quando un utente fa clic sul pulsante Crea, l&#39;opzione della pagina non è disponibile (NPR-31756).

* Impossibile sincronizzare la campagna in  campagna di Adobe contenente il componente Importazione progettazione OOOTB (Out of the box) (NPR-31728).

* Quando si tenta di modificare un elenco di elenchi puntati in elenchi numerati, vengono modificati solo i primi due elementi dell&#39;elenco (NPR-31636).

* Quando una pagina viene decreata e viene selezionato il nodo figlio, nella finestra di dialogo di selezione viene ancora visualizzato il nodo iniziale. Quando la pagina viene creata e l&#39;utente fa clic su Sfoglia, la pagina reindirizza al nodo principale invece del nodo creato (NPR-31618).

* La finestra di dialogo di configurazione della visualizzazione non funziona correttamente per la funzione di personalizzazione Inbox (NPR-32503 e NPR-32492).

* Viene visualizzato un messaggio di errore durante la visualizzazione delle informazioni sul flusso di lavoro tramite Inbox (CQ-4282168).

### Assets {#assets-6540-enhancements}

* Il pulsante per attivare il flusso di lavoro nella pagina di raccolta delle risorse è disattivato (NPR-32471).

* Una cartella senza nome viene creata in SPS (Scene7 Publishing System) mentre si sposta una risorsa da una cartella all’altra in  Experience Manager con configurazione Scene7 per file multimediali dinamici (NPR-32440).

* L’azione per spostare tutte le risorse (tramite Seleziona tutto e quindi Sposta) in una cartella contenente le risorse pubblicate non riesce e ha esito negativo (NPR-32366).

* Generazione della rappresentazione per le risorse con ${extension} non riuscita (NPR-32294).

* Gli URL della cronologia delle versioni vengono visualizzati nel campo Con riferimento nella pagina Proprietà delle risorse (NPR-31889).

* Impossibile aprire il file ZIP scaricato da DAM tramite WinZip (NPR-32293).

* Le autorizzazioni originali di una cartella vengono aggiornate quando le Impostazioni cartella vengono aperte per cambiare il titolo della cartella o l&#39;immagine in miniatura e quindi salvate (NPR-32292).

* L&#39;icona Calendario per l&#39;attivazione pianificata non viene visualizzata nella colonna Stato (nell&#39;interfaccia classica dell&#39;elenco di risorse DAM) per le risorse la cui attivazione è pianificata per una data e un&#39;ora successive (NPR-32291).

* La creazione di snippet mediante i modelli di snippet genera un errore durante la ricerca delle raccolte durante il processo di creazione degli snippet (NPR-32290).

* Quando si selezionano più tag dal filtro di ricerca (NPR-32143), vengono attivate più query di ricerca.

* ’interfaccia utente Risorse Experience Manager mostra i nomi dei file troncati quando vengono caricate risorse con più di 50 caratteri nel nome del file (NPR-32054).

* Tutte le caselle di controllo nel pannello Filtro vengono deselezionate quando la prima e la seconda casella di controllo sono deselezionate, quando sono state selezionate le caselle di controllo di livello due della struttura delle caselle di controllo in  Adobe Stock (NPR-31919).

* La ricerca di file e cartelle con facet Omnisearch fa eccezione (NPR-31872).

* L&#39;evidenziazione dei campi per la selezione obbligatoria dei campi nell&#39;editor di metadati non viene rimossa neanche dopo aver selezionato il campo richiesto, quando le regole di dipendenza sono impostate nel modulo di schema di metadati corrispondente (NPR-31834).

* I nomi completi dei tag a livello di foglia (dalla gerarchia dei tag) non vengono visualizzati nella pagina Proprietà della risorsa (NPR-31820).

* L’utilizzo del comando Indietro dalla pagina Proprietà della risorsa nel browser Safari restituisce un errore (NPR-31753).

* La pagina dei risultati della ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente (NPR-31307).

* La pagina dei dettagli delle risorse PDF non mostra i pulsanti delle azioni tranne I pulsanti Raccolta e Aggiungi rappresentazione nell&#39;Experience Manager  esecuzione in modalità di esecuzione di Dynamic Media Scene7 (CQ-4286705).

* L&#39;elaborazione delle risorse richiede troppo tempo durante il processo di caricamento batch di Scene7 (CQ-4286445).

* Il pulsante Salva non importa il set remoto quando l&#39;utente non ha apportato modifiche nell&#39;Editor set nel client per contenuti multimediali dinamici (CQ-4285690).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene assimilato  Experience Manager (CQ-4283701).

* Lo stato non elaborato del predefinito per visualizzatori video per ritaglio avanzato viene visualizzato due volte sul testo del banner e sul nome del predefinito (CQ-4283517).

* L’altezza contenitore errata di un modello 3D caricato visualizzato in anteprima nel visualizzatore 3D viene visualizzata nella pagina dei dettagli della risorsa (CQ-4283309).

* Carosello Editor non si apre in IE 11 in modalità ibrida  Experience Manager Dynamic Media (CQ-4255590).

* Lo stato attivo si blocca nel menu a discesa E-mail nella finestra di dialogo Download, nei browser Chrome e Safari (NPR-32067).

* La casella di controllo Sincronizza tutto il contenuto non è abilitata per impostazione predefinita quando si tenta di aggiungere la configurazione cloud DM sul  Experience Manager (CQ-4288533).

### Interfaccia utente di base {#foundation-ui-6540}

* Il controllo del mouse passa al campo filtro precedente invece di rimanere nel campo filtro esistente durante la ricerca delle risorse mediante il pannello Filtro (NPR-32538).

* Assegnazione tag piattaforma: La ricerca di tag digitando nei campi tag mostra i tag al di fuori dei limiti principali e non rispetta la proprietà `rootPath` dei campi tag (NPR-31895).

* Interfaccia utente della piattaforma: Se nel campo di testo viene aggiunto un percorso non valido (NPR-31884), il browser del percorso si interrompe.

* La notifica viene nascosta dietro un menu fisso nella selezione delle pagine (NPR-31628).

### Piattaforma {#platform-sling-6540}

* (HTL) I caratteri di sottolineatura sostituiscono i due punti nella sezione del percorso dell&#39;URL (NPR-32231).

### Progetti {#projects-6540}

* Il pulsante Crea non è visibile all&#39;utente anche se l&#39;utente dispone dell&#39;autorizzazione per creare un progetto nella sottocartella (NPR-31832).

### Traduzione progetti {#projects-translation-6540}

* La creazione di un progetto di traduzione interrompe l&#39;interfaccia utente quando l&#39;opzione Rifila spazi è attivata in `Apache Sling JSP Script Handler` (NPR-32154).

* L&#39;errore nell&#39;interfaccia utente e l&#39;eccezione del punto Null nei registri di errore viene rilevato quando un tag, da tradurre, viene aggiunto a un progetto di traduzione (NPR-31896).

### Integrations (Integrazioni){#integrations-6540}

* La generazione degli URL della libreria di avvio si basa solo sui valori `path` e `library_name` dell&#39;API di Launch e non sul valore `library_path` (NPR-31550).

* Viene visualizzato un messaggio di errore durante l&#39;elaborazione degli elementi correlati a LiveFyre (FYR-12420).

* ReportSuitesServlet è vulnerabile all&#39;SSRF (NPR-32156).

### Editor modelli WCM {#wcm-template-editor-6540}

* In modalità struttura modelli modificabili, l&#39;elenco dei componenti consentiti nel contenitore di layout non visualizza il componente pulsante di collegamento (CQ-4282099).

### Editor pagina WCM {#wcm-page-editor-6540}

* Si è verificato un errore durante la selezione di una sovrapposizione e la selezione di componenti reattivi Trascinate qui i componenti (CQ-4283342).

### Targeting delle campagne {#campaign-targeting-6540}

* La configurazione cloud di destinazione non riesce. Errore: richiesta mbox di recupero (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Gli utenti di Brand Portal non sono in grado di pubblicare le risorse delle cartelle dei contributi su [!DNL Assets] durante l’aggiornamento ad  Adobe I/O all’Experience Manager 6.5.4 (CQDOC-15655). Per una correzione immediata all&#39; Experience Manager 6.5.4, si consiglia di [scaricare l&#39;hotfix](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e installarlo nell&#39;istanza di creazione.

* I valori popup dello schema di metadati non sono visibili nelle proprietà delle risorse (CQ-4283287).

* Il sottoschema metadati non visualizza schede in base al tipo di mimetismo nelle proprietà delle risorse (CQ-4283288).

* Lo schema di metadati Annulla pubblicazione compila un messaggio di errore anche se lo schema viene rimosso nel backend.

* L&#39;immagine di anteprima non viene visualizzata per una risorsa pubblicata (CQ-4285886).

* L&#39;utente non può pubblicare o annullare la pubblicazione di risorse contenenti virgolette singole nel nome (CQ-4272686).

* I termini e le condizioni non vengono visualizzati durante il download di più risorse (CQ-4281224).

* Sono state risolte vulnerabilità di sicurezza minori.

### Communities {#communities-6540}

* Il modulo Crea membro viene visualizzato come una pagina vuota (NPR-31997).

* L&#39;utente non è in grado di visualizzare il rapporto di Analytics sull&#39;istanza di creazione (NPR-30913).

### Quercia- Indicizzazione e query {#oak-indexing-6540}

* Documenti MS Word e MS Excel contenenti immagini JPEG, se analizzati con il parser Tika non riescono ad analizzare e la classe non trova errore (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
> Experience Manager Service Pack non include correzioni per  Experience Manager Forms. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per  Adobe Experience Manager Forms su JEE. Per ulteriori informazioni, vedere [Installare  Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare  Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gestione corrispondenza: Le lettere contengono caratteri aggiuntivi dopo l&#39;invio ai flussi di lavoro di post-elaborazione (NPR-32626).

* Gestione corrispondenza: Le lettere visualizzano un segnaposto a discesa come componente di testo dopo l&#39;invio ai flussi di lavoro successivi al processo (NPR-32539).

* Gestione corrispondenza: I valori predefiniti definiti nel modello di lettera non vengono visualizzati nella modalità Anteprima (NPR-32511).

* Mobile Forms: Il pulsante di invio viene visualizzato come espanso nelle dimensioni durante il rendering di un modulo XDP in una versione HTML (NPR-32514).

* Document Services: Problemi di accesso agli URL per Lettere e altre pagine dopo l’applicazione di Service Pack 2 (NPR-32508, NPR-32509).

* Document Services: Se il numero di transazioni su un server supera un limite specifico, la conversione da HTML a PDF non riesce e le impostazioni del tipo di file vengono rimosse dal server [!DNL Forms] (NPR-32204).

* Forms adattivo: Lo strumento di accessibilità del browser segnala gli errori nei moduli adattivi in base alle linee guida WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Forms adattivo: Lo strumento di accessibilità del browser Chrome segnala un errore best practice (NPR-32310).

* Forms adattivo: Problemi di traduzione durante la configurazione di un modulo adattivo incorporato in una pagina di siti di Experience Manager  (NPR-32168).

* Workbench: Viene visualizzato un messaggio di errore durante l&#39;utilizzo dell&#39;operazione Ottieni proprietà PDF per il servizio Utilità PDF (NPR-32150).

* Document Security: Un file PDF protetto non viene aperto offline con l&#39;opzione DisableGlobalOfflineSynchronizationData impostata su True (NPR-32078).

* Designer: Se l&#39;opzione relativa ai tag è attivata, il bordo del sottomodulo scompare nell&#39;output PDF generato (NPR-32547, NPR-31983, NPR-31950).

* Designer: Se in una tabella sono presenti celle unite, il test di accessibilità non riesce per il file PDF di output convertito da un modulo XDP utilizzando il servizio di output (CQ-4285372).

* Foundation JEE: Se un server Forms di Experience Manager  è disconnesso da un cluster, i problemi di cache ne impediscono la riconnessione al server (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 è una versione importante che include correzioni e miglioramenti a livello di prestazioni, stabilità e sicurezza introdotti dai clienti a partire dalla release 6.5 di  **aprile 2019**. Può essere installato sopra a [!DNL Adobe Experience Manager] 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.6.

* [!DNL Experience Manager Assets] ora supporta gli archivi ZIP creati utilizzando l&#39;algoritmo Deflate64.

* La nuova colonna relativa alla data di creazione, ordinabile, è stata aggiunta nella visualizzazione a elenco DAM e nei risultati della ricerca di risorse nella visualizzazione a elenco.

* L’ordinamento delle risorse basato sulla colonna Nome è stato attivato nella visualizzazione Elenco.

* [!DNL Dynamic Media] ora supporta la funzione di ritaglio avanzato delle risorse video. Smart Crop è una funzione guidata di apprendimento automatico che ritaglia un video mentre si sposta il fotogramma per seguire il punto focale della scena.

* [!DNL Dynamic Media] supporta le immagini intelligenti.

* Possibilità di impostare le preferenze di [Out of Office](../forms/using/configure-out-of-office-settings.md) nei flussi di lavoro [!DNL Experience Manager].

* Possibilità di [condividere elementi Inbox o Inbox](../forms/using/configure-shared-queues-osgi.md) con altri utenti nei flussi di lavoro [!DNL Experience Manager].

* Possibilità di [generare comunicazioni interattive in modalità batch](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* È stata aggiornata la versione di jQuery inclusa nel pacchetto ContextHub alla 3.4.1.

### Risorse {#assets-6530-enhancements}

**Miglioramenti apportati al prodotto**

* [!DNL Experience Manager Assets] ora supporta gli archivi ZIP creati utilizzando l&#39;algoritmo Deflate64 (NPR-27573).

* La nuova colonna relativa alla data di creazione, ordinabile, viene aggiunta nella visualizzazione a elenco DAM e nei risultati della ricerca di risorse nella visualizzazione a elenco (NPR-31312).

* Nella vista a elenco, gli utenti possono ordinare l’elenco delle risorse utilizzando la colonna [!UICONTROL Nome] (NPR-31299).

* I file GLB, GLTF, OBJ e STL possono essere visualizzati in anteprima nella pagina [!UICONTROL Asset Details] in DAM (CQ-4282277).

* `ReplicationOnModifyListener` viene attivato per i nodi di blocco durante il caricamento di blocchi in  [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] ora supporta la funzione di ritaglio avanzato delle risorse video. Smart Crop è una funzione guidata per l&#39;apprendimento automatico che ritaglia un video mentre si sposta il fotogramma per seguire il punto focale della scena (CQ-4278995).

* [!DNL Dynamic Media] supporta le immagini intelligenti (CQ-422249).

* La visualizzazione di ricerca o ricerca è impostata come visualizzazione predefinita nel selettore Foundation se i parametri di query vengono passati nella richiesta (NPR-31601).

**Problemi risolti**

* I metadati di alcuni documenti PDF non vengono aggiornati e salvati nel PDF quando il titolo viene modificato (NPR-31629).

* La condivisione delle risorse non funziona per una risorsa con il carattere più (`+`) nel nome file (NPR-31547).

* Le modifiche nel modulo di ricerca predefinito Risorse Admin Search Rail non funzionano come previsto (NPR-31502).

* I suggerimenti non vengono visualizzati quando si utilizza Omnisearch nella visualizzazione delle risorse per la ricerca delle risorse (NPR-31496).

* I riferimenti alle risorse all&#39;interno delle raccolte non vengono aggiornati quando le risorse di riferimento vengono spostate in un&#39;altra posizione, nei casi in cui a una raccolta diversa fanno riferimento le stesse risorse da parte di utenti diversi (NPR-31486).

* I tag IPTC duplicati vengono aggiunti ai metadati delle risorse (NPR-31328).

* Il conteggio dei risultati della ricerca non viene aggiornato con precisione quando viene attivata una ricerca dalla barra laterale del filtro (NPR-31316).

* Tutte le caselle di controllo vengono deselezionate quando si deseleziona la casella di controllo di secondo livello nel filtro Tipo file e il testo nella barra di ricerca non è sincronizzato con le proprietà selezionate o deselezionate (NPR-31287).

* Tutti i membri (utenti/gruppi) non possono essere rimossi dalla sezione Membri di una cartella; quando si tenta di rimuovere tutti gli utenti, l&#39;utente connesso viene aggiunto all&#39;elenco (NPR-31171).

* Le risorse con il simbolo più (`+`) nel nome del file non possono essere eliminate (NPR-31162).

* Il menu a discesa Crea, visibile nel menu principale quando si seleziona una cartella, non mostra l&#39;opzione &quot;Cartella&quot; come opzione di creazione (NPR-30877).

* Selezione cartella L&#39;elemento azione Crea > Caricamento file non è presente quando l&#39;ACL per Rifiuta `jcr:removeChildNodes` e `jcr:removeNode` sul percorso viene applicato a un utente (NPR-30840).

* I flussi di lavoro DAM diventano obsoleti quando vengono caricate determinate risorse mp4, causando il blocco di tutti i flussi di lavoro rimanenti (NPR-30662).

* Errore di memoria insufficiente quando un file PDF di grandi dimensioni (di diversi Gigabyte) viene caricato in DAM e le relative risorse secondarie vengono elaborate (NPR-30614).

* Lo spostamento di massa delle risorse non riesce e viene visualizzato un messaggio di avviso (NPR-30610).

* I nomi delle risorse vengono modificati in lettere maiuscole quando si spostano le risorse da una cartella all&#39;altra in [!DNL Experience Manager] in esecuzione in modalità [!DNL Dynamic Media]-Scene7 (NPR-31630).

* Durante la modifica di un set di immagini remoto, si verifica un errore per l&#39;immagine che risiede nella cartella denominata uguale al nome della società Scene7 (NPR-31340).

* [!DNL Dynamic Media] le risorse contenenti riferimenti non vengono pubblicate (NPR-31180).

* Il completamento dei caricamenti dalla modalità [!DNL Dynamic Media]7-Scene7 a [!DNL Dynamic Media Classic] richiede troppo tempo (NPR-31048).

* L’area sensibile aggiunta a una risorsa immagine non è visibile tramite il visualizzatore immagini interattivo nella pagina dei dettagli della risorsa (NPR-30979).

* Vengono creati enormi processi di sling e il banner di elaborazione viene nuovamente visualizzato quando le azioni eseguite sulle risorse in [!DNL Experience manager Assets] vengono trasmesse ad Scene7 (NPR-30947).

* Si verifica un conflitto durante la creazione della copia in lingua delle risorse e delle risorse non caricate in Scene7 (NPR-30932).

* Le rappresentazioni dinamiche scaricate da [!DNL Experience Manager] in esecuzione in modalità [!DNL Dynamic Media]-ibrida sono interrotte (sono di tipo testo con contenuto &quot;impossibile trovare l&#39;immagine&quot; invece del tipo di contenuto immagine) (NPR-30876).

* [!DNL Dynamic Media] Il flusso di lavoro Codifica video non genera le miniature per il video migrato dalla modalità  [!DNL Dynamic Media Classic] a  [!DNL Dynamic Media]Scene7 su Adobe Experience Manager (CQ-4282011).

* IpsApiException durante la migrazione delle risorse da un’istanza all’altra tramite ID società Scene7 diversi (CQ-4280548).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene assimilato in [!DNL Experience Manager] (CQ-4283701).

* I pulsanti di scorrimento vengono visualizzati nel visualizzatore, se una risorsa 3D dispone di poche viste della fotocamera (CQ-4283322).

* Altezza contenitore errata di un modello 3D caricato visualizzato in anteprima nel visualizzatore dimensionale nella pagina Dettagli risorsa (CQ-4283309).

* I video non possono essere riprodotti con SmartCropVideoViewer su Internet Explorer 11 e Safari (CQ-4281422).

* L&#39;utilizzo del pulsante Sposta per spostare più risorse, da una cartella all&#39;altra, non riesce in [!DNL Experience Manager] in esecuzione in [!DNL Dynamic Media]-Scene7 runmode (CQ-4280384).

* I video distorti vengono visualizzati sui dettagli delle risorse quando il tipo MIME è diverso da MP4 (CQ-4279704).

* I video appena caricati in cartelle con profilo video restano nello stato di elaborazione anche dopo il completamento della percentuale di codifica al 100% (CQ-4279389).

* Lo spostamento delle risorse da una cartella crea un numero elevato di processi Sling (chiamate API Scene7) rispetto a quanto richiesto idealmente (CQ-4278664).

* I nomi del set di immagini vengono modificati in minuscolo in Scene7, quando viene creato un set di immagini (o un set di file multimediali) e vengono denominati con la convenzione di denominazione appropriata in DAM (CQ-4281112).

* Scene7 Migrator imposta lo stato di pubblicazione in modo errato (CQ-4263492).

* La ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) nella pagina dei risultati scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente nei frammenti di contenuto (CQ-4282898).

* I file PDF non sono indicizzati e il contenuto al loro interno non è ricercabile (CQ-4278916).

* Errore &quot;Gruppo non elencato dal selettore utente: previsto falso su uguale a vero&quot; viene osservato quando si aggiunge un gruppo di utenti chiuso con `principalName` e `authorizableId` diversi (CQ-4278177).

* La vista a colonne dell&#39;interfaccia utente delle risorse mostra tutti i percorsi indipendentemente dal percorso radice del tenant specifico (CQ-4278175).

* La ricerca del selettore delle risorse non funziona come previsto (CQ-4275886).

* Flussi di lavoro di rappresentazione non riusciti (CQ-4271928).

* DAM Event Purge elimina i dati dell&#39;evento più recente (`maxSavedActivities`) e contiene i dati creati in precedenza (NPR-31336).

* La pagina dei risultati della ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente (NPR-31307).

* La barra delle azioni e il conteggio delle risorse non si aggiornano quando si selezionano tutti gli elementi (cartelle o singole risorse) nell&#39;interfaccia utente touch (NPR-31118).

* Durante il polling per i dettagli del processo di una risorsa, viene visualizzata un&#39;eccezione in [!DNL Experience Manager] (CQ-4283569).

### Sites

* Se l&#39;ereditarietà LiveCopy è interrotta, nelle pagine di LiveCopy sono visualizzati i collegamenti per la copia della lingua invece dei collegamenti LiveCopy (NPR-30980).
* Per una nuova Blueprint, Se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza righe vuote per gli altri record (NPR-31182).
* Quando un utente aggiunge caratteri giapponesi o coreani nella proprietà description di un menu, nel menu vengono visualizzati caratteri distorti per il testo in lingua giapponese e coreana (NPR-31331).
* Editor Rich Text (RTE) non consente di inserire una tabella incorporata come voce di elenco (NPR-30879).
* Escluso, scaffolding Rich Text Editor (RTE). applica la dimensione del font in linea agli elementi, in modo imprevisto (NPR-31284).
* Quando un utente sposta lo stato attivo sui campi della barra a sinistra e utilizza una scelta rapida da tastiera per incollare il contenuto, viene incollato il contenuto degli Appunti dell’Editor pagina invece del contenuto copiato dai campi della barra a sinistra (NPR-31172).
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso dell’immagine viene memorizzato nel nodo componente invece del nodo multi-campo (NPR-30882).
* L&#39;API `ResponsiveGridExporter` non restituisce l&#39;interfaccia `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. Il pacchetto `com.day.cq.wcm.foundation.model.impl` è dichiarato come pacchetto privato (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il prefisso `editor.html` e `wcmmode=disabled` o in Publisher)., la richiesta termina con il codice di errore dello stato HTTP `500` (NPR-30743).
* Gli utenti non possono modificare la password e accedere alla pagina del profilo (NPR-31161).

### Interfaccia di ricerca e utente {#ui-interface-and-search}

* Quando si passa dalla vista a schede alla vista a elenco in una pagina dei risultati di ricerca, si verifica un ritardo prima che la pagina possa essere scorrevole (NPR-31286).

* La casella di controllo [!UICONTROL Seleziona tutto] è nascosta nella vista a elenco nell&#39;interfaccia utente [!DNL Sites] (NPR-31614).

* Il conteggio [!UICONTROL Select All] in una pagina di risultati della ricerca non è corretto (NPR-31120).

* L&#39;editor di metadati visualizza i tag che non esistono (NPR-31119).

### Traduzione {#translation}

* Due finestre a comparsa del calendario vengono visualizzate quando si seleziona l&#39;opzione Data scadenza in un processo di traduzione (NPR-31270).

### Platform

* L&#39;opzione Tipo mime nella console Web non funziona (NPR-31108).

* Il certificato client non è accettato durante la configurazione del single sign-on (NPR-31165).

* Gli aggiornamenti nella configurazione della dimensione del buffer per il servizio HTTP basato su Jetty non vengono salvati (NPR-30925).

* QueryBuilder supporta ora l&#39;ordine di `fn:name()` nelle query xpath (NPR-31322).

* L&#39;albero di attivazione duplicato viene creato al momento dell&#39;aggiornamento da [!DNL Experience Manager] 6.3 (NPR-31513).

* Le richieste inoltrate non conservano le intestazioni di risposta impostate durante l&#39;autenticazione Sling (NPR-30013).

* La ricerca all&#39;interno dei componenti del selettore non funziona (NPR-31692).

* Viene visualizzato un errore durante l&#39;associazione di un file ZIP a un post [!DNL Experience Manager Communities] a causa delle diverse versioni del bundle Apache POI e Apache Tika (NPR-31018).

* Il bundle `org.apache.sling.distribution.api` è nascosto nel gestore di configurazione e pertanto non è disponibile per i bundle personalizzati (NPR-31720).

### Progetti

* La sostituzione delle viste del calendario non funziona (NPR-31271).

### Portale marchio {#assets-brand-portal-6530}

**Miglioramenti apportati al prodotto**

* Il flusso di lavoro di importazione di Asset Sourcing in [!DNL Experience Manager Assets] viene modificato per recuperare solo le risorse appena create da [!DNL Brand Portal] a [!DNL Experience Manager] e ignorare le risorse già esistenti nella cartella NEW per evitare la replica (CQ-4278527).

**Problemi risolti**

* Quando si crea una nuova cartella Contribution nella funzione Asset Sourcing (CQ-4282825), viene visualizzata un’icona errata.
* Quando create una nuova cartella Contribution, una o entrambe le sottocartelle (NEW e SHARED) non vengono visualizzate all’interno della cartella Contribution (CQ-4282424).
* Il sistema genera un’eccezione se l’utente tenta di ripubblicare la cartella Contribution da [!DNL Experience Manager] a [!DNL Brand Portal] dopo aver ricevuto le nuove risorse nella cartella Contribution da [!DNL Brand Portal] end (CQ-4279740).
* La creazione di una cartella Contribution all’interno di una cartella Contribution (cartella nidificata) non è consentita per evitare la complessità (CQ-4278391).
* Il sistema genera un&#39;eccezione durante il caricamento dell&#39;elenco di utenti [!DNL Brand Portal] (file .csv) importato da [!DNL Experience Manager]  Admin Console. Nel file .csv sono obbligatori solo i campi Email, FirstName e LastName (CQ-4278390).

### Community {#communities-6530}

**Problemi risolti**

* I collegamenti rapidi per gestire i gruppi (Open/Edit/Publish/Delete Groups) non sono visibili agli amministratori della community (Group admin/Site admin) (NPR-31627).
* Un blog inviato viene visualizzato solo se la pagina viene aggiornata/ricaricata manualmente (NPR-31599).
* La query JCR utilizzata dalla funzione &quot;Mentions&quot; è sensibile alle maiuscole/minuscole e richiede troppo tempo per restituire i risultati (NPR-31475).
* [!DNL Experience Manager] 6.5 Il file UberJar genera un&#39;eccezione,  `cq-social-translation` il bundle è mancante nel file UberJar  [!DNL Experience Manager] 6.5 (NPR-31186).
* Librerie Databind di Jackson aggiornate alla versione 2.9.9.3 per risolvere nuove vulnerabilità (NPR-30967).
* I titoli di Attività e Notifiche non sono coerenti (NPR-30941).
* La paginazione non funziona correttamente nei [!DNL Communities] blog (NPR-30914).
* I report di analisi non vengono compilati nell&#39;ambiente di creazione [!DNL Experience Manager]. Viene visualizzata una pagina vuota (NPR-30913).

### Quercia {#oak}

* Aggiornamenti dell&#39;indice Lucene che rallentano il server di creazione (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per  [!DNL Experience Manager Forms]. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per [!DNL Experience Manager Forms] su JEE. Per ulteriori informazioni, vedere [Installare  Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare  Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Pacchetto di componenti aggiuntivi per Forms {#forms-add-on-package-6530}

**Moduli adattivi**

* Le stringhe contengono la chiave del dizionario durante la localizzazione dei moduli adattivi (NPR-31110).

**Comunicazione interattiva**

* **MissingNode.toString()** restituisce risultati imprecisi dopo aver aggiornato le librerie Jackson a 2.10.0 (NPR-31549).

* L&#39;editor di testo rimuove in modo casuale gli spazi dal testo copiato da Microsoft Word (NPR-31113).

**Gestione della corrispondenza**

* Le didascalie e le descrizioni comandi non vengono visualizzate durante la migrazione delle lettere dal LiveCycle ES4SP1 a [!DNL Experience Manager] 6.5 (NPR-31615).

* **Durante il salvataggio delle lettere come bozze (NPR-30463), la formattazione del flusso di testo non è più** supportata.

**Flusso di lavoro**

* Il flusso di lavoro OSGi non riesce a causa dell&#39;utilizzo della CPU al 100% (NPR-31233).

**Moduli HTML5**

* Quando si genera l’anteprima HTML5 di un modulo XDP, viene visualizzato uno sfarfallio durante l’aggiunta di istanze di un sottomodulo (NPR-30909).

#### Forms sul programma di installazione JEE {#forms-jee-installer-6530}

**Forms - Servizi basati su documenti**

* Il servizio Web SOAP che utilizza MTOM in un progetto .NET visualizza le eccezioni per i metodi AssemblerServiceClient invoke e HtmlToPDF2 (NPR-4281771).

* Vulnerabilità di sicurezza 2012-5784 e 2014-3596 trovata con AXIS 1.4 jar e correzione fornita con [AXIS1.4.1 jar](https://helpx.adobe.com/it/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015).

**JEE per Foundation**

* La configurazione dell&#39;azione non carica i nomi dei processi per Richiamare un&#39;azione di invio di un Forms Workflow (NPR-31478).

### Feature Pack inclusi {#feature-packs-included-6530}

>[!NOTE]
>
>Per i clienti [!DNL Experience Manager Forms], è essenziale installare il pacchetto del componente aggiuntivo [!DNL Experience Manager Forms] dopo l&#39;installazione di qualsiasi [!DNL Experience Manager] Service Pack, Cumulative Fix Pack o Feature Pack.

#### Forms - JEE di base {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Supporto Forms per  Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 è una versione importante che include correzioni e miglioramenti a livello di prestazioni, stabilità e sicurezza introdotti dai clienti dopo la data di disponibilità generale del  [!DNL Adobe Experience Manager] 6.5 nell&#39; **aprile 2019**. Può essere installato sopra a [!DNL Experience Manager] 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.3.
* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per [!DNL Adobe Target].
* Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Consulta la sezione sull’[utilizzo di risorse collegate](../assets/use-assets-across-connected-assets-instances.md).

* Ottimizza i filtri di tipo Documento con più tipi MIME per supportare le opzioni multivalore.
* Introduzione di un flusso di lavoro Rielabora esterno per il supporto di più risorse.
* Prestazioni [!DNL Dynamic Media] ottimizzate utilizzando i filtri risorse predefiniti per la replica.
* Ripristino delle opzioni di modifica di Assets relative a ritaglio/rotazione per DMS7.
* Implementazione di un’opzione per la disattivazione audio di un video durante il caricamento in VideoPlayer.
* Implementazione di una correzione per fare in modo che nella vista a colonne dell’interfaccia utente di Assets sia visualizzato solo il contenuto specifico del tenant.
* Implementazione di una correzione per consentire che le modifiche del pannello a soffietto dello stile rispecchino i risultati della ricerca.

### Assets

**Miglioramenti apportati al prodotto**

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Hotfix per CQ-4270245. Consulta la sezione sull’[utilizzo di risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets]Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

**Problemi risolti**

* I percorsi delle risorse negli URL e i metadati delle cartelle generati dall’API ACP non sono codificati in URL. GRANITE-26198: Hotfix per CQ-4271814
* Non è possibile aprire un archivio con una cartella con un segno percentuale (%) nel nome corrispondente utilizzando l&#39;interfaccia [!DNL Experience Manager Assets]. NPR-29989: Hotfix per CQ-4270467
* Interfaccia touch: Durante la procedura guidata di gestione della pubblicazione, i riferimenti vengono aggiunti dopo la pagina nel corpo della richiesta di pubblicazione, causando la pubblicazione di tutte le risorse dopo la pagina, e quando viene eseguito il rendering della pagina, alcune risorse nell’istanza di pubblicazione vengono perdute. NPR-29985: Hotfix per CQ-4270724
* La funzione Scollega di Assets non funziona per le risorse correlate il cui nome contiene caratteri speciali (caratteri che diventano con codifica URI). NPR-30387: Hotfix per CQ-4274446
* Quando si modifica un frammento di contenuto, la versione viene creata con l’utente errato.
* Errore durante la creazione di raccolte nel sistema basato su tenant. NPR-30114: Hotfix per CQ-4272948
* La vista a colonne dell’interfaccia utente di Assets non rispetta il percorso principale DAM del tenant corrente, ma accede a tutti i percorsi DAM del tenant. NPR-30636: Hotfix per CQ-4275481
* Possibilità di attacchi che sfruttano la vulnerabilità cross-site scripting (XSS) tramite la finestra di avviso File con limitazioni, in quanto l’immagine inserita può risultare visibile. NPR-30617: Hotfix per CQ-4270133
* MultiTenant: I tenant che salvano le proprietà della cartella osservano sia il messaggio di riuscita che il messaggio di errore che descrive l&#39;azione non è riuscito, &quot;Impossibile modificare le proprietà. Autorizzazioni insufficienti.” e questo genera confusione. NPR-30545: Hotfix per CQ-4275333
* La finestra di dialogo di Selettore risorse non consente la selezione della risorsa, pertanto non è possibile aggiornare l’origine utilizzando la funzionalità di sostituzione dell’origine correlata. NPR-30502: Hotfix per CQ-4275029
* [!UICONTROL Flusso di lavoro di ] risorse aggiornamento DAM: stato obsoleto durante il caricamento di file mp4 di grandi dimensioni. NPR-30480: Hotfix per CQ-4271352
* La funzionalità Crea attività di revisione non funziona a causa di un payload nullo che impedisce il completamento di tutte le azioni successive correlate all’attività di revisione. NPR-30468: Hotfix per CQ-4274263
* Problema di connettività di Tag avanzati di Adobe tramite DataPower. NPR-30026: Hotfix per CQ-4269457
* Nella vista a colonne dell’interfaccia utente di Assets viene generato un errore quando si prova ad aprire i filtri nella barra a sinistra. NPR-30501: Hotfix per CQ-4273862
* Quando si aggiungono gruppi sincronizzati da LDAP nelle proprietà di Gruppo utenti chiuso di una cartella risorse, il gruppo non viene salvato e recuperato. NPR-30615: Hotfix per CQ-4274689
* I campi di orientamento e stile per la ricerca con filtro non applicano il valore di completamento automatico alla query di ricerca. NPR-30620: Hotfix per CQ-4275724
* Con il collegamento di Condivisione risorse di una cartella il cui nome include spazi e il carattere “&amp;” vengono visualizzate schede grigie vuote per alcune risorse. NPR-30557: Hotfix per CQ-4270187
* Il modulo dello schema dei metadati della cartella non rileva automaticamente il tipo di dati e, di conseguenza, non crea l’elemento TypeHint correlato nell’invio del modulo. NPR-30599: Hotfix per CQ-4275227
* Le opzioni di modifica di Assets relative a ritaglio e rotazione vengono disabilitate dall’interfaccia utente di authoring di DMS7. NPR-30118: Hotfix per CQ-4273221
* La funzione Condividi collegamento non funziona sull&#39;istanza [!DNL Experience Manager] con la configurazione DMS7. NPR-30080, NPR-30492: Hotfix per CQ-4273651
* Aggiungendo il componente [!DNL Dynamic Media]-Scene7 alla pagina, la pubblicazione della pagina non attiva ogni volta la configurazione dmscene7. NPR-30641: Hotfix per CQ-4275962
* È stato aggiunto un IPSJobJournal in [!DNL Experience Manager] per creare un solo processo IPS (Intrusion Prevention Systems) per profilo di elaborazione. NPR-30490: Hotfix per CQ-4273614
* [!DNL Dynamic Media]: Aggiunta di filtri predefiniti per escludere le risorse dalla replica nel nodo di Publish. [!DNL Experience Manager] NPR-30538: Hotfix per CQ-4274678
* Introduzione di un flusso di lavoro Rielabora esterno per supportare più risorse e consentire la creazione della cartella come payload. Il flusso di lavoro prevede due passaggi: rielaborazione delle risorse senza alcun handle tramite la mappatura dei metadati al passaggio successivo e ricaricamento di tutte le risorse senza handle di risorsa a S7 in un singolo processo IPS. Per ulteriori dettagli, consultate Configurazione di Cloud Services [!DNL Dynamic Media]. NPR-30489: Hotfix per CQ-4272903
* Caricamento di un CSV non corretto dopo la cancellazione del CSV corretto. Hotfix per CQ-4277694, CQ-4277814
* Icona errata specifica delle cartelle contributi da rimuovere. Hotfix per CQ-4277580
* Selezionando un utente nel selettore utenti della scheda Contributo risorse, il nome dell’utente non viene visualizzato nella tabella e nella pagina delle proprietà della finestra di dialogo Elimina utente viene visualizzato testo errato. Hotfix per CQ-4277875
* Non è possibile aggiungere collaboratori alla cartella Contributo risorse dal selettore utente selezionando l’utente e facendo clic su Aggiungi. Hotfix per CQ-4277824, CQ-4278087
* La ricerca per nome utente in minuscolo non funziona nel selettore utente. Hotfix per CQ-4277958, CQ-4277930
* Gli utenti non amministratori possono pubblicare risorse in una nuova cartella di una cartella Contributo risorse. Hotfix per CQ-4278200
* L’utente DAM (non amministratore) non può scegliere di aggiungere collaboratori alla cartella Contributo risorse. Hotfix per CQ-4278192
* Il pulsante “Crea” è visibile nella cartella Contributo risorse. Hotfix per CQ-4277560
* L&#39;ordinamento della query di ricerca in base alla rilevanza restituisce i documenti [!DNL InDesign] insieme ai modelli [!DNL InDesign]. Hotfix per CQ-4273864
* Se l’utente dispone di un ID e-mail in maiuscolo, non potrà eseguire la consegna per le risorse ritirate in precedenza. Hotfix per CQ-4276575
* L’operazione Elimina si applica solo ai predefiniti selezionati; se la schermata aggiorna automaticamente l’elenco dopo l’operazione, vengono visualizzati altri predefiniti già aggiornati. Hotfix per CQ-4261461
* La configurazione di Cloud Services [!DNL Dynamic Media] in [!DNL Dynamic Media] modalità ibrida determina la creazione di più suite di rapporti vuote in [!DNL Analytics] e la mancata memorizzazione di ID suite di rapporti in [!DNL Experience Manager], con conseguente duplicazione delle suite di rapporti. Hotfix per CQ-4249780
* L&#39;operazione di ridenominazione in [!DNL Experience Manager] risorsa in nome duplicato non viene eseguita correttamente e non viene eseguita la sincronizzazione con Scene7. Hotfix per CQ-4276763
* I contenuti generati dall’utente non vengono visualizzati correttamente nel pannello del filtro di ricerca. Hotfix per CQ-4273875
* L’opzione Trova simile non è disponibile per le immagini TIFF. Hotfix per CQ-4278238
* Implementazione di un’opzione per disattivare l’audio dei video durante il caricamento in VideoPlayer. Hotfix per CQ-4266465
* Visualizzatori - VideoViewer: poster=none funziona in modo errato nel caso di un video esterno utilizzato. Hotfix per CQ-4265536
* L’icona di attesa è visibile durante la riproduzione video nei browser IE11 e MS Edge. Hotfix per CQ-4251539
* I file README dell’SDK 3.8 e dei visualizzatori 5.13 non vengono aggiornati e contengono informazioni provenienti da versioni precedenti. Hotfix per CQ-4273737
* Viene creata una versione del frammento di contenuto ancor prima del salvataggio delle modifiche. NPR-30616: Hotfix per CQ-4273088
* Sostituzione di Asset#getMetadata(String) con Asset#getMetadataValueFromJcr(String) nel processo miniature. NPR-30491: Hotfix per CQ-4273067
* Il caricamento di un file jpg causa l’attivazione di più istanze del messaggio: “Replica di ReplicateOnModifyWorker AGGIORNATA” per ciascuna risorsa, causando un peggioramento delle prestazioni.
* La decompressione dell’archivio ZIP mediante la funzione Estrai archivio causa problemi con le cartelle il cui nome contiene il segno di percentuale (%) nel titolo. NPR-29990: Hotfix per CQ-4270467

### Siti {#sites-6520}

* Se l&#39;ereditarietà LiveCopy è interrotta, nelle pagine di LiveCopy sono visualizzati i collegamenti per la copia della lingua invece dei collegamenti LiveCopy (NPR-30980).
* Per una nuova Blueprint, Se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza righe vuote per gli altri record (NPR-31182).
* Il plug-in Editor Rich Text (RTE) del componente Testo visualizza i caratteri distorti per il testo in lingua giapponese e coreana (NPR-31331).
* Editor Rich Text (RTE) non consente di inserire una tabella incorporata come voce di elenco (NPR-30879).
* L&#39;Editor Rich Text per la scaffolding (RTE) viene applicato in linea alle dimensioni dei font agli elementi in modo imprevisto (NPR-31284).
* Quando un utente si concentra sui campi della barra a sinistra e utilizza una scelta rapida da tastiera per incollare il contenuto, incolla il contenuto degli Appunti dell&#39;Editor pagina invece del contenuto copiato dai campi della barra a sinistra (NPR-31172).
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso dell’immagine viene memorizzato nel nodo componente invece del nodo multi-campo (NPR-30882).
* L&#39;API `ResponsiveGridExporter` non restituisce l&#39;interfaccia `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. Il pacchetto `com.day.cq.wcm.foundation.model.impl` è dichiarato come pacchetto privato (NPR-31398).
* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il prefisso `editor.html` e `wcmmode=disabled` o in Publisher), la richiesta termina con il codice di errore dello stato HTTP 500 (NPR-30743).

### WCM - Editor pagina {#wcm-page-editor-6520}

**Miglioramenti apportati al prodotto**

* Ottimizza i filtri di tipo Documento con più tipi MIME per supportare opzioni con più valori. Hotfix per CQ-4270694

### Gestione dei frammenti di contenuto {#content-fragment-management-6520}

* La query utilizzata dall’interfaccia utente dei modelli di frammenti di contenuto è molto lenta e alla fine genera un errore. Hotfix per CQ-4270807

### Interfaccia utente - Foundation {#ui-foundation}

* Con l’attivazione dei tasti di scelta rapida l’utente non può usare i tasti m, p ed e all’interno di specifiche interfacce utente. NPR-30355: Hotfix per GRANITE-26346
* La chiusura dell&#39; [!DNL Experience Manager Assets] interfaccia utente di ricerca non reimposta la barra a sinistra sulla selezione del contenuto, impedendo all&#39;utente di aprire la barra laterale del filtro la seconda volta in seguito. NPR-30509: Hotfix per CQ-4274716
* Ambiente multi-tenant: [!DNL Experience Manager Assets] la navigazione superiore dell&#39;interfaccia utente non è disponibile e viene generato un errore JavaScript. NPR-30104: Hotfix per GRANITE-26344

### Traduzione {#translation-6520}

* Problema di traduzione - Solo alcuni componenti vengono tradotti utilizzando la traduzione automatica. NPR-30079: Hotfix per CQ-4273764

### Piattaforma  {#platform-6520}

* [!DNL Experience Manager]Il mittente predefinito di non è in grado di inviare messaggi a un server SMTP remoto tramite TLS v1.2. NPR-30476: Hotfix per GRANITE-26605

### Progetti {#projects-6520}

* I valori dam:folderThumbnailPaths non vengono aggiornati e vengono visualizzate miniature vecchie anche dopo l’eliminazione delle risorse nella cartella. NPR-30424: Hotfix per CQ-4273667
* Quando si completa l’opzione “Sposta”, titolo e nome della risorsa restano invariati. NPR-30647: Hotfix per CQ-4276265

### Communities  {#communities-6520}

* Diagnostica sincronizzazione utenti è danneggiato e non funziona. NPR-30004, NPR-29943: Hotfix per CQ-4270287, CQ-4271348

### Sling {#sling}

* In seguito all’aggiornamento dell’istanza dalla versione 6.3.3.2 alla versione 6.5 vengono create configurazioni OSGi duplicate. NPR-30130: Hotfix per CQ-4274016

### Integrazione

* Il contenuto personalizzato non viene visualizzato correttamente nell’istanza di pubblicazione fino al riavvio dell’istanza. NPR-30377: Hotfix per CQ-4273706
* Durante la configurazione di Launch in un sito Web, l’indirizzo della libreria è preceduto da una barra (/) e questo causa ogni volta la necessità di un intervento manuale. NPR-30694: Hotfix per CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per  [!DNL Experience Manager Forms]. Vengono distribuite utilizzando un pacchetto aggiuntivo [!DNL Forms] separato. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per [!DNL Experience Manager Forms] su JEE. Per ulteriori informazioni, vedere [Installare  Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare  Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

Le principali evidenziazioni per i moduli [!DNL Experience Manager] 6.5.2.0 sono:

* È stata aggiunta l&#39;impostazione &quot;Auto&quot; a `RenderAtClient` nell&#39;API `PDFFormRenderOptions` per [!DNL Experience Manager] Forms OSGi.

#### Pacchetto di componenti aggiuntivi per Forms

**Integrazione back-end**

* Impossibile configurare il modello dati del modulo utilizzando un URL con bilanciamento del carico ospitato da AWS. NPR-30123: Hotfix per CQ-4273359
* Durante la creazione del modello dati del modulo (FDM) con il linguaggio WSDL (Web Service Definition Language), viene restituito il messaggio di errore `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type`: NPR-30477: Hotfix per CQ-4272921

**Gestione della corrispondenza**

* &quot;Crea rappresentazione dell’interfaccia utente di corrispondenza (interfaccia utente CCR) non riesce a intermittenza con l’errore riportato di seguito nella console:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Comunicazione interattiva**

* Un campo contrassegnato come obbligatorio nel modello dati del modulo viene visualizzato come obbligatorio nell’interfaccia utente di Crea corrispondenza (interfaccia utente CCR). NPR-30623: Hotfix per CQ-4274902

**Forms - Flusso di lavoro**

* Le variabili di output non mappate in cartelle esaminate causano errori di chiamata. Hotfix per CQ-4264451

**Moduli HTML5**

* Quando il codice o il progetto personalizzato viene distribuito per la seconda volta, la pagina non viene sottoposta a rendering e si verifica il seguente errore:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: Hotfix per CQ-4272509

* Quando si utilizza l’accesso desktop non visivo in modalità Sfoglia per leggere un modulo HTML5, il browser Chrome legge l’elemento “grafico” prima di qualsiasi file SVG nella struttura del modulo. NPR-30449: Hotfix per CQ-4274732

#### Programma di installazione di JEE per Forms

**Forms - Sicurezza dei documenti**

* L’applicazione di una firma con marca temporale non riesce e viene restituito l’errore: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: Errore di chiamata. NPR-30820: Hotfix per CQ-4275852

**Forms - Servizi basati su documenti**

* Se “SubmitURL” contiene una e commerciale (&amp;), nel registro sono presenti errori di analisi quando si effettua la richiesta POST al servlet renderpdf. NPR-30865: Hotfix per CQ-4278232

**Forms - JEE di base**

* Il servizio HTMLtoPDF non visualizza maxReuseCount nella console JMX. NPR-30134, NPR-30304: Hotfix per CQ-4273763
* L&#39;aggiunta o la modifica di una connessione a un servizio Web richiamando i servizi Web da [!DNL Experience Manager Forms] Workbench genera un errore: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Hotfix per CQ-4273217

### Feature Pack inclusi

>[!NOTE]
>
>Per i clienti [!DNL Experience Manager Forms], è essenziale installare il pacchetto del componente aggiuntivo [!DNL Experience Manager Forms] dopo l&#39;installazione di qualsiasi [!DNL Experience Manager] Service Pack, Cumulative Fix Pack o Feature Pack.

#### Siti {#sites-feature-packs-included}

* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per [!DNL Adobe Target]. NPR-29189: Hotfix per CQ-4249782

#### Forms - Servizi basati su documenti {#forms-document-services-1}

* È stata aggiunta l&#39;impostazione &quot;Auto&quot; a `RenderAtClient` nell&#39;API `PDFFormRenderOptions` per [!DNL Experience Manager Forms] OSGi. NPR-30759: Hotfix per CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 è una versione importante che include correzioni e miglioramenti a livello di prestazioni, stabilità e sicurezza introdotti dai clienti dopo la data di disponibilità generale del  [!DNL Adobe Experience Manager] 6.5 nell&#39; *aprile 2019.* Può essere installato sulla parte superiore di  [!DNL Experience Manager] 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Abilitazione dell’inclusione dello stato dell’interfaccia utente dinamica negli eventi di tracciamento come attributi personalizzati.
* È stato incluso il supporto per la distribuzione di risorse video a 360 gradi in modalità [!DNL Dynamic Media]-Scene7.
* Abilitata la funzione *Parola giapponese Wrap* tramite il plug-in stili di Editor Rich Text. Per ulteriori informazioni, vedere [Configurare il ritorno a capo automatico in giapponese](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Risorse

* Aggiornamento dell’interfaccia DMGGateway di DAM per il supporto multipart di S3. NPR-29740: Hotfix per CQ-4226303
* L&#39;anteprima delle rappresentazioni genera un errore `Only empty tenantId is currently supported` dopo l&#39;aggiornamento a [!DNL Experience Manager] 6.5. NPR-29986: Hotfix per CQ-4272353
* La finestra di dialogo Elimina non è visibile per consentire l’eliminazione di lavori. NPR-29720: Hotfix per CQ-4271074
* Dopo aver aggiunto il titolo della risorsa nella pagina delle proprietà, quando un utente tenta di chiudere la pagina, [!DNL Experience Manager] apre di nuovo la pagina delle proprietà. NPR-29627: Hotfix per CQ-4264929
* VersioningTimelineEventProvider deve fornire la versione principale unitamente al nodo della versione nt: del tipo. Hotfix per GRANITE-26063
* È stata implementata la possibilità di caricare e riprodurre video sferici a 360 gradi in modalità [!DNL Experience Manager] DM-Scene7. Hotfix per CQ-4265131
* Live Copy recupera lo stato non corretto in caso di modifica dell’origine. Hotfix per CQ-4265451
* Abilitazione del supporto per l’utilità di gestione di più siti per [!DNL Experience Manager Assets]. Hotfix per CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] nell’interfaccia deve essere visualizzata una voce aggiuntiva per la versione corrente della risorsa nella cronologia del tempo, in cui viene visualizzato il commento di archiviazione più recente da  [!DNL Adobe Asset Link]. Hotfix per CQ-4262864
* Nella timeline dei frammenti di contenuto viene visualizzato un messaggio di errore in caso di assenza di proprietà. Hotfix per CQ-4272560
* Problema relativo al lettore video di Scene7 quando viene espanso a schermo intero. Hotfix per CQ-4266700
* ZoomVerticalViewer: i pulsanti di spostamento non devono essere visualizzati se viene utilizzata una singola risorsa immagine. Hotfix per CQ-4264795
* Se si elimina un nodo figlio nella Live Copy, è necessario scollegare liveRelationship. Hotfix per CQ-4270395
* Lo schema di metadati contiene solo elementi della configurazione globale; quelli del tenant attivo non sono presenti. Il valore dell’URL di formPath viene ripristinato a quello predefinito anche se modificato. NPR-29945: Hotfix per CQ-4262898
* La pubblicazione dei predefiniti per immagini su [!DNL Brand Portal] non riesce con il codice di errore 500. NPR-29510: Hotfix per CQ-4268659

### Siti

* Le proprietà vuote e multiple non vengono propagate dalla blueprint durante il rollout. Il ripristino di Live Copy con la blueprint non funziona per i componenti. NPR-29253: Hotfix per CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, se utilizzato con `Multifield`, memorizza la `fileReferenceParameter` a livello di componente invece che a livello di campo multiplo. NPR-29537: Hotfix per CQ-4266129
* È stato migliorato il componente di testo [!DNL Experience Manager] e l’editor di testo in giapponese. NPR-29785: Hotfix per CQ-4265090
* La pagina ripristinata con Timewarp deve fare riferimento all’immagine corretta al momento del controllo delle versioni. NPR-29431: Hotfix per CQ-4262638
* Un problema relativo all&#39;ereditarietà dei nodi Style System dall&#39;elemento padre all&#39;elemento secondario. NPR-29516: Hotfix per CQ-4270330
* Messaggio di errore durante la configurazione del messaggio social network per l&#39;autenticazione [!DNL Facebook]. NPR-29211: Hotfix per CQ-4266630
* La miniatura di cui è stato eseguito il rendering nel frammento di contenuto mostra la rappresentazione interna del calendario per il campo Data e ora. NPR-29531: Hotfix per CQ-4269362
* All’apertura della scheda Autorizzazioni nell’implementazione di Coral2 non viene visualizzato alcun pulsante. Hotfix per CQ-4269419

### Commerce

* ConstraintViolationException durante l’esecuzione della migrazione lenta dei contenuti per l’e-commerce. NPR-29247: Hotfix per CQ-4264383

### Gestione dei frammenti di contenuto

* Errore di analisi durante l&#39;apertura di un frammento di contenuto con caratteri dollaro `($)` e parentesi graffa aperta `({)`. Hotfix per CQ-4270266

### Frammenti esperienza

* Esporta [!DNL Experience Manager] frammenti esperienza in [!DNL Adobe Target]. Hotfix per CQ-4265469
* L’esportazione di frammenti esperienza come destinazione non riesce con l’immagine intelligente. Hotfix per CQ-4269606

* L’utente rimane bloccato quando prova a spostare i frammenti esperienza tramite Omnisearch nella vista a schede. Hotfix per CQ-4263848

### WCM - Editor pagina

* Vulnerabilità cross-site scripting (XSS) rilevabile quando si utilizza un selettore non valido. Hotfix per CQ-4270397

### Replica

* I dati forniti dall&#39;utente non sono preceduti da un carattere di escape nell&#39;output del componente `cq/replication/components/agent`, con conseguente vulnerabilità XSS (Cross-Site Scripting) memorizzato. Hotfix per CQ-4266263

### Flusso di lavoro

* Il campo del selettore del calendario di Partecipante finestra di dialogo è danneggiato. NPR-29727: Hotfix per CQ-4270423

### WCM - Editor SPA

* Abilitazione del recupero da un endpoint remoto di contenuti di cui è già stato eseguito il rendering. Hotfix per CQ-4270238
* Aggiunta di avvisi nei registri quando viene aperta una pagina di modello per applicazione a pagina singola di cui viene eseguito il rendering sul lato server. Hotfix per CQ-4270238

### WCM - MSM

* Con l&#39;aggiornamento a [!DNL Experience Manager] 6.4.3, l&#39;implementazione di Multi-Site Manager richiede molto tempo. Hotfix per CQ-4271410

### Integrazione

* Credenziali BrightEdge non valide ed errore di connessione. NPR-29168: Hotfix per CQ-4265872

* Viene visualizzato un messaggio di eccezione quando si tenta di modificare e salvare la configurazione di avvio [!DNL Experience Manager]. NPR-29176: Hotfix per CQ-4265782/CQ-4266153

### Interfaccia utente

* Aggiunta del supporto per il tracciamento degli stati dell’interfaccia utente dinamica come attributi personalizzati durante il tracciamento di determinati eventi nell’API di tracciamento di base. Hotfix per GRANITE-26283
* Impossibile impostare la funzione di tracciamento sul pulsante di invio. Hotfix per GRANITE-26326
* La procedura guidata non riesce a impostare la funzione di tracciamento sul pulsante di invio. NPR-29995, NPR-30025: Hotfix per CQ-4264289

### Community

* Impossibile allineare i nuovi badge nel menu a discesa sulla pagina del profilo del membro. NPR-29381: Hotfix per CQ-4267987
* Visitatori e membri, senza privilegi di moderatore, possono visualizzare i post non approvati/in sospeso incollando l’URL. NPR-29724: Hotfix per CQ-4271124, CQ-4271441
* Durante l’accesso dell’utente alla community è possibile notare un tempo di risposta elevato, fino a 40-50 secondi. NPR-29677: Hotfix per CQ-4269444

### Replica

* Il componente Agente di replica è soggetto a una vulnerabilità per cui informazioni sensibili vengono rivelate a utenti non autorizzati. NPR-29611: Hotfix per GRANITE-25070

* Falla nella sessione durante OAuth per ogni replica su [!DNL Brand Portal]. NPR-30001: Hotfix per GRANITE-26196

### Progetti

* La pubblicazione [!DNL Experience Manager Assets] dalla [!DNL Experience Manager] cartella Author /content/dam/mac a [!DNL Brand Portal] non funziona. NPR-29819: Hotfix per CQ-4271118

### Piattaforma

* HtmlLibraryManager elimina tutti i contenuti di crx-quickstart in seguito all’annullamento della validità della cache. NPR-29863: Hotfix per GRANITE-26197

### Felix

* I dettagli sull’utilizzo della memoria non vengono visualizzati nella console del sistema quando si utilizza Java 11\. NPR-29669

### Forms

Le principali evidenziazioni per [!DNL Experience Manager Forms] 6.5.1.0 sono:

* Solo OSGi: È stato aggiunto un nuovo attributo `PAGECOUNT` in Output e Forms Service.

* Solo OSGI: È stato abilitato il supporto per la creazione di file PDF statici tramite Forms Service.
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root.
* Abilitazione del supporto per ADFS v3.0 per l’integrazione On-Premise di Dynamics.

#### Pacchetto di componenti aggiuntivi per Forms

**Integrazione con il back-end**

* Errore durante il recupero del linguaggio WSDL (Web Service Definition Language) protetto. NPR-29944: Hotfix per CQ-4270777
* Se [!DNL Experience Manager Forms] è installato su IBM WebSphere, la creazione di un modello dati modulo basato su SOAP non riesce. Hotfix per CQ-4251134
* Abilitazione del supporto per ADFS (Active Directory Federation Services) v3.0 per l’integrazione On-Premise di Microsoft Dynamics. Hotfix per CQ-4270586
* Quando si modifica il titolo di un’origine dati, il modello dati del modulo non visualizza il titolo aggiornato. Hotfix per CQ-4265599
* Se il nome di un&#39;entità o di un attributo contiene trattino o spazio, le espressioni non riescono a valutare tali entità e attributi. Hotfix per CQ-4225129

* L&#39;output non è corretto quando nell&#39;output della stringa primitiva sono presenti due punti. Hotfix per CQ-4260825

* Anche quando non è previsto alcun contenuto dall’output dell’API REST, l’operazione di richiamo del modello dati del modulo genera un errore. Hotfix per CQ-4268828

**Moduli adattivi**

* Impossibile aggiungere una nuova istanza nel frammento di modulo adattivo durante il caricamento lento. NPR-29818: Hotfix per CQ-4269875
* Il componente Verifica non registra o visualizza errori per i modelli della documentazione. Hotfix per CQ-4272999
* Aggiunta del supporto per disabilitare l’editor di layout per Moduli adattivi. Hotfix per CQ-4270810
* È stato ripristinato il passaggio di verifica per Forms adattivo in [!DNL Experience Manager] 6.5. Hotfix per CQ-4269583

* Errori di convalida del campo modulo adattivo [!DNL Adobe Sign]. Hotfix per CQ-4269463
* Quando un&#39;istanza [!DNL Experience Manager Forms] contiene più di 20 frammenti di modulo adattivo e il nome di tutti i frammenti di modulo inizia con la stessa stringa, la ricerca restituisce solo 20 frammenti creati o solo 20 frammenti recenti. Hotfix per CQ-4264414, CQ-4264914

* Problemi di prestazioni quando l’app Moduli adattivi viene utilizzata con set di dati di grandi dimensioni. . Hotfix per CQ-4235310

* Se l’accesso viene effettuato tramite un account anonimo in un’istanza pubblicata, lo script GuideRuntime non viene caricato. Hotfix per CQ-4268679

**Forms - Comunicazione interattiva**

* Il modello di comunicazione interattiva non elenca i componenti intestazione e piè di pagina nell’elenco dei componenti consentiti. Hotfix per CQ-4237895
* Quando crei un modello di stampa per comunicazioni interattive contenente un campo immagine, il titolo del grafico è impostato su una stringa vuota. Hotfix per CQ-4264772
* Il colore della linea di un grafico, se eliminato, è impostato su non definito. Hotfix per CQ-4264762
* Le modifiche al livello di layout apportate al frammento del documento non vengono visualizzate quando si eseguono modifiche alla sincronizzazione. Hotfix per CQ-4266054
* L’elemento del modello dati modulo all’interno di un frammento di documento associato a un campo di testo non visualizza l’icona di ereditarietà e consente l’associazione. Hotfix per CQ-4261089
* L’API di rendering del canale di stampa non include l’opzione per passare dati come parametro nell’API. Hotfix per CQ-4263540
* Le impostazioni dell&#39;agente non sono visibili perché la casella di controllo Modificabile dall&#39;agente viene deselezionata quando il tipo di binding viene modificato da Frammento di testo a Nessuno/Oggetto modello dati per il campo/variabile Stringa. Hotfix per CQ-4261953
* Durante l&#39;invio dell&#39;interfaccia utente dell&#39;agente, il file json di dati Web risultante memorizza le informazioni per i campi non associati annullati dall&#39;ereditarietà. Hotfix per CQ-4265621

**Forms - Flusso di lavoro**

* Quando un modulo viene nuovamente inviato dalla casella in uscita dell’app Moduli adattivi, si verifica una perdita di dati. NPR-28345: Hotfix per CQ-4260929
* I documenti non vengono chiusi durante il salvataggio per i casi non variabili. Hotfix per CQ-4269784
* L’app Moduli adattivi non supporta più Microsoft Windows 8.1. Hotfix per CQ-4265274
* Quando un&#39;immagine di oltre 2 MB viene associata a un modulo come allegato a livello di campo nella versione Android dell&#39;app [!DNL Experience Manager Forms], l&#39;app subisce un arresto anomalo. Hotfix per CQ-4265578

* Abilitazione delle opzioni di precompilazione per il canale di stampa delle comunicazioni interattive nell’attività Assegna. Hotfix per CQ-4265577
* Gli utenti non possono visualizzare un’attività condivisa finché non diventano membri del gruppo a cui è assegnata l’attività. Hotfix per CQ-4248733
* Il salvataggio o l’invio di applicazioni JEE nell’app Moduli adattivi è bloccato in Windows. Hotfix per CQ-4268704
* Il modello dati del modulo associato alla variabile del modello dati del modulo non è visibile. Hotfix per CQ-4266554
* Assenza del supporto per la variabile di stato della firma del documento quando viene utilizzato il supporto per le variabili. Hotfix per CQ-4266312
* Gli invii dall’area di lavoro non riescono se è presente il carattere umlaut. Hotfix per CQ-4263172
* In una configurazione aggiornata, se il flusso di lavoro viene aperto per la modifica, nell’interfaccia utente della cartella di controllo (interfaccia utente) viene visualizzato un errore invece del nome del flusso di lavoro. Hotfix per CQ-4238579

**Forms - Gestione**

* Quando viene caricata un’estensione diversa da xsd o schema.json, il caricamento non viene eseguito e non viene generato alcun messaggio di errore. Hotfix per CQ-4266716

**Forms - Gestione della corrispondenza**

* [!DNL Experience Manager Forms] 6.5 L&#39;interfaccia utente Crea corrispondenza (interfaccia utente CCR) non riesce ad aprire la corrispondenza creata con  [!DNL Experience Manager Forms] 6.3. Hotfix per CQ-4266392
* La funzione di somma in XDP non funziona se i dati DDE sono di tipo numero. Hotfix per CQ-4227403
* La logica di annullamento validità della cache in memoria delle lettere deve essere aggiornata, perché quando viene pubblicata una risorsa, l’ora dell’ultima modifica non viene aggiornata. Hotfix per CQ-4250465
* Impossibile pubblicare il frammento di documento, DD e lettere. Hotfix per CQ-4272893

#### Programma di installazione di JEE per Forms

**PDF Generator**

* La conversione di file CAD in PDF non riesce con JDK a 64 bit. NPR-29924, NPR-29925: Hotfix per CQ-4272113
* Sostituzione del nome di PhantomJS in WebToPDF per la conversione HTMLtoPDF. NPR-29933: Hotfix per CQ-4234545
* Viene generato un errore durante la conversione del file ZIP in PDF. Hotfix per CQ-4268628

**Forms - Designer**

* Quando viene eseguito un controllo completo dell&#39;accessibilità sul PDF statico creato con [!DNL Experience Manager Forms Designer], il controllo della lingua principale non riesce a causa dell&#39;attributo della lingua mancante. Hotfix per CQ-4272923, CQ-4271002

**Forms - Sicurezza dei documenti**

* La firma digitale con il modulo di sicurezza hardware non funziona in OSGi Linux su Java 11 e Java 8\. NPR-29838: Hotfix per CQ-4270441
* La firma digitale con il modulo di sicurezza hardware non funziona in JEE Linux e in tutti i server app supportati, ad esempio JBoss e Websphere. NPR-29839: Hotfix per CQ-4266721
* Durante la verifica delle firme in un PDF tramite l’uso di firme elettroniche avanzate PDF (PAdES) viene generata l’eccezione InvalidOperationException. NPR-29842: Hotfix per CQ-4244837
* Aggiunta del supporto per Document Security Extension per Office 2019\. Hotfix per CQ-4254369, CQ-4259764

**Forms - Servizi basati su documenti**

* La conversione del PDF in PDF/A-1b con il campo Modulo non ha il codice di aspetto. NPR-29940: Hotfix per CQ-4269618

* OSGi: Impossibile determinare il numero di pagine generate durante il rendering. NPR-28922: Hotfix per CQ-4270870
* Abilitato il supporto per i file PDF statici tramite Forms Service in [!DNL Experience Manager Forms OSGi]. NPR-28572: Hotfix per CQ-4270869
* Impossibile modificare le autorizzazioni per XMLForm.exe. NPR-29828, NPR-29237: Hotfix per Q-4267080
* Il PDF statico creato dal modulo di output del server [!DNL Experience Manager Forms] non compila l&#39;attributo/tag della lingua con la lingua del documento creato. NPR-27332: Hotfix per CQ-4271002

**Forms - JEE di base**

* Il file pdfg_srt non è disponibile negli artefatti finali e questo impedisce l’esecuzione del programma di installazione. NPR-29854: Hotfix per CQ-4270137
* LCBackupMode.sh non funziona. NPR-29840: Hotfix per CQ-4269424
* È necessario rimuovere il riferimento alla porta UDP dall’interfaccia utente per WebSphere. Hotfix per CQ-4264782

### Feature Pack inclusi

#### Risorse - Incluse

* Abilitazione del supporto per l’utilità di gestione di più siti per [!DNL Experience Manager Assets]. Per ulteriori informazioni, consultate [Riutilizzare le risorse utilizzando MSM per  risorse di Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/reuse-assets-using-msm.html). NPR-29199: Hotfix per CQ-4259922

#### Siti - Inclusi

* Esporta [!DNL Experience Manager] frammenti esperienza in [!DNL Adobe Target]. Per ulteriori dettagli, consultate [Il provider di rewriter del collegamento del frammento esperienza - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Hotfix per CQ-4265469

#### Forms - Servizi basati su documenti - Incluso

* Solo OSGi: È stato aggiunto un nuovo attributo PAGECOUNT in Output e Forms Service. NPR-28922: Hotfix per CQ-4270870
* Solo OSGi: È stato abilitato il supporto per la creazione di file PDF statici tramite Forms Service. NPR-28572: Hotfix per CQ-4270869
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root. NPR-29237: Hotfix per CQ-4267080

### Bundle OSGi e pacchetti di contenuti

I seguenti documenti di testo elencano i bundle OSGi e i pacchetti di contenuto inclusi in [!DNL Experience Manager] 6.5.1.0

Elenco dei bundle OSGi inclusi in [!DNL Experience Manager] 6.5.1.0

[Ottieni file](assets/6_5-bundle-list.txt)

Elenco dei pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.1.0

[Ottieni file](assets/6_5-content-package-list.txt)
