---
title: Tendenze attività
seo-title: Activity Trends
description: Aggiunta di un componente Elenco attività community a una pagina
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

# Tendenze attività {#activity-trends}

## Introduzione {#introduction}

Il `Community Activity List` Questo componente consente di aggiungere informazioni sulle tendenze relative a post e visualizzazioni dei membri, nonché a post e visualizzazioni di contenuti.

Il documento descrive:

* Aggiunta di `Community Activity List` da componente a [sito community](/help/communities/overview.md#community-sites).

* Impostazioni di configurazione per `Community Activity List` componente.

### Requisito {#requirement}

Dati per `Community Activity List` è disponibile solo quando Adobe Analytics è concesso in licenza e configurato per il sito community.

Consulta [Configurazione di Analytics per le funzioni di Communities](/help/communities/analytics.md).

### Aggiunta di un elenco di attività community a una pagina {#adding-a-community-activity-list-to-a-page}

Per aggiungere una `Community Activity List` a una pagina in modalità di authoring, individua il componente

* `Communities / Community Activity List`

e trascinarlo nella posizione desiderata su una pagina.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](/help/communities/basics.md).

La prima volta che viene inserito in una pagina di un sito community, viene visualizzato questo componente:

![attività della community](assets/community-activity.png)

### Configurazione dell’elenco attività community  {#configuring-community-activity-list}

Seleziona la inserita `Community Activity List` per accedere e selezionare il `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Sotto **Commenti** , specifica se e come vengono visualizzati i commenti per i file caricati:

![proprietà](assets/activity-list-properties.png)

* **Tipo**

   Specifica se visualizzare i dati relativi ai membri della community o ai contenuti generati dagli utenti (UGC, User-Generated Content).

   Seleziona da:

   * `Members`
   * `Content`

   Il valore predefinito è `Members`.

* **Titolo da visualizzare**

   Titolo descrittivo da visualizzare sopra i dati, ad esempio `Trending Content`.
Il valore predefinito non è un titolo.

* **Numero di visualizzazioni**

   Il numero di elementi da elencare.
Il valore predefinito è 10.

* **Tipo di attività**

   Seleziona una delle seguenti opzioni:

   * `Views`(visite alle pagine)
   * `Posts`(creazione UGC)
   * `Follows`
   * `Likes`

   L&#39;impostazione predefinita è Viste.

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

   Consente di eseguire l’ambito dell’attività in un sottoinsieme del sito, ad esempio un blog specifico.
L&#39;impostazione predefinita corrisponde all&#39;intero sito community.

* **Aggregazione conteggio dei membri**

   Se è deselezionato (disattivato), vengono conteggiati solo i post di livello superiore. Ad esempio, se il contesto è la pagina principale (impostazione predefinita), allora un `Activity Type` di `Posts` non mostrerà mai alcuna attività, in quanto non è possibile pubblicare contenuti sulla pagina principale. Se questa opzione è selezionata, vengono inclusi i conteggi su tutte le pagine discendenti.
Il valore predefinito è selezionato.

### Pagina di esempio con 4 componenti {#example-page-with-components}

**Visitatori principali** config: Type = Membri, Activity type = Viste

**Collaboratori principali** config: Tipo = Membri, Tipo di attività = Post

**Contenuto principale** config: Type = Content, Activity type = Views,

**Contenuto di tendenza** config: Type = Contenuto, Activity type = Post

![componenti](assets/activity-list-components.png)
