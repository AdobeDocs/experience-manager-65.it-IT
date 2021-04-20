---
title: '"Esercitazione: Pubblica il tuo modulo adattivo"'
seo-title: '"Esercitazione: Pubblica il tuo modulo adattivo"'
description: Pubblica il modulo adattivo come pagina AEM, incorpora il modulo in una pagina AEM Sites o incorpora il modulo adattivo in una pagina web esterna
seo-description: Pubblica il modulo adattivo come pagina AEM, incorpora il modulo in una pagina AEM Sites o incorpora il modulo adattivo in una pagina web esterna
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 2%

---


# Esercitazione: Pubblicare il modulo adattivo {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Questa esercitazione è un passaggio della serie [Crea il tuo primo modulo adattivo](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) . Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

Una volta pronto il modulo adattivo, puoi pubblicarlo per renderlo disponibile agli utenti finali. Gli utenti finali possono aprire il modulo pubblicato su qualsiasi dispositivo e browser Internet. Quando viene pubblicato un modulo adattivo, il modulo e il contenuto correlato vengono copiati da un’istanza di authoring AEM in un’istanza di pubblicazione AEM. Il modulo viene reso disponibile all’utente finale tramite l’istanza di pubblicazione.

Per pubblicare un modulo adattivo sono disponibili i seguenti metodi:

* [Pubblicare il modulo adattivo come pagina AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporare il modulo adattivo in una pagina AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporare il modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata all’esterno di AEM)](../../forms/using/publish-your-adaptive-form.md)

## Prima di iniziare {#before-you-start}

* **[Imposta un&#39;istanza](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)** di pubblicazione AEM Forms: L’istanza di pubblicazione è un’istanza rivolta al pubblico di AEM  [!DNL Forms] in esecuzione in modalità di pubblicazione. In un ambiente di produzione, l&#39;istanza di pubblicazione si trova al di fuori del firewall dell&#39;organizzazione.
* **[Imposta replica e replica](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)** inversa: La replica copia il contenuto dall’istanza di authoring a un’istanza di pubblicazione e restituisce l’input dell’utente (ad esempio, l’input del modulo) dall’istanza di pubblicazione all’istanza di authoring.

## Pubblica il modulo adattivo come pagina AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando il modulo adattivo viene pubblicato come pagina AEM, l’intera pagina web contiene solo il modulo pubblicato. Puoi utilizzare l’URL del modulo adattivo per collegarlo da un’altra pagina web. Per pubblicare il modulo adattivo **shipping-address-add-update-form** come pagina AEM:

1. Accedi all&#39;istanza di authoring AEM [!DNL Forms] e individua il modulo adattivo per l&#39;indirizzo di spedizione-add-update-form nell&#39;interfaccia utente AEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleziona il modulo adattivo per l’indirizzo di spedizione-aggiunta-aggiornamento-modulo e tocca **[!UICONTROL Pubblica]**. Viene visualizzata una finestra di dialogo contenente le risorse correlate al modulo adattivo. Tocca **[!UICONTROL Pubblica]**. Il modulo adattivo viene pubblicato e viene visualizzata una finestra di dialogo di successo.
1. Apri il modulo nell’istanza di pubblicazione. Il modulo è disponibile per la compilazione e l’invio da parte dell’utente finale.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporare il modulo adattivo in una pagina AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] consente agli sviluppatori di moduli di incorporare facilmente i moduli adattivi in una pagina AEM [!DNL Sites]. Il modulo adattivo incorporato è completamente funzionale e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo.

AEM [!DNL Forms] fornire un componente, AEM [!DNL Forms] Container, per incorporare un modulo adattivo in una pagina AEM [!DNL Sites]. Per impostazione predefinita, il componente non è visibile nel contenitore AEM [!DNL Sites] . Esegui i seguenti passaggi per abilitare il componente AEM [!DNL Forms] Contenitore e per incorporare il modulo adattivo in una pagina AEM [!DNL Sites]:

1. Crea e apri una pagina del sito We.Retail per la modifica. Ad esempio, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Il modulo adattivo è incorporato nella pagina [!DNL Sites] .

   Puoi anche incorporare il modulo adattivo in una pagina esistente di We.Retail [!DNL Site's] . Ad esempio, la pagina ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Consente di risparmiare tempo per la creazione di una pagina. I passaggi seguenti utilizzano la pagina appena creata.

   Il sito We.Retail viene fornito con AEM. Se non hai installato il sito We.Retail, consulta [Implementazione di riferimento We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) installare il sito.

1. Tocca ![proprietà](assets/properties.png) informazioni sulla pagina e seleziona l’opzione **[!UICONTROL Modifica modello]** nella pagina del sito We.Retail appena creata. Il modello della pagina viene aperto in una nuova scheda del browser.
1. Tocca all’interno della casella **[!UICONTROL Contenitore di layout]** e tocca ![gestione dei feed](assets/feedmanagement.png). Nella scheda **[!UICONTROL Componenti consentiti]** , espandi il pannello a soffietto **[!UICONTROL Generale]**, seleziona l’opzione **[!UICONTROL AEM modulo]** e tocca ![salva_icona](assets/save_icon.svg). Il componente AEM [!DNL Forms] Contenitore è abilitato per la pagina.

1. Apri la scheda del browser contenente AEM pagina [!DNL Sites] aperta al passaggio 1. Tocca la casella **[!UICONTROL Trascina qui i componenti]** e tocca **+.** Nella  **[!UICONTROL casella Inserisci nuovo]** componente, toccare  **[!UICONTROL AEM modulo]**. Il componente **[!UICONTROL AEM Forms Container]** viene aggiunto alla pagina.
1. Tocca il componente **[!UICONTROL contenitore AEM Forms]** e tocca ![configure-icon](assets/configure-icon.svg). Viene visualizzata una finestra di dialogo con le proprietà AEM contenitore [!DNL Forms]. Nel campo **[!UICONTROL Percorso risorsa]** , sfoglia e seleziona il modulo adattivo per l’indirizzo di spedizione-add-update-form. Tocca ![save_icon](assets/save_icon.svg). Il modulo adattivo è incorporato nella pagina .
1. Pubblica il modulo adattivo e la pagina [!DNL Sites] . Di seguito sono riportati alcuni punti da tenere in considerazione:

   * Se si pubblica la pagina AEM [!DNL Sites] per la prima volta e include un modulo incorporato, pubblicare la pagina [!DNL Sites] e il modulo incorporato.
   * Se si modifica solo il modulo incorporato in una pagina del sito pubblicata, pubblicare il modulo originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento al modulo e non richiede la ripubblicazione della pagina.
   * Se si modificano la pagina [!DNL Sites] e il modulo incorporato, ripubblicare la pagina [!DNL Sites] e il modulo.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Modulo di modifica dell&#39;indirizzo di spedizione e fatturazione aggiunto a una pagina AEM [!DNL Sites].

## Incorporare il modulo adattivo in una pagina web esterna {#embed-the-adaptive-form-in-an-external-webpage}

È possibile incorporare un modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata all’esterno di AEM) inserendo alcune righe di JavaScript nella pagina web esterna. Il codice JavaScript invia una richiesta HTTP al server AEM [!DNL Forms] per il modulo adattivo e le risorse correlate e aggiunge il modulo adattivo alla pagina web. Per passaggi dettagliati, consulta [incorporare il modulo adattivo in una pagina web esterna](/help/forms/using/embed-adaptive-form-external-web-page.md).
