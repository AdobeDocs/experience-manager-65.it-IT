---
title: Aggiungi commento a pagina di esempio
seo-title: Aggiungi commento a pagina di esempio
description: Aggiunta di commenti personalizzati a una pagina
seo-description: Aggiunta di commenti personalizzati a una pagina
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Aggiungi commento a pagina di esempio {#add-comment-to-sample-page}

Ora che i componenti per il sistema di commenti personalizzato sono presenti nella directory dell&#39;applicazione (/apps), è possibile utilizzare il componente esteso. L’istanza del sistema di commenti in un sito Web da modificare deve impostare resourceType come sistema di commenti personalizzato e includere tutte le librerie client necessarie.

## Identifica ClientLibs Richiesti {#identify-required-clientlibs}

Le librerie client necessarie per lo stile e il funzionamento dei commenti predefiniti sono necessarie anche per i commenti estesi.

La Guida ai componenti [della](/help/communities/components-guide.md) community identifica le librerie client richieste. Passare alla Guida ai componenti e visualizzare il componente Commenti, ad esempio:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Tenere presenti le tre librerie client necessarie affinché Commenti possa eseguire correttamente il rendering e il funzionamento. Devono essere inclusi dove si fa riferimento ai commenti estesi e nella libreria [client dei commenti](/help/communities/extend-create-components.md#create-a-client-library-folder) estesi ( `apps.custom.comments`).

![chlimage_1-79](assets/chlimage_1-79.png)

### Aggiunta di commenti personalizzati a una pagina {#add-custom-comments-to-a-page}

Poiché per ogni pagina può essere presente un solo sistema di commenti, è più semplice creare una pagina di esempio come descritto nella breve esercitazione [Crea una pagina](/help/communities/create-sample-page.md) di esempio.

Una volta creato, entrate in modalità Progettazione e rendete disponibile il gruppo di componenti Personalizzato per consentire l’aggiunta del `Alt Comments` componente alla pagina.

Affinché il commento venga visualizzato e funzioni correttamente, è necessario aggiungere le librerie client per i commenti all&#39;elenco clientlibslist della pagina (vedere [Clientlibs for Communities Components](/help/communities/clientlibs.md)).

#### Commenti Clientlibs sulla pagina di esempio {#comments-clientlibs-on-sample-page}

![Commenti Clientlibs sulla pagina di esempio](assets/chlimage_1-80.png)

#### Autore: Commento Alt sulla pagina di esempio {#author-alt-comment-on-sample-page}

![Commento Alt sulla pagina di esempio](assets/chlimage_1-81.png)

#### Autore: Nodo commenti pagina di esempio {#author-sample-page-comments-node}

È possibile verificare resourceType in CRXDE visualizzando le proprietà del nodo dei commenti per la pagina di esempio in `/content/sites/sample/en/jcr:content/content/primary/comments`.

![chlimage_1-82](assets/chlimage_1-82.png)

#### Pubblica pagina di esempio {#publish-sample-page}

Dopo che il componente personalizzato è stato aggiunto alla pagina, è necessario anche (ri) [pubblicare la pagina](/help/communities/sites-console.md#publishing-the-site).

#### Pubblica: Commento Alt sulla pagina di esempio {#publish-alt-comment-on-sample-page}

Dopo aver pubblicato l&#39;applicazione personalizzata e la pagina di esempio, è possibile inserire un commento. Una volta effettuato l’accesso, con un utente [](/help/communities/tutorials.md#demo-users) dimostrativo o un amministratore, è possibile pubblicare un commento.

Di seguito è riportato aaron.mcdonald@mailinator.com di un commento:

![chlimage_1-83](assets/chlimage_1-83.png) ![chlimage_1-84](assets/chlimage_1-84.png)

Ora che il componente esteso funziona correttamente con l’aspetto predefinito, è ora di modificare l’aspetto.