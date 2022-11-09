---
title: Creazione guidata nuova app AEM Mobile
seo-title: Creating a new AEM Mobile app using create wizard
description: Le app AEM Mobile si basano su un modello che definisce una struttura e proprietà della pagina. Segui questa pagina per scoprire come creare una nuova app basata su un modello di app.
seo-description: AEM Mobile apps are based on a blueprint that defines a page structure and properties. Follow this page to learn about how to create a new app based on an app template.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---

# Creazione guidata nuova app AEM Mobile{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le app AEM Mobile si basano su un modello che definisce una struttura e proprietà della pagina. Puoi configurare le seguenti proprietà dell&#39;applicazione:

* **Titolo:** Titolo dell&#39;applicazione.
* **Percorso di destinazione:** La posizione nel repository in cui è memorizzata l&#39;applicazione. Lascia l’impostazione predefinita per creare un percorso basato sul nome dell’app.

* **Nome:** Il valore predefinito è il valore della proprietà Titolo a cui sono stati rimossi gli spazi. Il nome viene utilizzato in AEM per fare riferimento all&#39;applicazione, ad esempio per il nodo del repository che rappresenta l&#39;applicazione.
* **Descrizione:** Descrizione della domanda.
* **URL server:** L’URL che fornisce contenuti OTA (Over-the-Air) viene aggiornato all’applicazione. Il valore predefinito è l&#39;URL del server di pubblicazione dell&#39;istanza utilizzata per creare un&#39;applicazione (prelevata dal servizio esternalizer). Nota: questa deve essere un&#39;istanza del server di pubblicazione anziché un autore, che richiede l&#39;autenticazione.

Puoi anche fornire un file immagine da utilizzare come miniatura dell’applicazione, selezionare la configurazione della PhoneGap Build da utilizzare e selezionare la configurazione di analisi dell’app mobile da utilizzare. Questa immagine viene utilizzata solo come miniatura per rappresentare la tua app mobile all’interno della console app mobili di Experience Manager.

Sono presenti schede aggiuntive (e facoltative) per creare il servizio cloud e integrare il plug-in Adobe Mobile Services SDK nella tua app.

* Build: Fai clic su gestisci configurazioni e configura il servizio build build build build build.phonegap.com qui. Dal menu a discesa potrai quindi selezionare il servizio cloud di build PhoneGap appena creato.
* Analytics: Fai clic su gestisci configurazioni e configura il tuo [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) servizio cloud. Quindi, dal menu a discesa potrai selezionare il nuovo Mobile Service da integrare nell’app mobile.

## Utilizzo dei modelli di app {#using-app-templates}

I modelli di app consentono di sfruttare facilmente i progetti esistenti creati dagli sviluppatori, utilizzati per la creazione di nuove app all’interno di AEM.

Che cos&#39;è un modello di app? Consideralo come una raccolta di modelli di pagina e componenti che rappresentano una linea di base o una base di un’app.
Quando crei una nuova app basata sul modello di un’altra app, riceverai un’app con un punto di partenza rappresentativo dell’app da cui è stata creata.

Per utilizzare questa funzione, devi disporre di un modello di app mobile esistente (o di un’app installata con un modello di app).

L&#39;ultimo pacchetto di esempi di app AEM include una versione aggiornata dell&#39;app Geometrixx con un modello di app. In alternativa, è possibile installare il [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) che fornisce anche un modello.

Passaggi per creare una nuova app basata su un modello di app:

1. Passa al catalogo delle app AEM Mobile: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Seleziona **Crea** e poi scegliere **App** come mostrato di seguito

![chlimage_1-158](assets/chlimage_1-158.png)

Seleziona un modello di app che ti è stato reso disponibile da uno sviluppatore AEM. Vedi [Struttura di un’app AEM Mobile](/help/mobile/phonegap-structure-an-app.md) per assistenza agli sviluppatori.

![chlimage_1-159](assets/chlimage_1-159.png)

Compila i dettagli della nuova app come necessario, compresa la modifica opzionale della relativa immagine miniatura. Questi valori possono essere modificati successivamente dalla **Gestione app** piastrelle.

![chlimage_1-160](assets/chlimage_1-160.png)

## Passaggi successivi {#the-next-steps}

Per ulteriori informazioni sugli altri ruoli di authoring, consulta le risorse seguenti:

* [La sezione Gestione app](/help/mobile/phonegap-app-details-tile.md)
* [Modifica dei metadati delle app](/help/mobile/phonegap-editmetadata.md)
* [Definizioni delle app](/help/mobile/phonegap-app-definitions.md)
* [Importare un’app ibrida esistente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e le responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Sviluppo per Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
