---
title: Note sulla versione di AEM 6.5 Service Pack
description: Note sulla versione specifiche di Adobe Experience Manager 6.5 Service Pack 5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d51577195e969ff8af31be49159ff575e3654cc9
workflow-type: tm+mt
source-wordcount: '4476'
ht-degree: 11%

---


# Note sulla versione di Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | **Adobe Experience Manager 6.5** |
|---|---|
| Versione | 6.5.5.0 |
| Tipo | Versione Service Pack |
| Data | 04 giugno 2020 |
| URL di download | [Condivisione](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0)pacchetti, distribuzione [software ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Contenuto in Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0 è un aggiornamento importante che include nuove funzioni, miglioramenti e prestazioni richiesti dai clienti chiave, stabilità, miglioramenti a livello di sicurezza, rilasciati a partire dalla release 6.5 di **aprile 2019**. Può essere installato sopra Adobe Experience Manager (AEM) 6.5.

Alcune funzioni chiave e miglioramenti introdotti in AEM 6.5.5.0 includono:

* Personalizzazione dei nomi di colonna visualizzati nella Casella in entrata AEM.

* Miglioramento dell&#39;accessibilità in varie aree di AEM Web Content Management (WCM), come Editor pagina, Componenti di base, Editor Rich Text e l&#39;interfaccia utente Amministratore.

* Salvataggio di una comunicazione interattiva come bozza.

* Supporto per [!DNL Oracle WebLogic 12] AEM Forms su JEE.

* È stata migliorata la gestione delle eccezioni nel flusso dell’interfaccia utente di [!DNL Adobe Experience Manager] Assets.

* All’interfaccia `getRemoteAssetPublishURL` `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` è stato aggiunto un nuovo metodo per ottenere l’URL di pubblicazione per i file multimediali dinamici di Scene7.

* [Miglioramenti](#assets-6550-changes) dell’accessibilità nelle [!DNL Adobe Experience Manager] risorse in conformità alle linee guida per l’accessibilità dei contenuti Web (WCAG).

* È stata rimossa l&#39;integrazione di Package Share con Adobe Experience Manager.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.3.

Per un elenco completo delle funzioni, degli elementi di rilievo e delle funzioni chiave introdotte nel service pack 5 di AEM 6.5, consultate [Novità di Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Di seguito è riportato l&#39;elenco delle correzioni fornite nella release [!DNL Experience Manager] 6.5.5.0.

### Sites {#sites-6550}

* AEM Sites offre un’opzione per pubblicare o annullare la pubblicazione di una pagina dal relativo alias. L&#39;opzione non funziona (NPR-33415).
* Quando un Contenitore di layout viene eliminato da un modello contenente più modelli, il rendering del modello non viene eseguito correttamente (NPR-33347).
* Quando una pagina AEM Sites fa parte di un set di contenuti di grandi dimensioni con più Live Copy, l&#39;anteprima della cronologia della versione della pagina non viene caricata (NPR-33311).
* Quando si utilizza il comando Sposta per rinominare una pagina AEM Sites, il titolo della pagina non viene aggiornato (NPR-33264).
* Quando si spostano le pagine nella vista a colonne, le colonne scompaiono (NPR-33216).
* Quando il nome di un componente locale in una copia per lingua è identico al nome di un componente nel blueprint e il componente viene implementato dal blueprint, il termine _msm_move non viene aggiunto al nome del componente locale (NPR-33208).
* Il servlet Page Redirect aggiunge .html a un URL AEM Sites in cui ResourceType non è cq:Page (NPR-33176).
* Quando incollate una sottostruttura, non è possibile stabilire se le relative sottopagine devono essere incollate o meno (NPR-33149).
* Il numero di risultati negli usi live di un componente è limitato al numero 49 (NPR-33058).
* Se si basa un frammento di contenuto su uno schema e questo contiene un&#39;area di testo obbligatoria o un campo percorso, il frammento di contenuto non viene salvato (NPR-33007).
* Quando create un componente personalizzato utilizzando il componente per frammento esperienza fornito e lo utilizzate nelle pagine AEM Sites, AEM non visualizza riferimenti (utilizzo) per il componente personalizzato (NPR-32852).
* Quando rinominate una cartella con numerosi riferimenti, molti riferimenti alla cartella non vengono aggiornati (NPR-32765).
* Quando abilitate l&#39;opzione di modifica sorgente, questa diventa disponibile per le opzioni di visualizzazione a schermo intero in linea ma non per la finestra di dialogo di modifica e le opzioni a schermo intero dell&#39;editor Rich Text (NPR-32763).
* Se si dispone di un campo multiplo e contiene un campo obbligatorio (ad esempio un menu a discesa o un campo percorso) nelle proprietà della pagina di un blueprint, quando una pagina contenente tale campo multiplo viene implementata, le proprietà della pagina della Live Copy non vengono salvate. (NPR-32751)
* Gli assistenti vocali non possono utilizzare la struttura dell&#39;intestazione per navigare nella pagina. Inoltre, nella scheda Componenti è presente un&#39;etichetta errata (NPR-32648).
* All&#39;avvio dell&#39;impaginazione, il Selettore frammenti esperienza non carica tutti gli elementi (NPR-32605).
* Le autorizzazioni di lettura, modifica, creazione ed eliminazione delle copie in diretta vengono revocate. Ogni autore doveva fornire esplicitamente le autorizzazioni di lettura e modifica per spostare le pagine all&#39;interno di una Blueprint (NPR-32550).
* Gli autori dei contenuti non riescono a creare Launch per una pagina che dispone di un&#39;integrazione con Adobe Analytics (NPR-32548).
* Quando un utente riprende l&#39;ereditarietà con la sincronizzazione, la live copy della pagina padre non si sincronizza con il blueprint e visualizza uno stato non corretto (NPR-32500).
* Il caricamento della pagina dell&#39;editor di AEM Sites richiede più di 15 secondi (NPR-32413).
* Alcuni campi non visualizzano l&#39;opzione Annulla ereditarietà (NPR-32362).
* Quando selezionate un percorso per un componente Frammento esperienza e la casella di controllo Apri finestra di dialogo di selezione, non viene visualizzato nel browser Percorso (NPR-32308).
* Quando eseguite l’aggiornamento da AEM 6.2 a AEM 6.5, il componente Parsys dei modelli statici non viene visualizzato correttamente. L’altezza del componente Parsys è impostata su 0 e i componenti al suo interno non sono visibili. (NPR-33663).
* Quando un utente copia e incolla un Contenitore di layout sulla stessa pagina, i componenti in un Contenitore di layout non vengono visualizzati (NPR-33648).
* Il controllo dello stato del dispatcher visualizza un messaggio di `Invalid cookie header` avviso nei file di registro (NPR-33629).

### Assets {#assets-6550-changes}

**Miglioramenti dell&#39;accessibilità in Experience Manager Assets**

* È ora possibile attivare l&#39;elenco [!UICONTROL Commenti] e fare clic sull&#39;opzione per [!UICONTROL creare] commenti sulla versione in [!UICONTROL Crea nuova versione] nel pannello [!UICONTROL Timeline] delle risorse (NPR-33424).

* Ora è possibile accedere all&#39;opzione [!UICONTROL Visualizza impostazioni] per le risorse e modificare le impostazioni nella finestra di dialogo Impostazioni  visualizzazione tramite i tasti della tastiera (NPR-33420).

* Il menu a discesa della casella di riepilogo della casella combinata (in vari campi su pagine diverse) ora mostra le voci come un elenco di opzioni che possono essere annunciate dagli assistenti vocali (NPR-33516).

* La funzionalità di ordinamento delle intestazioni ordinabili (nella vista a elenco, nella vista [!UICONTROL Timeline] e nella pagina [!UICONTROL Gestisci pubblicazione] ) ora è annunciata dagli assistenti vocali e i controlli di ordinamento sulle intestazioni delle colonne sono accessibili tramite tastiera (NPR-32979).

* Gli elementi su cui è possibile fare clic (come schede di commenti, aggiornamenti della versione, caselle combinate e icone a forma di freccia dei menu) sono ora attivabili e utilizzabili mediante la tastiera (NPR-33514).

* Funzionalità (o scopo dell&#39;azione) delle icone delle informazioni (per uso, impression e clic) nella vista  Insights ora vengono annunciate correttamente dagli assistenti vocali (NPR-33513).

* I campi modulo di sola lettura (ad esempio i campi disabilitati nella scheda  Base delle [!UICONTROL proprietà]della risorsa) sono ora attivabili mediante la tastiera (NPR-33493, CQ-4273031).

* Le etichette in vari campi di input sono ora etichette permanenti (quindi accessibili) e non solo etichette segnaposto, scomparse al momento dell&#39;immissione del testo (NPR-33475).

* Diversi livelli di intestazione (come titoli di pagina e intestazioni di sezione) vengono ora percepiti come titoli con livelli diversi per gli utenti degli assistenti vocali (NPR-33471).

* Gli elementi interattivi dell&#39;interfaccia utente, come i collegamenti e le opzioni (nelle opzioni di intestazione e zoom della pagina delle risorse, nella navigazione delle cartelle), sono ora accessibili tramite una tastiera (NPR-33468, CQ-4271412).

* Gli indicatori di avanzamento di [!UICONTROL Opzioni], [!UICONTROL Ambito]e Flussi [!UICONTROL di lavoro nella pagina] Gestisci pubblicazione  ora vengono letti correttamente dagli assistenti vocali come indicatori di avanzamento, invece delle schede (NPR-33416).

* Il colore delle icone di valutazione a stella (ad esempio nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] nelle [!UICONTROL proprietà] della risorsa o nella vista a schede) viene modificato per rendere visibile il contrasto appropriato agli utenti con una visione limitata e senza percezione del colore (NPR-33414).

* È ora possibile accedere alla freccia rivolta verso l&#39;alto accanto al campo [!UICONTROL Commento] nella pagina dei dettagli delle risorse tramite i tasti di scelta rapida (NPR-33397).

* Gli stati espansi e compressi della finestra di dialogo [!UICONTROL Tag] in [!UICONTROL Proprietà] risorsa e nella barra di navigazione a sinistra (nell’interfaccia utente delle risorse) ora vengono annunciati correttamente dagli assistenti vocali (NPR-33396).

* I titoli di tutte le pagine visualizzate su [!DNL Adobe Experience Manager] Risorse sono ora univoci (NPR-33343).

* Mentre si naviga nella struttura ad albero vari elementi del controllo della visualizzazione ad albero vengono ora correttamente annunciati dagli assistenti vocali (NPR-33304).

* Sono ora accessibili diverse versioni delle risorse nella visualizzazione [!UICONTROL Timeline] nella pagina dei dettagli delle risorse tramite i tasti di scelta rapida (NPR-33283).

* I nomi dei suggerimenti di ricerca visualizzati nella casella combinata Omnisearch ora vengono annunciati dagli assistenti vocali mentre utilizzano la funzionalità di ricerca (NPR-33280).

* Gli elementi selezionabili e il collegamento [!UICONTROL Vai a nella barra laterale]  Riferimenti vengono ora annunciati dagli assistenti vocali come elementi selezionabili (NPR-33278).

* Le informazioni sulla struttura della tabella (come riga 1, cella 1, tabella) della finestra di dialogo [!UICONTROL Condividi collegamento] non vengono più annunciate dagli assistenti vocali all&#39;apertura della finestra di dialogo (NPR-33268).

* Lo scopo di vari elementi della casella combinata (ad esempio il campo Percorso e l&#39;opzione per aprire la finestra di dialogo di selezione nella scheda Base delle proprietà della risorsa) ora viene annunciato correttamente dagli assistenti vocali (NPR-33235).

* Le informazioni che le righe nella tabella di visualizzazione a elenco sono selezionabili vengono ora comunicate agli utenti dell&#39;assistente vocale quando sono attivate dalla tastiera. Queste informazioni vengono annunciate quando il mouse si trova sulle righe (NPR-33234).

* Le opzioni (con [!UICONTROL x]) per rimuovere ciascuno dei tag selezionati sotto il campo [!UICONTROL Tag] nella scheda [!UICONTROL Base] di [!UICONTROL Proprietà] sono ora accessibili agli assistenti vocali (NPR-33206).

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

* Viene inoltre annunciato lo scopo dell&#39;icona [!UICONTROL x] sull&#39;opzione per rimuovere i tag attualmente selezionati, insieme al numero di tag selezionati (CQ-4273017).

* Le icone decorative e le immagini vengono ora ignorate dagli assistenti vocali, per evitare confusione per gli utenti non vedenti che utilizzano l&#39;assistente vocale (CQ-4272944).

**Problemi risolti in Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets risolve i seguenti problemi:

* [!UICONTROL L&#39;opzione Avvia] nella finestra di dialogo [!UICONTROL Crea flusso di lavoro] per le risorse di una raccolta è disabilitata, impedendo l&#39;attivazione del flusso di lavoro (NPR-32471).

* Quando si utilizza un menu a discesa a cascata negli schemi di metadati, quando si seleziona e si salva un&#39;opzione a discesa contenente un apostrofo (dall&#39;elenco a discesa figlio) l&#39;opzione dell&#39;apostrofo selezionato scompare dopo la riapertura delle [!UICONTROL proprietà] della risorsa (NPR-32649).

* [!UICONTROL Asset Insights Sync Job] si interrompe e non riesce se rileva voci non valide (sul lato Analytics) invece di passare alla voce successiva (NPR-32674).

* Il giroscopio non funziona perché i sensori di movimento sono disattivati per impostazione predefinita sui browser mobili nel visualizzatore panoramico (CQ-4272937).

* [!UICONTROL La configurazione] guidata delle risorse collegate non funziona con l’errore 404. Durante l’installazione della versione 6.5.3 in 6.5.1 (NPR-32730).

* Durante il processo di writeback XMP, tutte le proprietà di metadati dello spazio nomi personalizzate modificano il prefisso dello spazio nomi personalizzato in ns2, invece del prefisso dello spazio nomi configurato (NPR-32748).

* Il caricamento lento non viene attivato e solo 100 risorse vengono visualizzate quando si seleziona per controllare le attività dalla inbox delle notifiche (NPR-32750).

* `NullPointerException` è stato osservato a causa di preferenze di nodo mancanti nel profilo utente appena creato (SAML/SSO). Questo errore impedisce agli utenti appena connessi di utilizzare l&#39; [!DNL Adobe Experience Manager Stock] integrazione (NPR-32777).

* Gli avvisi relativi alle transizioni sono riportati nei registri relativi all&#39;apertura di una raccolta intelligente contenente più di 10.000 risorse (NPR-32980).

* I nomi delle risorse vengono modificati in lettere minuscole quando si spostano le risorse da una cartella all’altra in modalità [!DNL Adobe Experience Manager] di esecuzione di Dynamic Media Scene7 (NPR-32995).

* Una risorsa ricercata non può essere eliminata dopo aver navigato nelle sue proprietà dai risultati della ricerca e essere tornata ai risultati della ricerca per eliminarla (NPR-32998).

* [!UICONTROL L&#39;opzione Successivo] rimane disattivata quando si seleziona la cartella di destinazione nell&#39;interfaccia [!UICONTROL Sposta risorse] (NPR-33356).

* [!UICONTROL L&#39;opzione Successivo] non è abilitata quando si seleziona il nodo principale (dove è visibile una singola cartella figlio) e si seleziona la cartella secondaria (NPR-33275).

* Le autorizzazioni di archiviazione e check-out sono disattivate in Adobe Asset Link (AAL) per gli utenti con autorizzazione di eliminazione, anche se sono consentite altre autorizzazioni come lettura, creazione o modifica (NPR-33272).

* Le rappresentazioni SmartCrop non sono disponibili nella finestra di dialogo di download delle risorse (NPR-33167).

* Eccezione nei registri relativi all&#39;apertura della barra delle rappresentazioni per un PDF in una cartella con profilo di ritaglio avanzato (CQ-4294201).

* I predefiniti per immagini non vengono pubblicati se la modalità [!UICONTROL di sincronizzazione per contenuti multimediali] dinamici è disabilitata per impostazione predefinita in AEM con la modalità di esecuzione di Dynamic Media Scene7 (CQ-4294200).

* L&#39;elaborazione delle risorse durante il caricamento in blocco si blocca e l&#39;istanza del flusso di lavoro mostra le istanze bloccate della risorsa di aggiornamento DAM (CQ-4293916).

* La creazione di una configurazione per contenuti multimediali dinamici in AEM funziona, ma nell’interfaccia utente non viene eseguita alcuna operazione selezionando Salva (CQ-4292442).

* L&#39;anteprima delle risorse video f4v non funziona nella riproduzione progressiva su Safari/Mac (CQ-4289844).

* Al ritaglio avanzato di una risorsa che si trova all’interno di una cartella principale con `.` il nome del punto (CQ-4289337) viene creata una cartella aggiuntiva.

* La miniatura è rotta e il banner di elaborazione video non viene visualizzato quando un video viene copiato (CQ-4284125).

* Il visualizzatore dimensionale visualizza erroneamente le miniature vuote in Firefox per alcuni modelli con viste fotocamera vuote (CQ-4283447).

* I problemi di prestazioni risolti in 6.5.5.0 sono (CQ-4279206):

   * Il caricamento di file binari di grandi dimensioni sui server di elaborazione immagini per file multimediali dinamici richiede troppo tempo.

   * Il tempo di generazione delle miniature in AEM aumenta a causa dell’architettura Dynamic Media Scene7.

* I problemi di migrazione di Dynamic Media Scene7 non vanno a buon fine per i clienti con un numero elevato di risorse (CQ-4279206).

* Il layout del visualizzatore video 360 viene interrotto se `setVideo` viene utilizzato, e il video si sposta verso il basso utilizzando `video= modifier` (CQ-4263201).

* Viene visualizzato un messaggio di errore durante l&#39;installazione del pacchetto AEM SDL (NPR-33175).

### Platform {#platform-6550}

* Il [!DNL Sling] filtro non viene chiamato se la voce della `sling:match` mappa è creata in `/etc/maps` (NPR-33362).
* Arresti anomali di AEM a causa di un errore di segmentazione con [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] pacchetto di base mancante nel file JAR dell&#39;utente AEM (NPR-32848).
* CRXDE Lite non carica il contenuto per gli utenti che non dispongono dell&#39;autorizzazione READ sulla `jcr:primaryType` proprietà di un nodo (NPR-32611).
* [!DNL Granite] la pianificazione delle attività di manutenzione viene inizializzata troppo spesso durante le distribuzioni AEM (CQ-4294627).
* Quando una query SQL viene eseguita per un periodo di tempo più lungo, ad esempio 7 ore, AEM smette di rispondere (NPR-33044).

### Interfaccia utente {#ui-6550}

* La selezione del pulsante di scelta non persiste in un campo multiplo (NPR-33309).
* Il limite di caricamento non funziona per la visualizzazione elenco (NPR-33124).
* Nella pagina dei risultati della ricerca omnisearch non viene visualizzato un messaggio in assenza di corrispondenze (NPR-32974).
* Il filtro di ricerca universale restituisce tutte le corrispondenze sotto il `/content` nodo ignorando la posizione selezionata (NPR-32849).

### Integrations (Integrazioni){#integrations-6550}

* La cache interna viene cancellata quando viene pubblicata una pagina con un componente Adobe Target (NPR-33162).
* L&#39;integrazione con Adobe Target non funziona sulla versione [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Durante la configurazione di Adobe Target, i campi [!UICONTROL Società] e Suite [!UICONTROL di] rapporti non vengono visualizzati quando si seleziona un&#39;origine di reporting (NPR-32502).
* Quando si esportano frammenti di esperienza utilizzando l&#39;I/O di Adobe, metadati come Prodotto di origine non vengono esportati in Adobe Target (NPR-32159).
* Gli utenti IMS autorizzati nel gruppo di amministrazione locale di AEM non possono creare o modificare configurazioni IMS (NPR-33045).
* La pagina delle configurazioni di Adobe Launch non visualizza tutti i record (NPR-33011).
* Gli utenti del gruppo di autori di contenuti non possono modificare le proprietà di un componente Adobe Target a causa di un errore JavaScript (NPR-32996).

### Progetti traduzione {#translation-6550}

* I tag convertiti non vengono importati in AEM da servizi di traduzione di terze parti (NPR-33154).
* Nella pagina di configurazione della traduzione viene visualizzato un provider di traduzione non corretto rispetto a quello utilizzato per la traduzione (NPR-32971).
* Se si aggiunge una cartella di frammenti esperienza a un progetto di traduzione esistente, viene creato un nuovo progetto (NPR-32843).
* Nei registri `NullPointerException` viene visualizzato un errore durante l&#39;esecuzione di un processo di traduzione (NPR-32628).

### WCM {#wcm-6550}

* Editor pagina - L&#39;Editor [!DNL Sites] pagina non consente agli utenti che utilizzano solo la tastiera di passare al contenuto principale, invece di spostare lo stato attivo tramite tutte le opzioni disponibili nell&#39;intestazione (CQ-4293883).
* Editor pagina - I pannelli che utilizzano il componente Bene e includono i dati salvati non vengono visualizzati a causa di aggiornamenti in [!DNL Chrome] e [!DNL Firefox] versioni (CQ-4292995).
* MSM - Se si elimina un componente dalla pagina, il componente non viene eliminato dalla versione pubblicata della pagina (CQ-4292360).

### Brand Portal {#assets-brand-portal-6550}

* La rimozione di uno schema di metadati pubblicato [!DNL Brand Portal] genera un errore (CQ-4292063).
* Se un amministratore configura [!DNL Experience Manager Assets] 6.5.4 con Brand Portal tramite Adobe Developer Console, l’ [!DNL Brand Portal] utente non è in grado di pubblicare la risorsa di una cartella di contributi da [!DNL Brand Portal] a [!DNL Experience Manager]. (NPR-33046).
* Replica duplicata delle cartelle principali che causano conflitti (NPR-33001).

### Communities {#communities-6550}

* Non è possibile eliminare una scheda nella console di moderazione utilizzando l&#39;opzione di menu di modifica rapida (NPR-33117).
* Errore durante l&#39;accesso alla pagina Flusso  attività (NPR-33146).
* I gruppi eliminati nell’istanza di creazione non vengono rimossi da tutte le istanze di pubblicazione (NPR-33199).
* Gli autori, dopo aver creato un nuovo gruppo, non vengono reindirizzati alla sezione Gruppo  community sulla versione [!DNL Internet Explorer] 11 (NPR-33205).
* L&#39;accesso a un messaggio in AEM Inbox non modifica lo stato del messaggio in Lettura (NPR-32764).
* La modifica di un [!DNL Communities] gruppo e la modifica dell&#39;immagine in miniatura non comporta l&#39;aggiornamento della miniatura del gruppo (NPR-32599).
* Un utente non è in grado di inviare un&#39;e-mail a un altro utente in una community (NPR-32598).
* Un blog inviato non viene visualizzato finché l&#39;utente non aggiorna la pagina (NPR-32391).
* Durante la creazione di una versione di notifiche e sottoscrizioni di contenuti generati dall&#39;utente (UGC), viene memorizzato un ID errato della pagina di origine (CQ-4279355, CQ-4289703).

### Flusso di lavoro {#workflow-6550}

* Il caricamento dell&#39;opzione [!UICONTROL Timeline] nella parte sinistra richiede più tempo del previsto (NPR-32851).
* Dopo il riavvio di un&#39;istanza di AEM, l&#39;e-mail per l&#39;attività di revisione di una raccolta include un collegamento di payload non corretto (NPR-32774).

### Forms {#forms-6550}

>[!NOTE]
>
>Il Service Pack di AEM non include le correzioni per AEM Forms. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per AEM Forms su JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Gestione corrispondenza: L&#39;ordine delle risorse in un&#39;area di destinazione viene visualizzato dopo l&#39;invio di una lettera (NPR-33359, NPR-33153).
* Moduli adattivi: Quando un utente modifica un modulo adattivo, l&#39;opzione [!UICONTROL Avvia flusso di lavoro] disponibile nel menu Informazioni  pagina non funziona (NPR-33004).
* Moduli adattivi: L&#39;utente non è in grado di salvare un modulo adattivo con più allegati (NPR-32997).
* Moduli adattivi: La modifica del layout del pannello in un modulo adattivo genera un errore (CQ-4293880).
* Moduli adattivi: Una nuova riga di una stringa in un dizionario di moduli adattivi aggiunge `&#xa;` caratteri al dizionario (NPR-33266).
* Accessibilità ai moduli adattivi: Quando un utente visualizza l&#39;anteprima di un modulo adattivo come modulo HTML, il campo Firma  scarabocchio non è in grado di mantenere lo stato attivo (NPR-33159).
* Accessibilità ai moduli adattivi: I messaggi di errore visualizzati durante l&#39;invio di un modulo adattivo non sono collegati a un `aria-describedBy` attributo (NPR-33071).
* Accessibilità ai moduli adattivi: I campi contrassegnati come obbligatori in un modulo adattivo non hanno l&#39;attributo obbligatorio impostato su True nello schema di accessibilità ARIA (NPR-33070).
* Servizio PDFG: Quando un utente converte un file di testo in un PDF, i caratteri giapponesi non vengono rappresentati correttamente (NPR-33238).
* Servizio PDFG: `CreatePDF` impossibile convertire un file PDF in formato OCR PDF (NPR-32994).
* Servizio PDFG: La conversione PDF non riesce per la 200a istanza di un [!DNL OpenOffice] documento (NPR-32766).
* BackendIntegration: Le richieste del modello dati del modulo non vanno a buon fine perché il token di aggiornamento scade a causa di uno stato inattivo non corretto (NPR-33169).
* Designer: Gli assistenti vocali eseguono l&#39;ordine di tabulazione in base all&#39;ordine geografico predefinito anziché all&#39;ordine di tabulazione personalizzato definito nel file XDP (NPR-32160).
* Designer: Se l&#39;opzione relativa ai tag è abilitata, il bordo del sottomodulo scompare nell&#39;output PDF generato (NPR-32778).

## Install 6.5.5.0 {#install}

**Requisiti di configurazione**

* AEM 6.5.5.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Il download del Service Pack è disponibile in Condivisione pacchetti Adobe, a cui puoi accedere direttamente dall’istanza di AEM 6.5.
* In una distribuzione con MongoDB e più istanze, installa AEM 6.5.5.0 in una delle istanze Autore tramite Gestione pacchetti.
* Prima di eseguire l’installazione, scegli un’istantanea o un nuovo backup dell’istanza AEM.
* Riavvia l’istanza prima dell’installazione. Anche se questa operazione è necessaria solo quando l’istanza è ancora in modalità di aggiornamento (e questo accade quando l’istanza è stata aggiornata da una versione precedente), è consigliabile riavviare l’istanza se questa è rimasta in esecuzione per un periodo più lungo.

>[!NOTE]
>
>Adobe sconsiglia la rimozione o la disinstallazione del pacchetto AEM 6.5.5.0.

### Installare Service Pack {#install-service-pack}

Per installare il Service Pack in un’istanza AEM 6.5 esistente, effettua le seguenti operazioni:

1. Fate clic sul collegamento [Condivisione](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0) pacchetti o Distribuzione [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) software per scaricare il pacchetto.

1. Aprite [Package Manager](http://localhost:4502/crx/packmgr/index.jsp) e fate clic su **Carica pacchetto** per caricare il pacchetto.

1. Selezionate il nome del pacchetto e fate clic su **Installa**.

>[!NOTE]
>
>**La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude prematuramente durante l’installazione della versione 6.5.5.0**
>
>È consigliabile attendere che i registri degli errori si stabilizzino prima di accedere all’istanza. L&#39;utente deve attendere i registri specifici relativi alla disinstallazione del bundle dell&#39;utility di aggiornamento prima di assicurarsi che le installazioni abbiano esito positivo. Il problema si verifica in genere in Safari, ma può accadere in modo intermittente in qualsiasi browser.

**Installazione automatica**

Esistono due modi per installare automaticamente AEM 6.5.5.0 in un’istanza in esecuzione:

A. Inserite il pacchetto nella `../crx-quickstart/install ` cartella mentre il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use `cmd=install&recursive=true` - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.5.0 non supporta l’installazione tramite bootstrap.

**Convalidare l’installazione**

1. Nella pagina Informazioni sul prodotto (/system/console/ productinfo) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager, Version 6.5.5.0` in Prodotti installati.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. Il bundle OSGI `org.apache.jackrabbit.oak-core` è sulla versione 1.10.6 o successiva (Usa console Web: `/system/console/bundles`).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms. Le correzioni apportate in AEM Forms vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi.

1. Assicurati di aver installato il Service Pack di AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Le correzioni in AEM Forms su JEE vengono distribuite tramite un programma di installazione separato.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/it/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

The UberJar for AEM 6.5.5.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

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
| Integrations (Integrazioni) | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Con l&#39;integrazione AEM e Target aggiornata in AEM 6.5 per supportare l&#39;API di Target Standard, che utilizza l&#39;autenticazione tramite Adobe IMS e I/O, e con il ruolo crescente di Adobe Launch nella strumentazione delle pagine AEM per l&#39;analisi e la personalizzazione, la procedura guidata di consenso è diventata funzionalmente irrilevante. | Configurare le connessioni di sistema, l&#39;autenticazione Adobe IMS e le integrazioni Adobe I/O tramite i rispettivi servizi cloud AEM |

## Problemi noti {#known-issues}

* Se state installando [!DNL Experience Manager] 6.5.5.0 con [!DNL Java] 11, riavviate il server dopo l&#39;installazione di Service Pack. Se state installando Service Pack con [!DNL Java] 8, non è necessario riavviare il sistema.

* Se una cartella nella gerarchia viene rinominata in [!DNL Experience Manager Assets] e la cartella nidificata che contiene una risorsa viene pubblicata in, il titolo della cartella non viene aggiornato in [!DNL Brand Portal][!DNL Brand Portal] finché la cartella principale non viene nuovamente pubblicata.

* L&#39;aggiornamento della [!DNL chrome] versione 83 causa un problema nella creazione di pacchetti. Per risolvere il problema, utilizzate altri browser disponibili, ad esempio [!DNL Internet Explorer] e [!DNL Firefox], o altre opzioni di installazione dei pacchetti standard di AEM.

* Impossibile inviare un&#39;e-mail al server SMTP remoto utilizzando il mittente di posta predefinito di AEM, in quanto consente solo la comunicazione mediante TLS v1.2. Rimuovete il bundle `javax.mail:mail:1.5.0-b01` da `system/console` e aggiornate i bundle per risolvere il problema.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l&#39;opzione per salvare una configurazione non viene visualizzata nel browser Proprietà. Se si seleziona questa opzione per configurare un altro campo del modulo adattivo nello stesso editor, il problema viene risolto.

* Se la configurazione [!UICONTROL delle risorse] connesse restituisce un messaggio di errore 404 dopo l’installazione, reinstallate manualmente i pacchetti `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` i pacchetti utilizzando Gestione pacchetti.

* Durante l’installazione di AEM 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * Quando l’integrazione di Target è configurata in AEM tramite l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce se vengono utilizzate funzioni di aggregazione quali SUM, MAX e MIN. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva Dynamic Media non è visibile durante l’anteprima della risorsa tramite il visualizzatore di banner per e-commerce.

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
>* [Pagina del prodotto AEM](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentazione di AEM 6.5](https://helpx.adobe.com/it/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

