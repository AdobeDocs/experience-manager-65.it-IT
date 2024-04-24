---
title: Clientlibs per i componenti Communities
description: Scopri come aggiungere librerie client-side (clientlibs) a una pagina per raccogliere i dettagli sull’utilizzo e utilizzare gli strumenti di debug per i componenti di Communities.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Clientlibs per i componenti Communities {#clientlibs-for-communities-components}

## Introduzione {#introduction}

Questa sezione della documentazione descrive come aggiungere librerie client (clientlibs) a una pagina per i componenti Communities.

Per informazioni di base, vedere:

* [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md) che fornisce dettagli sull’utilizzo e strumenti di debug
* [Clientlibs per SCF](/help/communities/client-customize.md#clientlibs) che fornisce informazioni utili per personalizzare i componenti SCF


## Perché sono richieste le clientlibs {#why-clientlibs-are-required}

Le clientlibs sono necessarie per il corretto funzionamento (JavaScript) e lo stile (CSS) di un componente.

Quando esiste un [funzione community](/help/communities/functions.md) per una funzione, tutti i componenti e le configurazioni necessari, comprese le clientlibs richieste, sono presenti nel sito community. Solo se gli autori devono disporre di componenti aggiuntivi, è necessario aggiungere altre clientlibs.

Quando mancano le clientlibs richieste, [aggiunta di un componente Communities a una pagina](/help/communities/author-communities.md) potrebbe causare errori JavaScript e un aspetto imprevisto.

### Esempio: revisioni posizionate senza clientlibs {#example-placed-reviews-without-clientlibs}

![places-review](assets/placed-reviews.png)

### Esempio: recensioni inserite con Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identificazione delle clientlibs richieste {#identifying-required-clientlibs}

Le informazioni essenziali sulle funzioni per gli sviluppatori identificano le clientlibs richieste.

Inoltre, da un’istanza dell’AEM, naviga nel [Guida ai componenti della community](/help/communities/components-guide.md) fornisce l’accesso a un elenco di categorie clientlib necessarie per un componente.

Ad esempio, nella parte superiore della sezione [Pagina Revisioni](https://localhost:4502/content/community-components/en/reviews.html) le clientlibs elencate sono

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Aggiunta di clientlibs richieste {#adding-required-clientlibs}

Quando si desidera aggiungere un componente Communities a una pagina, se non è già presente, è necessario aggiungere le clientlibs richieste per il componente.

Utilizzare [CRXDE|Lite](#using-crxde-lite) per modificare un elenco clientlibslist esistente per una pagina del sito community.

Per aggiungere una libreria client a un sito community tramite [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md):

* Sfoglia per [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Individua il `clientlibslist` per la pagina alla quale desideri aggiungere il componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con `clientlibslist` nodo selezionato:

   * Individua la stringa[] proprietà `scg:requiredClientLibs`.
   * Seleziona il relativo `Value` in modo da poter accedere alla finestra di dialogo Array di stringhe.

      * Scorri verso il basso, se necessario.
      * Seleziona + per immettere una nuova libreria client.

         * Ripeti l’operazione per aggiungere altre librerie client.

         * Seleziona **OK**.

   * Seleziona **Salva tutto**.

>[!NOTE]
>
>Se il sito non è un sito di community, è necessario individuare l&#39;esistenza o la posizione delle librerie client utilizzate per il sito.

Utilizzo di [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md) esempio, dove `site-name` è *coinvolgere*, questo è l’aspetto del clientliblist se si aggiunge il componente recensioni:

![review-component](assets/review-component.png)
