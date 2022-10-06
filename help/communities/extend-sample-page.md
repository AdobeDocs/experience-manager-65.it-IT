---
title: Aggiungi commento alla pagina di esempio
seo-title: Add Comment to Sample Page
description: Aggiungere commenti personalizzati a una pagina
seo-description: Add Custom Comments to a page
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Aggiungi commento alla pagina di esempio  {#add-comment-to-sample-page}

Ora che i componenti del sistema di commento personalizzato sono presenti nella directory dell&#39;applicazione (/apps), è possibile utilizzare il componente esteso. L&#39;istanza del sistema di commenti in un sito Web da modificare deve impostare resourceType come sistema di commenti personalizzato e includere tutte le librerie client necessarie.

## Identificare le clientlib richieste {#identify-required-clientlibs}

Le librerie client necessarie per lo stile e il funzionamento dei commenti predefiniti sono necessarie anche per i commenti estesi.

La [Guida ai componenti della community](/help/communities/components-guide.md) identifica le librerie client richieste. Accedi alla Guida dei componenti e visualizza il componente Commenti , ad esempio:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Tieni presente le tre librerie client necessarie affinché Commenti possa eseguire correttamente il rendering e il funzionamento di . Questi dovranno essere inclusi nei casi in cui si fa riferimento ai commenti estesi, e [libreria client di commenti esteso](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Aggiungere commenti personalizzati a una pagina {#add-custom-comments-to-a-page}

Poiché può esistere un solo sistema di commento per pagina, è più semplice creare una pagina di esempio come descritto nel breve [Creare una pagina di esempio](/help/communities/create-sample-page.md) esercitazione.

Una volta creato, entra in modalità Progettazione e rende disponibile il gruppo di componenti Personalizzato per consentire al `Alt Comments` da aggiungere alla pagina.

Affinché il Commento appaia e funzioni correttamente, è necessario aggiungere le librerie client per Commenti all’elenco delle clientlibslist per la pagina (consulta [Componenti Clientlibs for Communities](/help/communities/clientlibs.md)).

#### Commenti Clientlibs sulla pagina di esempio {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Autore: Commento Alt sulla pagina di esempio {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Autore: Nodo dei commenti della pagina di esempio {#author-sample-page-comments-node}

Puoi verificare resourceType in CRXDE visualizzando le proprietà del nodo dei commenti per la pagina di esempio in `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Pubblica pagina di esempio {#publish-sample-page}

Dopo aver aggiunto il componente personalizzato alla pagina, è necessario anche (ri) [pubblicare la pagina](/help/communities/sites-console.md#publishing-the-site).

#### Pubblica: Commento Alt sulla pagina di esempio {#publish-alt-comment-on-sample-page}

Dopo aver pubblicato sia l’applicazione personalizzata che la pagina di esempio, è possibile inserire un commento. Al momento dell’accesso, con un [utente dimostrativo](/help/communities/tutorials.md#demo-users) o amministratore, è possibile pubblicare un commento.

Ecco aaron.mcdonald@mailinator.com un commento:

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Ora che sembra che il componente esteso funzioni correttamente con l’aspetto predefinito, è il momento di modificare l’aspetto.
