---
title: Tendenze attività
seo-title: Tendenze attività
description: Aggiunta di un componente Elenco attività community a una pagina
seo-description: Aggiunta di un componente Elenco attività community a una pagina
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---


# Tendenze attività {#activity-trends}

## Introduzione {#introduction}

Il componente `Community Activity List` consente di aggiungere informazioni di tendenza relative a post e visualizzazioni da parte dei membri, nonché a post e visualizzazioni di contenuto.

Il documento descrive:

* Aggiunta del componente `Community Activity List` a un [sito community](/help/communities/overview.md#community-sites).

* Impostazioni di configurazione per il componente `Community Activity List`.

### Requisito {#requirement}

I dati per `Community Activity List` sono disponibili solo se  Adobe Analytics è concesso in licenza e configurato per il sito della community.

Consultate [Analytics Configuration for Communities Features](/help/communities/analytics.md).

### Aggiunta di un elenco di attività community a una pagina {#adding-a-community-activity-list-to-a-page}

Per aggiungere un componente `Community Activity List` a una pagina in modalità di creazione, individuare il componente

* `Communities / Community Activity List`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visitare [Community Components Basics](/help/communities/basics.md).

La prima volta che il componente viene inserito in una pagina di un sito community, viene visualizzato così:

![attività della comunità](assets/community-activity.png)

### Configurazione dell&#39;elenco delle attività della community {#configuring-community-activity-list}

Selezionare il componente `Community Activity List` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

Nella scheda **Commenti**, specificate se e come vengono visualizzati i commenti per i file caricati:

![proprietà](assets/activity-list-properties.png)

* **Tipo**

   Specificate se visualizzare i dati relativi ai membri della community o al contenuto generato dall&#39;utente (UGC).

   Seleziona da:

   * `Members`
   * `Content`

   Il valore predefinito è `Members`.

* **Titolo da visualizzare**

   Titolo descrittivo da visualizzare sopra i dati, ad esempio `Trending Content`.
Il valore predefinito non è un titolo.

* **Numero di visualizzazioni**

   Numero di elementi da elencare.
Il valore predefinito è 10.

* **Tipo di attività**

   Selezionate una delle seguenti opzioni:

   * `Views`(visite alle pagine)
   * `Posts`(creazione di UGC)
   * `Follows`
   * `Likes`

   Il valore predefinito è Visualizzazioni.

* **Periodo di tempo**

   Selezionate una delle seguenti opzioni:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   Il valore predefinito è `Total`.

* **Percorso contesto**

   Fornisce la possibilità di estendere l&#39;attività a un sottoinsieme del sito, ad esempio un Blog specifico.
Default è l&#39;intero sito della community.

* **Aggregazione conteggio dei membri**

   Quando è deselezionato (disattivato), vengono contati solo i post di primo livello. Ad esempio, se il contesto è la pagina principale (impostazione predefinita), un `Activity Type` di `Posts` non mostrerà mai alcuna attività in quanto non è possibile pubblicare contenuto nella pagina principale. Se questa opzione è selezionata, vengono inclusi i conteggi di tutte le pagine discendenti.
Il valore predefinito è selezionato.

### Pagina di esempio con 4 componenti {#example-page-with-components}

**Top** Visitorsconfig: Tipo = Membri, Tipo di attività = Viste

**Top** Contributorsconfig: Tipo = Membri, Tipo di attività = Post

**Top** Contentconfig: Tipo = Contenuto, Tipo di attività = Viste,

**Tendenza** Contentconfig: Tipo = Contenuto, Tipo di attività = Post

![components](assets/activity-list-components.png)

