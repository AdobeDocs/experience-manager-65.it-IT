---
title: Gestisci porzione app
seo-title: Manage App Tile
description: Leggi questa pagina per scoprire di più su Gestione riquadro app nel dashboard dell’app che consente di modificare i dettagli dell’applicazione.
seo-description: Follow this page to learn about the Manage App Tile on the app dashboard that provides the ability to modify details about the Application.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 2%

---

# Gestisci porzione app{#manage-app-tile}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La **Gestione app** Il riquadro nella dashboard dell&#39;app consente di modificare i dettagli dell&#39;applicazione. Per aprire la pagina Dettagli, fai clic sul collegamento dei dettagli della sezione Gestione app . Dalla pagina Gestione app è possibile modificare le impostazioni di Configurazione applicazione PhoneGap (config.xml) e preparare l&#39;applicazione per l&#39;invio ai vari archivi delle applicazioni.

![chlimage_1-116](assets/chlimage_1-116.png)

## Informazioni sulla sezione Gestione app {#understanding-the-manage-app-tile}

Puoi analizzare ogni tessera nel **Gestione app** per visualizzare o modificare i dettagli facendo clic su &quot;..&quot; nell&#39;angolo in basso a destra.

### Scheda Base {#the-basic-tab}

È possibile modificare le **Nome**, **Autore**, **Descrizione breve** e **Descrizione** per la tua app da questa scheda.

![chlimage_1-117](assets/chlimage_1-117.png)

### Scheda Avanzate {#the-advanced-tab}

Ogni piattaforma di app mobile descrive i dati raccolti, con targeting specifico per ogni archivio di applicazioni.

Le piattaforme visualizzate sono guidate dal contenuto PhoneGap config.xml:

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Per visualizzare i dettagli dell&#39;applicazione ai clienti, ogni archivio applicazioni fornitore, ad esempio Apple App Store o Google Play Store, richiede una o più schermate dell&#39;applicazione mobile. Queste schermate possono avere requisiti rigidi su dimensioni e contenuto (in pratica devono rappresentare l’applicazione). AEM Apps fornisce il supporto per la selezione e la gestione di queste schermate per le piattaforme supportate e per visualizzare le dimensioni di porta come richiesto da ogni negozio di applicazioni di ciascun fornitore.

>[!NOTE]
>
>L’app AEM Verifica consente di inviare le schermate direttamente ai dettagli dell’app in AEM.
>
>Vedi [Quickstart per dispositivi mobili per AEM verificare](/help/mobile/phonegap-mobile-quickstart.md) per ulteriori dettagli.

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadati {#metadata}

>[!NOTE]
>
>Una volta che hai familiarità con il **Gestione app** riquadro, vedi [Modifica dei metadati delle app](/help/mobile/phonegap-editmetadata.md) per visualizzare e modificare i metadati.

#### Metadati comuni {#common-metadata}

A ogni applicazione devono essere associati metadati che consentono di configurare diversi aspetti dell&#39;applicazione. La pagina Gestione app è separata in due diverse aree relative alla raccolta di metadati. Metadati specifici della piattaforma e metadati comuni.

Sono presenti configurazioni e metadati comuni per tutte le piattaforme.

In questa sezione si definisce l&#39;URL del server di aggiornamento del contenuto, la pagina di destinazione per la propria app mobile, la versione di PhoneGap per la compilazione, la versione dell&#39;applicazione, il nome, la descrizione e altro ancora.

**Versione app** è la versione funzionante dell&#39;applicazione. La best practice comune consiste nell’utilizzare una notazione con 3 decimali e iniziare al di sotto della 1.0.0 prima della prima versione.

**Versione PhoneGap** è la versione in cui si desidera compilare l&#39;applicazione con PhoneGap. Si consiglia di tenere il passo con la versione corrente al fine di ottenere le funzioni e le correzioni di bug più recenti e più importanti.

**URL server di aggiornamento del contenuto** è l&#39;URL che l&#39;applicazione utilizzerà per chiamare per gli aggiornamenti di ContentSync. Deve essere impostato sull’URL del dispatcher o, se non utilizzi un dispatcher, su una delle istanze di pubblicazione che verrà utilizzata per distribuire gli aggiornamenti di ContentSync all’applicazione.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Questa sezione può apparire vuota a meno che non siano presenti dati che compilano i campi.
>
>Nella parte superiore della visualizzazione dei dettagli sono disponibili Versione applicazione, Versione PhoneGap e URL di aggiornamento. Ognuno di questi valori può essere impostato nella sezione Metadati comuni . Tuttavia, l&#39;ID applicazione non può essere modificato.

#### Metadati piattaforma {#platform-metadata}

Ogni piattaforma definita nel file config.xml di PhoneGap può contenere proprietà di piattaforma personalizzate. Uno sviluppatore AEM deve contribuire alla struttura del contenuto per acquisire queste proprietà. Un esempio fornito di proprietà specifiche della piattaforma può essere trovato per iOS.

I metadati per tutte le piattaforme configurate vengono ora visualizzati contemporaneamente nella scheda Avanzate del riquadro Gestione app.

>[!NOTE]
>
>Le sezioni dei metadati della piattaforma non vengono utilizzate da PhoneGap durante una build CLI o Remote PhoneGap, ma AEM tenta di acquisire i metadati per le piattaforme in modo che possano essere utilizzati successivamente durante l&#39;invio all&#39;archivio applicazioni del fornitore di destinazione.

Per le piattaforme che non sono comprese da AEM, è ancora possibile per uno sviluppatore AEM estendere l’interfaccia utente per acquisire questi metadati che in seguito possono essere esportati e utilizzati durante il processo di invio dell’applicazione.

#### Metadati iOS {#ios-metadata}

Apple AppStore richiede metadati aggiuntivi per inviare la tua applicazione per la distribuzione. La sezione metadati iOS tenta di raccogliere le informazioni richieste che possono essere utilizzate dallo strumento di Apple iTMSTransporter per pubblicare i metadati sull&#39;account dello sviluppatore Apple associato.

Per ottenere i metadati specifici di Apple, devi prima creare l’applicazione su [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Al momento della creazione dell’applicazione, Apple genera i metadati richiesti dalla sezione metadati iOS se desideri utilizzare lo strumento Apple iTMSTransporter per convalidare e caricare i metadati su itunesconnect.apple.com. Se desideri semplicemente ottenere i metadati per la raccolta, non devi necessariamente compilare i metadati specifici di iOS. Puoi comunque esportare i metadati che uniranno iOS e i metadati comuni e raccogliere tutte le schermate in un file zip che può essere scaricato in qualsiasi momento.

Il file zip scaricato contiene un file itmsp che può essere esaminato per il file metadata.xml. Il file itmsp contiene i metadati esportati (all&#39;interno del file metadata.xml), insieme a tutte le schermate associate.

La funzionalità di esportazione viene utilizzata per fornire un modo pratico per raccogliere le schermate e i metadati che possono essere trasmessi all&#39;editore dell&#39;applicazione per l&#39;input nell&#39;archivio applicazioni specifico del fornitore.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Metadati Android {#android-metadata}

Durante la selezione della piattaforma Android, a questo punto non è possibile impostare metadati personalizzati. Quando si fa clic sul pulsante di download come file zip, verrà generato con un file di proprietà che contiene tutti i metadati e le schermate associate.

La funzionalità di esportazione viene utilizzata per fornire un modo pratico per raccogliere le schermate e i metadati che possono essere trasmessi all&#39;editore dell&#39;applicazione per l&#39;input nell&#39;archivio applicazioni specifico del fornitore.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL server per aggiornamento contenuti {#content-update-server-url}

Una delle caratteristiche principali delle app AEM è la capacità di avere un&#39;applicazione mobile che richiede nuovo contenuto tramite ContentSync, dove il contenuto può essere risorse html, pagine, video, immagini, testo e altro ancora. Una volta che un autore di contenuti ha aggiornato il contenuto e lo pubblica, il server rende disponibile l’aggiornamento del contenuto per il download dell’app mobile.

La proprietà URL Content Update Server è l&#39;URL che deve puntare a un&#39;istanza di pubblicazione; direttamente o tramite il dispatcher o CDN. Il formato dell’URL è semplicemente:

`https://[hostname]:[port]`

>[!NOTE]
>
>Se l’istanza del server di authoring si replica su più istanze del server di pubblicazione (architettura comune per AEM), ogni server di pubblicazione avrà lo stesso contenuto di aggiornamento perché l’aggiornamento è generato sull’autore e replicato in tutte le istanze di pubblicazione. In sostanza, il bilanciamento del carico e il failover sono completamente supportati.

### Scheda Plug-in {#the-plugins-tab}

La **Plug-in** descrive i plug-in associati all’app. Queste informazioni verranno utilizzate per recuperare il plug-in appropriato durante una build.

![chlimage_1-122](assets/chlimage_1-122.png)

### Scheda Schermate {#the-screenshots-tab}

La **Schermate** visualizza le risoluzioni dello screenshot supportate su piattaforme diverse.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Per aggiungere e rimuovere le schermate, vedi [Modifica dei metadati delle app](/help/mobile/phonegap-editmetadata.md).

### Scheda Autenticazione {#the-authentication-tab}

La **Autenticazione** La scheda ti consente di selezionare un client OAuth da associare all’applicazione e di utilizzare l’autenticazione OAuth di Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Passaggi successivi {#the-next-steps}

Dopo aver appreso come gestire il riquadro app nel dashboard dell&#39;applicazione, consulta le seguenti risorse per altri ruoli di authoring:

* [Modifica dei metadati delle app](/help/mobile/phonegap-editmetadata.md)
* [Definizioni delle app](/help/mobile/phonegap-app-definitions.md)
* [Creazione di una nuova app tramite Creazione guidata app](/help/mobile/phonegap-create-new-app.md)
* [Importare un’app ibrida esistente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e le responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Sviluppo per Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
