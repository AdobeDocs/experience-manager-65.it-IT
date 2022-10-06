---
title: Componenti Clientlibs for Communities
seo-title: Clientlibs for Communities Components
description: Librerie lato client per Communities
seo-description: Client-side libraries for Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Componenti Clientlibs for Communities {#clientlibs-for-communities-components}

## Introduzione {#introduction}

Questa sezione della documentazione descrive come aggiungere librerie lato client (clientlibs) a una pagina per i componenti di Communities.

Per informazioni di base, visita :

* [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md) che fornisce dettagli sull’utilizzo e strumenti di debug
* [Clientlibs per SCF](/help/communities/client-customize.md#clientlibs) che fornisce informazioni utili durante la personalizzazione dei componenti SCF


## Perché sono necessarie le clientlibs {#why-clientlibs-are-required}

Le librerie client sono necessarie per il corretto funzionamento (JavaScript) e lo stile (CSS) di un componente.

Quando esiste una [funzione comunitaria](/help/communities/functions.md) per una funzione, tutti i componenti e le configurazioni necessarie, incluse le clientlib richieste, saranno presenti nel sito community. Solo se gli autori devono disporre di componenti aggiuntivi, è necessario aggiungere ulteriori clientlibs.

Se mancano le clientlib richieste, [aggiunta di un componente Community a una pagina](/help/communities/author-communities.md) potrebbe causare errori javascript e un aspetto imprevisto.

### Esempio : Recensioni posizionate senza Clientlibs {#example-placed-reviews-without-clientlibs}

![valutazioni inserite](assets/placed-reviews.png)

### Esempio : Recensioni inserite con Clientlibs {#example-placed-reviews-with-clientlibs}

![recensioni-clientlibs](assets/reviews-clientlibs.png)

## Identificazione delle librerie client richieste {#identifying-required-clientlibs}

Le informazioni essenziali sulle funzioni per gli sviluppatori identificano le clientlib richieste.

Inoltre, da un&#39;istanza AEM, naviga fino al [Guida ai componenti della community](/help/communities/components-guide.md) fornisce l’accesso a un elenco di categorie clientlib richieste per un componente.

Ad esempio, nella parte superiore della [Pagina Recensioni](https://localhost:4502/content/community-components/en/reviews.html) le clientlibs richieste elencate sono

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Aggiunta di clientlibs richiesti {#adding-required-clientlibs}

Se desideri aggiungere un componente Community a una pagina, dovrai aggiungere le clientlib richieste per il componente, se non già presenti.

Utilizzo [CRXDE|Lite](#using-crxde-lite) per modificare un elenco clientlibslist esistente per una pagina del sito community.

Per aggiungere una clientlib per un sito della community utilizzando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Sfoglia per [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Individua il `clientlibslist` nodo della pagina in cui desideri aggiungere il componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con `clientlibslist` nodo selezionato:

   * Individua la stringa[] property `scg:requiredClientLibs`.
   * Seleziona i relativi `Value` per accedere alla finestra di dialogo Array di stringa.

      * Se necessario, scorri verso il basso.
      * Seleziona + per immettere una nuova libreria client.

         * Ripeti questa operazione per aggiungere altre librerie client.

         * Seleziona **OK**.
   * Seleziona **Salva tutto**.


>[!NOTE]
>
>Se il sito non è un sito community, è necessario individuare l’esistenza o la posizione delle librerie client in uso per il sito.

Utilizzo della [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md) esempio, dove `site-name` è *coinvolgere*, questo è il modo in cui apparirebbe la clientliblist se si aggiungesse il componente recensioni:

![componente di revisione](assets/review-component.png)
