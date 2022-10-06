---
title: Tendenze delle attività
seo-title: Activity Trends
description: Aggiunta di un componente Elenco attività della community a una pagina
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# Tendenze delle attività {#activity-trends}

## Introduzione {#introduction}

La `Community Activity List` Il componente consente di aggiungere informazioni di tendenza relative a post e visualizzazioni per membri, nonché a post e visualizzazioni di contenuto.

Il documento descrive:

* Aggiunta di `Community Activity List` a un [sito della community](/help/communities/overview.md#community-sites).

* Impostazioni di configurazione per `Community Activity List` componente.

### Requisito {#requirement}

Dati per `Community Activity List` è disponibile solo quando Adobe Analytics è concesso in licenza e configurato per il sito della community.

Vedi [Funzionalità di configurazione di Analytics for Communities](/help/communities/analytics.md).

### Aggiunta di un elenco di attività della community a una pagina {#adding-a-community-activity-list-to-a-page}

Per aggiungere una `Community Activity List` in una pagina in modalità di authoring, individua il componente

* `Communities / Community Activity List`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando viene posizionato per la prima volta su una pagina di un sito della community, viene visualizzato questo componente:

![attività della comunità](assets/community-activity.png)

### Configurazione dell’elenco delle attività della community  {#configuring-community-activity-list}

Seleziona il `Community Activity List` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

Sotto la **Commenti** scheda , specifica se e come vengono visualizzati i commenti per i file caricati:

![proprietà](assets/activity-list-properties.png)

* **Tipo**

   Specifica se visualizzare i dati relativi ai membri della community o al contenuto generato dall’utente (UGC).

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

   Seleziona una delle seguenti opzioni:

   * `Views`(visite alle pagine)
   * `Posts`(creazione di UGC)
   * `Follows`
   * `Likes`

   Il valore predefinito è Visualizzazioni.

* **Periodo di tempo**

   Seleziona una delle seguenti opzioni:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   Il valore predefinito è `Total`.

* **Percorso contesto**

   Consente di estendere l’ambito dell’attività a un sottoinsieme del sito, ad esempio a un Blog specifico.
L&#39;impostazione predefinita è l&#39;intero sito della community.

* **Aggregazione conteggio dei membri**

   Quando è deselezionato (disattivato), vengono conteggiati solo i post di primo livello. Ad esempio, se il contesto è la pagina principale (l’impostazione predefinita), un `Activity Type` di `Posts` non mostrerà mai alcuna attività in quanto non è possibile pubblicare contenuto nella pagina principale. Quando questa opzione è selezionata, vengono inclusi i conteggi di tutte le pagine discendenti.
Il valore predefinito è selezionato.

### Pagina di esempio con 4 componenti {#example-page-with-components}

**Visitatori principali** config: Tipo = Membri, Tipo di attività = Viste

**Collaboratori principali** config: Tipo = Membri, Tipo di attività = Posti

**Contenuto principale** config: Tipo = Contenuto, tipo di attività = Viste,

**Contenuto di tendenza** config: Tipo = Contenuto, tipo di attività = Posts

![componenti](assets/activity-list-components.png)
