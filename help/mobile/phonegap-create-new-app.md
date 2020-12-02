---
title: Creazione di una nuova app  AEM Mobile tramite la creazione guidata
seo-title: Creazione di una nuova app  AEM Mobile tramite la creazione guidata
description: ' app AEM Mobile si basano su un progetto che definisce una struttura e proprietà di pagina. Segui questa pagina per scoprire come creare una nuova app basata su un modello di app.'
seo-description: ' app AEM Mobile si basano su un progetto che definisce una struttura e proprietà di pagina. Segui questa pagina per scoprire come creare una nuova app basata su un modello di app.'
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Creazione di una nuova app AEM Mobile  tramite la creazione guidata{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

 app AEM Mobile si basano su un progetto che definisce una struttura e proprietà di pagina. Potete configurare le seguenti proprietà dell’applicazione:

* **Titolo:** Titolo dell’applicazione.
* **Percorso di destinazione:** percorso nella directory archivio in cui è memorizzata l&#39;applicazione. Lasciate l&#39;impostazione predefinita per creare un percorso basato sul nome dell&#39;app.

* **Nome:** il valore predefinito è il valore della proprietà Titolo a cui sono stati rimossi gli spazi. Il nome viene utilizzato in AEM per fare riferimento all&#39;applicazione, ad esempio per il nodo del repository che rappresenta l&#39;applicazione.
* **Descrizione:** Una descrizione dell’applicazione.
* **URL server:** l&#39;URL che fornisce aggiornamenti di contenuto Over-the-Air (OTA) all&#39;applicazione. Il valore predefinito è l’URL del server di pubblicazione dell’istanza utilizzata per creare un’applicazione (proveniente dal servizio esternalizzatore). Nota: questa deve essere un&#39;istanza del server di pubblicazione anziché un autore, che richiede l&#39;autenticazione.

Puoi anche fornire un file immagine da usare come miniatura dell’applicazione, selezionare la configurazione delle PhoneGap Build da utilizzare e selezionare la configurazione di analisi per app mobili da utilizzare. Questa immagine viene utilizzata solo come miniatura per rappresentare l’applicazione mobile all’interno della console delle app mobili  Experience Manager.

Sono presenti schede aggiuntive (e facoltative) per creare il servizio cloud e integrare il plug-in SDK di Mobile Services  Adobe nell&#39;app.

* Build: Fai clic su Gestione configurazioni e configura il servizio build build build build build build build build.phonegap.com qui. Dal menu a discesa potrete selezionare il nuovo servizio cloud PhoneGap build.
* Analytics: Fai clic su Gestione configurazioni e configura il servizio cloud [ Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/using/home.html). Dal menu a discesa potrete selezionare il nuovo Mobile Service da integrare nell&#39;app mobile.

## Utilizzo dei modelli di app {#using-app-templates}

I modelli di app forniscono un modo semplice per sfruttare i progetti esistenti creati dagli sviluppatori, utilizzati per la creazione di nuove app all&#39;interno di AEM.

Che cos&#39;è un modello di app? Può essere considerato come una raccolta di modelli di pagina e componenti che rappresentano una linea di base o una base di un&#39;app.
Quando crei una nuova app basata sul modello di un&#39;altra app, riceverai un&#39;app con un punto di partenza rappresentativo dell&#39;app da cui è stata creata.

Per utilizzare questa funzione, è necessario disporre di un modello di app mobile esistente (o di un&#39;app installata con un modello di app).

L&#39;ultimo pacchetto di esempi di app AEM include una versione aggiornata dell&#39;app Geometrixx con un modello di app. In alternativa, è possibile installare il [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) che fornisce anche un modello.

Passaggi per creare una nuova app basata su un modello di app:

1. Andate al  catalogo delle app AEM Mobile: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Selezionare **Crea**, quindi scegliere **App** come illustrato di seguito

![chlimage_1-158](assets/chlimage_1-158.png)

Selezionate un modello di app reso disponibile da uno sviluppatore AEM. Consultate [Struttura di un&#39;app AEM Mobile ](/help/mobile/phonegap-structure-an-app.md) per assistenza agli sviluppatori.

![chlimage_1-159](assets/chlimage_1-159.png)

Compila i dettagli della nuova app in base alle esigenze, compresa la modifica opzionale della relativa miniatura. Questi valori possono essere modificati successivamente dalla sezione **Gestisci app**.

![chlimage_1-160](assets/chlimage_1-160.png)

## Passaggi successivi {#the-next-steps}

Per ulteriori informazioni su altri ruoli di authoring, consulta le seguenti risorse:

* [Gestisci sezione app](/help/mobile/phonegap-app-details-tile.md)
* [Modifica dei metadati dell&#39;app](/help/mobile/phonegap-editmetadata.md)
* [Definizioni delle app](/help/mobile/phonegap-app-definitions.md)
* [Importare un&#39;app ibrida esistente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Risorse aggiuntive {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Sviluppo per  Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per  Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
