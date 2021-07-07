---
title: '[!DNL Experience Manager] Note sulla versione 6.5 del service pack'
description: Note sulla versione specifiche di  [!DNL Adobe Experience Manager] 6.5 service pack 9
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 19dd081674b4954498d6aa62335f6b5a9f2a4146
workflow-type: tm+mt
source-wordcount: '3835'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] Note sulla versione 6.5 del service pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.9.0 |
| Tipo | Versione Service Pack |
| Data | 27 maggio 2021 |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip) |

## Contenuto in [!DNL Adobe Experience Manager] 6.5.9.0 {#what-s-included-in-aem}

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

* Nella finestra di dialogo Rollout, attivata nell’editor o dalla panoramica Live Copy, le icone di stato per le pagine scollegate, sospese o non create sono errate (NPR-35691).

* Casella di controllo per il rollout su pagina di Multi-Site Manager delle proprietà master ignora il rollout della pagina e delle sottopagine (NPR-35634).

* La funzionalità di ripristino della struttura, disponibile nell&#39;interfaccia classica, non è presente nell&#39;interfaccia utente touch (CQ-4315352, CQ-4309415).

* Problemi durante il ripristino dell’ereditarietà e il rollout di una pagina in una pagina [!DNL Experience Manager Sites] (NPR-36033).

### [!DNL Assets] {#assets-6590}

I seguenti miglioramenti dell’esperienza utente vengono eseguiti in [!DNL Assets]:

* Per visualizzare le risorse non ordinate in base ai parametri [!UICONTROL Crea], [!UICONTROL Modifica] o [!UICONTROL Nome], [!DNL Adobe Experience Manager] offre un&#39;opzione [!UICONTROL Nessuno] nelle opzioni [!UICONTROL Ordina per]. L’opzione [!UICONTROL None] assicura che le risorse nell’interfaccia utente di Assets (nella vista a schede, colonne e informazioni approfondite) siano nello stesso ordine in cui esistono nel nodo JCR (NPR-36356).

* Per impostare l’ID e-mail in minuscolo nella risposta API ACP da [!DNL Adobe Experience Manager], è stata introdotta un’impostazione opzionale; poiché gli utenti [!DNL Adobe Asset Link] non potevano archiviare le risorse se il loro ID non conteneva tutti i caratteri in lettere minuscole. Il pannello [!DNL Adobe Asset Link] utilizza la risposta API ACP da [!DNL Adobe Experience Manager] (CQ-4317704).

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] fornisce i seguenti miglioramenti dell’accessibilità.

È stato migliorato il contrasto (con lo sfondo) del testo e delle icone seguenti, in modo che gli utenti con visione limitata e percezione del colore possano comprendere:

* Titolo della risorsa sulla pagina [!UICONTROL Proprietà] (NPR-35967).
* Icone di valutazione a stella nelle sezioni [!UICONTROL Valutazione] in vari punti (NPR-36009).
* Testo nella vista a schede della risorsa e della cartella (NPR-35966).
* Testo segnaposto nella vista [!UICONTROL Timeline] (NPR-35965).
* Nomi di risorse nei risultati di ricerca delle risorse (NPR-35964).
* Testo segnaposto nella finestra di dialogo [!UICONTROL Condivisione collegamenti] (NPR-35963).
* [!UICONTROL Metadati],  [!UICONTROL stato] e   altro testo nell’opzione   Elenco nella finestra di dialogo  [!UICONTROL Visualizza ] impostazioni (NPR-35910).
*  Posizione e  [!UICONTROL tipo per la ] ricerca di testi segnaposto nella ricerca globale (NPR-35909).
* Espandi e comprimi le icone sotto la [!UICONTROL Struttura contenuto] (NPR-35908).
* Il testo [!UICONTROL Risorse] nella pagina in cui vengono visualizzate le cartelle di risorse (NPR-35905).
* Testo in [!UICONTROL Metadati risorsa], [!UICONTROL Statistiche di utilizzo] all’interno dell’opzione [!UICONTROL Panoramica] nella pagina dei dettagli della risorsa (NPR-35904).
* Testo dei tasti di scelta rapida per le opzioni [!UICONTROL proprietà] e [!UICONTROL modifica] nella pagina dei dettagli della risorsa (NPR-35904).

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] risolve i seguenti problemi.

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

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] fornisce i seguenti miglioramenti dell’accessibilità in  [!DNL Dynamic Media].

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
>* È ora possibile sviluppare e utilizzare applicazioni con [!DNL Azul Zulu] build di [!DNL OpenJDK] per [!DNL Experience Manager Forms] nelle distribuzioni OSGi.


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

## Installare la versione 6.5.9.0 {#install}

**Requisiti di configurazione e ulteriori informazioni**

* Experience Manager 6.5.9.0 richiede Experience Manager 6.5. Per istruzioni dettagliate, consulta la [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) .
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* In una distribuzione con MongoDB e più istanze, installa Experience Manager 6.5.9.0 in una delle istanze Autore utilizzando Gestione pacchetti.

>[!NOTE]
>
>Adobe sconsiglia di rimuovere o disinstallare il pacchetto [!DNL Adobe Experience Manager] 6.5.9.0.

### Installare il service pack {#install-service-pack}

Per installare il service pack su un&#39;istanza [!DNL Adobe Experience Manager] 6.5, segui questi passaggi:

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (e questo accade quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia inoltre di riavviare se l&#39;orario di attività corrente per un&#39;istanza è elevato.

1. Prima di installare, scegli uno snapshot o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip).

1. Apri Gestione pacchetti e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l&#39;istanza dopo l&#39;installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l&#39;istanza. Consulta [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude durante l’installazione del service pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere questo accade su [!DNL Safari] ma può accadere in modo intermittente su qualsiasi browser.

**Installazione automatica**

Esistono due modi per installare automaticamente [!DNL Experience Manager] 6.5.9.0 in un&#39;istanza di lavoro:

A. Posiziona il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Utilizza l’ [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizza `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0 non supporta l’installazione di Bootstrap.

**Convalida l&#39;installazione**

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.9.0)` in [!UICONTROL Prodotti installati].

1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (Usa la console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.3 o successiva (Usa console Web: `/system/console/bundles`).

Per conoscere le piattaforme certificate per l’utilizzo con questa versione, consulta i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

### Installare il pacchetto aggiuntivo di Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora questa sezione se non utilizzi Experience Manager Forms. Le correzioni apportate in Experience Manager Forms vengono distribuite tramite un pacchetto aggiuntivo separato una settimana dopo il rilascio pianificato di [!DNL Experience Manager] Service Pack .

1. Assicurati di aver installato il Service Pack di Adobe Experience Manager.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) per il sistema operativo in uso.
1. Installa il pacchetto aggiuntivo di Forms come descritto in [Installazione dei pacchetti aggiuntivi di AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.9.0 include una nuova versione di [Pacchetto di compatibilità AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). Se utilizzi una versione precedente del pacchetto di compatibilità di AEM Forms e aggiorni ad Experience Manager 6.5.9.0, installa la versione più recente del pacchetto dopo l’installazione del pacchetto aggiuntivo di Forms.

### Installare Adobe Experience Manager Forms su JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Le correzioni in Adobe Experience Manager Forms su JEE vengono distribuite tramite un programma di installazione separato.

Per informazioni sull&#39;installazione del programma di installazione cumulativo per Experience Manager Forms su JEE e sulla configurazione post-distribuzione, consulta le [note sulla versione](jee-patch-installer-65.md).

>[!NOTE]
>
>Dopo aver installato il programma di installazione cumulativo per Experience Manager Forms su JEE, installa il pacchetto aggiuntivo Forms più recente, elimina il pacchetto aggiuntivo Forms dalla cartella `crx-repository\install` e riavvia il server.

### UberJar {#uber-jar}

UberJar per Experience Manager 6.5.9.0 è disponibile nell’ [archivio centrale Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9-1.0/).

Per utilizzare UberJar in un progetto Maven, consulta [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9-1.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece dell’archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Pertanto, non esiste `classifier`, con `apis` come valore, per il tag `dependency`.

## Funzioni obsolete {#removed-deprecated-features}

Di seguito è riportato un elenco di funzioni e funzionalità contrassegnate come obsolete con [!DNL Experience Manager] 6.5.7.0. Le funzioni vengono contrassegnate come obsolete inizialmente e successivamente rimosse in una versione futura. È disponibile un’opzione alternativa.

Controlla se utilizzi una funzione o una funzionalità in una distribuzione. Inoltre, pianifica di modificare l’implementazione in modo da utilizzare un’opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrations (Integrazioni) | La schermata **[!UICONTROL Opt-in di AEM Cloud Services]** è obsoleta. Con l’integrazione Experience Manager e Adobe Target aggiornata all’Experience Manager 6.5 per supportare l’API Adobe Target Standard, che utilizza l’autenticazione tramite Adobe IMS e [!DNL Adobe I/O], e il ruolo crescente di Adobe Launch per la strumentazione delle pagine di Experience Manager per l’analisi e la personalizzazione, la procedura guidata di consenso è diventata irrilevante dal punto di vista funzionale. | Configura le connessioni di sistema, l’autenticazione Adobe IMS e le integrazioni [!DNL Adobe I/O] tramite i rispettivi servizi cloud [!DNL Experience Manager]. |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto, ad Experience Manager 6.5. | N/D |

## Problemi noti {#known-issues}

* Se aggiorni la tua istanza [!DNL Experience Manager] dalla versione 6.5 alla versione 6.5.9.0, puoi visualizzare le eccezioni `RRD4JReporter` nel file `error.log` . Riavvia l&#39;istanza per risolvere il problema.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 5 o un precedente service pack su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Se una cartella nella gerarchia viene rinominata in [!DNL Assets] e una cartella nidificata contenente una risorsa viene pubblicata in [!DNL Brand Portal], il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Durante l’installazione di Experience Manager 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l’integrazione di Adobe Target è configurata in Experience Manager utilizzando l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti di esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando si utilizzano funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.9.0:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5.9.0](assets/6590_bundles.txt)

* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.9.0](assets/6590_packages.txt)

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* Consulta [come contattare l&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Note sulla versione 6.5](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] pagina di prodotto](https://www.adobe.com/it/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

