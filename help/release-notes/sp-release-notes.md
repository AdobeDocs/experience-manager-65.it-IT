---
title: ' Adobe Experience Manager 6.5 - Note sulla versione del Service Pack'
description: Note sulla versione specifiche di Adobe Experience Manager 6.5 Service Pack 5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '4496'
ht-degree: 7%

---


#  Adobe Experience Manager 6.5 - Note sulla versione del Service Pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.5.0 |
| Tipo | Versione Service Pack |
| Data | 04 giugno 2020 |
| URL di download | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Contenuto nell&#39; Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

 Adobe Experience Manager 6.5.5.0 è un aggiornamento importante che include nuove funzioni, miglioramenti fondamentali richiesti dai clienti e miglioramenti a prestazioni, stabilità e sicurezza, rilasciati a partire dalla release 6.5 di **aprile 2019**. Può essere installato sopra  Adobe Experience Manager 6.5.

Alcune funzioni chiave e miglioramenti introdotti  Adobe Experience Manager 6.5.5.0 includono:

* Personalizzare i nomi delle colonne visualizzati nella casella in entrata  Adobe Experience Manager.

* È stata migliorata l&#39;accessibilità in varie aree in  Web Content Management (WCM) di Experience Manager, come Editor pagina, Componenti di base, Editor Rich Text e l&#39;interfaccia utente Amministratore.

* Salvate un file [!DNL Interactive Communication] come bozza.

* Supporto [!DNL Oracle WebLogic 12] per Forms di  Experience Manager su JEE.

* Gestione delle eccezioni migliorata nel flusso dell&#39;interfaccia [!DNL Adobe Experience Manager Assets] utente.

* Per ottenere l’URL di pubblicazione per Dynamic Media Scene7, `getRemoteAssetPublishURL` viene aggiunto un nuovo metodo all’ `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` interfaccia.

* [Miglioramenti](#assets-6550) dell&#39;accessibilità in [!DNL Adobe Experience Manager Assets] conformità con le linee guida WCAG (Web Content Accessibility Guidelines).

* È stata rimossa l&#39;integrazione di Package Share dall&#39;interno  Adobe Experience Manager.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.3.

Per un elenco completo delle funzioni, degli elementi salienti e delle caratteristiche principali introdotti  service pack 5 dell&#39;Experience Manager 6.5, vedere [Novità  Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Di seguito è riportato l&#39;elenco delle correzioni fornite nella release [!DNL Experience Manager] 6.5.5.0.

### [!DNL Sites] {#sites-6550}

*  Siti Experience Manager offre l’opzione per pubblicare o annullare la pubblicazione di una pagina dal relativo alias. L&#39;opzione non funziona (NPR-33415).
* Quando un Contenitore di layout viene eliminato da un modello contenente più modelli, il rendering del modello non viene eseguito correttamente (NPR-33347).
* Quando una pagina di siti di Experience Manager  fa parte di un set di contenuti di grandi dimensioni con più Live Copy, l&#39;anteprima della cronologia delle versioni della pagina non viene caricata (NPR-33311).
* Quando si utilizza il comando Sposta per rinominare una pagina di siti di Experience Manager , il titolo della pagina non viene aggiornato (NPR-33264).
* Quando si spostano le pagine nella vista a colonne, le colonne scompaiono (NPR-33216).
* Quando il nome di un componente locale in una copia per lingua è identico al nome di un componente nel blueprint e il componente viene implementato dal blueprint, il termine non `_msm_moved` viene aggiunto al nome del componente locale (NPR-33208).
* Il servlet Page Redirect aggiunge .html a un URL di siti di  dove ResourceType non è `cq:Page` (NPR-33176).
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
* Il controllo dello stato di Dispatcher visualizza un messaggio di `Invalid cookie header` avviso nei file di registro (NPR-33629).

### [!DNL Assets] {#assets-6550}

**Miglioramenti dell&#39;accessibilità in  risorse Experience Manager**

* È ora possibile attivare l&#39;elenco [!UICONTROL Commenti] e fare clic sull&#39;opzione per [!UICONTROL creare] commenti sulla versione in [!UICONTROL Crea nuova versione] nel pannello [!UICONTROL Timeline] delle risorse (NPR-33424).

* Ora è possibile accedere all&#39;opzione [!UICONTROL Visualizza impostazioni] per le risorse e modificare le impostazioni nella finestra di dialogo Impostazioni  visualizzazione tramite i tasti della tastiera (NPR-33420).

* La casella di riepilogo a comparsa della casella combinata (in vari campi su pagine diverse) ora mostra le voci come un elenco di opzioni che possono essere annunciate dagli assistenti vocali (NPR-33516).

* La funzionalità di ordinamento delle intestazioni ordinabili (nella vista a elenco, nella vista [!UICONTROL Timeline] e nella pagina [!UICONTROL Gestisci pubblicazione] ) ora è annunciata dagli assistenti vocali e i controlli di ordinamento sulle intestazioni delle colonne sono accessibili tramite tastiera (NPR-32979).

* Gli elementi su cui è possibile fare clic, come schede per commenti, aggiornamenti delle versioni, caselle combinate e icone chevron dei menu, ora possono essere attivati e interagire con l&#39;utilizzo di una tastiera (NPR-33514).

* Funzionalità (o scopo dell&#39;azione) delle icone delle informazioni (per uso, impression e clic) nella vista  Insights ora vengono annunciate correttamente dagli assistenti vocali (NPR-33513).

* Read-only form fields (for example disabled fields on [!UICONTROL Basic tab] of asset [!UICONTROL Properties]) are now focusable using keyboard (NPR-33493, CQ-4273031).

* Le etichette in vari campi di input sono ora etichette permanenti (quindi accessibili) e non solo etichette segnaposto, scomparse al momento dell&#39;immissione del testo (NPR-33475).

* Diversi livelli di intestazione (come titoli di pagina e intestazioni di sezione) vengono ora percepiti come titoli con livelli diversi per gli utenti degli assistenti vocali (NPR-33471).

* Gli elementi interattivi dell&#39;interfaccia utente, come i collegamenti e le opzioni (nelle opzioni di intestazione e zoom della pagina delle risorse, nella navigazione delle cartelle), sono ora accessibili tramite una tastiera (NPR-33468, CQ-4271412).

* Gli indicatori di avanzamento di [!UICONTROL Opzioni], [!UICONTROL Ambito]e Flussi [!UICONTROL di lavoro nella pagina] Gestisci pubblicazione  ora vengono letti correttamente dagli assistenti vocali come indicatori di avanzamento, invece delle schede (NPR-33416).

* Il colore delle icone di valutazione a stella (ad esempio nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] nelle [!UICONTROL proprietà] della risorsa o nella vista a schede) viene modificato per rendere visibile il contrasto appropriato agli utenti con una visione limitata e senza percezione del colore (NPR-33414).

* È ora possibile accedere alla freccia rivolta verso l&#39;alto accanto al campo [!UICONTROL Commento] nella pagina dei dettagli delle risorse tramite i tasti di scelta rapida (NPR-33397).

* Gli stati espansi e compressi della finestra di dialogo [!UICONTROL Tag] in [!UICONTROL Proprietà] risorsa e nella barra di navigazione a sinistra (nell’interfaccia utente delle risorse) ora vengono annunciati correttamente dagli assistenti vocali (NPR-33396).

* Titles of all the browsed pages on [!DNL Adobe Experience Manager] Assets are now unique (NPR-33343).

* Quando si naviga nella struttura ad albero, diversi elementi del controllo della visualizzazione ad albero vengono ora correttamente annunciati dagli assistenti vocali (NPR-33304).

* Sono ora accessibili diverse versioni delle risorse nella visualizzazione [!UICONTROL Timeline] nella pagina dei dettagli delle risorse tramite i tasti di scelta rapida (NPR-33283).

* I nomi dei suggerimenti di ricerca visualizzati nella casella combinata Omnisearch ora vengono annunciati dagli assistenti vocali quando si utilizza la funzionalità di ricerca (NPR-33280).

* Gli elementi selezionabili e il collegamento [!UICONTROL Vai a nella barra laterale]  Riferimenti vengono ora annunciati dagli assistenti vocali come elementi selezionabili (NPR-33278).

* Le informazioni sulla struttura della tabella (come riga 1, cella 1, tabella) della finestra di dialogo [!UICONTROL Condividi collegamento] non vengono più annunciate dagli assistenti vocali all&#39;apertura della finestra di dialogo (NPR-33268).

* Lo scopo di vari elementi della casella combinata (ad esempio il campo Percorso e l&#39;opzione per aprire la finestra di dialogo di selezione nella scheda Base delle proprietà della risorsa) ora viene annunciato correttamente dagli assistenti vocali (NPR-33235).

* Le informazioni che le righe nella tabella di visualizzazione a elenco sono selezionabili vengono ora comunicate agli utenti dell&#39;assistente vocale quando sono attivate dalla tastiera. Quando un puntatore passa sulle righe, gli assistenti vocali annunciano le informazioni (NPR-33234).

* Options (having [!UICONTROL x]) to remove each of the selected tags below the [!UICONTROL Tags] field in [!UICONTROL Basic] tab of [!UICONTROL Properties] are now accessible to screen readers (NPR-33206).

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

* [!UICONTROL Le opzioni Seleziona], [!UICONTROL Scarica], [!UICONTROL Proprietà]e [!UICONTROL Altre azioni] sulle schede delle risorse nella vista  Insights sono ora accessibili tramite tastiera (NPR-32609).

* I contenuti visivamente nascosti (ad esempio, contenuti della barra di intestazione sui risultati della ricerca) non vengono più annunciati dagli assistenti vocali quando vi si accede utilizzando la tastiera (NPR-32606).

* Lo scopo delle etichette sui controlli per passare ai mesi successivi e precedenti nel selettore della data del calendario è ora annunciato dagli assistenti vocali (NPR-32604).

* Le icone di valutazione a stella sono ora attivabili e utilizzabili tramite tasti della tastiera (NPR-32513).

* La funzionalità di controllo del volume video è ora accessibile tramite scheda (per concentrarsi sul cursore del volume) e tasti freccia (per regolare il volume) sulla tastiera (NPR-32065).

* Lo scopo dei campi di input con limite inferiore ([!UICONTROL Da]) e con limite superiore ([!UICONTROL A]) del filtro Dimensione file è ora annunciato agli utenti di utilità di lettura dello schermo non vedenti (NPR-32064).

* Il menu [!UICONTROL Lingue] nel modulo [!UICONTROL Crea e Traduci] è ora accessibile agli assistenti vocali in modalità Sfoglia (CQ-4293906).

* Il pannello [!UICONTROL Riferimenti] è ora accessibile con i seguenti miglioramenti (NPR-33261, CQ-4293798):

   * In modalità Sfoglia, l&#39;assistente vocale non si sposta più sui campi di modifica multiriga nascosti nelle sezioni Riferimenti sito, Riferimenti risorsa, [!UICONTROL Copie]e Riferimenti  modulo.

   * Gli assistenti vocali annunciano ora il ruolo degli elementi Riferimenti [!UICONTROL al] sito e Copie [!UICONTROL di] lingua.

   * Lo stato attivo degli assistenti vocali in modalità Sfoglia si sposta in una sequenza significativa a vari elementi.

* [!UICONTROL La pagina Editor] schema metadati e i relativi elementi sono ora accessibili mediante la tastiera e sono compatibili con gli assistenti vocali (CQ-4290962, CQ-4272953).

* Lo scopo del `X` simbolo di rimuovere i tag selezionati viene ora annunciato dagli assistenti vocali insieme al numero di tag selezionati (CQ-4273017).

* Per evitare confusione negli utenti non vedenti che utilizzano l&#39;assistente vocale, le icone decorative e le immagini vengono ora ignorate dagli assistenti vocali (CQ-4272944).

**Problemi risolti in Risorse  Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets risolve i seguenti problemi:

* [!UICONTROL L&#39;opzione Avvia] nella finestra di dialogo [!UICONTROL Crea flusso di lavoro] per le risorse di una raccolta è disabilitata, impedendo l&#39;attivazione del flusso di lavoro (NPR-32471).

* Quando si utilizza la finestra a comparsa a cascata negli schemi di metadati, quando si seleziona e si salva un&#39;opzione a discesa contenente un apostrofo (dall&#39;elenco a discesa figlio) l&#39;opzione dell&#39;apostrofo selezionato scompare dopo la riapertura delle [!UICONTROL proprietà] della risorsa (NPR-32649).

* [!UICONTROL Asset Insights Sync Job] si interrompe e non riesce se rileva voci non valide (sul lato Analytics ) invece di passare alla voce successiva (NPR-32674).

* Il giroscopio non funziona perché i sensori di movimento sono disattivati per impostazione predefinita sui browser mobili nel visualizzatore panoramico (CQ-4272937).

* [!UICONTROL La configurazione] guidata delle risorse collegate non funziona con l’errore 404. Durante l’installazione della versione 6.5.3 in 6.5.1 (NPR-32730).

* Durante il processo di XMP writeback, tutte le proprietà di metadati dello spazio dei nomi personalizzate modificano il prefisso dello spazio dei nomi personalizzato in ns2 invece del prefisso dello spazio dei nomi configurato (NPR-32748).

* Il caricamento lento non viene attivato e solo 100 risorse vengono visualizzate quando si seleziona per controllare le attività dalla inbox delle notifiche (NPR-32750).

* `NullPointerException` è stato osservato a causa di preferenze di nodo mancanti nel profilo utente appena creato (SAML/SSO). Questo errore impedisce agli utenti appena connessi di utilizzare l&#39; [!DNL Adobe Experience Manager Stock] integrazione (NPR-32777).

* Gli avvisi relativi alle transizioni sono riportati nei registri relativi all&#39;apertura di una raccolta intelligente contenente più di 10.000 risorse (NPR-32980).

* I nomi delle risorse vengono modificati in lettere minuscole quando si spostano le risorse da una cartella all&#39;altra in modalità [!DNL Adobe Experience Manager] di esecuzione Dynamic Media Scene7 (NPR-32995).

* Una risorsa ricercata non può essere eliminata dopo aver navigato nelle sue proprietà dai risultati della ricerca e essere tornata ai risultati della ricerca per eliminarla (NPR-32998).

* [!UICONTROL L&#39;opzione Successivo] rimane disattivata quando si seleziona la cartella di destinazione nell&#39;interfaccia [!UICONTROL Sposta risorse] (NPR-33356).

* [!UICONTROL L&#39;opzione Successivo] non è abilitata quando si seleziona il nodo principale (dove è visibile una singola cartella figlio) e si seleziona la cartella secondaria (NPR-33275).

* Le autorizzazioni di Check-in e check-out sono disattivate in  Adobe Asset Link (AAL) per gli utenti con autorizzazione di eliminazione, anche se sono concesse altre autorizzazioni come lettura, creazione o modifica (NPR-33272).

* Le rappresentazioni SmartCrop non sono disponibili nella finestra di dialogo di download delle risorse (NPR-33167).

* Eccezione nei registri relativi all&#39;apertura della barra delle rappresentazioni per un PDF in una cartella con profilo di ritaglio avanzato (CQ-4294201).

* I predefiniti per immagini non vengono pubblicati se la modalità [!UICONTROL di sincronizzazione] Dynamic Media è disabilitata per impostazione predefinita  Experience Manager con Dynamic Media Scene7 runmode (CQ-4294200).

* L&#39;elaborazione delle risorse durante il caricamento in blocco si blocca e l&#39;istanza del flusso di lavoro mostra le istanze bloccate della risorsa di aggiornamento DAM (CQ-4293916).

* La creazione di una configurazione Dynamic Media sul Experience Manager  funziona, ma nell&#39;interfaccia utente non accade nulla quando si seleziona Salva (CQ-4292442).

* L&#39;anteprima delle risorse video F4V non funziona nella riproduzione progressiva su Safari/Mac (CQ-4289844).

* Al ritaglio avanzato di una risorsa che si trova all’interno di una cartella principale con `.` il nome del punto (CQ-4289337) viene creata una cartella aggiuntiva.

* La miniatura è rotta e il banner di elaborazione video non viene visualizzato quando un video viene copiato (CQ-4284125).

* Il visualizzatore dimensionale visualizza erroneamente le miniature vuote in Firefox per alcuni modelli con viste fotocamera vuote (CQ-4283447).

* I problemi di prestazioni risolti in 6.5.5.0 sono (CQ-4279206):

   * Il caricamento di file binari di grandi dimensioni sui server Dynamic Media Image Processing richiede troppo tempo.

   * Il tempo di generazione delle miniature sul  Experience Manager aumenta a causa dell&#39;architettura Dynamic Media Scene7.

* I problemi di migrazione ad Dynamic Media Scene7 non vanno a buon fine per i clienti con un numero elevato di risorse (CQ-4279206).

* Il layout del visualizzatore video 360 viene interrotto se `setVideo` viene utilizzato, e il video si sposta verso il basso utilizzando `video= modifier` (CQ-4263201).

* Viene visualizzato un messaggio di errore durante l&#39;installazione del pacchetto SDL del Experience Manager  (NPR-33175).

### Platform {#platform-6550}

* Il [!DNL Sling] filtro non viene chiamato se la voce della `sling:match` mappa è creata in `/etc/maps` (NPR-33362).
*  Experience Manager si arresta in modo anomalo a causa di un errore di segmentazione con [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] pacchetto di base mancante  file uberjar di Experience Manager (NPR-32848).
* CRXDE Lite non carica contenuto per gli utenti senza l&#39;autorizzazione di lettura sulla `jcr:primaryType` proprietà di un nodo (NPR-32611).
* [!DNL Granite] la pianificazione delle attività di manutenzione viene inizializzata troppo spesso durante  distribuzioni di Experienci Manager (CQ-4294627).
* Quando una query SQL viene eseguita per un periodo di tempo prolungato, ad esempio 7 ore,  Experience Manager smette di rispondere (NPR-33044).

### Interfaccia utente {#ui-6550}

* La selezione del pulsante di scelta non persiste in un campo multiplo (NPR-33309).
* Il limite di caricamento non funziona per la visualizzazione elenco (NPR-33124).
* Nella pagina dei risultati della ricerca omnisearch non viene visualizzato un messaggio in assenza di corrispondenze (NPR-32974).
* Il filtro di ricerca universale restituisce tutte le corrispondenze sotto il `/content` nodo ignorando la posizione selezionata (NPR-32849).

### Integrations (Integrazioni){#integrations-6550}

* La cache interna viene cancellata quando viene pubblicata una pagina con un componente Adobe Target  (NPR-33162).
* L&#39;integrazione con  Adobe Target non funziona sulla versione [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Durante la configurazione  Adobe Target, i campi [!UICONTROL Società] e Suite [!UICONTROL di] rapporti non vengono visualizzati quando si seleziona un&#39;origine di reporting (NPR-32502).
* Durante l&#39;esportazione [!DNL Experience Fragments] con  I/O Adobe, i metadati come Prodotto sorgente non vengono esportati  Adobe Target (NPR-32159).
* Gli utenti IMS autorizzati nel gruppo di amministrazione  Experience Manager locale non possono creare o modificare configurazioni IMS (NPR-33045).
*  pagina Configurazioni lancio Adobe non visualizza tutti i record (NPR-33011).
* Gli utenti appartenenti al gruppo content-authors non possono modificare le proprietà di un componente Adobe Target  a causa di un errore JavaScript (NPR-32996).

### Progetti traduzione {#translation-6550}

* I tag convertiti non vengono importati in  Experience Manager da servizi di traduzione di terze parti (NPR-33154).
* Nella pagina di configurazione della traduzione viene visualizzato un provider di traduzione non corretto rispetto a quello utilizzato per la traduzione (NPR-32971).
* Se si aggiunge una cartella di frammenti esperienza a un progetto di traduzione esistente, viene creato un nuovo progetto (NPR-32843).
* Nei registri `NullPointerException` viene visualizzato un errore durante l&#39;esecuzione di un processo di traduzione (NPR-32628).

### WCM {#wcm-6550}

* Editor pagina - L&#39;Editor [!DNL Sites] pagina non consente agli utenti che utilizzano solo la tastiera di passare al contenuto principale, invece di spostare lo stato attivo tramite tutte le opzioni disponibili nell&#39;intestazione (CQ-4293883).
* Editor pagina - I pannelli che utilizzano il componente Bene e includono i dati salvati non vengono visualizzati a causa di aggiornamenti in [!DNL Chrome] e [!DNL Firefox] versioni (CQ-4292995).
* MSM - Se si elimina un componente dalla pagina, il componente non viene eliminato dalla versione pubblicata della pagina (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* La rimozione di uno schema di metadati pubblicato [!DNL Brand Portal] genera un errore (CQ-4292063).
* Se un amministratore configura [!DNL Experience Manager Assets] 6.5.4 con Brand Portal tramite  Adobe Developer Console, l’ [!DNL Brand Portal] utente non è in grado di pubblicare la risorsa di una cartella di contributi da [!DNL Brand Portal] a [!DNL Experience Manager] (NPR-33046).
* Replica duplicata delle cartelle principali che causano conflitti (NPR-33001).

### [!DNL Communities] {#communities-6550}

* Non è possibile eliminare una scheda nella console di moderazione utilizzando l&#39;opzione di menu di modifica rapida (NPR-33117).
* Errore durante l&#39;accesso alla pagina Flusso  attività (NPR-33146).
* I gruppi eliminati nell’istanza di creazione non vengono rimossi da tutte le istanze di pubblicazione (NPR-33199).
* Gli autori, dopo aver creato un nuovo gruppo, non vengono reindirizzati alla sezione Gruppo  community sulla versione [!DNL Internet Explorer] 11 (NPR-33205).
* L&#39;accesso a un messaggio in  Casella in entrata Experience Manager non modifica lo stato del messaggio in Lettura (NPR-32764).
* La modifica di un [!DNL Communities] gruppo e la modifica dell&#39;immagine in miniatura non comporta l&#39;aggiornamento della miniatura del gruppo (NPR-32599).
* Un utente non è in grado di inviare un&#39;e-mail a un altro utente in una community (NPR-32598).
* Un blog inviato non viene visualizzato finché l&#39;utente non aggiorna la pagina (NPR-32391).
* Durante la creazione di una versione di notifiche e sottoscrizioni di contenuti generati dall&#39;utente (UGC), viene memorizzato un ID errato della pagina di origine (CQ-4279355, CQ-4289703).

### Flusso di lavoro {#workflow-6550}

* Il caricamento dell&#39;opzione [!UICONTROL Timeline] nella parte sinistra richiede più tempo del previsto (NPR-32851).
* Dopo il riavvio di un&#39;istanza di Experience Manager , l&#39;e-mail per l&#39;attività di revisione per una raccolta include un collegamento di payload non corretto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
> Service Pack di Experience Manager non include correzioni per [!DNL Forms]. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per AEM Forms su JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Gestione corrispondenza: L&#39;ordine delle risorse in un&#39;area di destinazione viene visualizzato dopo l&#39;invio di una lettera (NPR-33359, NPR-33153).
* Forms adattivo: Quando un utente modifica un modulo adattivo, l&#39;opzione [!UICONTROL Avvia flusso di lavoro] disponibile nel menu Informazioni  pagina non funziona (NPR-33004).
* Forms adattivo: L&#39;utente non è in grado di salvare un modulo adattivo con più allegati (NPR-32997).
* Forms adattivo: La modifica del layout del pannello in un modulo adattivo genera un errore (CQ-4293880).
* Forms adattivo: Una nuova riga di una stringa in un dizionario di moduli adattivi aggiunge `&#xa;` caratteri al dizionario (NPR-33266).
* Accessibilità Forms adattiva: Quando un utente visualizza l&#39;anteprima di un modulo adattivo come modulo HTML, il campo Firma  scarabocchio non è in grado di mantenere lo stato attivo (NPR-33159).
* Accessibilità Forms adattiva: I messaggi di errore visualizzati durante l&#39;invio di un modulo adattivo non sono collegati a un `aria-describedBy` attributo (NPR-33071).
* Accessibilità Forms adattiva: I campi contrassegnati come obbligatori in un modulo adattivo non hanno l&#39;attributo obbligatorio impostato su True nello schema di accessibilità ARIA (NPR-33070).
* Servizio PDFG: Quando un utente converte un file di testo in un PDF, i caratteri giapponesi non vengono rappresentati correttamente (NPR-33238).
* Servizio PDFG: `CreatePDF` impossibile convertire un file PDF in formato OCR PDF (NPR-32994).
* Servizio PDFG: La conversione PDF non riesce per la 200a istanza di un [!DNL OpenOffice] documento (NPR-32766).
* BackendIntegration: Le richieste del modello dati del modulo non vanno a buon fine perché il token di aggiornamento scade a causa di uno stato inattivo non corretto (NPR-33169).
* Designer: Gli assistenti vocali eseguono l&#39;ordine di tabulazione in base all&#39;ordine geografico predefinito anziché all&#39;ordine di tabulazione personalizzato definito nel file XDP (NPR-32160).
* Designer: Se l&#39;opzione relativa ai tag è abilitata, il bordo del sottomodulo scompare nell&#39;output PDF generato (NPR-32778).

## Install 6.5.5.0 {#install}

**Requisiti di configurazione**

* AEM 6.5.5.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Il download del service pack è disponibile  Adobe Distribuzione [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)software.
* In una distribuzione con MongoDB e più istanze, installa AEM 6.5.5.0 in una delle istanze Autore tramite Gestione pacchetti.
* Prima di eseguire l&#39;installazione, scegli un&#39;istantanea o un nuovo backup dell&#39;istanza AEM.
* Riavvia l’istanza prima dell’installazione. Anche se questa operazione è necessaria solo quando l’istanza è ancora in modalità di aggiornamento (e questo accade quando l’istanza è stata aggiornata da una versione precedente), è consigliabile riavviare l’istanza se questa è rimasta in esecuzione per un periodo più lungo.

>[!NOTE]
>
> Adobe non consiglia di rimuovere o disinstallare il pacchetto  Adobe Experience Manager 6.5.5.0.

### Installare Service Pack {#install-service-pack}

Per installare Service Pack in un&#39;istanza  Adobe Experience Manager 6.5 esistente, effettuate le seguenti operazioni:

1. Scaricate il service pack da [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip).

1. Aprite Gestione pacchetti e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per sapere come utilizzarlo, consulta Gestione [](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)pacchetti.

1. Select the package and click **[!UICONTROL Install]**.

>[!NOTE]
>
>La finestra di dialogo nell&#39;interfaccia utente di Package Manager talvolta si chiude durante l&#39;installazione del service pack.  Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendete i registri specifici relativi alla disinstallazione del pacchetto di aggiornamento prima di essere certi che le installazioni abbiano esito positivo. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Installazione automatica**

Esistono due modi per installare automaticamente  Adobe Experience Manager 6.5.5.0 in un&#39;istanza di lavoro:

A. Inserite il pacchetto nella `../crx-quickstart/install` cartella quando il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Utilizzate l&#39;API [HTTP da Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Utilizzate questa `cmd=install&recursive=true` opzione per installare i pacchetti nidificati.

>[!NOTE]
>
> Adobe Experience Manager 6.5.5.0 non supporta l&#39;installazione di Bootstrap.

**Convalidare l’installazione**

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa della versione aggiornata `Adobe Experience Manager (6.5.5.0)` in Prodotti installati.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. Il bundle OSGI `org.apache.jackrabbit.oak-core` è della versione 1.22.3 o successiva (Usa console Web: `/system/console/bundles`).

Per conoscere le piattaforme certificate per l’utilizzo con questa versione, consulta i requisiti [tecnici](/help/sites-deploying/technical-requirements.md).

### Installare  pacchetto del componente aggiuntivo Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms. Le correzioni  Adobe Experience Manager Forms vengono distribuite tramite un pacchetto aggiuntivo separato.

1. Accertatevi di aver installato  Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installare  Adobe Experience Manager Forms su JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Le correzioni  Adobe Experience Manager Forms su JEE vengono distribuite tramite un programma di installazione separato.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/it/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

UberJar per  Experience Manager 6.5.5.0 è disponibile nell’archivio [Public Maven del Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/).

Per utilizzare UberJar in un progetto Maven, consulta [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includere nel POM del progetto la seguente dipendenza:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Funzioni obsolete {#removed-deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete con AEM 6.5.5.0. Le funzioni pianificate per essere rimosse in una versione futura sono impostate per prime su obsoleto, con un&#39;opzione alternativa da utilizzare.

Si consiglia ai clienti di verificare se utilizzano la funzionalità o la funzionalità nella distribuzione corrente e di pianificare la modifica della propria implementazione per utilizzare l&#39;opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrations (Integrazioni) | La schermata **[!UICONTROL AEM cloud services consenso]** è obsoleta. Con l&#39;integrazione AEM e Target aggiornata in AEM 6.5 per supportare l&#39;API Target Standard, che utilizza l&#39;autenticazione tramite  Adobe IMS e I/O, e il ruolo crescente di  lancio del Adobe per strumentalizzare AEM pagine per l&#39;analisi e la personalizzazione, la procedura guidata di consenso è diventata funzionale e irrilevante. | Configurate le connessioni di sistema, l&#39;autenticazione  Adobe IMS e le integrazioni di I/O  Adobe tramite i rispettivi AEM cloud services. |
| Connettori | Il connettore JCR  Adobe per Microsoft SharePoint 2010 e Microsoft SharePoint 2013 non è più supportato per AEM 6.5. | N/D |

## Problemi noti {#known-issues}

* Se state installando [!DNL Experience Manager] 6.5.5.0 con [!DNL Java] 11, riavviate il server dopo l&#39;installazione di Service Pack. Se state installando Service Pack con [!DNL Java] 8, non è necessario riavviare il sistema.

* Se una cartella nella gerarchia viene rinominata in [!DNL Experience Manager Assets] e la cartella nidificata che contiene una risorsa viene pubblicata in, il titolo della cartella non viene aggiornato in [!DNL Brand Portal][!DNL Brand Portal] finché la cartella principale non viene nuovamente pubblicata.

* Durante l&#39;installazione di AEM 6.5.5.0, l&#39;aggiornamento della [!DNL Chrome] versione 83 causa un problema nella creazione dei pacchetti. Per risolvere il problema, utilizzate altri browser disponibili, ad esempio [!DNL Internet Explorer] e [!DNL Firefox], o altre opzioni di installazione dei pacchetti standard AEM. Il problema viene risolto dopo l&#39;installazione di AEM 6.5.5.0.

* Impossibile inviare un&#39;e-mail al server SMTP remoto utilizzando AEM mittente di posta predefinito, in quanto consente solo la comunicazione tramite TLS v1.2. Rimuovete il bundle `javax.mail:mail:1.5.0-b01` da `system/console` e aggiornate i bundle per risolvere il problema.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l&#39;opzione per salvare una configurazione non viene visualizzata nel browser Proprietà. Se si seleziona questa opzione per configurare un altro campo del modulo adattivo nello stesso editor, il problema viene risolto.

* Se la configurazione [!UICONTROL delle risorse] connesse restituisce un messaggio di errore 404 dopo l’installazione, reinstallate manualmente i pacchetti `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` i pacchetti utilizzando Gestione pacchetti.

* Durante l&#39;installazione di AEM 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * Quando l’integrazione di Target è configurata in AEM tramite l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce se vengono utilizzate funzioni di aggregazione quali SUM, MAX e MIN. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * L’area sensibile in un’immagine Dynamic Media interattiva non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore per banner acquistabili.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Nei documenti di testo seguenti sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in AEM 6.5.5.0:

* [Elenco dei bundle OSGi inclusi in AEM 6.5.5.0](assets/6550_bundles.txt)

* [Elenco dei pacchetti di contenuti inclusi in AEM 6.5.5.0](assets/6550_packages.txt)

## Restricted sites {#restricted-sites}

Questi siti sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Per ulteriori informazioni sull’accesso al portale di assistenza,](https://docs.adobe.com/content/help/en/customer-one/using/home.html)contattate l’assistenza clienti. Per ulteriori informazioni sull’accesso, consultate [Accesso al portale](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)di assistenza.

>[!MORELIKETHIS]
>
>* [Note sulla versione di AEM 6.5](/help/release-notes/release-notes.md)
>* [Pagina del prodotto AEM](https://www.adobe.com/it/marketing/experience-manager.html)
>* [Documentazione di AEM 6.5](https://helpx.adobe.com/it/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

