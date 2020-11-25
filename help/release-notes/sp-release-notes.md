---
title: '[!DNL Adobe Experience Manager] 6.5 Note sulla versione di Service Pack'
description: Release notes specific to [!DNL Adobe Experience Manager] 6.5 Service Pack 7.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: e056d25cf16d79e8eadc80b9cb17b60b2ba8d7e1
workflow-type: tm+mt
source-wordcount: '3796'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] 6.5 Note sulla versione di Service Pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.7.0 |
| Tipo | Versione Service Pack |
| Data | 26 novembre 2020 |
| URL di download | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## What&#39;s included in [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.7.0 è un aggiornamento importante che include nuove funzioni, miglioramenti fondamentali richiesti dai clienti, e miglioramenti in termini di prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 di aprile 2019. Il service pack è installato in [!DNL Adobe Experience Manager] 6.5.

Le funzioni chiave e i miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.7.0 includono:

* Ordinare le pagine Live Copy disponibili per il rollout utilizzando le proprietà [!UICONTROL Nome], Data [!UICONTROL ultima modifica,] Data [!UICONTROL ultimo rollout] .

* L&#39;esecuzione degli spostamenti di pagina e dei rollout MSM come operazioni asincrone per ridurre il loro impatto sulle prestazioni del runtime.

* Gli utenti possono ordinare le risorse digitali nelle viste a schede e a colonne.

* [!DNL Assets] e [!DNL Dynamic Media] fornire diversi miglioramenti a livello di accessibilità. I miglioramenti riguardano la navigazione tramite tastiera, l&#39;uso di assistenti vocali e la possibilità per gli utenti di utilizzare una tecnologia di supporto (AT) simile. Consultate [[!DNL Assets] Miglioramenti](#assets-6570) e [[!DNL Dynamic Media] miglioramenti](#dynamic-media-6570).

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.5.

Per un elenco completo delle funzioni e dei miglioramenti introdotti in [!DNL Experience Manager] 6.5.7.0, consulta [Novità in [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

Di seguito è riportato l&#39;elenco delle correzioni fornite nella release [!DNL Experience Manager] 6.5.7.0.

### [!DNL Sites] {#sites-6570}

* Quando aprite l’opzione [!UICONTROL Timewrap] per una pagina, mantenete aperta l’opzione della barra laterale Timeline e passate alla console [!UICONTROL Siti] , l’ `Failed to Load` errore si verifica (NPR-34951).

* L&#39;opzione [!UICONTROL Timewrap] non visualizza le immagini per l&#39;intervallo di data e ora selezionato (NPR-34951).

* Quando un filtro effettua una chiamata `getHeader()` da una pagina contenente un frammento di contenuto, si verifica l&#39; `java.lang.AbstractMethodError` errore (NPR-34942).

* Quando il percorso di una pagina contiene più sottostringhe di contenuto, il rendering delle anteprime non riesce e anche la funzione di confronto delle versioni non riesce (NPR-34740).

* Quando si imposta un valore numerico per la proprietà dell&#39;etichetta di `String` tipo di un componente, è possibile eliminare il componente e annullare l&#39;operazione di eliminazione. Tuttavia, dopo l&#39;annullamento dell&#39;eliminazione, la proprietà label cambia da `String` a `Long` (NPR-34739).

* La seguente eccezione si verifica quando si aggiunge un frammento esperienza basato su un modello con layout bloccato a una pagina (NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* Quando spostate una cartella, si verificano dei problemi di navigazione e si verifica il seguente errore (NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* Quando nuove risorse vengono create, pubblicate e spostate in un nuovo percorso, il `Request to complete move operation` flusso di lavoro viene creato e si verifica uno stato Interrotto. Il caricamento di una nuova risorsa e l&#39;esecuzione di un&#39; `move` operazione determina la creazione del `Request to complete move operation` flusso di lavoro in sospeso (NPR-34543).

* Quando esportate un frammento esperienza dall&#39;ambiente [!DNL Experience Manager] 6.5.2 a [!DNL Target] Standard, la chiamata API ha esito negativo perché la proprietà workspace non è disponibile per [!DNL Target] Standard (NPR-34557).

* Gli utenti non possono pubblicare le pagine tramite l&#39;opzione [!UICONTROL Gestisci pubblicazione] perché l&#39;opzione [!UICONTROL Pubblica] scompare (NPR-34542).

* Quando aggiungete degli stili al testo, al testo viene aggiunto un `<div>` tag e lo stile non può più essere applicato al testo (NPR-34531).

* Quando selezionate una voce in un menu a comparsa e aggiornate i file richiesti, non è possibile salvare i valori delle finestre di dialogo poiché l&#39;altro menu contiene un campo obbligatorio vuoto (NPR-34529).

* Quando create una pagina da un modello personalizzato e la spostate all’interno della gerarchia di blueprint, i componenti eliminati in precedenza dalla pagina iniziano a essere visualizzati sulla pagina all’interno della gerarchia delle Live Copy (NPR-34527).

* Non è possibile rimuovere uno stile articolo applicato a un contenuto (NPR-34486).

* Tutte le copie in diretta e le copie di un frammento esperienza puntano allo stesso ID [!DNL Adobe Target] offerta (NPR-34469).

* Gli elementi dell&#39;elenco puntato vengono visualizzati in aggiunta all&#39;elenco numerato (NPR-34455).

* L&#39;opzione di confronto con l&#39;origine non mostra la differenza tra la pagina di origine e la versione modificata di una pagina (NPR-34285).

* Quando eliminate una pagina, i dettagli relativi alle versioni non sono configurabili (NPR-34159).

* Quando un utente seleziona l&#39;opzione [!UICONTROL Apri selezione] , lo stato attivo si sposta sul controllo nascosto presente sulla pagina (CQ-4307779, CQ-4293601).

* Quando spostate una cartella pubblicata in Author, i percorsi delle cartelle non vengono aggiornati di conseguenza sull’istanza Pubblica (CQ-4305144).

* Quando un utente seleziona il `Enter` tasto dell&#39;opzione [!UICONTROL Seleziona tutto] , lo stato attivo non si sposta sull&#39;opzione [!UICONTROL Crea controllo] (CQ-4293599).

* Selezionando la `Esc` chiave, lo stato attivo non viene ripristinato al controllo principale (CQ-4293593, CQ-4293590).

* Miglioramento della conformità WCAG per l&#39; [!DNL Sites] interfaccia utente e i componenti core (CQ-4293448).

* [!UICONTROL Le funzioni Zoom] e [!UICONTROL Scala] sono disattivate per la [!DNL Sites Editor] pagina (CQ-4282353).

* Dopo aver usato l’opzione Ruota a destra, l’assistente vocale interrompe la narrazione dello stato di rotazione o di capovolgimento corrente (CQ-4282128).

* I pulsanti di dialogo Fine e Annulla configurazione hanno più arresti tabulazione (CQ-4274601).

* Lo spostamento di pagine con un nome simile sullo stesso livello non è consentito (NPR-35041).

* Dopo aver selezionato l&#39;opzione Cancella (x), lo stato attivo non si sposta sul campo [!UICONTROL Filtro] (CQ-4293581).

* Con l&#39;aggiornamento alla versione [!DNL Experience Manager] 6.5.6.0, il comportamento del sistema paragrafo ereditato cambia e non funziona correttamente (NPR-35117).

* Gli utenti di tastiera non possono spostare lo stato attivo in un ordine appropriato dopo aver selezionato la sezione [!UICONTROL Azione] in una [!DNL AEM Sites] pagina (CQ-4307786).

* Dopo aver selezionato un&#39;opzione nell&#39;elenco del menu di destinazione del collegamento della barra degli strumenti dell&#39;editor Rich Text quando si modifica un frammento di contenuto, la finestra di dialogo di creazione del frammento di contenuto inizia a sfarfallare (CQ-4305532).

* Gli utenti di tastiera non possono selezionare le opzioni nell&#39;elenco a discesa [!UICONTROL Aggiungi componente] utilizzando il tasto freccia giù (CQ-4295097).

* Lo stato attivo non si sposta in un ordine appropriato quando si seleziona una data dal menu Calendario nella scheda [!UICONTROL Risorse] di una [!DNL Sites] pagina (CQ-4293600).

* Lo stato attivo non si sposta sulle opzioni successive o precedenti per gli utenti della tastiera dopo l&#39;eliminazione delle opzioni Collegamento o Testo disponibili durante la modifica di una pagina Siti (CQ-4293597).

* Gli utenti della tastiera non possono spostare lo stato attivo su Altre opzioni nella sezione [!UICONTROL Azioni] dopo aver visualizzato le opzioni disponibili e aver premuto il `Esc` tasto (CQ-4293592).

* Quando si attiva l&#39;opzione [!UICONTROL Ruota] per un&#39;immagine in modalità [!UICONTROL Modifica] , l&#39;elemento attivo nella scheda, invece di rimanere su Ruota, si sposta sull&#39;opzione [!UICONTROL Ripristina] per gli utenti della tastiera (CQ-4293587).

* Nella finestra di dialogo [!UICONTROL Apri selezione] disponibile nella scheda [!UICONTROL Collegamento e azioni] , dopo l’opzione [!UICONTROL Annulla] (CQ-4293579) viene attivato lo stato attivo della scheda.

* Quando un utente utilizza la tastiera per modificare un&#39;immagine, passare all&#39;opzione [!UICONTROL Fine] e premere il tasto Invio, gli assistenti vocali non annunciano il completamento (CQ-4282351).

* Le opzioni Sposta in alto e Sposta in basso disponibili nella finestra di dialogo [!UICONTROL Collegamento e Azioni] non sono disponibili per l&#39;assistente vocale e gli utenti di tastiera (CQ-4281120).

* Gli utenti della tastiera non possono ripristinare lo stato attivo dopo aver selezionato Chiudi (X) nella pagina [!UICONTROL Proprietà] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 [!DNL Assets] risolve i seguenti problemi e fornisce i seguenti miglioramenti.

* I seguenti miglioramenti sono stati apportati per l&#39;accessibilità in questa [!DNL Experience Manager Assets] versione. Per ulteriori informazioni, vedere Funzioni di [accessibilità in [!DNL Assets]](/help/assets/accessibility.md).

   * Quando si naviga nella timeline utilizzando una tastiera, il `Esc` tasto può comprimere l&#39;opzione [!UICONTROL Mostra tutto] senza perdere lo stato attivo (CQ-4293598).
   * Quando si naviga utilizzando il tasto di tabulazione della tastiera, dopo aver rimosso l&#39;ultimo tag dai tag aggiunti, il campo del tag rimane attivo (NPR-35109).
   * [!DNL Experience Manager] i componenti ora contengono informazioni appropriate per nome, ruolo e valore che devono essere utilizzati dagli assistenti vocali (NPR-34255).
   * Dopo aver eliminato la casella combinata Tipo/Dimensione, Collegamento, Lingua o Testo, lo stato attivo torna agli elementi dell&#39;interfaccia utente successivi o precedenti o a un elemento dell&#39;interfaccia utente più rilevante (CQ-4293585).
   * Quando si passa il puntatore del mouse su diverse opzioni, vengono visualizzati i suggerimenti come Seleziona e Scarica. Gli utenti che utilizzano l&#39;ingrandimento dello schermo potrebbero avere difficoltà a visualizzare le miniature dei file a causa del contenuto visualizzato a causa del passaggio del mouse. Ora è possibile mantenere lo stato attivo, dopo aver rimosso l&#39;opzione utilizzando un `Escape` tasto (CQ-4293554).
   * Selezionando una cella della griglia presente nella pagina, lo stato attivo si sposta sulla barra delle azioni visualizzata sullo schermo (CQ-4282127).
   * Gli utenti visivi possono distinguere tra testo normale e collegamento, in quanto vengono visualizzati indizi visivi (sottolineatura e icona a forma di freccia) per i collegamenti a tutte le soluzioni nella pagina [!DNL Experience Manager] principale (CQ-4282072).

* Il seguente miglioramento dell’esperienza utente viene effettuato in [!DNL Assets]:

   * Abilitare l&#39;ordinamento delle risorse nelle viste a schede e a colonne (NPR-35097).

* Dopo l&#39;aggiornamento alla versione 6.5, se un file JSON viene generato utilizzando l&#39;API HTTP Assets, si verificano problemi con la codifica utilizzata nel file (NPR-35129).

* Gli utenti di un gruppo a cui non è stata concessa l&#39;autorizzazione per creare raccolte (l&#39;opzione Crea raccolta non è disponibile) possono comunque creare raccolte accedendo direttamente all&#39;URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* Se ordinate per nome, le risorse ricercate vengono ordinate in base alle maiuscole/minuscole. In questo modo vengono creati due elenchi ordinati separati in base al casing che vengono visualizzati in modo ordinato nei risultati della ricerca (NPR-35068).

* Quando un frammento di contenuto viene aperto nell&#39;editor, i messaggi di avviso (`Invalid value specified for a metadata property`) vengono registrati nei registri degli errori (NPR-35012).

* Gli utenti senza privilegi di amministratore possono modificare le risorse scadute utilizzando [&#39;app desktop Experience Manager] . (NPR-34993).

* Quando la stessa risorsa viene trascinata sull’interfaccia utente di Assets e viene creata una nuova versione, le modifiche nei metadati non sono persistenti (NPR-34940).

* Quando modificate le raccolte, un utente può eliminare il titolo della raccolta e salvare le modifiche (NPR-34889).

* Quando si carica un&#39;immagine duplicata, viene visualizzata un&#39;opzione di eliminazione. Se si seleziona Elimina, le immagini verranno caricate. Viene attivato anche il flusso di lavoro Aggiorna risorsa DAM (NPR-34744).

* Quando si utilizza [!DNL Adobe Asset Link] con [!DNL Adobe InDesign], i risultati della ricerca non contengono cartelle e raccolte ma solo risorse (NPR-34699, CQ-4303666).

* Passando il puntatore del mouse sulla vista a schede, lo schermo scorre come risultato (automatico) dell&#39;attivazione delle azioni rapide disponibili nella scheda (NPR-34514).

* Quando modificate le proprietà di più risorse in blocco, selezionando l’opzione [!UICONTROL Salva] la vista dell’editor in blocco viene chiusa e reindirizzata alla [!DNL Assets] pagina principale. Questo comportamento è identico a quello dell&#39;opzione [!UICONTROL Salva e chiudi] e non è previsto (NPR-34546).

* La raccolta smart non presenta l&#39;impostazione corretta dell&#39;interfaccia utente dopo il salvataggio. La query viene salvata correttamente ma l&#39;interfaccia visualizza sempre l&#39;ultimo predicato Option aggiunto (NPR-34539).

* Quando si aggiungono risorse a [!DNL Experience Manager], i metadati senza spazio nomi non vengono importati (NPR-34530).

* Quando trascinate una risorsa su una cartella per spostarla, l&#39;interfaccia utente mostra anche l&#39;opzione [!UICONTROL Rilascia in Lightbox] e [!UICONTROL Rilascia nella raccolta]. Anche se l&#39;operazione di spostamento viene annullata, l&#39;interfaccia utente continua a visualizzare le ultime due opzioni (NPR-34526).

* Il simbolo `%>` viene visualizzato nella pagina delle raccolte (NPR-34499).

* Nella vista a colonne, [!DNL Assets] visualizza nomi di cartelle e risorse duplicati quando si scorre verso l’alto o il basso prima che vengano visualizzate tutte le risorse (NPR-34464).

* Se create una cartella privata subito dopo la creazione di una cartella pubblica, questa utilizza le impostazioni della cartella privata (NPR-34415).

* Nella vista a schede, le schede non sono elencate in ordine alfabetico e non possono essere ordinate in ordine alfabetico (NPR-34234).

* Quando si riaprono le regole di CSS, le scelte non vengono mantenute nell&#39;interfaccia utente (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* I seguenti miglioramenti sono stati apportati per l&#39;accessibilità in [!DNL Dynamic Media] (CQ-4290306). Per informazioni dettagliate, consultate Funzioni di [accessibilità in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * Gli assistenti vocali (JAWS, Assistente vocale) indicano il nome, il ruolo e lo stato delle voci di menu nell&#39;opzione di menu Incorpora dimensioni (CQ-4290927).
   * Gli utenti possono passare alla finestra di dialogo del collegamento E-mail utilizzando la `Tab` chiave (CQ-4290926).
   * Il flusso di lavoro per la creazione di profili di codifica video è più semplice da usare, grazie al miglioramento dell&#39;assistente vocale (CQ-4290623, CQ-4290622).
   * Quando si naviga utilizzando `Tab` la chiave, lo stato attivo si sposta sugli elementi dell&#39;interfaccia utente appropriati nel flusso di lavoro per creare un video interattivo (CQ-4290621, CQ-4290620, CQ-4290619).
   * Sono state migliorate le pagine Pubblica, Modifica risorsa, Modifica Smart Crops e Editor set di immagini per soddisfare gli standard Web. Gli utenti della tecnologia di assistenza (AT) ora possono navigare facilmente in queste pagine e intraprendere azioni quali il ritaglio delle immagini (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-4290 610, CQ-4290614).
   * I visualizzatori sono stati migliorati per consentire agli utenti di spostarsi utilizzando una tastiera (CQ-4290615).
   * Gli utenti di tastiera e utilità di lettura dello schermo possono utilizzare la funzionalità di ritaglio (CQ-4290609).
   * Gli utenti della tastiera possono gestire meglio i punti di attivazione (CQ-4290604, CQ-4290603).

* I set di immagini remoti non possono essere modificati in [!DNL Experience Manager] se il nome della società e del nome della cartella sono identici (NPR-31340).

* L&#39;ordine z-index non è corretto quando si tenta di visualizzare l&#39;anteprima dell&#39;output dopo l&#39;aggiunta di un punto critico a un&#39; [!DNL Dynamic Media] immagine o dopo la modifica di un [!DNL Dynamic Media] video o di un [!DNL Experience Fragment] video con un&#39;immagine (CQ-4307267).

* [!DNL Dynamic Media] la sincronizzazione non riesce quando i set di file multimediali diversi vengono rielaborati (CQ-4307184).

* Se una risorsa viene spostata in una cartella in cui [!DNL Dynamic Media] è configurata la sincronizzazione automatica, la risorsa non viene sincronizzata (CQ-4307122).

* [!DNL Dynamic Media] il video non viene riprodotto sui dispositivi iOS con i controlli video HTML5 nativi (CQ-4306977, CQ-4306727).

* Impossibile scaricare le immagini a cui è applicato SmartCrop (CQ-4304558).

* Impossibile pubblicare in modo selettivo le cartelle su file multimediali dinamici (CQ-4304526).

* L’annullamento della pubblicazione di un file video da [!DNL Experience Manager] non annulla la pubblicazione del set video adattivo da una distribuzione Scene7 configurata (CQ-4304405).

* Se si aggiunge una risorsa immagine panoramica in un componente per contenuti multimediali panoramici e si aggiorna la pagina, si `Uncaught ReferenceError: $ is not defined` verifica un errore (CQ-4302810).

* Nell’Editor [!UICONTROL predefiniti per]visualizzatori, quando si modifica il predefinito [!UICONTROL PanoramicImage/PanoramicImage_VR] , nel `PanoramicView` componente l’etichetta del `PANORAMICVIEW_AUTOROTATE` modificatore non è disponibile (CQ-4302443).

* I sottotitoli video non vengono visualizzati se il video non è il primo in un set di file multimediali diversi (CQ-4298161).

* Il visualizzatore HTML5 per eCatalog su dispositivi mobili iPhone non può voltare le pagine o capovolgere le pagine (CQ-4296611).

* Quando si scorrono i campioni su un dispositivo mobile, per alcuni secondi i campioni scorrono a destra e all’esterno dell’area visibile prima di tornare alla visualizzazione (CQ-4296439).

* Quando create un record master predefinito per visualizzatori, i CSS e le immagini non vengono pubblicati e viene pubblicato solo il predefinito per visualizzatori (CQ-4262205).

* Quando si tenta di collegare un frammento esperienza per un dato punto di attivazione nel componente Video/Immagini  interattive, non viene visualizzato il percorso del frammento esperienza selezionato. ma restituisce un valore vuoto dal campo percorso (NPR-35146, CQ-4298136).

* Impossibile visualizzare in anteprima un frammento esperienza in IVV Editor (CQ-4308560).

* Quando si aggiunge un punto di attivazione a un&#39;immagine e si seleziona un frammento esperienza, non è possibile selezionare le sottocartelle e le varianti del frammento esperienza (CQ-4307455).

* Le risorse non immagine non vengono visualizzate come pubblicate dopo il caricamento (CQ-4306415).

#### [!DNL Experience Manager] Risorse 3D {#three-d-assets-6570}

* `DAM CQ MIME Type` il servizio applica tipi MIME non corretti alle risorse 3D che determinano un rendering non corretto (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* L&#39;interfaccia utente della raccolta prodotti Commerce non elenca più di 15 prodotti all&#39;interno di una raccolta (NPR-34502).

### Platform {#platform-6570}

* Una sessione HTTP su HTTPS non viene invalidata (NPR-35083).
* Quando si avviano attività di manutenzione giornaliere o settimanali dall&#39;interfaccia utente `NullPointerException` viene restituito un errore (NPR-34953).
* La funzione di convalida W3C segnala gli avvisi relativi ai file JavaScript della libreria client conformi (NPR-34898).
* La `AudienceOmniSearchHandler` funzione utilizza un indice obsoleto (NPR-34870).
* La disconnessione dal  Experience Manager non cancella i cookie (NPR-34743).
* La `findByTitle` funzione dell&#39; `TagManager` API non funziona se il nome del tag contiene un carattere speciale (NPR-34357).
* Il processo di importazione del pacchetto di sincronizzazione utenti non riesce (NPR-34399).
* È stato aggiunto il supporto per `ariaLabel` e `ariaLabelledby` le proprietà per il `Coral.Masonry` componente (GRANITE-29962).
* La cache del dispatcher non viene aggiornata per le pagine con frammenti di contenuto dopo l&#39;installazione dei pacchetti componenti core più recenti (CQ-4306788).
* I nomi dei tag localizzati con virgolette (`"`) non vengono visualizzati correttamente nell&#39;interfaccia utente (CQ-4305439).

### Interfaccia utente {#ui-6570}

* Il campo [!UICONTROL Collega] alle proprietà del componente presenta suggerimenti di completamento automatico non corrispondenti alla stringa specificata (NPR-34865).

* AEM il seguente messaggio di errore quando pianificate una finestra di manutenzione giornaliera distribuita tra 2 giorni (NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integrations (Integrazioni){#integrations-6570}

* La modifica di una [!DNL Adobe Launch] configurazione esistente non riesce (NPR-35045).
* Impossibile esportare [!DNL Experience Fragments] in [!DNL Adobe Target] [!DNL Adobe Target Standard] se si utilizza la configurazione e l&#39;ambiente IMS (NPR-34555).
* L&#39;opzione [!UICONTROL Crea] viene visualizzata nella pagina [!UICONTROL Audiences] quando si passa da una cartella alla pagina [!UICONTROL Audiences] (NPR-35151).

### Sling {#sling-6570}

* Il controllo dello stato di accesso predefinito convalida le credenziali di un utente che non esiste (NPR-34686).

### Progetti traduzione {#translation-6570}

* Quando si annulla un progetto di traduzione in [!DNL Experience Manager], la richiesta di annullamento non viene inviata al provider di traduzione (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Tutti i casi di terminologia iniqua nel prodotto vengono sostituiti con equivalenti accettati (NPR-34311).
* [!DNL Google+] viene rimosso dall&#39;elenco delle opzioni di condivisione mediante social network (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* L&#39;interfaccia utente non risponde quando si selezionano le risorse nella vista  elenco (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] rilascia i pacchetti del componente aggiuntivo una settimana dopo la data di rilascio pianificata per [!DNL Experience Manager] Service Pack.

Per informazioni sugli aggiornamenti della sicurezza, consultate [pagina](https://helpx.adobe.com/security/products/experience-manager.html)dei bollettini sulla sicurezza degli Experienci Manager.

## Install 6.5.7.0 {#install}

**Requisiti di configurazione e ulteriori informazioni**

* AEM 6.5.7.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Il download del service pack è disponibile  Adobe Distribuzione [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)software.
* In una distribuzione con MongoDB e più istanze, installa AEM 6.5.7.0 in una delle istanze Autore tramite Gestione pacchetti.

>[!NOTE]
>
>Adobe does not recommend removing or uninstalling the [!DNL Adobe Experience Manager] 6.5.7.0 package.

### Installare Service Pack {#install-service-pack}

Per installare Service Pack in un’istanza Adobe Experience Manager 6.5 esistente, effettuate le seguenti operazioni:

1. Riavviate l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (e questo accade quando l’istanza è stata aggiornata da una versione precedente).  Adobe consiglia inoltre di riavviare il sistema se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di eseguire l&#39;installazione, scegli un&#39;istantanea o un nuovo backup dell&#39;istanza del Experience Manager [] .

1. Scaricate il service pack da [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip).

1. Aprite Gestione pacchetti e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta Gestione [](/help/sites-administering/package-manager.md)pacchetti.

1. Select the package and click **[!UICONTROL Install]**.

1. Per aggiornare il connettore S3, arrestare l&#39;istanza dopo l&#39;installazione del Service Pack, sostituire il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavviare l&#39;istanza. Vedere [archivio](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)dati Amazon S3.

>[!NOTE]
>
>La finestra di dialogo nell&#39;interfaccia utente di Package Manager talvolta si chiude durante l&#39;installazione del service pack.  Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendete i registri specifici relativi alla disinstallazione del pacchetto di aggiornamento prima di essere certi che le installazioni abbiano esito positivo. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Installazione automatica**

Esistono due modi per installare automaticamente Adobe Experience Manager 6.5.7.0 su un’istanza di lavoro:

A. Inserite il pacchetto nella `../crx-quickstart/install` cartella quando il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Utilizzate l&#39;API [HTTP da Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Utilizzate questa `cmd=install&recursive=true` opzione per installare i pacchetti nidificati.

>[!NOTE]
>
>Adobe Experience Manager 6.5.7.0 non supporta l&#39;installazione di Bootstrap.

**Convalidare l’installazione**

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa della versione aggiornata `Adobe Experience Manager (6.5.7.0)` in Prodotti installati.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è della versione 1.22.3 o successiva (Usa console Web: `/system/console/bundles`).

Per conoscere le piattaforme certificate per l’utilizzo con questa versione, consulta i requisiti [tecnici](/help/sites-deploying/technical-requirements.md).

### Installare  pacchetto del componente aggiuntivo Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] rilascia i pacchetti del componente aggiuntivo una settimana dopo la data di rilascio pianificata per [!DNL Experience Manager] Service Pack.

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms. Le correzioni  Adobe Experience Manager Forms vengono distribuite tramite un pacchetto aggiuntivo separato.

1. Accertatevi di aver installato Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installare  Adobe Experience Manager Forms su JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Le correzioni  Adobe Experience Manager Forms su JEE vengono distribuite tramite un programma di installazione separato.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

### UberJar {#uber-jar}

UberJar per  Experience Manager 6.5.7.0 è disponibile nell’archivio [](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)Maven Central.

Per utilizzare UberJar in un progetto Maven, consulta [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includere nel POM del progetto la seguente dipendenza:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artifact correlati sono disponibili nel repository centrale di Maven invece di  repository di Public Maven Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Pertanto, non esiste `classifier`, con `apis` il valore, per il `dependency` tag.

## Funzioni obsolete {#removed-deprecated-features}

Di seguito è riportato un elenco di funzioni e funzionalità contrassegnate come obsolete con [!DNL Experience Manager] 6.5.7.0. Le funzioni sono contrassegnate come obsolete inizialmente e successivamente rimosse in una versione futura. In genere viene fornita un&#39;opzione alternativa.

Verifica se utilizzi una funzione o una funzionalità in una distribuzione. Pianificate inoltre di modificare l&#39;implementazione in modo da utilizzare un&#39;opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrations (Integrazioni) | La schermata di consenso dei servizi **[!UICONTROL AEM Cloud non è più disponibile]** . Con l&#39;integrazione AEM e Target aggiornata in AEM 6.5 per supportare l&#39;API di Target Standard, che utilizza l&#39;autenticazione tramite  IMS Adobe e I/O, e il ruolo crescente di  lancio del Adobe per strumentalizzare AEM pagine per l&#39;analisi e la personalizzazione, la procedura guidata di consenso è diventata funzionale e irrilevante. | Configurate le connessioni di sistema, l&#39;autenticazione  Adobe IMS e le integrazioni di I/O  Adobe tramite i rispettivi servizi cloud AEM. |
| Connettori | Il connettore JCR  Adobe per Microsoft SharePoint 2010 e Microsoft SharePoint 2013 non è più supportato per AEM 6.5. | N/D |

## Problemi noti {#known-issues}

* Ignorare gli errori seguenti nel `error.log` file durante l&#39;installazione dell&#39;Experience Manager 6.5.7.0 :

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* Se state effettuando l&#39;aggiornamento dell&#39; [!DNL Experience Manager] istanza dalla versione 6.5 alla versione 6.5.7.0, potete visualizzare `RRD4JReporter` le eccezioni nel `error.log` file. Riavviate l&#39;istanza per risolvere il problema.

* Se installate [!DNL Experience Manager] 6.5 Service Pack 5 o un service pack precedente al [!DNL Experience Manager] 6.5, la copia in fase di esecuzione del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata.
Per recuperare la copia runtime,  Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la copia in fase di esecuzione utilizzando l&#39;API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Contatta  Assistenza clienti di Adobe in caso di problemi durante la modifica e la creazione di regole a cascata nell&#39;Editor [!UICONTROL Forms Schema metadati] cartella e nell&#39;Editor [!UICONTROL Forms Schema] metadati utilizzando la finestra di dialogo [!UICONTROL Definisci regola] . Le regole già create e salvate funzionano come previsto.

* Se una cartella nella gerarchia viene rinominata in [!DNL Experience Manager Assets] e la cartella nidificata che contiene una risorsa viene pubblicata in, il titolo della cartella non viene aggiornato in [!DNL Brand Portal][!DNL Brand Portal] finché la cartella principale non viene nuovamente pubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l&#39;opzione per salvare una configurazione non viene visualizzata nel browser Proprietà. Se si seleziona questa opzione per configurare un altro campo del modulo adattivo nello stesso editor, il problema viene risolto.

* Se la configurazione [!UICONTROL delle risorse] connesse restituisce un messaggio di errore 404 dopo l’installazione, reinstallate manualmente i pacchetti `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` i pacchetti utilizzando Gestione pacchetti.

* Durante l&#39;installazione di AEM 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * Quando l’integrazione di Target è configurata in AEM tramite l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce se vengono utilizzate funzioni di aggregazione quali SUM, MAX e MIN. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * L’area sensibile in un’immagine multimediale dinamica interattiva non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore per banner acquistabili.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Nei documenti di testo seguenti sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in AEM 6.5.7.0:

* [Elenco dei bundle OSGi inclusi in AEM 6.5.7.0](assets/6570_bundles.txt)

* [Elenco dei pacchetti di contenuti inclusi in AEM 6.5.7.0](assets/6570_packages.txt)

## Siti Web limitati {#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* Scopri [come contattare l’assistenza](https://experienceleague.adobe.com/docs/customer-one/using/home.html)clienti.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Note di rilascio 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] pagina prodotto](https://www.adobe.com/it/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

