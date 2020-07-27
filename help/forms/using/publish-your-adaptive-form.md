---
title: '"Esercitazione: Pubblicare il modulo adattivo"'
seo-title: '"Esercitazione: Pubblicare il modulo adattivo"'
description: Pubblicate il modulo adattivo come pagina AEM, incorporate il modulo in una pagina di AEM Sites o incorporate il modulo adattivo in una pagina Web esterna
seo-description: Pubblicate il modulo adattivo come pagina AEM, incorporate il modulo in una pagina di AEM Sites o incorporate il modulo adattivo in una pagina Web esterna
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---


# Esercitazione: Pubblicare il modulo adattivo {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Questa esercitazione è un passaggio della serie [Crea il primo modulo](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) adattivo. Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

Una volta che il modulo adattivo è pronto, è possibile pubblicare il modulo per renderlo disponibile agli utenti finali. Gli utenti finali possono aprire il modulo pubblicato su qualsiasi dispositivo e browser Internet. Quando viene pubblicato un modulo adattivo, il modulo e il contenuto correlato vengono copiati da un’istanza di creazione AEM a un’istanza di pubblicazione AEM. Il modulo viene reso disponibile all’utente finale tramite l’istanza di pubblicazione.

Esistono i seguenti metodi per pubblicare un modulo adattivo:

* [Pubblicare il modulo adattivo come pagina AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporare il modulo adattivo in una pagina AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporare il modulo adattivo in una pagina Web esterna (una pagina Web non AEM ospitata all’esterno di AEM)](../../forms/using/publish-your-adaptive-form.md)

## Prima di iniziare {#before-you-start}

* **[Impostate un’istanza](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**di pubblicazione AEM Forms: L’istanza di pubblicazione è un’istanza pubblica di AEM Forms in esecuzione in modalità di pubblicazione. In un ambiente di produzione, l’istanza di pubblicazione si trova all’esterno del firewall dell’organizzazione.
* **[Configurare la replica e la replica](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**inversa: La replica copia il contenuto dall’istanza di creazione a un’istanza di pubblicazione e restituisce l’input dell’utente (ad esempio, l’input del modulo) dall’istanza di pubblicazione all’istanza di creazione.

## Pubblicare il modulo adattivo come pagina AEM {#publish-the-adaptive-form-as-an-aem-page}

Quando il modulo adattivo viene pubblicato come pagina AEM, l’intera pagina Web contiene solo il modulo pubblicato. È possibile utilizzare l&#39;URL del modulo adattivo per collegarlo da un&#39;altra pagina Web. Per pubblicare il modulo adattivo **shipping-address-add-update-form** come pagina AEM:

1. Accedete all’istanza di creazione dei AEM Forms e individuate il modulo adattivo per l’indirizzo di spedizione, il modulo Add-update-form nell’interfaccia utente dei AEM Forms.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Selezionate il modulo adattivo per l’indirizzo di spedizione, il modulo per l’aggiornamento e toccate **Pubblica**. Viene visualizzata una finestra di dialogo contenente le risorse correlate al modulo adattivo. Toccate **Pubblica**. Il modulo adattivo viene pubblicato e viene visualizzata una finestra di dialogo di riuscita.
1. Aprire il modulo nell’istanza di pubblicazione. Il modulo è disponibile per la compilazione e l&#39;invio da parte dell&#39;utente finale.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporare il modulo adattivo in una pagina AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

I AEM Forms consentono agli sviluppatori di moduli di incorporare facilmente moduli adattivi in una pagina AEM Sites. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente agli utenti di restare nel contesto di altri elementi della pagina Web e di interagire contemporaneamente con il modulo.

I AEM Forms forniscono un componente, Contenitore AEM Forms, per incorporare un modulo adattivo in una pagina di AEM Sites. Per impostazione predefinita, il componente non è visibile nel contenitore AEM Sites. Effettuate le seguenti operazioni per abilitare il componente Contenitore AEM Forms e incorporare il modulo adattivo in una pagina AEM Sites:

1. Create e aprite una pagina nel sito We.Retail per la modifica. Ad esempio, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Il modulo adattivo è incorporato nella pagina dei siti.

   È inoltre possibile incorporare il modulo adattivo in una pagina esistente del sito Web We.Retail. Ad esempio, la pagina ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Consente di risparmiare tempo per la creazione di una pagina. Nei passaggi seguenti viene utilizzata la pagina appena creata.

   Il sito We.Retail viene fornito con AEM. Se il sito We.Retail non è installato, vedere l&#39;implementazione [di riferimento](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) We.Retail installare il sito.

1. Toccate ![le informazioni sulla pagina delle proprietà](assets/properties.png) e selezionate l&#39;opzione **Modifica modello** nella pagina del sito Web We.Retail appena creata. Il modello della pagina si apre in una nuova scheda del browser.
1. Toccate all&#39;interno della casella Contenitore **di** layout e toccate ![Gestione](assets/feedmanagement.png)feed. Nella scheda Componenti **** consentiti, espandete il **pannello a soffietto Generale** , selezionate l&#39;opzione Modulo **** AEM e toccate ![save_icon](assets/save_icon.svg). Il componente Contenitore AEM Forms è abilitato per la pagina.

1. Aprite la scheda del browser contenente la pagina dei AEM Sites aperta al punto 1. Toccate la casella **Trascinate qui** i componenti e toccate **+.** Nella casella **Inserisci nuovo componente** , toccate Modulo **AEM.** Il componente Contenitore **** AEM Forms viene aggiunto alla pagina.
1. Toccate il componente contenitore **** AEM Forms e toccate ![l’icona](assets/configure-icon.svg)di configurazione. Viene visualizzata una finestra di dialogo con le proprietà del contenitore AEM Forms. Nel campo Percorso **** risorsa, individuate e selezionate il modulo adattivo per l’indirizzo di spedizione, il modulo Add-update-form. Toccate ![save_icon](assets/save_icon.svg). Il modulo adattivo è incorporato nella pagina.
1. Pubblicate il modulo adattivo e la pagina dei siti. Di seguito sono riportati alcuni punti da tenere in considerazione:

   * Se si pubblica per la prima volta la pagina dei siti AEM e si include un modulo incorporato, pubblicare la pagina dei siti e il modulo incorporato.
   * Se modificate solo il modulo incorporato in una pagina del sito pubblicata, pubblicate il modulo originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento al modulo e non richiede la ripubblicazione della pagina.
   * Se si modificano la pagina del sito e il modulo incorporato, è necessario ripubblicare la pagina del sito e il modulo.

   ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Modulo di modifica indirizzo di spedizione e fatturazione aggiunto a una pagina AEM Sites.

## Incorporare il modulo adattivo in una pagina Web esterna {#embed-the-adaptive-form-in-an-external-webpage}

Potete incorporare un modulo adattivo in una pagina Web esterna (una pagina Web non AEM ospitata all’esterno di AEM) inserendo alcune righe di JavaScript nella pagina Web esterna. Il codice JavaScript invia una richiesta HTTP al server AEM Forms per il modulo adattivo e le risorse correlate e aggiunge il modulo adattivo alla pagina Web. Per i passaggi dettagliati, vedere [Incorporare il modulo adattivo in una pagina](/help/forms/using/embed-adaptive-form-external-web-page.md)Web esterna.
