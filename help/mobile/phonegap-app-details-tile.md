---
title: Gestisci sezione app
seo-title: Gestisci sezione app
description: Seguite questa pagina per saperne di più su Gestione sezione app nella dashboard app che consente di modificare i dettagli relativi all'applicazione.
seo-description: Seguite questa pagina per saperne di più su Gestione sezione app nella dashboard app che consente di modificare i dettagli relativi all'applicazione.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 2%

---


# Gestisci sezione app{#manage-app-tile}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La sezione **Manage App** del dashboard app consente di modificare i dettagli dell&#39;applicazione. Per aprire la pagina Dettagli, fai clic sul collegamento dei dettagli della sezione Gestione app. Dall&#39;interno della pagina Gestisci app è possibile modificare le impostazioni di configurazione dell&#39;applicazione PhoneGap (config.xml) e preparare l&#39;applicazione per l&#39;invio ai vari store dell&#39;applicazione.

![chlimage_1-116](assets/chlimage_1-116.png)

## Informazioni su Gestione sezione app {#understanding-the-manage-app-tile}

Per visualizzare o modificare i dettagli, puoi eseguire il drill-through in ciascuna sezione della sezione **Gestisci app** facendo clic su &#39;...&#39; nell&#39;angolo in basso a destra.

### Scheda Base {#the-basic-tab}

Da questa scheda è possibile modificare **Nome**, **Autore**, **Descrizione breve** e **Descrizione** per l&#39;app.

![chlimage_1-117](assets/chlimage_1-117.png)

### Scheda Avanzate {#the-advanced-tab}

Ogni piattaforma di applicazioni mobili descrive i dati raccolti, con targeting specifico per ogni store di applicazioni.

Le piattaforme visualizzate sono gestite dal contenuto di config.xml PhoneGap:

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Ogni store di applicazioni fornitore, ad esempio Apple App Store o Google Play Store, richiede uno o più screenshot dell&#39;applicazione mobile per visualizzare i dettagli dell&#39;applicazione ai clienti. Tali screenshot possono avere requisiti rigorosi sulle dimensioni e sui contenuti (in pratica devono rappresentare l&#39;applicazione). AEM Apps fornisce il supporto per la selezione e la gestione di queste schermate per le piattaforme supportate e per visualizzare le dimensioni delle porte come richiesto dallo store applicazione di ciascun fornitore.

>[!NOTE]
>
>L&#39;app AEM Verify consente di inviare le schermate direttamente ai dettagli dell&#39;app in AEM.
>
>Per ulteriori informazioni, vedere [Mobile Quickstart per AEM Verify](/help/mobile/phonegap-mobile-quickstart.md).

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadati {#metadata}

>[!NOTE]
>
>Una volta acquisita familiarità con la sezione **Gestione app**, consulta [Modifica dei metadati dell&#39;app](/help/mobile/phonegap-editmetadata.md) per visualizzare e modificare i metadati.

#### Metadati comuni {#common-metadata}

A ogni applicazione devono essere associati dei metadati che agevolino la configurazione di diversi aspetti dell&#39;applicazione. La pagina Gestisci app è separata in due diverse aree correlate alla raccolta di metadati. Metadati specifici della piattaforma e metadati comuni.

Sono disponibili configurazioni e metadati comuni per tutte le piattaforme.

In questa sezione viene definito l&#39;URL di Content Update Server, la pagina di destinazione per l&#39;applicazione mobile, la versione di PhoneGap per la compilazione, la versione dell&#39;applicazione, il nome, la descrizione e altro ancora.

**App** Version è la versione di lavoro dell&#39;applicazione. Come procedura ottimale, è consigliabile utilizzare una notazione con tre decimali e iniziare al di sotto di 1.0.0 prima della prima release.

**PhoneGap** Versionè la versione in cui si desidera compilare l&#39;applicazione con PhoneGap. La best practice consiste nel tenere il passo con la versione corrente per garantire che siano disponibili le funzioni e le correzioni di bug più recenti e complete.

**Content Update Server** URL è l&#39;URL che l&#39;applicazione utilizzerà per chiamare gli aggiornamenti ContentSync. Deve essere impostato sull’URL del dispatcher o, se non si utilizza un dispatcher, su una delle istanze di pubblicazione che verranno utilizzate per distribuire gli aggiornamenti ContentSync all’applicazione.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Questa sezione può apparire vuota a meno che non siano presenti dati che popolano i campi.
>
>Nella parte superiore della visualizzazione dei dettagli sono elencati la versione dell’applicazione, la versione di PhoneGap e l’URL di aggiornamento. Ciascuno di questi valori può essere impostato nella sezione Metadati comuni. Tuttavia, l&#39;ID applicazione non può essere modificato.

#### Metadati piattaforma {#platform-metadata}

Ogni piattaforma definita nel file config.xml PhoneGap può contenere proprietà della piattaforma personalizzate. Uno sviluppatore AEM deve contribuire alla struttura del contenuto per acquisire queste proprietà. Un esempio fornito di proprietà specifiche della piattaforma può essere trovato per iOS.

I metadati per tutte le piattaforme configurate ora vengono visualizzati contemporaneamente nella scheda Avanzate della sezione Gestione app.

>[!NOTE]
>
>Le sezioni di metadati della piattaforma non vengono utilizzate da PhoneGap durante una build CLI o Remote PhoneGap, ma AEM tenta di acquisire i metadati per le piattaforme in modo che possano essere utilizzati in seguito durante l&#39;invio allo store applicazione del fornitore di destinazione.

Per le piattaforme che non sono comprese da AEM, è ancora possibile per uno sviluppatore AEM estendere l&#39;interfaccia utente per acquisire i metadati che successivamente possono essere esportati e utilizzati durante il processo di invio dell&#39;applicazione.

#### Metadati iOS {#ios-metadata}

Per inviare l’applicazione per la distribuzione, Apple AppStore richiede ulteriori metadati. La sezione relativa ai metadati iOS tenta di raccogliere le informazioni necessarie che possono essere utilizzate dallo strumento Apple iTMSTransporter per pubblicare i metadati nell&#39;account dello sviluppatore Apple associato.

Per ottenere i metadati specifici di Apple è innanzitutto necessario creare l&#39;applicazione su [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Al momento della creazione dell&#39;applicazione, Apple genererà i metadati richiesti dalla sezione dei metadati iOS se desiderate utilizzare lo strumento Apple iTMSTransporter per convalidare e caricare i metadati su itunesconnect.apple.com. Se desiderate solo ottenere i metadati per la raccolta, non dovete necessariamente compilare i metadati specifici di iOS. Potete comunque esportare i metadati che uniranno iOS e i metadati comuni e raccogliere tutte le schermate in un file zip che può essere scaricato in qualsiasi momento.

Il file zip scaricato contiene un file itmsp che può essere analizzato per il file metadata.xml. Il file itmsp contiene i metadati esportati (all’interno del file metadata.xml), insieme a tutte le schermate associate.

La funzionalità di esportazione è utilizzata per fornire un metodo pratico per raccogliere le schermate e i metadati che possono essere trasmessi all&#39;editore dell&#39;applicazione per l&#39;input nello store dell&#39;applicazione specifico del fornitore.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Metadati Android {#android-metadata}

Quando si seleziona la piattaforma Android, a questo punto non è possibile impostare metadati personalizzati. Quando si fa clic sul pulsante di download come file ZIP, verrà generato un file di proprietà che contiene tutti i metadati e le schermate associate.

La funzionalità di esportazione è utilizzata per fornire un metodo pratico per raccogliere le schermate e i metadati che possono essere trasmessi all&#39;editore dell&#39;applicazione per l&#39;input nello store dell&#39;applicazione specifico del fornitore.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL server per aggiornamento contenuti {#content-update-server-url}

Una delle caratteristiche chiave di AEM Apps è la capacità di avere un nuovo contenuto per applicazioni mobili tramite ContentSync, dove il contenuto può essere risorse HTML, pagine, video, immagini, testo e altro ancora. Dopo che un autore di contenuto ha aggiornato il contenuto e lo ha pubblicato, il server rende disponibile l’aggiornamento del contenuto per il download dell’applicazione mobile.

La proprietà URL di Content Update Server è l’URL che deve puntare a un’istanza di pubblicazione; direttamente o tramite il dispatcher o CDN. Il formato dell’URL è semplicemente:

`https://[hostname]:[port]`

>[!NOTE]
>
>Se l’istanza del server di authoring si sta replicando su più istanze del server di pubblicazione (architettura comune per AEM), ogni server di pubblicazione avrà lo stesso contenuto di aggiornamento perché l’aggiornamento è basato sull’autore e replicato in tutte le istanze di pubblicazione. In sostanza, il bilanciamento del carico e il failover sono completamente supportati.

### Scheda Plugins {#the-plugins-tab}

La scheda **Plugins** descrive i plug-in associati all&#39;app. Queste informazioni verranno utilizzate per recuperare il plug-in appropriato durante una build.

![chlimage_1-122](assets/chlimage_1-122.png)

### Scheda Screenshots {#the-screenshots-tab}

La scheda **Screenshots** visualizza le risoluzioni delle schermate supportate su piattaforme diverse.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Per aggiungere e rimuovere le schermate, consultate [Modifica dei metadati dell&#39;app](/help/mobile/phonegap-editmetadata.md).

### Scheda Autenticazione {#the-authentication-tab}

La scheda **Autenticazione** consente di selezionare un client OAuth da associare all&#39;applicazione e consente a uno sviluppatore di utilizzare l&#39;autenticazione OAuth di Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Passaggi successivi {#the-next-steps}

Dopo aver appreso come gestire la sezione Applicazione nel dashboard, consulta le risorse seguenti per altri ruoli di authoring:

* [Modifica dei metadati dell&#39;app](/help/mobile/phonegap-editmetadata.md)
* [Definizioni delle app](/help/mobile/phonegap-app-definitions.md)
* [Creazione di una nuova app tramite Creazione guidata app](/help/mobile/phonegap-create-new-app.md)
* [Importare un&#39;app ibrida esistente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Risorse aggiuntive {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Sviluppo per  Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per  Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

