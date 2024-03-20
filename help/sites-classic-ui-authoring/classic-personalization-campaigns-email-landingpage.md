---
title: Creazione di una pagina di destinazione efficace per la newsletter
description: Una pagina di destinazione efficace per la newsletter ti consente di iscrivere quante più persone possibile alla newsletter (o ad altre campagne di e-mail marketing). Per ottenere i lead, puoi utilizzare le informazioni raccolte dalle iscrizioni alle newsletter.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Creazione di una pagina di destinazione efficace per la newsletter{#creating-an-effective-newsletter-landing-page}

Una pagina di destinazione efficace per la newsletter ti consente di iscrivere quante più persone possibile alla newsletter (o ad altre campagne di e-mail marketing). Per ottenere i lead, puoi utilizzare le informazioni raccolte dalle iscrizioni alle newsletter.

Per creare una pagina di destinazione efficace per la newsletter, devi effettuare le seguenti operazioni:

1. Crea un elenco per la newsletter in modo che le persone possano iscriversi alla newsletter.
1. Creare il modulo di registrazione. In questo caso, aggiungi un passaggio del flusso di lavoro che aggiunga automaticamente all’elenco dei lead la persona che si iscrive alla newsletter.
1. Crea una pagina di conferma che ringrazia gli utenti per la registrazione ed eventualmente offre loro una promozione.
1. Aggiungere teaser.

>[!NOTE]
>
>L’Adobe non prevede di migliorare ulteriormente questa funzionalità (Gestione di lead ed elenchi).
>Si consiglia di utilizzare [Adobe Campaign e l&#39;integrazione con l&#39;AEM](/help/sites-administering/campaign.md).

## Creazione di un elenco per la newsletter {#creating-a-list-for-the-newsletter}

Crea un elenco, ad esempio: **Newsletter Geometrixx**, in MCM per la newsletter a cui le persone devono abbonarsi. La creazione degli elenchi è descritta in [Creazione di elenchi](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

Di seguito è riportato un esempio di elenco:

![mcm_listcreate](assets/mcm_listcreate.png)

## Creare un modulo di registrazione {#create-a-sign-up-form}

Crea un modulo di registrazione per newsletter che consenta agli utenti di iscriversi ai tag. Il Geometrixx Web di esempio include una pagina newsletter nella barra degli strumenti di Geometrixx in cui è possibile creare il modulo.

Per creare un modulo per newsletter personalizzato, consulta le informazioni sulla creazione di moduli in [Documentazione di Forms](/help/sites-authoring/default-components.md#form). La newsletter utilizza i tag della libreria Tag. Per aggiungere altri tag, consulta [Amministrazione tag](/help/sites-authoring/tags.md#tagadministration).

I campi nascosti nell’esempio seguente forniscono la quantità minima di informazioni (e-mail); inoltre, è possibile aggiungere altri campi in un secondo momento, ma questo influirà sul tasso di conversione.

L&#39;esempio seguente è un modulo creato in https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html.

1. Crea il modulo.

   ![mcm_newsletter](assets/mcm_newsletterpage.png)

1. Clic **Modifica** nel componente Modulo per configurare il modulo in modo che venga visualizzata una pagina di ringraziamento (vedere [Creazione di pagine di ringraziamento](#creating-a-thank-you-page)).

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. Imposta l’azione Modulo (che si verifica quando invii il modulo) e configura il gruppo per assegnare gli utenti registrati all’elenco creato in precedenza (ad esempio, geometrixx-newsletter).

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### Creazione di una pagina di ringraziamento {#creating-a-thank-you-page}

Quando gli utenti fanno clic su **Iscriviti ora**, si desidera aprire automaticamente una pagina di ringraziamento. Crea la pagina di ringraziamento nella pagina Newsletter di Geometrixx. Dopo aver creato il modulo newsletter, modifica il componente Modulo e aggiungi il percorso alla pagina di ringraziamento.

Quando si invia la richiesta, l’utente riceve un **Grazie** dopo di che riceveranno un’e-mail. La pagina di ringraziamento è stata creata in /content/geometrixx/en/toolbar/newsletter/thank_you.

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### Aggiunta di teaser {#adding-teasers}

Aggiungi [teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) per rivolgersi a tipi di pubblico specifici. Ad esempio, puoi aggiungere teaser alla pagina di ringraziamento e alla pagina di iscrizione alla newsletter.

Per aggiungere teaser per creare una pagina di destinazione efficace per le newsletter:

1. Crea un paragrafo teaser per un regalo di iscrizione. Seleziona **Primo** come strategia e includi un testo che informi il cliente in merito al regalo che riceverà.

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. Crea un paragrafo teaser per la pagina di ringraziamento. Seleziona **Primo** come strategia e includi il testo che indica che il regalo è in arrivo.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Crea una campagna con i due teaser: assegna un tag a business e uno a tutti e due.

### Invio di contenuti agli abbonati {#pushing-content-to-subscribers}

Invia le modifiche alle pagine tramite la funzionalità Newsletter in MCM. Dopodiché invii agli abbonati i contenuti aggiornati.

Consulta [Invio di newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
