---
title: Creazione di un’app AEM Mobile tramite la procedura guidata
description: Le app AEM Mobile si basano su una blueprint che definisce la struttura e le proprietà di una pagina. Segui questa pagina per scoprire come creare un’app basata su un modello di app.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Creazione di un’app AEM Mobile tramite la procedura guidata{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Le app AEM Mobile si basano su una blueprint che definisce la struttura e le proprietà di una pagina. Puoi configurare le seguenti proprietà dell’applicazione:

* **Titolo:** Titolo dell’applicazione.
* **Percorso di destinazione:** Posizione nell&#39;archivio in cui è memorizzata l&#39;applicazione. Lascia l’impostazione predefinita per creare un percorso basato sul nome dell’app.

* **Nome:** Il valore predefinito è il valore della proprietà Title con spazi rimossi. Il nome viene utilizzato all’interno di AEM per fare riferimento all’applicazione, ad esempio, per il nodo dell’archivio che rappresenta l’applicazione.
* **Descrizione:** Descrizione dell&#39;applicazione.
* **URL server:** L’URL che fornisce aggiornamenti di contenuto OTA (Over-the-Air) all’applicazione. Il valore predefinito è l’URL del server di pubblicazione dell’istanza utilizzata per creare un’applicazione (derivata dal servizio esternalizzatore). Nota: questa deve essere un’istanza del server di pubblicazione anziché un’istanza Autore, che richiede l’autenticazione.

Puoi anche fornire un file di immagine da utilizzare come miniatura dell’applicazione, selezionare la configurazione di PhoneGap Build da utilizzare e selezionare la configurazione di analisi dell’app mobile da utilizzare. Ad Experience Manager, questa immagine viene utilizzata solo come miniatura per rappresentare l’app mobile nella console delle app mobili.

Sono disponibili schede aggiuntive (e facoltative) per build Cloud Service e per l’integrazione del plug-in SDK di Adobe Mobile Services nell’app.

* Genera: fai clic su Gestisci configurazioni e configura il servizio di build build.phonegap.com qui. Quindi, dall’elenco a discesa, potrai selezionare il servizio cloud PhoneGap Build appena creato.
* Analytics: fai clic su Gestisci configurazioni e configura il tuo [SDK di Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) servizio cloud. Quindi, dal menu a discesa, puoi selezionare il servizio mobile appena creato da integrare nell’app mobile.

## Utilizzo dei modelli di app {#using-app-templates}

I modelli di app offrono un modo semplice di utilizzare le progettazioni esistenti create dagli sviluppatori e utilizzate per la creazione di nuove app nell’ambito dell’AEM.

Che cos’è un modello di app? Consideralo come una raccolta di modelli di pagina e componenti che rappresentano una linea di base o le basi di un’app.
Quando crei un’app basata sul modello di un’altra app, otterrai un’app con un punto di partenza rappresentativo dell’app da cui è stata creata.

Per utilizzare questa funzione, è necessario disporre di un modello di app mobile esistente (o di un’app con un modello di app installato).

Il pacchetto di esempi più recente delle app AEM include una versione aggiornata dell’app Geometrixx con un modello di app. In alternativa, è possibile installare [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) che fornisce anche un modello.

Passaggi per creare un’app basata su un modello di app:

1. Passa al catalogo delle app AEM Mobile: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Seleziona **Crea** e quindi scegliere **App** come mostrato di seguito

![chlimage_1-158](assets/chlimage_1-158.png)

Seleziona un modello di app reso disponibile da uno sviluppatore AEM. Consulta [Struttura di un’app AEM Mobile](/help/mobile/phonegap-structure-an-app.md) per assistenza agli sviluppatori.

![chlimage_1-159](assets/chlimage_1-159.png)

Compila i dettagli della nuova app secondo necessità, inclusa la modifica facoltativa dell’immagine di anteprima. Questi valori possono essere modificati in un secondo momento da **Gestisci app** affiancare.

![chlimage_1-160](assets/chlimage_1-160.png)

## Passaggi successivi {#the-next-steps}

Per ulteriori informazioni su altri ruoli di authoring, consulta le risorse seguenti:

* [Sezione Gestione app](/help/mobile/phonegap-app-details-tile.md)
* [Modifica dei metadati dell’app](/help/mobile/phonegap-editmetadata.md)
* [Definizioni delle app](/help/mobile/phonegap-app-definitions.md)
* [Importa un&#39;app ibrida esistente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un amministratore e di uno sviluppatore, consulta le risorse seguenti:

* [Sviluppo per Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
