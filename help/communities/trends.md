---
title: Tendenze attività
description: Aggiunta di un componente Elenco attività community a una pagina
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# Tendenze attività {#activity-trends}

## Introduzione {#introduction}

Il componente `Community Activity List` consente di aggiungere informazioni sulle tendenze relative a post e visualizzazioni per membri e post e visualizzazioni di contenuto.

Il documento descrive:

* Aggiunta del componente `Community Activity List` a un [sito community](/help/communities/overview.md#community-sites).

* Impostazioni di configurazione per il componente `Community Activity List`.

### Requisito {#requirement}

I dati per `Community Activity List` sono disponibili solo quando Adobe Analytics è concesso in licenza e configurato per il sito community.

Consulta [Configurazione di Analytics per le funzionalità delle community](/help/communities/analytics.md).

### Aggiunta di un elenco di attività community a una pagina {#adding-a-community-activity-list-to-a-page}

Per aggiungere un componente `Community Activity List` a una pagina in modalità di creazione, individuare il componente `Communities / Community Activity List` e trascinarlo nella posizione desiderata in una pagina.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](/help/communities/basics.md).

La prima volta che viene inserito in una pagina di un sito community, viene visualizzato questo componente:

![attività-community](assets/community-activity.png)

### Configurazione dell’elenco attività community  {#configuring-community-activity-list}

Seleziona il componente `Community Activity List` inserito, quindi fai clic sull&#39;icona `Configure` per aprire la finestra di dialogo di modifica.

![configura](assets/configure-new.png)

Nella scheda **Commenti**, specifica se e come vengono visualizzati i commenti per i file caricati:

![proprietà](assets/activity-list-properties.png)

* **Tipo**

  Specifica se visualizzare i dati relativi ai membri della community o ai contenuti generati dagli utenti (UGC, User-Generated Content).

  Seleziona da:

   * `Members`
   * `Content`

  Il valore predefinito è `Members`.

* **Titolo visualizzato**

  Titolo descrittivo da visualizzare sopra i dati, ad esempio `Trending Content`.
Il valore predefinito non è un titolo.

* **Conteggio visualizzazioni**

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
   * `This year (since Jan 1)`
   * `Total`

  Il valore predefinito è `Total`.

* **Percorso contesto**

  Questo consente di eseguire l’ambito dell’attività in un sottoinsieme del sito, ad esempio un blog specifico.
L&#39;impostazione predefinita corrisponde all&#39;intero sito community.

* **Aggregazione conteggio membri**

  Se è deselezionato (disattivato), vengono conteggiati solo i post di livello superiore. Ad esempio, se il contesto è la pagina principale (impostazione predefinita), un `Activity Type` di `Posts` non mostra mai alcuna attività, in quanto non è possibile pubblicare contenuti nella pagina principale. Se questa opzione è selezionata, vengono inclusi i conteggi su tutte le pagine discendenti.
Il valore predefinito è selezionato.

### Pagina di esempio con quattro componenti {#example-page-with-components}

Configurazione **Visitatori principali**: Tipo = Membri, Tipo attività = Viste

**Configurazione collaboratori principali**: Tipo = Membri, Tipo attività = Post

**Configurazione contenuto principale**: Tipo = Contenuto, Tipo attività = Visualizzazioni,

**Configurazione contenuto di tendenza**: Tipo = Contenuto, Tipo attività = Post

![componenti](assets/activity-list-components.png)
