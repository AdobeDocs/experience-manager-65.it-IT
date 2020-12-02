---
title: Creazione e aggiunta di modelli e componenti
seo-title: Creazione e aggiunta di modelli e componenti
description: Segui questa pagina per informazioni sulla creazione e l'aggiunta di modelli e componenti all'app. La pagina utilizza l'app Geometrixx Unlimited come app che contiene un modello di app di esempio e modelli di pagina.
seo-description: Segui questa pagina per informazioni sulla creazione e l'aggiunta di modelli e componenti all'app. La pagina utilizza l'app Geometrixx Unlimited come app che contiene un modello di app di esempio e modelli di pagina.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 0%

---


# Creazione e aggiunta di modelli e componenti {#creating-and-adding-templates-and-components}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

 AEM Mobile On-Demand fornisce un modello di app completamente configurato, un modello di articolo e componenti articolo.

L&#39;app We.Unlimited è un modello di esempio che rappresenta la shell di un&#39;applicazione AEM Mobile On-Demand completamente configurabile e gestibile .

Selezionando questo modello di esempio durante la creazione di una nuova app, viene distribuito un dashboard ricco di funzioni per  AEM Mobile.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>Per gestire l&#39;applicazione e il contenuto dell&#39;app mobile  AEM Mobile Apps Control Center, vedete il [ AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## Creazione di modelli di app {#creating-app-templates}

Un modello app viene utilizzato per creare una nuova app e funge da raccolta di modelli di pagina e componenti che rappresentano una linea di base o una base di un&#39;app. Il modello elimina alcune proprietà fondamentali per guidare l&#39;app nel modo appropriato. In generale, un cliente non creerebbe troppe app in totale.

I modelli di app forniscono un modo semplice per sfruttare i progetti esistenti creati dagli sviluppatori, utilizzati per la creazione di nuove app all&#39;interno di AEM.

Quando crei una nuova app basata sul modello di un&#39;altra app, riceverai un&#39;app con un punto di partenza rappresentativo dell&#39;app da cui è stata creata.

Passaggi per creare una nuova app basata su un modello di app:

1. Andate al  catalogo delle app AEM Mobile: *&lt;server-url>/aem/apps.html/content/mobileapps*
1. Selezionare **Create** —> **App** come illustrato di seguito

Dopo aver creato un&#39;app utilizzando questo modello, potete aggiungere articoli, banner e raccolte all&#39;app. Per visitare di nuovo gli articoli, i banner e le raccolte, consultate [Azioni di gestione dei contenuti](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>In alternativa, puoi anche selezionare un modello di app di esempio, ad esempio l&#39;app **We.Unlimited**, resa disponibile da uno sviluppatore AEM. Se utilizzate questo modello di esempio per la vostra app, potete ottenere alcuni articoli di esempio e raccolte su cui lavorare. Potete utilizzare i modelli e i componenti di esempio, personalizzare quelli esistenti o crearne di nuovi per l&#39;app.

>[!CAUTION]
>
>Impostazione della proprietà ***redirectTarget***
>
>Quando si utilizza uno dei modelli di app, lo sviluppatore definisce il contenuto dell&#39;applicazione. Tuttavia, lo sviluppatore deve sapere dove viene creata l&#39;applicazione in jcr e il valore della proprietà ***redirectTarget***.
>
>***redirectTarget*** viene calcolato come parte dell&#39;operazione di creazione dell&#39;app e tenta di risolvere un percorso, se esiste una proprietà redirectTarget disponibile come parte del modello di app e il valore di redirectTarget è definito come relativo. Quando il processo di creazione dell&#39;app trova un valore relativo per redirectTarget nel modello di app, il valore viene aggiunto alla posizione risolta in cui è stata creata l&#39;app.
>
>Ad esempio, se un modello di app definisce un ***redirectTarget*** con un valore di &quot;*language-masters/en*&quot; e l&#39;app è stata creata in &quot;*/content/mobileapps/fooApp*&quot;, il valore finale per redirectTarget dopo la creazione dell&#39;app sarà &quot;&lt;a6//content/mobileapps/fooApp/language-masters/en *&quot;.*


## Creazione di modelli di contenuto {#creating-content-templates}

Ogni tipo di entità ha due modelli predefiniti. Secondo questi principi, il contenuto deve essere:

* **Modelli predefiniti:** utilizzati per la creazione di contenuto con proprietà/struttura predefinite applicabili
* **Modelli importati:** utilizzati per importare contenuti da  AEM Mobile con proprietà/struttura predefinite applicabili

### Modelli articolo {#article-templates}

L&#39;articolo Unlimited è un modello di esempio che rappresenta un layout tipico  articolo AEM Mobile On-Demand.

1. Fate clic su **+** in **Gestisci articoli** per creare un nuovo articolo. È possibile scegliere un **Articolo illimitato** o un **articolo RTF**. L&#39;immagine seguente mostra l&#39;opzione che consente di scegliere tra questi due modelli di articolo.

1. Fate clic su **Next** per definire i metadati dell&#39;articolo come Nome/Titolo articolo, Descrizione, Autore, Abstract, Dipartimento, Miniatura immagine, Accesso articolo e così via.
1. Fare clic su **Next** per compilare il campo Proprietà annuncio.
1. Fate clic su **Next** per inserire l&#39;immagine dell&#39;articolo o social media
1. Fate clic su **Next** per scegliere un collegamento alla raccolta a cui collegare il nuovo articolo.
1. Fate clic su **Next** per inserire i dettagli per la condivisione per social network.
1. Fate clic su **Crea** per completare il processo di creazione di un articolo utilizzando l&#39;esempio. Fate clic su **Fine** o su **Modifica articolo** per modificare le proprietà di questo articolo.

![chlimage_1-71](assets/chlimage_1-71.png)

### Aggiunta di componenti all&#39;articolo {#adding-components-to-article}

Una volta creato, un autore può modificare il contenuto di un articolo aggiungendo componenti come testo e immagini. Gli articoli sono un&#39;estensione AEM modelli di pagina.

Selezionate un articolo, desiderate modificarlo e fate clic su **Modifica** per aggiungere componenti all&#39;articolo.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

Scegliete &#39;**+**&#39; nel pannello a sinistra per aggiungere componenti all&#39;articolo.

![chlimage_1-74](assets/chlimage_1-74.png)

### Creazione di modelli predefiniti {#creating-out-of-the-box-templates}

Non esistono modelli di articolo predefiniti, ma esiste un modello predefinito che i modelli personalizzati dovrebbero estendere. Consultate Esempio di modello di articolo dell&#39;app Geometrixx Unlimited [esempio](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article).

Le proprietà chiave oltre le normali proprietà richieste per il modello AEM includono:

***dps-resourceType=&quot;dps:Article&quot;***

Questa proprietà assicura che la pagina AEM venga riconosciuta come pagina di articolo  destinazione AEM Mobile.

In base AEM modelli, è possibile aggiungere proprietà predefinite o nodi secondari al ***jcr:content*** del modello.

### Modelli di banner e raccolta {#banner-and-collection-templates}

>[!CAUTION]
>
>I banner e le raccolte non dispongono di contenuto, pertanto la loro creazione non supporta i modelli personalizzati.

## Creazione e aggiunta di componenti {#creating-and-adding-components}

I componenti utilizzano e consentono l&#39;accesso ai Widget e questi vengono utilizzati per il rendering del contenuto.

Un semplice componente è incluso nell’archivio dei codici, la cui origine si trova in AEM. Successivamente, può essere aperto localmente in CRXDE Lite.

>[!NOTE]
>
>Al momento non sono disponibili componenti forniti per  AEM Mobile.


Puoi aggiungere componenti alla pagina. Qualsiasi componente può essere utilizzato in un&#39;app  AEM Mobile, ma se applicato potrebbe non essere eseguito correttamente il rendering.

Tuttavia, i componenti personalizzati potrebbero non essere esportati e caricati correttamente in  AEM Mobile On-demand Services senza un gestore di sincronizzazione del contenuto per l’esportazione personalizzato che esegue il rendering in AEM.

Una volta che il componente è già stato incluso in una pagina AEM, insieme ad altri componenti per blocchi predefiniti, è possibile aggiungere un altro componente alla pagina o modificarne uno esistente.

**Per aggiungere un altro componente alla pagina:**

1. Scegliete la pagina desiderata e accertatevi di essere in modalità Modifica, mediante il menu a discesa in alto a destra dell’intestazione dell’editor
1. Per attivare o disattivare il pannello laterale, usate l’icona più a sinistra nell’intestazione dell’editor
1. Selezionare la scheda **Componenti**
1. Trascinare uno dei componenti disponibili sulla pagina

![chlimage_1-75](assets/chlimage_1-75.png)

**Per modificare un componente esistente:**

1. Scegliere la pagina e assicurarsi di essere in modalità **Modifica** e selezionare il componente
1. Toccate l’icona della chiave inglese per configurare il componente

>[!NOTE]
>
>È possibile creare un componente in AEM e personalizzare lo stesso utilizzando [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Dopo aver personalizzato il componente esistente come requisiti, è possibile aggiungerlo nella pagina utilizzando l&#39;opzione **Modifica** in **Gestisci articoli** come illustrato nella figura precedente.

>[!NOTE]
>
>Fare riferimento a [Best practice per lo sviluppo di modelli e componenti](/help/mobile/best-practices-aem-mobile.md) in  AEM Mobile.

### Passaggi successivi {#the-next-steps}

* [Utilizzo delle proprietà di contenuto per esportare il contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Mobile con sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md)