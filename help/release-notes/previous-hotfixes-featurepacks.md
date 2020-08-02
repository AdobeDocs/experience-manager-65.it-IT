---
title: ' Adobe Experience Manager 6.5 Note sulla versione del Service Pack precedente'
description: Note sulla versione specifiche per  Adobe Experience Manager 6.5 Service Pack 3 e versioni precedenti.
contentOwner: AK
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '8108'
ht-degree: 36%

---


# Hotfix e Feature Pack inclusi nei Service Pack precedenti {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

 Adobe Experience Manager 6.5.4.0 è un aggiornamento importante che include nuove funzioni, miglioramenti e prestazioni richiesti dai clienti chiave, stabilità, miglioramenti a livello di sicurezza, rilasciati a partire dalla release 6.5 di **aprile 2019**. Può essere installato sopra  Adobe Experience Manager 6.5.

Alcune funzioni chiave e miglioramenti introdotti  Adobe Experience Manager 6.5.4.0 includono:

*  risorse Adobe Experience Manager è ora configurato con Portale marchio tramite  console I/O Adobe.

* È ora disponibile un nuovo passaggio [Genera output](../forms/using/aem-forms-workflow-step-reference.md) stampabile per  flussi di lavoro Adobe Experience Manager Forms.

* [Supporto](../forms/using/resize-using-layout-mode.md) a più colonne per la modalità di layout per moduli adattivi e comunicazioni interattive.

* Supporto per [Rich Text](../forms/using/designing-form-template.md) nei moduli HTML5.

* [Miglioramenti](new-features-latest-service-pack.md#accessibility-enhancements) all’accessibilità in  risorse Experienci Manager.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.8.

* Ora potete sincronizzare le sottostrutture di contenuto selettivo nella modalità *Dynamic Media - Scene7 invece di tutte le sottostrutture disponibili in* `content/dam`.

* L&#39;integrazione del modello dati del modulo con il servizio Web SOAP ora supporta i gruppi di scelta o gli attributi sugli elementi.

* Le strutture di input o output SOAP e i dati complessi ora supportano la sostituzione di gruppi dinamici.

Per un elenco completo delle funzioni e delle caratteristiche principali introdotte nei Service Pack più recenti, consulta [Novità  Adobe Experience Manager 6.5 Service Pack](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Quando un URL di pagine Adobe Experience Manager Sites  contiene due punti (`:`) o simboli di percentuale (`%`), il browser smette di rispondere e i picchi di utilizzo della CPU (NPR-32369, NPR-31918).

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

* In SPS (Scene7 Publishing System) viene creata una cartella senza nome durante lo spostamento di una risorsa da una cartella all’altra in  Experience Manager con configurazione Dynamic Media Scene7 (NPR-32440).

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

* La pagina dei dettagli delle risorse PDF non mostra i pulsanti delle azioni eccetto A raccolta e Aggiungi rappresentazione nell&#39;Experience Manager  esecuzione in modalità Scene7 Dynamic Media (CQ-4286705).

* L&#39;elaborazione delle risorse richiede troppo tempo durante il processo di caricamento batch di Scene7 (CQ-4286445).

* Il pulsante Salva non importa il set remoto se l&#39;utente non ha apportato modifiche nell&#39;Editor set nel client Dynamic Media (CQ-4285690).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene assimilato  Experience Manager (CQ-4283701).

* Lo stato non elaborato del predefinito per visualizzatori video per ritaglio avanzato viene visualizzato due volte sul testo del banner e sul nome del predefinito (CQ-4283517).

* L’altezza contenitore errata di un modello 3D caricato visualizzato in anteprima nel visualizzatore 3D viene visualizzata nella pagina dei dettagli della risorsa (CQ-4283309).

* Carosello Editor non si apre in IE 11 in modalità ibrida Dynamic Media  Experience Manager (CQ-4255590).

* Lo stato attivo si blocca nel menu a discesa E-mail nella finestra di dialogo Download, nei browser Chrome e Safari (NPR-32067).

* La casella di controllo Sincronizza tutto il contenuto non è abilitata per impostazione predefinita quando si tenta di aggiungere la configurazione cloud DM sul  Experience Manager (CQ-4288533).

### Interfaccia di base {#foundation-ui-6540}

* Il controllo del mouse passa al campo filtro precedente invece di rimanere nel campo filtro esistente durante la ricerca delle risorse mediante il pannello Filtro (NPR-32538).

* Assegnazione tag Platform: La ricerca di tag digitando nei campi tag mostra i tag al di fuori dei limiti principali e non rispetta la `rootPath` proprietà dei campi tag (NPR-31895).

* Interfaccia utente Platform: Se nel campo di testo viene aggiunto un percorso non valido (NPR-31884), il browser del percorso si interrompe.

* La notifica viene nascosta dietro un menu fisso nella selezione delle pagine (NPR-31628).

### Platform {#platform-sling-6540}

* (HTL) I caratteri di sottolineatura sostituiscono i due punti nella sezione del percorso dell&#39;URL (NPR-32231).

### Progetti {#projects-6540}

* Il pulsante Crea non è visibile all&#39;utente anche se l&#39;utente dispone dell&#39;autorizzazione per creare un progetto nella sottocartella (NPR-31832).

### Traduzione progetti {#projects-translation-6540}

* La creazione di progetti di traduzione interrompe l&#39;interfaccia utente quando l&#39;opzione Rifila spazi è attivata in `Apache Sling JSP Script Handler` (NPR-32154).

* L&#39;errore nell&#39;interfaccia utente e l&#39;eccezione del punto Null nei registri di errore viene rilevato quando un tag, da tradurre, viene aggiunto a un progetto di traduzione (NPR-31896).

### Integrations (Integrazioni){#integrations-6540}

* La generazione dell&#39;URL della libreria di avvio è basata solo su `path` e `library_name` valori dell&#39;API di Launch e non è basata su `library_path` valori (NPR-31550).

* Viene visualizzato un messaggio di errore durante l&#39;elaborazione degli elementi correlati a LiveFyre (FYR-12420).

* ReportSuitesServlet è vulnerabile all&#39;SSRF (NPR-32156).

### Editor modelli WCM {#wcm-template-editor-6540}

* In modalità struttura modelli modificabili, l&#39;elenco dei componenti consentiti nel contenitore di layout non visualizza il componente pulsante di collegamento (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Si è verificato un errore durante la selezione di una sovrapposizione e la selezione di componenti reattivi Trascinate qui i componenti (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* La configurazione cloud di Target non riesce e la richiesta di mbox di ricezione dell&#39;errore non è riuscita (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Gli utenti di Brand Portal non sono in grado di pubblicare le risorse delle cartelle dei contributi [!DNL Assets] in caso di aggiornamento a  I/O Adobe all&#39;Experience Manager 6.5.4 (CQDOC-15655). Per una correzione immediata all&#39; Experience Manager 6.5.4, si consiglia di [scaricare l&#39;hotfix](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e installarlo nell&#39;istanza di creazione.

* I valori popup dello schema di metadati non sono visibili nelle proprietà delle risorse (CQ-4283287).

* Il sottoschema metadati non visualizza schede in base al tipo di mimetismo nelle proprietà delle risorse (CQ-4283288).

* Lo schema di metadati Annulla pubblicazione compila un messaggio di errore anche se lo schema viene rimosso nel backend.

* L&#39;immagine di anteprima non viene visualizzata per una risorsa pubblicata (CQ-4285886).

* L&#39;utente non può pubblicare o annullare la pubblicazione di risorse contenenti virgolette singole nel nome (CQ-4272686).

* I termini e le condizioni non vengono visualizzati durante il download di più risorse (CQ-4281224).

* Sono state risolte vulnerabilità di sicurezza minori.

### Communities {#communities-6540}

* Il modulo Crea membro viene visualizzato come una pagina vuota (NPR-31997).

* L&#39;utente non è in grado di visualizzare il  rapporto Analytics sull&#39;istanza di creazione (NPR-30913).

### Quercia - Indicizzazione e query {#oak-indexing-6540}

* Documenti MS Word e MS Excel contenenti immagini JPEG, se analizzati con il parser Tika non riescono ad analizzare e la classe non trova errore (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
> Experience Manager Service Pack non include correzioni per  Experience Manager Forms. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per  Adobe Experience Manager Forms su JEE. Per ulteriori informazioni, consultate [Installare  Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare  Experience Manager Forms in JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gestione corrispondenza: Le lettere contengono caratteri aggiuntivi dopo l&#39;invio ai flussi di lavoro di post-elaborazione (NPR-32626).

* Gestione corrispondenza: Le lettere visualizzano un segnaposto a discesa come componente di testo dopo l&#39;invio ai flussi di lavoro successivi al processo (NPR-32539).

* Gestione corrispondenza: I valori predefiniti definiti nel modello di lettera non vengono visualizzati nella modalità Anteprima (NPR-32511).

* Mobile Forms: Il pulsante di invio viene visualizzato come espanso nelle dimensioni durante il rendering di un modulo XDP in una versione HTML (NPR-32514).

* Document Services: Problemi di accesso agli URL per Lettere e altre pagine dopo l’applicazione di Service Pack 2 (NPR-32508, NPR-32509).

* Document Services: Se il numero di transazioni su un server supera un limite specifico, la conversione da HTML a PDF non riesce e le impostazioni del tipo di file vengono rimosse dal [!DNL Forms] server (NPR-32204).

* Forms adattivo: Lo strumento di accessibilità del browser segnala gli errori nei moduli adattivi in base alle linee guida WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Forms adattivo: Lo strumento di accessibilità del browser Chrome segnala un errore best practice (NPR-32310).

* Forms adattivo: Problemi di traduzione durante la configurazione di un modulo adattivo incorporato in una pagina di siti di Experience Manager  (NPR-32168).

* Workbench: Viene visualizzato un messaggio di errore durante l&#39;utilizzo dell&#39;operazione Ottieni proprietà PDF per il servizio Utilità PDF (NPR-32150).

* Document Security: Un file PDF protetto non viene aperto offline con l&#39;opzione DisableGlobalOfflineSynchronizationData impostata su True (NPR-32078).

* Designer: Se l&#39;opzione relativa ai tag è attivata, il bordo del sottomodulo scompare nell&#39;output PDF generato (NPR-32547, NPR-31983, NPR-31950).

* Designer: Se in una tabella sono presenti celle unite, il test di accessibilità non riesce per il file PDF di output convertito da un modulo XDP utilizzando il servizio di output (CQ-4285372).

* Foundation JEE: Se un server Forms di Experience Manager  è disconnesso da un cluster, i problemi di cache ne impediscono la riconnessione al server (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 è una versione importante che include correzioni e miglioramenti a livello di prestazioni, stabilità e sicurezza introdotti dai clienti a partire dalla release 6.5 di **aprile 2019**. It can be installed on top of [!DNL Adobe Experience Manager] 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.6.

* [!DNL Experience Manager Assets] ora supporta gli archivi ZIP creati utilizzando l&#39;algoritmo Deflate64.

* La nuova colonna relativa alla data di creazione, ordinabile, è stata aggiunta nella visualizzazione a elenco DAM e nei risultati della ricerca di risorse nella visualizzazione a elenco.

* L’ordinamento delle risorse basato sulla colonna Nome è stato attivato nella visualizzazione Elenco.

* [!DNL Dynamic Media] ora supporta la funzione di ritaglio avanzato delle risorse video. Smart Crop è una funzione guidata di apprendimento automatico che ritaglia un video mentre si sposta il fotogramma per seguire il punto focale della scena.

* [!DNL Dynamic Media] supporta le immagini intelligenti.

* Possibilità di [impostare le preferenze di Office](../forms/using/configure-out-of-office-settings.md) nei [!DNL Experience Manager] flussi di lavoro.

* Possibilità di [condividere elementi](../forms/using/configure-shared-queues-osgi.md) Inbox o Inbox con altri utenti nei [!DNL Experience Manager] flussi di lavoro.

* Possibilità di [generare comunicazioni interattive in modalità](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

* È stata aggiornata la versione di jQuery inclusa nel pacchetto ContextHub alla 3.4.1.

### Assets {#assets-6530-enhancements}

**Miglioramenti apportati al prodotto**

* [!DNL Experience Manager Assets] ora supporta gli archivi ZIP creati utilizzando l&#39;algoritmo Deflate64 (NPR-27573).

* La nuova colonna relativa alla data di creazione, ordinabile, viene aggiunta nella visualizzazione a elenco DAM e nei risultati della ricerca di risorse nella visualizzazione a elenco (NPR-31312).

* Nella vista a elenco, gli utenti possono ordinare l’elenco delle risorse utilizzando la colonna [!UICONTROL Nome] (NPR-31299).

* I file GLB, GLTF, OBJ e STL possono essere visualizzati in anteprima nella pagina Dettagli  risorsa in DAM (CQ-4282277).

* `ReplicationOnModifyListener` viene attivato per i nodi di blocco durante il caricamento di blocchi in [!DNL Dynamic Media] (CQ-4281279).

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

* Selezione cartella L&#39;elemento azione Crea > Caricamento file non è presente quando ACL per Rifiuta `jcr:removeChildNodes` e `jcr:removeNode` sul percorso vengono applicati a un utente (NPR-30840).

* I flussi di lavoro DAM diventano obsoleti quando vengono caricate determinate risorse mp4, causando il blocco di tutti i flussi di lavoro rimanenti (NPR-30662).

* Errore di memoria insufficiente quando un file PDF di grandi dimensioni (di diversi Gigabyte) viene caricato in DAM e le relative risorse secondarie vengono elaborate (NPR-30614).

* Lo spostamento di massa delle risorse non riesce e viene visualizzato un messaggio di avviso (NPR-30610).

* I nomi delle risorse vengono modificati in lettere maiuscole quando si spostano le risorse da una cartella all&#39;altra in [!DNL Experience Manager] esecuzione in modalità [!DNL Dynamic Media]Scene7 (NPR-31630).

* Durante la modifica di un set di immagini remoto, si verifica un errore per l&#39;immagine che risiede nella cartella denominata uguale al nome della società Scene7 (NPR-31340).

* [!DNL Dynamic Media] le risorse contenenti riferimenti non vengono pubblicate (NPR-31180).

* Il completamento dei caricamenti dalla modalità [!DNL Dynamic Media]7-Scene7 [!DNL Dynamic Media Classic] richiede troppo tempo (NPR-31048).

* L’area sensibile aggiunta a una risorsa immagine non è visibile tramite il visualizzatore immagini interattivo nella pagina dei dettagli della risorsa (NPR-30979).

* Vengono creati enormi processi di sling e il banner di elaborazione viene nuovamente visualizzato quando le azioni eseguite sulle risorse in [!DNL Experience manager Assets] vengono trasmesse ad Scene7 (NPR-30947).

* Si verifica un conflitto durante la creazione della copia in lingua delle risorse e delle risorse non caricate in Scene7 (NPR-30932).

* Le rappresentazioni dinamiche scaricate dall&#39; [!DNL Experience Manager] esecuzione in modalità [!DNL Dynamic Media]ibrida sono interrotte (sono di tipo testo con contenuto &quot;impossibile trovare l&#39;immagine&quot; invece del tipo di contenuto dell&#39;immagine) (NPR-30876).

* [!DNL Dynamic Media] Il flusso di lavoro di codifica video non riesce a generare le miniature per il video migrato dalla modalità [!DNL Dynamic Media Classic] [!DNL Dynamic Media]Scene7 al  Adobe Experience Manager (CQ-4282011).

* IpsApiException durante la migrazione delle risorse da un’istanza all’altra tramite ID società Scene7 diversi (CQ-4280548).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene assimilato in [!DNL Experience Manager] (CQ-4283701).

* I pulsanti di scorrimento vengono visualizzati nel visualizzatore, se una risorsa 3D dispone di poche viste della fotocamera (CQ-4283322).

* Altezza contenitore errata di un modello 3D caricato visualizzato in anteprima nel visualizzatore dimensionale nella pagina Dettagli risorsa (CQ-4283309).

* I video non possono essere riprodotti con SmartCropVideoViewer su Internet Explorer 11 e Safari (CQ-4281422).

* L’utilizzo del pulsante Sposta per spostare più risorse, da una cartella all’altra, non riesce in [!DNL Experience Manager] esecuzione in modalità [!DNL Dynamic Media]Scene7 (CQ-4280384).

* I video distorti vengono visualizzati sui dettagli delle risorse quando il tipo MIME è diverso da MP4 (CQ-4279704).

* I video appena caricati in cartelle con profilo video restano nello stato di elaborazione anche dopo il completamento della percentuale di codifica al 100% (CQ-4279389).

* Lo spostamento delle risorse da una cartella crea un numero elevato di processi Sling (chiamate API Scene7) rispetto a quanto richiesto idealmente (CQ-4278664).

* I nomi del set di immagini vengono modificati in minuscolo in Scene7, quando viene creato un set di immagini (o un set di file multimediali) e vengono denominati con la convenzione di denominazione appropriata in DAM (CQ-4281112).

* Scene7 Migrator imposta lo stato di pubblicazione in modo errato (CQ-4263492).

* La ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) nella pagina dei risultati scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente nei frammenti di contenuto (CQ-4282898).

* I file PDF non sono indicizzati e il contenuto al loro interno non è ricercabile (CQ-4278916).

* Errore &quot;Gruppo non elencato dal selettore utente: previsto da false a uguale a true&quot; viene osservato per l&#39;aggiunta di Closed User Group con different `principalName` and `authorizableId` (CQ-4278177).

* La vista a colonne dell&#39;interfaccia utente delle risorse mostra tutti i percorsi indipendentemente dal percorso radice del tenant specifico (CQ-4278175).

* La ricerca del selettore delle risorse non funziona come previsto (CQ-4275886).

* Flussi di lavoro di rappresentazione non riusciti (CQ-4271928).

* DAM Event Purge elimina i dati dell&#39;evento più recenti (`maxSavedActivities`) e contiene i dati creati in precedenza (NPR-31336).

* La pagina dei risultati della ricerca nell&#39;interfaccia touch (realizzata tramite Omnisearch) scorre automaticamente verso l&#39;alto e perde la posizione di scorrimento dell&#39;utente (NPR-31307).

* La barra delle azioni e il conteggio delle risorse non si aggiornano quando si selezionano tutti gli elementi (cartelle o singole risorse) nell&#39;interfaccia utente touch (NPR-31118).

* Durante [!DNL Experience Manager] il polling dei dettagli del processo di una risorsa, viene visualizzata un’eccezione (CQ-4283569).

### Sites {#sites}

* Se l&#39;ereditarietà LiveCopy è interrotta, nelle pagine di LiveCopy sono visualizzati i collegamenti per la copia della lingua invece dei collegamenti LiveCopy (NPR-30980).
* Per una nuova Blueprint, Se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza righe vuote per gli altri record (NPR-31182).
* Quando un utente aggiunge caratteri giapponesi o coreani nella proprietà description di un menu, nel menu vengono visualizzati caratteri distorti per il testo in lingua giapponese e coreana (NPR-31331).
* Editor Rich Text (RTE) non consente di inserire una tabella incorporata come voce di elenco (NPR-30879).
* Escluso, scaffolding Rich Text Editor (RTE). applica la dimensione del font in linea agli elementi, in modo imprevisto (NPR-31284).
* Quando un utente sposta lo stato attivo sui campi della barra a sinistra e utilizza una scelta rapida da tastiera per incollare il contenuto, viene incollato il contenuto degli Appunti dell’Editor pagina invece del contenuto copiato dai campi della barra a sinistra (NPR-31172).
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso dell’immagine viene memorizzato nel nodo componente invece del nodo multi-campo (NPR-30882).
* L&#39; `ResponsiveGridExporter` API non restituisce `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` l&#39;interfaccia. Il `com.day.cq.wcm.foundation.model.impl` pacchetto è dichiarato come pacchetto privato (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il `editor.html` prefisso e, `wcmmode=disabled`o in Publisher)., la richiesta termina con il codice di errore dello stato HTTP `500` (NPR-30743).
* Gli utenti non possono modificare la password e accedere alla pagina del profilo (NPR-31161).

### Ricerca e interfaccia utente {#ui-interface-and-search}

* Quando si passa dalla vista a schede alla vista a elenco in una pagina dei risultati di ricerca, si verifica un ritardo prima dello scorrimento della pagina (NPR-31286).

* La casella di controllo [!UICONTROL Seleziona tutto] è nascosta nella vista a elenco dell&#39;interfaccia [!DNL Sites] utente (NPR-31614).

* Il conteggio [!UICONTROL Seleziona tutto] in una pagina di risultati della ricerca non è corretto (NPR-31120).

* L&#39;editor di metadati visualizza i tag che non esistono (NPR-31119).

### Traduzione {#translation}

* Due finestre a comparsa del calendario vengono visualizzate quando si seleziona l&#39;opzione Data scadenza in un processo di traduzione (NPR-31270).

### Platform {#platform}

* L&#39;opzione Tipo mime nella console Web non funziona (NPR-31108).

* Il certificato client non è accettato durante la configurazione del single sign-on (NPR-31165).

* Gli aggiornamenti nella configurazione della dimensione del buffer per il servizio HTTP basato su Jetty non vengono salvati (NPR-30925).

* QueryBuilder supporta ora l&#39;ordine ``fn:name()`` nelle query xpath (NPR-31322).

* L&#39;albero di attivazione duplicato viene creato durante l&#39;aggiornamento dalla versione [!DNL Experience Manager] 6.3 (NPR-31513).

* Le richieste inoltrate non conservano le intestazioni di risposta impostate durante l&#39;autenticazione Sling (NPR-30013).

* La ricerca all&#39;interno dei componenti del selettore non funziona (NPR-31692).

* Viene visualizzato un errore quando si allega un file ZIP a un [!DNL Experience Manager Communities] post a causa di diverse versioni del bundle Apache POI e Apache Tika (NPR-31018).

* Il ``org.apache.sling.distribution.api`` bundle è nascosto nel gestore di configurazione e pertanto non è disponibile per i bundle personalizzati (NPR-31720).

### Progetti {#projects}

* La sostituzione delle viste del calendario non funziona (NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**Miglioramenti apportati al prodotto**

* Il flusso di lavoro di importazione di Asset Sourcing in [!DNL Experience Manager Assets] viene modificato per recuperare solo le risorse appena create da [!DNL Brand Portal] a [!DNL Experience Manager], e per evitare la replica ignorate le risorse già presenti nella cartella NEW (CQ-4278527).

**Problemi risolti**

* Quando si crea una nuova cartella Contribution nella funzione Asset Sourcing (CQ-4282825), viene visualizzata un’icona errata.
* Quando create una nuova cartella Contribution, una o entrambe le sottocartelle (NEW e SHARED) non vengono visualizzate all’interno della cartella Contribution (CQ-4282424).
* Il sistema genera un’eccezione se l’utente tenta di ripubblicare la cartella Contribution da [!DNL Experience Manager] a [!DNL Brand Portal] dopo aver ricevuto nuove risorse dalla [!DNL Brand Portal] fine della cartella Contribution (CQ-4279740).
* La creazione di una cartella Contribution all’interno di una cartella Contribution (cartella nidificata) non è consentita per evitare la complessità (CQ-4278391).
* Il sistema genera un&#39;eccezione durante il caricamento dell&#39;elenco di [!DNL Brand Portal] utenti (file .csv) importato da [!DNL Experience Manager] Admin Console. Nel file .csv sono obbligatori solo i campi Email, FirstName e LastName (CQ-4278390).

### Communities {#communities-6530}

**Problemi risolti**

* I collegamenti rapidi per gestire i gruppi (Open/Edit/Publish/Delete Groups) non sono visibili agli amministratori della community (Group admin/Site admin) (NPR-31627).
* Un blog inviato viene visualizzato solo se la pagina viene aggiornata/ricaricata manualmente (NPR-31599).
* La query JCR utilizzata dalla funzione &quot;Mentions&quot; è sensibile alle maiuscole/minuscole e richiede troppo tempo per restituire i risultati (NPR-31475).
* [!DNL Experience Manager] 6.5 Il file UberJar genera un&#39;eccezione, `cq-social-translation` bundle mancante nel file [!DNL Experience Manager] UberJar 6.5 (NPR-31186).
* Librerie Databind di Jackson aggiornate alla versione 2.9.9.3 per risolvere nuove vulnerabilità (NPR-30967).
* I titoli di Attività e Notifiche non sono coerenti (NPR-30941).
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Quercia {#oak}

* Aggiornamenti dell&#39;indice Lucene che rallentano il server di creazione (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per [!DNL Experience Manager Forms]. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. Per ulteriori informazioni, consultate [Installare  Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare  Experience Manager Forms in JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Pacchetto di componenti aggiuntivi per Forms {#forms-add-on-package-6530}

**Moduli adattivi**

* Le stringhe contengono la chiave del dizionario durante la localizzazione dei moduli adattivi (NPR-31110).

**Comunicazione interattiva**

* **MissingNode.toString()** restituisce risultati imprecisi dopo aver aggiornato le librerie Jackson a 2.10.0 (NPR-31549).

* L&#39;editor di testo rimuove in modo casuale gli spazi dal testo copiato da Microsoft Word (NPR-31113).

**Gestione della corrispondenza**

* Le didascalie e le descrizioni comandi non vengono visualizzate durante la migrazione delle lettere dal LiveCycle ES4SP1 a [!DNL Experience Manager] 6.5 (NPR-31615).

* **Durante il salvataggio delle lettere come bozze (NPR-30463), la formattazione del flusso di testo non è più supportata** .

**Flusso di lavoro**

* Il flusso di lavoro OSGi non riesce a causa dell&#39;utilizzo della CPU al 100% (NPR-31233).

**Moduli HTML5**

* Quando si genera l’anteprima HTML5 di un modulo XDP, viene visualizzato uno sfarfallio durante l’aggiunta di istanze di un sottomodulo (NPR-30909).

#### Forms sul programma di installazione JEE {#forms-jee-installer-6530}

**Forms - Servizi basati su documenti**

* Il servizio Web SOAP che utilizza MTOM in un progetto .NET visualizza le eccezioni per i metodi AssemblerServiceClient invoke e HtmlToPDF2 (NPR-4281771).

* [Le versioni 1.4 e 1.4.1](https://helpx.adobe.com/it/aem-forms/quick-fixes/6-5/jee-patch-0014.html) dell&#39;Axis Jar includono una vulnerabilità di sicurezza (NPR-31015).

**JEE per Foundation**

* La configurazione dell&#39;azione non carica i nomi dei processi per Richiamare un&#39;azione di invio di un Forms Workflow (NPR-31478).

### Feature Pack inclusi {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms - JEE di base {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Supporto Forms per Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 è una versione importante che include correzioni e miglioramenti a livello di prestazioni, stabilità e sicurezza introdotti dai clienti a partire dalla data di disponibilità generale del [!DNL Adobe Experience Manager] 6.5 di **aprile 2019**. It can be installed on top of [!DNL Experience Manager] 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.3.
* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per [!DNL Adobe Target].
* Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Consulta la sezione sull’[utilizzo di risorse collegate](../assets/use-assets-across-connected-assets-instances.md).

* Ottimizza i filtri di tipo Documento con più tipi MIME per supportare le opzioni multivalore.
* Introduzione di un flusso di lavoro Rielabora esterno per il supporto di più risorse.
* Prestazioni ottimizzate [!DNL Dynamic Media] utilizzando i filtri risorse predefiniti per la replica.
* Ripristino delle opzioni di modifica di Assets relative a ritaglio/rotazione per DMS7.
* Implementazione di un’opzione per la disattivazione audio di un video durante il caricamento in VideoPlayer.
* Implementazione di una correzione per fare in modo che nella vista a colonne dell’interfaccia utente di Assets sia visualizzato solo il contenuto specifico del tenant.
* Implementazione di una correzione per consentire che le modifiche del pannello a soffietto dello stile rispecchino i risultati della ricerca.

### Assets {#assets}

**Miglioramenti apportati al prodotto**

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Hotfix per CQ-4270245. Consulta la sezione sull’[utilizzo di risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets]Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

**Problemi risolti**

* I percorsi delle risorse negli URL e i metadati delle cartelle generati dall’API ACP non sono codificati in URL. GRANITE-26198: Hotfix per CQ-4271814
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989: Hotfix per CQ-4270467
* Interfaccia touch: Durante la procedura guidata di gestione della pubblicazione, i riferimenti vengono aggiunti dopo la pagina nel corpo della richiesta di pubblicazione, causando la pubblicazione di tutte le risorse dopo la pagina, e quando viene eseguito il rendering della pagina, alcune risorse nell’istanza di pubblicazione vengono perdute. NPR-29985: Hotfix per CQ-4270724
* La funzione Scollega di Assets non funziona per le risorse correlate il cui nome contiene caratteri speciali (caratteri che diventano con codifica URI). NPR-30387: Hotfix per CQ-4274446
* Quando si modifica un frammento di contenuto, la versione viene creata con l’utente errato.
* Errore durante la creazione di raccolte nel sistema basato su tenant. NPR-30114: Hotfix per CQ-4272948
* La vista a colonne dell’interfaccia utente di Assets non rispetta il percorso principale DAM del tenant corrente, ma accede a tutti i percorsi DAM del tenant. NPR-30636: Hotfix per CQ-4275481
* Possibilità di attacchi che sfruttano la vulnerabilità cross-site scripting (XSS) tramite la finestra di avviso File con limitazioni, in quanto l’immagine inserita può risultare visibile. NPR-30617: Hotfix per CQ-4270133
* MultiTenant: I tenant che salvano le proprietà della cartella osservano sia il messaggio di riuscita che il messaggio di errore che descrive l&#39;azione non è riuscito, &quot;Impossibile modificare le proprietà. Autorizzazioni insufficienti.” e questo genera confusione. NPR-30545: Hotfix per CQ-4275333
* La finestra di dialogo di Selettore risorse non consente la selezione della risorsa, pertanto non è possibile aggiornare l’origine utilizzando la funzionalità di sostituzione dell’origine correlata. NPR-30502: Hotfix per CQ-4275029
* [!UICONTROL Flusso di lavoro di aggiornamento risorse] DAM: stato precedente per il caricamento di file mp4 di grandi dimensioni. NPR-30480: Hotfix per CQ-4271352
* La funzionalità Crea attività di revisione non funziona a causa di un payload nullo che impedisce il completamento di tutte le azioni successive correlate all’attività di revisione. NPR-30468: Hotfix per CQ-4274263
* Problema di connettività di Tag avanzati di Adobe tramite DataPower. NPR-30026: Hotfix per CQ-4269457
* Nella vista a colonne dell’interfaccia utente di Assets viene generato un errore quando si prova ad aprire i filtri nella barra a sinistra. NPR-30501: Hotfix per CQ-4273862
* Quando si aggiungono gruppi sincronizzati da LDAP nelle proprietà di Gruppo utenti chiuso di una cartella risorse, il gruppo non viene salvato e recuperato. NPR-30615: Hotfix per CQ-4274689
* I campi di orientamento e stile per la ricerca con filtro non applicano il valore di completamento automatico alla query di ricerca. NPR-30620: Hotfix per CQ-4275724
* Con il collegamento di Condivisione risorse di una cartella il cui nome include spazi e il carattere “&amp;” vengono visualizzate schede grigie vuote per alcune risorse. NPR-30557: Hotfix per CQ-4270187
* Il modulo dello schema dei metadati della cartella non rileva automaticamente il tipo di dati e, di conseguenza, non crea l’elemento TypeHint correlato nell’invio del modulo. NPR-30599: Hotfix per CQ-4275227
* Le opzioni di modifica di Assets relative a ritaglio e rotazione vengono disabilitate dall’interfaccia utente di authoring di DMS7. NPR-30118: Hotfix per CQ-4273221
* Share Link feature is not working on [!DNL Experience Manager] instance with DMS7 configuration. NPR-30080, NPR-30492: Hotfix per CQ-4273651
* Adding the [!DNL Dynamic Media]–Scene7 component to the page, and then publishing the page does not trigger the dmscene7 configuration every time. NPR-30641: Hotfix per CQ-4275962
* Added an IPSJobJournal in [!DNL Experience Manager] to create only one Intrusion Prevention Systems (IPS) job per processing profile. NPR-30490: Hotfix per CQ-4273614
* [!DNL Dynamic Media]: Aggiunta di filtri predefiniti per escludere le risorse dalla replica nel nodo di Publish. [!DNL Experience Manager] NPR-30538: Hotfix per CQ-4274678
* Introduzione di un flusso di lavoro Rielabora esterno per supportare più risorse e consentire la creazione della cartella come payload. Il flusso di lavoro prevede due passaggi: rielaborazione delle risorse senza alcun handle tramite la mappatura dei metadati al passaggio successivo e ricaricamento di tutte le risorse senza handle di risorsa a S7 in un singolo processo IPS. For more details, see Configuring [!DNL Dynamic Media] Cloud Services. NPR-30489: Hotfix per CQ-4272903
* Caricamento di un CSV non corretto dopo la cancellazione del CSV corretto. Hotfix per CQ-4277694, CQ-4277814
* Icona errata specifica delle cartelle contributi da rimuovere. Hotfix per CQ-4277580
* Selezionando un utente nel selettore utenti della scheda Contributo risorse, il nome dell’utente non viene visualizzato nella tabella e nella pagina delle proprietà della finestra di dialogo Elimina utente viene visualizzato testo errato. Hotfix per CQ-4277875
* Non è possibile aggiungere collaboratori alla cartella Contributo risorse dal selettore utente selezionando l’utente e facendo clic su Aggiungi. Hotfix per CQ-4277824, CQ-4278087
* La ricerca per nome utente in minuscolo non funziona nel selettore utente. Hotfix per CQ-4277958, CQ-4277930
* Gli utenti non amministratori possono pubblicare risorse in una nuova cartella di una cartella Contributo risorse. Hotfix per CQ-4278200
* L’utente DAM (non amministratore) non può scegliere di aggiungere collaboratori alla cartella Contributo risorse. Hotfix per CQ-4278192
* Il pulsante “Crea” è visibile nella cartella Contributo risorse. Hotfix per CQ-4277560
* Sorting search query by relevance returns [!DNL InDesign] documents along with [!DNL InDesign] templates. Hotfix per CQ-4273864
* Se l’utente dispone di un ID e-mail in maiuscolo, non potrà eseguire la consegna per le risorse ritirate in precedenza. Hotfix per CQ-4276575
* L’operazione Elimina si applica solo ai predefiniti selezionati; se la schermata aggiorna automaticamente l’elenco dopo l’operazione, vengono visualizzati altri predefiniti già aggiornati. Hotfix per CQ-4261461
* Configuring [!DNL Dynamic Media] Cloud Services in [!DNL Dynamic Media]–Hybrid mode results in multiple empty report suites created in [!DNL Analytics], and with no report suite id stored in [!DNL Experience Manager], resulting in report suite duplication. Hotfix per CQ-4249780
* Rename operation in [!DNL Experience Manager] asset to duplicated name fails to synchronize to Scene7. Hotfix per CQ-4276763
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

### Sites {#sites-6520}

* Se l&#39;ereditarietà LiveCopy è interrotta, nelle pagine di LiveCopy sono visualizzati i collegamenti per la copia della lingua invece dei collegamenti LiveCopy (NPR-30980).
* Per una nuova Blueprint, Se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza righe vuote per gli altri record (NPR-31182).
* Il plug-in Editor Rich Text (RTE) del componente Testo visualizza i caratteri distorti per il testo in lingua giapponese e coreana (NPR-31331).
* Editor Rich Text (RTE) non consente di inserire una tabella incorporata come voce di elenco (NPR-30879).
* L&#39;Editor Rich Text per la scaffolding (RTE) viene applicato in linea alle dimensioni dei font agli elementi in modo imprevisto (NPR-31284).
* Quando un utente si concentra sui campi della barra a sinistra e utilizza una scelta rapida da tastiera per incollare il contenuto, incolla il contenuto degli Appunti dell&#39;Editor pagina invece del contenuto copiato dai campi della barra a sinistra (NPR-31172).
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso dell’immagine viene memorizzato nel nodo componente invece del nodo multi-campo (NPR-30882).
* L&#39; `ResponsiveGridExporter` API non restituisce `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` l&#39;interfaccia. Il `com.day.cq.wcm.foundation.model.impl` pacchetto è dichiarato come pacchetto privato (NPR-31398).
* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il `editor.html` prefisso e, `wcmmode=disabled`o in Publisher), la richiesta termina con il codice di errore dello stato HTTP 500 (NPR-30743).

### WCM - Editor pagina {#wcm-page-editor-6520}

**Miglioramenti apportati al prodotto**

* Ottimizza i filtri di tipo Documento con più tipi MIME per supportare opzioni con più valori. Hotfix per CQ-4270694

### Gestione dei frammenti di contenuto {#content-fragment-management-6520}

* La query utilizzata dall’interfaccia utente dei modelli di frammenti di contenuto è molto lenta e alla fine genera un errore. Hotfix per CQ-4270807

### Interfaccia utente - Foundation {#ui-foundation}

* Con l’attivazione dei tasti di scelta rapida l’utente non può usare i tasti m, p ed e all’interno di specifiche interfacce utente. NPR-30355: Hotfix per GRANITE-26346
* Closing [!DNL Experience Manager Assets] Search UI does not reset the left rail to Content selection preventing the user from opening the filter rail the second time subsequently. NPR-30509: Hotfix per CQ-4274716
* Multi-tenant environment: [!DNL Experience Manager Assets] UI top navigation is not available and throwing JavaScript error. NPR-30104: Hotfix per GRANITE-26344

### Traduzione {#translation-6520}

* Problema di traduzione - Solo alcuni componenti vengono tradotti utilizzando la traduzione automatica. NPR-30079: Hotfix per CQ-4273764

### Piattaforma {#platform-6520}

* [!DNL Experience Manager]Il mittente predefinito di non è in grado di inviare messaggi a un server SMTP remoto tramite TLS v1.2. NPR-30476: Hotfix per GRANITE-26605

### Progetti {#projects-6520}

* I valori dam:folderThumbnailPaths non vengono aggiornati e vengono visualizzate miniature vecchie anche dopo l’eliminazione delle risorse nella cartella. NPR-30424: Hotfix per CQ-4273667
* Quando si completa l’opzione “Sposta”, titolo e nome della risorsa restano invariati. NPR-30647: Hotfix per CQ-4276265

### Communities {#communities-6520}

* Diagnostica sincronizzazione utenti è danneggiato e non funziona. NPR-30004, NPR-29943: Hotfix per CQ-4270287, CQ-4271348

### Sling {#sling}

* In seguito all’aggiornamento dell’istanza dalla versione 6.3.3.2 alla versione 6.5 vengono create configurazioni OSGi duplicate. NPR-30130: Hotfix per CQ-4274016

### Integrazione {#integration}

* Il contenuto personalizzato non viene visualizzato correttamente nell’istanza di pubblicazione fino al riavvio dell’istanza. NPR-30377: Hotfix per CQ-4273706
* Durante la configurazione di Launch in un sito Web, l’indirizzo della libreria è preceduto da una barra (/) e questo causa ogni volta la necessità di un intervento manuale. NPR-30694: Hotfix per CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per [!DNL Experience Manager Forms]. They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) and [Install Experience Manager Forms JEE installer](#forms-jee-installer).

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Pacchetto di componenti aggiuntivi per Forms {#forms-add-on-package}

**Integrazione back-end**

* Impossibile configurare il modello dati del modulo utilizzando un URL con bilanciamento del carico ospitato da AWS. NPR-30123: Hotfix per CQ-4273359
* Durante la creazione del modello dati del modulo (FDM) con il linguaggio WSDL (Web Service Definition Language), `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` viene restituito il messaggio di errore: NPR-30477: Hotfix per CQ-4272921

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

#### Programma di installazione di JEE per Forms {#forms-jee-installer}

**Forms - Sicurezza dei documenti**

* L’applicazione di una firma con marca temporale non riesce e viene restituito l’errore: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: Errore di chiamata. NPR-30820: Hotfix per CQ-4275852

**Forms - Servizi basati su documenti**

* Se “SubmitURL” contiene una e commerciale (&amp;), nel registro sono presenti errori di analisi quando si effettua la richiesta POST al servlet renderpdf. NPR-30865: Hotfix per CQ-4278232

**Forms - JEE di base**

* Il servizio HTMLtoPDF non visualizza maxReuseCount nella console JMX. NPR-30134, NPR-30304: Hotfix per CQ-4273763
* Adding or editing a Web Service connection by invoking web services from [!DNL Experience Manager Forms] Workbench throws an error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Hotfix per CQ-4273217

### Feature Pack inclusi {#feature-packs-included}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Sites {#sites-feature-packs-included}

* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per [!DNL Adobe Target]. NPR-29189: Hotfix per CQ-4249782

#### Forms - Servizi basati su documenti {#forms-document-services-1}

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager Forms] OSGi. NPR-30759: Hotfix per CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 è una versione importante che include correzioni suggerite dai clienti e miglioramenti a prestazioni, stabilità sicurezza rilasciati a partire dalla data di disponibilità generale del [!DNL Adobe Experience Manager] 6.5 di *aprile 2019.* Può essere installato sulla parte superiore di [!DNL Experience Manager] 6.5.

Di seguito sono elencati alcuni elementi di rilievo di questo Service Pack:

* Abilitazione dell’inclusione dello stato dell’interfaccia utente dinamica negli eventi di tracciamento come attributi personalizzati.
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media]–Scene7 mode.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Assets

* Aggiornamento dell’interfaccia DMGGateway di DAM per il supporto multipart di S3. NPR-29740: Hotfix per CQ-4226303
* L&#39;anteprima delle rappresentazioni genera `Only empty tenantId is currently supported` un errore dopo l&#39;aggiornamento a [!DNL Experience Manager] 6.5. NPR-29986: Hotfix per CQ-4272353
* La finestra di dialogo Elimina non è visibile per consentire l’eliminazione di lavori. NPR-29720: Hotfix per CQ-4271074
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627: Hotfix per CQ-4264929
* VersioningTimelineEventProvider deve fornire la versione principale unitamente al nodo della versione nt: del tipo. Hotfix per GRANITE-26063
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. Hotfix per CQ-4265131
* Live Copy recupera lo stato non corretto in caso di modifica dell’origine. Hotfix per CQ-4265451
* Abilitazione del supporto per l’utilità di gestione di più siti per [!DNL Experience Manager Assets]. Hotfix per CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] nell’interfaccia deve essere visualizzata una voce aggiuntiva per la versione corrente della risorsa nella cronologia del tempo, in cui viene visualizzato il commento di archiviazione più recente da [!DNL Adobe Asset Link]. Hotfix per CQ-4262864
* Nella timeline dei frammenti di contenuto viene visualizzato un messaggio di errore in caso di assenza di proprietà. Hotfix per CQ-4272560
* Problema relativo al lettore video di Scene7 quando viene espanso a schermo intero. Hotfix per CQ-4266700
* ZoomVerticalViewer: i pulsanti di spostamento non devono essere visualizzati se viene utilizzata una singola risorsa immagine. Hotfix per CQ-4264795
* Se si elimina un nodo figlio nella Live Copy, è necessario scollegare liveRelationship. Hotfix per CQ-4270395
* Lo schema di metadati contiene solo elementi della configurazione globale; quelli del tenant attivo non sono presenti. Il valore dell’URL di formPath viene ripristinato a quello predefinito anche se modificato. NPR-29945: Hotfix per CQ-4262898
* Publish image presets to [!DNL Brand Portal] fails with 500 error code. NPR-29510: Hotfix per CQ-4268659

### Sites

* Le proprietà vuote e multiple non vengono propagate dalla blueprint durante il rollout. Il ripristino di Live Copy con la blueprint non funziona per i componenti. NPR-29253: Hotfix per CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537: Hotfix per CQ-4266129
* Enhancement of [!DNL Experience Manager] text component and Text Editor to Japanese. NPR-29785: Hotfix per CQ-4265090
* La pagina ripristinata con Timewarp deve fare riferimento all’immagine corretta al momento del controllo delle versioni. NPR-29431: Hotfix per CQ-4262638
* Un problema relativo all&#39;ereditarietà dei nodi Style System dall&#39;elemento padre all&#39;elemento secondario. NPR-29516: Hotfix per CQ-4270330
* An error message while setting up the social posting to [!DNL Facebook] authentication. NPR-29211: Hotfix per CQ-4266630
* La miniatura di cui è stato eseguito il rendering nel frammento di contenuto mostra la rappresentazione interna del calendario per il campo Data e ora. NPR-29531: Hotfix per CQ-4269362
* All’apertura della scheda Autorizzazioni nell’implementazione di Coral2 non viene visualizzato alcun pulsante. Hotfix per CQ-4269419

### Commerce

* ConstraintViolationException durante l’esecuzione della migrazione lenta dei contenuti per l’e-commerce. NPR-29247: Hotfix per CQ-4264383

### Gestione dei frammenti di contenuto

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Hotfix per CQ-4270266

### Frammenti esperienza

* Esporta frammenti [!DNL Experience Manager] esperienza in [!DNL Adobe Target]. Hotfix per CQ-4265469
* L’esportazione di frammenti esperienza come destinazione non riesce con l’immagine intelligente. Hotfix per CQ-4269606

* L’utente rimane bloccato quando prova a spostare i frammenti esperienza tramite Omnisearch nella vista a schede. Hotfix per CQ-4263848

### WCM - Editor pagina

* Vulnerabilità cross-site scripting (XSS) rilevabile quando si utilizza un selettore non valido. Hotfix per CQ-4270397

### Replica

* User-provided data is not escaped on output in the `cq/replication/components/agent` component, resulting in a stored Cross-site scripting (XSS) vulnerability. Hotfix per CQ-4266263

### Flusso di lavoro

* Il campo del selettore del calendario di Partecipante finestra di dialogo è danneggiato. NPR-29727: Hotfix per CQ-4270423

### WCM - Editor SPA

* Abilitazione del recupero da un endpoint remoto di contenuti di cui è già stato eseguito il rendering. Hotfix per CQ-4270238
* Aggiunta di avvisi nei registri quando viene aperta una pagina di modello per applicazione a pagina singola di cui viene eseguito il rendering sul lato server. Hotfix per CQ-4270238

### WCM - MSM

* Upgrade to [!DNL Experience Manager] 6.4.3 makes Multi-Site Manager take a long time to roll out. Hotfix per CQ-4271410

### Integrazione

* Credenziali BrightEdge non valide ed errore di connessione. NPR-29168: Hotfix per CQ-4265872

* An exception message is displayed when trying to edit and save the [!DNL Experience Manager] launch configuration. NPR-29176: Hotfix per CQ-4265782/CQ-4266153

### Interfaccia utente

* Aggiunta del supporto per il tracciamento degli stati dell’interfaccia utente dinamica come attributi personalizzati durante il tracciamento di determinati eventi nell’API di tracciamento di base. Hotfix per GRANITE-26283
* Impossibile impostare la funzione di tracciamento sul pulsante di invio. Hotfix per GRANITE-26326
* La procedura guidata non riesce a impostare la funzione di tracciamento sul pulsante di invio. NPR-29995, NPR-30025: Hotfix per CQ-4264289

### Communities

* Impossibile allineare i nuovi badge nel menu a discesa sulla pagina del profilo del membro. NPR-29381: Hotfix per CQ-4267987
* Visitatori e membri, senza privilegi di moderatore, possono visualizzare i post non approvati/in sospeso incollando l’URL. NPR-29724: Hotfix per CQ-4271124, CQ-4271441
* Durante l’accesso dell’utente alla community è possibile notare un tempo di risposta elevato, fino a 40-50 secondi. NPR-29677: Hotfix per CQ-4269444

### Replica

* Il componente Agente di replica è soggetto a una vulnerabilità per cui informazioni sensibili vengono rivelate a utenti non autorizzati. NPR-29611: Hotfix per GRANITE-25070

* Falla nella sessione durante OAuth per ogni replica su [!DNL Brand Portal]. NPR-30001: Hotfix per GRANITE-26196

### Progetti

* Publish [!DNL Experience Manager Assets] from [!DNL Experience Manager] Author /content/dam/mac folder to [!DNL Brand Portal] doesn&#39;t work. NPR-29819: Hotfix per CQ-4271118

### Piattaforma

* HtmlLibraryManager elimina tutti i contenuti di crx-quickstart in seguito all’annullamento della validità della cache. NPR-29863: Hotfix per GRANITE-26197

### Felix

* I dettagli sull’utilizzo della memoria non vengono visualizzati nella console del sistema quando si utilizza Java 11\. NPR-29669

### Forms

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* Solo OSGI: È stato abilitato il supporto per la creazione di file PDF statici tramite Forms Service.
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root.
* Abilitazione del supporto per ADFS v3.0 per l’integrazione On-Premise di Dynamics.

#### Pacchetto di componenti aggiuntivi per Forms

**Integrazione con il back-end**

* Errore durante il recupero del linguaggio WSDL (Web Service Definition Language) protetto. NPR-29944: Hotfix per CQ-4270777
* When [!DNL Experience Manager Forms] is installed on IBM WebSphere, creating a form data model based on SOAP fails. Hotfix per CQ-4251134
* Abilitazione del supporto per ADFS (Active Directory Federation Services) v3.0 per l’integrazione On-Premise di Microsoft Dynamics. Hotfix per CQ-4270586
* Quando si modifica il titolo di un’origine dati, il modello dati del modulo non visualizza il titolo aggiornato. Hotfix per CQ-4265599
* Se il nome di un&#39;entità o di un attributo contiene trattino o spazio, le espressioni non riescono a valutare tali entità e attributi. Hotfix per CQ-4225129

* L&#39;output non è corretto quando nell&#39;output della stringa primitiva sono presenti due punti. Hotfix per CQ-4260825

* Anche quando non è previsto alcun contenuto dall’output dell’API REST, l’operazione di richiamo del modello dati del modulo genera un errore. Hotfix per CQ-4268828

**Moduli adattivi**

* Impossibile aggiungere una nuova istanza nel frammento di modulo adattivo durante il caricamento lento. NPR-29818: Hotfix per CQ-4269875
* Il componente Verifica non registra o visualizza errori per i modelli della documentazione. Hotfix per CQ-4272999
* Aggiunta del supporto per disabilitare l’editor di layout per Moduli adattivi. Hotfix per CQ-4270810
* Restored the verify step for Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix for CQ-4269583

* Adaptive Form field validation failure breaks [!DNL Adobe Sign]. Hotfix per CQ-4269463
* When an [!DNL Experience Manager Forms] instance has more than 20 adaptive form fragments and name of all the form fragments starts with the same string, the search returns no or only recent 20 created fragments. Hotfix per CQ-4264414, CQ-4264914

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
* When an image of more than 2 MB is attached as a field level attachment to a form in the Android version of [!DNL Experience Manager Forms] app, the app crashes. Hotfix per CQ-4265578

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

* [!DNL Experience Manager Forms] 6.5 L&#39;interfaccia utente Crea corrispondenza (interfaccia utente CCR) non riesce ad aprire la corrispondenza creata con [!DNL Experience Manager Forms] 6.3. Hotfix per CQ-4266392
* La funzione di somma in XDP non funziona se i dati DDE sono di tipo numero. Hotfix per CQ-4227403
* La logica di annullamento validità della cache in memoria delle lettere deve essere aggiornata, perché quando viene pubblicata una risorsa, l’ora dell’ultima modifica non viene aggiornata. Hotfix per CQ-4250465
* Impossibile pubblicare il frammento di documento, DD e lettere. Hotfix per CQ-4272893

#### Programma di installazione di JEE per Forms

**PDF Generator**

* La conversione di file CAD in PDF non riesce con JDK a 64 bit. NPR-29924, NPR-29925: Hotfix per CQ-4272113
* Sostituzione del nome di PhantomJS in WebToPDF per la conversione HTMLtoPDF. NPR-29933: Hotfix per CQ-4234545
* Viene generato un errore durante la conversione del file ZIP in PDF. Hotfix per CQ-4268628

**Forms - Designer**

* When a full accessibility check is performed on the static PDF created using [!DNL Experience Manager Forms Designer], the Primary Language check fails due to missing language attribute. Hotfix per CQ-4272923, CQ-4271002

**Forms - Sicurezza dei documenti**

* La firma digitale con il modulo di sicurezza hardware non funziona in OSGi Linux su Java 11 e Java 8\. NPR-29838: Hotfix per CQ-4270441
* La firma digitale con il modulo di sicurezza hardware non funziona in JEE Linux e in tutti i server app supportati, ad esempio JBoss e Websphere. NPR-29839: Hotfix per CQ-4266721
* Durante la verifica delle firme in un PDF tramite l’uso di firme elettroniche avanzate PDF (PAdES) viene generata l’eccezione InvalidOperationException. NPR-29842: Hotfix per CQ-4244837
* Aggiunta del supporto per Document Security Extension per Office 2019\. Hotfix per CQ-4254369, CQ-4259764

**Forms - Servizi basati su documenti**

* La conversione del PDF in PDF/A-1b con il campo Modulo non ha il codice di aspetto. NPR-29940: Hotfix per CQ-4269618

* OSGi: Impossibile determinare il numero di pagine generate durante il rendering. NPR-28922: Hotfix per CQ-4270870
* È stato abilitato il supporto per i file PDF statici tramite Forms Service in [!DNL Experience Manager Forms OSGi]. NPR-28572: Hotfix per CQ-4270869
* Impossibile modificare le autorizzazioni per XMLForm.exe. NPR-29828, NPR-29237: Hotfix per Q-4267080
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332: Hotfix per CQ-4271002

**Forms - JEE di base**

* Il file pdfg_srt non è disponibile negli artefatti finali e questo impedisce l’esecuzione del programma di installazione. NPR-29854: Hotfix per CQ-4270137
* LCBackupMode.sh non funziona. NPR-29840: Hotfix per CQ-4269424
* È necessario rimuovere il riferimento alla porta UDP dall’interfaccia utente per WebSphere. Hotfix per CQ-4264782

### Feature Pack inclusi

#### Risorse - Incluse

* Abilitazione del supporto per l’utilità di gestione di più siti per [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199: Hotfix per CQ-4259922

#### Siti - Inclusi

* Esporta frammenti [!DNL Experience Manager] esperienza in [!DNL Adobe Target]. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Hotfix per CQ-4265469

#### Forms - Servizi basati su documenti - Incluso

* Solo OSGi: È stato aggiunto un nuovo attributo PAGECOUNT in Output e Forms Service. NPR-28922: Hotfix per CQ-4270870
* Solo OSGi: È stato abilitato il supporto per la creazione di file PDF statici tramite Forms Service. NPR-28572: Hotfix per CQ-4270869
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root. NPR-29237: Hotfix per CQ-4267080

### Bundle OSGi e pacchetti di contenuti

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[Ottieni file](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[Ottieni file](assets/6_5-content-package-list.txt)
