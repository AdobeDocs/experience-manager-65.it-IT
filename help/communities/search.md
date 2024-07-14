---
title: Funzione di ricerca
description: Aggiunta e configurazione della ricerca in un sito community
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Funzione di ricerca {#search-feature}

La funzione di ricerca funziona con diverse altre funzioni, come i forum, per fornire la possibilità di cercare contenuti.

Quando si aggiunge la possibilità di cercare i post immessi dai membri della community, denominati contenuti generati dagli utenti (UGC, User Generated Content), sono disponibili due componenti: [Ricerca](#search) e [Risultati ricerca](#search-results).

La pagina che include il componente `Search Results` supporta sia la ricerca che la visualizzazione dei risultati.

La pagina che include il componente `Search` consente di avviare una ricerca con i risultati visualizzati nella pagina `Search Results`.

La funzione di ricerca può essere utilizzata con qualsiasi altra funzione che consenta ai visitatori e ai membri del sito di visualizzare il contenuto.

## Ricerca {#search-features}

### Aggiungere ricerca a una pagina {#add-search-to-a-page}

Per aggiungere un componente `Search` a una pagina in modalità di creazione, utilizzare il browser componenti per individuare `Communities / Search` e trascinarlo in posizione su una pagina. L&#39;utilizzo di `Search` richiede una seconda pagina per `Search Results.`

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando la libreria lato client richiesta, `cq.social.hbs.search`, è inclusa, il componente `Search` verrà visualizzato in questo modo.

![aggiungi-ricerca](assets/add-search.png)

### Configurare la ricerca aggiunta {#configure-the-added-search}

Seleziona il componente `Search` inserito a cui accedere e seleziona l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Nella scheda **[!UICONTROL Impostazioni ricerca]**, specifica in che modo vengono cercati i percorsi quando un visitatore immette una query.

![impostazioni di ricerca](assets/search-settings.png)

* **[!UICONTROL Percorsi di ricerca]**
Aggiungendo i percorsi di ricerca tramite il pulsante Aggiungi elemento, la ricerca del contenuto è limitata. Ad esempio, per limitare la ricerca a un forum specifico, seleziona un componente forum all’interno di una pagina:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Pagina dei risultati]**
I risultati verranno visualizzati in una pagina separata specificata utilizzando il browser per selezionare una pagina contenente il componente `Search Results`.

## Risultati di ricerca {#search-results}

### Aggiungere risultati di ricerca a una pagina {#add-search-results-to-a-page}

Per aggiungere un componente `Search Results` a una pagina in modalità di creazione, utilizza il browser componenti per individuare

* `Communities / Search Results`

e trascinarlo nella posizione desiderata su una pagina. A differenza del componente Ricerca, non è necessaria una seconda pagina, in quanto i risultati vengono visualizzati sulla stessa pagina.

Se si utilizza Cerca in un altro punto del sito Web, questa pagina con `Search Results` può essere configurata come `Result Page` per una o tutte le istanze di `Search`.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando la libreria lato client richiesta, `cq.social.hbs.search`, è inclusa, il componente `Search Result` verrà visualizzato in questo modo:

![risultato ricerca](assets/search-result1.png)

### Configurare i risultati di ricerca aggiunti {#configure-the-added-search-result}

Seleziona il componente `Search Results` inserito a cui accedere e seleziona l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Nella scheda **[!UICONTROL Impostazioni risultati ricerca]** è possibile specificare i percorsi inclusi nella ricerca quando un visitatore immette una query.

![impostazioni-risultati-ricerca](assets/search-result-settings.png)

* **[!UICONTROL Risultati di ricerca per pagina]**

  Definisci il numero di topic/post mostrati per pagina. Il valore predefinito è 10.

* **[!UICONTROL Percorsi di ricerca]**

  Aggiungendo i percorsi di ricerca tramite il pulsante Aggiungi elemento, la ricerca del contenuto è limitata.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Search Essentials](search-implementation.md) per sviluppatori.
