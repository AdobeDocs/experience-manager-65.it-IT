---
title: Componenti Clientlibs for Communities
seo-title: Componenti Clientlibs for Communities
description: Librerie lato client per Communities
seo-description: Librerie lato client per Communities
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
source-wordcount: '390'
ht-degree: 0%

---

# Componenti Clientlibs for Communities {#clientlibs-for-communities-components}

## Introduzione {#introduction}

Questa sezione della documentazione descrive come aggiungere librerie lato client (clientlibs) a una pagina per i componenti di Communities.

Per informazioni di base, visita :

* [Utilizzo delle ](/help/sites-developing/clientlibs.md) librerie lato client per informazioni sull’utilizzo e per strumenti di debug
* [Clientlibs per ](/help/communities/client-customize.md#clientlibs) SCF che fornisce informazioni utili durante la personalizzazione dei componenti SCF


## Perché sono necessarie le clientlibs {#why-clientlibs-are-required}

Le librerie client sono necessarie per il corretto funzionamento (JavaScript) e lo stile (CSS) di un componente.

Quando esiste una [funzione community](/help/communities/functions.md) per una funzione, tutti i componenti e le configurazioni necessarie, incluse le clientlib richieste, saranno presenti nel sito della community. Solo se gli autori devono disporre di componenti aggiuntivi, è necessario aggiungere ulteriori clientlibs.

Se mancano le clientlib richieste, l&#39;aggiunta di un componente Communities a una pagina](/help/communities/author-communities.md) potrebbe causare errori javascript e un aspetto imprevisto.[

### Esempio : Recensioni posizionate senza Clientlibs {#example-placed-reviews-without-clientlibs}

![valutazioni inserite](assets/placed-reviews.png)

### Esempio : Recensioni inserite con Clientlibs {#example-placed-reviews-with-clientlibs}

![recensioni-clientlibs](assets/reviews-clientlibs.png)

## Identificazione delle librerie client richieste {#identifying-required-clientlibs}

Le informazioni essenziali sulle funzioni per gli sviluppatori identificano le clientlib richieste.

Inoltre, da un&#39;istanza AEM, la navigazione alla [Guida ai componenti della community](/help/communities/components-guide.md) fornisce l&#39;accesso a un elenco delle categorie clientlib richieste per un componente.

Ad esempio, nella parte superiore della [Pagina recensioni](https://localhost:4502/content/community-components/en/reviews.html) le clientlibs richieste sono elencate

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Aggiunta di clientlibs richiesti {#adding-required-clientlibs}

Se desideri aggiungere un componente Community a una pagina, dovrai aggiungere le clientlib richieste per il componente, se non già presenti.

Utilizza [CRXDE|Lite](#using-crxde-lite) per modificare un elenco di clientlibslist esistente per una pagina del sito community.

Per aggiungere una clientlib per un sito community utilizzando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Vai a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Individua il nodo `clientlibslist` della pagina in cui desideri aggiungere il componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con il nodo `clientlibslist` selezionato:

   * Individua la proprietà String[] `scg:requiredClientLibs` .
   * Selezionare la relativa `Value` per accedere alla finestra di dialogo Array String.

      * Se necessario, scorri verso il basso.
      * Seleziona + per immettere una nuova libreria client.

         * Ripeti questa operazione per aggiungere altre librerie client.

         * Selezionare **OK**.
   * Selezionare **Salva tutto**.


>[!NOTE]
>
>Se il sito non è un sito community, è necessario individuare l’esistenza o la posizione delle librerie client in uso per il sito.

Utilizzando l&#39;esempio [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md), dove `site-name` è *coinvolgi*, questo è il modo in cui apparirebbe la lista clientliblist se si aggiunge il componente recensioni:

![componente di revisione](assets/review-component.png)
