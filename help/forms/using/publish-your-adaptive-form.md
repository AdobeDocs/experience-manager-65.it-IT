---
title: "Tutorial: Publish il tuo modulo adattivo"
description: Publish il modulo adattivo come pagina AEM, incorporalo in una pagina AEM Sites o incorporalo in una pagina web esterna
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Tutorial: crea un Publish per il modulo adattivo {#tutorial-publish-your-adaptive-form}

![Immagine protagonista](do-not-localize/13-publish-your-adaptive-form-small.png)

Questo tutorial è un passaggio della serie [Creare il primo modulo adattivo](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

Una volta che il modulo adattivo è pronto, puoi pubblicarlo per renderlo disponibile agli utenti finali. Gli utenti finali possono aprire il modulo pubblicato su qualsiasi dispositivo e browser Internet. Quando viene pubblicato un modulo adattivo, il modulo e il contenuto correlato vengono copiati da un’istanza di authoring AEM a un’istanza di pubblicazione AEM. Il modulo viene reso disponibile all’utente finale tramite l’istanza Publish.

Per pubblicare un modulo adattivo, sono disponibili i seguenti metodi:

* [Publish il modulo adattivo come pagina AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporare il modulo adattivo in una pagina AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporare il modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata al di fuori dell’AEM)](../../forms/using/publish-your-adaptive-form.md)

## Prima di iniziare {#before-you-start}

* **[Configura un&#39;istanza di pubblicazione di AEM Forms](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: l&#39;istanza di pubblicazione è un&#39;istanza pubblica dell&#39;AEM [!DNL Forms] in esecuzione in modalità di pubblicazione. In un ambiente di produzione, l’istanza Publish si trova all’esterno del firewall dell’organizzazione.
* **[Imposta replica e replica inversa](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: la replica copia il contenuto dall&#39;istanza di authoring a un&#39;istanza di pubblicazione e restituisce l&#39;input utente (ad esempio, l&#39;input del modulo) dall&#39;istanza di pubblicazione all&#39;istanza di authoring.

## Publish il modulo adattivo come pagina AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando il modulo adattivo viene pubblicato come pagina AEM, l’intera pagina web contiene solo il modulo pubblicato. Puoi utilizzare l’URL del modulo adattivo per collegarlo da un’altra pagina web. Per pubblicare il modulo adattivo **shipping-address-add-update-form** come pagina AEM:

1. Accedi all’istanza di authoring [!DNL Forms] dell’AEM e individua il modulo adattivo shipping-address-add-update-form nell’interfaccia utente [!DNL Forms] dell’AEM.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleziona il modulo adattivo shipping-address-add-update-form e seleziona **[!UICONTROL Publish]**. Viene visualizzata una finestra di dialogo contenente le risorse correlate al modulo adattivo. Seleziona **[!UICONTROL Publish]**. Il modulo adattivo viene pubblicato e viene visualizzata una finestra di dialogo di successo.
1. Apri il modulo sull’istanza Publish. Il modulo può essere compilato e inviato dall’utente finale.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporare il modulo adattivo in una pagina AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] consente agli sviluppatori di moduli di incorporare facilmente i moduli adattivi in una pagina AEM [!DNL Sites]. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e interagire contemporaneamente con il modulo.

AEM [!DNL Forms] fornisce un componente, AEM [!DNL Forms] Container, per incorporare un modulo adattivo in una pagina AEM [!DNL Sites]. Per impostazione predefinita, il componente non è visibile nel contenitore AEM [!DNL Sites]. Per abilitare il componente Contenitore [!DNL Forms] dell&#39;AEM e incorporare il modulo adattivo in una pagina [!DNL Sites] dell&#39;AEM, eseguire la procedura seguente:

1. Crea e apri una pagina nel sito We.Retail per la modifica. Ad esempio, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Modulo adattivo incorporato nella pagina [!DNL Sites].

   È inoltre possibile incorporare il modulo adattivo in una pagina We.Retail [!DNL Site's] esistente. Ad esempio, la pagina INFO SU [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Consente di risparmiare tempo per creare una pagina. I passaggi seguenti utilizzano la pagina appena creata.

   Il sito We.Retail è fornito con AEM. Se non hai installato il sito We.Retail, consulta la sezione [Implementazione di riferimento We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) per installare il sito.

1. Seleziona ![proprietà](assets/properties.png) informazioni pagina e seleziona l&#39;opzione **[!UICONTROL Modifica modello]** nella pagina del sito We.Retail appena creata. Il modello della pagina si apre in una nuova scheda del browser.
1. Seleziona nella casella **[!UICONTROL contenitore layout]** e seleziona ![gestione feed](assets/feedmanagement.png). Nella scheda **[!UICONTROL Componenti consentiti]**, espandi il pannello a soffietto **[!UICONTROL Generale]**, seleziona l&#39;opzione **[!UICONTROL Modulo AEM]** e seleziona ![icona_salvataggio](assets/save_icon.svg). Il componente contenitore [!DNL Forms] dell&#39;AEM è abilitato per la pagina.

1. Aprire la scheda del browser contenente la pagina AEM [!DNL Sites] aperta al passaggio 1. Selezionare la casella **[!UICONTROL Trascina qui i componenti]** e selezionare **+.** Nella casella **[!UICONTROL Inserisci nuovo componente]** selezionare **[!UICONTROL Modulo AEM]**. Il componente **[!UICONTROL Contenitore AEM Forms]** è stato aggiunto alla pagina.
1. Seleziona il componente **[!UICONTROL AEM Forms container]** e seleziona ![configure-icon](assets/configure-icon.svg). Verrà visualizzata una finestra di dialogo con le proprietà del contenitore [!DNL Forms] dell&#39;AEM. Nel campo **[!UICONTROL Percorso risorsa]**, sfoglia e seleziona il modulo adattivo shipping-address-add-update-form. Seleziona ![icona_salvataggio](assets/save_icon.svg). Il modulo adattivo è incorporato nella pagina.
1. Publish presenta sia il modulo adattivo che la pagina [!DNL Sites]. Di seguito sono riportati alcuni punti da considerare:

   * Se si pubblica la pagina AEM [!DNL Sites] per la prima volta e include un modulo incorporato, pubblicare la pagina [!DNL Sites] e il modulo incorporato.
   * Se si modifica solo il modulo incorporato in una pagina del sito pubblicata, pubblicare il modulo originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento al modulo e non richiede la ripubblicazione della pagina.
   * Se si modifica la pagina [!DNL Sites] e il modulo incorporato, ripubblicare la pagina [!DNL Sites] e il modulo.

     ![incorporare in aem-sites](assets/embed-in-aem-sites.png)

   Modulo di modifica dell&#39;indirizzo di spedizione e fatturazione aggiunto a una pagina AEM [!DNL Sites].

## Incorporare il modulo adattivo in una pagina web esterna {#embed-the-adaptive-form-in-an-external-webpage}

Puoi incorporare un modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata al di fuori dell’AEM) inserendo alcune righe di JavaScript nella pagina web esterna. Il codice JavaScript invia una richiesta HTTP al server AEM [!DNL Forms] per il modulo adattivo e le risorse correlate e aggiunge il modulo adattivo alla pagina Web. Per i passaggi dettagliati, consulta [incorporare il modulo adattivo in una pagina Web esterna](/help/forms/using/embed-adaptive-form-external-web-page.md).
