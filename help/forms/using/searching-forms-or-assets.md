---
title: Ricerca di moduli e risorse
seo-title: Ricerca di moduli e risorse
description: È possibile cercare moduli e risorse nell'istanza AEM utilizzando AEM. La ricerca di base e avanzata consente di individuare rapidamente le risorse.
seo-description: È possibile cercare moduli e risorse nell'istanza AEM utilizzando AEM. La ricerca di base e avanzata consente di individuare rapidamente le risorse.
uuid: 0928a453-3dc4-448b-9320-dcbf20606dd9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: e65925ff-1fbf-4da6-bf09-0cf056c86e5a
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---


# Ricerca di moduli e risorse{#searching-for-forms-and-assets}

È possibile cercare i moduli o le risorse dei moduli utilizzando una stringa di testo o una stringa di testo con i caratteri jolly. Potete anche limitare la ricerca utilizzando i criteri disponibili in varie categorie nel pannello Ricerca.

Quando selezionate uno o più criteri e specificate anche una stringa di testo, l’intersezione del testo e dei criteri viene restituita come risultati di ricerca. I risultati della ricerca sono validi quanto i metadati del modulo e delle risorse forniti.

Fare clic su ![aem6forms_search](assets/aem6forms_search.png) per visualizzare o nascondere il pannello di ricerca.

## Ricerca di base {#basic-search}

Una ricerca di base è la ricerca predefinita, eseguita senza specificare alcun filtro. Una ricerca full-text sulle proprietà dei metadati viene condotta da  AEM Forms.

Per eseguire una ricerca di base, immettete la query di ricerca nel campo di testo e premete Invio. È inoltre possibile immettere il carattere jolly (*) per far corrispondere qualsiasi numero di caratteri.

Adobe Experience Manager cerca il testo immesso nelle proprietà dei metadati e restituisce i risultati corrispondenti. Se si digitano più parole, l&#39;operazione di ricerca corrisponde al testo completo per la ricerca.

Tenete presenti i seguenti punti sulla ricerca di base:

* La ricerca viene eseguita utilizzando le proprietà dei metadati del modulo e delle risorse.
* Se si digitano più parole, l&#39;operazione di ricerca corrisponde al testo completo per la ricerca.
* La ricerca non fa distinzione tra maiuscole e minuscole. Ad esempio, quando digitate `geometrixx`, nei risultati della ricerca vengono visualizzate le risorse con titoli `Geometrixx`, `GEOMETRIXX` e `GeoMetRixx`.

* Le corrispondenze parziali di una parola non sono supportate. Per eseguire la ricerca utilizzando stringhe parziali, utilizzare il carattere jolly *. Tuttavia, se la query di ricerca corrisponde a una parola completa, viene visualizzato il modulo o la risorsa corrispondente.
* Gli spazi aggiuntivi vengono rispettati e non vengono tagliati durante la ricerca. Ad esempio, `My form` non è la stessa query di ricerca di `My form`.

* Se i dati e i valori di visualizzazione dei campi nelle proprietà dei metadati sono diversi, non è possibile utilizzare i valori di visualizzazione come parametri di ricerca. Ad esempio, non è possibile effettuare ricerche basate su uno stato, ad esempio Modificato o Pubblicato, poiché queste proprietà sono memorizzate in un formato diverso.

## Ricerca avanzata {#advanced-search}

Nei criteri di ricerca, oltre alla query è possibile specificare alcuni parametri di ricerca per rendere la ricerca di base più efficiente e mirata.

![Campo di ricerca e parametri o filtri per AEM ricerca di moduli e risorse](assets/search_forms_assets.png)

Campo di ricerca e parametri o filtri per AEM ricerca di moduli e risorse

### Percorso risorsa {#asset-path}

Utilizzando il filtro del percorso della risorsa, puoi limitare i risultati della ricerca alla directory corrente. Se l&#39;opzione Cerca nella directory corrente non è selezionata, i risultati della ricerca contengono le risorse della directory di base. Se la pagina corrente non è una directory e l’opzione &quot;Cerca nella directory corrente&quot; è selezionata, la ricerca restituisce le risorse presenti nella directory principale.

### Modifica risorsa {#asset-modification}

Selezionate una delle seguenti opzioni per effettuare ricerche in tutte le risorse modificate in un determinato periodo di tempo.

| **Opzione** | **Descrizione** |
|---|---|
| Due ore fa | Consente di effettuare ricerche in tutte le risorse modificate nelle ultime due ore. |
| Una settimana fa | Consente di effettuare ricerche in tutte le risorse modificate nell’ultima settimana. |
| Un mese fa | Consente di effettuare ricerche in tutte le risorse modificate nell’ultimo mese. |
| Un anno fa | Consente di effettuare ricerche in tutte le risorse modificate nell’ultimo anno. |

### Stato risorsa {#asset-status}

Potete cercare le risorse utilizzando uno dei seguenti stati:

* **Pubblicato**: Cercate tutte le risorse pubblicate e non modificate dopo la pubblicazione.

* **Non pubblicato**: Cercate tutte le risorse che non sono mai state pubblicate.

* **Modificato**: Cercate tutte le risorse modificate o non pubblicate dopo la pubblicazione.

### Tipo risorsa {#asset-type}

Potete selezionare un numero qualsiasi di tipi di risorse. La ricerca restituisce l’unione di tutti i tipi di risorse selezionati.

<table>
 <tbody>
  <tr>
   <th>Opzione</th> 
   <th>Descrizione</th> 
  </tr>
  <tr>
   <td>Modello modulo<br /> </td> 
   <td>Cerca in tutti i modelli di modulo.<br /> </td> 
  </tr>
  <tr>
   <td>Modulo PDF</td> 
   <td>Eseguire ricerche in tutti i documenti PDF.</td> 
  </tr>
  <tr>
   <td>Documento</td> 
   <td>Consente di effettuare ricerche in tutti i documenti.</td> 
  </tr>
  <tr>
   <td>Modulo adattivo<br /> </td> 
   <td>Consente di effettuare ricerche in tutti i moduli adattivi.</td> 
  </tr>
  <tr>
   <td>Risorsa</td> 
   <td>Cerca in tutte le risorse.<br /> </td> 
  </tr>
 </tbody>
</table>

### Tag {#tags}

I tag sono etichette associate alle risorse per l’identificazione. Durante la ricerca, selezionate un numero qualsiasi di tag dall&#39;elenco a discesa o aggiungete eventuali tag personalizzati. Un risultato di ricerca contiene l&#39;intersezione dei tag selezionati.
