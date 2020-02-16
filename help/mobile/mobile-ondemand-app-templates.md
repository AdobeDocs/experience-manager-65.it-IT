---
title: Creazione e aggiunta di modelli e componenti
seo-title: Creazione e aggiunta di modelli e componenti
description: Segui questa pagina per informazioni sulla creazione e l'aggiunta di modelli e componenti all'app. La pagina utilizza Geometrixx Unlimited App come app che contiene un modello di app di esempio e modelli di pagina.
seo-description: Segui questa pagina per informazioni sulla creazione e l'aggiunta di modelli e componenti all'app. La pagina utilizza Geometrixx Unlimited App come app che contiene un modello di app di esempio e modelli di pagina.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creazione e aggiunta di modelli e componenti {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

AEM Mobile On-Demand fornisce un modello di app completamente configurato, un modello di articolo e componenti articolo.

L&#39;app We.Unlimited è un modello di esempio che rappresenta la shell di un&#39;applicazione AEM Mobile On-Demand completamente configurabile e gestibile.

Selezionando questo modello di esempio durante la creazione di una nuova app, viene distribuito un dashboard ricco di funzioni di AEM Mobile.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>Per gestire l&#39;applicazione e il contenuto dell&#39;app mobile dal Centro di controllo delle app AEM Mobile, consultate il Pannello [applicazione](/help/mobile/mobile-apps-ondemand-application-dashboard.md)AEM Mobile.

## Creazione di modelli di app {#creating-app-templates}

Un modello app viene utilizzato per creare una nuova app e funge da raccolta di modelli di pagina e componenti che rappresentano una linea di base o una base di un&#39;app. Il modello elimina alcune proprietà fondamentali per guidare l&#39;app nel modo appropriato. In generale, un cliente non creerebbe troppe app in totale.

I modelli di app forniscono un modo semplice per sfruttare i progetti esistenti creati dagli sviluppatori, utilizzati per creare nuove app in AEM.

Quando crei una nuova app basata sul modello di un&#39;altra app, riceverai un&#39;app con un punto di partenza rappresentativo dell&#39;app da cui è stata creata.

Passaggi per creare una nuova app basata su un modello di app:

1. Andate al catalogo delle app AEM Mobile: *&lt;server-url>/aem/apps.html/content/mobileapps*
1. Seleziona **Crea** —> **App** come mostrato di seguito

Dopo aver creato un&#39;app utilizzando questo modello, potete aggiungere articoli, banner e raccolte all&#39;app. Per visitare nuovamente, creare articoli, banner e raccolte, consultate Azioni [di gestione dei](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)contenuti.

>[!NOTE]
>
>In alternativa, puoi anche selezionare un modello di app di esempio, ad esempio **We.Unlimited** app, che ti sarà reso disponibile da uno sviluppatore AEM. Se utilizzate questo modello di esempio per la vostra app, potete ottenere alcuni articoli di esempio e raccolte su cui lavorare. Potete utilizzare i modelli e i componenti di esempio, personalizzare quelli esistenti o crearne di nuovi per l&#39;app.

>[!CAUTION]
>
>Impostazione della proprietà ***redirectTarget***
>
>Quando si utilizza uno dei modelli di app, lo sviluppatore definisce il contenuto dell&#39;applicazione. Tuttavia, lo sviluppatore deve sapere dove viene creata l&#39;applicazione nel jcr e il valore della proprietà ***redirectTarget*** .
>
>Il ***redirectTarget*** viene calcolato come parte dell&#39;operazione di creazione dell&#39;app e tenta di risolvere un percorso, se esiste una proprietà redirectTarget disponibile come parte del modello di app e il valore di redirectTarget è definito come relativo. Quando il processo di creazione dell&#39;app trova un valore relativo per redirectTarget nel modello di app, il valore viene aggiunto alla posizione risolta in cui è stata creata l&#39;app.
>
>Ad esempio, se un modello di app definisce un ***redirectTarget*** con un valore &quot;*language-masters/en*&quot; e l&#39;app è stata creata in &quot;*/content/mobileapps/fooApp*&quot;, il valore finale per redirectTarget dopo la creazione dell&#39;app sarà &quot;*/content/mobileapps/fooApp/language-masters/en*&quot;.


## Creazione di modelli di contenuto {#creating-content-templates}

Ogni tipo di entità ha due modelli predefiniti. Si tratta di:

* **** Modelli predefiniti: utilizzato per la creazione di contenuto con proprietà/struttura predefinite applicabili
* **** Modelli importati: utilizzato per importare contenuto da AEM Mobile con proprietà/struttura predefinite applicabili

### Modelli articolo {#article-templates}

L&#39;articolo Unlimited è un modello di esempio che rappresenta un tipico layout di articolo AEM Mobile On-Demand.

1. Fate clic su **+** in **Gestisci articoli** per creare un nuovo articolo. Potete scegliere un articolo **** illimitato o **RTF**. L&#39;immagine seguente mostra l&#39;opzione che consente di scegliere tra questi due modelli di articolo.

1. Fate clic su **Avanti** per definire i metadati dell&#39;articolo come Nome/Titolo articolo, Descrizione, Autore, Abstract, Dipartimento, Immagine miniatura, Accesso articolo e così via.
1. Fate clic su **Avanti** per compilare il campo Proprietà annuncio.
1. Fate clic su **Avanti** per inserire l&#39;immagine dell&#39;articolo o l&#39;immagine del social media
1. Fate clic su **Avanti** per scegliere un collegamento alla raccolta a cui collegare il nuovo articolo.
1. Fate clic su **Avanti** per immettere i dettagli per la condivisione per social network.
1. Fate clic su **Crea** per completare il processo di creazione di un articolo utilizzando l&#39;esempio. Fate clic su **Fine** o **Modifica articolo** per modificare le proprietà di questo articolo.

![chlimage_1-71](assets/chlimage_1-71.png)

### Aggiunta di componenti a un articolo {#adding-components-to-article}

Una volta creato, un autore può modificare il contenuto di un articolo aggiungendo componenti come testo e immagini. Gli articoli sono un&#39;estensione dei modelli di pagina AEM.

Selezionate un articolo, che desiderate modificare e fate clic su **Modifica** per aggiungere componenti all’articolo.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

Scegliete &#39;**+**&#39; nel pannello a sinistra per aggiungere componenti all&#39;articolo.

![chlimage_1-74](assets/chlimage_1-74.png)

### Creazione di modelli predefiniti {#creating-out-of-the-box-templates}

Non sono disponibili modelli di articolo predefiniti, ma esiste un modello predefinito che i modelli personalizzati devono estendere. Consultate Esempio [di modello per](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article)articolo dell’app Geometrixx Unlimited.

Le proprietà chiave oltre le normali proprietà richieste per i modelli AEM includono:

***dps-resourceType=&quot;dps:Article&quot;***

Questa proprietà assicura che la pagina AEM venga riconosciuta come pagina di articolo di destinazione di AEM Mobile.

In base ai modelli AEM, potete aggiungere proprietà o nodi figlio predefiniti al ***jcr:content*** del modello.

### Modelli per banner e raccolte {#banner-and-collection-templates}

>[!CAUTION]
>
>I banner e le raccolte non dispongono di contenuto, pertanto la loro creazione non supporta i modelli personalizzati.

## Creazione e aggiunta di componenti {#creating-and-adding-components}

I componenti utilizzano e consentono l&#39;accesso ai Widget e questi vengono utilizzati per il rendering del contenuto.

Un semplice componente è incluso nell’archivio dei codici, la cui origine si trova in AEM. Successivamente, può essere aperto localmente anche in CRXDE Lite.

>[!NOTE]
>
>Al momento non sono disponibili componenti forniti per AEM Mobile.


Puoi aggiungere componenti alla pagina. Qualsiasi componente può essere utilizzato in un&#39;app AEM Mobile, ma se applicato, potrebbe non essere eseguito correttamente il rendering.

Tuttavia, i componenti personalizzati potrebbero non essere esportati e caricati correttamente in AEM Mobile On-Demand Services senza un gestore di sincronizzazione dei contenuti per l&#39;esportazione personalizzato che esegue il rendering in AEM.

Una volta che il componente è già stato incluso in una pagina AEM, insieme ad altri componenti per blocchi costitutivi, potete aggiungere un altro componente alla pagina o modificarne uno esistente.

**Per aggiungere un altro componente alla pagina:**

1. Scegliete la pagina desiderata e accertatevi di essere in modalità Modifica, mediante il menu a discesa in alto a destra dell’intestazione dell’editor
1. Attiva/disattiva il pannello laterale utilizzando l’icona più a sinistra nell’intestazione dell’editor
1. Select the **Components** tab
1. Trascinare uno dei componenti disponibili sulla pagina

![chlimage_1-75](assets/chlimage_1-75.png)

**Per modificare un componente esistente:**

1. Scegli la pagina desiderata e accertati di essere in modalità **Modifica** e seleziona il componente
1. Toccate l’icona della chiave inglese per configurare il componente

>[!NOTE]
>
>Potete creare un componente in AEM e personalizzarlo utilizzando [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Dopo aver personalizzato il componente esistente come requisiti, potete aggiungerlo nella pagina utilizzando l’opzione **Modifica** in **Gestisci articoli** come illustrato nella figura precedente.

>[!NOTE]
>
>Fate riferimento alle [best practice per lo sviluppo](/help/mobile/best-practices-aem-mobile.md) di modelli e componenti in AEM Mobile.

### Passaggi successivi {#the-next-steps}

* [Utilizzo delle proprietà di contenuto per esportare contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Mobile con sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md)