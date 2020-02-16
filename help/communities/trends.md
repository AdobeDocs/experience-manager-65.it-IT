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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Tendenze attività{#activity-trends}

## Introduzione {#introduction}

Il `Community Activity List` componente consente di aggiungere informazioni di tendenza relative ai post e alle viste dei membri, nonché ai post e alle viste dei contenuti.

Il documento descrive:

* aggiunta del `Community Activity List` componente a un sito [community](/help/communities/overview.md#community-sites)

* impostazioni di configurazione per il `Community Activity List` componente

### Requisito {#requirement}

I dati per il sito `Community Activity List` sono disponibili solo se Adobe Analytics è concesso in licenza e configurato per il sito della community.

Consultate Configurazione [di Analytics per le funzioni](/help/communities/analytics.md)Community.

### Aggiunta di un elenco di attività community a una pagina {#adding-a-community-activity-list-to-a-page}

Per aggiungere un `Community Activity List` componente a una pagina in modalità di creazione, individuare il componente

* `Communities / Community Activity List`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visita [Community Components Basics](/help/communities/basics.md).

La prima volta che il componente viene inserito in una pagina di un sito community, viene visualizzato così:

![chlimage_1-54](assets/chlimage_1-54.png)

### Configurazione dell&#39;elenco delle attività community {#configuring-community-activity-list}

Selezionate il `Community Activity List` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-55](assets/chlimage_1-55.png)

Nella scheda **Commenti **specificare se e come vengono visualizzati i commenti per i file caricati:

![chlimage_1-56](assets/chlimage_1-56.png)

* **Tipo**

   Specificate se visualizzare i dati relativi ai membri della community o al contenuto generato dall&#39;utente (UGC).

   Seleziona da

   * `Members`
   * `Content`
   Default is `Members`.

* **Titolo da visualizzare**

   Titolo descrittivo da visualizzare sopra i dati, ad esempio `Trending Content`.
Il valore predefinito non è un titolo.

* **Numero di visualizzazioni**

   Numero di elementi da elencare.
Il valore predefinito è 10.

* **Tipo di attività**

   Seleziona uno dei

   * `Views`(visite alle pagine)
   * `Posts`(creazione di UGC)
   * `Follows`
   * `Likes`
   Il valore predefinito è Visualizzazioni.

* **Periodo di tempo**

   Seleziona uno dei

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`
   Default is `Total`.

* **Percorso contesto**

   Fornisce la possibilità di estendere l&#39;attività a un sottoinsieme del sito, ad esempio un blog specifico.
Default è l&#39;intero sito della community.

* **Aggregazione conteggio dei membri**

   Quando è deselezionato (disattivato), vengono contati solo i post di primo livello. Ad esempio, se il contesto è la pagina principale (impostazione predefinita), una `Activity Type`di non `Posts`mostrerà mai alcuna attività in quanto non è possibile pubblicare contenuto nella pagina principale. Se questa opzione è selezionata, vengono inclusi i conteggi di tutte le pagine discendenti.
Il valore predefinito è selezionato.

### Pagina di esempio con 4 componenti {#example-page-with-components}

**Configurazione visitatori** principali: Tipo = Membri, Tipo di attività = Viste

**Configurazione collaboratori** principali: Tipo = Membri, Tipo di attività = Post

**Configurazione contenuto** principale: Tipo = Contenuto, Tipo di attività = Viste,

**Configurazione dei contenuti** di tendenza: Tipo = Contenuto, Tipo di attività = Post

![chlimage_1-57](assets/chlimage_1-57.png)

