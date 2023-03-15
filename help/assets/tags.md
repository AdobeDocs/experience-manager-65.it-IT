---
title: Integrare i visualizzatori Dynamic Media con i tag Analytics e Adobe Experience Platform
description: Scopri l’estensione Dynamic Media Viewers per Experience Platform Tags e Dynamic Media Viewers 5.13. Consente ai clienti di Adobe Analytics e Experience Platform Tags di utilizzare eventi e dati specifici per i visualizzatori Dynamic Media nella configurazione dei tag Experienci Platform.
mini-toc-levels: 3
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Viewers
role: User, Admin,Developer,Data Engineer,Data Architect
exl-id: 161dfe22-bc1c-4b60-8ab6-a19407a39e2e
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '6633'
ht-degree: 7%

---

# Integrare i visualizzatori Dynamic Media con i tag Analytics e Adobe Experience Platform {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Cos’è l’integrazione dei visualizzatori Dynamic Media con Adobe Analytics e i tag di Experience Platform? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch -->

*Visualizzatori Dynamic Media* Estensione per Experience Platform Tags and Dynamic Media Viewers 5.13, consente ai clienti Adobe Analytics e Tag per Experience Platform di utilizzare eventi e dati specifici per i visualizzatori Dynamic Media nella configurazione dei tag per Experienci Platform.

Questa integrazione consente di monitorare l’utilizzo dei visualizzatori Dynamic Media sul sito web con Adobe Analytics. Allo stesso tempo, puoi utilizzare gli eventi e i dati esposti dai visualizzatori con qualsiasi altra estensione Experience Platform Tag proveniente da un Adobe o da una terza parte.

Per ulteriori informazioni su estensioni di Adobe o estensioni di terze parti, consulta [Estensioni di Adobe](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) nella Guida utente sui tag di Experience Platform.

**Questo argomento è destinato a:** Amministratori di siti, sviluppatori nell’Experience Platform e persone nelle operazioni.

### Limitazioni dell&#39;integrazione {#limitations-of-the-integration}

* L’integrazione dei tag di Experience Platform per i visualizzatori Dynamic Media non funziona nel nodo di authoring di Experience Manager. Non puoi visualizzare alcun tracciamento da una pagina WCM finché non viene pubblicata.
* L’integrazione dei tag di Experience Platform per i visualizzatori Dynamic Media non è supportata per la modalità operativa &quot;pop-up&quot;, in cui l’URL del visualizzatore viene ottenuto utilizzando il pulsante &quot;URL&quot; nella pagina Dettagli risorsa.
* L’integrazione dei tag di Experience Platform non può essere utilizzata simultaneamente con l’integrazione dei visualizzatori legacy di Analytics (tramite `config2=` ).
* Il supporto per il tracciamento video è limitato solo al tracciamento &quot;riproduzione core&quot;, come descritto in [Panoramica del tracciamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). In particolare, il tracciamento di QoS, annunci, capitoli/segmenti o errori non è supportato.
* La configurazione della durata di archiviazione per gli elementi dati non è supportata per gli elementi dati che utilizzano *Visualizzatori Dynamic Media* estensione. La durata dell&#39;archiviazione deve essere impostata su **[!UICONTROL Nessuno]**.

### Casi di utilizzo dell’integrazione {#use-cases-for-the-integration}

L’integrazione con i tag di Experience Platform è un caso d’uso principale per i clienti che utilizzano sia Adobe Experience Manager Assets che Adobe Experience Manager Sites. In questi scenari, puoi impostare un’integrazione standard tra il nodo di authoring di Experience Manager e i tag di Experience Platform, quindi associare l’istanza di Sites alla proprietà Tag di Experience Platform. In seguito, qualsiasi componente WCM di Dynamic Media aggiunto a una pagina Sites terrà traccia dei dati e degli eventi dei visualizzatori.

Vedi [Tracciamento visualizzatori Dynamic Media in Experience Manager Sites](#tracking-dynamic-media-viewers-in-aem-sites).

Un caso d’uso secondario supportato dall’integrazione sono i clienti che utilizzano solo Experience Manager Assets o Dynamic Media Classic. In questi casi, ottieni il codice di incorporamento per il visualizzatore e lo aggiungi alla pagina del sito web. Quindi, ottieni l’URL di produzione della libreria Tag di Experience Platform da Tag di Experience Platform e aggiungilo manualmente al codice della pagina web.

Vedi [Tracciare i visualizzatori Dynamic Media utilizzando il codice di incorporamento](#tracking-dynamic-media-viewers-using-embed-code).

<!-- Path on internal wiki [About tracking Dynamic Media viewers using embed code](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode). -->

## Funzionamento del tracciamento di dati ed eventi nell’integrazione {#how-data-and-event-tracking-works-in-the-integration}

L’integrazione sfrutta due tipi distinti e indipendenti di tracciamento dei visualizzatori Dynamic Media: *Adobe Analytics* e *Adobe Analytics per audio e video*.

### Informazioni sul tracciamento con Adobe Analytics  {#about-tracking-using-adobe-analytics}

Adobe Analytics consente di tenere traccia delle azioni eseguite dall’utente finale quando interagisce con i visualizzatori Dynamic Media sul sito web. Adobe Analytics consente inoltre di tenere traccia dei dati specifici del visualizzatore. Ad esempio, puoi tenere traccia e registrare gli eventi di caricamento della visualizzazione insieme al nome della risorsa, alle azioni di zoom che si sono verificate e alle azioni di riproduzione video.

Ad Experience Platform, i concetti di *Elementi dati* e *Regole* collaborare per abilitare il tracciamento di Adobe Analytics.

#### Informazioni sugli elementi dati nei tag di Experience Platform {#about-data-elements-in-adobe-launch}

Un elemento dati nei tag Experience Platform è una proprietà denominata il cui valore è definito in modo statico o calcolato in modo dinamico in base allo stato di una pagina web o dei dati dei visualizzatori Dynamic Media.

Le opzioni disponibili per una definizione di elemento dati dipendono dall’elenco delle estensioni installate nella proprietà dei tag di Experience Platform. L&#39;estensione &quot;Core&quot; è preinstallata ed è disponibile out-of-the-box in qualsiasi configurazione. Questa estensione &quot;Core&quot; consente di definire un elemento dati che viene dal cookie, dal codice JavaScript, dalla stringa di query e da molte altre sorgenti.

Per il tracciamento di Adobe Analytics è necessario installare diverse estensioni, come descritto in [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions). L’estensione Dynamic Media Viewers aggiunge la possibilità di definire un elemento dati il cui valore è un argomento dell’evento Dynamic Viewer. Ad esempio, è possibile fare riferimento al tipo di visualizzatore, o al nome della risorsa segnalato dal visualizzatore al momento del caricamento, al livello di zoom riportato quando l’utente finale effettua uno zoom e molto altro.

L’estensione Dynamic Media Viewer mantiene automaticamente aggiornati i valori dei suoi elementi dati.

Una volta definito, un elemento dati può essere utilizzato in altre aree dell’interfaccia utente dei tag di Experience Platform, utilizzando il widget Selettore elemento dati . In particolare, agli elementi dati definiti ai fini del tracciamento dei visualizzatori Dynamic Media viene fatto riferimento da Imposta azione variabili dell’estensione Adobe Analytics nella regola (vedi di seguito).

Vedi [Elementi dati](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html).

#### Informazioni sulle regole nei tag di Experience Platform {#about-rules-in-adobe-launch}

Una regola in Experience Platform Tags è una configurazione agnostica che definisce tre aree che compongono una regola: *Eventi*, *Condizioni* e *Azioni*:

* *Eventi* (if) indica ai tag di Experience Platform quando attivare una regola.
* *Condizioni* (if) indica ai tag di Experience Platform quali altre restrizioni consentire o meno quando si attiva una regola.
* *Azioni* (then) dì ai tag di Experience Platform cosa fare quando viene attivata una regola.

Le opzioni disponibili nella sezione Eventi, condizioni e azioni dipendono dalle estensioni installate in Proprietà tag di Experience Platform. La *Core* l&#39;estensione è preinstallata ed è disponibile come impostazione predefinita in qualsiasi configurazione. L&#39;estensione fornisce diverse opzioni per Eventi, ad esempio azioni di base a livello di browser. Tali azioni includono la modifica dello stato attivo, la pressione di tasti e l’invio di moduli. Include inoltre opzioni per le Condizioni, ad esempio il valore del cookie, il tipo di browser e altro ancora. Per Azioni, è disponibile solo l’opzione Codice personalizzato .

Per il tracciamento di Adobe Analytics, è necessario installare diverse altre estensioni, come descritto in [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions). In particolare:

* L’estensione Dynamic Media Viewers estende l’elenco degli eventi supportati agli eventi specifici dei visualizzatori Dynamic Media, come il caricamento del visualizzatore, lo scambio di risorse, lo zoom in e la riproduzione video.
* L&#39;estensione Adobe Analytics estende l&#39;elenco delle azioni supportate con due azioni necessarie per l&#39;invio di dati ai server di tracciamento: *Imposta variabili* e *Invia beacon*.

Per tenere traccia dei visualizzatori Dynamic Media, è possibile utilizzare uno qualsiasi dei seguenti tipi:

* Eventi da estensione Dynamic Media Viewers, estensione Core o qualsiasi altra estensione.
* Condizioni nella definizione della regola. In alternativa, è possibile lasciare vuota l’area delle condizioni.

Nella sezione Azioni è necessario disporre di un *Imposta variabili* azione. Questa azione indica ad Adobe Analytics come popolare le variabili di tracciamento con i dati. Allo stesso tempo, il *Imposta variabili* action non invia nulla al server di tracciamento.

La *Imposta variabili* deve essere seguita da un&#39;azione *Invia beacon* azione. La *Invia beacon* invia effettivamente i dati al server di tracciamento di analytics. Entrambe le azioni, *Imposta variabili* e *Invia beacon*, proviene dall’estensione Adobe Analytics.

Vedi [Regole](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html).

#### Configurazione di esempio {#sample-configuration}

La seguente configurazione di esempio all’interno di Tag per Experienci Platform illustra come tenere traccia del nome di una risorsa al caricamento del visualizzatore.

1. Da **[!UICONTROL Elementi dati]** scheda , definire un elemento dati `AssetName` che fa riferimento a `asset` del `LOAD` dall’estensione Dynamic Media Viewers .

   ![image2019-11](assets/image2019-11.png)

1. Da **[!UICONTROL Regole]** scheda , definire una regola *TrackAssetOnLoad*.

   In questa regola, il **[!UICONTROL Evento]** utilizza **[!UICONTROL CARICA]** dall’estensione Dynamic Media Viewers .

   ![image2019-22](assets/image2019-22.png)

1. La configurazione Azione dispone di due tipi di Azione dall&#39;estensione Adobe Analytics:

   *Imposta variabili*, che mappano una variabile di analisi scelta al valore di `AssetName` Elemento dati.

   *Invia beacon*, che invia informazioni di tracciamento ad Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. La configurazione della regola risultante avrà il seguente aspetto:

   ![image2019-4](assets/image2019-4.png)

### Informazioni su Adobe Analytics per audio e video {#about-adobe-analytics-for-audio-and-video}

Quando un account di Experience Cloud è abbonato per utilizzare Adobe Analytics per audio e video, è sufficiente per abilitare il tracciamento video nel *Visualizzatori Dynamic Media* impostazioni di estensione. Le metriche video diventano disponibili in Adobe Analytics. Il tracciamento video dipende dalla presenza di estensioni Adobe Medium Analytics for Audio and Video.

Vedi [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions).

Attualmente, il supporto per il tracciamento video è limitato solo al tracciamento &quot;core playback&quot;, come descritto in [Panoramica sul tracciamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). In particolare, il tracciamento di QoS, annunci, capitoli/segmenti o errori non è supportato.

## Utilizzare l’estensione Dynamic Media Viewers {#using-the-dynamic-media-viewers-extension}

Come indicato in [Casi di utilizzo dell’integrazione](#use-cases-for-the-integration), è possibile tenere traccia dei visualizzatori Dynamic Media con la nuova integrazione dei tag Experience Platform in Experience Manager Sites e utilizzando il codice di incorporamento .

### Tracciamento visualizzatori Dynamic Media in Experience Manager Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Per tenere traccia dei visualizzatori Dynamic Media in Experience Manager Sites, tutti i passaggi elencati in [Configurare tutti i pezzi di integrazione](#configuring-all-the-integration-pieces) deve essere eseguita. In particolare, devi creare la configurazione IMS e la configurazione cloud Experience Platform Tags.

In base alla configurazione corretta, qualsiasi visualizzatore Dynamic Media aggiunto a una pagina Sites, utilizzando un componente WCM supportato da Dynamic Media, traccia automaticamente i dati in Adobe Analytics, o Adobe Analytics for Video, o entrambi.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### Tracciare i visualizzatori Dynamic Media utilizzando il codice di incorporamento {#tracking-dynamic-media-viewers-using-embed-code}

I clienti che non utilizzano Experience Manager Sites, o che incorporano i visualizzatori Dynamic Media in pagine web al di fuori di Experience Manager Sites, o entrambi, possono comunque utilizzare l’integrazione dei tag di Experience Platform.

Completa i passaggi di configurazione dal [Configurare Adobe Analytics](#configuring-adobe-analytics-for-the-integration) e [Configurare i tag di Experience Platform](#configuring-adobe-launch-for-the-integration) sezioni. Tuttavia, non sono necessari passaggi di configurazione relativi ad Experience Manager.

Seguendo la configurazione corretta, puoi aggiungere il supporto per i tag di Experience Platform a una pagina web con un visualizzatore Dynamic Media.

Vedi [Aggiungere il codice di incorporamento dei tag di Experience Platform](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html#configure-launch) per ulteriori informazioni su come utilizzare il codice di incorporamento della libreria dei tag di Experience Platform.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of Experience Manager Dynamic Media.
-->

**Tracciare i visualizzatori Dynamic Media utilizzando il codice di incorporamento:**

1. Avere una pagina web pronta per l’incorporazione di un visualizzatore Dynamic Media.
1. Per ottenere il codice di incorporamento per la libreria dei tag di Experience Platform, accedi prima a Tag di Experience Platform (consulta [Configurazione dei tag di Experience Platform](#configuring-adobe-launch-for-the-integration)).
1. Seleziona **[!UICONTROL Proprietà]**, quindi seleziona la **[!UICONTROL Ambienti]** scheda .
1. Scegli il livello Ambiente appropriato per l’ambiente della pagina web. Quindi, nella **[!UICONTROL Installa]** , seleziona l’icona della casella.
1. **[!UICONTROL Nelle istruzioni di installazione web]** , copia l’intero codice di incorporamento della libreria Tag di Experience Platform, insieme all’ambiente circostante `<script/>` tag.

## Guida di riferimento per l’estensione Dynamic Media Viewers {#reference-guide-for-the-dynamic-media-viewers-extension}

### Informazioni sulla configurazione dei visualizzatori Dynamic Media {#about-the-dynamic-media-viewers-configuration}

L’estensione Dynamic Media Viewer si integra automaticamente con la libreria Tag Experience Platform se le seguenti condizioni sono vere:

* Oggetto globale della libreria dei tag di Experience Platform ( `_satellite`) è presente nella pagina.
* Funzione di estensione dei visualizzatori Dynamic Media `_dmviewers_v001()` è definito in `_satellite`.

* `config2=` il parametro del visualizzatore non è specificato, il che significa che il visualizzatore non utilizza l’integrazione legacy di Analytics.

Inoltre, esiste un’opzione per disabilitare esplicitamente l’integrazione dei tag di Experience Platform nel visualizzatore specificando `launch=0` nella configurazione del visualizzatore. Il valore predefinito di questo parametro è `1`.

### Configurare l’estensione Dynamic Media Viewers {#configuring-the-dynamic-media-viewers-extension}

L’unica opzione di configurazione per l’estensione Dynamic Media Viewers è **[!UICONTROL Abilitare Adobe Medium Analytics per audio e video]**.

Quando selezioni (attiva) questa opzione e installi e configuri l’estensione Adobe Medium Analytics for Audio and Video, le metriche di riproduzione video vengono inviate alla soluzione Adobe Analytics for Audio and Video . La disattivazione di questa opzione disattiva il tracciamento video.

Se abiliti questa opzione *senza* con l&#39;estensione Adobe Medium Analytics for Audio and Video installata, l&#39;opzione non ha alcun effetto.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Informazioni sugli elementi dati nell’estensione Dynamic Media Viewers {#about-data-elements-in-the-dynamic-media-viewers-extension}

L’unico tipo di elemento di dati fornito dall’estensione Dynamic Media Viewers è **[!UICONTROL Evento visualizzatore]**, proveniente dall’elenco a discesa **[!UICONTROL Data Element Type (Tipo di elemento dati)]**.

Quando è selezionato, l’editor Elemento dati esegue il rendering di un modulo con due campi:

* **[!UICONTROL DM viewers event data type (Tipo di dati evento visualizzatori DM)]**: un elenco a discesa che identifica tutti gli eventi visualizzatore supportati dall’estensione Dynamic Media Viewers che presentano argomenti, con l’aggiunta di un elemento **[!UICONTROL COMMON]** speciale. Un elemento **[!UICONTROL COMMON]** rappresenta un elenco di parametri evento che sono comuni a tutti i tipi di eventi inviati dai visualizzatori.
* **[!UICONTROL Parametro di tracciamento]** - un argomento dell’evento di visualizzatore Dynamic Media selezionato.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Consulta la sezione [Guida di riferimento per i visualizzatori Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) per l’elenco degli eventi supportati per ciascun tipo di visualizzatore; vai a una sezione specifica del visualizzatore, quindi seleziona Supporto per la sottosezione di tracciamento di Adobe Analytics. Attualmente, la guida di riferimento visualizzatori Dynamic Media non documenta gli argomenti relativi agli eventi.

Ora considera il ciclo di vita dei visualizzatori Dynamic Media *Elemento dati*. Il valore di tale elemento dati viene popolato dopo che l’evento corrispondente del visualizzatore Dynamic Media si verifica sulla pagina. Ad esempio, supponiamo che l’elemento dati punti al **[!UICONTROL CARICA]** e il relativo argomento &quot;asset&quot;. In tal caso, il valore di tale elemento dati riceve dati validi dopo che il visualizzatore esegue il **[!UICONTROL CARICA]** per la prima volta. Se l’elemento dati punta alla variabile **[!UICONTROL ZOOM]** e il relativo argomento &quot;scala&quot;, il valore di tale elemento dati rimane vuoto finché il visualizzatore non invia un **[!UICONTROL ZOOM]** per la prima volta.

Allo stesso modo, i valori di Elementi dati vengono aggiornati automaticamente quando il visualizzatore invia un evento corrispondente sulla pagina. L’aggiornamento del valore si verifica anche se l’evento specifico non è indicato nella configurazione Regola. Ad esempio, supponiamo che l’elemento dati **[!UICONTROL ZoomScale]** è definito per il parametro &quot;scale&quot; dell&#39;evento ZOOM. Tuttavia, l&#39;unica regola presente nella configurazione della regola viene attivata dal **[!UICONTROL CARICA]** evento. Il valore di **[!UICONTROL ZoomScale]** viene comunque aggiornato ogni volta che un utente esegue uno zoom all’interno del visualizzatore.

Qualsiasi visualizzatore Dynamic Media è dotato di un identificatore univoco sulla pagina web. L’elemento dati tiene traccia del valore stesso e del visualizzatore che lo ha popolato. Ad esempio, supponiamo che ci siano diversi visualizzatori sulla stessa pagina e un **[!UICONTROL NomeRisorsa]** Elemento dati che punta al **[!UICONTROL CARICA]** e il relativo argomento &quot;asset&quot;. La **[!UICONTROL NomeRisorsa]** Elemento dati mantiene una raccolta di nomi di risorse associati a ciascun visualizzatore caricato sulla pagina.

Il valore esatto restituito dall’elemento dati dipende dal contesto. Se l&#39;elemento dati è richiesto in una regola attivata da un evento visualizzatore Dynamic Media, viene restituito il valore dell&#39;elemento dati per il visualizzatore che ha avviato la regola. Inoltre, l&#39;elemento dati è richiesto in una regola attivata da un evento da un&#39;altra estensione Experience Platform Tags. A quel punto, il valore dell’elemento dati proviene dal visualizzatore che è stato l’ultimo ad aggiornare questo elemento dati.

**Considera la seguente impostazione di esempio:**

* Pagina Web con due visualizzatori zoom Dynamic Media: *visualizzatore1* e *visualizzatore2*.

* **[!UICONTROL ZoomScale]** L’elemento dati punta al **[!UICONTROL ZOOM]** evento e relativo argomento &quot;scale&quot;.
* **[!UICONTROL TrackPan]** Regola con quanto segue:

   * Utilizza il visualizzatore Dynamic Media **[!UICONTROL PAN]** come attivatore.
   * Invia il valore di **[!UICONTROL ZoomScale]** Elemento dati in Adobe Analytics.

* **[!UICONTROL TrackKey]** Regola con quanto segue:

   * Utilizza l’evento di pressione tasti dell’estensione Core Experience Platform Tags come attivatore.
   * Invia il valore di **[!UICONTROL ZoomScale]** Elemento dati in Adobe Analytics.

Ora, si supponga che l’utente finale carichi la pagina web con i due visualizzatori. In *visualizzatore1*, zoom in una scala del 50%; quindi, in *visualizzatore2*, zoom in scala 25%. In *visualizzatore1*, effettua una panoramica dell’immagine e infine seleziona un tasto sulla tastiera.

L’attività dell’utente finale si traduce in due chiamate di tracciamento effettuate ad Adobe Analytics:

* La prima chiamata si verifica perché **[!UICONTROL TrackPan]** La regola viene attivata quando l&#39;utente effettua il pansing in *visualizzatore1*. Questa chiamata invia il 50% come valore di **[!UICONTROL ZoomScale]** Elemento dati perché è a conoscenza del fatto che la regola viene attivata da *visualizzatore1* e recupera il valore di scala corrispondente;
* La seconda chiamata si verifica perché **[!UICONTROL TrackKey]** La regola viene attivata quando l&#39;utente preme un tasto sulla tastiera. Questa chiamata invia il 25% come valore di **[!UICONTROL ZoomScale]** Elemento dati perché la regola non è stata attivata dal visualizzatore. Di conseguenza, l’elemento dati restituisce il valore più aggiornato.

Il campione impostato sopra influisce anche sulla durata del valore dell’elemento dati. Il valore dell’elemento dati gestito dal visualizzatore Dynamic Media è memorizzato nel codice della libreria Tag Experience Platform anche dopo l’eliminazione del visualizzatore stesso sulla pagina web. Questa funzionalità significa che se è presente una regola attivata da un’estensione del visualizzatore non Dynamic Media e fa riferimento a tale elemento dati, l’elemento dati restituisce l’ultimo valore noto. Anche se il visualizzatore non è più presente sulla pagina web.

In ogni caso, i valori degli elementi dati guidati dai visualizzatori Dynamic Media non vengono memorizzati nell’archivio locale o sul server; vengono invece conservati solo nella libreria dei tag di Experience Platform lato client. I valori di tali elementi dati scompaiono quando la pagina web viene ricaricata.

In genere, l’editor degli elementi dati supporta [selezione della durata dello storage](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). Tuttavia, gli elementi dati che utilizzano l’estensione Dynamic Media Viewers supportano solo l’opzione della durata di archiviazione di **[!UICONTROL Nessuno]**. L’impostazione di qualsiasi altro valore è possibile nell’interfaccia utente, ma in questo caso il comportamento Elemento dati non è definito. L&#39;estensione gestisce il valore dell&#39;elemento dati da sola: l’elemento dati che mantiene il valore dell’argomento evento visualizzatore durante l’intero ciclo di vita del visualizzatore.

### Informazioni sulle regole nell’estensione Dynamic Media Viewers {#about-rules-in-the-dynamic-media-viewers-extension}

Nell’editor delle regole, l’estensione aggiunge nuove opzioni di configurazione per l’editor Eventi. Inoltre, l’editor fornisce un’opzione per fare riferimento manualmente ai parametri dell’evento nell’editor azioni come opzione di breve durata invece di utilizzare elementi dati preconfigurati.

#### Informazioni sull’editor di eventi {#about-the-events-editor}

Nell’editor evento, l’estensione Dynamic Media Viewers aggiunge un **[!UICONTROL Tipo evento]** chiamato **[!UICONTROL Evento visualizzatore]**.

Quando questa opzione è selezionata, nell’editor eventi viene eseguito il rendering del menu a discesa **[!UICONTROL Eventi del visualizzatore Dynamic Media]**, elencando tutti gli eventi disponibili supportati dai visualizzatori Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Informazioni sull’editor Azioni {#about-the-actions-editor}

L’estensione Dynamic Media Viewers consente di utilizzare i parametri evento dei visualizzatori Dynamic Media per mappare le variabili di Analytics nell’editor Imposta variabili dell’estensione Adobe Analytics.

Il metodo più semplice per farlo è quello di completare il seguente processo in due fasi:

* Innanzitutto, definisci uno o più elementi dati, in cui ogni elemento dati rappresenta un parametro di un evento Dynamic Media Viewer.
* Infine, nell’editor Imposta variabili dell’estensione Adobe Analytics, seleziona la **[!UICONTROL Elemento dati]** icona del selettore (tre dischi impilati) per aprire la finestra di dialogo Seleziona elemento dati , quindi selezionare un elemento dati da esso.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

È tuttavia possibile adottare un approccio alternativo e ignorare la creazione di elementi dati. È possibile fare riferimento direttamente a un argomento da un evento Dynamic Media Viewer. Immetti il nome completo dell&#39;argomento dell&#39;evento nel **[!UICONTROL value]** campo di input dell’assegnazione della variabile Analytics. Assicurati di circondarla con segni di percentuale (%). Ad esempio:

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

C&#39;è una differenza importante tra l&#39;utilizzo di Elementi dati e il riferimento diretto all&#39;argomento evento. Per l’elemento dati, non importa quale evento attiva l’azione Imposta variabili . L’evento che attiva la regola può non essere correlato al visualizzatore dinamico. Ad esempio, seleziona la pagina web dall’estensione core. Tuttavia, quando si utilizza un riferimento a un argomento diretto, è importante garantire che l&#39;evento che attiva la regola corrisponda all&#39;argomento evento a cui fa riferimento.

Ad esempio, il riferimento a `%event.detail.dm.LOAD.asset%` restituisce il nome corretto della risorsa se la regola viene attivata dall’evento **[!UICONTROL LOAD]** dell’estensione Dynamic Media Viewer. Tuttavia, restituisce un valore vuoto per qualsiasi altro evento.

Nella tabella seguente sono elencati gli eventi del visualizzatore Dynamic Media e i relativi argomenti supportati:

<table>
 <tbody>
  <tr>
   <td>Nome evento del visualizzatore</td>
   <td>Riferimento argomento</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## Configurare tutti i pezzi di integrazione {#configuring-all-the-integration-pieces}

**PRIMA DI INIZIARE**

L’Adobe consiglia di esaminare tutta la documentazione prima di questa sezione in modo da comprendere l’integrazione completa.

Questa sezione descrive i passaggi di configurazione necessari per integrare i visualizzatori Dynamic Media con Adobe Analytics e Adobe Analytics for Audio and Video. Anche se è possibile utilizzare l’estensione Dynamic Media Viewers per altri scopi nei tag di Experience Platform, tali scenari non sono descritti in questa documentazione.

Per configurare l’integrazione, utilizza i seguenti prodotti di Adobe:

* Adobe Analytics : utilizzato per configurare variabili di tracciamento e rapporti.
* Tag di Experience Platform : utilizzato per definire una proprietà, una o più regole e uno o più elementi dati per abilitare il tracciamento del visualizzatore.

Inoltre, se questa soluzione di integrazione viene utilizzata con Experience Manager Sites, è necessario eseguire anche la seguente configurazione:

* [!DNL Adobe I/O] Console: viene creata l’integrazione per Experience Platform Tag.
* Nodo autore Experience Manager: configurazione IMS e configurazione cloud dei tag Experience Platform.

Come parte della configurazione, assicurati di avere accesso a una società in Adobe Experience Cloud che dispone di Adobe Analytics e tag Experience Platform già abilitati.

## Configurare Adobe Analytics per l’integrazione {#configuring-adobe-analytics-for-the-integration}

Dopo aver configurato Adobe Analytics, per l’integrazione verrà impostato quanto segue:

* Una suite di rapporti è inserita e selezionata.
* Le variabili di Analytics sono disponibili per ricevere i dati di tracciamento.
* Sono disponibili rapporti per visualizzare i dati raccolti all’interno di Adobe Analytics.

Vedi anche [Guida all’implementazione di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**Per configurare Adobe Analytics per l’integrazione:**

1. Accedi ad Adobe Analytics dall’Experience Cloud [home page](https://experience.adobe.com/#/home). Nella barra dei menu, seleziona la **[!UICONTROL Soluzioni]** icona (a tre per tre tabelle di punti) nell’angolo in alto a destra della pagina, quindi seleziona **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Ora seleziona una suite di rapporti.

### Selezionare una suite di rapporti {#selecting-a-report-suite}

1. Nell’angolo in alto a destra della pagina Adobe Analytics, alla destra del campo **[!UICONTROL Search Reports (Cerca rapporti)]**, seleziona la report suite corretta dall’elenco a discesa. Se sono disponibili più report suite e non sai quale utilizzare, contatta l’amministratore Adobe Analytics che ti fornirà supporto al riguardo.

   Nella schermata seguente, un utente ha creato una suite di rapporti denominata *DynamicMediaViewersExtensionDoc* e l&#39;ha selezionata dall&#39;elenco a discesa. Il nome della suite di rapporti è solo un nome di esempio. Il nome della suite di rapporti selezionata in ultima analisi dipende da te.

   Se non è disponibile alcuna suite di rapporti, è necessario crearne una o più prima di procedere con la configurazione.

   Vedi [Report e suite per report](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html#manage-report-suites) e [Creare una suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).

   In Adobe Analytics, le suite di rapporti sono gestite in **[!UICONTROL Amministratore]** > **[!UICONTROL Suite di rapporti]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Ora configura le variabili Adobe Analytics.

### Impostare le variabili di Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Designa una o più variabili Adobe Analytics da utilizzare per monitorare il comportamento dei visualizzatori Dynamic Media sulla pagina web.

   È possibile utilizzare qualsiasi tipo di variabile supportata da Adobe Analytics. La decisione relativa al tipo di variabile (come Traffico personalizzato) [proprietà], Conversione [eVar]) è determinata dalle esigenze specifiche dell’implementazione di Analytics.

   Vedi [Panoramica di prop ed eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   Ai fini di questa documentazione, verrà utilizzata solo una variabile Traffico personalizzato (proprietà) perché diventano disponibili in un rapporto di Analytics entro pochi minuti dall’esecuzione di un’azione su una pagina web.

   Per abilitare una nuova variabile Traffico personalizzato, in Adobe Analytics, nella barra degli strumenti, passa a **[!UICONTROL Amministratore]** > **[!UICONTROL Suite di rapporti]**.

1. Sulla **[!UICONTROL Report Suite Manager]** , seleziona il rapporto corretto, quindi nella barra degli strumenti passa a **[!UICONTROL Modifica impostazioni]** > **[!UICONTROL Traffico]** > **[!UICONTROL Variabili di traffico]**.
1. Seleziona una variabile che non viene utilizzata e assegnagli un nome descrittivo (**[!UICONTROL Risorsa visualizzatore (prop 30)]**) e cambia la casella combinata in &quot;Abilitato&quot; nella colonna Abilitato.

   La schermata seguente è un esempio di variabile Traffico personalizzato ( **[!UICONTROL prop30]**) per tenere traccia del nome di una risorsa utilizzata dal visualizzatore:

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. Nella parte inferiore dell’elenco delle variabili, seleziona **[!UICONTROL Salva]**.

### Impostare un rapporto {#setting-up-a-report}

1. In genere, l’impostazione di un rapporto in Adobe Analytics è guidata da specifiche esigenze di progetto. Di conseguenza, una configurazione dettagliata dei rapporti va oltre lo scopo di questa integrazione.

   È tuttavia sufficiente sapere che i rapporti Traffico personalizzato diventano automaticamente disponibili in Adobe Analytics dopo aver impostato le variabili Traffico personalizzato in [Configurare le variabili Adobe Analytics](#setting-up-adobe-analytics-variables).

   Ad esempio, il rapporto per **[!UICONTROL Risorsa visualizzatore (prop 30)]** è disponibile dal menu Rapporti in **[!UICONTROL Traffico personalizzato]** > **[!UICONTROL Traffico personalizzato 21-30]** > **[!UICONTROL Risorsa visualizzatore (prop 30)]**.

   Se accedi a questo rapporto subito dopo la creazione di **[!UICONTROL Viewer asset (Risorsa visualizzatore) (prop 30)]** non troverai alcun dato, il che è piuttosto normale a questo punto dell’integrazione.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## Configurare i tag di Experience Platform per l’integrazione {#configuring-adobe-launch-for-the-integration}

Dopo aver configurato i tag di Experience Platform, per l’integrazione verrà impostato quanto segue:

* La creazione di una nuova proprietà per mantenere tutte le configurazioni insieme.
* Installazione e configurazione di estensioni. Il codice lato client di tutte le estensioni installate nella Proprietà viene compilato insieme in una libreria. Questa libreria viene utilizzata dalla pagina web in un secondo momento.
* Configurazione di elementi dati e regole. Questa configurazione definisce i dati da acquisire dai visualizzatori Dynamic Media, quando attivare la logica di tracciamento e dove inviare i dati del visualizzatore in Adobe Analytics.
* Pubblicazione della libreria.

**Per configurare i tag di Experience Platform per l’integrazione:**

1. Per iniziare, accedi ai tag di Experience Platform dall’Experience Cloud [home page](https://experience.adobe.com/#/home). Nella barra dei menu, seleziona la **[!UICONTROL Soluzioni]** icona (tre per tre tabelle di punti) vicino all’angolo superiore destro della pagina, quindi seleziona **[!UICONTROL Tag]**.

   È inoltre possibile [aprire direttamente i tag di Experience Platform](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Creare una proprietà in Tag di Experience Platform {#creating-a-property-in-adobe-launch}

Una proprietà in Experience Platform Tags è una configurazione denominata che mantiene tutte le impostazioni insieme. Viene generata e pubblicata una libreria delle impostazioni di configurazione a diversi livelli di ambiente (sviluppo, staging e produzione).

Vedi anche [Creare una proprietà Tag](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-mobile-android-apps-with-launch/configure-launch/launch-create-a-property.html#configure-launch).

1. In Tag per Experienci Platform, seleziona **[!UICONTROL Nuova proprietà]**.
1. Nella finestra di dialogo **[!UICONTROL Crea proprietà]**, digita un nome descrittivo nel campo **[!UICONTROL Nome]**, ad esempio il titolo del tuo sito web. Esempio, `DynamicMediaViewersProp.`
1. In **[!UICONTROL Domini]** , immetti il dominio del tuo sito web.
1. In **[!UICONTROL Opzioni avanzate]** a discesa, abilita **[!UICONTROL Configura per lo sviluppo dell&#39;estensione (non può essere modificato in seguito)]** nel caso in cui l&#39;estensione che desideri utilizzare, in questo caso *Visualizzatori Dynamic Media*- non ancora rilasciato.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Seleziona **[!UICONTROL Salva]**.

   Seleziona la nuova proprietà creata, quindi procedi *Installazione e configurazione di estensioni*.

### Installazione e configurazione di estensioni {#installing-and-setup-of-extensions}

Tutte le estensioni disponibili in Experience Platform Tags sono elencate in **[!UICONTROL Estensioni]** > **[!UICONTROL Catalogo]**.

Per installare un&#39;estensione, seleziona **[!UICONTROL Installa]**. Se necessario, esegui una configurazione di estensione una tantum, quindi seleziona **[!UICONTROL Salva]**.

Se necessario, è necessario installare e configurare le seguenti estensioni:

* (Obbligatorio) *Servizio Experience Cloud ID* estensione.

Non è necessaria alcuna configurazione aggiuntiva, accetta per eventuali valori proposti. Al termine, assicurati di selezionare **[!UICONTROL Salva]**.

Vedi [Estensione del servizio Adobe Experience Cloud Identity](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html).

* (Obbligatorio) *Adobe Analytics* estensione

Per configurare questa estensione, devi disporre dell’ID suite di rapporti presente in Adobe Analytics, in **[!UICONTROL Amministratore]** > **[!UICONTROL Suite di rapporti]**, **[!UICONTROL ID suite di rapporti]** intestazione di colonna.

(Solo a scopo dimostrativo, l’ID della suite di rapporti **[!UICONTROL DynamicMediaViewersExtensionDoc]** Suite di rapporti viene utilizzata nelle schermate seguenti. Questo ID è stato creato e utilizzato in [Selezionare una suite di rapporti](#selecting-a-report-suite) prima).

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

Nella pagina Installa estensione, immetti l’ID Report Suite nel campo **[!UICONTROL Development Report Suites]** (Report Suite di sviluppo), nel campo **[!UICONTROL Staging Report Suites]** (Report Suite di staging) e nel campo **[!UICONTROL Production Report Suites]** (Report Suite di produzione).

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configura l’elemento seguente solo se intendi usare il tracciamento video:*

Sulla **[!UICONTROL Estensione di installazione]** pagina, espandi **[!UICONTROL Generale]**, quindi specifica il server di tracciamento. Il server di tracciamento segue il modello `<trackingNamespace>.sc.omtrdc.net`, dove `<trackingNamespace>` è l’informazione ottenuta nell’e-mail di provisioning.

Seleziona **[!UICONTROL Salva]**.

Vedi [Estensione Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html).

* (Facoltativo; richiesto solo se è necessario il tracciamento video) *Adobe Medium Analytics per audio e video* estensione

Compila il campo del server di tracciamento . Server di tracciamento per *Adobe Medium Analytics per audio e video* l&#39;estensione è diversa dal server di tracciamento utilizzato per Adobe Analytics. Segue il modello `<trackingNamespace>.hb.omtrdc.net`, dove `<trackingNamespace>` è l’informazione dell’e-mail di provisioning.

Tutti gli altri campi sono facoltativi.

Vedi [Estensione Adobe Medium Analytics for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html).

* (Obbligatorio) *Visualizzatori Dynamic Media* estensione

Per attivare il tracking Video Heartbeat, seleziona **[!UICONTROL enable Adobe Analytics for Video (Abilita Adobe Analytics per video)]**.

A partire da questa scrittura, il *Visualizzatori Dynamic Media* L&#39;estensione è disponibile solo se la proprietà Experience Platform Tags viene creata per lo sviluppo.

Vedi [Creare una proprietà in Tag di Experience Platform](#creating-a-property-in-adobe-launch).

Una volta installate e configurate le estensioni, almeno le seguenti cinque estensioni (quattro se non stai monitorando il video) saranno elencate nell&#39;area Estensioni > Installate .

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Impostare elementi dati e regole {#setting-up-data-elements-and-rules}

In Experience Platform Tag , crea elementi dati e regole necessari per tenere traccia dei visualizzatori Dynamic Media.

Vedi [Funzionamento del tracciamento di dati ed eventi nell’integrazione](#how-data-and-event-tracking-works-in-the-integration) per una panoramica del tracciamento con i tag di Experience Platform.

Vedi [Configurazione di esempio](#sample-configuration) per una configurazione di esempio in Tag di Experience Platform che dimostra come tenere traccia del nome di una risorsa al caricamento del visualizzatore.

Vedi [Configurare l’estensione Dynamic Media Viewers](#configuring-the-dynamic-media-viewers-extension) per informazioni approfondite sulle funzionalità dell&#39;estensione.

### Pubblicare una libreria {#publishing-a-library}

Per modificare la configurazione dei tag di Experience Platform (inclusa la configurazione di Proprietà, Estensioni, Regole ed Elementi dati), devi *pubblicare* tali modifiche. La pubblicazione nei tag di Experience Platform viene eseguita dalla scheda Pubblicazione nella configurazione di Proprietà.

I tag di Experience Platform possono avere potenzialmente più ambienti di sviluppo, un ambiente di staging e un ambiente di produzione. Per impostazione predefinita, la configurazione cloud dei tag di Experience Platform in Experience Manager indirizza il nodo autore di Experience Manager all’ambiente stage dei tag di Experience Platform. Il nodo Pubblica di Experience Manager punta all’ambiente Produzione di tag di Experience Platform. Questo significa che, con le impostazioni di Experience Manager predefinite, è necessario pubblicare la libreria Tag di Experience Platform nell’ambiente di staging. In questo modo puoi utilizzarlo in Experience Manager Author. Puoi quindi pubblicarlo nell’ambiente di produzione in modo che possa essere utilizzato nella pubblicazione Experience Manager.

Vedi [Ambienti](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html) per ulteriori informazioni sugli ambienti Experience Platform Tags.

La pubblicazione di una libreria prevede i due passaggi seguenti:

* Aggiunta e creazione di una nuova libreria includendo tutte le modifiche necessarie (nuove e aggiornate) nella libreria.
* Spostamento della libreria nei diversi livelli di ambiente (da Sviluppo a Staging e Produzione).

#### Aggiungi e genera una nuova libreria {#adding-and-building-a-new-library}

1. La prima volta che apri la scheda Pubblicazione in Tag Experience Platform, l’elenco della libreria è vuoto.

   Nella colonna di sinistra, seleziona **[!UICONTROL Aggiungi nuova libreria]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. Nella pagina Crea nuova libreria , **[!UICONTROL Nome]** immettere un nome descrittivo per la nuova libreria. Ad esempio:

   *DynamicMediaViewersLib*

   Dall’elenco a discesa Ambiente , scegli il livello Ambiente . Inizialmente, è disponibile solo il livello di sviluppo per la selezione. Vicino al lato inferiore sinistro della pagina, seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva e genera per sviluppo]**.

   In pochi minuti, la libreria viene creata e pronta per l&#39;uso.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >La prossima volta che modifichi la configurazione dei tag di Experience Platform, passa alla pagina **[!UICONTROL Pubblicazione]** sotto la scheda **[!UICONTROL Proprietà]** , quindi seleziona la libreria creata in precedenza.
   >
   >
   >Dalla schermata di pubblicazione della libreria, seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**, quindi seleziona **[!UICONTROL Salva e genera per sviluppo]**.

#### Spostarsi verso l&#39;alto in una libreria attraverso i livelli dell&#39;ambiente {#moving-a-library-up-through-environment-levels}

1. Dopo l&#39;aggiunta di una nuova libreria, questa viene trovata nell&#39;ambiente di sviluppo. Per spostarlo a livello di ambiente di staging (corrispondente alla colonna Inviato), dal menu a discesa della libreria, seleziona **[!UICONTROL Invia per approvazione]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Nella finestra di dialogo di conferma, seleziona **[!UICONTROL Invia]**.

   Una volta che la libreria si sposta nella colonna Inviato, dal menu a discesa della libreria, seleziona **[!UICONTROL Generazione per staging]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Per spostare la libreria dall’ambiente di staging all’ambiente di produzione (colonna Pubblicato ), segui un processo simile.

   Innanzitutto, dal menu a discesa, seleziona **[!UICONTROL Approva per la pubblicazione]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. Dal menu a discesa, seleziona **[!UICONTROL Creare e pubblicare in produzione]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Vedi [Pubblicazione](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) per ulteriori informazioni sul processo di pubblicazione in Experience Platform Tags.

## Configurare Adobe Experience Manager per l’integrazione {#configuring-adobe-experience-manager-for-the-integration}

Prerequisiti:

* Experience Manager esegue sia le istanze Author che Publish.
* Il nodo autore di Experience Manager è configurato in modalità di esecuzione Dynamic Media - Scene7 (dynamic media_s7)
* I componenti WCM di Dynamic Media sono abilitati in Experience Manager Sites.

La configurazione dell’Experience Manager consiste dei due passaggi principali seguenti:

* Configurazione di Experience Manager IMS.
* Configurazione di Experience Platform Tags Cloud.

### Configurare Experience Manager IMS {#configuring-aem-ims}

1. In Experience Manager Author, seleziona la **[!UICONTROL Strumenti]** icona (martello), quindi vai a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Nella pagina Configurazione IMC di Adobe, nell’angolo in alto a sinistra, seleziona **[!UICONTROL Crea]**.
1. Sulla **[!UICONTROL Configurazione dell’account tecnico Adobe IMS]** nella pagina **[!UICONTROL Soluzione cloud]** elenco a discesa, seleziona **[!UICONTROL Experience Platform di tag]**.
1. Abilita **[!UICONTROL Crea nuovo certificato]**, quindi nel campo di testo, immetti qualsiasi valore significativo per il certificato. Ad esempio: *AdobeLaunchIMSCert*. Seleziona **[!UICONTROL Crea certificato]**.

   Viene visualizzato il seguente messaggio Info:

   *Per recuperare un token di accesso valido, la nuova chiave pubblica del certificato viene aggiunta all’account tecnico all’Adobe I/O.*

   Per chiudere la finestra di dialogo Informazioni, selezionare **[!UICONTROL OK]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Per scaricare un file di chiave pubblica (&#42;.crt) nel sistema locale, seleziona **[!UICONTROL Scarica chiave pubblica]**.

   >[!NOTE]
   >
   >A questo punto, ***lasciare aperta*** la **[!UICONTROL Configurazione dell’account tecnico Adobe IMS]** pagina; ***non*** chiudi la pagina e ***non*** selezionare Avanti. Tornerai a questa pagina più avanti nei passaggi successivi.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. In una nuova scheda del browser, passa alla [[!DNL Adobe I/O] Console](https://console.adobe.io/integrations).

1. Da **[!UICONTROL Integrazioni della console Adobe I/O]** nell’angolo in alto a destra, seleziona **[!UICONTROL Nuova integrazione]**.
1. In **[!UICONTROL Creare una nuova integrazione]** verificare che **[!UICONTROL Accedere a un’API]** pulsante di scelta selezionato, quindi selezionare **[!UICONTROL Continua]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. Al secondo **[!UICONTROL Creare una nuova integrazione]** pagina, abilita (attiva) **[!UICONTROL API dei tag di Experience Platform]** pulsante di scelta. Nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Continua]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Il terzo **[!UICONTROL Creare una nuova integrazione]** , procedi come segue:

   * In **[!UICONTROL Nome]** campo, immettere un nome descrittivo. Ad esempio: *DynamicMediaViewersIO*.

   * In **[!UICONTROL Descrizione]** immettere la descrizione dell&#39;integrazione.

   * In **[!UICONTROL Certificati a chiave pubblica]** area, carica il file della chiave pubblica (&#42;.crt) scaricato in precedenza in questi passaggi.

   * Sotto la **[!UICONTROL Selezionare un ruolo per l’API dei tag di Experience Platform]** intestazione, selezionare **[!UICONTROL Amministratore]**.

   * Sotto la **[!UICONTROL Seleziona uno o più profili di prodotto per Experience Platform API Tag]** , seleziona il profilo di prodotto denominato **[!UICONTROL Tag - &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Seleziona **[!UICONTROL Creare un’integrazione]**.
1. Sulla **[!UICONTROL Integrazione creata]** pagina, seleziona **[!UICONTROL Informazioni sull’integrazione]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Viene visualizzata una pagina dei dettagli delle integrazioni, **** simile al seguente:

   >[!NOTE]
   >
   >***Lascia aperta la pagina dei dettagli di integrazione***. Avrete bisogno di varie informazioni dal **[!UICONTROL Panoramica]** e **[!UICONTROL JWT]** tra un attimo.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   Pagina dei dettagli di integrazione.

1. Torna alla pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** che hai lasciato aperta in precedenza. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Successivo]** per aprire **[!UICONTROL Account]** nella pagina **[!UICONTROL Configurazione dell’account tecnico Adobe IMS]** finestra.

   Se hai chiuso la pagina prima, torna ad Experience Manager Author e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**. Seleziona **[!UICONTROL Crea]**. In **[!UICONTROL Soluzione cloud]** elenco a discesa, seleziona **[!UICONTROL Experience Platform di tag]**. Nell’elenco a discesa **[!UICONTROL Certificato]**, fai clic sul nome del certificato creato in precedenza.)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Configurazione account tecnico Adobe IMS: pagina Certificato.

1. La **[!UICONTROL Account]** La pagina contiene cinque campi che devi compilare utilizzando le informazioni della pagina dei dettagli di integrazione del passaggio precedente.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Configurazione account tecnico Adobe IMS: pagina Account.

1. Sulla **[!UICONTROL Account]** , compila i campi seguenti:

   * **[!UICONTROL Titolo]** - Inserire un titolo descrittivo del conto.
   * **[!UICONTROL Server autorizzazioni]** - Torna alla pagina dei dettagli di integrazione aperta in precedenza. Seleziona la **[!UICONTROL JWT]** scheda . Copia il nome del server, senza il percorso, come evidenziato di seguito.

(il nome del server è solo un esempio)   Torna alla pagina **[!UICONTROL Account]**, quindi incolla il nome nel rispettivo campo.
Ad esempio: `https://ims-na1.adobelogin.com/`
(il nome del server è solo un esempio)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   Pagina dei dettagli dell’integrazione - Scheda JWT

1. **[!UICONTROL Chiave API]**: torna alla pagina dei dettagli di integrazione. Seleziona la **[!UICONTROL Panoramica]** , quindi a destra del **[!UICONTROL Chiave API (ID client)]** campo , seleziona **[!UICONTROL Copia]**.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla la chiave nel rispettivo campo.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   Pagina dei dettagli di integrazione.

1. **[!UICONTROL Segreto client]**: torna alla pagina dei dettagli di integrazione. Da **[!UICONTROL Panoramica]** scheda , seleziona **[!UICONTROL Recupera segreto client]**. A destra del **[!UICONTROL Segreto client]** campo , seleziona **[!UICONTROL Copia]**.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla la chiave nel rispettivo campo.

1. **[!UICONTROL Payload]** - Torna alla pagina dei dettagli di integrazione . Da **[!UICONTROL JWT]** , nel campo Payload JWT , copia l’intero codice oggetto JSON.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla il codice nel rispettivo campo.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   Pagina dei dettagli di integrazione - Scheda JWT

   La pagina Account , con tutti i campi compilati, ha un aspetto simile al seguente:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Vicino all&#39;angolo superiore destro del **[!UICONTROL Account]** pagina, seleziona **[!UICONTROL Crea]**.

   Con Experience Manager IMS configurato, ora hai un nuovo account IMSA elencato in **[!UICONTROL Configurazioni Adobe IMS]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configurare Experience Platform Tag Cloud per l’integrazione {#configuring-adobe-launch-cloud-for-the-integration}

1. In Experience Manager Author, nell’angolo in alto a sinistra, seleziona la **[!UICONTROL Strumenti]** icona (martello), quindi vai a **[!UICONTROL Cloud Services]** > **[!UICONTROL Experience Platform di configurazioni dei tag]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. Sulla **[!UICONTROL Experience Platform di configurazioni dei tag]** nel pannello a sinistra, selezionate un sito di Experience Manager per il quale desiderate applicare la configurazione dei tag di Experience Platform.

   Solo a scopo esemplificativo, il **`We.Retail`** il sito viene selezionato nella schermata seguente.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL Crea]**.
1. Sulla **[!UICONTROL Generale]** pagina (1/3 pagine) del **[!UICONTROL Creare la configurazione dei tag di Experience Platform]** , compila i campi seguenti:

   * **[!UICONTROL Titolo]** - Inserisci un titolo di configurazione descrittivo. Esempio: `We.Retail Tags cloud configuration`.

   * **[!UICONTROL Configurazione Adobe IMS associata]** - Seleziona la configurazione IMS creata in precedenza in [Configurare Experience Manager IMS](#configuring-aem-ims).

   * **[!UICONTROL Azienda]** - Dal **[!UICONTROL Azienda]** dall’elenco a discesa, seleziona la società di Experienci Cloud. L’elenco viene compilato automaticamente.

   * **[!UICONTROL Proprietà]** - Dall’elenco a discesa Proprietà , seleziona la proprietà Tag Experience Platform creata in precedenza. L’elenco viene compilato automaticamente.
   Dopo aver completato tutti i campi, **[!UICONTROL Generale]** La pagina avrà un aspetto simile al seguente:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Nell’angolo in alto a sinistra, seleziona **[!UICONTROL Successivo]**.
1. Sulla **[!UICONTROL Staging]** pagina (2/3 pagine) del **[!UICONTROL Creare la configurazione dei tag di Experience Platform]** , compila il seguente campo:

   In **[!UICONTROL URI libreria]** (Uniform Resource Identifier), controlla il percorso della versione di staging della libreria dei tag di Experience Platform. Experience Manager compila automaticamente questo campo.

   Solo per scopi di esempio, questo passaggio utilizza librerie di tag di Experience Platform distribuite in Adobe CDN.

   >[!NOTE]
   >
   >Controlla che l&#39;URI della libreria popolata automaticamente (Uniform Resource Identifier) non sia malformato. Se necessario, correggilo in modo che l’URI rappresenti un URI relativo al protocollo. Cioè, inizia da una doppia barra in avanti.
   >
   >
   >Esempio: `//assets.adobetm.com/launch-xxxx`.

   Le **[!UICONTROL Staging]** probabilmente la pagina sarà simile alla seguente. La **[!UICONTROL Archivia]** e **[!UICONTROL Carica libreria in modo asincrono]** le opzioni ***not*** set:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Nell’angolo in alto a destra, seleziona **[!UICONTROL Successivo]**.
1. Sulla **[!UICONTROL Produzione]** pagina (3/3 pagine) del **[!UICONTROL Creare la configurazione dei tag di Experience Platform]** Se necessario, correggi l’URI di produzione con popolamento automatico in modo simile a come è stato fatto nel precedente **[!UICONTROL Staging]** pagina.
1. Nell’angolo in alto a destra, seleziona **[!UICONTROL Crea]**.

   La nuova configurazione cloud dei tag di Experience Platform viene ora creata ed elencata accanto al sito web, in modo simile all’esempio seguente:

1. Seleziona la nuova configurazione cloud dei tag di Experience Platform (viene visualizzato un segno di spunta a sinistra del titolo della configurazione quando è selezionato). Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblica]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Attualmente, Experience Manager Author non supporta l’integrazione dei visualizzatori Dynamic Media con tag Experience Platform.

È tuttavia supportato nel nodo di pubblicazione Experience Manager. Utilizzando le impostazioni predefinite di Experience Platform Tags Cloud Configuration, il nodo di pubblicazione di Experience Manager utilizza l’ambiente di produzione di Experience Platform Tags. Di conseguenza, è necessario inviare ogni volta durante il test gli aggiornamenti della libreria Tag di Experience Platform da Sviluppo all’ambiente di produzione.

È possibile aggirare questa limitazione. Specifica l’URL di sviluppo o staging della libreria Tag piattaforma nella configurazione Experience Platform Tags Cloud per il nodo di pubblicazione Experience Manager di cui sopra. In questo modo il nodo di pubblicazione Experience Manager utilizza la versione di Sviluppo o Staging della libreria Tag Experience Platform.

Vedi [Integrare Experience Manager con i tag di Experience Platform tramite [!DNL Adobe I/O]](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=it) per ulteriori informazioni sulla configurazione di Experience Platform Tags Cloud Configuration.
