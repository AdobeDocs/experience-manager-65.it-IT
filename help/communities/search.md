---
title: Funzione di ricerca
seo-title: Funzione di ricerca
description: Aggiunta e configurazione della ricerca a un sito community
seo-description: Aggiunta e configurazione della ricerca a un sito community
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Funzione di ricerca {#search-feature}

La funzione di ricerca funziona con altre funzioni, come i forum, per consentire la ricerca di contenuti.

Quando si aggiunge la possibilità di cercare post inseriti dai membri della community, denominati contenuti generati dall&#39;utente (UGC), sono disponibili due componenti: [ `Search`](#search) e [ `Search Results`](#search-results).

La pagina che include il `Search Results` componente supporta sia la ricerca che la visualizzazione dei risultati.

La pagina che include il `Search`componente consente di avviare una ricerca con i risultati visualizzati sulla `Search Results` pagina.

La funzione di ricerca può essere utilizzata con qualsiasi altra funzione che consente ai visitatori e ai membri del sito di visualizzare il contenuto.

## Ricerca {#search-features}

### Aggiungere una ricerca a una pagina {#add-search-to-a-page}

Per aggiungere un `Search` componente a una pagina in modalità di creazione, usate il browser Componenti per individuarlo `Communities / Search` e trascinarlo nella posizione desiderata sulla pagina. L&#39;utilizzo di `Search` richiede una seconda pagina per `Search Results.`

Per le informazioni necessarie, visita [Community Components Basics](basics.md).

Quando la libreria lato client richiesta `cq.social.hbs.search`è inclusa, viene visualizzata così il `Search` componente.

![chlimage_1-373](assets/chlimage_1-373.png)

### Configurare la ricerca aggiunta {#configure-the-added-search}

Selezionate il `Search` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-374](assets/chlimage_1-374.png)

Nella scheda Impostazioni **[!UICONTROL di]** ricerca, specificate i percorsi di ricerca quando un visitatore inserisce una query.

![chlimage_1-375](assets/chlimage_1-375.png)

* **[!UICONTROL Percorsi]** di ricerca Per aggiungere percorsi di ricerca mediante il pulsante Aggiungi elemento, la ricerca nel contenuto è limitata. Ad esempio, per limitare la ricerca a un forum specifico, selezionate un componente forum all’interno di una pagina:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Pagina]** risultati I risultati verranno visualizzati su una pagina separata specificata dal browser per selezionare una pagina contenente il `Search Results` componente.

## Risultati di ricerca {#search-results}

### Aggiungere risultati di ricerca a una pagina {#add-search-results-to-a-page}

Per aggiungere un `Search Results` componente a una pagina in modalità di creazione, usate il browser Componenti per individuare

* `Communities / Search Results`

e trascinarlo nella posizione desiderata su una pagina. A differenza del componente Ricerca, non è necessaria una seconda pagina, in quanto i risultati verranno visualizzati sulla stessa pagina.

Se si utilizza la funzione di ricerca altrove nel sito Web, `Search Results` è possibile configurare questa pagina in modo che sia la `Result Page` sola o tutte le istanze di `Search`.

Per le informazioni necessarie, visita [Community Components Basics](basics.md).

Quando la libreria lato client richiesta `cq.social.hbs.search`è inclusa, viene visualizzato così il `Search Result` componente:

![chlimage_1-376](assets/chlimage_1-376.png)

### Configurare il risultato di ricerca aggiunto {#configure-the-added-search-result}

Selezionate il `Search Results` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-377](assets/chlimage_1-377.png)

Nella scheda Impostazioni **[!UICONTROL risultati di]** ricerca è possibile specificare i percorsi inclusi nella ricerca quando una query viene inserita da un visitatore.

![chlimage_1-378](assets/chlimage_1-378.png)

* **[!UICONTROL Risultati ricerca per pagina]** Definite il numero di argomenti/post mostrati per pagina. Il valore predefinito è 10.

* **[!UICONTROL Percorsi]** di ricerca Per aggiungere percorsi di ricerca mediante il pulsante Aggiungi elemento, la ricerca nel contenuto è limitata.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Search Essentials](search-implementation.md) per gli sviluppatori.
