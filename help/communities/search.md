---
title: Funzione di ricerca
seo-title: Search Feature
description: Aggiunta e configurazione della ricerca a un sito di Communities
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# Funzione di ricerca {#search-feature}

La funzione di ricerca funziona con altre funzioni, ad esempio i forum, per fornire la possibilità di cercare contenuti.

Quando si aggiunge la possibilità di cercare i post inseriti dai membri della community, denominati contenuti generati dagli utenti (UGC, User generato Content), sono disponibili due componenti: [Ricerca](#search) e [Risultati ricerca](#search-results).

La pagina che include `Search Results` Il componente supporta sia la ricerca che la visualizzazione dei risultati.

La pagina che include `Search` il componente fornisce una posizione per avviare una ricerca con i risultati visualizzati nella `Search Results` pagina.

La funzione di ricerca può essere utilizzata con qualsiasi altra funzione che consente ai visitatori e ai membri del sito di visualizzare il contenuto.

## Ricerca {#search-features}

### Aggiungi ricerca a una pagina {#add-search-to-a-page}

Per aggiungere una `Search` componente per una pagina in modalità di creazione, usate il browser componenti per individuare `Communities / Search` e trascinarlo nella posizione desiderata su una pagina. Utilizzo di `Search` richiede una seconda pagina per `Search Results.`

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando la libreria lato client richiesta, `cq.social.hbs.search`, è incluso, è così che `Search` apparirà .

![ricerca aggiuntiva](assets/add-search.png)

### Configurare la ricerca aggiunta {#configure-the-added-search}

Seleziona il `Search` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![confusione](assets/configure-new.png)

Sotto la **[!UICONTROL Impostazioni di ricerca]** Specifica i percorsi di ricerca quando una query viene inserita da un visitatore.

![impostazioni di ricerca](assets/search-settings.png)

* **[!UICONTROL Percorsi di ricerca]**
Aggiungendo percorsi di ricerca utilizzando il pulsante Aggiungi elemento, la ricerca del contenuto è limitata. Ad esempio, per limitare la ricerca a un forum specifico, selezionate un componente forum all’interno di una pagina:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Pagina dei risultati]**
I risultati verranno visualizzati in una pagina separata specificata dal browser per selezionare una pagina contenente il 
`Search Results` componente.

## Risultati di ricerca {#search-results}

### Aggiungere risultati di ricerca a una pagina {#add-search-results-to-a-page}

Per aggiungere una `Search Results` componente per una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Search Results`

e trascinarlo nella posizione desiderata su una pagina. A differenza del componente Ricerca, non è necessaria alcuna seconda pagina, in quanto i risultati verranno visualizzati sulla stessa pagina.

Se utilizzi Ricerca in un altro sito web, questa pagina con `Search Results` può essere configurato come `Result Page` per una o tutte le istanze `Search`.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando la libreria lato client richiesta, `cq.social.hbs.search`, è incluso, è così che `Search Result` apparirà il componente:

![risultato della ricerca](assets/search-result1.png)

### Configurare il risultato della ricerca aggiunta {#configure-the-added-search-result}

Seleziona il `Search Results` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

Sotto la **[!UICONTROL Impostazioni dei risultati di ricerca]** è possibile specificare quali percorsi vengono inclusi nella ricerca quando una query viene inserita da un visitatore.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Risultati di ricerca per pagina]**

   Definisci il numero di argomenti/post visualizzati per pagina. Il valore predefinito è 10.

* **[!UICONTROL Percorsi di ricerca]**

   Aggiungendo percorsi di ricerca utilizzando il pulsante Aggiungi elemento, la ricerca del contenuto è limitata.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sulla ricerca](search-implementation.md) per sviluppatori.
