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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Componenti Clientlibs per Community {#clientlibs-for-communities-components}

## Introduzione {#introduction}

Questa sezione della documentazione descrive come aggiungere librerie lato client (clientlibs) a una pagina per i componenti Community.

Per informazioni di base, visita :

* [Utilizzo delle ](/help/sites-developing/clientlibs.md) librerie lato client per fornire dettagli di utilizzo e strumenti di debug
* [Clientlibs per ](/help/communities/client-customize.md#clientlibs) SCF, che fornisce informazioni utili per la personalizzazione dei componenti SCF
* [Blog : AEM librerie client spiegate dall&#39;esempio](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Perché Clientlibs sono richiesti {#why-clientlibs-are-required}

Per il corretto funzionamento (JavaScript) e lo stile (CSS) di un componente sono necessari i client.

Quando esiste una [funzione community](/help/communities/functions.md) per una funzione, tutti i componenti e le configurazioni necessari, inclusi i clientlibs richiesti, saranno presenti nel sito community. Solo se agli autori devono essere disponibili componenti aggiuntivi, è necessario aggiungere altri clientlibé.

Se mancano i clientlibs richiesti, l&#39;aggiunta di un componente Community a una pagina[ potrebbe causare errori javascript e un aspetto imprevisto.](/help/communities/author-communities.md)

### Esempio: Recensioni inserite senza Clientlibs {#example-placed-reviews-without-clientlibs}

![valutazioni inserite](assets/placed-reviews.png)

### Esempio: Recensioni inserite con Clientlibs {#example-placed-reviews-with-clientlibs}

![recensioni-clientlibs](assets/reviews-clientlibs.png)

## Identificazione delle librerie di client necessarie {#identifying-required-clientlibs}

Le informazioni essenziali sulle funzioni per gli sviluppatori identificano i clientlibs richiesti.

Inoltre, da un&#39;istanza AEM, l&#39;accesso alla [Guida ai componenti della community](/help/communities/components-guide.md) consente di accedere a un elenco delle categorie clientlib richieste per un componente.

Ad esempio, nella parte superiore della pagina [Recensioni](https://localhost:4502/content/community-components/en/reviews.html) i clientlibs richiesti elencati sono

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Aggiunta di Clientlibs richiesti {#adding-required-clientlibs}

Se si desidera aggiungere un componente Community a una pagina, sarà necessario aggiungere i clientlibs richiesti per il componente, se non è già presente.

Utilizzate [CRXDE|Lite](#using-crxde-lite) per modificare un elenco di clientlibslist esistente per una pagina di sito community.

Per aggiungere una clientlib per un sito community utilizzando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Individuate [https://&lt;server>:&lt;porta>/crx/de](https://localhost:4502/crx/de).
* Individuare il nodo `clientlibslist` per la pagina in cui si desidera aggiungere il componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con il nodo `clientlibslist` selezionato:

   * Individuare la proprietà String[] `scg:requiredClientLibs`.
   * Selezionare `Value` per accedere alla finestra di dialogo dell&#39;array String.

      * Se necessario, scorrete verso il basso.
      * Selezionate + per immettere una nuova libreria client.

         * Ripetete questa procedura per aggiungere altre librerie client.

         * Selezionare **OK**.
   * Selezionare **Salva tutto**.


>[!NOTE]
>
>Se il sito non è un sito community, è necessario individuare l&#39;esistenza o la posizione delle librerie client in uso per il sito.

Utilizzando l&#39;esempio [Guida introduttiva a  AEM Communities](/help/communities/getting-started.md), dove `site-name` è *interazione*, l&#39;elenco clientliblist viene visualizzato in questo modo se si aggiunge il componente recensioni:

![review-component](assets/review-component.png)

