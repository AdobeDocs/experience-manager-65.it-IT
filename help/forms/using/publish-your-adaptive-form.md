---
title: '"Esercitazione: Pubblicare il modulo adattivo"'
seo-title: '"Esercitazione: Pubblicare il modulo adattivo"'
description: Pubblicare il modulo adattivo come pagina AEM, incorporare il modulo in una pagina AEM Sites  o incorporare il modulo adattivo in una pagina Web esterna
seo-description: Pubblicare il modulo adattivo come pagina AEM, incorporare il modulo in una pagina AEM Sites  o incorporare il modulo adattivo in una pagina Web esterna
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---


# Esercitazione: Pubblicare il modulo adattivo {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Questa esercitazione è un passaggio della serie [Crea il tuo primo modulo adattivo](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

Una volta che il modulo adattivo è pronto, è possibile pubblicare il modulo per renderlo disponibile agli utenti finali. Gli utenti finali possono aprire il modulo pubblicato su qualsiasi dispositivo e browser Internet. Quando un modulo adattivo viene pubblicato, il modulo e il contenuto correlato vengono copiati da un’istanza di AEM autore a un’istanza AEM pubblicazione. Il modulo viene reso disponibile all’utente finale tramite l’istanza di pubblicazione.

Esistono i seguenti metodi per pubblicare un modulo adattivo:

* [Pubblicare il modulo adattivo come pagina AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporare il modulo adattivo in una  pagina AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporare il modulo adattivo in una pagina Web esterna (una pagina Web non AEM ospitata all’esterno di AEM)](../../forms/using/publish-your-adaptive-form.md)

## Prima di iniziare {#before-you-start}

* **[Configurate un’istanza](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)** di pubblicazione AEM Forms : L’istanza di pubblicazione è un’istanza pubblica di AEM  [!DNL Forms] in esecuzione in modalità di pubblicazione. In un ambiente di produzione, l’istanza di pubblicazione si trova all’esterno del firewall dell’organizzazione.
* **[Configurare la replica e la replica](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)** inversa: La replica copia il contenuto dall’istanza di creazione a un’istanza di pubblicazione e restituisce l’input dell’utente (ad esempio, l’input del modulo) dall’istanza di pubblicazione all’istanza di creazione.

## Pubblicare il modulo adattivo come AEM pagina {#publish-the-adaptive-form-as-an-aem-page}

Quando il modulo adattivo viene pubblicato come pagina AEM, l’intera pagina Web contiene solo il modulo pubblicato. È possibile utilizzare l&#39;URL del modulo adattivo per collegarlo da un&#39;altra pagina Web. Per pubblicare il modulo adattivo **shipping-address-add-update-form** come pagina AEM:

1. Accedete a AEM istanza di creazione [!DNL Forms] e individuate il modulo adattivo per la spedizione-indirizzo-add-update-form nell&#39;interfaccia AEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Selezionate il modulo adattivo per l&#39;indirizzo di spedizione, l&#39;indirizzo e l&#39;aggiornamento e toccate **[!UICONTROL Pubblica]**. Viene visualizzata una finestra di dialogo contenente le risorse correlate al modulo adattivo. Toccate **[!UICONTROL Pubblica]**. Il modulo adattivo viene pubblicato e viene visualizzata una finestra di dialogo di riuscita.
1. Aprire il modulo nell’istanza di pubblicazione. Il modulo è disponibile per la compilazione e l&#39;invio da parte dell&#39;utente finale.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporare il modulo adattivo in una  pagina AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] consente agli sviluppatori di moduli di incorporare direttamente moduli adattivi in una pagina [!DNL Sites] AEM. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente agli utenti di restare nel contesto di altri elementi della pagina Web e di interagire contemporaneamente con il modulo.

AEM [!DNL Forms] fornire un componente, AEM [!DNL Forms] Container, per incorporare un modulo adattivo in una pagina AEM [!DNL Sites]. Per impostazione predefinita, il componente non è visibile nel contenitore AEM [!DNL Sites]. Effettuate le seguenti operazioni per attivare il componente contenitore AEM [!DNL Forms] e per incorporare il modulo adattivo in una pagina AEM [!DNL Sites]:

1. Create e aprite una pagina nel sito We.Retail per la modifica. Ad esempio, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Il modulo adattivo è incorporato nella pagina [!DNL Sites].

   È inoltre possibile incorporare il modulo adattivo in una pagina esistente di We.Retail [!DNL Site's]. Ad esempio, la pagina ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Consente di risparmiare tempo per la creazione di una pagina. Nei passaggi seguenti viene utilizzata la pagina appena creata.

   Il sito We.Retail viene fornito con AEM. Se il sito We.Retail non è installato, vedere [We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) installare il sito.

1. Toccate le informazioni di pagina ![proprietà](assets/properties.png) e selezionate l&#39;opzione **[!UICONTROL Modifica modello]** nella pagina del sito Web We.Retail appena creata. Il modello della pagina si apre in una nuova scheda del browser.
1. Toccate all&#39;interno della casella **[!UICONTROL Contenitore di layout]** e toccate ![Gestione feed](assets/feedmanagement.png). Nella scheda **[!UICONTROL Componenti consentiti]**, espandere il pannello di controllo **[!UICONTROL Generale]**, selezionare l&#39;opzione **[!UICONTROL AEM Form]** e toccare ![save_icon](assets/save_icon.svg). Il componente Contenitore AEM [!DNL Forms] è abilitato per la pagina.

1. Aprite la scheda del browser contenente AEM pagina [!DNL Sites] aperta nel passaggio 1. Toccate la casella **[!UICONTROL Trascinate qui i componenti]** e toccate **+.** Nella  **[!UICONTROL casella Inserisci nuovo]** componente, toccare  **[!UICONTROL AEM modulo]**. Il componente **[!UICONTROL AEM Forms Container]** viene aggiunto alla pagina.
1. Toccate il componente **[!UICONTROL contenitore AEM Forms]** e toccate ![configure-icon](assets/configure-icon.svg). Viene visualizzata una finestra di dialogo con le proprietà del contenitore AEM [!DNL Forms]. Nel campo **[!UICONTROL Percorso risorsa]**, individuare e selezionare il modulo adattivo per l&#39;indirizzo di spedizione, l&#39;indirizzo e l&#39;aggiornamento. Toccate ![save_icon](assets/save_icon.svg). Il modulo adattivo è incorporato nella pagina.
1. Pubblicate il modulo adattivo e la pagina [!DNL Sites]. Di seguito sono riportati alcuni punti da tenere in considerazione:

   * Se si pubblica la pagina AEM [!DNL Sites] per la prima volta e include un modulo incorporato, pubblicare la pagina [!DNL Sites] e il modulo incorporato.
   * Se modificate solo il modulo incorporato in una pagina del sito pubblicata, pubblicate il modulo originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento al modulo e non richiede la ripubblicazione della pagina.
   * Se si modifica la pagina [!DNL Sites] e il modulo incorporato, è necessario ripubblicare la pagina [!DNL Sites] e il modulo.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Modulo di modifica indirizzo di spedizione e fatturazione aggiunto a una pagina di AEM [!DNL Sites].

## Incorporare il modulo adattivo in una pagina Web esterna {#embed-the-adaptive-form-in-an-external-webpage}

È possibile incorporare un modulo adattivo in una pagina Web esterna (una pagina Web non AEM ospitata all&#39;esterno di AEM) inserendo alcune righe di JavaScript nella pagina Web esterna. Il codice JavaScript invia una richiesta HTTP al server AEM [!DNL Forms] per il modulo adattivo e le risorse correlate e aggiunge il modulo adattivo alla pagina Web. Per i passaggi dettagliati, vedere [incorporare il modulo adattivo in una pagina Web esterna](/help/forms/using/embed-adaptive-form-external-web-page.md).
