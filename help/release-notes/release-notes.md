---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: '"[!DNL Adobe Experience Manager] Note 6.5 che descrivono le informazioni sulla versione, le novità, le modalità di installazione e gli elenchi dettagliati delle modifiche."'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: db94e464b130c6ca223314c3c5ffb8893a92a142
workflow-type: tm+mt
source-wordcount: '3752'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.13.0 |
| Tipo | Versione Service Pack |
| Data | 26 maggio 2022 |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## Cosa è incluso in [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti successivamente alla data di disponibilità iniziale del 6.5 di aprile 2019. [Installa questo service pack](#install) su [!DNL Experience Manager] 6.5.

Funzioni chiave e miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.13.0:

* Utilizza il CAPTCHA invisibile in un modulo adattivo: Ora puoi utilizzare un CAPTCHA invisibile per mostrare la sfida CAPTCHA solo nel caso di un’attività sospetta. Se non viene trovata alcuna attività sospetta, la sfida CAPTCHA non viene visualizzata. Consente di valutare il completamento dei moduli senza bisogno di caselle di controllo, ridurre le operazioni di personalizzazione e migliorare l’esperienza dell’utente finale. (NPR-38500)

* È stato aggiunto il supporto per recuperare le intestazioni di risposta nel post-processore Form Data Model per gli endpoint REST. (NPR-38275)

* Ora, quando si genera un file di traduzione Modulo adattivo, la stessa sequenza di testi del file XLIFF generato è identica alla sequenza di componenti del modulo adattivo corrispondente. (NPR-37700)

* Quando si localizza un Modulo adattivo e si apporta anche una piccola modifica al testo della lingua di base, la traduzione completa risulta mancante per tutte le altre lingue. Il problema è risolto in [!DNL Experience Manager] 6.5.13.0. (NPR-37189)

* Miglioramenti all’accessibilità per Forms:

   * È stato aggiunto il supporto per gli assistenti vocali per riconoscere l’intestazione e il corpo di una tabella mentre continuavano e le entità collegate. Consente agli assistenti vocali di navigare correttamente nelle tabelle. (NPR-37139)
   * È stato aggiunto il supporto per consentire agli assistenti vocali di interrompere la navigazione nell’area di lavoro di HTML fino all’apertura di una finestra di dialogo. (NPR-37134)
   * Aggiunta la possibilità di specificare il testo del Reader di schermate per i collegamenti ipertestuali in Forms Designer.(NPR-36221)

Sono state introdotte le seguenti correzioni di bug, funzioni chiave e miglioramenti in [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* Quando si tenta di modificare un campo a discesa di sola lettura, il valore a discesa viene reimpostato su vuoto. (NPR-38389)
* L’utente non è in grado di acquisire una risorsa video (.mp4) se nel file video non è presente audio. Il flusso di lavoro Aggiorna risorsa DAM non riesce e riflette un messaggio di errore. (NPR-38116)
* Quando si utilizza la procedura guidata Sposta risorsa per spostare una cartella contenente risorse, il flusso di lavoro non riesce e viene visualizzato un messaggio di errore. (NPR-38061)
* Errore del flusso di lavoro di transcodifica FFmpeg per il profilo video FLV. (CQ-4343249)
* Dopo l’aggiornamento a [!DNL Experience Manager] 6.5 SP10, l’editor dei metadati delle risorse non funziona correttamente. (CQ-4341359)
* Quando si apre una Raccolta avanzata salvata con il filtro di ricerca applicato come Pubblicazione, il filtro di ricerca diventa automaticamente Non pubblicato. (CQ-4341191)
* Quando si cambia lingua in **[!UICONTROL Preferenze utente]**, l&#39;etichetta **[!UICONTROL Ordina per]**, il pulsante a discesa e altre opzioni nelle opzioni di ordinamento nella home page della risorsa non vengono riportate nella lingua selezionata. (CQ-4339306)
* Quando si aggiunge una regola a un campo a discesa in **[!UICONTROL Schema metadati]**, **[!UICONTROL Dipendente da]** L’elenco non riflette l’etichetta del campo del menu a discesa. (ASSETS-9442)
* L’elenco a discesa Metadati risorse disattivati non mantiene i valori. (ASSETS-8918)
* Quando visualizzi la risorsa utilizzando **[!UICONTROL Maggiori dettagli]** opzione in **[!UICONTROL Colonna]** vengono visualizzate annotazioni non corrette. (ASSETS-8851)
* Quando crei una risorsa duplicata con una versione diversa, le rappresentazioni non vengono generate. (ASSETS-8607)

* Un utente non amministratore può pubblicare una risorsa già estratta da un altro utente. (NPR-38128)
* Il visualizzatore dimensionale non funziona su Chrome 97. (CQ-4340456)
* Il pulsante di download delle risorse non mostra il menu completo nella pagina Dettagli risorsa. (CQ-4336703)
* Quando si utilizza Condivisione collegamenti, alcune stringhe nella finestra di condivisione collegamenti non sono localizzate. (CQ-4330540)
* Quando si aggiungono elementi in Gestisci pubblicazione, la stringa che riflette il conteggio degli elementi selezionati non viene localizzata. (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* Anteprima protetta basata su token per le risorse Dynamic Media su AEM Authors. (ATTIVO-4995)
* Quando si crea un predefinito per immagini per Dynamic Media in [!DNL Experience Manager], il massimo consentito è limitato a 2000x2000 pixel nell’interfaccia utente. Quando il valore viene aumentato a 2001 pixel per larghezza o altezza, il **[!UICONTROL Salva]** pulsante disattivato. (ATTIVO-5691)
* L&#39;utente può impedire il caricamento di determinati formati di file in Dynamic Media. (ATTIVO-5693)
* Accessibilità : gli utenti con problemi visivi che si affidano agli assistenti vocali vengono interessati se l’attributo Alt non è implementato su un’immagine nell’interfaccia utente dei predefiniti immagine. (ASSETS-9817)
* Accessibilità : gli assistenti vocali vengono interessati quando gli assistenti vocali leggono immagini non etichettate per le immagini presenti nel &quot;segmento Timeline&quot; e nella scheda &quot;Azioni&quot;, quando vengono navigate in modalità freccia giù. (ASSETS-5651)
* Accessibilità : gli assistenti vocali vengono influenzati dal fatto che gli assistenti vocali (NVDA/JAWS) non leggono il nome descrittivo (Invia e-mail) per il pulsante &quot;Invia e-mail&quot; nella finestra di dialogo &quot;EmailLink&quot; nel lettore video, durante la navigazione utilizzando le modalità (Sfoglia/cursore). (ASSETS-5641)
* Accessibilità - Lo stato attivo della tastiera non si sposta sul pulsante &quot;Ripristina&quot; visualizzato dopo aver richiamato il pulsante &quot;Annulla&quot; nella pagina Editor set di immagini durante la navigazione tramite il tasto TAB sulla tastiera. (ASSETS-5582)
* Accessibilità : gli utenti che si affidano agli assistenti vocali vengono influenzati dal fatto che l’attributo Alt non viene fornito per un’immagine di un set di immagini presente nell’intestazione Proprietà . (ASSETS-5576)
* Accessibilità : gli assistenti vocali non stanno narrando il ruolo di intestazione per `Cannot save this set` nel testo `Cannot save this set` avviso, durante la navigazione con il tasto di scelta rapida intestazione `H`e Freccia giù. (ASSETS-5569)
* Accessibilità : gli utenti che si affidano agli assistenti vocali vengono interessati a spostarsi all’interno dei moduli. Hanno difficoltà a comprendere le informazioni sui controlli del modulo se NVDA non sta narrando le informazioni dell&#39;etichetta per i controlli di rotazione &quot;Larghezza e altezza&quot;. Questi controlli sono presenti sotto l&#39;intestazione Ritaglio immagine reattivo durante la navigazione in modalità formato NVDA ‘F’. (ATTIVO-5393)
* Dopo aver aggiunto un componente Dynamic Media su un sito e dopo la pubblicazione della pagina, la risorsa Dynamic Media appena aggiunta non è visibile sulla pagina pubblicata, né nella pagina Anteprima. Questo problema si verificava sia per i tipi di risorse immagine che per quelle video. (ASSETS-9467)

## Commerce {#commerce-6513}

* &quot;all&quot; ha jcr:write su `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* L’ordinamento locale dei prodotti Commerce non funziona più. (CQ-4343750)
* Impossibile pubblicare rapidamente un prodotto dalla pagina dei risultati della ricerca dopo la modifica delle proprietà. (CQ-4343318)

## CRX {#crx-6513}

* Impossibile scaricare un pacchetto se ha il carattere speciale `+` nel nome del pacchetto. (NPR-38102)

## [!DNL Forms] {#forms-65130}

* Quando si utilizza il servizio di precompilazione per compilare un modulo adattivo contenente un frammento e il frammento contiene una casella di testo che supporta testo RTF, l’invio del modulo non riesce e si verifica il seguente errore:

   `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542)

* I componenti Pulsante di scelta, Casella di controllo e Caricamento file non vengono tradotti correttamente dalla lingua tedesca alla lingua inglese. (NPR-38527)
* Codifica codice a barre PDF417 prodotta da [!DNL Experience Manager] Forms non valido per un gruppo di pulsanti di scelta. (NPR-38525)
* Il seguente errore si verifica durante l’invio di un modulo adattivo.
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* L’opzione Escludi campi nascosti dal documento di record non funziona. (NPR-38512)
* Dopo aver aggiunto il componente Contenitore di Forms a una pagina Sites, gli utenti non possono passare a una pagina Sites diversa e la pagina Sites si blocca in alcune occasioni. Il problema appare a intermittenza. (NPR-38506)
* Gli utenti sperimentano la sovrapposizione del testo in Adaptive Forms dopo l&#39;applicazione [!DNL Experience Manager] 6.5 Service Pack 11. (NPR-38376, CQ-4342472)
* Gli utenti rilevano un’eccezione durante lo spostamento dei pannelli dei moduli adattivi al nuovo layout dinamico. (NPR-38369)
* Il supporto ECMASCRIPT 6 (ES6) non è abilitato per la libreria client ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* Quando utilizzi un [!DNL Experience Manager] Flusso di lavoro per inviare un’e-mail in lingua ebraica, l’e-mail ricevuta alla fine dell’utente contiene punti interrogativi (??) invece del testo in lingua ebraica (NPR-38296).
* Gli utenti vengono disconnessi in modo casuale [!DNL Experience Manager] Impossibile inviare le istanze di pubblicazione e un modulo adattivo. Il problema viene visualizzato su [!DNL Experience Manager] istanze che utilizzano Dispatcher. (NPR-38285)
* Quando utilizzi l’opzione getFormDataString in una regola di Launch per acquisire i dati del modulo adattivo, l’opzione non restituisce i dati Forms adattivi. (NPR-38283)
* [!DNL Experience Manager] 6.5 L&#39;API java.acl.Group obsoleta per Forms e i seguenti messaggi di errore appaiono nel file error.log:
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* Forms creato in tedesco non riesce a tradurre in inglese o in qualsiasi altra lingua. (NPR-38280)
* Quando si utilizza una versione localizzata di un modulo adattivo, il documento di record corrispondente non viene localizzato. (NPR-38235)
* Quando si utilizza il passaggio Invia e-mail per inviare un allegato insieme a un messaggio e-mail, l’allegato non mantiene il nome specificato nel passaggio Flusso di lavoro. (NPR-38216)
* Quando viene pubblicata una nuova versione della lettera, gli utenti non possono aprire le bozze delle lettere precedenti. (NPR-38215, CQ-4342515)
* Quando si richiama un metodo del servizio end-point SOAP del servizio JEE di AEM Forms su un pulsante e si fa clic su configurato come regola di modulo adattivo, il servizio SOAP non riesce, con la seguente eccezione:
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* Quando si utilizza com.adobe.fd.pdfutility.services.PDFUtilityService#convertPDFtoXDP per convertire un PDF in formato XDP, viene restituito un file XDP non valido. (NPR-38140, CQ-4342099)
* Quando più utenti utilizzano Gestione Corrispondenza per generare lettere diverse, in anteprima viene visualizzata una lettera errata per alcuni utenti. (NPR-38134)
* Il componente AEM Forms incorporato nella pagina SITES utilizza l’attributo larghezza che ha valore in % e non è valido in base alla convalida W3C HTML. Errore di analisi degli utenti durante la convalida di HTML. (NPR-38124)
* Gli elementi dei pulsanti di scelta e delle caselle di controllo per la maggior parte dei temi OOTB nei moduli adattivi non fanno parte dell’ordine di tabulazione (NPR-38108)
* Quando un utente aggiunge tag HTML alla sezione commento durante l&#39;esecuzione di un flusso di lavoro, viene eseguito il rendering dei tag HTML. (NPR-37591)
* Durante l’importazione e la pubblicazione di una lettera che include un nuovo file XDP, le lettere non vengono visualizzate in anteprima nell’istanza di pubblicazione. Tuttavia, se le lettere vengono importate e pubblicate una seconda volta utilizzando lo stesso file CMP, le lettere vengono visualizzate in anteprima correttamente. (CQ-4343599)
* Il rendering di un modulo con la proprietà Prepare data process impostata non viene eseguito in HTML Workspace. (CQ-4343294)
* Per i PDF forms statici creati con Forms 6.5 Designer, l’accessibilità di PDF non riesce e viene generato un errore `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* Impossibile convertire un&#39;immagine in PDF utilizzando il servizio PDFG con OCR, dopo aver applicato la patch AEMForms-6.5.0-0038 (log4jv2.16). (CQ-4342450)
* Viene visualizzato un valore non corretto per il codice a barre SSCC-18. I server Forms omettono il valore nella parte destra del codice a barre. (CQ-4342400)
* Impossibile importare un file Microsoft® Word in Forms Designer. Errore dell&#39;utente `Word (version XP or onwards) could not be found on the machine`. (CQ-4342146)
* In Forms 6.5 Designer, quando si apre un modulo creato con Forms 6.1 Designer e si modifica una casella di testo, la spaziatura tra i paragrafi supera lo spazio specificato. Tutte le impostazioni precedenti dello spazio vengono rimosse e è necessario riformattare manualmente la casella di testo. (CQ-4341899)
* L&#39;utente non è in grado di impostare l&#39;ora personalizzata in Utilità di pianificazione rimozione processo. (CQ-4339192)
* L&#39;utente non è in grado di aggiornare alcuna configurazione nell&#39;interfaccia utente di gestione degli endpoint e si è verificato un errore ` Uncaught ReferenceError: updateEndpoint_required is not defined`. (CQ-4331523)
* Per i tag non validi, la gestione corretta del messaggio di errore non funziona come previsto. (NPR-38106 e CQ-4337173)

>[!NOTE]
>
>* I pacchetti del componente aggiuntivo [!DNL Experience Manager Forms] vengono rilasciati una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].


## Granite {#granite-6513}

* Omnisearch restituisce il risultato per gli utenti senza diritti di lettura. (NPR-38373)
* Abilita ES6 per `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## Integrazioni {#integrations-6513}

* Perdita di sessioni del risolutore risorse sul servizio Test e Target da UserInfoServlet obsoleto. (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak - Indicizzazione e query {#oak-6513}

* La versione Oak per la versione 6.5.13.0 è stata aggiornata alla versione 1.22.11. (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## Platform {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* Dipendenza da aggiornamento di `org.apache.httpcomponents.httpclient` in [!DNL Experience Manager] 6.5. (NPR-37999)
* Carico elevato dell’autore a causa dei suggerimenti sul campo del percorso. (CQ-4341826)
* L’utente deve aggiornare la pagina quando cambia il progetto dalla vista Scheda alla vista Calendario. (CQ-4340368)
* I tag vengono persi a causa di limitazioni delle autorizzazioni. (CQ-4339543)
* Problemi multipli segnalati con Ricerca e Filtro nella selezione del percorso non funzionanti. (CQ-4339402)
* Smetti di utilizzare DTM su 6.5 - passa a Launch per Omega Instrumentation e aggiungi il supporto Gainsight. (CQ-4337809)
* Limita la funzione di ricerca del componente del campo percorso in base alla proprietà del filtro del campo percorso impostata. (CQ-4309556)
* [!DNL Experience Manager] Piattaforma 6.5: Correzioni di denominazione locale cinese. (CQ-4308978)
* Passa a Launch per Omega Instrumentation. (NPR-38377)
* [!DNL Experience Manager] Piattaforma 6.5: Correzioni per la denominazione locale cinese. (CQ-4308978)

## Replica {#replication-6513}

* Pubblicazione del nodo utente Non riuscita da Autore a Editore. (NPR-38005)

## [!DNL Sites] {#sites-6513}

### Amministratore {#sites-admin-6513}

* È stata risolta la regressione introdotta con SP 12 che potrebbe aver causato un problema durante lo spostamento delle pagine. (SITES-5298)

### Interfaccia utente classica {#sites-classicui-6513}

* RTE: L’immagine aggiornata non è visibile quando si trascina una nuova immagine sopra un’immagine esistente. (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### Frammenti di contenuto {#sites-contentfragments-6513}

* È supportata la creazione di modelli di frammenti di contenuto nelle sottoconfigurazioni. (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* Migliorare le prestazioni quando si utilizza la convalida &quot;Campo univoco&quot; nel modello a frammento di contenuto. (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* Migliorare il tempo di risposta all’apertura dell’Editor modello frammento di contenuto. I clienti con numerosi frammenti in Assets potrebbero aver visto errori all’apertura. (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* È stata introdotta una regressione di correzione durante l’aggiornamento da 6.5.11 a 6.5.12 che potrebbe aver causato errori nell’Editor modello frammento di contenuto. (SITES-5088 e SITES-4967)

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* Migliorare la localizzazione dell&#39;interfaccia utente dell&#39;Editor modello frammento di contenuto. (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* È stato corretto un problema a causa del quale la chiusura dell’Editor frammento di contenuto poteva causare un errore quando si utilizzava il server di authoring con Dispatcher. (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* È stato risolto un problema che impediva il salvataggio di un modello quando la convalida veniva utilizzata in un campo RTE. (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* Problema relativo al frammento di contenuto con la proprietà booleana che non mostra il testo del campo in &quot;title&quot;, ma mostra &quot;Nome proprietà&quot;. (NPR-38244)
* Errore durante l&#39;esecuzione della query persistente con la variabile di query tramite Postman. (NPR-38251, NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* Componente frammento di contenuto: Regressione nell&#39;opzione &quot;intestazioni handle come paragrafi&quot; fissa che era 6.5 SP7. (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* È stata corretta la regressione introdotta in 6.5.11 che può aver causato errori di ricerca delle risorse. (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* Utilizzo **[!UICONTROL Modifica]** dai risultati della ricerca potrebbe risultare in un `Not Found` errore. (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* I modelli dell’interfaccia utente di Context Hub non vengono sottoposti correttamente al rendering senza un aggiornamento della pagina. (NPR-38212)

### Editor e-mail {#sites-emaileditor-6513}

* Abilita il supporto per la prossima versione dei componenti core per e-mail [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445 e NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### Frammenti di esperienza {#sites-experiencefragments-6513}

* Quando utilizzi l’azione Passa a pagina nei Riferimenti per un frammento esperienza, viene aperta la pagina errata. (NPR-38062)
* Proprietà di layout provenienti dal modello XF non osservate al lato di una pagina. (NPR-38214)
* Migliori prestazioni del calcolo del riferimento XF. (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### Editor pagina {#sites-pageeditor-6513}

* Migliorare l’annullamento per i componenti che non dispongono della funzione di modifica in linea o di destinazione nel `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* Il menu a discesa Sistema di stili potrebbe essere stato posizionato nella parte superiore della pagina anziché nel contesto del componente, per i componenti che utilizzano `cq:editConfig` &quot;post-modifica: REFRESH_PAGE&quot;. Questo problema è stato risolto. (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* Il componente testo non è allineato quando viene aggiunto ai contenitori di layout nidificati. (NPR-38193)
* Una scheda stile vuota era visualizzata quando non era presente alcuna configurazione del sistema di stili per un componente; la scheda ora è nascosta quando non è presente alcuna configurazione. (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* La proprietà `useLegacyResponsiveBehaviour` funziona solo se autenticato. (NPR-37996)
* L’aggiornamento di jquery-ui all’ultima versione causava l’interruzione dell’editor. (SITES-5647)

### Sicurezza {#sites-security-6513}

* L&#39;interfaccia utente di Gestione dei gruppi di utenti a volte non è riuscita a rimuovere gli utenti, in particolare nei gruppi con +20 utenti. (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* Sitemap Generator e i tag Canonical aggiungono supporto per gli URL senza .html. (CIF-2647)
* Aggiungi il supporto per la rimozione di lingue alternative utilizzando la configurazione noindex. (CIF-2496)
* Aggiungi il supporto per fornire un URL personalizzato per sovrascrivere l’URL canonico predefinito per le pagine con contenuto quasi identico. (CIF-2747)

### Editor SPA e SDK {#sites-spa-sdk-6513}

* A partire dalla versione 6.5.13, non è più necessario creare il nodo del componente contenitore in JCR prima di apportare modifiche tramite l’editor SPA. A `virtual container` viene creato prima di salvarlo tramite l’SDK. (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### Editor modelli {#sites-templateeditor-6513}

* Correggi la regressione secondo cui la pubblicazione di un modello modificato non pubblicava tutte le dipendenze. (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* Il valoreMap TemplatedResource deve consentire letture profonde secondo l&#39;API ValueMap. (NPR-38439)

## Sling {#sling-6513}

* Perdita di memoria `DiscoveryLiteDescriptor`. (NPR-38288)
* Aggiorna `sling-javax.activation` bundle con fix di SLING-8777. (NPR-38077)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## Progetti di traduzione {#translation-6513}

* Creazione di più lanci per le pagine di riferimento/xf. (NPR-38263)
* È stato modificato il comportamento dell’aggiunta di pagine ai progetti di traduzione a partire dal Service Pack 10. Il progetto di traduzione non contiene una pagina appena creata [ex: test-page-women-2] nell’elenco, se selezionato come elemento padre della nuova pagina creata [non la nuova pagina creata direttamente]. (NPR-38256)
* Aggiungi `cq:isTranslationLaunch` in Lanci creati dal progetto di traduzione. (NPR-38224)
* Viene creato Launch per una pagina con un XF di riferimento contenente una risorsa. (NPR-38199)
* [!DNL Experience Manager] l&#39;aggiornamento della memoria di traduzione non funziona. (NPR-38196)
* Abilita ES6 per `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* Ultimo pacchetto 18n per traduzioni per [!DNL Experience Manager] 6.5. (CQ-4339505)

## Interfaccia utente {#ui-6513}

* Quando ti trovi nella pagina iniziale > Sezione Strumenti e fai clic sul pulsante [!DNL Experience Manager] l&#39;icona [!DNL Experience Manager] Viene visualizzata la schermata di navigazione. (NPR-38417)
* Abilita ES6 per `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* Abilita ES6 per `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* Il selettore data nell’interfaccia touch viene visualizzato in coreano. (NPR-38079)
* Finestra di dialogo di authoring con più campi, dopo aver riordinato i campi perdendo il valore di selezione del pulsante di scelta. (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM (Campaign) 6.5: Correzioni di denominazione locale cinese. (CQ-4308973)
* ResourceResolver non chiuso in com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification (NPR-38286)

## Installa [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0 richiede [!DNL Experience Manager] 6.5. Vedi [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate.
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.13.0 su una delle istanze Autore che utilizza Gestione pacchetti.

>[!NOTE]
>
>Adobe sconsiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.13.0.

### Installa il service pack su [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia un riavvio se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di installare, scegli uno snapshot o un nuovo backup del tuo [!DNL Experience Manager] istanza.

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip).

1. Apri Gestione pacchetti e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l&#39;istanza dopo l&#39;installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l&#39;istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude durante l’installazione del service pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere, questo problema si verifica in [!DNL Safari] browser ma può verificarsi a intermittenza su qualsiasi browser.

**Installazione automatica**

Esistono due metodi diversi per l&#39;installazione automatica [!DNL Experience Manager] 6.5.13.0.

* Inserire il pacchetto in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza la [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzo `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0 non supporta l’installazione di Bootstrap.

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo con questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. La pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa di versione aggiornata `Adobe Experience Manager (6.5.13.0)` sotto [!UICONTROL Prodotti installati].

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (Usa console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.2.2.3 o successiva (Utilizzare la console Web: `/system/console/bundles`).


### Installa [!DNL Experience Manager] Pacchetto aggiuntivo di Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora se non utilizzi [!DNL Experience Manager] Forms. Correzioni in [!DNL Experience Manager] Forms viene fornito tramite un pacchetto aggiuntivo separato una settimana dopo il programma [!DNL Experience Manager] Versione Service Pack.

1. Assicurati di aver installato la [!DNL Experience Manager] Service Pack.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) per il sistema operativo in uso.
1. Installa il pacchetto aggiuntivo di Forms come descritto in [Installazione dei pacchetti aggiuntivi di AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installa [!DNL Experience Manager] Forms su JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Correzioni in [!DNL Experience Manager] Forms su JEE viene fornito tramite un programma di installazione separato.

Per informazioni sull&#39;installazione del programma di installazione cumulativo per [!DNL Experience Manager] Forms su JEE e configurazione post-distribuzione, vedi [note sulla versione](jee-patch-installer-65.md).

>[!NOTE]
>
>Dopo aver installato il programma di installazione cumulativo per [!DNL Experience Manager] Forms su JEE, installa il pacchetto aggiuntivo Forms più recente, elimina il pacchetto aggiuntivo Forms dal `crx-repository\install` e riavviare il server.

### UberJar {#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.13.0 è disponibile nella [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://).

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includere nel POM del progetto la seguente dipendenza:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
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
| Integrazioni | La **[!UICONTROL Opt-in di AEM Cloud Services]** la schermata è obsoleta poiché la [!DNL Experience Manager] e [!DNL Adobe Target] l&#39;integrazione viene aggiornata in [!DNL Experience Manager] 6.5. L’integrazione supporta l’API Adobe Target Standard. L’API utilizza l’autenticazione tramite Adobe IMS e [!DNL Adobe I/O]. Sostiene il ruolo crescente di Launch Adobe per lo strumento [!DNL Experience Manager] nelle pagine di analisi e personalizzazione, la procedura guidata di consenso è funzionalmente irrilevante. | Configura le connessioni di sistema, l’autenticazione Adobe IMS e [!DNL Adobe I/O] integrazioni tramite le rispettive [!DNL Experience Manager] servizi cloud. |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto per [!DNL Experience Manager] 6.5. | N/D |

## Problemi noti {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [Frammento di contenuto AEM con pacchetto indice GraphQL 1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* Come [!DNL Microsoft® Windows Server 2019] non supporta [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] non supporta installazioni chiavi in mano per [!DNL AEM Forms 6.5.10.0].

* Se stai aggiornando il tuo [!DNL Experience Manager] istanza dalla versione 6.5 alla versione 6.5.10.0, puoi visualizzare `RRD4JReporter` eccezioni `error.log` file. Per risolvere il problema, riavvia l&#39;istanza.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 10 o un service pack precedente su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminato.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Gli utenti possono rinominare una cartella in una gerarchia [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando l’integrazione Adobe Target è configurata in [!DNL Experience Manager] se si utilizza l’API di Target Standard (autenticazione IMS) e poi si esportano frammenti di esperienza in Target, vengono creati tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

* Quando si tenta di spostare/eliminare/pubblicare frammenti di contenuto o siti/pagine, si verifica un problema quando i riferimenti ai frammenti di contenuto vengono recuperati, in seguito a un errore della query in background; ovvero la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell&#39;indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.13.0:

* [Elenco dei bundle OSGi inclusi nell&#39;Experience Manager 6.5.13.0](/help/release-notes/assets/65130_bundles.txt)

* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.13.0](/help/release-notes/assets/65130_packages.txt)

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina di prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

