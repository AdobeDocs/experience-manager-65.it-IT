---
title: '[!DNL Adobe Experience Manager] 6.5 note sulla versione precedente del service pack'
description: Note sulla versione per  [!DNL Adobe Experience Manager] 6.5 service pack
contentOwner: AK
mini-toc-levels: 2
exl-id: aeed49a0-c7c2-44da-b0b8-ba9f6b6f7101
source-git-commit: 97d0b0d85276c733b487a8f3c5095bc4feb7e08d
workflow-type: tm+mt
source-wordcount: '23168'
ht-degree: 13%

---

# Hotfix e Feature Pack inclusi nei service pack precedenti {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.9.0 {#experience-manager-6590}

[!DNL Adobe Experience Manager] La versione 6.5.9.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 di aprile 2019. Il service pack è installato su [!DNL Adobe Experience Manager] 6.5.

Le funzioni chiave e i miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.9.0 sono i seguenti:

* [!DNL Experience Manager Sites] Il componente Dynamic Media Foundation ora consente di attivare o disattivare l’ottimizzazione per dispositivi a risoluzione più elevata quando si utilizza un predefinito per immagini reattive o un ritaglio avanzato.

* Per migliorare le prestazioni, la condizione `hidden=false` viene spostata dalla query JCR al valutatore [!UICONTROL QueryBuilder]. Per verificare che un predicato nascosto funzioni dopo la modifica, [!DNL Experience Manager] controlla che non venga visualizzata alcuna cartella nascosta.

* Possibilità di ripristinare le pagine e la struttura eliminate su una pagina [!DNL Experience Manager Sites].

* Supporto per un nuovo utente per aggiornare il token di accesso utilizzando un token di aggiornamento per il servizio di configurazione del mailer.

* [Supporto per il meccanismo SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) per il servizio di configurazione della posta.

* Supporto per le versioni 4.2 e 4.4 di [!DNL MongoDB] .

* Le occorrenze di nomi relativi a Hong Kong, Macao e Taiwan vengono aggiornate in base alle nuove convenzioni di denominazione per le impostazioni internazionali e le regioni cinesi.

* Miglioramenti all’accessibilità in [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590) e [[!DNL Dynamic Media]](#accessibility-dm-6590).

* L&#39;ottimizzazione DPR (Device Pixel Ratio) e della larghezza di banda della rete per l&#39;imaging intelligente consente di fornire immagini di qualità superiore in modo efficiente; su dispositivi con display ad alta risoluzione e larghezza di banda limitata. Per informazioni dettagliate e sulla timeline, consulta [domande frequenti relative all’imaging intelligente](/help/assets/imaging-faq.md).

* [!DNL Dynamic Media] delivery (modificatore `fmt` URL) supporta il formato immagine AVIF (formato immagine AV1) di nuova generazione. Per ulteriori dettagli e timeline, consulta [servizio immagini e rendering API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

* Possibilità di inviare un messaggio e-mail di notifica a un gruppo utilizzando il passaggio del flusso di lavoro [!UICONTROL Assegna attività] .

* Possibilità di recuperare una bozza di comunicazione interattiva dopo aver modificato la comunicazione interattiva di origine.

* Imposta il nome di dominio personalizzato per il caricamento, il rendering e la convalida del servizio reCAPTCHA in [!DNL Experience Manager Forms].

* Miglioramenti ai dati di input per il passaggio del flusso di lavoro [!UICONTROL Invoke Form Data Model Service] .

* Possibilità di utilizzare più pagine master in un modello Documento di record in [!DNL Experience Manager Forms].

* Interruzioni della pagina di supporto nel documento di record in [!DNL Experience Manager Forms].

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.7.

Per un elenco completo delle funzioni e dei miglioramenti introdotti in [!DNL Experience Manager] 6.5.9.0, consulta [novità in [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>A partire dal Service Pack 9, [!DNL Experience Manager] i clienti possono sviluppare e utilizzare le loro [!DNL Experience Manager] applicazioni con distribuzioni delle [!DNL Azul Zulu] build di OpenJDK, conformi agli standard di Java™ SE.
>Il supporto per i [!DNL Azul Zulu] JDK è fornito anche da Adobe ai clienti [!DNL Experience Manager].
>È possibile scaricare le versioni pertinenti dei JDK di [!DNL Azul Zulu] da [Distribuzione di software di Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>I diritti di utilizzo della tecnologia Oracle Java™, distribuiti per Adobe, scadranno entro la fine di dicembre 2022. [!DNL Experience Manager] I clienti sono incoraggiati a pianificare e implementare l’utilizzo di  [!DNL Azul Zulu] JDK al più tardi entro questa data. Per ulteriori informazioni sull&#39;utilizzo della tecnologia [!DNL Oracle Java™] e della tecnologia [!DNL Azul Zulu], consulta le [Domande frequenti ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf) associate.

Di seguito è riportato l&#39;elenco delle correzioni fornite nella versione 6.5.9.0 di .[!DNL Experience Manager]

### [!DNL Sites] {#sites-6590}

* Le pagine pubblicate con la proprietà Authentication Requirements abilitata non reindirizzano alla pagina di accesso e restituiscono il messaggio di errore 404 (NPR-36354).

* Durante la creazione di un collegamento ipertestuale, l’opzione per cercare un collegamento non funziona nel componente testo (NPR-35849).

* Viene attivata una query traversal utilizzando l’API `com.day.cq.wcm.commons.ReferenceSearch`. Ha un impatto sulle prestazioni del server [!DNL Experience Manager] (NPR-36407).

* Il contenitore di layout nidificato all’interno di un altro contenitore di layout ridimensionato mostra un numero errato di colonne per i relativi componenti secondari, causando l’assenza dell’allineamento di questi componenti alla griglia (NPR-36359).

* Il controllo collegamenti esterno visualizza collegamenti esterni validi come collegamenti non validi (NPR-36289).

* Dopo aver visualizzato i riferimenti per un po&#39; di tempo, il pannello dei riferimenti inizia a visualizzare un messaggio di errore (NPR-36167).

* Quando si sposta un componente, parsys creato automaticamente non ha il nodo `sling:resourceType` (NPR-36165).

* Quando si tenta di sincronizzare una Live Copy (utilizzando le configurazioni di rollout [!UICONTROL Attiva su Blueprint activation] e [!UICONTROL Disattiva su Blueprint activation]) se un componente viene eliminato nel master livecopy, la sincronizzazione non riesce e viene registrato un `NullPointerException` (NPR-36127).

* Quando un utente digita un testo improvvisato per il tag (tag che non esiste sul sistema) e preme Invio, il tag viene visualizzato sotto il campo ma quando il frammento di contenuto viene salvato e riaperto, il tag improvvisato scompare (NPR-36132).

* Nella casella in entrata non è disponibile l’opzione per visualizzare lo stato delle operazioni asincrone (NPR-36104).

* Un componente duplicato viene creato dopo il ripristino dell’ereditarietà (NPR-36000).

* Quando si utilizza il `RemoteContentRenderingService`, la richiesta al `RemoteContentRendererRequestHandler.getRequest` include sempre la pagina principale per il `ComponentExporter`, ma non include la pagina richiesta se non è inclusa nel modello principale in base alle opzioni di profondità di traversata e filtro impostate. La richiesta deve sempre includere la pagina richiesta in modo che il SPA disponga di informazioni sufficienti per eseguire il rendering di una risposta (NPR-35961).

* Gli elementi onTime/offTime non vengono attivati/disattivati in base al valore previsto onTime/offTime (NPR-35936).

* Quando pubblichi una pagina contenente un Frammento esperienza senza proprietà `cq:lastModified` , si verifica un `NullPointerException` (NPR-35914).

* Quando si tenta di ridimensionare un componente all’interno di un contenitore, non è possibile ripristinare le dimensioni originali. Quando le dimensioni del contenitore dei componenti sono ridotte, non è possibile ripristinare le dimensioni originali (NPR-35809).

* Nella finestra di dialogo di rollout, attivata nell’editor o dalla panoramica Live Copy, le icone di stato per le pagine staccate, sospese o non create sono errate (NPR-35691).

* Casella di controllo per il rollout su pagina di Multi-Site Manager delle proprietà master ignora il rollout della pagina e delle sottopagine (NPR-35634).

* La funzionalità di ripristino della struttura, disponibile nell&#39;interfaccia classica, non è presente nell&#39;interfaccia utente touch (CQ-4315352, CQ-4309415).

* Problemi durante il ripristino dell’ereditarietà e il rollout di una pagina in una pagina [!DNL Experience Manager Sites] (NPR-36033).

### [!DNL Assets] {#assets-6590}

I seguenti miglioramenti dell’esperienza utente vengono eseguiti in [!DNL Assets]:

* Per visualizzare le risorse non ordinate in base ai parametri [!UICONTROL Crea], [!UICONTROL Modifica] o [!UICONTROL Nome], [!DNL Adobe Experience Manager] offre un&#39;opzione [!UICONTROL Nessuno] nelle opzioni [!UICONTROL Ordina per]. L’opzione [!UICONTROL None] assicura che le risorse nell’interfaccia utente di Assets (nella vista a schede, colonne e informazioni approfondite) siano nello stesso ordine in cui esistono nel nodo JCR (NPR-36356).

* Per impostare l’ID e-mail in minuscolo nella risposta API ACP da [!DNL Adobe Experience Manager], è stata introdotta un’impostazione opzionale; poiché gli utenti [!DNL Adobe Asset Link] non potevano archiviare le risorse se il loro ID non conteneva tutti i caratteri in lettere minuscole. Il pannello [!DNL Adobe Asset Link] utilizza la risposta API ACP da [!DNL Adobe Experience Manager] (CQ-4317704).

I seguenti miglioramenti dell’accessibilità sono disponibili in [!DNL Assets] come parte del service pack 9:

È stato migliorato il contrasto (con lo sfondo) del testo e delle icone seguenti, in modo che gli utenti con visione limitata e percezione del colore possano comprendere:

* Titolo della risorsa sulla pagina [!UICONTROL Proprietà] (NPR-35967).
* Icone di valutazione a stella nelle sezioni [!UICONTROL Valutazione] in vari punti (NPR-36009).
* Testo nella vista a schede della risorsa e della cartella (NPR-35966).
* Testo segnaposto nella vista [!UICONTROL Timeline] (NPR-35965).
* Nomi di risorse nei risultati di ricerca delle risorse (NPR-35964).
* Testo segnaposto nella finestra di dialogo [!UICONTROL Condivisione collegamenti] (NPR-35963).
* [!UICONTROL Metadati],  [!UICONTROL stato] e   altro testo nell’opzione   Elenco nella finestra di dialogo  [!UICONTROL Visualizza ] impostazioni (NPR-35910).
*  Posizione e  [!UICONTROL tipo per la ] ricerca di testi segnaposto nella ricerca globale (NPR-35909).
* Espandi e comprimi le icone in [!UICONTROL Struttura contenuto] (NPR-35908).
* Il testo [!UICONTROL Risorse] nella pagina in cui vengono visualizzate le cartelle di risorse (NPR-35905).
* Testo in [!UICONTROL Metadati risorsa], [!UICONTROL Statistiche di utilizzo] all’interno dell’opzione [!UICONTROL Panoramica] nella pagina dei dettagli della risorsa (NPR-35904).
* Testo dei tasti di scelta rapida per le opzioni [!UICONTROL proprietà] e [!UICONTROL modifica] nella pagina dei dettagli della risorsa (NPR-35904).

Le seguenti correzioni di bug sono disponibili in [!DNL Assets] come parte del service pack 9:

* I tag creati all’interno di un elemento di selezione dei tag in un modulo [!UICONTROL Folder Metadata Schema] non vengono salvati (NPR-36119).

* Quando si utilizza una piccola ellisse per annotare le risorse, l’ellisse si sovrappone al numero dell’annotazione nella versione di stampa (NPR-36114).

* A volte, nella vista a colonne, [!DNL Experience Manager] non richiede conflitti tra risorse duplicati quando viene caricata una risorsa duplicata (NPR-36048).

* La finestra di dialogo Condividi collegamento non si chiude facendo clic sul pulsante Chiudi se viene aperta e non vengono apportate modifiche (NPR-36030).

* Quando selezioni più risorse per aggiornare le proprietà, a volte si verifica un errore o le proprietà di una risorsa deselezionata vengono aggiornate (NPR-36002).

* Quando all’inizio o alla fine dei nomi dei file di risorse vengono aggiunti spazi bianchi per il caricamento delle risorse, con i caratteri rimanenti uguali al nome di una risorsa esistente nell’archivio, la risorsa esistente viene sostituita senza registrare alcun errore (NPR-36001).

* Quando il video viene riprodotto nella pagina dei dettagli della risorsa, le opzioni di riproduzione e pausa non funzionano (NPR-35999).

* Quando si annulla la pubblicazione in blocco delle risorse, Brand Portal genera un errore che indica che l’URI della richiesta è troppo lungo (NPR-35954).

* Quando viene stampata una risorsa con testo di annotazione lungo, il testo dell’annotazione viene troncato, anche se è disponibile spazio (NPR-35948).

* L’opzione per passare alla pagina successiva è disabilitata quando si seleziona la pagina in visualizzazione Modelli nella pagina Crea catalogo (CQ-4315462).

* Quando si avvia l’aggiornamento del flusso di lavoro delle risorse sulla risorsa video, la pagina viene aggiornata ripetutamente (CQ-4313375).

* Le cartelle DAM non possono essere eliminate o spostate e viene registrata un&#39;eccezione (NPR-35942).

### [!DNL Dynamic Media] {#dynamic-media-6590}

In [!DNL Adobe Experience Manager] 6.5.9.0, i seguenti miglioramenti dell’accessibilità sono disponibili in [!DNL Dynamic Media]:

* Quando apri la finestra di dialogo per aggiungere risorse utilizzando i tasti di tastiera nell&#39;editor [!UICONTROL Set immagini]:
   * Gli assistenti vocali osservano che la finestra di dialogo viene aperta.
   * Lo stato attivo della tastiera si sposta sulla finestra di dialogo all&#39;apertura.
   * Lo stato attivo torna all’opzione Aggiungi risorsa quando la finestra di dialogo viene chiusa (CQ-4312134).

* È ora possibile aggiungere e modificare gli hotspot sulle risorse utilizzando i tasti di scelta rapida nell’editor Hotspot (CQ-4305965).

* È ora possibile inserire i collegamenti ipertestuali in un punto attivo tramite la gestione dei punti attivi tramite i tasti di tastiera. Lo stato attivo dell’assistente vocale ora si sposta sul campo per modificare il percorso URL e l’opzione per aprire la finestra di dialogo di selezione (CQ-4290735).

* Il contrasto (con lo sfondo) del testo e dei controlli nella pagina Editor set di immagini è migliorato, in modo che gli utenti con visione limitata e percezione del colore possano comprendere (CQ-4290733).

* Ora puoi passare alle opzioni di condivisione delle risorse in Editor predefiniti per visualizzatore e comprimere l’opzione di condivisione estesa utilizzando i tasti di scelta rapida (CQ-4290724).

* È ora possibile spostarsi e visualizzare le descrizioni comandi sulle icone delle informazioni e le icone di avviso nelle schede Base e Avanzate della pagina Modifica codifica video utilizzando i tasti di scelta rapida (CQ-4290722).

* Gli assistenti vocali ora leggono le istruzioni per vari campi nella scheda Aspetto e Comportamento dell’Editor predefiniti per visualizzatori (CQ-4290721).

* Quando si naviga nella pagina Modifica predefinito immagine in modalità Modulo, l’assistente vocale legge lo scopo e i nomi dei vari campi e controlli (CQ-4290717).

* Quando si naviga nella pagina dei dettagli delle risorse, gli assistenti vocali ora descrivono lo scopo di varie opzioni all’interno dei visualizzatori (CQ-4290716).

* È stato migliorato il contrasto (con lo sfondo) del testo segnaposto L’opzione Tutte le rappresentazioni nelle rappresentazioni della pagina dei dettagli della risorsa, in modo che gli utenti con vista limitata e percezione del colore possano comprendere (CQ-4290713).

* Nel campo Titolo della risorsa in Editor set di immagini è ora disponibile un asterisco visivo per indicare un campo obbligatorio, mentre gli assistenti vocali comunicano le informazioni richieste per tale campo (CQ-4290712).

* Gli assistenti vocali ora possono accedere e visualizzare lo scopo di varie opzioni interattive all’interno dei visualizzatori nella pagina dei dettagli delle risorse (CQ-4290708).

Adobe Experience Manager 6.5.9.0 Assets risolve i seguenti problemi in [!DNL Dynamic Media]:

* I predefiniti per visualizzatori personalizzati e i CSS non vengono replicati in [!DNL Dynamic Media] quando [!DNL Dynamic Media] viene attivato selettivamente e disabilitato da [default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html#troubleshoot-dm-config) (NPR-36232).

* Quando tenti di visualizzare in anteprima le rappresentazioni video nella pagina dei dettagli delle risorse, i video vengono caricati lentamente (CQ-4320122).

* La pagina del browser non risponde e rallenta il caricamento di più di 200 risorse con il rilevatore di risorse duplicato abilitato (CQ-4319633).

* Quando una risorsa immagine panoramica viene aggiunta su un componente multimediale panoramico in una pagina, viene registrato un errore di riferimento non rilevato (CQ-4317666).

* Quando il visualizzatore per contenuti multimediali interattivi è implementato con Frammento esperienza, il frammento esperienza non viene aperto dall’editore e viene registrato un errore (CQ-4317655).

* [!UICONTROL L’opzione Pubblica su Dynamic ] Media non è disponibile nelle opzioni  [!UICONTROL Pubblicazione rapida ] nella pagina   Proprietà (CQ-4317199).

* Gli autori di siti con autorizzazioni di sola lettura possono utilizzare la funzionalità di ritaglio avanzato sulle risorse e modificare le rappresentazioni ritagliate avanzate (CQ-4316450).

* Le annotazioni video non funzionano per i percorsi delle cartelle in cui la configurazione [!DNL Dynamic Media] non è abilitata, anche se l&#39;istanza [!DNL Experience Manager] è impostata in modalità [!DNL Dynamic Media] (CQ-4314950).

* Quando il titolo delle risorse ha caratteri a doppio byte, multibyte, ASCII alto, Cirillico, coppia surrogato, Ebraico, Arabo e GB18030, dopo aver pubblicato su Dynamic Media il titolo della risorsa ha un punto interrogativo (?) (CQ-4311872).

>Problemi noti di riproduzione video in Dynamic Media *solo in Experience Manager 6.5.9.0*:
>
>* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.
>* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.


### Platform {#platform-6590}

* Quando generi una miniatura per una blueprint e distribuisci le modifiche alla Live Copy, l’ereditarietà di alcuni campi non funziona (CQ-4319517).

* Quando crei una cartella, seleziona la proprietà Orderable e aggiungi più di 20 risorse alla cartella. Selezionando tutte le risorse nella cartella viene visualizzato un conteggio errato (CQ-4316243).

* Quando aggiorni una pagina, l’ordinamento di una cartella o di una risorsa non visualizza i risultati appropriati (CQ-4316200).

* La libreria JavaScript Handlebars viene aggiornata alla versione 4.7.7 (NPR-36375).

* I bundle personalizzati non vengono aggiornati quando si installa un nuovo pacchetto di codice utilizzando Gestione pacchetti (NPR-35949).

* Un bundle `resourceresolver` Sling causa il mancato funzionamento della query `Sling:alias` (NPR-35335).

* Il percorso contestuale viene rimosso quando si imposta SSL nell’Experience Manager (NPR-35294).

* L&#39;eccezione `SegmentNotFound` viene restituita dopo una sessione di lunga durata (NPR-36405).

### Integrations (Integrazioni) {#integrations-6590}

* Impossibile salvare le proprietà di pagina con l’ereditarietà abilitata per i frammenti esperienza Cloud Services (NPR-36107).

* L’impaginazione e il caricamento lento dell’interfaccia utente IMS non presentano risultati appropriati (NPR-36046).

* Quando crei la configurazione di A4T Target e selezioni l’origine per la generazione di rapporti come [!DNL Adobe Analytics], nell’elenco a discesa non sono disponibili suite di rapporti abilitate per Adobe Target (NPR-36006).

### Progetti {#projects-6590}

* Impossibile salvare le proprietà di un progetto perché il percorso JCR del progetto non è stato risolto a causa di una barra (`/`) aggiuntiva aggiunta al percorso del progetto (NPR-36191).

### Screens {#screens-6590}

* [!DNL Experience Manager Screens] i lettori non possono eseguire l&#39;autenticazione se viene utilizzato un gestore di autenticazione a due fattori personalizzato (NPR-35854).

### Commerce {#commerce-6590}

* La procedura guidata [!UICONTROL Commerce Catalog] non riesce a caricare più di 40 elementi nella vista a colonne (CQ-4318379).

### Progetti di traduzione {#translation-6590}

* Le opzioni di aggiornamento o sovrascrittura non vengono visualizzate durante la riconversione di una pagina `es` in `es_es` (NPR-36170).

* Quando l’opzione di approvazione automatica è selezionata per un progetto con traduzione umana, lo stato del processo viene visualizzato come `Unknown` (NPR-35981).

* Quando traduci una pagina, il percorso di riferimento di [!DNL Experience Fragments] non viene aggiornato al percorso di riferimento [!DNL Experience Fragment] di destinazione (NPR-35911).

* Quando apporti modifiche alle pagine padre e figlio e invii la pagina padre per la traduzione, anche le pagine figlie vengono tradotte in modo non corretto (NPR-35896).

* Quando sono presenti più progetti di traduzione simultanei per una pagina selezionata, l&#39;opzione [!UICONTROL Vai a progetti] non si collega al progetto di traduzione più recente (NPR-35454).

* Quando pubblichi le risorse in [!DNL Dynamic Media], [!DNL Experience Manager] visualizza un messaggio non corretto per i tag non pubblicati (CQ-4315914, CQ-4315913).

* Quando apri un processo eliminato, [!DNL Experience Manager] visualizza un messaggio non corretto (CQ-4315910).

### Flusso di lavoro {#workflow-6590}

* Quando fai clic su Completa, Delega o Apri azioni per gli elementi disponibili nella casella in entrata, non esiste alcun indizio visivo per il completamento di queste azioni (NPR-36317).

### [!DNL Communities] {#communities-6590}

* Nel filtraggio dello spam, il sistema consuma il 100% dello spazio heap Java™, rendendo il server di Experience Manager non reattivo (NPR-36316, NPR-36493).
* Nei forum, i dati delle sessioni JCR provenienti da `SearchCommentSocialComponentListProvider` vengono persi (NPR-36235).
* L’apertura di un messaggio specifico nella casella in entrata riflette tutti i messaggi con impaginazione impropria e altri problemi (NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* Il flag della funzione Origine risorse è abilitato automaticamente durante la configurazione di [!DNL Experience Manager Assets] con [!DNL Brand Portal] (NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* Per [!DNL Experience Manager Forms] vengono rilasciati pacchetti del componente aggiuntivo una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].


**Moduli adattivi**

* Problemi di inizializzazione della lingua in [!DNL Experience Manager Forms] 6.5.7.0 durante la generazione di più dizionari di traduzione (NPR-36439).
* Quando si aggiunge un allegato al frammento di modulo adattivo e si invia il modulo, [!DNL Experience Manager Forms] visualizza il seguente messaggio di errore (NPR-36195):

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* Quando utilizzi la traduzione umana per aggiornare un dizionario e visualizzare in anteprima un modulo adattivo, le modifiche non vengono visualizzate (NPR-36035).

**Comunicazioni interattive**

* Quando carichi un’immagine utilizzando il canale Stampa comunicazioni interattive e la modifichi, l’immagine non è più visibile (NPR-36518).

* Quando si modifica una risorsa di testo e si compila un segnaposto, tutti gli elementi interattivi vengono rimossi dal riquadro di navigazione (NPR-35991).

**Flusso di lavoro**

* Quando chiami l&#39;endpoint REST di un servizio [!DNL Experience Manager Forms] su JBoss®, [!DNL Experience Manager] visualizza il seguente messaggio di errore (NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* Impossibile salvare un modello dati del modulo durante il binding dell&#39;argomento del servizio di lettura a un valore letterale contenente un trattino (NPR-36366).

**Sicurezza dei documenti**

* Quando imposti la certificazione e HSM per GlobalSign, [!DNL Experience Manager Forms] visualizza i messaggi di errore `Unsuported Algorithm` e `Invalid TSA Certificate` durante l&#39;aggiunta di una marca temporale a LTV (NPR-36026, NPR-36025).

**Servizi documentali**

* Aggiornamenti alla libreria [!DNL Gibson] per l&#39;integrazione con [!DNL Experience Manager Forms] (NPR-36211).

**JEE per Foundation**

* Quando selezioni Gestione endpoint nell&#39;interfaccia utente amministratore, [!DNL Experience Manager Forms] visualizza il messaggio di errore `endpoint registry failure` (CQ-4320249).

Per informazioni sugli aggiornamenti di sicurezza, vedere [[!DNL Experience Manager] pagina dei bollettini sulla sicurezza](https://helpx.adobe.com/security/products/experience-manager.html).

### Problemi noti in Experience Manager 6.5.9.0 {#known-issues-6590}

* Se aggiorni l’istanza [!DNL Experience Manager] dalla versione 6.5 alla versione 6.5.10.0, puoi visualizzare le eccezioni `RRD4JReporter` nel file `error.log` . Per risolvere il problema, riavvia l&#39;istanza.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 5 o un precedente service pack su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Gli utenti possono rinominare una cartella in una gerarchia in [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Durante l’installazione di Experience Manager 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l’integrazione di Adobe Target è configurata in Experience Manager utilizzando l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti di esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando si utilizzano funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

## [!DNL Adobe Experience Manager] 6.5.8.0 {#experience-manager-6580}

[!DNL Adobe Experience Manager] La versione 6.5.8.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 di aprile 2019. Il service pack è installato su [!DNL Adobe Experience Manager] 6.5.

Le funzioni chiave e i miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.8.0 sono:

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* Quando utilizzi la funzionalità [Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md), ora puoi visualizzare un elenco di tutte le [!DNL Sites] pagine che utilizzano la risorsa. Questi riferimenti a una risorsa sono disponibili nella pagina [!UICONTROL Proprietà] di una risorsa. Questo consente agli amministratori, agli esperti di marketing e ai bibliotecari di visualizzare in modo completo l’utilizzo delle risorse, consentendo un migliore monitoraggio, gestione e coerenza del marchio.

* Quando si elimina una risorsa a cui viene fatto riferimento in una pagina web, [!DNL Experience Manager] [visualizza un avviso](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). Puoi forzare l’eliminazione di una risorsa di riferimento oppure controllare e modificare i riferimenti visualizzati nella pagina [!DNL Properties] della risorsa. Facendo clic sui riferimenti vengono aperte le pagine locali e remote [!DNL Sites] .

* Ordinamento delle pagine Live Copy disponibili per il rollout utilizzando le proprietà [!UICONTROL Name], [!UICONTROL Last modified date,] e [!UICONTROL Last rollout date] .

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.6. <!-- TBD: Mention the version -->

Per un elenco completo delle funzioni e dei miglioramenti introdotti in [!DNL Experience Manager] 6.5.8.0, consulta [novità in [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

Di seguito è riportato l&#39;elenco delle correzioni apportate in [!DNL Experience Manager] 6.5.8.0 .

### [!DNL Sites] {#sites-6580}

* Quando una pagina viene spostata in blueprint, la destinazione dei collegamenti non viene aggiornata (NPR-35724).
* Il lettore basato su Tizen non riesce ad autenticarsi su alcuni browser. Il problema si verifica con i browser che non supportano l&#39;attributo samesite=none (NPR-35589).
* Un contenitore dinamico sbloccato non visualizza i componenti consentiti (NPR-35565).
* Quando crei una Live Copy di una pagina appena aggiunta, il Language Master crea due copie per ciascun dominio (NPR-35545).
* Deadlock nel Registro componenti SCR quando molti thread sono bloccati a causa del timer `org.apache.felix.scr.impl.ComponentRegistry`. Come risultato, [!DNL Experience Manager] smette di rispondere per un tempo indeterminato (GRANITE-33125,FELIX-6252).
* Quando esegui la ricerca di una risorsa specifica nella barra laterale, il risultato contiene alcune risorse non sottoposte a ricerca (NPR-35524).
* Quando si abilita SSL per un&#39;istanza di Experience Manager, il percorso contestuale viene rimosso (NPR-35477).
* Quando crei un elenco, aggiungi del testo come primo elemento, aggiungi una tabella come secondo elemento e aggiungi un elenco all’interno della tabella, l’elenco principale si distorce (NPR-35465).
* Quando si utilizzano plug-in diversi su voci di elenco consecutive, agli elementi di elenco viene aggiunto un tag aggiuntivo <br> (NPR-35464).
* Quando si inserisce un elenco tra due paragrafi, non è possibile aggiungere una tabella all’elenco (NPR-35356).
* Quando avvii un aggiornamento di un&#39;istanza AEM da AEM 6.3 a AEM 6.5, l&#39;avvio dell&#39;istanza di aggiornamento richiede più tempo (NPR-35323).
* Quando replichi una risorsa AEM che include una parentesi graffa (). nel nome, la replica non riesce (GRANITE-27004, NPR-35315).
* Quando si aggiungono titoli a un editor Rich Text, il pulsante paragrafo è disattivato (NPR-35256).
* Quando aggiungi un elemento a un elenco esistente, questo elimina l’elenco comprimibile o attivabile successivo (NPR-35206).
* Quando l’opzione Rollout pagina è selezionata, viene visualizzata una finestra di dialogo con tutte le Live Copy disponibili e viene eseguito il rollout automatico. Le Live Copy delle pagine vengono distribuite in tutte le aree geografiche senza l’intervento dell’utente (NPR-35138).
* Quando utilizzi l’opzione Includi elementi figlio, l’opzione Gestisci pubblicazione non elenca tutte le pagine. Sono elencate solo 22 pagine (NPR-35086).
* Quando un criterio viene modificato, il componente di testo non mantiene le modifiche ai criteri (NPR-35070).
* Quando si applicano un rientro ad alcuni elementi di un elenco numerato, tutti gli elementi mantengono lo stesso numero, anche se la numerazione deve iniziare da 1 per gli elementi con lo stesso rientro (CQ-4313011).
* Quando la minimizzazione è abilitata, non puoi modificare alcuna pagina o componente. I problemi sono iniziati dopo l&#39;installazione di AEM 6.5 Service Pack 7 (CQ-4311133).
* I filtri di ricerca e risorse Omni restituiscono risultati irrilevanti o nessun risultato (CQ-4312322, NPR-35793).
* Quando più pagine accedono contemporaneamente a una libreria client, il gestore della libreria HTML non carica la libreria client. Porta al rendering non corretto delle pagine (NPR-35538).
* Il percorso contestuale viene rimosso automaticamente quando si imposta un SSL in [!DNL Experience Manager] (NPR-35294).
* La gestione dei pacchetti non disconnette gli utenti dopo aver fatto clic sull&#39;opzione di disconnessione (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0  [!DNL Assets] risolve i seguenti problemi e fornisce i seguenti miglioramenti.

* Al ripristino di una versione precedente di una risorsa, l’evento DamEvent.Type RESTORED non viene attivato nella console OSGi (NPR-35789).
* `IndexWriter.merge` causa  `OutOfMemoryError` errori poiché la funzionalità di assegnazione tag avanzati crea  `/oak:index/lucene` indici  `/oak:index/ntBaseLucene` e di grandi dimensioni (NPR-35651).
* Viene visualizzato un messaggio di errore quando si tenta di salvare una cartella di tipo [!UICONTROL Contributo risorse] con caratteri multibyte nel nome (NPR-35605).
* Quando si utilizzano i campi del sottotipo metadati a cascata, si verifica un errore &quot;Compila questo campo&quot; errato (NPR-35643).
* Quando una risorsa esistente viene trascinata sull’ interfaccia utente [!DNL Assets] e viene creata una nuova versione, le modifiche nei metadati non sono persistenti (NPR-34940).
* Quando crei regole nell&#39;editor dello schema metadati per un menu a cascata, l&#39;opzione [!UICONTROL Dipendente da] ripete lo stesso nome (NPR-35596).
* La ricerca per similarità non funziona dopo la modifica della [!UICONTROL Barra di ricerca amministrazione risorse] (NPR-35588).
* Dall&#39;interno di una cartella, se apri la ricerca delle risorse nella barra a sinistra facendo clic su [!UICONTROL Filtro], il filtro in [!UICONTROL Stato] > [!UICONTROL Pagamento] > [!UICONTROL Estratto] non funziona (NPR-35530).
* Se tenti di eliminare tutti i tag avanzati di una risorsa e salvi le modifiche, i tag non vengono rimossi. Tuttavia, l’interfaccia utente indica che le modifiche sono state salvate (NPR-35519).
* Gli utenti non possono ridisporre o ordinare le risorse nella vista a elenco in una cartella ordinabile (NPR-35516).
* Se modifichi lo schema metadati predefinito, il campo tag della pagina [!UICONTROL Proprietà] della risorsa diventa un campo di testo. La modifica consente agli utenti inconsapevoli di aggiungere tag on-demand e i tag vengono memorizzati come stringa nell&#39;archivio (NPR-35478).
* Durante il download di una risorsa, se fornisci un nome che non dispone di un indirizzo e-mail valido, l’opzione di download non è disponibile. Tuttavia, se è selezionata un’altra opzione nella finestra di dialogo di download, il pulsante è abilitato, ma non viene inviato un messaggio e-mail (NPR-35365).
* Gli utenti non possono archiviare le risorse dopo aver modificato quelle in [!DNL Adobe InDesign] e ricevono un errore per mancanza di autorizzazioni (NPR-35341).
* La libreria JavaScript Handlebars viene aggiornata alla versione 4.7.6 (NPR-35333).
* L’interfaccia dell’editor di metadati smette di funzionare come previsto quando si inizia dalla modifica in serie dei metadati e si deselezionano gli elementi fino a quando non viene selezionato un singolo elemento (NPR-35144).
* La navigazione globale non apre la console corretta quando si fa clic all’interno della pagina `assets.html` (CQ-4312311).
* [!DNL Assets] non visualizza il rendering RGB per una risorsa con rendering RGB (CQ-4310190).
* L&#39;opzione [!UICONTROL Relate] nel menu non viene visualizzata correttamente nella pagina [!UICONTROL Proprietà] (CQ-4310188).
* Se il filtro filetype per i documenti viene utilizzato per cercare le risorse e creare una Raccolta avanzata, il filtro non viene applicato quando si accede alla raccolta. Nella ricerca vengono invece visualizzati tutti i tipi di risorse (NPR-35759).
* Non puoi trascinare e aggiungere risorse in una Lightbox dall’ interfaccia utente di [!DNL Assets] (NPR-35901).
* Quando viene creata una nuova versione di una risorsa esistente dopo la risoluzione del conflitto di denominazione, i metadati della risorsa originale vengono sovrascritti (CQ-4313594).
* Quando filtri la ricerca delle risorse utilizzando un filtro di ricerca o un predicato, apri una risorsa per visualizzarla o modificarla e torna alla pagina dei risultati della ricerca, il filtro non funziona. Tutte le risorse ricercate sono elencate come non filtrate (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* L’opzione URL per il predefinito immagine RESS è abilitata nella pagina dei dettagli della risorsa. Ora, nella pagina dei dettagli della risorsa sono disponibili entrambe le opzioni URL e RESS quando nella sezione delle rappresentazioni dinamiche è selezionato il predefinito immagine RESS . (CQ-4311241)
* Componente multimediale interattivo : il video interattivo non funziona se l’utente ha [!DNL Experience Manager] con configurazione di pubblicazione selettiva (CQ-4311054).
* Se sposti le risorse tra le cartelle, la sincronizzazione tra [!DNL Experience Manager] e [!DNL Dynamic Media–Scene7] tramite API è molto lenta (CQ-4310001).
* Quando si utilizza Omnisearch, le dimensioni dei registri aumentano in modo significativo (CQ-4309153).
* Quando la sincronizzazione selettiva è abilitata e una risorsa viene copiata (non spostata) in una cartella di sincronizzazione, non viene sincronizzata come previsto (CQ-4307122).
* Per le risorse caricate che vengono pubblicate automaticamente in DM, lo stato non viene visualizzato Pubblicato in AEM. Inoltre, la colonna dello stato di pubblicazione di Dynamic Media non mostra lo stato di pubblicazione corretto (CQ-4306415).
* Se una risorsa viene pubblicata su [!DNL Experience Manager] e è impostata per la pubblicazione su [!DNL Dynamic Media] all’attivazione, il valore dei metadati `scene7FileStatus` non viene aggiornato come previsto (CQ-4308269).
* Durante la modifica del profilo video, [!DNL Experience Manager] non visualizza i valori di altezza e bitrate impostati per il predefinito video. I campi appaiono vuoti (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* Impossibile creare un tag personalizzato per tutti i prodotti in Commerce (CQ-4310682).

* L’aggiornamento del riferimento delle risorse di prodotto fa sì che i thread di replica siano nello stato di attesa fino a quando il thread ProductAssetListener non completa i suoi impegni verso il JCR (NPR-35269).

### Piattaforma {#platform-6580}

* Quando si utilizza un componente Visualizzazione tabulazione Coral senza schede e si attiva una convalida Foundation, si verifica il seguente errore (NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* La replica in avanti SCD non riesce per gli eventi Delete per i nodi che includono una virgola nel nome (NPR-35191).

* Dopo l&#39;aggiornamento a AEM 6.5.7, le build iniziano a non riuscire. Il motivo è che una vecchia versione o nessun jackson-core è incorporato nel uber-jar (GRANITE-33006).

### Interfaccia utente {#ui-6580}

* Quando si passa dalla vista a schede alla vista a elenco per i documenti presenti in una cartella della console Risorse, l’ordinamento non funziona correttamente (NPR-35842).

* Quando si crea un collegamento ipertestuale a un testo in un componente di testo, la funzione di ricerca non visualizza i risultati appropriati (NPR-35849).

* Quando un valore non viene fornito a un campo nascosto contrassegnato come obbligatorio, impedisce il salvataggio di un componente (NPR-35219).

### Integrations (Integrazioni) {#integrations-6580}

* Quando utilizzi valori diversi per l’ID tenant IMS e il codice client di Target, [!DNL Experience Manager] non riesce a integrarsi con [!DNL Adobe Target] (NPR-35342).

### Progetti di traduzione {#translation-6580}

* Problemi durante l’esportazione o l’importazione di un processo di traduzione in [!DNL Experience Manager] (NPR-35259).

### Campaign {#campaign-6580}

* Quando crei una pagina della campagna utilizzando un modello predefinito nell’interfaccia utente touch e apri la scheda E-mail nella finestra di dialogo delle proprietà della pagina, la variabile di personalizzazione per i campi oggetto e corpo rimane disabilitata (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* Quando si aggiunge una struttura di pagina a un gruppo community, il titolo [!UICONTROL Gruppo] nel breadcrumb viene modificato nel titolo del primo [!UICONTROL Pagina] (NPR-35803).
* A differenza dei moderatori, un membro della comunità standard non è in grado di accedere e modificare alcun post provvisorio (NPR-35339).
* Controllo degli accessi non funzionante e rifiuto del servizio con `DSRPReindexServlet` che riduce il sito community fino al completamento dell&#39;indicizzazione (NPR-35591).
* La rimozione di [!UICONTROL Tutti gli utenti] dal campo [!UICONTROL Amministratori] in realtà non li rimuove dal back-end (NPR-35592, NPR-35611).
* Il componente [!UICONTROL Componi messaggio] non restituisce alcun risultato quando il testo immesso è una corrispondenza parziale (NPR-35666).

* È possibile notare un certo impatto sulle prestazioni e lentezza durante il tentativo di aggiungere tag a un nuovo blog selezionando **[!UICONTROL Aggiungi tag]**. Per migliorare le prestazioni, installa [cqTagLucene-0.0.1.zip hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip).

### [!DNL Brand Portal] {#brandportal-6580}

* L’aggiunta di un membro a una cartella di tipo [!UICONTROL Contributo risorse] mostra la didascalia [!UICONTROL Aggiungi utente o gruppo] nell’interfaccia utente, anche se sono supportati solo gli utenti attivi di Brand Portal e non i gruppi (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>Per [!DNL Experience Manager Forms] vengono rilasciati pacchetti del componente aggiuntivo una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].

**Moduli adattivi**

* Quando si inserisce una tabella con una riga ripetibile in un pannello ripetibile con più istanze in un modulo adattivo, la tabella viene sempre aggiunta alla prima istanza del pannello (NPR-35635).

* Quando lo stato attivo raggiunge nuovamente il componente CAPTCHA dopo averlo verificato correttamente in un modulo adattivo, [!DNL Experience Manager Forms] visualizza il messaggio di errore `Provide Captcha phrase to proceed` (NPR-35539).

**Comunicazione interattiva**

* Quando si invia un modulo tradotto, i messaggi di invio vengono visualizzati in inglese e non vengono tradotti nella lingua appropriata (NPR-35808).

* Quando si include una condizione Nascondi nell&#39;XDP o nei frammenti di documento allegati, la comunicazione interattiva non viene caricata (NPR-35745).

**Gestione della corrispondenza**

* Quando si modifica una lettera, il caricamento dei moduli con condizioni richiede un tempo maggiore (NPR-35325).

* Quando selezioni una risorsa dal riquadro di navigazione a sinistra che non è inclusa in una lettera e quindi selezioni la risorsa successiva, l’evidenziazione blu non viene rimossa dalla risorsa selezionata in precedenza (NPR-35851).

* Quando si modificano i campi di testo in una lettera, [!DNL Experience Manager Forms] visualizza il messaggio di errore `Text Edit Failed` (CQ-4313770).

**Flusso di lavoro**

* Quando tenti di aprire un modulo adattivo su un&#39;applicazione mobile [!DNL Experience Manager Forms] per iOS, l&#39;applicazione si ferma per rispondere (CQ-4314825).

* La scheda [!UICONTROL To-do] nell’area di lavoro HTML visualizza i caratteri HTML (NPR-35298).

**XMLFM**

* Quando si genera un documento XML utilizzando il servizio di output, si verifica l&#39;errore `OutputServiceException` per alcuni dei file XML (CQ-4311341, CQ-4313893).

* Quando applichi la proprietà apice al primo carattere del punto elenco, la dimensione del punto elenco diventa più piccola (CQ-4306476).

* I PDF forms generati utilizzando il servizio di output non includono bordi (CQ-4312564).

**Designer**

* Quando si apre un file XDP in [!DNL Experience Manager Forms] Designer, viene generato un file designer.log nella stessa cartella del file XDP (CQ-4309427, CQ-4310865).

**Moduli HTML5**

* Quando selezioni una casella di controllo in un modulo adattivo nel browser Web [!DNL Safari] per [!DNL iOS 14.1 or 14.2], non vengono visualizzati altri campi (NPR-35652).

**Gestione Forms**

* Nessun messaggio di conferma per indicare il corretto caricamento in massa di file XDP nell’archivio CRX (NPR-35546).

**Sicurezza dei documenti**

* Sono stati segnalati diversi problemi per l’opzione [!UICONTROL Modifica criterio] in AdminUI (NPR-35747).

### Problemi noti in Experience Manager 6.5.8.0 {#known-issues-6580}

* Se aggiorni la tua istanza [!DNL Experience Manager] dalla versione 6.5 alla versione 6.5.8.0, puoi visualizzare le eccezioni `RRD4JReporter` nel file `error.log` . Riavvia l&#39;istanza per risolvere il problema.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 5 o un precedente service pack su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Contatta l’Assistenza clienti Adobe in caso di problemi durante la modifica e la creazione di regole a cascata nella finestra di dialogo [!UICONTROL Folder Metadata Schema Forms Editor] e [!UICONTROL Metadata Schema Forms Editor] utilizzando [!UICONTROL Define Rule] (Definisci regola). Le regole già create e salvate funzionano come previsto.

* Se una cartella nella gerarchia viene rinominata in [!DNL Experience Manager Assets] e la cartella nidificata contenente una risorsa viene pubblicata in [!DNL Brand Portal], il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene pubblicata nuovamente.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Se la procedura guidata [!UICONTROL Configurazione risorse collegate] restituisce un messaggio di errore 404 dopo l&#39;installazione, reinstallare manualmente i pacchetti `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` utilizzando Gestione pacchetti.

* Durante l’installazione di Experience Manager 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l’integrazione di Adobe Target è configurata in Experience Manager utilizzando l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti di esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando si utilizzano funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

## [!DNL Adobe Experience Manager] 6.5.7.0 {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 è un aggiornamento importante che include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 di aprile 2019. Il Service Pack è installato su [!DNL Adobe Experience Manager] 6.5.

Le funzioni chiave e i miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.7.0 includono:

* L’esecuzione dei movimenti della pagina e dei rollout MSM come operazioni asincrone per ridurne l’impatto sulle prestazioni di runtime.

* Gli utenti possono ordinare le risorse digitali nelle viste a schede e a colonne.

* [!DNL Assets] e  [!DNL Dynamic Media] forniscono diversi miglioramenti dell’accessibilità. I miglioramenti riguardano la navigazione da tastiera, l’uso di assistenti vocali e la possibilità per gli utenti di utilizzare tecnologie per l’accessibilità simili (AT). Consulta [[!DNL Assets] miglioramenti](#assets-6570) e [[!DNL Dynamic Media] miglioramenti](#dynamic-media-6570).

* [Configurazione del client HTTP del modello dati modulo ](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) per ottimizzare le prestazioni.

* [Disponibilità dell’opzione Ripristina per ciascun ](../../help/forms/using/resize-using-layout-mode.md#resize-components) componente in modalità Layout

* [!DNL Experience Manager] 6.5 Service Pack 7 Forms migliora le prestazioni per:

   * Convalida dei valori dei campi sul server quando si invia un modulo adattivo.

   * Conversione di un modulo PDF in un modulo adattivo utilizzando [!DNL Automated Forms Conversion service].

* Supporto per [!DNL Microsoft SQL Server] 2019 in [!DNL Experience Manager Forms].

* Supporto dei gruppi di disponibilità [!DNL Microsoft] SQL Server 2016 Always On per le distribuzioni OSGi ad alta disponibilità.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.5.

Per un elenco completo delle funzioni e dei miglioramenti introdotti in [!DNL Experience Manager] 6.5.7.0, consulta [Novità in [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

Di seguito è riportato l&#39;elenco delle correzioni apportate in [!DNL Experience Manager] 6.5.7.0 .

### [!DNL Sites] {#sites-6570}

* Quando apri l’opzione [!UICONTROL Timewrap] per una pagina, mantieni aperta l’opzione della barra laterale Timeline e accedi alla console [!UICONTROL Sites] , si verifica l’errore `Failed to Load` (NPR-34951).

* L&#39;opzione [!UICONTROL Timewrap] non visualizza le immagini per l&#39;intervallo di date e ore selezionato (NPR-34951).

* Quando un filtro chiama `getHeader()` da una pagina contenente un frammento di contenuto, si verifica l&#39;errore `java.lang.AbstractMethodError` (NPR-34942).

* Quando il percorso di una pagina contiene più sottostringhe di contenuto, il rendering delle anteprime non riesce e non riesce nemmeno la funzione di confronto delle versioni (NPR-34740).

* Quando imposti un valore numerico per la proprietà dell’etichetta di tipo `String` di un componente, puoi eliminare il componente e annullare l’operazione di eliminazione. Tuttavia, dopo aver annullato l’eliminazione, la proprietà dell’etichetta cambia da `String` a `Long` (NPR-34739).

* La seguente eccezione si verifica quando si aggiunge un frammento esperienza basato su un modello con layout bloccato a una pagina (NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* Quando si sposta una cartella, si verificano problemi di attraversamento e si verifica il seguente errore (NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* Quando vengono create, pubblicate e spostate nuove risorse in una nuova posizione, viene creato il flusso di lavoro `Request to complete move operation` e si verifica uno stato Interrotto. Il caricamento di una nuova risorsa ed esecuzione di un’operazione `move` comporta la creazione del flusso di lavoro `Request to complete move operation` in sospeso (NPR-34543).

* Quando si esporta un frammento esperienza da un ambiente [!DNL Experience Manager] 6.5.2 a [!DNL Target] Standard, la chiamata API non riesce perché la proprietà workspace non è disponibile per [!DNL Target] Standard (NPR-34557).

* Gli utenti non possono pubblicare pagine tramite l&#39;opzione [!UICONTROL gestisci pubblicazione] perché l&#39;opzione [!UICONTROL Pubblica] scompare (NPR-34542).

* Quando aggiungi alcuni stili al testo, al testo viene aggiunto un tag `<div>` e lo stile non può più essere applicato al testo (NPR-34531).

* Quando si seleziona una voce in un menu a comparsa e si aggiornano i file richiesti, non è possibile salvare i valori della finestra di dialogo, poiché l&#39;altro menu ha un campo obbligatorio vuoto (NPR-34529).

* Quando crei una pagina da un modello personalizzato e la sposti all’interno della gerarchia della blueprint, i componenti eliminati in precedenza dalla pagina iniziano a essere visualizzati nella pagina all’interno della gerarchia della Live Copy (NPR-34527).

* Una volta applicato lo stile di un articolo a un contenuto, non può essere rimosso (NPR-34486).

* Tutte le Live Copy e le copie di un Frammento esperienza puntano allo stesso [!DNL Adobe Target] ID offerta (NPR-34469).

* Gli elementi dell’elenco puntato vengono visualizzati in aggiunta all’elenco numerato (NPR-34455).

* L’opzione Confronta con sorgente non mostra la differenza tra la pagina sorgente e la versione modificata di una pagina (NPR-34285).

* Quando elimini una pagina, i dettagli del controllo delle versioni non sono configurabili (NPR-34159).

* Quando un utente seleziona l&#39;opzione di dialogo [!UICONTROL Apri selezione], lo stato attivo si sposta sul controllo nascosto presente nella pagina (CQ-4307779, CQ-4293601).

* Quando si sposta una cartella pubblicata sull&#39;autore, i percorsi delle cartelle non vengono aggiornati di conseguenza sull&#39;istanza Pubblica (CQ-4305144).

* Quando un utente seleziona il tasto `Enter` sull&#39;opzione [!UICONTROL Seleziona tutto], lo stato attivo non si sposta sull&#39;opzione [!UICONTROL Crea controllo] (CQ-4293599).

* Quando si seleziona il tasto `Esc`, lo stato attivo non viene ripristinato nel controllo principale (CQ-4293593, CQ-4293590).

* Migliorata la conformità alle linee guida WCAG per l’ [!DNL Sites] interfaccia utente e componenti core (CQ-4293448).

*  Le funzioni   di zoom e ridimensionamento sono disabilitate per la  [!DNL Sites Editor] pagina (CQ-4282353).

* Dopo aver utilizzato l’opzione Ruota a destra, l’assistente vocale smette di narrare lo stato di rotazione o capovolgimento corrente (CQ-4282128).

* I pulsanti di dialogo Fine e Annulla Configura hanno numerosi arresti tabulazione (CQ-4274601).

* Lo spostamento di pagine con un nome simile sullo stesso livello non è consentito (NPR-35041).

* Dopo aver selezionato l&#39;opzione Cancella (x), lo stato attivo della tastiera non si sposta sul campo [!UICONTROL Filtro] (CQ-4293581).

* Quando esegui l’aggiornamento a [!DNL Experience Manager] 6.5.6.0, il comportamento del sistema di paragrafi ereditato cambia e non funziona correttamente (NPR-35117).

* Gli utenti della tastiera non possono spostare lo stato attivo in un ordine appropriato dopo aver selezionato la sezione [!UICONTROL Azione] in una pagina [!DNL AEM Sites] (CQ-4307786).

* Dopo aver selezionato un’opzione nell’elenco del menu di destinazione del collegamento della barra degli strumenti dell’editor Rich Text quando si modifica un frammento di contenuto, la finestra di dialogo per l’authoring dei frammenti di contenuto inizia a presentare uno sfarfallio (CQ-4305532).

* Gli utenti di tastiera non possono selezionare le opzioni nell&#39;elenco a discesa [!UICONTROL Aggiungi componente] utilizzando il tasto freccia giù (CQ-4295097).

* Lo stato attivo non si sposta in un ordine appropriato quando selezioni una data dal menu Calendario nella scheda [!UICONTROL Risorse] di una pagina [!DNL Sites] (CQ-4293600).

* Lo stato attivo non si sposta sulle opzioni successive o precedenti per gli utenti della tastiera dopo l’eliminazione delle opzioni Collegamento o Testo disponibili durante la modifica di una pagina Sites (CQ-4293597).

* Gli utenti della tastiera non possono tornare a visualizzare altre opzioni nella sezione [!UICONTROL Azioni] dopo aver visualizzato le opzioni disponibili e aver premuto il tasto `Esc` (CQ-4293592).

* Quando si attiva l&#39;opzione [!UICONTROL Ruota] per un&#39;immagine in modalità [!UICONTROL Modifica], l&#39;elemento attivo a schede, invece di rimanere su Ruota, passa all&#39;opzione [!UICONTROL Ripristina] per gli utenti di tastiera (CQ-4293587).

* Nella finestra di dialogo [!UICONTROL Apri selezione] disponibile nella scheda [!UICONTROL Collegamento e azioni] , lo stato attivo si sposta sugli elementi nascosti nella pagina dopo l&#39;opzione [!UICONTROL Annulla] (CQ-4293579).

* Quando gli utenti della tastiera modificano un&#39;immagine, accedono all&#39;opzione [!UICONTROL Fine] e premono il tasto Invio, gli assistenti vocali non ne annunciano il completamento (CQ-4282351).

* Le opzioni Sposta su e Sposta giù disponibili nella finestra di dialogo [!UICONTROL Collegamento e azioni] non sono disponibili per gli utenti di utilità di lettura dello schermo e tastiera (CQ-4281120).

* Gli utenti della tastiera non possono ripristinare lo stato attivo dopo aver navigato all&#39;opzione Chiudi (X) nella pagina [!UICONTROL Proprietà] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0  [!DNL Assets] risolve i seguenti problemi e fornisce i seguenti miglioramenti.

* I seguenti miglioramenti sono stati apportati all’accessibilità in [!DNL Experience Manager Assets] in questa versione. Per ulteriori informazioni, consulta [funzioni di accessibilità in [!DNL Assets]](/help/assets/accessibility.md).

   * Quando si naviga nella timeline utilizzando una tastiera, il tasto `Esc` può comprimere l&#39;opzione [!UICONTROL Mostra tutto] senza perdere lo stato attivo (CQ-4293598).
   * Quando si naviga utilizzando il tasto di tabulazione della tastiera, dopo aver rimosso l’ultimo tag dai tag aggiunti, il campo tag mantiene lo stato attivo (NPR-35109).
   * [!DNL Experience Manager] i componenti ora contengono informazioni appropriate per nome, ruolo e valore che devono essere utilizzati dagli assistenti vocali (NPR-34255).
   * Dopo aver eliminato la casella combinata Tipo/Dimensione, la casella combinata Collegamento, la casella combinata Lingua o la casella di modifica Testo, lo stato attivo torna agli elementi dell&#39;interfaccia utente successivi o precedenti o a un elemento dell&#39;interfaccia utente più rilevante (CQ-4293585).
   * Quando si passa il puntatore del mouse sulle opzioni, vengono visualizzati suggerimenti come Seleziona e Scarica . Gli utenti che utilizzano una lente di ingrandimento dello schermo potrebbero non vedere le miniature dei file a causa di questi suggerimenti. Ora è possibile mantenere lo stato attivo, dopo aver rimosso l&#39;opzione utilizzando il tasto `Escape`. (CQ-4293554).
   * Selezionando una cella della griglia dalla griglia presente nella pagina, lo stato attivo si sposta sulla barra delle azioni visualizzata sullo schermo (CQ-4282127).
   * Gli utenti visivi possono distinguere tra testo normale e collegamento, in quanto vengono visualizzati indizi visivi (sottolineatura e icona freccia) per i collegamenti a tutte le soluzioni nella home page di [!DNL Experience Manager] (CQ-4282072).

* Il seguente miglioramento dell’esperienza utente viene eseguito in [!DNL Assets]:

   * Abilita l’ordinamento delle risorse nelle viste a schede e a colonne (NPR-35097).

* Dopo l’aggiornamento alla versione 6.5, se un file JSON viene generato utilizzando l’API HTTP Assets, si verificano problemi con la codifica utilizzata nel file (NPR-35129).

* Gli utenti di un gruppo a cui non è stata concessa l’autorizzazione per creare raccolte (l’opzione Crea raccolta non è disponibile) possono comunque creare raccolte accedendo direttamente all’URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* Se ordinati per nome, le risorse ricercate vengono ordinate in modo sensibile a maiuscole e minuscole. In questo modo vengono creati due elenchi ordinati separati in base al casing che vengono visualizzati in modo ordinato nei risultati della ricerca (NPR-35068).

* Quando un frammento di contenuto viene aperto nell’editor, i messaggi di avviso (`Invalid value specified for a metadata property`) vengono registrati nei registri degli errori (NPR-35012).

* Gli utenti senza privilegi di amministratore possono modificare le risorse scadute utilizzando l’app desktop [Experience Manager]. (NPR-34993).

* Quando la stessa risorsa viene trascinata sull’interfaccia utente di Assets e viene creata una nuova versione, le modifiche nei metadati non sono persistenti (NPR-34940).

* Durante la modifica delle raccolte, un utente può eliminare il titolo della raccolta e salvare le modifiche (NPR-34889).

* Quando si carica un’immagine duplicata, viene visualizzata un’opzione di eliminazione. Se selezioni Elimina , le immagini vengono caricate. Viene attivato anche il flusso di lavoro Risorsa di aggiornamento DAM (NPR-34744).

* Quando si utilizza [!DNL Adobe Asset Link] con [!DNL Adobe InDesign], i risultati della ricerca non contengono cartelle e raccolte ma contengono solo risorse (NPR-34699, CQ-4303666).

* Passando il puntatore del mouse sulla vista a schede, lo schermo scorre in seguito all&#39;attivazione (automatica) delle azioni rapide disponibili nella scheda (NPR-34514).

* Quando modifichi le proprietà di più risorse in blocco, selezionando l&#39;opzione [!UICONTROL Salva] viene chiusa la visualizzazione dell&#39;editor in blocco e viene reindirizzato alla pagina principale [!DNL Assets]. Questo comportamento è lo stesso dell&#39;opzione [!UICONTROL Salva e chiudi] e non è previsto (NPR-34546).

* La raccolta avanzata non presenta l’impostazione corretta dell’interfaccia utente dopo il salvataggio. La query viene salvata correttamente ma l&#39;interfaccia visualizza sempre l&#39;ultimo predicato Option aggiunto (NPR-34539).

* Quando si aggiungono risorse a [!DNL Experience Manager], i metadati senza spazio dei nomi non vengono importati (NPR-34530).

* Quando si trascina una risorsa su una cartella per spostarla, l’interfaccia utente visualizza anche l’opzione [!UICONTROL Rilascia in Lightbox] e [!UICONTROL Rilascia in raccolta]. Anche se l&#39;operazione di spostamento viene annullata, l&#39;interfaccia utente continua a visualizzare le ultime due opzioni (NPR-34526).

* Il simbolo `%>` viene visualizzato nella pagina delle raccolte (NPR-34499).

* Nella vista a colonne, [!DNL Assets] visualizza nomi di cartelle e risorse duplicati quando si scorre verso l’alto o il basso prima che vengano visualizzate tutte le risorse (NPR-34464).

* Se crei una cartella privata subito dopo la creazione di una cartella pubblica, la cartella pubblica utilizza le impostazioni della cartella privata (NPR-34415).

* Nella vista a schede, le schede non sono elencate in ordine alfabetico e le schede non possono essere ordinate in ordine alfabetico (NPR-34234).

* Quando si riaprono le regole a cascata, le scelte non vengono mantenute sull&#39;interfaccia utente (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* I seguenti miglioramenti sono stati apportati all’accessibilità in [!DNL Dynamic Media] (CQ-4290306). Per informazioni dettagliate, consulta [funzioni di accessibilità in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * Gli assistenti vocali (JAWS, Assistente vocale) indicano il nome, il ruolo e lo stato delle voci di menu nell’opzione di menu Incorpora dimensioni (CQ-4290927).
   * Gli utenti possono navigare nella finestra di dialogo Collegamento e-mail utilizzando la chiave `Tab` (CQ-4290926).
   * Il flusso di lavoro per la creazione di profili di codifica video è più semplice da usare in considerazione del miglioramento dell’assistente vocale (CQ-4290623, CQ-4290622).
   * Quando si naviga utilizzando il tasto `Tab`, lo stato attivo si sposta sugli elementi dell&#39;interfaccia utente appropriati nel flusso di lavoro per creare un video interattivo (CQ-4290621, CQ-4290620, CQ-4290619).
   * Le pagine Pubblica , Modifica risorsa , Modifica ritaglio avanzato e Editor set di immagini sono state migliorate per conformarsi agli standard web. Gli utenti della tecnologia di assistenza (AT) ora possono navigare facilmente in queste pagine e intraprendere azioni come le immagini di ritaglio (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-42990 610, CQ-4290614).
   * I visualizzatori sono stati migliorati per consentire agli utenti di navigare utilizzando una tastiera (CQ-4290615).
   * Gli utenti di tastiera e assistenti vocali possono utilizzare la funzionalità di ritaglio (CQ-4290609).
   * Gli utenti di tastiera possono gestire meglio gli hotspot (CQ-4290604, CQ-4290603).

* I set di immagini remoti non sono modificabili in [!DNL Experience Manager] se il nome dell&#39;azienda e quello della cartella sono gli stessi (NPR-31340).

* L&#39;ordine dell&#39;indice z non è corretto quando si tenta di visualizzare l&#39;anteprima dell&#39;output dopo l&#39;aggiunta di un punto attivo a un&#39;immagine [!DNL Dynamic Media] o dopo la modifica di un video [!DNL Dynamic Media] o di un [!DNL Experience Fragment] con un&#39;immagine (CQ-4307267).

* [!DNL Dynamic Media] La sincronizzazione non riesce quando i set di file multimediali diversi vengono rielaborati (CQ-4307184).

* Se una risorsa viene spostata in una cartella in cui è configurata la sincronizzazione automatica con [!DNL Dynamic Media], la risorsa non viene sincronizzata (CQ-4307122).

* [!DNL Dynamic Media] video non riprodotto su dispositivi iOS con i controlli video HTML5 nativi (CQ-4306977, CQ-4306727).

* Non è possibile scaricare immagini in cui è applicato SmartCrop (CQ-4304558).

* Non è possibile pubblicare le cartelle in modo selettivo in Dynamic Media (CQ-4304526).

* L’annullamento della pubblicazione di un file video da [!DNL Experience Manager] non annulla la pubblicazione del set video adattivo da una distribuzione Scene7 configurata (CQ-4304405).

* L’aggiunta di una risorsa immagine panoramica in un componente multimediale panoramico e l’aggiornamento della pagina generano un errore `Uncaught ReferenceError: $ is not defined` (CQ-4302810).

* Nel [!UICONTROL Editor predefiniti visualizzatore], quando si modifica il predefinito [!UICONTROL PanoramicImage/PanoramicImage_VR], nel componente `PanoramicView` l&#39;etichetta del modificatore `PANORAMICVIEW_AUTOROTATE` non è disponibile (CQ-4302443).

* I sottotitoli video non vengono visualizzati se il video non è il primo in un MixedMediaSet (CQ-4298161).

* Il visualizzatore HTML5 per eCatalog su dispositivi mobili iPhone non può girare le pagine o capovolgere le pagine (CQ-4296611).

* Quando si scorrono i campioni su un dispositivo mobile, per alcuni secondi i campioni scorrono a destra e all’esterno dell’area visibile, quindi tornano a essere visualizzati (CQ-4296439).

* Quando si crea un record master predefinito per visualizzatori, i CSS e le immagini non vengono pubblicati e viene pubblicato solo il predefinito per visualizzatori (CQ-4262205).

* Quando tenti di collegare un frammento esperienza per un determinato punto attivo nel componente [!UICONTROL Video/immagini interattive], non mostra il percorso del frammento esperienza selezionato. Al contrario, restituisce un valore vuoto dal campo percorso (NPR-35146, CQ-4298136).

* Impossibile visualizzare in anteprima un frammento esperienza in IVV Editor (CQ-4308560).

* Quando aggiungi un punto attivo a un’immagine e selezioni un frammento esperienza, non è possibile selezionare le sottocartelle e le varianti del frammento esperienza (CQ-4307455).

* Le risorse non immagine non vengono visualizzate come pubblicate dopo il caricamento (CQ-4306415).

#### [!DNL Experience Manager] Risorse 3D {#three-d-assets-6570}

* `DAM CQ MIME Type` Il servizio applica tipi MIME non corretti alle risorse 3D, generando un rendering non corretto (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* L’interfaccia utente per la raccolta dei prodotti Commerce non elenca più di 15 prodotti all’interno di una raccolta (NPR-34502).

### Piattaforma {#platform-6570}

* Una sessione HTTP su HTTPS non viene invalidata (NPR-35083).
* Viene restituito un `NullPointerException` quando si avviano attività di manutenzione giornaliere o settimanali dall’interfaccia utente (NPR-34953).
* La funzione di convalida W3C segnala gli avvisi relativi ai file JavaScript della libreria client conformi (NPR-34898).
* La funzione `AudienceOmniSearchHandler` utilizza un indice obsoleto (NPR-34870).
* La disconnessione da Experience Manager non cancella i cookie (NPR-34743).
* La funzione `findByTitle` dell’ API `TagManager` non funziona se il nome del tag contiene un carattere speciale (NPR-34357).
* Il processo di importazione del pacchetto di sincronizzazione utente non riesce (NPR-34399).
* È stato aggiunto il supporto per le proprietà `ariaLabel` e `ariaLabelledby` al componente `Coral.Masonry` (GRANITE-29962).
* La cache del dispatcher non viene aggiornata per le pagine con frammenti di contenuto dopo l’installazione dei pacchetti componenti core più recenti (CQ-4306788).
* I nomi dei tag localizzati con virgolette (`"`) non vengono visualizzati correttamente nell’interfaccia utente (CQ-4305439).

### Interfaccia utente {#ui-6570}

* Il campo [!UICONTROL Collega a] nelle proprietà del componente visualizza suggerimenti di completamento automatico che non corrispondono alla stringa specificata (NPR-34865).

* AEM il seguente messaggio di errore quando si pianifica una finestra di manutenzione giornaliera distribuita tra 2 giorni (NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integrations (Integrazioni) {#integrations-6570}

* La modifica di una configurazione [!DNL Adobe Launch] esistente non riesce (NPR-35045).
* Non è possibile esportare [!DNL Experience Fragments] in [!DNL Adobe Target] se si utilizza la configurazione IMS e l’ambiente [!DNL Adobe Target Standard] (NPR-34555).
* L&#39;opzione [!UICONTROL Crea] viene visualizzata nella pagina [!UICONTROL Tipi di pubblico] quando si passa da una cartella alla pagina [!UICONTROL Tipi di pubblico] (NPR-35151).

### Sling {#sling-6570}

* Il controllo di integrità dell&#39;accesso predefinito convalida le credenziali di un utente che non esiste (NPR-34686).

### Progetti di traduzione {#translation-6570}

* Quando si annulla un progetto di traduzione in [!DNL Experience Manager], la richiesta di annullamento non viene inviata al provider di traduzione (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Tutti i casi di terminologia iniqua nel prodotto sono sostituiti con equivalenti accettati (NPR-34311).
* [!DNL Google+] viene rimosso dall&#39;elenco delle opzioni di condivisione social network (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* L&#39;interfaccia utente non risponde selezionando le risorse nella [!UICONTROL Vista a elenco] (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>Per [!DNL Experience Manager Forms] vengono rilasciati pacchetti del componente aggiuntivo una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per  [!DNL Forms]. Vengono distribuite utilizzando un pacchetto aggiuntivo [!DNL Forms] separato. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per [!DNL Experience Manager Forms] su JEE. Per ulteriori informazioni, consulta [Installare il componente aggiuntivo AEM Forms](#install-aem-forms-add-on-package) e [Installare AEM Forms su JEE](#install-aem-forms-jee-installer).

**Moduli adattivi**

* Impossibile modificare un modulo adattivo utilizzando l’interfaccia classica dopo l’applicazione di [!DNL Experience Manager] Service Pack 6 (NPR-35126).

* Quando si converte un PDF in un modulo adattivo, non è possibile impostare un valore per un pannello nidificato utilizzando un modello dati modulo nel layout a schede. Inoltre, si verificano problemi durante l&#39;impostazione dinamica di un valore per i gruppi di pulsanti di scelta con un array statico che utilizza l&#39;editor di codice (NPR-35062).

* Quando immetti caratteri giapponesi in un componente campo di testo in un modulo adattivo, puoi specificare più caratteri del limite massimo di 35 caratteri (NPR-35039).

* Il modulo adattivo visualizza i parametri indesiderati, ad esempio `owner` e `status`, nella pagina **[!UICONTROL Grazie]** visualizzata dopo l’invio del modulo (NPR-34989).

* La finestra di dialogo [!UICONTROL Selezione file] per il componente [!UICONTROL Allegato] visualizza i tipi di file non supportati e la selezione, dando luogo a un errore durante l’invio del modulo adattivo (NPR-34970).

* Quando si inserisce un modulo adattivo in una pagina [!DNL Experience Manager Sites] contenente testo precedente al modulo, lo stato attivo del cursore si sposta direttamente nel modulo anziché nel testo precedente al modulo (NPR-34947).

* [!UICONTROL L&#39;opzione Anteprima con ] dati per precompilare un modulo adattivo utilizzando un file XML di dati  [!DNL Experience Manager] 6.2 non funziona correttamente (NPR-35087).

* Quando si aggiorna il dizionario dati per un modulo adattivo, il modulo non viene tradotto in quanto il modulo adattivo restituisce i valori memorizzati nella cache (NPR-34845).

* Il caricamento dei frammenti in un modulo adattivo richiede più tempo a causa dell’annullamento della validità della cache (NPR-34567).

* La navigazione a schede non funziona correttamente per gli assistenti vocali in un modulo adattivo (NPR-34544).

**Gestione della corrispondenza**

* Impossibile salvare i valori per i tag XML con dati numerici, che includono il tipo mobile, come bozza (NPR-35050).

* Quando esegui la migrazione delle risorse da ES3, le risorse includono due condizioni predefinite non modificabili (NPR-34972).

* Quando modifichi un dizionario dati in una lettera, nella sezione [!UICONTROL Contenuto prestato] vengono visualizzati rettangoli girevoli anziché informazioni utili (NPR-34853).

**Comunicazione interattiva**

* Il nome della configurazione di rollout per la comunicazione interattiva, disponibile dopo l’installazione del pacchetto aggiuntivo [!DNL Forms], duplica il nome della configurazione di rollout standard (NPR-34976).

**Sicurezza dei documenti**

* Quando salvi un nuovo criterio di protezione dei documenti, Experience Manager Forms visualizza il messaggio di errore `Relative validity period is required` (NPR-34679).

* Document Security non è in grado di proteggere il documento PDF 2.0 (CQ-4305851).

Per informazioni sugli aggiornamenti di sicurezza, vedere [pagina dei bollettini sulla sicurezza degli Experienci Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.6.0 {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0 è un aggiornamento importante che include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti successivamente alla versione 6.5 di **aprile 2019**. Può essere installato su Adobe Experience Manager 6.5.

Le funzioni chiave e i miglioramenti introdotti in Adobe Experience Manager 6.5.6.0 includono:

* Puoi pubblicare o annullare selettivamente la pubblicazione delle risorse su [!DNL Experience Manager] o [!DNL Dynamic Media] utilizzando la procedura guidata [!UICONTROL Pubblicazione rapida] o [!UICONTROL Gestisci pubblicazione].

* Utilizza l’ interfaccia utente [!DNL Dynamic Media] per annullare la validità del contenuto nella cache CDN (Content Delivery Network).

* La pubblicazione delle cartelle dei contributi delle risorse da Brand Portal ad Experience Manager Assets è ora supportata anche tramite il server proxy.

* I gruppi generati automaticamente della cartella privata vengono ora eliminati al momento dell&#39;eliminazione della cartella privata in [!DNL Experience Manager Assets].

* Le descrizioni dei modificatori nel video [!UICONTROL Viewer] predefinito editor sono state aggiornate in [!DNL Dynamic Media].

* Viene fornita una nuova impostazione aziendale per riflettere lo stato del connettore [!DNL Dynamic Media].

* Le opzioni predefinite per `test` e `aiprocess` vengono aggiornate a `Thumbnail`, da `Rasterize` in precedenza in Dynamic Media, per garantire che gli utenti debbano creare solo miniature e ignorare l’estrazione della pagina e delle parole chiave.

* [Precompila un modulo adattivo sul client](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [Integrazione del modello dati del modulo con API RESTful su un server con implementazione](../../help/forms/using/configure-data-sources.md) SSL bidirezionale.

* [Memorizzazione in cache migliorata per le pagine](../../help/forms/using/configure-adaptive-forms-cache.md) dei moduli adattivi tradotte.

* Supporto per [Tag testo Adobe Sign nel servizio Automated forms conversion](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* Supporto per [convertire i moduli colorati in moduli adattivi](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) utilizzando [!DNL Automated Forms Conversion service].

* Supporto per i protocolli SMB 2 e SMB 3.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.4.

Per un elenco completo delle funzioni e dei miglioramenti introdotti all’Experience Manager 6.5.6.0, consulta [Novità di Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md).

Di seguito è riportato l&#39;elenco delle correzioni apportate in [!DNL Experience Manager] 6.5.6.0.

### [!DNL Sites] {#sites-6560}

* In [!DNL Sites] o [!DNL Screens], seleziona un progetto e fai clic su [!UICONTROL Pubblicazioni di gestione]. Gli utenti non possono avanzare nella procedura guidata [!UICONTROL Gestisci pubblicazione] a causa di errori nell&#39;interfaccia utente. In particolare, l&#39;opzione [!UICONTROL Pubblica] non funziona (NPR-34099).
* La posizione di iParsys (Sistema paragrafo ereditato) non viene ripristinata nella posizione predefinita originale dopo aver deselezionato le opzioni [!UICONTROL Annulla ereditarietà] o [!UICONTROL Disattiva ereditarietà] (NPR-34097).
* Se il `RolloutConfigManagerFactoryImpl` non è in grado di caricare una configurazione di rollout, non tenta di caricare le configurazioni mancanti. Restituisce le configurazioni memorizzate nella cache (NPR-34092).
* Nel componente di base Testo, dopo aver utilizzato l’opzione di modifica HTML di origine, la classe dal tag `em` viene rimossa (NPR-34081).
* Dopo l’aggiornamento da Experience Manager 6.3.3 a Experience Manager 6.5.3, il processo di rollout richiede molto più tempo e il rollout non riesce con un errore di timeout (NPR-34049).
* Il `htmlwriter` non codifica i valori degli attributi. Il markup presente nel markup XF viene esportato con valori di attributo decodificati (ovvero `"` anziché `&#34`). Causa problemi sul lato Target con Visual Experience Composer che utilizza il XF esportato (NPR-34048).
* Durante lo spostamento delle pagine in [!DNL Experience Manager Sites], aumenta la registrazione per acquisire l’errore di creazione della versione con un motivo (NPR-34014).
* In [!DNL Rich Text Editor] se viene rimosso tutto il testo, viene rimosso anche il tag paragrafo (NPR-33976).
* Quando la pagina `siteadmin` (nell’interfaccia classica) viene aperta o aggiornata, le opzioni nel menu `New` vengono disattivate (NPR-33949).

   ![Schermata per illustrare il problema del menu mancante nell’interfaccia classica](assets/33949_missing_menu.png)

* Un [!DNL Content Fragment] non può essere utilizzato come `TemplatedResource` in quanto non riesce in `ContentFragmentUsePojo` (NPR-33911).
* Le operazioni di spostamento sincrone e asincrono possono causare errori a causa di trasferimenti simultanei. Le operazioni di spostamento delle pagine sono limitate solo allo spostamento asincrono. Impedisce lo spostamento simultaneo di pagine (NPR-33875).
* [!UICONTROL L’operazione Gestisci ] pubblicazione per replicare il contenuto dall’istanza Autore a Pubblica non riesce e genera un errore JavaScript (NPR-33872).
* Quando selezioni più pagine o risorse per creare versioni, la nuova versione viene creata solo per l’ultima pagina o risorsa selezionata (NPR-33866).
* Sposta una pagina blueprint con Live Copy in un’altra cartella. Quando lo si sposta nella cartella originale, l&#39;operazione di spostamento non riesce senza alcun errore (NPR-33864).
* Quando si utilizza un’azione Sposta per rinominare una pagina web nella console [!DNL Sites] , vengono visualizzate due finestre di dialogo sovrapposte all’ultimo passaggio della procedura guidata (NPR-33831).

   ![Schermata per illustrare il problema NPR-33831 della sovrapposizione della finestra di dialogo di spostamento](assets/33831_rename_dialog.png)

* Le proprietà `cq:acLinks` e `cq:acUUID` per [!DNL Adobe Campaign] nella copia vengono rimosse durante l&#39;operazione di copia e incolla (NPR-33794).
* Quando si tenta di eseguire il rollout su una pagina figlia di una Live Copy padre staccata, [!DNL Experience Manager] genera un&#39;eccezione Null Pointer (NPR-33676).
* I componenti [!DNL RTE] in un contenitore di layout non sono visibili quando il contenitore di layout viene copiato e incollato nuovamente sulla pagina. I componenti [!DNL RTE] non sono modificabili, ma vengono visualizzati all’aggiornamento della pagina (NPR-33662).
* Quando si ridimensiona un componente layout per diversi punti di interruzione (medio e grande), il layout non si comporta come previsto (NPR-33608).
* In modalità di modifica in linea in [!DNL RTE], il trascinamento di un’immagine non funziona per il componente Testo (NPR-33602).
* È possibile creare un componente in una pagina blueprint con lo stesso nome della pagina. Durante il rollout, `_msm_moved` viene aggiunto un suffisso per rinominare il componente. Il componente viene spostato alla fine del [!UICONTROL Sistema paragrafo] (NPR-33535).
* Quando offTime o onTime è impostato su molte pagine o risorse, è ad alta intensità di risorse e rallenta il sistema durante l&#39;avvio e lo spegnimento (NPR-33482).
* Un utente con autorizzazioni CRUD su `/content/experience-fragment` non è in grado di eliminare una cartella (NPR-33436).
* Puoi selezionare [!UICONTROL HTML e JSON] come opzione per [!UICONTROL Adobe Target export format] su una cartella principale nella sezione [!DNL Experience Fragments]. Le stesse proprietà vengono visualizzate nell&#39;interfaccia touch per le sottocartelle di questa cartella principale. Tuttavia, in CRXDE, per `cq:adobeTargetExportFormat` viene visualizzato solo HTML anziché `html,json` (NPR-33423).
* La pubblicazione o l’annullamento della pubblicazione da un alias di pagina non è supportata. Rimuovere l&#39;opzione che sembra richiedere diversamente (NPR-33415).
* Un tag specifico può essere spostato da una posizione all’altra in [!DNL Experience Manager]. Può essere applicato anche a pagine diverse prima e dopo lo spostamento. Durante la modifica delle proprietà delle pagine, il tag non viene visualizzato per la modifica, anche se il tag è lo stesso (NPR-33353).
* Un modello di pagina non viene riprodotto correttamente quando un contenitore di layout viene eliminato da un modello che contiene più contenitori di layout (NPR-33347).
* Nell’editor modelli, prova a eliminare un modello utilizzato da più di 100000 pagine in `/content/`. Viene visualizzato un errore senza alcun messaggio di errore (NPR-33312).
* Il reindirizzamento alla pagina [!DNL Experience Manager] con ancoraggio non funziona sull&#39;istanza di authoring perché `PageRedirectServlets` inserisce la stringa di query dopo un frammento URL o un ancoraggio (NPR-34288).
* La creazione di un marchio in `/content/campaign` genera una struttura che non consente di creare campagne. [!UICONTROL Crea ] ramo lascia il marchio appena creato senza la possibilità di creare  [!UICONTROL offerte e ] attività, in quanto non esiste un’  opzione di creazione (NPR-34113).
* Puoi sospendere la sezione [!DNL Live Copy] di una pagina e l’ereditarietà viene interrotta come mostrato nella modalità Editor. Nelle proprietà della pagina, l’icona che rappresenta l’ereditarietà indica in modo errato che l’ereditarietà esiste e non è interrotta (NPR-34017).
* Le pagine con molti riferimenti non possono essere spostate in modo asincrono e talvolta l&#39;operazione di spostamento non riesce (CQ-4297969).
* Una pagina web con il carattere `/` nell’URL non risponde durante l’authoring. Quando viene aggiunto un componente durante l&#39;authoring, l&#39;utilizzo della CPU aumenta e il browser smette di rispondere (CQ-4295749).
* In modalità Sfoglia, NVDA non legge un valore selezionato dall&#39;opzione di menu Tipo/Dimensione. L’elemento visivo non è attivo sull’elemento selezionato. L&#39;utente che si basa su un assistente vocale non può utilizzare la modalità Sfoglia (CQ-4294993).
* Quando crei una pagina web, gli utenti possono selezionare il modello [!UICONTROL Pagina di contenuto] . Nella scheda [!UICONTROL Social Media], gli utenti selezionano una [!UICONTROL variante XF preferita]. Per selezionare un frammento esperienza in modalità Sfoglia di NVDA, gli utenti non possono utilizzare i tasti di scelta rapida (CQ-4292669).
* Aggiornamento della libreria handlebars alla versione v4.7.3 più sicura (NPR-34484).
* Più istanze di scripting tra siti nei componenti [!DNL Experience Manager Sites] (NPR-33925).
* Il campo del nome della cartella durante la creazione di una nuova cartella è vulnerabile alla memorizzazione di script tra siti diversi (GRANITE-30094).
* I risultati della ricerca nella pagina[!UICONTROL  Benvenuti] e nel modello di completamento del percorso sono vulnerabili agli script tra siti diversi (NPR-33719, NPR-33718).
* La creazione di una proprietà binaria su un nodo non strutturato determina l&#39;uso di script tra siti nella finestra di dialogo delle proprietà binarie (NPR-33717).
* Vulnerabilità cross-site scripting quando si utilizza l&#39;opzione [!UICONTROL Test di controllo accessi] sull&#39;interfaccia CRX DE (NPR-33716).
* Gli input degli utenti non vengono codificati in modo appropriato per vari componenti quando si inviano informazioni al client (NPR-33695).
* Vulnerabilità cross-site scripting nella vista Calendario, ad Experience Manager Inbox (NPR-33545).
* Un URL che termina con `childrenlist.html` visualizza una pagina HTML invece di una risposta 404. Tali URL sono vulnerabili agli script tra siti diversi (NPR-33441).


### [!DNL Assets] {#assets-6560}

**Miglioramenti all’accessibilità in Experience Manager Assets**

* Utilizzando i tasti di tastiera, gli utenti possono ora accedere alle opzioni dell’interfaccia utente interattiva nell’elenco [!UICONTROL Riferimenti] delle risorse (NPR-34115).

* L’assistente vocale ora annuncia l’azione prevista dei predicati nella pagina di ricerca (NPR-34104).

* La pagina di ricerca e la pagina dei risultati di ricerca ora dispongono di titoli più informativi per una migliore comprensione degli utenti di assistenti vocali (NPR-34093).

* Gli assistenti vocali ora annunciano le opzioni per eliminare i tag selezionati nella scheda [!UICONTROL Base] della pagina della risorsa [!UICONTROL Proprietà] (NPR-33972).

* Gli elementi di ogni riga nella vista a elenco vengono ora annunciati come elementi della stessa riga dagli assistenti vocali (NPR-33932).

* Lo stato attivo durante la navigazione con il tasto `Tab` ora si sposta sull’opzione di chiusura nell’anteprima della versione (NPR-33863).

* Lo stato attivo dell’utente ora si sposta sull’icona di ricerca dopo la chiusura di Omnisearch (NPR-33705).

* Le opzioni dell’interfaccia utente utilizzabili ora sono più visibili e presentano un contrasto maggiore quando si passa da una tastiera all’altra. Gli utenti che utilizzano la tastiera possono identificare le aree interessate (NPR-33542).

* La funzionalità di trascinamento tramite tastiera ora funziona in [!UICONTROL Editor schema metadati] in modalità Sfoglia dell’assistente vocale (CQ-4296326).

* Nella finestra di dialogo di condivisione dei collegamenti, quando si naviga in modalità Sfoglia, un assistente vocale,

   * Non legge le informazioni della tabella non appena viene caricata la finestra di dialogo.

   * Puoi passare a tutti i suggerimenti automatici elencati.

   * Narra i suggerimenti automatici visualizzati per [!UICONTROL Aggiungi indirizzo e-mail/Ricerca] (CQ-4294232).

* L&#39;utilizzo del tasto `Esc` per rimuovere le icone delle azioni rapide dalla vista a schede non rimuove più lo stato attivo dall&#39;ultimo elemento attivo (CQ-4293554).

* Per le opzioni interattive nell’interfaccia utente, l’assistente vocale legge ora il loro scopo anziché i nomi letterali delle icone (CQ-4272943).

* Lo stato attivo della tastiera ora si sposta correttamente su [!UICONTROL Flyout], [!UICONTROL InlineZoom], [!UICONTROL Shoppable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL ZoomVertical_dark&lt;a1 opzioni/> e [!UICONTROL ZoomVertical_light] durante la navigazione tramite il tasto Tab della tastiera nei dettagli delle risorse [!UICONTROL Visualizzatori] in [!DNL Dynamic Media] (CQ-4290605).]

* [!UICONTROL È ora possibile accedere all’opzione Salva e ] chiudi   nella pagina Proprietà delle risorse utilizzando i tasti di scelta rapida (NPR-34107).

* I messaggi di errore dovuti a combinazioni errate di nome utente e password nella pagina di accesso vengono ora annunciati dagli assistenti vocali ogni volta che si verifica l’errore (NPR-33722).

* Nella sezione di intestazione [!DNL Experience Manager], quando si naviga in modalità Sfoglia, l’assistente vocale annuncia ora:

   * Suggerimenti modificati automaticamente in [!UICONTROL Digitare per cercare] in Omnisearch.

   * Lo stato viene espanso o compresso per le opzioni [!UICONTROL Soluzioni], [!UICONTROL Aiuto], [!UICONTROL Casella in entrata] e [!UICONTROL Utente].

   * Il messaggio di stato [!UICONTROL Ricerca nella Guida] visualizzato quando l&#39;utente immette una stringa di ricerca nel campo [!UICONTROL Ricerca nella Guida] sotto l&#39;opzione [!UICONTROL Aiuto].

   ![Menu Aiuto nell&#39;intestazione](assets/Help_aem_header.png)

   *Figura:  [!UICONTROL Cerca ] Helpmenu   Helpmenu.*

   * Il messaggio di errore se il valore immesso non è corretto nel campo [!UICONTROL Impersona come] sotto l&#39;opzione [!UICONTROL Utente] e lo stato attivo si sposta correttamente nel campo di testo (NPR-33804).

   ![Menu utente nell’intestazione](assets/User_aem_header.png)

   *Figura:  [!UICONTROL Impersona ] un campo nel menu   utente nell’intestazione.*

* È ora possibile modificare lo stato attivo utilizzando la tastiera all’interno di:

   * [!UICONTROL Cerca/Aggiungi ] indirizzo e-mail nella finestra di dialogo  [!UICONTROL Condivisione collegamenti ] .

   * [!UICONTROL Aggiungi un campo Utente o ] Gruppo in  [!UICONTROL Gruppo utenti chiuso nella ] scheda Autorizzazioni   Proprietà   cartella (NPR-34452).

**Problemi risolti in Experience Manager Assets**

[!DNL Adobe Experience Manager] La versione 6.5.6.0  [!DNL Assets] fornisce correzioni ai seguenti problemi:

* Le annotazioni non vengono evidenziate quando selezionate dalla timeline della risorsa (CQ-4302422).

* L&#39;anteprima delle risorse collaterali di marketing (come brochure, volantino e biglietto da visita) create utilizzando il modello [!DNL Adobe InDesign] non visualizza le interruzioni di riga e di paragrafo (NPR-34268).

* L’estrazione del testo e quindi la ricerca full-text per i file PDF caricati non funziona (NPR-34164). Per risolvere il problema, riavviare la distribuzione [!DNL sAdobe Experience Manager] dopo aver installato Service Pack 6.

* La Timeline delle risorse multipagina mostra le annotazioni applicate a tutte le risorse secondarie quando esplori la risorsa nella vista Timeline, invece di visualizzare le annotazioni specifiche per le risorse secondarie specifiche (NPR-34100).

* Le cartelle di risorse non vengono pubblicate utilizzando l’opzione [!UICONTROL Gestisci pubblicazione] se le cartelle contengono risorse in formati di file JavaScript, CSS o JSON (NPR-34090).

* Deselezionando o rimuovendo i tag o i filtri applicati in Omnisearch la query di ricerca viene eseguita più volte, il che porta ad un aumento del tempo di ricerca (NPR-34078).

* Nella vista a schede quando un flusso di lavoro (su una risorsa in una cartella) è in corso o in sospeso, la pagina viene ricaricata fino al completamento o alla fine del flusso di lavoro. Pertanto, gli autori non possono lavorare su quelle risorse nella cartella per la quale devono scorrere verso il basso (NPR-33986).

* Se l&#39;utente sposta una risorsa pubblicata in una nuova posizione, la risorsa viene ripubblicata anche se l&#39;opzione [!UICONTROL Ripubblica] è deselezionata. Questo porta a molte risorse orfane sdraiate sull’istanza di pubblicazione. Il comportamento predefinito, tuttavia, consiste nel fatto che l’operazione di spostamento su una risorsa pubblicata la annulla automaticamente; questa risorsa viene ripubblicata se l’autore seleziona l’opzione [!UICONTROL Ripubblica] quando sposta la risorsa (NPR-33934).

* La pagina [!UICONTROL Sposta risorse] per le risorse nelle raccolte non carica tutti i contenuti HTML, ad esempio l&#39;opzione [!UICONTROL Regola/Ripubblica]. Pertanto, gli utenti non possono completare l’operazione di spostamento (NPR-33860).

* Lo spostamento di una risorsa e l’aggiunta di caratteri speciali nel nome e nel titolo delle risorse spostate crea una cartella aggiuntiva (con lo stesso nome) nella nuova posizione della risorsa (NPR-33826).

*  Il pulsante Scarica per una risorsa viene disattivato quando l’opzione   E-mail è selezionata nella finestra di dialogo   Download (NPR-33730).

* Si osserva l’errore &quot;Request-URI too long&quot; (URI di richiesta troppo lungo) durante l’esecuzione di operazioni in blocco sulle risorse, come la modifica in serie dei metadati (NPR-33723).

* Si osserva un errore JavaScript e gli utenti non possono selezionare o eliminare le scelte generate nel campo [!UICONTROL a discesa] da [!UICONTROL Aggiungi tramite percorso JSON] nella funzionalità [!UICONTROL Folder Metadata Schema Form Editor], se il file JSON caricato ha spazio o caratteri speciali nel valore (NPR-33712).

* Le rappresentazioni statiche delle risorse non vengono aggiornate quando la risorsa viene aggiornata tramite l’opzione [!UICONTROL Apri] in [!DNL desktop app] o [!DNL Adobe Asset Link] e vengono sincronizzate di nuovo in [!DNL Adobe Experience Manager] (CQ-4296279).

* Nella vista a colonne l’operazione Sposta su un set di risorse sposta anche le risorse selezionate prima di utilizzare l’opzione [!UICONTROL Filtro]. L&#39;utilizzo dell&#39;opzione [!UICONTROL Filtro] deseleziona la selezione precedente (NPR-34018).

* Le barre rovesciate vengono aggiunte prima dei caratteri speciali nei suggerimenti di ricerca delle risorse, che hanno caratteri speciali nel loro nome (NPR-33834).

* Quando si creano regole per l&#39;elenco a discesa in [!UICONTROL Modulo schema metadati cartelle], l&#39;utente non può selezionare valori dalla colonna [!UICONTROL Scelte campi] (CQ-4297530).

* La copia in fase di esecuzione del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata quando si installa [!DNL Experience Manager] 6.5 Service Pack 5 o una versione precedente su [!DNL Experience Manager] 6.5 (NPR-34532). Per recuperare la copia in fase di esecuzione, sincronizza la copia in fase di progettazione del modello di flusso di lavoro con la copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

**Problemi risolti in Dynamic Media**

* Se l’utente definisce le impostazioni di codifica nelle modifiche dopo aver creato il profilo video, le impostazioni di ritaglio avanzato vengono rimosse dai profili video (CQ-4299177).

* Le risorse vengono visualizzate momentaneamente al caricamento della pagina quando l’utente passa da un’opzione all’altra della barra laterale (ad esempio, [!UICONTROL Panoramica], [!UICONTROL Timeline], [!UICONTROL Visualizzatori]) nella pagina dei dettagli delle risorse (NPR-34235).

* I seguenti problemi vengono osservati con il processo di rielaborazione:

   * ID processo mancante nell&#39;handle di processo restituito dal processo di rielaborazione.

   * Rielabora il processo solo nome file dei log video e non percorso completo.

   * Il processo di rielaborazione non dispone dell&#39;opzione per impostare il tipo di risorsa come statico.

   * `ExcludeFromAVS` non è disponibile l&#39;opzione (CQ-4298401).

* La funzionalità Ritaglio avanzato non riesce e viene visualizzato un errore quando il profilo immagine viene aggiunto a una cartella con più rapporti di formato (ad esempio, 11) (NPR-34082).

* Il flusso di lavoro delle risorse di aggiornamento DAM viene attivato quando l’utente scorre verso il basso nella pagina [!UICONTROL Archivio flussi di lavoro] nella scheda [!UICONTROL Flusso di lavoro] all’interno di [!UICONTROL Strumenti] in [!DNL Adobe Experience Manager] configurata con Dynamic Media Scene7 (CQ-429727).

* I simboli nella scheda [!UICONTROL Comportamento] di [!UICONTROL Editor predefiniti visualizzatore] non sono localizzati (CQ-4299026).

* La vista principale visualizza l&#39;immagine in un layout non corretto che non si adatta al visualizzatore, se il visualizzatore è in modalità reattiva (CQ-4298293).

* Le modifiche ai predefiniti immagine in [!UICONTROL Adobe Experience Manager] non si sincronizzano con Scene7 Publishing System (CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* I collegamenti alle risorse dei prodotti non vengono reinseriti nel refactoring quando le risorse vengono spostate (NPR-34098).

### Piattaforma {#platform-6560}

* Impossibile scaricare i registri utilizzando lo strumento Diagnosi su un&#39;istanza aggiornata di Experience Manager (NPR-34336).
* L&#39;aggiornamento non riesce con un errore a causa delle dipendenze da una versione specifica del pacchetto di fondazione `cq-wcm-api` (CQ-4300520).
* I valori predefiniti per le impostazioni **[!UICONTROL Connect Timeout]** e **[!UICONTROL Socket Timeout]** per la configurazione Default Agent (publish) non sono specificati (NPR-33707).
* Gli aggiornamenti alla configurazione della mappatura in `/etc/map.publish` non si riflettono sulle pagine del sito (NPR-34015).
* [La ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) documentazione di riferimento API non include la documentazione per il  `com.day.cq.tagging` pacchetto (CQ-4295864).

### Interfaccia utente {#ui-6560}

* L&#39;interfaccia del browser di offload non visualizza tutti gli argomenti del processo (NPR-34308).
* L&#39;interfaccia [Browser configurazioni](/help/sites-administering/configurations.md) non visualizza tutte le configurazioni (NPR-33644).
* Premendo il tasto `Esc` durante la ricerca di utenti da impersonare, la finestra di dialogo **[!UICONTROL Utente]** si chiude invece dell&#39;elenco di utenti (NPR-34084).

### Integrations (Integrazioni) {#integrations-6560}

* Le attività con nomi lunghi non vengono sincronizzate con [!DNL Adobe Target] (NPR-34254).

* Quando si seleziona una proprietà durante la creazione di una nuova configurazione di Adobe Launch, viene visualizzato il seguente messaggio di errore (NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### Progetti traduzione {#translation-6560}

* Un progetto di traduzione non viene creato se l’ `authorizableID` dell’utente include caratteri speciali (NPR-33828).

### Sling {#sling-6560}

* La funzione Verifica stato e Rilevatore pattern hanno funzionalità sovrapposte. Di conseguenza, il controllo di integrità viene rimosso dal prodotto (NPR-33928).

### WCM {#wcm-6560}

* Componenti di base : quando aggiungi un componente immagine di base a una pagina e fai riferimento a un’immagine, l’operazione `Undo` non funziona (NPR-34516).

* Impossibile utilizzare l&#39;operazione Sposta pagina (CQ-4303028).

### [!DNL Communities] {#communities-6560}

* La condivisione di un post sui social media mostra un&#39;opzione obsoleta Google+ (NPR-33877).

* Il membro della community non è in grado di modificare il modello di gruppo o altre impostazioni della funzione di gruppo (NPR-33530).

* I tag dei collegamenti ipertestuali presenti sulle immagini non vengono generati correttamente in un post del forum (NPR-33464).

* Gli errori di accessibilità sono identificati nella funzione Assegnazione community (NPR-33442).

* Gli utenti esistenti di un gruppo community aggiunto tramite admin console vengono rimossi dall’elenco di utenti in caso di modifiche nella console dei gruppi della community (NPR-34315).

* Il `TagFilterServlet` perde dati potenzialmente sensibili (NPR-33868).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per  [!DNL Forms]. Vengono distribuite utilizzando un pacchetto aggiuntivo [!DNL Forms] separato. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per [!DNL Experience Manager Forms] su JEE. Per ulteriori informazioni, consulta [Installare il componente aggiuntivo AEM Forms](#install-aem-forms-add-on-package) e [Installare AEM Forms su JEE](#install-aem-forms-jee-installer).

Dopo aver installato il pacchetto aggiuntivo [!DNL Experience Manager Forms] 6.5.6.0:

* Interrompi l&#39;istanza [!DNL Experience Manager Forms].

* Elimina i file `bcpkix-1.51`, `bcmail-1.51` e `bcprov-1.51` JAR dalla directory `crx-repository\launchpad\ext`.

* Elimina la proprietà` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` dal file `sling.properties`.

* Riavvia l&#39;istanza [!DNL Experience Manager Forms].

**Moduli adattivi**

* In presenza di un frammento di modulo adattivo mancante, il modulo adattivo non viene riprodotto correttamente (NPR-34302).

* La descrizione del contenuto della Guida per i campi di un modulo adattivo visualizza un tag HTML paragrafo (NPR-34116).

* Quando si seleziona la proprietà **[!UICONTROL Rivalida sul server]** , il modulo adattivo non viene inviato (NPR-33876).

* L&#39;azione di invio **[!UICONTROL Invia all&#39;endpoint REST]** non funziona per un modulo adattivo (CQ-4299044).

* Accessibilità: Quando tenti di inviare un modulo adattivo senza caricare un allegato per un campo obbligatorio, lo stato attivo non si sposta automaticamente sul campo allegato (CQ-4298065).

* Quando si aggiungono righe a una tabella di un modulo adattivo, le opzioni **[!UICONTROL Aggiungi all&#39;inizio]** e **[!UICONTROL Aggiungi al fondo]** non visualizzano i risultati appropriati (CQ-4297511).

* Lo script [!UICONTROL Value Commit] viene attivato in modo errato, causando la perdita di dati in un modulo adattivo (CQ-4296874).

* Il selettore data non funziona correttamente per i moduli adattivi localizzati (NPR-34333).

* Se nel nome del file è presente un carattere di sottolineatura o uno spazio, non è possibile allegare il file a un modulo adattivo (CQ-4301001).

* Quando un pannello ripetibile nidificato ha più occorrenze del suo elemento padre, tutte le occorrenze di tale pannello ripetibile nidificato non vengono precompilate (NPR-33666).

* I moduli adattivi hanno alcuni risolutori di risorse aperte. Ciò comporta errori di invio. Il problema si verifica a intermittenza (CQ-4299407).

* Quando apri la configurazione del campo per la prima volta, l&#39;icona delle proprietà non viene visualizzata (CQ-4296284).

* Quando si invia un modulo adattivo, gli utenti possono modificare i metadati di invio, ad esempio `afPath`, `afSubmissionTime` e `signers`. Per risolvere il problema, i valori dei metadati vengono rimossi dai dati di invio del modulo sul lato client. Gli utenti possono utilizzare l&#39;oggetto `FormSubmitInfo` per recuperare questi valori dal server (NPR-33654).

* Gli input utente non vengono codificati in modo appropriato per i componenti [!DNL Forms] quando si inviano informazioni al client (NPR-33611).

**Flusso di lavoro**

* Quando un approvatore di un flusso di lavoro carica un allegato, questo viene rinominato in `undefined` (NPR-33699).

* [!DNL Experience Manager] L&#39;operazione di eliminazione del flusso di lavoro non riesce e visualizza il seguente messaggio di errore (NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] l&#39;app per  [!DNL Windows] smette di rispondere dopo l&#39;invio di un modulo (NPR-34409).

* Quando si installa AEM Service Pack, l&#39;elenco **Da fare** degli elementi non viene visualizzato come collegamenti. Il testo per gli elementi **Da fare** include i tag HTML (NPR-34317).

**Comunicazione interattiva**

* Quando si include un frammento di documento di testo con componenti ripetibili nidificati, la comunicazione interattiva non viene salvata (NPR-34095).

**Gestione della corrispondenza**

* Quando si modifica un frammento di documento di testo che include i valori del dizionario dati, l&#39;interfaccia utente dell&#39;agente smette di rispondere (NPR-33930).

* Se si copia e incolla il contenuto da un documento [!DNL Microsoft Word] a un frammento di documento di testo in una lettera, si verificano problemi di formattazione (NPR-33536).

**Servizi documentali**

* Quando si genera un file PDF da un file XDP utilizzando i servizi Output e Forms, il testo risulta mancante e sovrapposto (NPR-34237, CQ-4299331).

* Quando si converte un file HTML in PDF, l&#39;attributo `MaxReuseCount` non è configurabile (NPR-33470).

* Quando si scarica un file PDF che include funzioni interattive Estensioni di Reader, non è possibile aggiungere un allegato al file PDF utilizzando [!DNL Adobe Reader] (NPR-33729).

**Sicurezza dei documenti**

* Impossibile eseguire l&#39;operazione Sign con certificati basati su HSM in un file PDF dopo l&#39;installazione di [!DNL Experience Manager] Service Pack (NPR-34310).

**Designer**

* Impossibile aprire XForms in Designer versione 6.5.x (CQ-4295322).

* Quando si apre Designer, nella schermata introduttiva viene visualizzato un anno non corretto (CQ-4295289).

* Quando installi [!DNL Acrobat DC] sul server, l&#39;opzione **[!UICONTROL Distribuisci modulo]** è inattiva (CQ-4296304).

Per informazioni sugli aggiornamenti di sicurezza, vedere [pagina dei bollettini sulla sicurezza degli Experienci Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0 è un aggiornamento importante che include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti successivamente alla versione 6.5 di **aprile 2019**. Può essere installato su Adobe Experience Manager 6.5.

Alcune funzioni chiave e miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.5.0 includono:

* Accesso anonimo ad CRXDE Lite non consentito. Gli utenti vengono invece indirizzati alla schermata di accesso. Vedere [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Personalizza i nomi delle colonne visualizzati nella casella in entrata [!DNL Adobe Experience Manager].

* Miglioramento dell’accessibilità in varie aree di Experience Manager Web Content Management (WCM) come Editor pagina, Componenti core, Editor Rich Text e Interfaccia utente amministratore.

* Salva un elemento [!DNL Interactive Communication] come bozza.

* Supporto per [!DNL Oracle WebLogic 12] ad Experience Manager Forms su JEE.

* È stata migliorata la gestione delle eccezioni nel flusso dell&#39;interfaccia utente [!DNL Adobe Experience Manager Assets] .

* Per ottenere l’URL di pubblicazione per Dynamic Media Scene7, viene aggiunto un nuovo metodo `getRemoteAssetPublishURL` all’interfaccia `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` .

* [Miglioramenti ](#assets-6550) all’accessibilità  [!DNL Adobe Experience Manager Assets] in conformità alle linee guida per l’accessibilità dei contenuti web (WCAG, Web Content Accessibility Guidelines).

* Integrazione di Package Share rimossa da Adobe Experience Manager.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.3.

Per un elenco completo delle funzioni, degli elementi di rilievo e delle funzioni chiave introdotte in Experience Manager 6.5 Service Pack 5, consulta [Novità di Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Di seguito è riportato l&#39;elenco delle correzioni apportate in [!DNL Experience Manager] 6.5.5.0 .

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites offre un’opzione per pubblicare o annullare la pubblicazione di una pagina dal relativo alias. L&#39;opzione non funziona (NPR-33415).
* Quando un contenitore di layout viene eliminato da un modello contenente più modelli, il modello non viene riprodotto correttamente (NPR-33347).
* Quando una pagina di Experience Manager Sites fa parte di un set di contenuti di grandi dimensioni con più Live Copy, l’anteprima della cronologia della versione della pagina non viene caricata (NPR-33311).
* Quando si utilizza il comando Sposta per rinominare una pagina di Experience Manager Sites, il titolo della pagina non viene aggiornato (NPR-33264).
* Quando si spostano le pagine nella vista a colonne, le colonne scompaiono (NPR-33216).
* Quando il nome di un componente locale in una copia per lingua è identico al nome di un componente nella blueprint e il componente viene rilasciato dalla blueprint, il termine `_msm_moved` non viene aggiunto al nome del componente locale (NPR-33208).
* Il servlet di reindirizzamento pagina aggiunge .html a un URL di Experience Manager Sites in cui ResourceType non è `cq:Page` (NPR-33176).
* Quando si incolla una sottostruttura, non è possibile decidere se le relative sottopagine devono essere incollate o meno (NPR-33149).
* Il numero di risultati negli usi live di un componente è limitato al numero 49 (NPR-33058).
* Quando si basa un frammento di contenuto su uno schema e questo contiene un’area di testo obbligatoria o un campo percorso, il frammento di contenuto non viene salvato (NPR-33007).
* Quando crei un componente personalizzato utilizzando il componente Frammento esperienza predefinito e lo utilizzi nelle pagine di Experience Manager Sites, in Experience Manager non vengono visualizzati i riferimenti (utilizzo) per il componente personalizzato (NPR-32852).
* Quando rinomini una cartella con un numero elevato di riferimenti, molti riferimenti alla cartella non vengono aggiornati (NPR-32765).
* Quando abiliti l’opzione di modifica sorgente, questa diventa disponibile per le opzioni a schermo intero in linea, ma rimane mancante per la finestra di dialogo di modifica e le opzioni a schermo intero dell’editor Rich Text (NPR-32763).
* Se disponi di un campo multiplo e contiene un campo obbligatorio (ad esempio un elenco a discesa o un campo percorso) nelle proprietà della pagina di un blueprint, quando viene implementata una pagina contenente tale campo multiplo, le proprietà della pagina della Live Copy non vengono salvate (NPR-32751).
* Gli assistenti vocali non possono utilizzare la struttura dell’intestazione per navigare su una pagina. Inoltre, la scheda Componenti presenta l’etichetta sbagliata (NPR-32648).
* All’avvio dell’impaginazione, il selettore dei frammenti esperienza non carica tutti gli elementi (NPR-32605).
* Le autorizzazioni di authoring per leggere, modificare, creare ed eliminare le Live Copy sono revocate. Ogni autore doveva fornire in modo esplicito le autorizzazioni di lettura e modifica per spostare le pagine all&#39;interno di una blueprint (NPR-32550).
* Gli autori dei contenuti non riescono a creare Launch per una pagina che ha un’integrazione con Adobe Analytics (NPR-32548).
* Quando un utente riprende l’ereditarietà con la sincronizzazione, la Live Copy della pagina padre non si sincronizza con la blueprint e visualizza uno stato errato (NPR-32500).
* Il caricamento della pagina dell’editor di Experience Manager Sites dura più di 15 secondi (NPR-32413).
* Alcuni campi non presentano l’opzione Annulla ereditarietà (NPR-32362).
* Quando selezioni un percorso per un componente Frammento esperienza e selezioni la casella di controllo Apri finestra di dialogo per selezione , non accedi al percorso selezionato nel browser Percorsi (NPR-32308).
* Quando esegui l’aggiornamento da Experience Manager 6.2 a Experience Manager 6.5, il componente Parsys dei modelli statici non viene visualizzato correttamente. L’altezza del componente Parsys è impostata su 0 e i componenti al suo interno non sono visibili (NPR-33663).
* Quando un utente copia e incolla un Contenitore di layout sulla stessa pagina, i componenti di un Contenitore di layout non vengono visualizzati (NPR-33648).
* Il controllo dello stato di Dispatcher visualizza il messaggio di avviso `Invalid cookie header` nei file di log (NPR-33629).
* XSS riflesso in PreferencesServlet (NPR-33438).
* Gli utenti anonimi possono accedere alle funzioni di CRXDE Lite (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>Consigliamo agli utenti Windows di [!DNL Experience Manager desktop app] di eseguire l’aggiornamento all’ [app desktop versione 2.0.3.2](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html#what-is-new) per accedere all’archivio DAM nell’istanza [!DNL Adobe Experience Manager 6.5.5.0]. Come possono incontrare problemi durante l’accesso all’archivio DAM sull’ istanza [!DNL Adobe Experience Manager] 6.5.5.0 utilizzando l’app desktop versione 2.0.2.

**Miglioramenti all’accessibilità in Experience Manager Assets**

* È ora possibile attivare la tastiera sull&#39;elenco [!UICONTROL Commenti] e fare clic sull&#39;opzione per [!UICONTROL Crea] commenti sulla versione in [!UICONTROL Crea nuova versione] nel pannello [!UICONTROL Timeline] delle risorse (NPR-33424).

* È ora possibile raggiungere l&#39;opzione [!UICONTROL Visualizza impostazioni] per le risorse e modificare le impostazioni nella finestra di dialogo [!UICONTROL Visualizza impostazioni] utilizzando i tasti di scelta rapida (NPR-33420).

* La finestra a comparsa della casella di riepilogo della casella combinata (in vari campi su pagine diverse) ora mostra le voci come un elenco di opzioni che possono essere annunciate dagli assistenti vocali (NPR-33516).

* La funzionalità di ordinamento delle intestazioni ordinabili (nella vista a elenco, la vista [!UICONTROL Timeline] e la pagina [!UICONTROL Gestisci pubblicazione] ) sono ora annunciate dagli assistenti vocali e i controlli di ordinamento delle intestazioni di colonna sono accessibili da tastiera (NPR-32979).

* Gli elementi cliccabili come le schede dei commenti, gli aggiornamenti delle versioni, le caselle combinate e le icone chevron dei menu possono ora essere concentrati e interagire con l&#39;uso di una tastiera (NPR-33514).

* La funzionalità (o lo scopo dell&#39;azione) delle icone di insights (per utilizzo, impression e clic) su [!UICONTROL Vista approfondimenti] ora viene annunciata correttamente dagli assistenti vocali (NPR-33513).

* I campi modulo di sola lettura (ad esempio i campi disabilitati nella scheda [!UICONTROL Base] della risorsa [!UICONTROL Proprietà]) sono ora attivabili da tastiera (NPR-33493, CQ-4273031).

* Le etichette in vari campi di input ora sono etichette permanenti (quindi accessibili) e non solo etichette dei segnaposto, scomparse quando il testo è stato immesso (NPR-33475).

* I diversi livelli di intestazione (come titoli di pagina e intestazioni di sezione) vengono ora percepiti come intestazioni con livelli diversi per gli utenti di utilità di lettura dello schermo (NPR-33471).

* Gli elementi interattivi dell’interfaccia utente, ad esempio collegamenti e opzioni (opzioni di intestazione e zoom della pagina delle risorse, navigazione delle cartelle), sono ora accessibili da tastiera (NPR-33468, CQ-4271412).

* Gli indicatori di avanzamento [!UICONTROL Opzioni], [!UICONTROL Ambito] e [!UICONTROL Flussi di lavoro] nella pagina [!UICONTROL Gestisci pubblicazione] vengono ora letti correttamente dagli assistenti vocali come indicatori di avanzamento, anziché come schede (NPR-33416).

* Il colore delle icone di valutazione a forma di stella (come nella sezione [!UICONTROL Valutazione] della scheda [!UICONTROL Avanzate] nella scheda della risorsa [!UICONTROL Proprietà] o nella vista a schede) viene modificato in modo che il contrasto appropriato sia visibile agli utenti con visione limitata e senza percezione del colore (NPR-33414).

* È ora possibile accedere alla freccia verticale accanto al campo [!UICONTROL Commento] nella pagina dei dettagli delle risorse utilizzando i tasti di scelta rapida (NPR-33397).

* Gli stati espansi e compressi della finestra di dialogo [!UICONTROL Tag] sulla risorsa [!UICONTROL Proprietà] e sulla barra di navigazione a sinistra (nell’interfaccia utente delle risorse) ora vengono annunciati correttamente dagli assistenti vocali (NPR-33396).

* I titoli di tutte le pagine visualizzate su [!DNL Adobe Experience Manager] Risorse sono ora univoci (NPR-33343).

* Durante la navigazione nella struttura ad albero, vari elementi del controllo della visualizzazione ad albero vengono ora annunciati correttamente dagli assistenti vocali (NPR-33304).

* Nella pagina dei dettagli delle risorse, le diverse versioni delle risorse nella vista [!UICONTROL Timeline] sono ora accessibili tramite tasti di scelta rapida (NPR-33283).

* I nomi dei suggerimenti di ricerca visualizzati nella casella combinata Omnisearch vengono ora annunciati dagli assistenti vocali quando si utilizza la funzionalità di ricerca (NPR-33280).

* Gli elementi selezionabili e [!UICONTROL Vai a collegamento] in [!UICONTROL Barra Riferimenti] vengono ora annunciati dagli assistenti vocali come elementi cliccabili (NPR-33278).

* Le informazioni sulla struttura della tabella (come riga 1, cella 1, tabella) della finestra di dialogo [!UICONTROL Condividi collegamento] non vengono più lette dagli assistenti vocali quando viene aperta la finestra di dialogo (NPR-33268).

* Lo scopo di vari elementi della casella combinata (ad esempio il campo Percorso e l’opzione per aprire la finestra di dialogo Selezione nella scheda Base delle Proprietà delle risorse) ora viene annunciato correttamente dagli assistenti vocali (NPR-33235).

* Le informazioni che consentono di selezionare le righe nella tabella nella vista a elenco vengono ora comunicate agli utenti degli assistenti vocali quando è attiva la tastiera. Quando un puntatore passa sopra le righe, gli assistenti vocali annunciano le informazioni (NPR-33234).

* Le opzioni (con [!UICONTROL x]) per rimuovere ciascuno dei tag selezionati sotto il campo [!UICONTROL Tag] nella scheda [!UICONTROL Base] di [!UICONTROL Proprietà] sono ora accessibili agli assistenti vocali (NPR-33206).

* Il selettore data del calendario è ora attivabile e utilizzabile dagli utenti di utilità di lettura dello schermo e da tastiera con vista (NPR-33200).

* L’interruttore che consente di passare dalla visualizzazione a elenco a quella a schede ora espone correttamente la sua funzionalità (di regolazione delle viste) all’assistente vocale (NPR-33069).

* Il menu nella barra a sinistra è ora accessibile. Funzionalità e scopo dell&#39;espansione del menu sono annunciati in modo appropriato dagli assistenti vocali (NPR-33068).

* La casella di riepilogo e molti altri elementi dell’interfaccia utente sono ora accessibili agli utenti non vedenti che utilizzano utilità di lettura dello schermo e le seguenti informazioni sono fornite dagli assistenti vocali (NPR-33040):

   * se l’input dell’utente è necessario su un elemento prima dell’invio del modulo.
   * se un elemento non è modificabile.
   * se un widget è selezionato o meno.

* È ora possibile accedere da tastiera all’opzione per aprire la barra laterale del filtro (NPR-32842, CQ-4273018).

* Il controllo delle caselle di controllo nell’intestazione della colonna della vista a elenco è ora accessibile e lo scopo dell’utilizzo del controllo è annunciato dagli assistenti vocali (NPR-32722, NPR-33005).

* I campi delle etichette per ore (HH) e minuti (mm) nel selettore data calendario sono ora etichette permanenti al posto delle etichette dei segnaposto e non scompaiono quando l’utente immette testo in questi campi (NPR-32720).

* Il testo dei collegamenti delle notifiche (che appaiono dopo aver fatto clic sull&#39;icona della campana) viene ora annunciato agli utenti degli assistenti vocali, che utilizzano la scheda per accedere a ogni collegamento (NPR-32645).

* [!UICONTROL Seleziona],  [!UICONTROL Scarica],  [!UICONTROL Proprietà] e  [!UICONTROL altre ] azioni sulle schede delle risorse in  [!UICONTROL Insights ] Vieware sono ora accessibili da tastiera (NPR-32609).

* I contenuti visivamente nascosti (come il contenuto della barra dei menu di intestazione sui risultati della ricerca) non vengono più visualizzati dagli assistenti vocali quando vi si accede utilizzando la tastiera (NPR-32606).

* Lo scopo delle etichette sui controlli per passare ai mesi successivi e precedenti nel selettore data calendario è ora annunciato dagli assistenti vocali (NPR-32604).

* Le icone di valutazione a stella sono ora attivabili e utilizzabili con i tasti della tastiera (NPR-32513).

* La funzionalità di controllo del volume video è ora accessibile tramite scheda (per attivare il dispositivo di scorrimento del volume) e tasti freccia (per regolare il volume) sulla tastiera (NPR-32065).

* Lo scopo dei campi di input associati ([!UICONTROL Da]) e associati ([!UICONTROL A]) del filtro Dimensione file viene ora annunciato agli utenti non vedenti di utilità di lettura dello schermo (NPR-32064).

* Il menu [!UICONTROL Lingue] nel modulo [!UICONTROL Crea e traduci] è ora accessibile agli assistenti vocali in modalità Sfoglia (CQ-4293906).

* Il pannello [!UICONTROL Riferimenti] è ora accessibile con i seguenti miglioramenti (NPR-33261, CQ-4293798):

   * In modalità Sfoglia, lo stato attivo dell’assistente vocale non si sposta più sui campi di modifica multilingue nascosti nelle sezioni [!UICONTROL Riferimenti al sito], [!UICONTROL Riferimenti risorsa], [!UICONTROL Copie] e [!UICONTROL Riferimenti al modulo].

   * Gli assistenti vocali ora annunciano il ruolo degli elementi [!UICONTROL Riferimenti al sito] e [!UICONTROL Copie per lingua] .

   * La messa a fuoco degli assistenti vocali in modalità Sfoglia si sposta in una sequenza significativa a vari elementi.

* [!UICONTROL La pagina ] Editor schema metadati e i relativi elementi sono ora accessibili da tastiera e compatibili con gli assistenti vocali (CQ-4290962, CQ-4272953).

* Lo scopo del simbolo `X` per rimuovere i tag selezionati viene ora annunciato dagli assistenti vocali insieme al numero di tag selezionati (CQ-4273017).

* Per evitare confusione per gli utenti non vedenti che utilizzano assistenti vocali, le icone decorative e le immagini vengono ora ignorate dagli assistenti vocali (CQ-4272944).

**Problemi risolti in Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets fornisce correzioni ai seguenti problemi:

*  L’opzione Start nella finestra di dialogo   Crea flusso di lavoro per le risorse di una raccolta è disabilitata, impedendo in tal modo l’attivazione del flusso di lavoro (NPR-32471).

* Quando si utilizza la finestra a comparsa a cascata negli schemi di metadati, quando si seleziona e si salva un&#39;opzione a discesa contenente un apostrofo (dall&#39;elenco a discesa figlio), l&#39;opzione apostrofo selezionata scompare dopo la riapertura della risorsa [!UICONTROL Proprietà] (NPR-32649).

* [!UICONTROL Asset Insights Sincronizza ] Jobstop e non riesce se si verificano voci non valide (sul lato Analytics) invece di passare alla voce successiva (NPR-32674).

* Il giroscopio non funziona perché i sensori di movimento sono disattivati per impostazione predefinita sui browser mobili nel visualizzatore panoramico (CQ-4272937).

* [!UICONTROL La procedura guidata di ] configurazione delle risorse collegate non funziona con l’errore 404 durante l’installazione della versione 6.5.3 in 6.5.1 (NPR-32730).

* Durante il processo di write-back di XMP, tutte le proprietà dei metadati dello spazio dei nomi personalizzato cambiano il prefisso dello spazio dei nomi personalizzato in ns2 invece del prefisso dello spazio dei nomi configurato (NPR-32748).

* Il caricamento lento non viene attivato e alla selezione vengono visualizzate solo 100 risorse per rivedere le attività dalla casella in entrata delle notifiche (NPR-32750).

* `NullPointerException` è osservato a causa di preferenze di nodo mancanti nel profilo utente appena creato (SAML/SSO). Questo errore impedisce agli utenti appena connessi di utilizzare l&#39;integrazione [!DNL Adobe Experience Manager Stock] (NPR-32777).

* Nei registri all’apertura di una raccolta avanzata contenente più di 10.000 risorse (NPR-32980) vengono osservati gli avvisi relativi alle transizioni.

* I nomi delle risorse vengono modificati in minuscolo quando si spostano le risorse da una cartella all’altra in [!DNL Adobe Experience Manager] in modalità runmode Dynamic Media Scene7 (NPR-32995).

* Una risorsa ricercata non può essere eliminata dopo aver navigato nelle sue proprietà dai risultati della ricerca e poi essere tornata ai risultati della ricerca per eliminarla (NPR-32998).

*  Nextoption rimane disabilitata quando si seleziona la cartella di destinazione nell’interfaccia  [!UICONTROL Sposta ] risorse (NPR-33356).

*  Nextoption non è abilitata quando si seleziona il nodo principale (in cui è visibile una singola cartella figlio) e si seleziona la cartella secondaria (NPR-33275).

* Le autorizzazioni di archiviazione e ritiro sono disabilitate in Adobe Asset Link (AAL) per gli utenti con autorizzazione di eliminazione, anche se sono concesse altre autorizzazioni come lettura, creazione o modifica (NPR-33272).

* Le rappresentazioni di ritaglio avanzato non sono disponibili nella finestra di dialogo per il download delle risorse (NPR-33167).

* Si osserva un’eccezione nei registri all’apertura della barra delle rappresentazioni per un PDF in una cartella con profilo di ritaglio avanzato (CQ-4294201).

* I predefiniti per immagini non vengono pubblicati se [!UICONTROL la modalità di sincronizzazione Dynamic Media] è disabilitata per impostazione predefinita all&#39;Experience Manager con la modalità di esecuzione Dynamic Media Scene7 (CQ-4294200).

* L’elaborazione delle risorse mentre il caricamento in serie si blocca e l’istanza del flusso di lavoro mostra le istanze bloccate della risorsa di aggiornamento DAM (CQ-4293916).

* La creazione di una configurazione Dynamic Media su Experience Manager funziona, ma sull&#39;interfaccia utente non succede nulla quando si seleziona Salva (CQ-4292442).

* L&#39;anteprima delle risorse video F4V non funziona in riproduzione progressiva su Safari/Mac (CQ-4289844).

* La cartella aggiuntiva viene creata con il ritaglio avanzato di una risorsa che si trova all’interno di una cartella principale con il carattere punto `.` nel nome (CQ-4289337).

* La miniatura è rotta e il banner di elaborazione video non viene visualizzato quando un video viene copiato (CQ-4284125).

* Il visualizzatore dimensionale visualizza in modo errato le miniature vuote in Firefox per alcuni modelli con viste videocamera vuote (CQ-4283447).

* I problemi di prestazioni risolti nella versione 6.5.5.0 sono (CQ-4279206):

   * Il caricamento di file binari di grandi dimensioni sui server di elaborazione delle immagini Dynamic Media richiede troppo tempo.

   * Il tempo di generazione delle miniature sull’Experience Manager aumenta a causa dell’architettura Scene7 di Dynamic Media.

* I problemi di migrazione di Dynamic Media Scene7 non riescono per i clienti con un numero elevato di risorse (CQ-4279206).

* Il layout del visualizzatore video 360 viene interrotto se si utilizza `setVideo` e il video si sposta all’uso con `video= modifier` (CQ-4263201).

* Viene visualizzato un messaggio di errore durante l’installazione del pacchetto Experience Manager SDL (NPR-33175).

* Vulnerabilità SSRF in Experience Manager (NPR-33435).

### Piattaforma {#platform-6550}

* Il filtro [!DNL Sling] non viene chiamato se la voce di mappa `sling:match` viene creata in `/etc/maps` (NPR-33362).
* Arresto anomalo dell&#39;Experience Manager a causa di un errore di segmentazione con [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] pacchetto principale mancante dal file uberjar di Experience Manager (NPR-32848).
* CRXDE Lite non carica contenuti per gli utenti senza autorizzazione di lettura sulla proprietà `jcr:primaryType` di un nodo (NPR-32611).
* [!DNL Granite] la pianificazione delle attività di manutenzione viene reinizializzata troppo spesso durante le distribuzioni di Experience Manager (CQ-4294627).
* Quando una query SQL viene eseguita per un lungo periodo di tempo, ad esempio 7 ore, l&#39;Experience Manager smette di rispondere (NPR-33044).

### Interfaccia utente {#ui-6550}

* La selezione del pulsante di scelta non persiste in un campo multiplo (NPR-33309).
* Il limite di caricamento non funziona per la visualizzazione elenco (NPR-33124).
* La pagina dei risultati di Omnisearch non visualizza un messaggio se non sono presenti corrispondenze (NPR-32974).
* Il filtro Omnisearch restituisce tutte le corrispondenze sotto il nodo `/content` ignorando la posizione selezionata (NPR-32849).

### Integrations (Integrazioni) {#integrations-6550}

* La cache interna viene cancellata quando viene pubblicata una pagina con un componente Adobe Target (NPR-33162).
* L&#39;integrazione con Adobe Target non funziona su [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Durante la configurazione di Adobe Target, i campi [!UICONTROL Azienda] e [!UICONTROL Suite di rapporti] non vengono visualizzati quando si seleziona un&#39;origine per la generazione di rapporti (NPR-32502).
* Durante l’esportazione di [!DNL Experience Fragments] utilizzando [!DNL Adobe I/O], metadati come Prodotto di origine non vengono esportati in Adobe Target (NPR-32159).
* Gli utenti IMS autorizzati nel gruppo di amministrazione locale di Experience Manager non possono creare o modificare configurazioni IMS (NPR-33045).
* La pagina delle configurazioni di Adobe Launch non visualizza tutti i record (NPR-33011).
* Gli utenti del gruppo content-authors non possono modificare le proprietà di un componente Adobe Target a causa di un errore JavaScript (NPR-32996).
* Script tra siti per JSON (NPR-32744).

### Progetti traduzione {#translation-6550}

* I tag tradotti non vengono importati in Experience Manager da servizi di traduzione di terze parti (NPR-33154).
* Nella pagina di configurazione della traduzione viene visualizzato un provider di traduzione errato rispetto a quello utilizzato per la traduzione (NPR-32971).
* Aggiungendo una cartella di frammenti di esperienza a un progetto di traduzione esistente si crea un nuovo progetto (NPR-32843).
* Nei registri viene visualizzato un errore `NullPointerException` durante l’esecuzione di un processo di traduzione (NPR-32628).

### WCM {#wcm-6550}

* Editor pagina : l’ [!DNL Sites] Editor pagina non consente agli utenti con solo tastiera di passare al contenuto principale invece di spostare lo stato attivo su tutte le opzioni disponibili nell’intestazione (CQ-4293883).
* Editor pagina : i pannelli che utilizzano il componente Bene e includono dati salvati non vengono visualizzati a causa di aggiornamenti nelle versioni [!DNL Chrome] e [!DNL Firefox] (CQ-4292995).
* MSM - L’eliminazione di un componente dalla pagina non elimina il componente dalla versione pubblicata della pagina (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* La rimozione di uno schema di metadati pubblicato da [!DNL Brand Portal] genera un errore (CQ-4292063).
* Se un amministratore configura [!DNL Experience Manager Assets] 6.5.4 con Brand Portal tramite Adobe Developer Console, l’ [!DNL Brand Portal] utente non è in grado di pubblicare la risorsa di una cartella di contributi da [!DNL Brand Portal] a [!DNL Experience Manager] (NPR-33046).
* Replica duplicata delle cartelle principali che causano conflitti (NPR-33001).

### [!DNL Communities] {#communities-6550}

* Non è possibile eliminare una scheda nella console di moderazione utilizzando l&#39;opzione del menu di modifica rapida (NPR-33117).
* Si verifica un errore durante l&#39;accesso alla pagina [!UICONTROL Flusso attività] (NPR-33146).
* I gruppi eliminati nell&#39;istanza dell&#39;autore non vengono rimossi da tutte le istanze di pubblicazione (NPR-33199).
* Gli autori, dopo aver creato un nuovo gruppo, non vengono reindirizzati alla sezione [!UICONTROL Gruppo community] su [!DNL Internet Explorer] 11 (NPR-33205).
* L&#39;accesso a un messaggio nella Casella in entrata Experience Manager non modifica lo stato del messaggio in Lettura (NPR-32764).
* La modifica di un gruppo [!DNL Communities] e la modifica dell&#39;immagine miniatura non aggiorna l&#39;immagine della miniatura del gruppo (NPR-32599).
* Un utente non è in grado di inviare un’e-mail a un altro utente in una community (NPR-32598).
* Un blog inviato non viene visualizzato finché l’utente non aggiorna la pagina (NPR-32391).
* Durante la creazione di una versione di notifiche e sottoscrizioni di contenuti generati dagli utenti (UGC, User Generated Content), viene memorizzato un ID errato della pagina sorgente (CQ-4279355, CQ-4289703).
* Problema di scripting tra siti (NPR-33203).

### Flusso di lavoro {#workflow-6550}

* Il caricamento dell&#39;opzione [!UICONTROL Timeline] nella barra a sinistra richiede più tempo del previsto (NPR-32851).
* Dopo il riavvio di un&#39;istanza di Experience Manager, l&#39;e-mail per l&#39;attività di revisione di una raccolta include un collegamento di payload non corretto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Il Service Pack di Experience Manager non include correzioni per [!DNL Forms]. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per AEM Forms su JEE. Per ulteriori informazioni, consulta [Installare il componente aggiuntivo Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gestione della corrispondenza: L’ordine delle risorse in un’area di destinazione viene mischiato dopo l’invio di una lettera (NPR-33359, NPR-33153).
* Forms adattivo: Quando un utente modifica un modulo adattivo, l&#39;opzione [!UICONTROL Avvia flusso di lavoro] disponibile nel menu [!UICONTROL Informazioni pagina] non funziona (NPR-33004).
* Forms adattivo: L&#39;utente non è in grado di salvare un modulo adattivo con più di un allegato (NPR-32997).
* Forms adattivo: La modifica del layout del pannello in un modulo adattivo genera un errore (CQ-4293880).
* Forms adattivo: Una nuova riga a una stringa in un dizionario dei moduli adattivi aggiunge caratteri `&#xa;` al dizionario (NPR-33266).
* Accessibilità adattata di Forms: Quando un utente visualizza l&#39;anteprima di un modulo adattivo come modulo HTML, il campo [!UICONTROL Firma scarabocchio] non è in grado di mantenere lo stato attivo (NPR-33159).
* Accessibilità adattata di Forms: I messaggi di errore visualizzati all’invio di un modulo adattivo non si collegano a un attributo `aria-describedBy` (NPR-33071).
* Accessibilità adattata di Forms: I campi contrassegnati come obbligatori in un modulo adattivo non hanno l’attributo obbligatorio impostato su True nello schema di accessibilità ARIA (NPR-33070).
* Servizio PDFG: Quando un utente converte un file di testo in un PDF, i caratteri giapponesi non vengono riprodotti correttamente (NPR-33238).
* Servizio PDFG: L&#39;operazione `CreatePDF` non riesce a convertire un file PDF in formato PDF OCR (NPR-32994).
* Servizio PDFG: La conversione PDF non riesce per la 200a istanza di un documento [!DNL OpenOffice] (NPR-32766).
* Integrazione back-end: Le richieste del modello dati del modulo non riescono perché scade il token di aggiornamento a causa di uno stato inattivo non corretto (NPR-33169).
* Designer: Gli assistenti vocali eseguono l’ordine di tabulazione in base all’ordine geografico predefinito anziché all’ordine di tabulazione personalizzato definito nel file XDP (NPR-32160).
* Designer: Se l’opzione di assegnazione tag è abilitata, il bordo del sottomodulo scompare nell’output PDF generato (NPR-32778).
* Archiviato XSS con il GuideSOMProviderServlet (NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 è un aggiornamento importante che include nuove funzioni, miglioramenti e prestazioni richiesti dai clienti chiave, stabilità, miglioramenti a livello di sicurezza, rilasciato a partire dalla versione 6.5 di **aprile 2019**. Può essere installato su Adobe Experience Manager 6.5.

Alcune funzioni chiave e miglioramenti introdotti in Adobe Experience Manager 6.5.4.0 includono:

* Adobe Experience Manager Assets è ora configurato con Brand Portal tramite la [!DNL Adobe I/O] console.

* È ora disponibile un nuovo passaggio [Genera output stampabile](../forms/using/aem-forms-workflow-step-reference.md) per i flussi di lavoro Adobe Experience Manager Forms.

* [Supporto di più colonne ](../forms/using/resize-using-layout-mode.md) per la modalità di layout per moduli adattivi e comunicazioni interattive.

* Supporto per [Rich Text](../forms/using/designing-form-template.md) nei moduli HTML5.

* [Miglioramenti ](new-features-latest-service-pack.md#accessibility-enhancements) all’accessibilità in Experience Manager Assets.

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.8.

* È ora possibile sincronizzare i sottoalberi di contenuto selettivo su *Dynamic Media - Modalità Scene7* invece di tutti quelli disponibili in `content/dam`.

* L’integrazione del modello dati modulo con il servizio Web SOAP ora supporta i gruppi di scelta o gli attributi sugli elementi.

* Le strutture di input o output SOAP e i dati complessi supportano la sostituzione di gruppi dinamici.

Per un elenco completo delle funzioni e degli elementi di rilievo introdotti nei Service Pack più recenti, consulta [Novità in Adobe Experience Manager 6.5 Service Pack](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Quando un URL di una pagina Adobe Experience Manager Sites contiene due punti (`:`) o un simbolo di percentuale (`%`), il browser smette di rispondere e i picchi di utilizzo della CPU (NPR-32369, NPR-31918).

* Quando una pagina di Experience Manager Sites viene aperta per la modifica e un componente viene copiato, l’azione Incolla non è disponibile per alcuni segnaposto (NPR-32317).

* Quando si apre la procedura guidata Gestisci pubblicazione , un frammento esperienza collegato a un componente core non viene visualizzato negli elenchi dei riferimenti pubblicati (NPR-32233).

* La panoramica della Live Copy nell’interfaccia touch richiede molto più tempo dell’interfaccia classica per il rendering (NPR-32149).

* Quando il server-time e il computer-time si trovano in fusi orari diversi, l’ora di pubblicazione pianificata visualizza l’ora del server nell’interfaccia utente touch, mentre nell’interfaccia classica viene visualizzata l’ora del computer (NPR-32077).

* Experience Manager Sites non riesce ad aprire una pagina con un suffisso nell’URL (NPR-32072).

* Quando un utente modifica un frammento di contenuto, viene ripristinata una variante eliminata del frammento di contenuto (NPR-32062).

* Gli utenti possono salvare un frammento di contenuto senza fornire informazioni nei campi richiesti (NPR-31988).

* kernel.js e ui.js non sono pre-rispettati o memorizzati nella cache. Porta a un tempo aggiuntivo per il rendering delle pagine (NPR-31891).

* Quando PageEventAuditListener è abilitato, la lunghezza della coda di commit aumenta. Ha un impatto sulle prestazioni di molte operazioni, come la pubblicazione in blocco, la navigazione e lo spostamento di risorse in massa (NPR-31890).

* Quando si trascinano i frammenti esperienza, si osserva un tempo di risposta elevato (NPR-31878).

* Quando selezioni l’opzione Trascina qui il componente nel segnaposto di una griglia reattiva, viene inviata una richiesta di GET e la richiesta si traduce in un errore HTTP 403 (NPR-31845).

* Quando si sposta il contenuto all’interno della stessa cartella, l’opzione di spostamento della pagina è disabilitata (NPR-31840).

* In modalità struttura modelli modificabili, l’elenco dei componenti consentiti nel contenitore di layout visualizza risultati errati. Solo i componenti con finestra di dialogo di progettazione vengono visualizzati nel contenitore di layout (NPR-31816).

* Quando una pagina dispone di autorizzazioni di sola lettura per un utente, l’opzione Apri proprietà è visibile in sites.html ma non in editor.html (NPR-31770).

* Quando un utente fa clic sul pulsante Crea, l’opzione di pagina non è disponibile (NPR-31756).

* Impossibile sincronizzare la campagna in una campagna Adobe contenente il componente Importazione progettazione OOTB (Out of the box) (NPR-31728).

* Quando tenti di modificare un elenco puntato in elenco numerato, vengono modificati solo i primi due elementi dell’elenco (NPR-31636).

* Quando una pagina viene decreata e il nodo figlio è selezionato, la finestra di dialogo di selezione visualizza ancora il nodo iniziale. Quando la pagina viene creata e l’utente fa clic su Sfoglia, la pagina reindirizza al nodo principale invece del nodo creato (NPR-31618).

* La finestra di dialogo di configurazione della visualizzazione non funziona correttamente per la funzione del flusso di lavoro di personalizzazione della casella in entrata (NPR-32503 e NPR-32492).

* Viene visualizzato un messaggio di errore durante la visualizzazione delle informazioni sul flusso di lavoro tramite Casella in entrata (CQ-4282168).

### Assets {#assets-6540-enhancements}

* Il pulsante per attivare il flusso di lavoro nella pagina di raccolta delle risorse è disattivato (NPR-32471).

* Viene creata una cartella senza nome in SPS (Scene7 Publishing System) mentre si sposta una risorsa da una cartella all’altra in Experience Manager con configurazione Dynamic Media Scene7 (NPR-32440).

* L’azione per spostare tutte le risorse (utilizzando Seleziona tutto e quindi Sposta) in una cartella contenente le risorse pubblicate non riesce e viene restituito un errore (NPR-32366).

* Generazione del rendering per le risorse con ${extension} non riuscita (NPR-32294).

* Gli URL della cronologia delle versioni vengono visualizzati nel campo Con riferimento nella pagina Proprietà delle risorse (NPR-31889).

* Impossibile aprire il file ZIP scaricato da DAM utilizzando WinZip (NPR-32293).

* Le autorizzazioni originali di una cartella vengono aggiornate quando le Impostazioni cartella vengono aperte per modificare il titolo della cartella o l&#39;immagine in miniatura e quindi salvate (NPR-32292).

* L’icona del calendario per l’attivazione pianificata non viene visualizzata nella colonna Stato (nell’interfaccia classica dell’elenco delle risorse DAM) per le risorse la cui attivazione è pianificata per una data e un’ora successive (NPR-32291).

* La creazione di snippet utilizzando i modelli di snippet genera un errore nella ricerca delle raccolte durante il processo di creazione dello snippet (NPR-32290).

* Vengono attivate più query di ricerca quando vengono selezionati più tag dal filtro di ricerca (NPR-32143).

* L’interfaccia utente di Experience Manager Assets visualizza i nomi dei file troncati quando vengono caricate risorse con più di 50 caratteri nel nome file (NPR-32054).

* Tutte le caselle di controllo nel pannello Filtro vengono deselezionate quando la prima e la seconda casella di controllo sono deselezionate, quando sono state selezionate le caselle di controllo di livello due della struttura delle caselle di controllo in Adobe Stock (NPR-31919).

* Fa eccezione la ricerca di file e cartelle utilizzando i facet Omnisearch (NPR-31872).

* L’evidenziazione dei campi per la selezione obbligatoria dei campi nell’editor di metadati non viene rimossa anche dopo aver selezionato il campo richiesto, quando le regole di dipendenza sono impostate nel modulo dello schema di metadati corrispondente (NPR-31834).

* I nomi completi dei tag a livello di foglia (dalla gerarchia dei tag) non vengono visualizzati nella pagina Proprietà della risorsa (NPR-31820).

* L’utilizzo del comando Indietro dalla pagina Proprietà della risorsa nel browser Safari restituisce l’errore (NPR-31753).

* La pagina dei risultati della ricerca nell’interfaccia touch (tramite Omnisearch) scorre automaticamente verso l’alto e perde la posizione di scorrimento dell’utente (NPR-31307).

* La pagina dei dettagli delle risorse PDF non mostra i pulsanti di azione eccetto A raccolta e Aggiungi rappresentazione in Experience Manager in esecuzione in modalità di esecuzione di Dynamic Media Scene7 (CQ-4286705).

* L’elaborazione delle risorse richiede troppo tempo durante il processo di caricamento batch di Scene7 (CQ-4286445).

* Il pulsante Salva non importa il set remoto se l’utente non ha apportato modifiche nell’Editor set nel client Dynamic Media (CQ-4285690).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene acquisito in Experience Manager (CQ-4283701).

* Lo stato non elaborato del predefinito visualizzatore video per ritaglio avanzato viene visualizzato due volte sul testo del banner accanto al nome predefinito (CQ-4283517).

* L’altezza errata del contenitore di un modello 3D caricato visualizzato in anteprima nel visualizzatore 3D viene osservata nella pagina dei dettagli della risorsa (CQ-4283309).

* L&#39;Editor carosello non si apre in IE 11 in modalità ibrida Experience Manager Dynamic Media (CQ-4255590).

* Lo stato attivo della tastiera si blocca nell’elenco a discesa E-mail nella finestra di dialogo Download, nei browser Chrome e Safari (NPR-32067).

* La casella di controllo Sincronizza tutto il contenuto non è abilitata per impostazione predefinita durante il tentativo di aggiungere la configurazione cloud DM su Experience Manager (CQ-4288533).

### Interfaccia utente di base {#foundation-ui-6540}

* Il controllo del mouse passa al campo filtro precedente invece di rimanere nel campo filtro esistente durante la ricerca delle risorse tramite il pannello Filtro (NPR-32538).

* Assegnazione tag alla piattaforma: La ricerca di tag digitando nei campi tag mostra i tag al di fuori dei limiti principali e non rispetta la proprietà `rootPath` dei campi tag (NPR-31895).

* Interfaccia utente della piattaforma: Il browser percorsi si interrompe se nel campo di testo viene aggiunto un percorso non valido (NPR-31884).

* La notifica viene nascosta dietro un menu fisso nella selezione della pagina (NPR-31628).

### Piattaforma {#platform-sling-6540}

* (HTL) I caratteri di sottolineatura sostituiscono i due punti nella sezione del percorso dell’URL (NPR-32231).

### Progetti {#projects-6540}

* Il pulsante Crea non è visibile all’utente anche se l’utente dispone dell’autorizzazione per creare un progetto nella sottocartella (NPR-31832).

### Traduzione progetti {#projects-translation-6540}

* La creazione di un progetto di traduzione interrompe l’interfaccia utente quando l’opzione Trim Spaces è attivata in `Apache Sling JSP Script Handler` (NPR-32154).

* L’errore nell’interfaccia utente e l’eccezione Null nei registri degli errori viene osservato quando un tag, da tradurre, viene aggiunto a un progetto di traduzione (NPR-31896).

### Integrations (Integrazioni) {#integrations-6540}

* La generazione degli URL della libreria Launch è basata solo sui valori `path` e `library_name` dell’API Launch e non è basata sul valore `library_path` (NPR-31550).

* Viene visualizzato un messaggio di errore durante l&#39;elaborazione degli elementi relativi a LiveFyre (FYR-12420).

* ReportSuitesServlet è vulnerabile a SSRF (NPR-32156).

### Editor modelli WCM {#wcm-template-editor-6540}

* In modalità struttura modelli modificabili, l’elenco dei componenti consentiti nel contenitore layout non visualizza il componente pulsante di collegamento (CQ-4282099).

### Editor pagina WCM {#wcm-page-editor-6540}

* Si osserva un errore durante la selezione di una sovrapposizione e la selezione di una griglia reattiva Trascina qui i componenti (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* La configurazione cloud di Target non riesce e la richiesta di acquisizione mbox dell&#39;errore non è riuscita (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Gli utenti Brand Portal non possono pubblicare le risorse della cartella dei contributi in [!DNL Assets] all’aggiornamento a [!DNL Adobe I/O] all’Experience Manager 6.5.4 (CQDOC-15655). Per una correzione immediata all&#39;Experience Manager 6.5.4, si consiglia di [scaricare l&#39;hotfix](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e installarlo nell&#39;istanza di authoring.

* I valori popup dello schema metadati non sono visibili nelle proprietà delle risorse (CQ-4283287).

* Il sottoschema metadati non visualizza schede basate su tipi MIME nelle proprietà delle risorse (CQ-4283288).

* Lo schema di annullamento della pubblicazione dei metadati popola un messaggio di errore anche se lo schema viene rimosso nel backend.

* L&#39;immagine di anteprima non viene visualizzata per una risorsa pubblicata (CQ-4285886).

* L&#39;utente non è in grado di pubblicare o annullare la pubblicazione delle risorse contenenti virgolette singole nel nome (CQ-4272686).

* I termini e le condizioni non vengono visualizzati durante il download di più risorse (CQ-4281224).

* Sono state risolte alcune vulnerabilità di sicurezza minori.

### Communities {#communities-6540}

* Il modulo Crea membro viene visualizzato come una pagina vuota (NPR-31997).

* L&#39;utente non è in grado di visualizzare il rapporto di Analytics sull&#39;istanza dell&#39;autore (NPR-30913).

### Oak - Indicizzazione e query {#oak-indexing-6540}

* Documenti MS Word e MS Excel, contenente immagine JPEG, quando l&#39;analisi con il parser Tika non riesce ad analizzare e la classe non trovato errore viene osservato (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
>Experience Manager Service Pack non include correzioni per Experience Manager Forms. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per Adobe Experience Manager Forms su JEE. Per ulteriori informazioni, consulta [Installare il componente aggiuntivo Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gestione della corrispondenza: Le lettere presentano caratteri aggiuntivi dopo l’invio ai flussi di lavoro post-elaborazione (NPR-32626).

* Gestione della corrispondenza: Le lettere visualizzano un segnaposto a discesa come componente di testo dopo l’invio ai flussi di lavoro post-elaborazione (NPR-32539).

* Gestione della corrispondenza: I valori predefiniti definiti nel modello di lettera non vengono visualizzati in modalità Anteprima (NPR-32511).

* Forms mobile: Il pulsante di invio viene visualizzato come esteso nelle dimensioni durante il rendering di un modulo XDP in una versione HTML (NPR-32514).

* Servizi documenti: Problemi di accesso agli URL per le lettere e altre pagine dopo l’applicazione del Service Pack 2 (NPR-32508, NPR-32509).

* Servizi documenti: Se il numero di transazioni su un server supera un limite specifico, la conversione da HTML a PDF non riesce e le impostazioni del tipo di file vengono rimosse dal server [!DNL Forms] (NPR-32204).

* Forms adattivo: Lo strumento di accessibilità del browser segnala gli errori nei moduli adattivi in base alle linee guida WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Forms adattivo: Lo strumento per l’accessibilità del browser Chrome segnala un errore di best practice (NPR-32310).

* Forms adattivo: Problemi di traduzione durante la configurazione di un modulo adattivo incorporato in una pagina di Experience Manager Sites (NPR-32168).

* Workbench: Viene visualizzato un messaggio di errore durante l&#39;utilizzo dell&#39;operazione Get PDF Properties per il servizio PDF Utilities (NPR-32150).

* Sicurezza dei documenti: Un file PDF protetto non si apre offline con l&#39;opzione DisableGlobalOfflineSynchronizationData impostata su True (NPR-32078).

* Designer: Se l’opzione di assegnazione tag è abilitata, il bordo del sottomodulo scompare nell’output PDF generato (NPR-32547, NPR-31983, NPR-31950).

* Designer: Se in una tabella sono presenti celle unite, il test di accessibilità non riesce per il file PDF di output convertito da un modulo XDP utilizzando il servizio di output (CQ-4285372).

* JEE di base: Se un server Forms di Experience Manager è disconnesso da un cluster, i problemi di caching ne impediscono la riconnessione al server (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 è una versione importante che include correzioni suggerite dai clienti e miglioramenti a prestazioni, stabilità sicurezza disponibili dal rilascio della versione 6.5 di  **aprile 2019**. Può essere installato su [!DNL Adobe Experience Manager] 6.5.

Alcuni elementi di rilievo di questa versione del Service Pack sono:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.6.

* [!DNL Experience Manager Assets] ora supporta gli archivi ZIP creati con l’algoritmo Deflate64.

* È stata aggiunta una nuova colonna per la data creata, ordinabile, nella vista a elenco DAM e nei risultati della ricerca delle risorse nella vista a elenco.

* L’ordinamento delle risorse basato sulla colonna Nome è stato abilitato nella vista Elenco.

* [!DNL Dynamic Media] ora supporta le risorse video Smart Crop. Smart Crop è una funzione di apprendimento automatico che ritaglia un video mentre si sposta il fotogramma per seguire il punto focale della scena.

* [!DNL Dynamic Media] supporta Smart imaging.

* Possibilità di impostare le preferenze di [Out of Office](../forms/using/configure-out-of-office-settings.md) nei flussi di lavoro [!DNL Experience Manager].

* Possibilità di [condividere elementi in entrata o in entrata](../forms/using/configure-shared-queues-osgi.md) con altri utenti nei flussi di lavoro [!DNL Experience Manager].

* Possibilità di [generare comunicazioni interattive in modalità batch](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* È stata aggiornata la versione di jQuery inclusa nel bundle ContextHub alla versione 3.4.1.

### Risorse {#assets-6530-enhancements}

**Miglioramenti apportati al prodotto**

* [!DNL Experience Manager Assets] ora supporta gli archivi ZIP creati con l’algoritmo Deflate64 (NPR-27573).

* La nuova colonna per la data creata, ordinabile, viene aggiunta nella vista a elenco DAM e nei risultati della ricerca di risorse nella vista a elenco (NPR-31312).

* Nella vista a elenco, gli utenti possono ordinare l’elenco delle risorse utilizzando la colonna [!UICONTROL Nome] (NPR-31299).

* I file GLB, GLTF, OBJ e STL possono essere visualizzati in anteprima nella pagina [!UICONTROL Dettagli risorsa] in DAM (CQ-4282277).

* `ReplicationOnModifyListener` viene attivato per i nodi di blocco durante il caricamento del blocco in  [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] ora supporta le risorse video Smart Crop. Smart Crop è una funzione guidata per l&#39;apprendimento automatico che ritaglia un video mentre si sposta il fotogramma per seguire il punto focale della scena (CQ-4278995).

* [!DNL Dynamic Media] supporta l’imaging avanzato (CQ-422249).

* La visualizzazione di ricerca o navigazione è impostata come visualizzazione predefinita nel selettore di Foundation se i parametri di query vengono passati nella richiesta (NPR-31601).

**Problemi risolti**

* I metadati per alcuni documenti PDF non vengono aggiornati e salvati nel PDF quando il titolo viene modificato (NPR-31629).

* La condivisione delle risorse non funziona per una risorsa con il carattere più (`+`) nel nome file (NPR-31547).

* Le modifiche nel modulo di ricerca predefinito Assets Admin Search Rail non funzionano come previsto (NPR-31502).

* I suggerimenti non vengono visualizzati quando si utilizza Omnisearch nella visualizzazione delle risorse per la ricerca delle risorse (NPR-31496).

* I riferimenti alle risorse all’interno delle raccolte non vengono aggiornati quando le risorse a cui si fa riferimento vengono spostate in un’altra posizione, nei casi in cui a una raccolta diversa facciano riferimento le stesse risorse da parte di utenti diversi (NPR-31486).

* I tag IPTC duplicati vengono aggiunti ai metadati delle risorse (NPR-31328).

* Il conteggio dei risultati della ricerca non viene aggiornato con precisione quando viene attivata una ricerca dalla barra dei filtri (NPR-31316).

* Tutte le caselle di controllo vengono deselezionate quando si deselezionano le caselle di controllo di secondo livello nel filtro Tipo file e il testo nella barra di ricerca non è sincronizzato con le proprietà selezionate o deselezionate (NPR-31287).

* Tutti i membri (utenti/gruppi) non possono essere rimossi dalla sezione Membri di una cartella; quando si tenta di rimuovere tutti gli utenti, l&#39;utente connesso viene aggiunto all&#39;elenco (NPR-31171).

* Le risorse con il simbolo più (`+`) nel nome del file non possono essere eliminate (NPR-31162).

* Il menu a discesa Crea , visibile nel menu principale quando si seleziona una cartella, non mostra l’opzione &quot;Cartella&quot; come opzione di creazione (NPR-30877).

* Selezione cartelle L&#39;elemento dell&#39;azione Crea > FileUpload è mancante quando l&#39;ACL per Rifiuta `jcr:removeChildNodes` e `jcr:removeNode` sul percorso viene applicato a un utente (NPR-30840).

* I flussi di lavoro DAM diventano obsoleti al momento del caricamento di determinate risorse mp4, causando l’esaurimento di tutti i flussi di lavoro rimanenti (NPR-30662).

* Si osserva un errore di memoria esaurita quando un file PDF di grandi dimensioni (di diversi Gigabyte) viene caricato in DAM e le relative risorse secondarie vengono elaborate (NPR-30614).

* Lo spostamento in blocco delle risorse non riesce e viene visualizzato un messaggio di avviso (NPR-30610).

* I nomi delle risorse vengono modificati in minuscolo quando si spostano le risorse da una cartella all’altra in [!DNL Experience Manager] in esecuzione in modalità [!DNL Dynamic Media]-Scene7 (NPR-31630).

* Si osserva un errore durante la modifica di un set di immagini remoto, per l&#39;immagine che si trova nella cartella denominata come nome dell&#39;azienda Scene7 (NPR-31340).

* [!DNL Dynamic Media] le risorse contenenti riferimenti non vengono pubblicate (NPR-31180).

* I caricamenti dalla modalità [!DNL Dynamic Media]7-Scene7 a [!DNL Dynamic Media Classic] richiedono troppo tempo per essere completati (NPR-31048).

* Il punto attivo aggiunto a una risorsa immagine non è visibile tramite il visualizzatore di immagini interattive nella pagina dei dettagli della risorsa (NPR-30979).

* Vengono creati enormi lavori sling e il banner di elaborazione viene visualizzato nuovamente quando le azioni eseguite sulle risorse in [!DNL Experience manager Assets] vengono passate a Scene7 (NPR-30947).

* Si verifica un conflitto durante la creazione di una copia in lingua delle risorse e delle risorse non caricate in Scene7 (NPR-30932).

* Le rappresentazioni dinamiche scaricate da [!DNL Experience Manager] in esecuzione in modalità [!DNL Dynamic Media]-Hybrid sono interrotte (sono di tipo testo con contenuto &quot;impossibile trovare l’immagine&quot; invece del tipo di contenuto immagine) (NPR-30876).

* [!DNL Dynamic Media] Il flusso di lavoro Codifica video non riesce a generare miniature per il video migrato dalla modalità  [!DNL Dynamic Media Classic] a  [!DNL Dynamic Media]-Scene7 su Adobe Experience Manager (CQ-4282011).

* IpsApiException osservata durante la migrazione delle risorse da un’istanza a un’altra utilizzando diversi ID società Scene7 (CQ-4280548).

* La miniatura della risorsa 3D non è informativa, quando un modello 3D supportato viene acquisito in [!DNL Experience Manager] (CQ-4283701).

* I pulsanti di scorrimento vengono visualizzati nel visualizzatore, se una risorsa 3D dispone di poche viste della fotocamera (CQ-4283322).

* Altezza errata del contenitore di un modello 3D caricato visualizzato in anteprima in DimensionalViewer nella pagina Dettagli risorsa (CQ-4283309).

* Non è possibile riprodurre video con SmartCropVideoViewer su Internet Explorer 11 e Safari (CQ-4281422).

* L&#39;utilizzo del pulsante Sposta per spostare più risorse, da una cartella all&#39;altra, non riesce in [!DNL Experience Manager] in esecuzione in modalità runmode [!DNL Dynamic Media]-Scene7 (CQ-4280384).

* Il video distorto viene visualizzato sui dettagli della risorsa quando il tipo MIME è diverso da MP4 (CQ-4279704).

* I video appena acquisiti in cartelle con profilo video rimangono in stato di elaborazione anche dopo il completamento della percentuale di codifica al 100% (CQ-4279389).

* Lo spostamento delle risorse da una cartella crea un numero elevato di processi sling (chiamate API Scene7) rispetto a quanto richiesto idealmente (CQ-4278664).

* I nomi del set di immagini vengono modificati in minuscolo in Scene7, quando il set di immagini (o il set di file multimediali) viene creato e denominato con la convenzione di denominazione appropriata in DAM (CQ-4281112).

* Scene7 Migrator imposta lo stato di pubblicazione in modo errato (CQ-4263492).

* La pagina dei risultati della ricerca nell’interfaccia touch (tramite Omnisearch) scorre automaticamente verso l’alto e perde la posizione di scorrimento dell’utente nei frammenti di contenuto (CQ-4282898).

* I file PDF non sono indicizzati e il contenuto all’interno non è ricercabile (CQ-4278916).

* Un errore &quot;Gruppo non elencato dal selettore utente: previsto false to equal true&quot; viene osservato quando si aggiunge Closed User Group con diversi `principalName` e `authorizableId` (CQ-4278177).

* La vista a colonne dell’interfaccia utente Assets mostra tutti i percorsi, indipendentemente dal percorso principale dam del tenant specifico (CQ-4278175).

* La ricerca del selettore delle risorse non funziona come previsto (CQ-4275886).

* I flussi di lavoro di rendering non riescono (CQ-4271928).

* DAM Event Purge elimina i dati dell’evento più recente (`maxSavedActivities`) e contiene i dati creati in precedenza (NPR-31336).

* La pagina dei risultati della ricerca nell’interfaccia touch (tramite Omnisearch) scorre automaticamente verso l’alto e perde la posizione di scorrimento dell’utente (NPR-31307).

* La barra delle azioni e il conteggio delle risorse non vengono aggiornati quando si selezionano tutti gli elementi e poi si deseleziona alcuni elementi (cartelle/singole risorse) nell’interfaccia utente touch (NPR-31118).

* Viene visualizzata un&#39;eccezione in [!DNL Experience Manager] durante il polling dei dettagli del processo di una risorsa (CQ-4283569).

### Sites

* Se l’ereditarietà Live Copy è interrotta, nelle pagine Live Copy vengono visualizzati i collegamenti di copia per lingua invece dei collegamenti LiveCopy (NPR-30980).
* Per una nuova blueprint, se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza le righe vuote per il resto dei record (NPR-31182).
* Quando un utente aggiunge caratteri giapponesi o coreani nella proprietà description di un menu, nel menu vengono visualizzati caratteri distorti per il testo in giapponese e coreano (NPR-31331).
* L’Editor Rich Text non consente di inserire una tabella incorporata come voce di elenco (NPR-30879).
* Con l’editor Rich Text (scaffolding Rich Text Editor), puoi iniziare a utilizzare i contenuti predefiniti. applica in modo imprevisto le dimensioni del font in linea agli elementi (NPR-31284).
* Quando un utente usa i campi della barra a sinistra e una scelta rapida da tastiera per incollare il contenuto, viene incollato il contenuto degli Appunti dell’Editor pagina invece del contenuto copiato dai campi della barra a sinistra (NPR-31172).
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso immagine viene memorizzato nel nodo del componente anziché nel nodo multicampo (NPR-30882).
* L&#39;API `ResponsiveGridExporter` non restituisce l&#39;interfaccia `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. Il pacchetto `com.day.cq.wcm.foundation.model.impl` è dichiarato come pacchetto privato (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il prefisso `editor.html` e `wcmmode=disabled` o in Publisher)., la richiesta termina con il codice di errore di stato HTTP `500` (NPR-30743).
* Gli utenti non possono modificare la password e accedere alla pagina del profilo (NPR-31161).

### Ricerca e interfaccia utente {#ui-interface-and-search}

* Quando si passa dalla visualizzazione a schede alla visualizzazione a elenco in una pagina dei risultati di ricerca, si verifica un ritardo prima dello scorrimento della pagina (NPR-31286).

* La casella di controllo [!UICONTROL Seleziona tutto] è nascosta nella vista a elenco nell&#39;interfaccia utente [!DNL Sites] (NPR-31614).

* Il conteggio [!UICONTROL Seleziona tutto] in una pagina dei risultati di ricerca non è corretto (NPR-31120).

* L’editor di metadati visualizza i tag che non esistono (NPR-31119).

### Traduzione {#translation}

* Due pop-up del calendario vengono visualizzati quando si seleziona l’opzione Data di scadenza in un processo di traduzione (NPR-31270).

### Piattaforma

* L’opzione Tipo MIME nella console Web non funziona (NPR-31108).

* Il certificato client non viene accettato durante la configurazione del single sign-on (NPR-31165).

* Gli aggiornamenti nella configurazione della dimensione del buffer per il servizio HTTP basato su Jetty non vengono salvati (NPR-30925).

* QueryBuilder supporta ora l’ordine `fn:name()` nelle query xpath (NPR-31322).

* La struttura di attivazione duplicata viene creata all&#39;aggiornamento da [!DNL Experience Manager] 6.3 (NPR-31513).

* Le richieste inoltrate non conservano le intestazioni di risposta impostate durante l’autenticazione sling (NPR-30013).

* La ricerca all’interno dei componenti del selettore non funziona (NPR-31692).

* Viene visualizzato un errore durante l’associazione di un file ZIP a un post [!DNL Experience Manager Communities] a causa di diverse versioni del bundle Apache POI e Apache Tika (NPR-31018).

* Il bundle `org.apache.sling.distribution.api` è nascosto nel gestore della configurazione e quindi non è disponibile per i bundle personalizzati (NPR-31720).

### Progetti

* Il cambiamento delle visualizzazioni del calendario non funziona (NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**Miglioramenti apportati al prodotto**

* Il flusso di lavoro di importazione di Asset Sourcing in [!DNL Experience Manager Assets] viene modificato per recuperare solo le risorse appena create da [!DNL Brand Portal] a [!DNL Experience Manager] e per evitare la replica le risorse già esistenti nella nuova cartella (CQ-4278527).

**Problemi risolti**

* Quando si crea una nuova cartella Contribution nella funzione Asset Sourcing, viene visualizzata un’icona errata. (CQ-4282825)
* Quando si crea una nuova cartella Contribution, una o entrambe le sottocartelle (NEW e SHARED) non vengono visualizzate all’interno della cartella Contribution (CQ-4282424).
* Il sistema genera un’eccezione se l’utente tenta di ripubblicare la cartella Contribution da [!DNL Experience Manager] a [!DNL Brand Portal] dopo aver ricevuto nuove risorse nella cartella Contribution da [!DNL Brand Portal] end (CQ-4279740).
* La creazione di una cartella Contribution all’interno di una cartella Contribution (cartella nidificata) non è consentita per evitare complessità (CQ-4278391).
* Il sistema genera un&#39;eccezione durante il caricamento dell&#39; [!DNL Brand Portal] elenco utenti (.csv file) importato dall&#39;Admin Console [!DNL Experience Manager]. Solo i campi Email, FirstName e LastName nel file .csv sono obbligatori (CQ-4278390).

### Community {#communities-6530}

**Problemi risolti**

* I collegamenti rapidi per gestire i gruppi (gruppi di apertura/modifica/pubblicazione/eliminazione) non sono visibili agli amministratori della community (amministratore di gruppo/amministratore del sito) (NPR-31627).
* Un blog inviato viene visualizzato solo se la pagina viene aggiornata/ricaricata manualmente (NPR-31599).
* La query JCR utilizzata dalla funzione &quot;Riferimenti&quot; è sensibile a maiuscole e minuscole e richiede troppo tempo per restituire i risultati (NPR-31475).
* [!DNL Experience Manager] Il file 6.5 UberJar genera un&#39;eccezione,  `cq-social-translation` bundle mancante dal file  [!DNL Experience Manager] 6.5 UberJar (NPR-31186).
* Librerie di Databind Jackson aggiornate alla versione 2.9.9.3 per risolvere nuove vulnerabilità (NPR-30967).
* I titoli di Attività e Notifiche non sono coerenti (NPR-30941).
* L&#39;impaginazione non funziona correttamente nei blog [!DNL Communities] (NPR-30914).
* I rapporti di Analytics non vengono compilati nell’ [!DNL Experience Manager] ambiente di authoring, viene visualizzata una pagina vuota (NPR-30913).

### Oak {#oak}

* Gli aggiornamenti dell&#39;indice Lucene causano il rallentamento del server di authoring (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per  [!DNL Experience Manager Forms]. Tali correzioni vengono distribuite utilizzando un pacchetto separato di componenti aggiuntivi per Forms. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per [!DNL Experience Manager Forms] su JEE. Per ulteriori informazioni, consulta [Installare il componente aggiuntivo Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Pacchetto di componenti aggiuntivi per Forms {#forms-add-on-package-6530}

**Moduli adattivi**

* Le stringhe contengono la chiave del dizionario durante la localizzazione dei moduli adattivi (NPR-31110).

**Comunicazione interattiva**

* **MissingNode.toString()** restituisce risultati imprecisi dopo l’aggiornamento delle librerie Jackson a 2.10.0 (NPR-31549).

* L’editor di testo rimuove in modo casuale i caratteri di spazio dal testo copiato da Microsoft Word (NPR-31113).

**Gestione della corrispondenza**

* Le didascalie e le descrizioni dei comandi non vengono visualizzate durante la migrazione delle lettere da LiveCycle ES4SP1 a [!DNL Experience Manager] 6.5 (NPR-31615).

* **La formattazione del flusso di testo non è più** supportata durante il salvataggio delle lettere come bozze (NPR-30463).

**Flusso di lavoro**

* Il flusso di lavoro OSGi non riesce a causa dell&#39;utilizzo della CPU al 100% (NPR-31233).

**Moduli HTML5**

* Quando si genera l’anteprima HTML5 di un modulo XDP, viene visualizzato uno sfarfallio durante l’aggiunta di istanze di un sottomodulo (NPR-30909).

#### Modulo di installazione di Forms su JEE {#forms-jee-installer-6530}

**Forms - Servizi basati su documenti**

* Il servizio Web SOAP che utilizza MTOM in un progetto .NET visualizza le eccezioni per i metodi di chiamata AssemblerServiceClient e HtmlToPDF2 (NPR-4281771).

* Vulnerabilità di sicurezza 2012-5784 e 2014-3596 trovata con JAR AXIS 1.4 e corretta fornita con [AXIS1.4.1 jar](https://helpx.adobe.com/it/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015).

**JEE per Foundation**

* La configurazione dell&#39;azione non carica i nomi dei processi per Richiamare un&#39;azione di invio di un Forms Workflow (NPR-31478).

### Feature Pack inclusi {#feature-packs-included-6530}

>[!NOTE]
>
>Per i clienti [!DNL Experience Manager Forms], è essenziale installare il pacchetto aggiuntivo [!DNL Experience Manager Forms] dopo aver installato qualsiasi Service Pack, Cumulative Fix Pack o Feature Pack [!DNL Experience Manager].

#### Forms - JEE di base {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Supporto Forms per Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 è una versione importante che include miglioramenti e correzioni a livello di prestazioni, stabilità, sicurezza e problemi segnalati dai clienti, introdotti successivamente alla data di disponibilità generale di  [!DNL Adobe Experience Manager] 6.5 di  **aprile 2019**. Può essere installato su [!DNL Experience Manager] 6.5.

Alcuni elementi di rilievo di questa versione del Service Pack sono:

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.10.3.
* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per [!DNL Adobe Target].
* Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Consulta la sezione sull’[utilizzo di risorse collegate](../assets/use-assets-across-connected-assets-instances.md).

* Il tipo EnhanceDocument filtra con più tipi MIME per supportare opzioni con più valori.
* Introduzione di un flusso di lavoro Rielabora esterno per il supporto di più risorse.
* Prestazioni ottimizzate [!DNL Dynamic Media] utilizzando filtri risorse predefiniti per la replica.
* Ripristino delle opzioni di modifica di Assets relative a ritaglio/rotazione per DMS7.
* Implementazione di un’opzione per la disattivazione audio di un video durante il caricamento in VideoPlayer.
* Implementazione di una correzione per fare in modo che nella vista a colonne dell’interfaccia utente di Assets sia visualizzato solo il contenuto specifico del tenant.
* Implementazione di una correzione per consentire che le modifiche del pannello a soffietto dello stile rispecchino i risultati della ricerca.

### Risorse

**Miglioramenti apportati al prodotto**

* Miglioramento della funzionalità Risorse collegate per aggiungere il supporto per il recupero di documenti da implementazioni DAM remote. Gli autori di siti possono ora cercare e filtrare i tipi di documenti supportati in Content Finder. I documenti remoti possono essere aggiunti al componente Download nelle pagine Web. Hotfix per CQ-4270245. Consulta la sezione sull’[utilizzo di risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets]Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di [!DNL Experience Manager]Dall’archivio DAM,  visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. Consulta la sezione sulla [ricerca visiva](../assets/search-assets.md#visualsearch).

**Problemi risolti**

* I percorsi delle risorse negli URL e i metadati delle cartelle generati dall’API ACP non sono codificati in URL. GRANITE-26198: Hotfix per CQ-4271814
* Non è possibile aprire un archivio con una cartella il cui nome contiene un segno di percentuale (%) utilizzando l’interfaccia [!DNL Experience Manager Assets]. NPR-29989: Hotfix per CQ-4270467
* Interfaccia touch: Durante la procedura guidata gestisci pubblicazione, i riferimenti vengono aggiunti dopo la pagina nel corpo della richiesta di pubblicazione, causando la pubblicazione di tutte le risorse dopo la pagina e, quando la pagina viene riprodotta, alcune risorse nell’istanza di pubblicazione vengono perse. NPR-29985: Hotfix per CQ-4270724
* La funzione Scollega di Assets non funziona per le risorse correlate il cui nome contiene caratteri speciali (caratteri che diventano con codifica URI). NPR-30387: Hotfix per CQ-4274446
* Quando si modifica un frammento di contenuto, la versione viene creata con l’utente errato.
* Errore durante la creazione di raccolte nel sistema basato su tenant. NPR-30114: Hotfix per CQ-4272948
* La vista a colonne dell’interfaccia utente di Assets non rispetta il percorso principale DAM del tenant corrente, ma accede a tutti i percorsi DAM del tenant. NPR-30636: Hotfix per CQ-4275481
* Possibilità di attacchi che sfruttano la vulnerabilità cross-site scripting (XSS) tramite la finestra di avviso File con limitazioni, in quanto l’immagine inserita può risultare visibile. NPR-30617: Hotfix per CQ-4270133
* MultiTenant: I tenant che salvano le proprietà della cartella osservano sia il prompt di successo che il messaggio di errore che descrive l’azione non è riuscita, &quot;Impossibile modificare le proprietà. Autorizzazioni insufficienti.” e questo genera confusione. NPR-30545: Hotfix per CQ-4275333
* La finestra di dialogo di Selettore risorse non consente la selezione della risorsa, pertanto non è possibile aggiornare l’origine utilizzando la funzionalità di sostituzione dell’origine correlata. NPR-30502: Hotfix per CQ-4275029
* [!UICONTROL DAM Update ] Asset Workflow - Lo stato non aggiornato sul caricamento di file mp4 di grandi dimensioni. NPR-30480: Hotfix per CQ-4271352
* La funzionalità Crea attività di revisione non funziona a causa di un payload nullo che impedisce il completamento di tutte le azioni successive correlate all’attività di revisione. NPR-30468: Hotfix per CQ-4274263
* Problema di connettività di Tag avanzati di Adobe tramite DataPower. NPR-30026: Hotfix per CQ-4269457
* Nella vista a colonne dell’interfaccia utente di Assets viene generato un errore quando si prova ad aprire i filtri nella barra a sinistra. NPR-30501: Hotfix per CQ-4273862
* Quando si aggiungono gruppi sincronizzati da LDAP nelle proprietà di Gruppo utenti chiuso di una cartella risorse, il gruppo non viene salvato e recuperato. NPR-30615: Hotfix per CQ-4274689
* I campi di orientamento e stile per la ricerca con filtro non applicano il valore di completamento automatico alla query di ricerca. NPR-30620: Hotfix per CQ-4275724
* Con il collegamento di Condivisione risorse di una cartella il cui nome include spazi e il carattere “&amp;” vengono visualizzate schede grigie vuote per alcune risorse. NPR-30557: Hotfix per CQ-4270187
* Il modulo dello schema dei metadati della cartella non rileva automaticamente il tipo di dati e, di conseguenza, non crea l’elemento TypeHint correlato nell’invio del modulo. NPR-30599: Hotfix per CQ-4275227
* Le opzioni di modifica di Assets relative a ritaglio e rotazione vengono disabilitate dall’interfaccia utente di authoring di DMS7. NPR-30118: Hotfix per CQ-4273221
* La funzione Condividi collegamento non funziona sull&#39;istanza [!DNL Experience Manager] con la configurazione DMS7. NPR-30080, NPR-30492: Hotfix per CQ-4273651
* L’aggiunta del componente [!DNL Dynamic Media]-Scene7 alla pagina e la pubblicazione della pagina non attiva ogni volta la configurazione dmscene7. NPR-30641: Hotfix per CQ-4275962
* È stato aggiunto un IPSJobJournal in [!DNL Experience Manager] per creare un solo processo IPS (Intrusion Prevention Systems) per profilo di elaborazione. NPR-30490: Hotfix per CQ-4273614
* [!DNL Dynamic Media]: Aggiunta di filtri predefiniti per escludere le risorse dalla replica nel nodo di Publish. [!DNL Experience Manager] NPR-30538: Hotfix per CQ-4274678
* Introduzione di un flusso di lavoro Rielabora esterno per supportare più risorse e consentire la creazione della cartella come payload. Il flusso di lavoro prevede due passaggi: rielaborazione delle risorse senza alcun handle tramite la mappatura dei metadati al passaggio successivo e ricaricamento di tutte le risorse senza handle di risorsa a S7 in un singolo processo IPS. Per ulteriori dettagli, consulta Configurazione dei Cloud Services [!DNL Dynamic Media] . NPR-30489: Hotfix per CQ-4272903
* Caricamento di un CSV non corretto dopo la cancellazione del CSV corretto. Hotfix per CQ-4277694, CQ-4277814
* Icona errata specifica delle cartelle contributi da rimuovere. Hotfix per CQ-4277580
* Selezionando un utente nel selettore utenti della scheda Contributo risorse, il nome dell’utente non viene visualizzato nella tabella e nella pagina delle proprietà della finestra di dialogo Elimina utente viene visualizzato testo errato. Hotfix per CQ-4277875
* Non è possibile aggiungere collaboratori alla cartella Contributo risorse dal selettore utente selezionando l’utente e facendo clic su Aggiungi. Hotfix per CQ-4277824, CQ-4278087
* La ricerca per nome utente in minuscolo non funziona nel selettore utente. Hotfix per CQ-4277958, CQ-4277930
* Gli utenti non amministratori possono pubblicare risorse in una nuova cartella di una cartella Contributo risorse. Hotfix per CQ-4278200
* L’utente DAM (non amministratore) non può scegliere di aggiungere collaboratori alla cartella Contributo risorse. Hotfix per CQ-4278192
* Il pulsante “Crea” è visibile nella cartella Contributo risorse. Hotfix per CQ-4277560
* L’ordinamento della query di ricerca in base alla pertinenza restituisce i documenti [!DNL InDesign] insieme ai modelli [!DNL InDesign]. Hotfix per CQ-4273864
* Se l’utente dispone di un ID e-mail in maiuscolo, non potrà eseguire la consegna per le risorse ritirate in precedenza. Hotfix per CQ-4276575
* L’operazione Elimina si applica solo ai predefiniti selezionati; se la schermata aggiorna automaticamente l’elenco dopo l’operazione, vengono visualizzati altri predefiniti già aggiornati. Hotfix per CQ-4261461
* La configurazione dei Cloud Services [!DNL Dynamic Media] in modalità [!DNL Dynamic Media]-ibrida determina la creazione di più suite di rapporti vuote in [!DNL Analytics] e l’archiviazione dell’ID della suite di rapporti in [!DNL Experience Manager], con conseguente duplicazione della suite di rapporti. Hotfix per CQ-4249780
* L’operazione di ridenominazione in [!DNL Experience Manager] risorsa in nome duplicato non viene eseguita e non viene eseguita la sincronizzazione con Scene7. Hotfix per CQ-4276763
* I contenuti generati dall’utente non vengono visualizzati correttamente nel pannello del filtro di ricerca. Hotfix per CQ-4273875
* L’opzione Trova simile non è disponibile per le immagini TIFF. Hotfix per CQ-4278238
* Implementazione di un’opzione per disattivare l’audio dei video durante il caricamento in VideoPlayer. Hotfix per CQ-4266465
* Visualizzatori - VideoViewer: poster=none funziona in modo errato nel caso di un video esterno utilizzato. Hotfix per CQ-4265536
* L’icona di attesa è visibile durante la riproduzione video nei browser IE11 e MS Edge. Hotfix per CQ-4251539
* I file README dei visualizzatori 3.8 SDK e 5.13 non vengono aggiornati e contengono informazioni provenienti da versioni precedenti. Hotfix per CQ-4273737
* Viene creata una versione del frammento di contenuto ancor prima del salvataggio delle modifiche. NPR-30616: Hotfix per CQ-4273088
* Sostituzione di Asset#getMetadata(String) con Asset#getMetadataValueFromJcr(String) nel processo miniature. NPR-30491: Hotfix per CQ-4273067
* Il caricamento di un file jpg causa l’attivazione di più istanze del messaggio: “Replica di ReplicateOnModifyWorker AGGIORNATA” per ciascuna risorsa, causando un peggioramento delle prestazioni.
* La decompressione dell’archivio ZIP mediante la funzione Estrai archivio causa problemi con le cartelle il cui nome contiene il segno di percentuale (%) nel titolo. NPR-29990: Hotfix per CQ-4270467

### Sites {#sites-6520}

* Se l’ereditarietà Live Copy è interrotta, nelle pagine Live Copy vengono visualizzati i collegamenti di copia per lingua invece dei collegamenti LiveCopy (NPR-30980).
* Per una nuova blueprint, se il numero di record è superiore a 40, vengono visualizzati solo i primi 40 record. Blueprint visualizza le righe vuote per il resto dei record (NPR-31182).
* Il plug-in Editor Rich Text del componente Testo visualizza i caratteri distorti per il testo in giapponese e coreano (NPR-31331).
* L’Editor Rich Text non consente di inserire una tabella incorporata come voce di elenco (NPR-30879).
* L’Editor Rich Text (RTE) per scaffolding viene applicato in modo imprevisto alle dimensioni del font in linea agli elementi (NPR-31284).
* Quando un utente si concentra sui campi della barra a sinistra e utilizza una scelta rapida da tastiera per incollare il contenuto, incolla il contenuto degli Appunti dell’editor di pagine invece del contenuto copiato dai campi della barra a sinistra (NPR-31172).
* Quando un utente aggiunge un campo Caricamento file a un campo multiplo, il percorso immagine viene memorizzato nel nodo del componente anziché nel nodo multicampo (NPR-30882).
* L&#39;API `ResponsiveGridExporter` non restituisce l&#39;interfaccia `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. Il pacchetto `com.day.cq.wcm.foundation.model.impl` è dichiarato come pacchetto privato (NPR-31398).
* Quando una pagina contenente alcuni frammenti esperienza viene aperta in modalità non editor (in Author senza il prefisso `editor.html` e `wcmmode=disabled` o in Publisher), la richiesta termina con il codice di errore di stato HTTP 500 (NPR-30743).

### WCM - Editor pagina {#wcm-page-editor-6520}

**Miglioramenti apportati al prodotto**

* `EnhanceDocument` digita i filtri con più tipi MIME per supportare le opzioni con più valori. Hotfix per CQ-4270694

### Gestione dei frammenti di contenuto {#content-fragment-management-6520}

* La query utilizzata dall’interfaccia utente dei modelli di frammenti di contenuto è molto lenta e alla fine genera un errore. Hotfix per CQ-4270807

### Interfaccia utente - Foundation {#ui-foundation}

* Con l’attivazione dei tasti di scelta rapida l’utente non può usare i tasti m, p ed e all’interno di specifiche interfacce utente. NPR-30355: Hotfix per GRANITE-26346
* La chiusura dell’ [!DNL Experience Manager Assets] interfaccia utente di ricerca non reimposta la barra a sinistra sulla selezione del contenuto, impedendo all’utente di aprire la barra del filtro la seconda volta dopo. NPR-30509: Hotfix per CQ-4274716
* Ambiente multi-tenant: [!DNL Experience Manager Assets] La navigazione superiore nell&#39;interfaccia utente non è disponibile e viene generato un errore JavaScript. NPR-30104: Hotfix per GRANITE-26344

### Traduzione {#translation-6520}

* Problema di traduzione - Solo alcuni componenti vengono tradotti utilizzando la traduzione automatica. NPR-30079: Hotfix per CQ-4273764

### Piattaforma {#platform-6520}

* [!DNL Experience Manager]Il mittente predefinito di non è in grado di inviare messaggi a un server SMTP remoto tramite TLS v1.2. NPR-30476: Hotfix per GRANITE-26605

### Progetti {#projects-6520}

* I valori dam:folderThumbnailPaths non vengono aggiornati e vengono visualizzate miniature vecchie anche dopo l’eliminazione delle risorse nella cartella. NPR-30424: Hotfix per CQ-4273667
* Quando si completa l’opzione “Sposta”, titolo e nome della risorsa restano invariati. NPR-30647: Hotfix per CQ-4276265

### Community {#communities-6520}

* Diagnostica sincronizzazione utenti è danneggiato e non funziona. NPR-30004, NPR-29943: Hotfix per CQ-4270287, CQ-4271348

### Sling {#sling}

* In seguito all’aggiornamento dell’istanza dalla versione 6.3.3.2 alla versione 6.5 vengono create configurazioni OSGi duplicate. NPR-30130: Hotfix per CQ-4274016

### Integrazione

* Il contenuto personalizzato non viene visualizzato correttamente nell’istanza di pubblicazione fino al riavvio dell’istanza. NPR-30377: Hotfix per CQ-4273706
* Durante la configurazione di Launch in un sito Web, l’indirizzo della libreria è preceduto da una barra (/) e questo causa ogni volta la necessità di un intervento manuale. NPR-30694: Hotfix per CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack non include correzioni per  [!DNL Experience Manager Forms]. Vengono distribuite utilizzando un pacchetto aggiuntivo [!DNL Forms] separato. Inoltre, viene rilasciato un programma di installazione cumulativo che include correzioni per [!DNL Experience Manager Forms] su JEE. Per ulteriori informazioni, consulta [Installare il componente aggiuntivo Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) e [Installare Forms Experience Manager su JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

Elementi di rilievo dei moduli [!DNL Experience Manager] 6.5.2.0:

* È stata aggiunta l’impostazione &quot;Auto&quot; a `RenderAtClient` nell’API `PDFFormRenderOptions` per [!DNL Experience Manager] Forms OSGi.

#### Pacchetto di componenti aggiuntivi per Forms

**Integrazione back-end**

* Impossibile configurare il modello dati del modulo utilizzando un URL con bilanciamento del carico ospitato da AWS. NPR-30123: Hotfix per CQ-4273359
* Durante la creazione del modello dati del modulo (FDM) con il linguaggio WSDL (Web Service Definition Language), viene restituito il messaggio di errore `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type`: NPR-30477: Hotfix per CQ-4272921

**Gestione della corrispondenza**

* &quot;Il rendering dell’interfaccia utente per la corrispondenza (interfaccia utente CCR) non riesce a intermittenza con il seguente errore nella console:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Comunicazione interattiva**

* Un campo contrassegnato come obbligatorio nel modello dati del modulo viene visualizzato come obbligatorio nell’interfaccia utente di Crea corrispondenza (interfaccia utente CCR). NPR-30623: Hotfix per CQ-4274902

**Forms - Flusso di lavoro**

* Le variabili di output non mappate in cartelle esaminate causano errori di chiamata. Hotfix per CQ-4264451

**Moduli HTML5**

* Quando il codice o il progetto personalizzato viene distribuito per la seconda volta, la pagina non esegue il rendering e si verifica il seguente errore:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: Hotfix per CQ-4272509

* Quando si utilizza l’accesso desktop non visivo in modalità Sfoglia per leggere un modulo HTML5, il browser Chrome legge l’elemento “grafico” prima di qualsiasi file SVG nella struttura del modulo. NPR-30449: Hotfix per CQ-4274732

#### Programma di installazione JEE per Forms

**Forms - Sicurezza dei documenti**

* L’applicazione di una firma con marca temporale non riesce e viene restituito l’errore: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: Errore di chiamata. NPR-30820: Hotfix per CQ-4275852

**Forms - Servizi basati su documenti**

* Se &quot;SubmitURL&quot; contiene una e commerciale (&amp;), nel registro vengono visualizzati errori di analisi quando si effettua la richiesta di POST al servlet `renderpdf`. NPR-30865: Hotfix per CQ-4278232

**Forms - JEE di base**

* Il servizio HTMLtoPDF non mostra maxReuseCount nella console JMX. NPR-30134, NPR-30304: Hotfix per CQ-4273763
* L&#39;aggiunta o la modifica di una connessione a un servizio Web richiamando i servizi Web da [!DNL Experience Manager Forms] Workbench genera un errore: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Hotfix per CQ-4273217

### Feature Pack inclusi

>[!NOTE]
>
>Per i clienti [!DNL Experience Manager Forms], è essenziale installare il pacchetto aggiuntivo [!DNL Experience Manager Forms] dopo aver installato qualsiasi Service Pack, Cumulative Fix Pack o Feature Pack [!DNL Experience Manager].

#### Sites {#sites-feature-packs-included}

* Aggiunta di una proprietà di configurazione per consentire l’esportazione di Frammenti esperienza direttamente in aree di lavoro definite dall’utente per [!DNL Adobe Target]. NPR-29189: Hotfix per CQ-4249782

#### Forms - Servizi basati su documenti {#forms-document-services-1}

* È stata aggiunta l’impostazione &quot;Auto&quot; a `RenderAtClient` nell’API `PDFFormRenderOptions` per [!DNL Experience Manager Forms] OSGi. NPR-30759: Hotfix per CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 è una versione importante che include miglioramenti e correzioni a livello di prestazioni, stabilità, sicurezza e problemi segnalati dai clienti, introdotti successivamente alla data di disponibilità generale di  [!DNL Adobe Experience Manager] 6.5 di  *aprile 2019.* Può essere installato sulla versione  [!DNL Experience Manager] 6.5.

Alcuni elementi di rilievo di questa versione del Service Pack sono:

* Abilitazione dell’inclusione dello stato dell’interfaccia utente dinamica negli eventi di tracciamento come attributi personalizzati.
* È stato incluso il supporto per la distribuzione di risorse video a 360 gradi in modalità [!DNL Dynamic Media]-Scene7.
* Abilitazione della funzione *Parola giapponese Wrap* tramite il plug-in Stili dell’Editor Rich Text. Per ulteriori informazioni, consulta [Configurare il ritorno a capo automatico in giapponese](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Risorse

* Aggiornamento dell’interfaccia DMGateway di DAM per il supporto multipart di S3. NPR-29740: Hotfix per CQ-4226303
* L’anteprima delle rappresentazioni genera un errore `Only empty tenantId is currently supported` dopo l’aggiornamento a [!DNL Experience Manager] 6.5. NPR-29986: Hotfix per CQ-4272353
* La finestra di dialogo Elimina non è visibile per consentire l’eliminazione di lavori. NPR-29720: Hotfix per CQ-4271074
* Dopo aver aggiunto il titolo della risorsa nella pagina delle proprietà, quando un utente tenta di chiudere la pagina, [!DNL Experience Manager] riapre la pagina delle proprietà. NPR-29627: Hotfix per CQ-4264929
* VersioningTimelineEventProvider deve fornire la versione principale unitamente al nodo della versione nt: del tipo. Hotfix per GRANITE-26063
* È stata implementata la possibilità di caricare e riprodurre video sferici a 360° in modalità [!DNL Experience Manager] DM-Scene7. Hotfix per CQ-4265131
* Live Copy recupera lo stato non corretto in caso di modifica dell’origine. Hotfix per CQ-4265451
* Abilitazione del supporto per l’utilità di gestione di più siti per [!DNL Experience Manager Assets]. Hotfix per CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] l’interfaccia di deve visualizzare una voce aggiuntiva per la versione corrente della risorsa nella cronologia della timeline, mostrando l’ultimo commento di archiviazione da  [!DNL Adobe Asset Link]. Hotfix per CQ-4262864
* La Timeline dei frammenti di contenuto visualizza un messaggio di errore quando mancano le proprietà. Hotfix per CQ-4272560
* Problema relativo al lettore video di Scene7 quando viene espanso a schermo intero. Hotfix per CQ-4266700
* ZoomVerticalViewer: i pulsanti di spostamento non devono essere visualizzati se viene utilizzata una singola risorsa immagine. Hotfix per CQ-4264795
* Se si elimina un nodo figlio nella Live Copy, è necessario scollegare liveRelationship. Hotfix per CQ-4270395
* Lo schema di metadati contiene solo elementi della configurazione globale; quelli del tenant attivo non sono presenti. Il valore dell’URL di formPath viene ripristinato a quello predefinito anche se modificato. NPR-29945: Hotfix per CQ-4262898
* La pubblicazione dei predefiniti immagine in [!DNL Brand Portal] non riesce con un codice di errore 500. NPR-29510: Hotfix per CQ-4268659

### Sites

* Le proprietà vuote e multiple non vengono propagate dalla blueprint durante il rollout. Il ripristino di Live Copy con la blueprint non funziona per i componenti. NPR-29253: Hotfix per CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, se utilizzato con `Multifield`, memorizza il `fileReferenceParameter` a livello di componente invece che a livello di campo multiplo. NPR-29537: Hotfix per CQ-4266129
* Miglioramento del componente di testo [!DNL Experience Manager] e dell’editor di testo in giapponese. NPR-29785: Hotfix per CQ-4265090
* La pagina ripristinata con Timewarp deve fare riferimento all’immagine corretta al momento del controllo delle versioni. NPR-29431: Hotfix per CQ-4262638
* Problema relativo all’ereditarietà dei nodi del sistema di stili da padre a figlio. NPR-29516: Hotfix per CQ-4270330
* Messaggio di errore durante l&#39;impostazione dell&#39;autenticazione per il post social su [!DNL Facebook] . NPR-29211: Hotfix per CQ-4266630
* La miniatura di cui è stato eseguito il rendering nel frammento di contenuto mostra la rappresentazione interna del calendario per il campo Data e ora. NPR-29531: Hotfix per CQ-4269362
* All’apertura della scheda Autorizzazioni nell’implementazione di Coral2 non viene visualizzato alcun pulsante. Hotfix per CQ-4269419

### Commerce

* ConstraintViolationException durante l’esecuzione della migrazione lenta dei contenuti per l’e-commerce. NPR-29247: Hotfix per CQ-4264383

### Gestione dei frammenti di contenuto

* Errore di analisi durante l’apertura di un frammento di contenuto con caratteri dollaro `($)` e parentesi graffa aperta `({)`. Hotfix per CQ-4270266

### Frammenti di esperienza

* Esporta [!DNL Experience Manager] Frammenti esperienza in [!DNL Adobe Target]. Hotfix per CQ-4265469
* L’esportazione dei frammenti esperienza in target non riesce con l’immagine intelligente. Hotfix per CQ-4269606

* L’utente rimane bloccato quando prova a spostare i frammenti esperienza tramite Omnisearch nella vista a schede. Hotfix per CQ-4263848

### WCM - Editor pagina

* Vulnerabilità cross-site scripting (XSS) rilevabile quando si utilizza un selettore non valido. Hotfix per CQ-4270397

### Replica

* I dati forniti dall’utente non sono preceduti dall’escape nell’output nel componente `cq/replication/components/agent` e causano la memorizzazione di una vulnerabilità cross-site scripting (XSS). Hotfix per CQ-4266263

### Flusso di lavoro

* Il campo del selettore del calendario di Partecipante finestra di dialogo è danneggiato. NPR-29727: Hotfix per CQ-4270423

### WCM - Editor SPA

* Abilitazione del recupero da un endpoint remoto di contenuti di cui è già stato eseguito il rendering. Hotfix per CQ-4270238
* Aggiunta di avvisi nei registri quando viene aperta una pagina di modello per applicazione a pagina singola di cui viene eseguito il rendering sul lato server. Hotfix per CQ-4270238

### WCM - MSM

* Con l’aggiornamento a [!DNL Experience Manager] 6.4.3, il rollout di Multi-Site Manager richiede molto tempo. Hotfix per CQ-4271410

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

* La pubblicazione di [!DNL Experience Manager Assets] dalla cartella /content/dam/mac a [!DNL Brand Portal] non funziona. [!DNL Experience Manager] NPR-29819: Hotfix per CQ-4271118

### Piattaforma

* HtmlLibraryManager elimina tutti i contenuti di crx-quickstart in seguito all’annullamento della validità della cache. NPR-29863: Hotfix per GRANITE-26197

### Felix

* I dettagli sull’utilizzo della memoria non vengono visualizzati nella console del sistema quando si utilizza Java 11\. NPR-29669

### Forms

Gli elementi di rilievo di [!DNL Experience Manager Forms] 6.5.1.0 sono:

* Solo OSGi: È stato aggiunto un nuovo attributo `PAGECOUNT` in Output e Forms Service.

* Solo OSGI: Abilitazione del supporto per la creazione di file PDF statici tramite Forms Service.
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root.
* Abilitazione del supporto per ADFS v3.0 per l’integrazione On-Premise di Dynamics.

#### Pacchetto di componenti aggiuntivi per Forms

**Integrazione con il back-end**

* Errore durante il recupero del linguaggio WSDL (Web Service Definition Language) protetto. NPR-29944: Hotfix per CQ-4270777
* Quando [!DNL Experience Manager Forms] è installato su IBM WebSphere, la creazione di un modello di dati del modulo basato su SOAP non riesce. Hotfix per CQ-4251134
* Abilitazione del supporto per ADFS (Active Directory Federation Services) v3.0 per l’integrazione On-Premise di Microsoft Dynamics. Hotfix per CQ-4270586
* Quando si modifica il titolo di un’origine dati, il modello dati del modulo non visualizza il titolo aggiornato. Hotfix per CQ-4265599
* Se il nome di un&#39;entità o di un attributo contiene trattini o spazi, le espressioni non riescono a valutare tali entità e attributi. Hotfix per CQ-4225129

* Viene osservato un output errato quando nell&#39;output della stringa primitiva sono presenti due punti. Hotfix per CQ-4260825

* Anche quando non è previsto alcun contenuto dall’output dell’API REST, l’operazione di richiamo del modello dati del modulo genera un errore. Hotfix per CQ-4268828

**Moduli adattivi**

* Impossibile aggiungere una nuova istanza nel frammento di modulo adattivo durante il caricamento lento. NPR-29818: Hotfix per CQ-4269875
* Il componente Verifica non registra o visualizza errori per i modelli della documentazione. Hotfix per CQ-4272999
* Aggiunta del supporto per disabilitare l’editor di layout per Moduli adattivi. Hotfix per CQ-4270810
* Ripristino del passaggio di verifica per Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix per CQ-4269583

* L’errore di convalida del campo del modulo adattivo si interrompe [!DNL Adobe Sign]. Hotfix per CQ-4269463
* Quando un’istanza [!DNL Experience Manager Forms] include più di 20 frammenti di modulo adattivo e il nome di tutti i frammenti di modulo inizia con la stessa stringa, la ricerca non restituisce alcun frammento o restituisce solo 20 frammenti creati di recente. Hotfix per CQ-4264414, CQ-4264914

* Problemi di prestazioni quando l’app Moduli adattivi viene utilizzata con set di dati di grandi dimensioni. . Hotfix per CQ-4235310

* Se l’accesso viene effettuato tramite un account anonimo in un’istanza pubblicata, lo script GuideRuntime non viene caricato. Hotfix per CQ-4268679

**Forms - Comunicazione interattiva**

* Il modello di comunicazione interattiva non elenca i componenti intestazione e piè di pagina nell’elenco dei componenti consentiti. Hotfix per CQ-4237895
* Quando crei un modello di stampa per comunicazioni interattive contenente un campo immagine, il titolo del grafico è impostato su una stringa vuota. Hotfix per CQ-4264772
* Il colore della linea di un grafico, se eliminato, è impostato su non definito. Hotfix per CQ-4264762
* Le modifiche al livello di layout apportate al frammento del documento scompaiono quando si esegue la sincronizzazione delle modifiche. Hotfix per CQ-4266054
* L’elemento del modello dati modulo all’interno di un frammento di documento associato a un campo di testo non visualizza l’icona di ereditarietà e consente l’associazione. Hotfix per CQ-4261089
* L’API di rendering del canale di stampa non include l’opzione per passare dati come parametro nell’API. Hotfix per CQ-4263540
* Le impostazioni dell&#39;agente non sono visibili in quanto la casella di controllo Modificabile dall&#39;agente viene deselezionata quando il tipo di binding viene modificato da Frammento di testo a Nessuno/Oggetto modello dati per campo/variabile stringa. Hotfix per CQ-4261953
* Durante l’invio dell’interfaccia utente dell’agente, il file json dei dati web risultante memorizza le informazioni per i campi non associati annullati dall’ereditarietà. Hotfix per CQ-4265621

**Forms - Flusso di lavoro**

* Quando un modulo viene nuovamente inviato dalla casella in uscita dell’app Moduli adattivi, si verifica una perdita di dati. NPR-28345: Hotfix per CQ-4260929
* I documenti non vengono chiusi durante il salvataggio per i casi non variabili. Hotfix per CQ-4269784
* L’app Moduli adattivi non supporta più Microsoft Windows 8.1. Hotfix per CQ-4265274
* Quando un’immagine di dimensioni superiori a 2 MB viene associata a un modulo come allegato a livello di campo nella versione Android di [!DNL Experience Manager Forms] app, l’app subisce un arresto anomalo. Hotfix per CQ-4265578

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

* [!DNL Experience Manager Forms] 6.5 Impossibile aprire la corrispondenza creata con la versione  [!DNL Experience Manager Forms] 6.3. Hotfix per CQ-4266392
* La funzione di somma in XDP non funziona se i dati DDE sono di tipo numero. Hotfix per CQ-4227403
* La logica di annullamento validità della cache in memoria delle lettere deve essere aggiornata, perché quando viene pubblicata una risorsa, l’ora dell’ultima modifica non viene aggiornata. Hotfix per CQ-4250465
* Impossibile pubblicare il frammento di documento, DD e lettere. Hotfix per CQ-4272893

#### Programma di installazione JEE per Forms

**PDF Generator**

* La conversione di file CAD in PDF non riesce con JDK a 64 bit. NPR-29924, NPR-29925: Hotfix per CQ-4272113
* Sostituzione del nome di PhantomJS in WebToPDF per la conversione HTMLtoPDF. NPR-29933: Hotfix per CQ-4234545
* Viene generato un errore durante la conversione del file ZIP in PDF. Hotfix per CQ-4268628

**Forms - Designer**

* Quando si esegue un controllo di accessibilità completo sul PDF statico creato utilizzando [!DNL Experience Manager Forms Designer], il controllo della lingua principale non riesce a causa di un attributo di lingua mancante. Hotfix per CQ-4272923, CQ-4271002

**Forms - Sicurezza dei documenti**

* La firma digitale con il modulo di sicurezza hardware non funziona in OSGi Linux su Java 11 e Java 8\. NPR-29838: Hotfix per CQ-4270441
* La firma digitale con il modulo di sicurezza hardware non funziona in JEE Linux e in tutti i server app supportati, ad esempio JBoss e Websphere. NPR-29839: Hotfix per CQ-4266721
* Durante la verifica delle firme in un PDF tramite l’uso di firme elettroniche avanzate PDF (PAdES) viene generata l’eccezione InvalidOperationException. NPR-29842: Hotfix per CQ-4244837
* Aggiunta del supporto per Document Security Extension per Office 2019\. Hotfix per CQ-4254369, CQ-4259764

**Forms - Servizi basati su documenti**

* La conversione del PDF in PDF/A-1b non riesce e il campo Modulo non dispone di un codice di aspetto. NPR-29940: Hotfix per CQ-4269618

* OSGi: Impossibile determinare il numero di pagine generate durante il rendering. NPR-28922: Hotfix per CQ-4270870
* Abilitazione del supporto per i file PDF statici tramite il servizio Forms in [!DNL Experience Manager Forms OSGi]. NPR-28572: Hotfix per CQ-4270869
* Impossibile modificare le autorizzazioni per XMLForm.exe. NPR-29828, NPR-29237: Hotfix per Q-4267080
* Il PDF statico creato dal modulo di output del server [!DNL Experience Manager Forms] non compila l&#39;attributo/tag della lingua con la lingua del documento creato. NPR-27332: Hotfix per CQ-4271002

**Forms - JEE di base**

* Il file pdfg_srt non è disponibile negli artefatti finali e questo impedisce l’esecuzione del programma di installazione. NPR-29854: Hotfix per CQ-4270137
* LCBackupMode.sh non funziona. NPR-29840: Hotfix per CQ-4269424
* È necessario rimuovere il riferimento alla porta UDP dall’interfaccia utente per WebSphere. Hotfix per CQ-4264782

### Feature Pack inclusi

#### Risorse - Incluso

* Abilitazione del supporto per l’utilità di gestione di più siti per [!DNL Experience Manager Assets]. Per ulteriori informazioni, consulta [Riutilizzare le risorse utilizzando MSM per Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/reuse-assets-using-msm.html). NPR-29199: Hotfix per CQ-4259922

#### Sites - Incluso

* Esporta [!DNL Experience Manager] Frammenti esperienza in [!DNL Adobe Target]. Per ulteriori dettagli, consulta [Provider rewriter di collegamento di frammento esperienza - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Hotfix per CQ-4265469

#### Forms - Servizi basati su documenti - Incluso

* Solo OSGi: È stato aggiunto un nuovo attributo PAGECOUNT in Output e Forms Service. NPR-28922: Hotfix per CQ-4270870
* Solo OSGi: Abilitazione del supporto per la creazione di file PDF statici tramite Forms Service. NPR-28572: Hotfix per CQ-4270869
* Abilitazione delle autorizzazioni su XMLForm.exe per gli utenti amministratore e root. NPR-29237: Hotfix per CQ-4267080

### Bundle OSGi e pacchetti di contenuti

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.1.0

Elenco dei bundle OSGi inclusi in [!DNL Experience Manager] 6.5.1.0

[Ottieni file](assets/6_5-bundle-list.txt)

Elenco dei pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.1.0

[Ottieni file](assets/6_5-content-package-list.txt)
