---
title: Aggiungi commento alla pagina di esempio
description: Scopri come un’istanza del sistema di commenti di un sito web deve impostare resourceType come sistema di commenti personalizzato e includere tutte le librerie client necessarie.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Aggiungi commento alla pagina di esempio  {#add-comment-to-sample-page}

Ora che i componenti per il sistema di commenti personalizzato sono presenti nella directory dell’applicazione (/apps), è possibile utilizzare il componente esteso. L’istanza del sistema di commenti in un sito web interessato deve impostare resourceType come sistema di commenti personalizzato e includere tutte le librerie client necessarie.

## Identificare le clientlibs richieste {#identify-required-clientlibs}

Per i commenti estesi sono necessarie anche le librerie client necessarie per lo stile e il funzionamento dei commenti predefiniti.

La [Guida ai componenti della community](/help/communities/components-guide.md) identifica le librerie client richieste. Passa alla Guida dei componenti e visualizza il componente Commenti, ad esempio:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Nota le tre librerie client necessarie per il rendering e il funzionamento corretto di Commenti. Devono essere inclusi nel punto in cui si fa riferimento ai commenti estesi e nella libreria client di [commenti estesi](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![commenti-componente1](assets/comments-component1.png)

### Aggiungere commenti personalizzati a una pagina {#add-custom-comments-to-a-page}

Poiché può esistere un solo sistema di commenti per pagina, è più semplice creare una pagina di esempio come descritto nel breve tutorial [creare una pagina di esempio](/help/communities/create-sample-page.md).

Dopo la creazione, entra in modalità Progettazione e rende disponibile il gruppo di componenti personalizzati per consentire l&#39;aggiunta del componente `Alt Comments` alla pagina.

Affinché il commento venga visualizzato e funzioni correttamente, le librerie client per i commenti devono essere aggiunte all&#39;elenco clientlibslist della pagina (vedi [Clientlibs per i componenti Communities](/help/communities/clientlibs.md)).

#### Commenti Clientlibs sulla pagina di esempio {#comments-clientlibs-on-sample-page}

![commenti-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Autore: commento alternativo sulla pagina di esempio {#author-alt-comment-on-sample-page}

![alt-commento](assets/alt-comment.png)

#### Autore: nodo commenti pagina di esempio {#author-sample-page-comments-node}

È possibile verificare il resourceType in CRXDE visualizzando le proprietà del nodo dei commenti per la pagina di esempio in `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Pagina di esempio Publish {#publish-sample-page}

Dopo aver aggiunto il componente personalizzato alla pagina, è necessario (ri) [pubblicare la pagina](/help/communities/sites-console.md#publishing-the-site).

#### Publish: commento Alt sulla pagina di esempio {#publish-alt-comment-on-sample-page}

Dopo aver pubblicato sia l’applicazione personalizzata che la pagina di esempio, è possibile immettere un commento. Una volta effettuato l&#39;accesso, con un [utente demo](/help/communities/tutorials.md#demo-users) o amministratore, è possibile pubblicare un commento.

Pubblicando un commento su aaron.mcdonald@mailinator.com :

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Ora che il componente esteso funziona correttamente con l&#39;aspetto di default, è necessario modificare l&#39;aspetto.
