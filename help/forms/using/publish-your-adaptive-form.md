---
title: "Esercitazione: Pubblica il tuo modulo adattivo"
seo-title: "Tutorial: Publish your adaptive form"
description: Pubblica il modulo adattivo come pagina AEM, incorpora il modulo in una pagina AEM Sites o incorpora il modulo adattivo in una pagina web esterna
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---

# Esercitazione: Pubblicare il modulo adattivo {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Questa esercitazione è un passaggio nel [Creare il primo modulo adattivo](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) serie. Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

Una volta pronto il modulo adattivo, puoi pubblicarlo per renderlo disponibile agli utenti finali. Gli utenti finali possono aprire il modulo pubblicato su qualsiasi dispositivo e browser Internet. Quando viene pubblicato un modulo adattivo, il modulo e il contenuto correlato vengono copiati da un’istanza di authoring AEM in un’istanza di pubblicazione AEM. Il modulo viene reso disponibile all’utente finale tramite l’istanza di pubblicazione.

Per pubblicare un modulo adattivo sono disponibili i seguenti metodi:

* [Pubblicare il modulo adattivo come pagina AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporare il modulo adattivo in una pagina AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporare il modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata all’esterno di AEM)](../../forms/using/publish-your-adaptive-form.md)

## Prima di iniziare {#before-you-start}

* **[Configurare un&#39;istanza di pubblicazione AEM Forms](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: L&#39;istanza di pubblicazione è un&#39;istanza di AEM rivolta al pubblico [!DNL Forms] in esecuzione in modalità di pubblicazione. In un ambiente di produzione, l&#39;istanza di pubblicazione si trova al di fuori del firewall dell&#39;organizzazione.
* **[Impostare la replica e la replica inversa](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: La replica copia il contenuto dall’istanza di authoring a un’istanza di pubblicazione e restituisce l’input dell’utente (ad esempio, l’input del modulo) dall’istanza di pubblicazione all’istanza di authoring.

## Pubblicare il modulo adattivo come pagina AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando il modulo adattivo viene pubblicato come pagina AEM, l’intera pagina web contiene solo il modulo pubblicato. Puoi utilizzare l’URL del modulo adattivo per collegarlo da un’altra pagina web. Per pubblicare **modulo di aggiornamento-indirizzo-spedizione** modulo adattivo come pagina AEM:

1. Accedi a AEM [!DNL Forms] istanza dell’autore e individua il modulo adattivo per l’indirizzo di spedizione-aggiunta-aggiornamento-modulo nell’AEM [!DNL Forms] Interfaccia utente.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleziona il modulo adattivo per l’indirizzo di spedizione, l’aggiunta dell’aggiornamento e tocca **[!UICONTROL Pubblica]**. Viene visualizzata una finestra di dialogo contenente le risorse correlate al modulo adattivo. Tocca **[!UICONTROL Pubblica]**. Il modulo adattivo viene pubblicato e viene visualizzata una finestra di dialogo di successo.
1. Apri il modulo nell’istanza di pubblicazione. Il modulo è disponibile per la compilazione e l’invio da parte dell’utente finale.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporare il modulo adattivo in una pagina AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] consente agli sviluppatori di moduli di incorporare facilmente i moduli adattivi in un AEM [!DNL Sites] pagina. Il modulo adattivo incorporato è completamente funzionale e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo.

AEM [!DNL Forms] fornire un componente, AEM [!DNL Forms] Contenitore, per incorporare un modulo adattivo in un AEM [!DNL Sites] pagina. Per impostazione predefinita, il componente non è visibile in AEM [!DNL Sites] contenitore. Esegui i seguenti passaggi per abilitare il AEM [!DNL Forms] Componente contenitore e per incorporare il modulo adattivo in un AEM [!DNL Sites] Pagina:

1. Crea e apri una pagina del sito We.Retail per la modifica. Ad esempio: [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Il modulo adattivo è incorporato nel [!DNL Sites] pagina.

   Puoi anche incorporare il modulo adattivo in un esistente We.Retail [!DNL Site's] pagina. Ad esempio, la pagina ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Consente di risparmiare tempo per la creazione di una pagina. I passaggi seguenti utilizzano la pagina appena creata.

   Il sito We.Retail viene fornito con AEM. Se non hai installato il sito We.Retail, consulta [Implementazione di riferimento di We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) installa il sito.

1. Tocca ![proprietà](assets/properties.png) informazioni sulla pagina e seleziona la **[!UICONTROL Modifica modello]** nella pagina del sito We.Retail appena creata. Il modello della pagina viene aperto in una nuova scheda del browser.
1. Tocca all’interno del **[!UICONTROL Contenitore di layout]** scatola e rubinetto ![alimentazione](assets/feedmanagement.png). In **[!UICONTROL Componenti consentiti]** scheda , espandi **[!UICONTROL Generale]** a soffietto, seleziona la **[!UICONTROL Modulo AEM]** e tocca ![save_icon](assets/save_icon.svg). AEM [!DNL Forms] Il componente Contenitore è abilitato per la pagina.

1. Apri la scheda del browser contenente AEM [!DNL Sites] pagina aperta al passaggio 1. Tocca **[!UICONTROL Trascina qui i componenti]** scatola e rubinetto **+** In **[!UICONTROL Inserisci nuovo componente]** scatola, toccare **[!UICONTROL Modulo AEM]**. La **[!UICONTROL Contenitore AEM Forms]** viene aggiunto alla pagina .
1. Tocca **[!UICONTROL Contenitore AEM Forms]** componente e tocco ![configure-icon](assets/configure-icon.svg). Finestra di dialogo con le proprietà di AEM [!DNL Forms] Viene visualizzato il contenitore . In **[!UICONTROL Percorso risorsa]** , sfoglia e seleziona il modulo adattivo per l’indirizzo di spedizione-aggiunta-aggiornamento-modulo. Tocca ![save_icon](assets/save_icon.svg). Il modulo adattivo è incorporato nella pagina .
1. Pubblicare sia il modulo adattivo che [!DNL Sites] pagina. Di seguito sono riportati alcuni punti da tenere in considerazione:

   * Se pubblichi il AEM [!DNL Sites] per la prima volta e include un modulo incorporato, pubblica il [!DNL Sites] e il modulo incorporato.
   * Se si modifica solo il modulo incorporato in una pagina del sito pubblicata, pubblicare il modulo originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento al modulo e non richiede la ripubblicazione della pagina.
   * Se modifichi la [!DNL Sites] pagina e il modulo incorporato, ripubblica [!DNL Sites] e il modulo.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Modulo di modifica dell&#39;indirizzo di spedizione e fatturazione aggiunto a un AEM [!DNL Sites] pagina.

## Incorporare il modulo adattivo in una pagina web esterna {#embed-the-adaptive-form-in-an-external-webpage}

È possibile incorporare un modulo adattivo in una pagina web esterna (una pagina web non AEM ospitata all’esterno di AEM) inserendo alcune righe di JavaScript nella pagina web esterna. Il codice JavaScript invia una richiesta HTTP al AEM [!DNL Forms] server per il modulo adattivo e le relative risorse e aggiunge il modulo adattivo alla pagina web. Per i passaggi dettagliati vedi [incorporare il modulo adattivo in una pagina web esterna](/help/forms/using/embed-adaptive-form-external-web-page.md).
