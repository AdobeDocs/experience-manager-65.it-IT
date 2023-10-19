---
title: Aggiungi commento alla pagina di esempio
description: Scopri come un’istanza del sistema di commenti di un sito web deve impostare resourceType come sistema di commenti personalizzato e includere tutte le librerie client necessarie.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Aggiungi commento alla pagina di esempio  {#add-comment-to-sample-page}

Ora che i componenti per il sistema di commenti personalizzato sono presenti nella directory dell’applicazione (/apps), è possibile utilizzare il componente esteso. L’istanza del sistema di commenti in un sito web interessato deve impostare resourceType come sistema di commenti personalizzato e includere tutte le librerie client necessarie.

## Identificare le clientlibs richieste {#identify-required-clientlibs}

Per i commenti estesi sono necessarie anche le librerie client necessarie per lo stile e il funzionamento dei commenti predefiniti.

Il [Guida ai componenti della community](/help/communities/components-guide.md) identifica le librerie client richieste. Passa alla Guida dei componenti e visualizza il componente Commenti, ad esempio:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Nota le tre librerie client necessarie per il rendering e il funzionamento corretto di Commenti. Devono essere incluse dove si fa riferimento ai commenti estesi e al [libreria client dei commenti estesi](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Aggiungere commenti personalizzati a una pagina {#add-custom-comments-to-a-page}

Poiché può esistere un solo sistema di commenti per pagina, è più semplice creare una pagina di esempio come descritto nella descrizione [creare una pagina di esempio](/help/communities/create-sample-page.md) esercitazione.

Una volta creato, entra in modalità Progettazione e rendi disponibile il gruppo di componenti Personalizzati per consentire al `Alt Comments` da aggiungere alla pagina.

Affinché il commento venga visualizzato e funzioni correttamente, le librerie client per i commenti devono essere aggiunte all’elenco clientlibslist della pagina (consulta [Clientlibs per i componenti Communities](/help/communities/clientlibs.md)).

#### Commenti Clientlibs sulla pagina di esempio {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Autore: commento alternativo sulla pagina di esempio {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Autore: nodo commenti pagina di esempio {#author-sample-page-comments-node}

Puoi verificare il resourceType in CRXDE visualizzando le proprietà del nodo dei commenti per la pagina di esempio in `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Pubblica pagina di esempio {#publish-sample-page}

Dopo aver aggiunto il componente personalizzato alla pagina, è anche necessario (ri) [pubblicare la pagina](/help/communities/sites-console.md#publishing-the-site).

#### Pubblicazione: commento alternativo nella pagina di esempio {#publish-alt-comment-on-sample-page}

Dopo aver pubblicato sia l’applicazione personalizzata che la pagina di esempio, è possibile immettere un commento. Una volta effettuato l’accesso, con [utente demo](/help/communities/tutorials.md#demo-users) o amministratore, è possibile pubblicare un commento.

Pubblicando un commento su aaron.mcdonald@mailinator.com :

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Ora che il componente esteso funziona correttamente con l&#39;aspetto di default, è necessario modificare l&#39;aspetto.
