---
title: Integrazione dei visualizzatori Dynamic Media con Adobe Analytics e Adobe Launch
description: Con l’estensione Dynamic Media Viewers per Adobe Launch, rilasciata con Dynamic Media Viewers 5.13, i clienti di Dynamic Media, Adobe Analytics e Adobe Launch possono utilizzare eventi e dati specifici per i visualizzatori Dynamic Media nella propria configurazione di Adobe Launch.
uuid: d218ee1c-cd2c-40c3-a3d4-b95719ae8e98
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: f4051767-182e-4cfd-9dfc-8f516378e0b6
docset: aem65
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '6596'
ht-degree: 17%

---


# Integrazione dei visualizzatori Dynamic Media con Adobe Analytics e Adobe Launch {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Che cos’è l’integrazione dei visualizzatori Dynamic Media con  Adobe Analytics e  lancio Adobe? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

La nuova estensione *Dynamic Media Viewers* per  lancio Adobe, insieme alla versione recente di Dynamic Media Viewers 5.13, consente ai clienti di Dynamic Media,  Adobe Analytics e  lancio del Adobe di utilizzare eventi e dati specifici per i visualizzatori Dynamic Media nella configurazione  lancio del Adobe.

Questa integrazione consente di monitorare l’utilizzo dei visualizzatori Dynamic Media sul sito Web con  Adobe Analytics. Allo stesso tempo, potete utilizzare gli eventi e i dati esposti dai visualizzatori con qualsiasi altra estensione Launch proveniente da  Adobe o da terzi.

Per ulteriori informazioni sulle estensioni, vedere [ Adobe Extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/overview.html#adobe-extension) nella Guida utente del Experience Platform Launch.

**Chi dovrebbe leggere questa documentazione:** amministratori di siti, sviluppatori sulla piattaforma AEM e addetti alle operazioni.

### Limiti dell&#39;integrazione {#limitations-of-the-integration}

* &#39;integrazione Lancio Adobe per i visualizzatori Dynamic Media non funziona nel nodo di creazione AEM. Non è possibile visualizzare alcun tracciamento da una pagina WCM finché non viene pubblicata.
* ’integrazione Lancio Adobe per i visualizzatori Dynamic Media non è supportata per la modalità operativa a comparsa, in cui l’URL del visualizzatore viene ottenuto utilizzando il pulsante &quot;URL&quot; nella pagina Dettagli risorsa.
* &#39;integrazione Lancio Adobe non può essere utilizzata simultaneamente con l&#39;integrazione dei visualizzatori precedenti Analytics (tramite il parametro `config2=`).
* Il supporto per il tracciamento video è limitato solo al tracciamento della &quot;riproduzione principale&quot;, come descritto in [Panoramica del tracciamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). In particolare, il monitoraggio di QoS, Annunci, Capitolo/Segmenti o Errori non è supportato.
* La configurazione della durata dell&#39;archiviazione per gli elementi dati non è supportata per gli elementi dati che utilizzano l&#39;estensione *Dynamic Media Viewers*. La durata dell&#39;archiviazione deve essere impostata su **[!UICONTROL None]**.

### Casi di utilizzo per l&#39;integrazione {#use-cases-for-the-integration}

L&#39;integrazione con  Adobe Launch è un caso d&#39;uso principale per i clienti che utilizzano sia  AEM Assets che  AEM Sites. In questi scenari, potete impostare un&#39;integrazione standard tra il nodo di creazione AEM e  lancio del Adobe, quindi associare l&#39;istanza di Siti alla proprietà  Adobe Lancio. In seguito, qualsiasi componente Dynamic Media WCM aggiunto a una pagina Siti terrà traccia dei dati e degli eventi dei visualizzatori.

Consultate [Il tracciamento dei visualizzatori Dynamic Media in  AEM Sites](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersinAEMSites).

Un caso d&#39;uso secondario supportato dall&#39;integrazione sono i clienti che utilizzano  solo AEM Assets o Dynamic Media Classic. In questi casi, potete ottenere il codice da incorporare per il visualizzatore e aggiungerlo alla pagina del sito Web. Quindi, ottenete l&#39;URL di produzione della libreria Lancio  Adobe da  lancio Adobe e aggiungetelo manualmente al codice della pagina Web.

Consultate [Il tracciamento dei visualizzatori Dynamic Media tramite codice da incorporare](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode).

## Funzionamento del tracciamento dei dati e degli eventi nell&#39;integrazione {#how-data-and-event-tracking-works-in-the-integration}

L&#39;integrazione sfrutta due tipi distinti e indipendenti di monitoraggio dei visualizzatori Dynamic Media: *Adobe Analytics* e *Adobe Analytics per audio e video*.

### Informazioni sul tracciamento mediante  Adobe Analytics {#about-tracking-using-adobe-analytics}

 Adobe Analytics consente di tenere traccia delle azioni eseguite dall’utente finale quando interagisce con i visualizzatori Dynamic Media sul sito Web.  Adobe Analytics consente inoltre di tenere traccia dei dati specifici del visualizzatore. Ad esempio, potete tenere traccia e registrare gli eventi di caricamento della visualizzazione insieme al nome della risorsa, le azioni di zoom che si sono verificate, le azioni di riproduzione video e così via.

In  Adobe Launch, i concetti di *Elementi dati* e *Regole* funzionano insieme per abilitare  tracciamento Adobe Analytics.

#### Informazioni sugli elementi di dati nel lancio  Adobe {#about-data-elements-in-adobe-launch}

Un elemento dati in  lancio Adobe è una proprietà denominata il cui valore è definito in modo statico o calcolato in modo dinamico in base allo stato di una pagina Web o dei dati dei visualizzatori Dynamic Media.

Le opzioni disponibili per una definizione di elemento dati dipendono dall&#39;elenco delle estensioni installate nella proprietà di avvio del Adobe . L&#39;estensione &quot;Core&quot; è preinstallata ed è disponibile in qualsiasi configurazione. Questa estensione &quot;Core&quot; consente di definire un elemento dati che proviene da cookie, codice JavaScript, stringa di query e molte altre origini.

Per  tracciamento Adobe Analytics è necessario installare diverse estensioni aggiuntive, come descritto in [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions). L’estensione dei visualizzatori Dynamic Media consente di definire un elemento dati che rappresenta un argomento dell’evento per visualizzatori dinamici. Ad esempio, è possibile fare riferimento al tipo di visualizzatore, o al nome della risorsa riportato dal visualizzatore al momento del caricamento, al livello di zoom riportato quando l’utente finale esegue lo zoom e molto altro ancora.

L’estensione Dynamic Media Viewer mantiene automaticamente aggiornati i valori degli elementi dati.

Dopo averlo definito, un elemento dati può essere utilizzato in altre aree dell&#39;interfaccia utente di avvio  Adobe, utilizzando il widget del selettore Elemento dati. In particolare, agli elementi dati definiti ai fini del tracciamento dei visualizzatori Dynamic Media verrà fatto riferimento da Imposta variabili azione  estensione Adobe Analytics nella regola (vedere di seguito).

Per ulteriori informazioni, vedere [Elementi dati](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/data-elements.html#reference) nella Guida utente dell&#39;Experience Platform Launch.

#### Informazioni sulle regole  lancio Adobe {#about-rules-in-adobe-launch}

Una regola  lancio Adobe è una configurazione agnostica che definisce tre aree che compongono una regola: *Eventi*, *Condizioni* e *Azioni*:

* *Gli eventi*  (if) informano  Adobe di avviare quando attivare una regola.
* *Condizioni*  (se)  Adobe Avviate quali ulteriori restrizioni consentire o rifiutare quando viene attivata una regola.
* *Azioni*  (quindi)  Adobe Comunicare cosa fare quando viene attivata una regola.

Le opzioni disponibili nella sezione Eventi, Condizioni e Azioni dipendono dalle estensioni installate in  Adobe Launch Property. L&#39;estensione *Core* è preinstallata ed è disponibile out-of-the-box in qualsiasi configurazione. L&#39;estensione offre diverse opzioni per gli eventi, ad esempio azioni di base a livello di browser che includono la modifica dello stato attivo, la pressione di tasti, l&#39;invio di moduli e così via. Include inoltre opzioni per Condizioni, come il valore del cookie, il tipo di browser e altro. Per le azioni, è disponibile solo l&#39;opzione Codice personalizzato.

Per  tracciamento Adobe Analytics, è necessario installare diverse estensioni aggiuntive, come descritto in [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions). In particolare:

* L’estensione dei visualizzatori Dynamic Media estende l’elenco degli eventi supportati agli eventi specifici per i visualizzatori Dynamic Media quali il caricamento del visualizzatore, lo scambio di risorse, lo zoom in e la riproduzione video.
*  estensione Adobe Analytics estende l&#39;elenco delle azioni supportate con due azioni necessarie per inviare i dati ai server di monitoraggio: *Imposta variabili* e *Invia beacon*.

Per tenere traccia dei visualizzatori Dynamic Media è possibile utilizzare uno dei seguenti tipi:

* Eventi da estensione visualizzatori Dynamic Media, estensione Core o qualsiasi altra estensione.
* Condizioni nella definizione della regola. In alternativa, è possibile lasciare vuota l&#39;area delle condizioni.

Nella sezione Azioni, è necessaria un&#39;azione *Imposta variabili*. Questa azione indica  Adobe Analytics come compilare le variabili di tracciamento con i dati. Allo stesso tempo, l&#39;azione *Imposta variabili* non invia nulla al server di tracciamento.

L&#39;azione *Imposta variabili* deve essere seguita da un&#39;azione *Invia beacon*. L&#39;azione *Invia beacon* in realtà invia dati al server di tracciamento analisi. Entrambe le azioni, *Set Variables* e *Send Beacon*, provengono dall&#39;estensione Adobe Analytics .

Per ulteriori informazioni, vedere [Rules](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html#reference) nella Guida utente del Experience Platform Launch.

#### Configurazione di esempio {#sample-configuration}

La seguente configurazione di esempio all’interno  lancio del Adobe illustra come tenere traccia del nome di una risorsa al caricamento del visualizzatore.

1. Dalla scheda **[!UICONTROL Elementi dati]**, definire un elemento dati `AssetName` che faccia riferimento al parametro `asset` dell&#39;evento `LOAD` dall&#39;estensione dei visualizzatori Dynamic Media.

   ![image2019-11](assets/image2019-11.png)

1. Dalla scheda **[!UICONTROL Rules]**, definire una regola *TrackAssetOnLoad*.

   In questa regola, il campo **[!UICONTROL Event]** utilizza l&#39;evento **[!UICONTROL LOAD]** dall&#39;estensione dei visualizzatori Dynamic Media.

   ![image2019-22](assets/image2019-22.png)

1. La configurazione Azione ha due tipi di Azione dall&#39;estensione Adobe Analytics :

   *Impostate Variabili*, che associano una variabile di analisi di vostra scelta al valore di Elemento  `AssetName` dati.

   *Invia beacon*, che invia le informazioni di tracciamento a  Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. La configurazione della regola risultante sarà simile alla seguente:

   ![image2019-4](assets/image2019-4.png)

### Informazioni  Adobe Analytics per audio e video {#about-adobe-analytics-for-audio-and-video}

Quando un account di Experience Cloud  è registrato per utilizzare  Adobe Analytics per audio e video, è sufficiente abilitare il tracciamento video nelle impostazioni di estensione *Dynamic Media Viewers*. Le metriche video diventano disponibili in  Adobe Analytics. Il tracciamento video dipende dalla presenza di  Adobe Media Analytics per l’estensione audio e video.

Vedere [Installazione e configurazione di estensioni](#installing-and-setup-of-extensions).

Al momento, il supporto per il tracciamento video è limitato solo al tracciamento della &quot;riproduzione di base&quot;, come descritto in [Panoramica del tracciamento](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events). In particolare, il monitoraggio di QoS, Annunci, Capitolo/Segmenti o Errori non è supportato.

## Utilizzo dell&#39;estensione visualizzatori Dynamic Media {#using-the-dynamic-media-viewers-extension}

Come indicato in [Casi di utilizzo per l&#39;integrazione](#use-cases-for-the-integration), è possibile tenere traccia dei visualizzatori Dynamic Media con la nuova integrazione di Launch Adobe  in  AEM Sites e utilizzando il codice da incorporare.

### Tracciamento dei visualizzatori Dynamic Media in  AEM Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Per tenere traccia dei visualizzatori Dynamic Media in  AEM Sites, è necessario eseguire tutti i passaggi elencati nella sezione [Configurazione di tutti i pezzi di integrazione](#configuring-all-the-integration-pieces). In particolare, è necessario creare la configurazione IMS e la configurazione di Launch Cloud del Adobe .

In base alla configurazione corretta, qualsiasi visualizzatore Dynamic Media aggiunto a una pagina Siti, utilizzando un componente WCM supportato da Dynamic Media, tiene traccia automaticamente dei dati  Adobe Analytics,  Adobe Analytics per i video o entrambi.

<!-- To be reviewed and updated although this is found live in the AEMaaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### Tracciamento dei visualizzatori Dynamic Media con codice da incorporare {#tracking-dynamic-media-viewers-using-embed-code}

I clienti che non utilizzano  visualizzatori AEM Sites o che incorporano Dynamic Media in pagine Web esterne  AEM Sites, o entrambi, possono comunque utilizzare l&#39;integrazione  Adobe Launch.

Devi completare i passaggi di configurazione delle sezioni [Configurazione di Adobe Analytics](#configuring-adobe-analytics-for-the-integration) e [Configurazione di Adobe Launch](#configuring-adobe-launch-for-the-integration). Tuttavia, i passaggi di configurazione relativi ad AEM non sono necessari.

Dopo la corretta configurazione, potete aggiungere  supporto per Lancio Adobe a una pagina Web con un visualizzatore Dynamic Media.

Per ulteriori informazioni sull&#39;utilizzo  codice da incorporare della libreria Lancio, vedere [Aggiungere il codice da incorporare della libreria Lancio](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html#configure-launch).

<!-- To be reviewed and updated although this is found live in the AEMaaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of AEM Dynamic Media.
-->

**Per tenere traccia dei visualizzatori Dynamic Media mediante il codice** incorporato:

1. Tenete pronta una pagina Web per incorporare un visualizzatore Dynamic Media.
1. Ottenete il codice da incorporare per  libreria Lancio Adobe effettuando prima l&#39;accesso  Lancio del Adobe (consultate [Configurazione  Lancio Adobe](#configuring-adobe-launch-for-the-integration)).
1. Fare clic su **[!UICONTROL Property]**, quindi fare clic sulla scheda **[!UICONTROL Ambienti]**.
1. Consente di alzare il livello Ambiente in base all&#39;ambiente della pagina Web. Quindi, nella colonna **[!UICONTROL Install]**, fare clic sull&#39;icona della casella.
1. **[!UICONTROL Nella finestra di dialogo]** Istruzioni per l&#39;installazione Web, copiate il codice da incorporare della libreria di avvio Adobe completo insieme ai  `<script/>` tag circostanti.

## Guida di riferimento per l&#39;estensione dei visualizzatori Dynamic Media {#reference-guide-for-the-dynamic-media-viewers-extension}

### Informazioni sulla configurazione dei visualizzatori Dynamic Media {#about-the-dynamic-media-viewers-configuration}

L’estensione Dynamic Media Viewer si integra automaticamente con la libreria  Adobe Launch se tutte le seguenti condizioni sono soddisfatte:

*  oggetto globale della libreria Lancio Adobe ( `_satellite`) è presente nella pagina.
* La funzione di estensione dei visualizzatori Dynamic Media `_dmviewers_v001()` è definita in `_satellite`.

* `config2=` il parametro del visualizzatore non è specificato, il che significa che il visualizzatore non utilizza l&#39;integrazione Analytics precedente.

Inoltre, è disponibile un&#39;opzione per disabilitare in modo esplicito &#39;integrazione Lancio Adobe nel visualizzatore specificando il parametro `launch=0` nella configurazione del visualizzatore. Il valore predefinito di questo parametro è `1`.

### Configurazione dell&#39;estensione dei visualizzatori Dynamic Media {#configuring-the-dynamic-media-viewers-extension}

L&#39;unica opzione di configurazione per l&#39;estensione dei visualizzatori Dynamic Media è **[!UICONTROL Abilita  Adobe Media Analytics per audio e video]**.

Quando selezionate (attivate o &quot;attivate&quot;) questa opzione e se &#39;estensione Audio e Video Analytics Adobe è installata e configurata correttamente, le metriche di riproduzione video vengono inviate alla soluzione  Adobe Analytics per Audio e Video. La disattivazione di questa opzione disattiva il tracciamento video.

Tenete presente che se abilitate questa opzione *senza* avere installato &#39;estensione Media Analytics for Audio and Video, l&#39;opzione non ha alcun effetto.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Gli elementi dati nell&#39;estensione dei visualizzatori Dynamic Media {#about-data-elements-in-the-dynamic-media-viewers-extension}

L’unico tipo di elemento di dati fornito dall’estensione Dynamic Media Viewers è **[!UICONTROL Evento visualizzatore]**, proveniente dall’elenco a discesa **[!UICONTROL Data Element Type (Tipo di elemento dati)]**.

Quando è selezionato, l&#39;Editor elemento dati esegue il rendering di un modulo con due campi:

* **[!UICONTROL DM viewers event data type (Tipo di dati evento visualizzatori DM)]**: un elenco a discesa che identifica tutti gli eventi visualizzatore supportati dall’estensione Dynamic Media Viewers che presentano argomenti, con l’aggiunta di un elemento **[!UICONTROL COMMON]** speciale. Un elemento **[!UICONTROL COMMON]** rappresenta un elenco di parametri evento che sono comuni a tutti i tipi di eventi inviati dai visualizzatori.
* **[!UICONTROL Parametro]**  di tracciamento - un argomento dell&#39;evento del visualizzatore Dynamic Media selezionato.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Consultate la [guida di riferimento dei visualizzatori Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) per l&#39;elenco degli eventi supportati per ciascun tipo di visualizzatore; andate a una sezione specifica del visualizzatore, quindi fate clic su Supporto per  sezione di tracciamento Adobe Analytics. Attualmente, la guida di riferimento dei visualizzatori Dynamic Media non documenta gli argomenti degli eventi.

Consideriamo ora il ciclo di vita dei visualizzatori Dynamic Media *Data Element*. Il valore di tale elemento dati viene popolato dopo che l&#39;evento visualizzatore Dynamic Media corrispondente si verifica sulla pagina. Ad esempio, se l&#39;elemento dati punta all&#39;evento **[!UICONTROL LOAD]** e al relativo argomento &quot;asset&quot;, il valore di tale elemento dati riceverà dati validi dopo che il visualizzatore avrà eseguito per la prima volta l&#39;evento LOAD. Se l&#39;elemento dati punta all&#39;evento **[!UICONTROL ZOOM]** e al relativo argomento &quot;scala&quot;, il valore di tale elemento dati resterà vuoto finché il visualizzatore non invia per la prima volta un evento **[!UICONTROL ZOOM]**.

Allo stesso modo, i valori di Elementi dati vengono aggiornati automaticamente quando il visualizzatore invia un evento corrispondente sulla pagina. L’aggiornamento del valore si verifica anche se l’evento specifico non è indicato nella configurazione Regola. Ad esempio, se l’elemento dati **[!UICONTROL ZoomScale]** è definito per il parametro “scale” dell’evento ZOOM, ma l’unica regola presente nella configurazione Regola è attivata dall’evento **[!UICONTROL LOAD]**, il valore di **[!UICONTROL ZoomScale]** viene comunque aggiornato ogni volta che un utente esegue lo zoom all’interno del visualizzatore.

Qualsiasi visualizzatore Dynamic Media è dotato di un identificatore univoco sulla pagina web. L’elemento dati tiene traccia del valore stesso e del visualizzatore che lo ha popolato. In altre parole, se sulla stessa pagina vi sono diversi visualizzatori ed è presente un elemento dati **[!UICONTROL AssetName]** che punta all’evento **[!UICONTROL LOAD]** e al relativo argomento “asset”, l’elemento dati **[!UICONTROL AssetName]** mantiene una raccolta di nomi di risorse che sono associati a ciascun visualizzatore caricato sulla pagina.

Il valore esatto restituito dall&#39;elemento dati dipende dal contesto. Se l&#39;elemento dati è richiesto in una regola attivata da un evento visualizzatore Dynamic Media, il valore dell&#39;elemento dati viene restituito per il visualizzatore che ha avviato la regola. Inoltre, se l&#39;elemento dati è richiesto in una regola attivata da un evento da un&#39;altra estensione Lancio  Adobe, il valore dell&#39;elemento dati è il valore del visualizzatore che è stato l&#39;ultimo ad aggiornare l&#39;elemento dati.

**Considerate la seguente impostazione** di esempio:

* Una pagina Web con due visualizzatori zoom Dynamic Media; verranno utilizzati come *visualizzatore1* e *visualizzatore2*.

* **[!UICONTROL L&#39;elemento]** ZoomScaleData punta all&#39; **** evento ZOOMevent e al relativo argomento &quot;scala&quot;.
* **[!UICONTROL TrackPanRule]** con le seguenti caratteristiche:

   * Utilizza l&#39;evento Dynamic Media Viewer **[!UICONTROL PAN]** come attivatore.
   * Invia il valore di **[!UICONTROL ZoomScale]** Data Element a  Adobe Analytics.

* **** TrackKeyRule con le seguenti caratteristiche:

   * Utilizza l&#39;evento di pressione tasti dall&#39;estensione Core  Adobe Launch come attivatore.
   * Invia il valore di **[!UICONTROL ZoomScale]** Data Element a  Adobe Analytics.

A questo punto, si supponga che l’utente finale carichi la pagina Web con i due visualizzatori. In *visualizzatore1*, lo zoom viene effettuato su una scala del 50%; quindi, in *viewer2*, viene applicato lo zoom in una scala del 25%. In *viewer1*, l&#39;immagine viene spostata e infine viene selezionato un tasto sulla tastiera.

L&#39;attività dell&#39;utente finale determina l&#39;effettuazione di due chiamate di tracciamento a  Adobe Analytics:

* La prima chiamata si verifica perché la regola **[!UICONTROL TrackPan]** viene attivata quando l&#39;utente esegue il panning in *viewer1*. Tale chiamata invia il 50% come valore dell&#39;elemento dati **[!UICONTROL ZoomScale]** perché l&#39;elemento dati sa che la regola viene attivata da *viewer1* e recupera il valore di scala corrispondente;
* La seconda chiamata si verifica perché la regola **[!UICONTROL TrackKey]** viene attivata quando l&#39;utente preme un tasto sulla tastiera. Tale chiamata invia il 25% come valore dell&#39;elemento dati **[!UICONTROL ZoomScale]** perché la regola non è stata attivata dal visualizzatore. Di conseguenza, l&#39;elemento dati restituisce il valore più aggiornato.

Il campione impostato sopra incide anche sulla durata del valore Data Element. Il valore dell’elemento dati gestito da Dynamic Media Viewer è memorizzato nel codice della libreria di avvio Adobe  anche dopo che il visualizzatore stesso è stato eliminato dalla pagina Web. Questo significa che se è presente una regola attivata da un’estensione di visualizzatore non Dynamic Media e che fa riferimento a tale elemento dati, l’elemento dati restituisce l’ultimo valore noto, anche se il visualizzatore non è più presente sulla pagina Web.

In ogni caso, i valori degli elementi dati guidati dai visualizzatori Dynamic Media non sono memorizzati nell&#39;archivio locale o sul server; vengono invece conservati solo nella libreria Lancio Adobe lato client  lato client. I valori di tale Data Element scompaiono quando la pagina Web viene ricaricata.

In genere, l&#39;editor Data Element supporta la selezione della durata di archiviazione [a1/>. ](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/data-elements.html?lang=en#create-a-data-element) Tuttavia, gli elementi dati che utilizzano l&#39;estensione dei visualizzatori Dynamic Media supportano solo l&#39;opzione di durata dell&#39;archiviazione **[!UICONTROL None]**. L&#39;impostazione di qualsiasi altro valore è possibile nell&#39;interfaccia utente, ma in questo caso il comportamento Elemento dati non è definito. L&#39;estensione gestisce il valore dell&#39;elemento dati autonomamente: l&#39;elemento dati che mantiene il valore dell&#39;argomento evento del visualizzatore durante l&#39;intero ciclo di vita del visualizzatore.

### Informazioni sulle regole nell&#39;estensione dei visualizzatori Dynamic Media {#about-rules-in-the-dynamic-media-viewers-extension}

Nell&#39;editor Regola, l&#39;estensione aggiunge nuove opzioni di configurazione per l&#39;editor Eventi. Inoltre, fornisce un&#39;opzione per fare riferimento manualmente ai parametri dell&#39;evento nell&#39;Editor azione come opzione di breve durata, anziché utilizzare elementi dati preconfigurati.

#### Informazioni sull&#39;editor eventi {#about-the-events-editor}

Nell’editor evento, l’estensione Dynamic Media Viewers aggiunge un nuovo **[!UICONTROL Tipo evento]** denominato **[!UICONTROL Evento visualizzatore]**.

Quando è selezionato, l&#39;Editor evento esegue il rendering degli eventi **[!UICONTROL visualizzatore Dynamic Media]** a discesa, elencando tutti gli eventi disponibili supportati dai visualizzatori Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Informazioni sull&#39;editor Azioni {#about-the-actions-editor}

L’estensione dei visualizzatori Dynamic Media consente di utilizzare i parametri evento dei visualizzatori Dynamic Media per mappare le variabili di analisi nell’editor Imposta variabili dell’estensione Adobe Analytics .

Il metodo più semplice per farlo consiste nel completare il seguente processo in due fasi:

* Innanzitutto, definite uno o più elementi dati, in cui ogni elemento dati rappresenta un parametro di un evento Dynamic Media Viewer.
* Infine, nell&#39;editor Imposta variabili dell&#39;estensione Adobe Analytics  fare clic sull&#39;icona del selettore Elemento dati (tre dischi impilati) per aprire la finestra di dialogo Seleziona elemento dati, quindi selezionare un elemento dati da esso.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

È tuttavia possibile adottare un approccio alternativo e ignorare la creazione di elementi dati. Per fare riferimento diretto a un argomento di un evento Dynamic Media Viewer: inserisci il nome completo dell’argomento dell’evento nel campo di immissione del **[!UICONTROL valore]** dell’assegnazione della variabile Analytics, circondato dai segni di percentuale (%). Esempio,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Si noti che esiste una differenza importante tra l&#39;utilizzo di Elementi dati e il riferimento dell&#39;argomento dell&#39;evento diretto. Per l&#39;elemento dati, non importa quale evento attivi l&#39;azione Imposta variabili, l&#39;evento che attiva la regola può essere correlato al visualizzatore dinamico (come un clic del mouse sulla pagina Web dall&#39;estensione Core). Tuttavia, quando si utilizza un riferimento a un argomento diretto, è importante garantire che l&#39;evento che attiva la regola corrisponda all&#39;argomento evento a cui fa riferimento.

Ad esempio, il riferimento a `%event.detail.dm.LOAD.asset%` restituisce il nome corretto della risorsa se la regola viene attivata dall’evento **[!UICONTROL LOAD]** dell’estensione Dynamic Media Viewer. Tuttavia, restituisce un valore vuoto per qualsiasi altro evento.

Nella tabella seguente sono elencati gli eventi del visualizzatore Dynamic Media e i relativi argomenti supportati:

<table>
 <tbody>
  <tr>
   <td>Nome evento visualizzatore</td>
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

## Configurazione di tutti i pezzi di integrazione {#configuring-all-the-integration-pieces}

**PRIMA DI INIZIARE**

Se non lo avete già fatto,  Adobe consiglia di rivedere tutta la documentazione precedente a questa sezione in modo da comprendere la completa integrazione.

Questa sezione descrive i passaggi di configurazione necessari per integrare i visualizzatori Dynamic Media con  Adobe Analytics e  Adobe Analytics per audio e video. Anche se è possibile utilizzare l’estensione dei visualizzatori Dynamic Media per altri scopi in  lancio del Adobe, tali scenari non sono inclusi in questa documentazione.

L&#39;integrazione verrà configurata nei seguenti prodotti  Adobe:

*  Adobe Analytics: configurerai le variabili di tracciamento e i rapporti.
*  Lancio Adobe: definirete una proprietà, una o più regole e uno o più elementi dati per abilitare il tracciamento del visualizzatore.

Inoltre, se questa soluzione di integrazione viene utilizzata con  AEM Sites, è necessario eseguire anche la seguente configurazione:

* [!DNL Adobe I/O] Console: l&#39;integrazione viene creata per  lancio Adobe.
* AEM nodo di authoring: configurazione IMS e configurazione  Adobe Launch cloud.

Come parte della configurazione, accertatevi di avere accesso a una società in Adobe Experience Cloud che ha già  Adobe Analytics e  lancio Adobe già attivato.

## Configurazione  Adobe Analytics per l&#39;integrazione {#configuring-adobe-analytics-for-the-integration}

Dopo aver configurato  Adobe Analytics, per l&#39;integrazione verranno configurate le seguenti impostazioni:

* Una suite di rapporti è inserita e selezionata.
* Le variabili di Analytics sono disponibili per ricevere i dati di tracciamento.
* Sono disponibili rapporti per visualizzare i dati raccolti all&#39;interno  Adobe Analytics.

Vedere anche [Guida all&#39;implementazione di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**Per configurare  Adobe Analytics per l&#39;integrazione**:

1. Per iniziare, accedi  Adobe Analytics dal Experience Cloud  [home page](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/). Nella barra dei menu, fate clic sull&#39;icona Soluzioni (una tabella di punti tre per tre) accanto all&#39;angolo superiore destro della pagina, quindi fate clic su **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Ora selezionerete una suite di rapporti.

### Selezione di una suite di rapporti {#selecting-a-report-suite}

1. Nell’angolo in alto a destra della pagina Adobe Analytics, alla destra del campo **[!UICONTROL Search Reports (Cerca rapporti)]**, seleziona la report suite corretta dall’elenco a discesa. Se sono disponibili più report suite e non sai quale utilizzare, contatta l’amministratore Adobe Analytics che ti fornirà supporto al riguardo.

   Nell&#39;illustrazione seguente, un utente ha creato una suite di rapporti denominata *DynamicMediaViewersExtensionDoc* e l&#39;ha selezionata dall&#39;elenco a discesa. Il nome della suite di rapporti è solo a scopo illustrativo; il nome della suite di rapporti selezionata differisce.

   Se non è disponibile alcuna suite di rapporti, l&#39;utente o l&#39;amministratore di Adobe Analytics  deve crearne una prima poter procedere ulteriormente con la configurazione.

   Vedere [Report e suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html#manage-report-suites) e [Creare una suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/create-report-suite.html#admin-console).

   In  Adobe Analytics, le suite di rapporti sono gestite in **[!UICONTROL Amministratore > Suite di rapporti]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   A questo punto  le variabili Adobe Analytics.

### Impostazione  variabili Adobe Analytics {#setting-up-adobe-analytics-variables}

1. A questo punto è possibile specificare una o più  variabili Adobe Analytics da usare per monitorare il comportamento dei visualizzatori Dynamic Media sulla pagina Web.

   È possibile utilizzare qualsiasi tipo di variabile supportata da  Adobe Analytics. La decisione relativa al tipo di variabile (come Custom Traffic [props], Conversion [ eVar]) deve essere determinata da esigenze specifiche dell&#39;implementazione Analytics.

   Vedere [Panoramica delle proprietà e delle eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   Ai fini di questa documentazione, verrà utilizzata solo una variabile Traffico personalizzato (prop), poiché diventano disponibili in un report di Analytics entro pochi minuti dall&#39;esecuzione di un&#39;azione su una pagina Web.

   Per abilitare una nuova variabile Custom Traffic (Traffico personalizzato), in  Adobe Analytics, sulla barra degli strumenti fare clic su **[!UICONTROL Admin > Report Suites]** (Amministratore > Suite di rapporti).

1. Nella pagina **[!UICONTROL Report Suite Manager]**, seleziona il rapporto corretto, quindi fai clic su **[!UICONTROL Edit Settings (Modifica impostazioni) > Traffic (Traffico) > Traffic Variables (Variabili traffico)]**.
1. Qui, selezionate la variabile non utilizzata, assegnatele un nome descrittivo ( **[!UICONTROL Risorsa visualizzatore (prop 30)]**) e modificate la casella combinata in &quot;Abilitato&quot; nella colonna Abilitato.

   La schermata seguente è un esempio di variabile Traffico personalizzato ( **[!UICONTROL prop30]**) per tenere traccia del nome di una risorsa utilizzata dal visualizzatore:

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. Nella parte inferiore dell&#39;elenco delle variabili, fare clic su **[!UICONTROL Salva]**.

### Impostazione di un report {#setting-up-a-report}

1. In genere, l&#39;impostazione di un report in  Adobe Analytics dipende da esigenze specifiche del progetto. Di conseguenza, la configurazione dettagliata dei report non rientra nell&#39;ambito di questa integrazione.

   È tuttavia sufficiente sapere che i report Custom Traffic (Traffico personalizzato) diventano automaticamente disponibili in  Adobe Analytics dopo l&#39;impostazione delle variabili Custom Traffic (Traffico personalizzato) in **[Impostazione  variabili Adobe Analytics](#setting-up-adobe-analytics-variables)**.

   Ad esempio, il rapporto per la variabile di **[!UICONTROL Viewer asset (Risorsa visualizzatore) (prop 30)]** è disponibile dal menu Rapporti di **[!UICONTROL Traffico personalizzato > Traffico personalizzato 21-30 > Viewer asset (Risorsa visualizzatore) (prop 30)]**.

   Se accedi a questo rapporto subito dopo la creazione di **[!UICONTROL Viewer asset (Risorsa visualizzatore) (prop 30)]** non troverai alcun dato, il che è piuttosto normale a questo punto dell’integrazione.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## Configurazione  lancio Adobe per l&#39;integrazione {#configuring-adobe-launch-for-the-integration}

Dopo aver configurato  Adobe Launch, per l&#39;integrazione verranno impostate le seguenti impostazioni:

* La creazione di una nuova proprietà per mantenere tutte le configurazioni unite.
* Installazione e configurazione delle estensioni. Il codice lato client di tutte le estensioni installate nella proprietà viene compilato insieme in una libreria. Questa libreria viene utilizzata dalla pagina Web in un secondo momento.
* Configurazione di elementi e regole dati. Questa configurazione definisce i dati da acquisire dai visualizzatori Dynamic Media, quando attivare la logica di tracciamento e dove inviare i dati del visualizzatore in  Adobe Analytics.
* Pubblicazione della libreria.

**Per configurare  lancio Adobe per l&#39;integrazione**:

1. Per iniziare, accedi  Adobe Launch dal Experience Cloud  [home page](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/). Nella barra dei menu, fate clic sull&#39;icona Soluzioni (tre per tre tabelle di punti) vicino all&#39;angolo superiore destro della pagina, quindi fate clic su **[!UICONTROL Avvia]**.

   È inoltre possibile [aprire  lancio Adobe direttamente](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Creazione di una proprietà in  lancio Adobe {#creating-a-property-in-adobe-launch}

Una proprietà in  lancio Adobe è una configurazione denominata che mantiene tutte le impostazioni insieme. Una libreria delle impostazioni di configurazione viene generata e pubblicata su diversi livelli di ambiente (sviluppo, staging e produzione).

Vedere anche [Creare una proprietà di avvio](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-mobile-android-apps-with-launch/configure-launch/launch-create-a-property.html#configure-launch).

1. In Lancio  Adobe, fare clic su **[!UICONTROL Nuova proprietà]**.
1. Nella finestra di dialogo **[!UICONTROL Crea proprietà]**, digita un nome descrittivo nel campo **[!UICONTROL Nome]**, ad esempio il titolo del tuo sito web. Esempio, `DynamicMediaViewersProp.`
1. Nel campo **[!UICONTROL Domains]**, immettete il dominio del sito Web.
1. Nel menu a discesa **[!UICONTROL Opzioni avanzate]**, abilitare **[!UICONTROL Configura per lo sviluppo delle estensioni (non può essere modificato in seguito)]** nel caso in cui l&#39;estensione da utilizzare, in questo caso, *Visualizzatori Dynamic Media*, non sia ancora stata rilasciata.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Fai clic su **[!UICONTROL Salva]**.

   Fare clic sulla proprietà appena creata, quindi procedere all&#39; *Installazione e configurazione delle estensioni*.

### Installazione e configurazione delle estensioni {#installing-and-setup-of-extensions}

Tutte le estensioni disponibili in  Adobe Launch sono elencate in **[!UICONTROL Estensioni > Catalog]**.

Per installare un&#39;estensione, fare clic su **[!UICONTROL Installa]**. Se necessario, eseguite una configurazione di estensione una tantum, quindi fate clic su **[!UICONTROL Salva]**.

Se necessario, devono essere installate e configurate le seguenti estensioni:

* (Obbligatorio) * servizio ID Experience Cloud *estensione

Non è necessaria alcuna configurazione aggiuntiva, accettare per eventuali valori proposti. Al termine, fare clic su **[!UICONTROL Salva]**.

Vedere [ Experience Cloud ID Service Extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html#extensions-ref).

* (Obbligatorio) *estensione Adobe Analytics*

Per configurare questa estensione, è innanzitutto necessario disporre dell’ID report suite presente all’interno di Adobe Analytics, accedendo ad **[!UICONTROL Admin > Report Suite]** e selezionando l’intestazione della colonna **[!UICONTROL ID report suite]**.

L’ID report suite di **[!UICONTROL DynamicMediaViewersExtensionDoc]** viene utilizzato nelle schermate seguenti solo a scopo dimostrativo. Questo ID è stato creato e utilizzato nella precedente sezione [Selezione di una report suite](#selecting-a-report-suite).

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

Nella pagina Installa estensione, immetti l’ID Report Suite nel campo **[!UICONTROL Development Report Suites]** (Report Suite di sviluppo), nel campo **[!UICONTROL Staging Report Suites]** (Report Suite di staging) e nel campo **[!UICONTROL Production Report Suites]** (Report Suite di produzione).

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configurate il seguente elemento solo se intendete utilizzare il tracciamento video:*

Nella pagina **[!UICONTROL Installa estensione]**, espandere **[!UICONTROL Generale]**, quindi specificare il server di tracciamento. Il server di tracciamento segue il modello `<trackingNamespace>.sc.omtrdc.net`, dove `<trackingNamespace>` sono le informazioni ottenute nel messaggio e-mail di provisioning.

Fai clic su **[!UICONTROL Salva]**.

Vedere [ Adobe Analytics Extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html#extensions-ref).

* (Facoltativo; richiesto solo se è necessario il tracciamento video) *Adobe Media Analytics for Audio and Video* extension

Compilare il campo del server di tracciamento. Il server di tracciamento per l&#39;estensione *Adobe Media Analytics for Audio and Video* è diverso dal server di tracciamento utilizzato per  Adobe Analytics. Segue il modello `<trackingNamespace>.hb.omtrdc.net`, dove `<trackingNamespace>` sono le informazioni contenute nel messaggio e-mail di provisioning.

Tutti gli altri campi sono facoltativi.

Consultate [ Adobe Media Analytics for Audio and Video Extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#extensions-ref).

* (Obbligatorio) Estensione *Visualizzatori Dynamic Media*

Per attivare il tracking Video Heartbeat, seleziona **[!UICONTROL enable Adobe Analytics for Video (Abilita Adobe Analytics per video)]**.

Al momento di questa scrittura, l&#39;estensione *Dynamic Media Viewers* è disponibile solo se per lo sviluppo è stata creata la proprietà di avvio del Adobe .

Vedere [Creazione di una proprietà in  Adobe Launch](#creating-a-property-in-adobe-launch).

Dopo che le estensioni sono installate e configurate, almeno, le seguenti cinque estensioni (quattro se non si sta monitorando video) saranno elencate nell&#39;area Estensioni > Installate.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Impostazione di elementi dati e regole {#setting-up-data-elements-and-rules}

In  lancio Adobe, create gli elementi dati e le regole necessari per tenere traccia dei visualizzatori Dynamic Media.

Per una panoramica del tracciamento con  lancio del Adobe, consultate [Funzionamento del tracciamento dei dati e degli eventi nell&#39;integrazione](#how-data-and-event-tracking-works-in-the-integration).

Consultate [Esempio di configurazione](#sample-configuration) per un esempio di configurazione in  lancio di Adobe che illustra come tenere traccia del nome di una risorsa al caricamento del visualizzatore.

Per informazioni dettagliate sulle funzionalità dell&#39;estensione, consultate [Configurazione dell&#39;estensione dei visualizzatori Dynamic Media](#configuring-the-dynamic-media-viewers-extension).

### Pubblicazione di una libreria {#publishing-a-library}

Per apportare modifiche alla configurazione di avvio del Adobe  (inclusa la configurazione di proprietà, estensioni, regole ed elementi dati), è necessario *pubblicare* tali modifiche*.* La pubblicazione in  lancio Adobe viene eseguita dalla scheda Pubblicazione nella configurazione Proprietà.

 Adobe Launch può disporre di più ambienti di sviluppo, un ambiente di gestione e un ambiente di produzione. Per impostazione predefinita, la configurazione di Launch Cloud del  Adobe in AEM indica il nodo AEM autore nell&#39;ambiente Stage  Launch del Adobe e il nodo AEM pubblicazione nell&#39;ambiente Produzione di  Launch del Adobe. Questo significa che, con le impostazioni di AEM predefinite, è necessario pubblicare la libreria  Adobe lancio nell&#39;ambiente di gestione temporanea in modo da utilizzarla in AEM&#39;autore, quindi pubblicarla nell&#39;ambiente di produzione in modo che possa essere utilizzata AEM pubblicazione.

Per ulteriori informazioni sugli ambienti di lancio  Adobe, vedere [Ambienti](https://experienceleague.adobe.com/docs/launch/using/reference/publish/environments/environments.html#environment-types).

La pubblicazione di una libreria comporta i due passaggi seguenti:

* Aggiunta e creazione di una nuova libreria, includendo tutte le modifiche necessarie (nuove e aggiornate) nella libreria.
* Spostamento della libreria verso l&#39;alto nei diversi livelli di ambiente (dallo sviluppo allo sviluppo allo sviluppo e alla produzione)

#### Aggiunta e creazione di una nuova libreria {#adding-and-building-a-new-library}

1. La prima volta che aprite la scheda Pubblicazione in  Adobe di avvio, l’elenco della libreria è vuoto.

   Nella colonna sinistra, fare clic su **[!UICONTROL Aggiungi nuova libreria]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. Nella pagina Crea nuova libreria, nel campo **[!UICONTROL Nome]** immettete un nome descrittivo per la nuova libreria. Esempio,

   *DynamicMediaViewersLib*

   Dall’elenco a discesa Ambiente, scegliete il livello Ambiente. Inizialmente, solo il livello di sviluppo è disponibile per la selezione. Vicino al lato inferiore sinistro della pagina, fare clic su **[!UICONTROL Aggiungi tutte le risorse modificate]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Nell&#39;angolo superiore destro della pagina, fare clic su **[!UICONTROL Salva e crea per lo sviluppo]**.

   In pochi minuti la libreria viene creata e pronta per l&#39;uso.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >Alla prossima modifica della configurazione di Adobe Launch, vai alla scheda **[!UICONTROL Pubblicazione]** nella configurazione di **[!UICONTROL Proprietà]**, quindi fai clic sulla libreria creata in precedenza.
   >
   >
   >Dalla schermata di pubblicazione della libreria, fate clic su **[!UICONTROL Aggiungi tutte le risorse modificate]**, quindi fate clic su **[!UICONTROL Salva e crea per lo sviluppo]**.

#### Spostamento di una libreria verso l&#39;alto attraverso i livelli di ambiente {#moving-a-library-up-through-environment-levels}

1. Dopo l&#39;aggiunta di una nuova libreria, questa si trova inizialmente nell&#39;ambiente di sviluppo. Per spostarlo al livello dell&#39;ambiente di gestione temporanea (corrispondente alla colonna Inviato), dal menu a discesa della libreria fare clic su **[!UICONTROL Invia per approvazione]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Nella finestra di dialogo di conferma, fare clic su **[!UICONTROL Invia]**.

   Quando la libreria si sposta sulla colonna Inviato, dal menu a discesa della libreria, fare clic su **[!UICONTROL Genera per gestione temporanea]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Seguite un processo simile per spostare la libreria dall&#39;ambiente di gestione temporanea all&#39;ambiente di produzione (che è la colonna Pubblicato).

   Innanzitutto, dal menu a discesa, fate clic su **[!UICONTROL Approva per la pubblicazione]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. Dal menu a discesa, fate clic su **[!UICONTROL Genera e pubblica su produzione]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consultate [Publishing](https://experienceleague.adobe.com/docs/launch/using/reference/publish/overview.html#reference) per ulteriori informazioni sul processo di pubblicazione in  lancio del Adobe.

## Configurazione di Adobe Experience Manager per l&#39;integrazione {#configuring-adobe-experience-manager-for-the-integration}

Prerequisiti:

* AEM esegue sia le istanze Author che Publish.
* AEM nodo di authoring è impostato in Dynamic Media - modalità di esecuzione Scene7 (dynamicmedia_s7)
* I componenti Dynamic Media WCM sono abilitati in  AEM Sites.

La configurazione AEM è composta dai due passaggi principali seguenti:

* Configurazione di AEM IMS.
* Configurazione di  Adobe Launch Cloud.

### Configurazione AEM IMS {#configuring-aem-ims}

1. In AEM autore, fate clic sull&#39;icona Strumenti (martello), quindi fate clic su **[!UICONTROL Protezione >  Adobe IMS Configurations]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Nella pagina Configurazione IMC del Adobe , accanto all&#39;angolo superiore sinistro, fare clic su **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]**, seleziona l’elenco a discesa **[!UICONTROL Soluzione Cloud]**, quindi fai clic su **[!UICONTROL Adobe Launch]**.
1. Abilita **[!UICONTROL Crea nuovo certificato]**, quindi nel campo di testo immetti qualsiasi valore significativo per il certificato. Ad esempio, *AdobeLaunchIMSCert*. Fai clic su **[!UICONTROL Crea certificato]**.

   Viene visualizzato il seguente messaggio Informazioni:

   *Per recuperare un token di accesso valido, è necessario aggiungere la chiave pubblica del nuovo certificato all&#39;account tecnico  Adobe I/O!*.

   Fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo Informazioni.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Fare clic su **[!UICONTROL Scarica chiave pubblica]** per scaricare un file di chiave pubblica (*.crt) nel sistema locale.

   >[!NOTE]
   >
   >A questo punto, ***lascia aperta*** la pagina **[!UICONTROL Adobe IMS Technical Account Configuration]**, ***non*** chiuderla e ***non*** fare clic su Avanti. Tornerai a questa pagina in un secondo momento.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. In una nuova scheda del browser, andate alla [[!DNL Adobe I/O] Console](https://console.adobe.io/integrations).

1. Dalla pagina **[!UICONTROL Adobe I/O Console Integrations]**, accanto all&#39;angolo superiore destro, fare clic su **[!UICONTROL Nuova integrazione]**.
1. Nella finestra di dialogo **[!UICONTROL Create a new integration (Crea una nuova integrazione)]**, accertati che sia selezionato il pulsante di scelta **[!UICONTROL Access an API (Accesso a un API)]**, quindi fai clic su **[!UICONTROL Continua]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. Nella seconda pagina **[!UICONTROL Crea una nuova integrazione]**, abilita (attiva) il pulsante di scelta **[!UICONTROL Experience Platform Launch API (API di Experience Platform Launch)]**. Nell’angolo inferiore destro della pagina, fai clic su **[!UICONTROL Continua]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Nella terza pagina **[!UICONTROL Crea una nuova integrazione]**, effettua le seguenti operazioni:

   * Nel campo **[!UICONTROL Name]**, immettere un nome descrittivo. Ad esempio, *DynamicMediaViewersIO*.

   * Nel campo **[!UICONTROL Description]**, immettere la descrizione per l&#39;integrazione.

   * Nell&#39;area **[!UICONTROL Certificati di chiave pubblica]**, carica il file di chiave pubblica (*.crt) che hai scaricato in precedenza in questi passaggi.

   * In **[!UICONTROL Selezionare un ruolo per l&#39;intestazione API di Experience Platform Launch]**, selezionare **[!UICONTROL Admin]**.

   * In **[!UICONTROL Selezionare uno o più profili di prodotto per l&#39;intestazione API di Experience Platform Launch]**, selezionare il profilo di prodotto denominato **[!UICONTROL Launch - &lt;nome_società>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Fare clic su **[!UICONTROL Crea integrazione]**.
1. Nella pagina **[!UICONTROL Integrazione creata]**, fare clic su **[!UICONTROL Continua con i dettagli di integrazione]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Viene visualizzata una pagina dei dettagli Integrations, **** simile alla seguente:

   >[!NOTE]
   >
   >***Lascia aperta la pagina dei dettagli di integrazione***. Tra poco ti occorreranno varie informazioni provenienti dalle schede **[!UICONTROL Panoramica]** e **[!UICONTROL JWT]**.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   Pagina dei dettagli dell&#39;integrazione.

1. Torna alla pagina **[!UICONTROL Configurazione account tecnico Adobe IMS]** che hai lasciato aperta in precedenza. Nell’angolo superiore destro della pagina, fai clic su **[!UICONTROL Avanti]** per aprire la pagina **[!UICONTROL Account]** alla finestra **[!UICONTROL Configurazione account tecnico Adobe IMS]**.

   Se hai chiuso la pagina accidentalmente, torna ad AEM Author e fai clic su **[!UICONTROL Strumenti > Protezione > Configurazioni Adobe IMS]**. Fai clic su **[!UICONTROL Crea]**. Nell’elenco a discesa **[!UICONTROL Soluzione Cloud]**, seleziona **[!UICONTROL Adobe Launch]**. Nell’elenco a discesa **[!UICONTROL Certificato]**, fai clic sul nome del certificato creato in precedenza.)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

    pagina Configurazione account tecnico IMS Adobe - Certificato.

1. La pagina **[!UICONTROL Account]** contiene cinque campi che dovranno essere compilati utilizzando le informazioni contenute nella pagina dei dettagli dell&#39;integrazione del passaggio precedente.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

    Adobe IMS Technical Account Configuration - Account.

1. Nella pagina **[!UICONTROL Account]**, compila i campi seguenti:

   * **[!UICONTROL Titolo]**  - Immettete un titolo di account descrittivo.
   * **[!UICONTROL Server]**  autorizzazioni: tornare alla pagina dei dettagli dell&#39;integrazione aperta in precedenza. Fare clic sulla scheda **[!UICONTROL JWT]**. Copiate il nome del server, senza il percorso, come evidenziato di seguito.

(il nome del server di esempio è solo a scopo illustrativo)   Torna alla pagina **[!UICONTROL Account]**, quindi incolla il nome nel rispettivo campo.
Ad esempio, `https://ims-na1.adobelogin.com/`
(il nome del server di esempio è solo a scopo illustrativo)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   Pagina dei dettagli dell&#39;integrazione - scheda JWT

1. **[!UICONTROL Chiave API]**: torna alla pagina dei dettagli di integrazione. Fai clic sulla scheda **[!UICONTROL Panoramica]**, quindi, a destra del campo **[!UICONTROL Chiave API (ID client)]**, fai clic su **[!UICONTROL Copia]**.

   Tornate alla pagina **[!UICONTROL Account]**, quindi incollate il tasto nel relativo campo ****.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   Pagina dei dettagli dell&#39;integrazione.

1. **[!UICONTROL Segreto client]**: torna alla pagina dei dettagli di integrazione. Nella scheda **[!UICONTROL Panoramica]**, fai clic su **[!UICONTROL Retrieve Client Secret (Recupera segreto client)]**. A destra del campo **[!UICONTROL Segreto client]**, fai clic su **[!UICONTROL Copia]**.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla la chiave nel rispettivo campo.

1. **[!UICONTROL Payload]**  - Torna alla pagina dei dettagli dell&#39;integrazione. Dalla scheda **[!UICONTROL JWT]**, nel campo Payload JWT, copiare l&#39;intero codice oggetto JSON.

   Torna alla pagina **[!UICONTROL Account]**, quindi incolla il codice nel rispettivo campo.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   Pagina dei dettagli dell&#39;integrazione - scheda JWT

   La pagina Account, con tutti i campi compilati, avrà un aspetto simile al seguente:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Account]**, fare clic su **[!UICONTROL Crea]**.

   Con AEM IMS configurato, ora è presente un nuovo account IMSA elencato in **[!UICONTROL Adobi IMS Configurations]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configurazione di  Adobe Launch Cloud per l&#39;integrazione {#configuring-adobe-launch-cloud-for-the-integration}

1. Nell&#39;autore AEM, accanto all&#39;angolo superiore sinistro, fare clic sull&#39;icona Strumenti (martello), quindi fare clic su **[!UICONTROL Cloud Services >  configurazioni di avvio Adobe]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. Nella pagina **[!UICONTROL Configurazioni lancio Adobe]**, nel pannello a sinistra, selezionate un sito AEM per il quale desiderate applicare  configurazione lancio Adobe.

   Solo a scopo illustrativo, il sito **[!UICONTROL We.Retail]** è selezionato nella schermata sottostante.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Fai clic su **[!UICONTROL Crea]** nell’angolo superiore sinistro della pagina.
1. Nella pagina **[!UICONTROL Generale]** (1/3 pagine) della finestra **[!UICONTROL Crea configurazione di Adobe Launch]**, compila i campi seguenti:

   * **[!UICONTROL Titolo]**  - Immettete un titolo di configurazione descrittivo. Esempio, `We.Retail Launch cloud configuration`.

   * **[!UICONTROL Configurazione]**  IMS Adobe  associata - Selezionate la configurazione IMS creata in precedenza in  [Configurazione AEM IMS](#configuring-aem-ims).

   * **[!UICONTROL Società]**  - Dall’elenco a discesa  **** Società, selezionate la società del Experience Cloud . L&#39;elenco viene compilato automaticamente.

   * **[!UICONTROL Proprietà]**  - Dall&#39;elenco a discesa Proprietà, selezionare la proprietà Lancio Adobe  creata in precedenza. L&#39;elenco viene compilato automaticamente.
   Dopo aver completato tutti i campi, la pagina **[!UICONTROL Generale]** avrà un aspetto simile al seguente:

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Vicino all&#39;angolo superiore sinistro, fare clic su **[!UICONTROL Avanti]**.
1. Nella pagina **[!UICONTROL Staging]** (2/3 pagine) della finestra **[!UICONTROL Crea configurazione di Adobe Launch]**, compila il seguente campo:

   Nel campo **[!UICONTROL URI libreria]**, verifica il percorso della versione di staging della libreria di Adobe Launch. AEM compila automaticamente questo campo.

   Solo a scopo illustrativo, questo passaggio utilizza  librerie Lancio Adobe distribuite  CDN Adobe.

   >[!NOTE]
   >
   >Verificare che l&#39;URI della libreria popolata automaticamente (Uniform Resource Identifier) non sia danneggiato. Se necessario, correggetelo in modo che l&#39;URI rappresenti un URI relativo al protocollo. Ovvero, inizia da una doppia barra in avanti.
   >
   >
   >Esempio: `//assets.adobetm.com/launch-xxxx`.

   La pagina **[!UICONTROL Staging]** deve avere un aspetto simile a quella riportata di seguito. Le opzioni **[!UICONTROL Archive (Archivia)]** e **[!UICONTROL Load Library Asynchronously (Carica libreria in modo asincrono)]** ***non*** sono impostate:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Nell&#39;angolo superiore destro, fare clic su **[!UICONTROL Avanti]**.
1. se necessario, nella pagina **[!UICONTROL Produzione]** (3/3 pagine) della finestra **[!UICONTROL Crea configurazione di Adobe Launch]**, correggi l’URI di produzione con compilazione automatica con una procedura simile a quanto già fatto nella pagina precedente di **[!UICONTROL Staging]**.
1. Nell&#39;angolo superiore destro, fare clic su **[!UICONTROL Crea]**.

   La nuova configurazione di Launch Cloud del Adobe viene ora creata ed elencata accanto al sito Web, in modo simile al seguente esempio:

1. Seleziona la nuova configurazione di Launch Cloud del Adobe  (quando è selezionata, viene visualizzato un segno di spunta a sinistra del titolo della configurazione). Sulla barra degli strumenti, fare clic su **[!UICONTROL Pubblica]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Al momento, AEM autore non supporta l’integrazione dei visualizzatori Dynamic Media con  lancio Adobe.

È tuttavia supportata nel nodo di pubblicazione AEM. Utilizzando le impostazioni predefinite di  Configurazione di Launch Cloud di Adobe, AEM pubblicazione utilizza l&#39;ambiente di produzione  Launch Adobe. In quanto tale, è necessario inviare  Adobe gli aggiornamenti della libreria Launch da Development all&#39;ambiente Production ogni volta durante il test.

È possibile ovviare a questo limite specificando l&#39;URL di sviluppo o di gestione temporanea della libreria di lancio di  Adobe nella configurazione  Adobe Launch Cloud per AEM pubblicazione precedente. In questo modo, il nodo di pubblicazione AEM utilizza la versione Sviluppo o Gestione temporanea della libreria  Lancio Adobe.

Per ulteriori informazioni sull&#39;impostazione  configurazione di Launch Cloud Adobe Adobe, vedere [Integrazione AEM con  lancio tramite  [!DNL Adobe I/O]](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html).
