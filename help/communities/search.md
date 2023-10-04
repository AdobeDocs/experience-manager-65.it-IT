---
title: Funzione di ricerca
description: Aggiunta e configurazione della ricerca in un sito community
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Funzione di ricerca {#search-feature}

La funzione di ricerca funziona con diverse altre funzioni, come i forum, per fornire la possibilità di cercare contenuti.

Quando si aggiunge la possibilità di cercare i post inseriti dai membri della community, denominati contenuti generati dagli utenti (UGC, User Generated Content), sono disponibili due componenti: [Ricerca](#search) e [Risultati di ricerca](#search-results).

La pagina che include `Search Results` il componente supporta sia la ricerca che la visualizzazione dei risultati.

La pagina che include `Search` fornisce una posizione in cui avviare una ricerca con i risultati visualizzati sul `Search Results` pagina.

La funzione di ricerca può essere utilizzata con qualsiasi altra funzione che consenta ai visitatori e ai membri del sito di visualizzare il contenuto.

## Ricerca {#search-features}

### Aggiungere ricerca a una pagina {#add-search-to-a-page}

Per aggiungere una `Search` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare `Communities / Search` e trascinarlo nella posizione desiderata su una pagina. Uso di `Search` richiede una seconda pagina per `Search Results.`

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando la libreria lato client richiesta, `cq.social.hbs.search`, è incluso, ecco come `Search` verrà visualizzato.

![add-search](assets/add-search.png)

### Configurare la ricerca aggiunta {#configure-the-added-search}

Seleziona la inserita `Search` per accedere e selezionare il `Configure` che apre la finestra di dialogo per modifica.

![confondere](assets/configure-new.png)

Sotto **[!UICONTROL Impostazioni di ricerca]** , specifica in che modo vengono cercati i percorsi quando un visitatore inserisce una query.

![search-settings](assets/search-settings.png)

* **[!UICONTROL Percorsi di ricerca]**
Aggiungendo i percorsi di ricerca tramite il pulsante Aggiungi elemento, la ricerca del contenuto è limitata. Ad esempio, per limitare la ricerca a un forum specifico, seleziona un componente forum all’interno di una pagina:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Pagina dei risultati]**
I risultati verranno visualizzati in una pagina separata specificata utilizzando il browser per selezionare una pagina contenente `Search Results` componente.

## Risultati di ricerca {#search-results}

### Aggiungere risultati di ricerca a una pagina {#add-search-results-to-a-page}

Per aggiungere una `Search Results` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Search Results`

e trascinarlo nella posizione desiderata su una pagina. A differenza del componente Ricerca, non è necessaria una seconda pagina, in quanto i risultati vengono visualizzati sulla stessa pagina.

Se utilizzi Cerca altrove nel sito web, questa pagina con `Search Results` può essere configurato per essere `Result Page` per tutte le istanze di `Search`.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando la libreria lato client richiesta, `cq.social.hbs.search`, è incluso, ecco come `Search Result` Il componente verrà visualizzato:

![risultato di ricerca](assets/search-result1.png)

### Configurare i risultati di ricerca aggiunti {#configure-the-added-search-result}

Seleziona la inserita `Search Results` per accedere e selezionare il `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Sotto **[!UICONTROL Impostazioni risultati di ricerca]** , è possibile specificare quali percorsi vengono inclusi nella ricerca quando una query viene immessa da un visitatore.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Risultati di ricerca per pagina]**

  Definisci il numero di topic/post mostrati per pagina. Il valore predefinito è 10.

* **[!UICONTROL Percorsi di ricerca]**

  Aggiungendo i percorsi di ricerca tramite il pulsante Aggiungi elemento, la ricerca del contenuto è limitata.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Search Essentials](search-implementation.md) pagina per sviluppatori.
