---
title: Memorizzazione in cache e prestazioni
description: Scopri le diverse configurazioni disponibili per abilitare GraphQL e la memorizzazione in cache dei contenuti per ottimizzare le prestazioni dell’implementazione commerce.
exl-id: ecce64bf-5960-4ddb-b6e3-dad401038c11
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 67%

---

# Memorizzazione in cache e prestazioni {#caching}

## Memorizzazione in cache di componenti e risposte GraphQL {#graphql}

I componenti core CIF di AEM dispongono già del supporto integrato necessario per memorizzare nella cache le risposte GraphQL per i singoli componenti. Questa funzione può essere utilizzata per ridurre notevolmente il numero di chiamate back-end di GraphQL. È possibile ottenere una memorizzazione efficace nella cache, in particolare per query ripetute come il recupero della struttura delle categorie per un componente di navigazione o il recupero di tutti i valori aggregati/facet disponibili visualizzati sulle pagine di ricerca di prodotto e categoria.

Per i componenti core CIF di AEM, la memorizzazione in cache è configurata in base al componente, quindi è possibile controllare se (e per quanto tempo) le richieste e le risposte GraphQL vengono memorizzate nella cache per ciascun componente. È inoltre possibile definire il comportamento di caching per i servizi OSGi utilizzando il client GraphQL.

### Configurazione

Una volta configurata per un determinato componente, la cache inizia a memorizzare le query e le risposte GraphQL in base a quanto definito da ciascuna voce per la configurazione della cache. Le dimensioni della cache e la durata della memorizzazione in cache di ciascuna voce devono essere definite in base al progetto, a seconda, ad esempio, della frequenza con cui i dati del catalogo possono cambiare, di quanto sia importante che un componente visualizzi sempre i dati più recenti possibili e così via. Non è prevista alcuna invalidazione della cache, quindi occorre prestare attenzione quando si impostano le durate della cache.

Quando si configura la memorizzazione in cache per i componenti, il nome della cache deve corrispondere al nome dei componenti **proxy** definiti nel progetto.

Prima che il client invii una richiesta GraphQL, controlla se **esatto** la stessa richiesta GraphQL è già memorizzata nella cache e potrebbe restituire la risposta nella cache. Per trovare una corrispondenza, la richiesta GraphQL DEVE corrispondere esattamente, ovvero la query, il nome dell’operazione (se presente), le variabili (se presenti) DEVONO essere tutte uguali alla richiesta memorizzata nella cache. Anche tutte le intestazioni HTTP personalizzate che potrebbero essere impostate DEVONO essere uguali. Ad esempio, Adobe Commerce `Store` L&#39;intestazione DEVE corrispondere.

### Esempi

È consigliabile configurare la memorizzazione in cache per il servizio di ricerca che raccoglie tutti i valori aggregati/facet disponibili visualizzati nelle pagine di ricerca e categoria del prodotto. Questi valori generalmente cambiano solo quando un nuovo attributo viene ad esempio aggiunto ai prodotti, pertanto la durata di questa voce della cache può essere “lunga” se il set di attributi di prodotto non cambia spesso. Anche se si tratta di un progetto specifico, consigliamo valori di alcuni minuti nelle fasi di sviluppo del progetto e di alcune ore per i sistemi di produzione stabili.

Questa configurazione è in genere configurata con la seguente voce cache:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Un altro scenario esemplificativo in cui si consiglia di utilizzare la funzione di caching GraphQl è il componente di navigazione, perché invia la stessa query GraphQL su tutte le pagine. In questo caso, la voce cache viene generalmente impostata su:

```
venia/components/structure/navigation:true:10:600
```

Quando consideri [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) viene utilizzato. Si noti l’uso del nome proxy del componente `venia/components/structure/navigation` e **non** del nome del componente di navigazione CIF (`core/cif/components/structure/navigation/v1/navigation`).

La memorizzazione nella cache per altri componenti deve essere definita in base al progetto, in genere in coordinamento con la memorizzazione nella cache configurata a livello di Dispatcher. Non è prevista l’invalidazione attiva di queste cache, pertanto la durata di memorizzazione nella cache deve essere impostata con attenzione. Non esiste un valore universale che vada bene per tutti i possibili progetti e casi di utilizzo. Occorre definire una strategia di caching a livello di progetto che corrisponda meglio ai requisiti del progetto.

## Memorizzazione in cache del dispatcher {#dispatcher}

La memorizzazione nella cache di pagine o frammenti AEM in [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) è una best practice per qualsiasi progetto AEM. In genere, si basa su tecniche di invalidazione che garantiscono che qualsiasi contenuto modificato in AEM venga aggiornato correttamente in Dispatcher. Si tratta di una funzione fondamentale della strategia di caching di AEM Dispatcher.

Oltre al contenuto CIF puro AEM gestito, in genere una pagina può visualizzare i dati di e-commerce recuperati dinamicamente da Adobe Commerce tramite GraphQL. Anche se la struttura della pagina stessa potrebbe non cambiare mai, il contenuto commerciale potrebbe cambiare, ad esempio, se alcuni dati di prodotto (come nome o prezzo) cambiano in Adobe Commerce.

Per fare in modo che le pagine CIF possano essere memorizzate nella cache per un periodo di tempo limitato nel Dispatcher di AEM, si consiglia quindi di utilizzare [Annullamento della validità della cache basata su tempo](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl) (anche noto come memorizzazione in cache basata su TTL) durante il caching delle pagine CIF nel Dispatcher di AEM. Questa funzione può essere configurata in AEM utilizzando il pacchetto [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) aggiuntivo.

Con il caching basato su TTL, uno sviluppatore definisce in genere una o più durate di memorizzazione nella cache per le pagine AEM selezionate. In questo modo le pagine CIF vengono memorizzate nella cache solo in Dispatcher AEM fino alla durata configurata e il contenuto viene aggiornato di frequente.

>[!NOTE]
>
>Mentre i dati lato server possono essere memorizzati nella cache da AEM Dispatcher, alcuni componenti CIF come `product`, `productlist`e `searchresults` in genere, i componenti recuperano sempre i prezzi dei prodotti in una richiesta browser lato client quando la pagina viene caricata. In questo modo, al caricamento della pagina vengono sempre recuperati i contenuti dinamici fondamentali.

## Risorse aggiuntive

- [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione della cache per GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
