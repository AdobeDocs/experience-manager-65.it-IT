---
title: Clientlibs per componenti Community
seo-title: Clientlibs per componenti Community
description: Librerie lato client per Communities
seo-description: Librerie lato client per Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: f6aa95514a266a042c9bd1165634e30e80479ae7
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Clientlibs per componenti Community {#clientlibs-for-communities-components}

## Introduzione {#introduction}

Questa sezione della documentazione descrive come aggiungere librerie lato client (clientlibs) a una pagina per i componenti Community.

Per informazioni di base, visita :

* [Utilizzo delle librerie](/help/sites-developing/clientlibs.md) lato client per fornire dettagli di utilizzo e strumenti di debug
* [Clientlibs per SCF](/help/communities/client-customize.md#clientlibs) che fornisce informazioni utili per la personalizzazione dei componenti SCF
* [Blog : AEM librerie client spiegate dall&#39;esempio](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Perché Clientlibs sono richiesti {#why-clientlibs-are-required}

Per il corretto funzionamento (JavaScript) e lo stile (CSS) di un componente sono necessari i client.

Se esiste una funzione [](/help/communities/functions.md) comunitaria per una funzione, tutti i componenti e le configurazioni necessari, inclusi i clientlibs richiesti, saranno presenti nel sito della community. Solo se agli autori devono essere disponibili componenti aggiuntivi, è necessario aggiungere altri clientlibé.

Se i clientlibs richiesti non sono disponibili, l’ [aggiunta di un componente Community a una pagina](/help/communities/author-communities.md) potrebbe causare errori javascript e un aspetto imprevisto.

### Esempio: Recensioni inserite senza Clientlibs {#example-placed-reviews-without-clientlibs}

![valutazioni inserite](assets/placed-reviews.png)

### Esempio: Recensioni inserite con Clientlibs {#example-placed-reviews-with-clientlibs}

![recensioni-clientlibs](assets/reviews-clientlibs.png)

## Identificazione delle librerie di client necessarie {#identifying-required-clientlibs}

Le informazioni essenziali sulle funzioni per gli sviluppatori identificano i clientlibs richiesti.

Inoltre, da un&#39;istanza AEM, l&#39;accesso alla Guida [ai componenti](/help/communities/components-guide.md) comunitari consente di accedere a un elenco delle categorie clientlib richieste per un componente.

Ad esempio, nella parte superiore della pagina [](https://localhost:4502/content/community-components/en/reviews.html) Recensioni i clientlibs richiesti sono elencati

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Aggiunta Di Clientlibs Richiesti {#adding-required-clientlibs}

Se si desidera aggiungere un componente Community a una pagina, sarà necessario aggiungere i clientlibs richiesti per il componente, se non è già presente.

Utilizzare [CRXDE|Lite](#using-crxde-lite) per modificare un elenco di clientlibslist esistente per una pagina di sito community.

Per aggiungere una clientlib per un sito community utilizzando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Individuate [https://&lt;server>:&lt;porta>/crx/de](https://localhost:4502/crx/de).
* Individuare il `clientlibslist` nodo della pagina in cui si desidera aggiungere il componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con `clientlibslist` il nodo selezionato:

   * Individuare la proprietà String[] `scg:requiredClientLibs`.
   * Selezionare la stringa `Value` per accedere alla finestra di dialogo dell&#39;array String.

      * Se necessario, scorrete verso il basso.
      * Selezionate + per immettere una nuova libreria client.

         * Ripetete questa procedura per aggiungere altre librerie client.

         * Selezionare **OK**.
   * Selezionate **Salva tutto**.


>[!NOTE]
>
>Se il sito non è un sito community, è necessario individuare l&#39;esistenza o la posizione delle librerie client in uso per il sito.


Utilizzando l’ [esempio Guida introduttiva  AEM Communities](/help/communities/getting-started.md) , in cui `site-name` è *attiva*, l’elenco clientliblist viene visualizzato così se si aggiunge il componente recensioni:

![review-component](assets/review-component.png)

