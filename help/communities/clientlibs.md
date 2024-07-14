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

* [Utilizzo di librerie lato client](/help/sites-developing/clientlibs.md) che fornisce dettagli sull&#39;utilizzo e strumenti di debug
* [Clientlibs per SCF](/help/communities/client-customize.md#clientlibs) che fornisce informazioni utili per la personalizzazione dei componenti SCF


## Perché sono richieste le clientlibs {#why-clientlibs-are-required}

Le clientlibs sono necessarie per il corretto funzionamento (JavaScript) e per lo stile (CSS) di un componente.

Quando esiste una [funzione community](/help/communities/functions.md) per una caratteristica, tutti i componenti e le configurazioni necessari, incluse le clientlibs richieste, sono presenti nel sito della comunità. Solo se gli autori devono disporre di componenti aggiuntivi, è necessario aggiungere altre clientlibs.

Quando mancano le clientlibs richieste, [l&#39;aggiunta di un componente Communities a una pagina](/help/communities/author-communities.md) potrebbe causare errori JavaScript e un aspetto imprevisto.

### Esempio: revisioni posizionate senza clientlibs {#example-placed-reviews-without-clientlibs}

![revisioni effettuate](assets/placed-reviews.png)

### Esempio: recensioni inserite con Clientlibs {#example-placed-reviews-with-clientlibs}

![recensioni-clientlibs](assets/reviews-clientlibs.png)

## Identificazione delle clientlibs richieste {#identifying-required-clientlibs}

Le informazioni essenziali sulle funzioni per gli sviluppatori identificano le clientlibs richieste.

Inoltre, da un&#39;istanza AEM, la navigazione alla [Guida ai componenti della community](/help/communities/components-guide.md) consente di accedere a un elenco di categorie clientlib richieste per un componente.

Ad esempio, nella parte superiore della pagina [Recensioni](https://localhost:4502/content/community-components/en/reviews.html) sono elencate le clientlibs richieste

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-Reviews](assets/clientlibs-reviews.png)

## Aggiunta di clientlibs richieste {#adding-required-clientlibs}

Quando si desidera aggiungere un componente Communities a una pagina, se non è già presente, è necessario aggiungere le clientlibs richieste per il componente.

Utilizza [CRXDE|Lite](#using-crxde-lite) per modificare un elenco clientlibslist esistente per una pagina del sito community.

Per aggiungere una clientlib per un sito community utilizzando [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md):

* Passa a [https://&lt;server>:&lt;porta>/crx/de](https://localhost:4502/crx/de).
* Individua il nodo `clientlibslist` per la pagina in cui desideri aggiungere il componente:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Con `clientlibslist` nodo selezionato:

   * Individuare la proprietà String[] `scg:requiredClientLibs`.
   * Selezionare `Value` per accedere alla finestra di dialogo Array di stringhe.

      * Scorri verso il basso, se necessario.
      * Seleziona + per immettere una nuova libreria client.

         * Ripeti l’operazione per aggiungere altre librerie client.

         * Selezionare **OK**.

   * Seleziona **Salva tutto**.

>[!NOTE]
>
>Se il sito non è un sito di community, è necessario individuare l&#39;esistenza o la posizione delle librerie client utilizzate per il sito.

Utilizzando l&#39;esempio [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md), dove `site-name` è *coinvolgi*, questo è l&#39;aspetto del clientliblist se si aggiunge il componente recensioni:

![revisione-componente](assets/review-component.png)
