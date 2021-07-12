---
title: Ricerca di moduli e risorse
seo-title: Ricerca di moduli e risorse
description: È possibile cercare moduli e risorse nell’istanza AEM utilizzando AEM ricerca. La ricerca avanzata e di base consente di individuare rapidamente le risorse.
seo-description: È possibile cercare moduli e risorse nell’istanza AEM utilizzando AEM ricerca. La ricerca avanzata e di base consente di individuare rapidamente le risorse.
uuid: 0928a453-3dc4-448b-9320-dcbf20606dd9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: e65925ff-1fbf-4da6-bf09-0cf056c86e5a
docset: aem65
role: Admin
exl-id: 1f4f49b7-5f32-47dd-9dc7-a6974faf2bdf
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---

# Ricerca di moduli e risorse{#searching-for-forms-and-assets}

È possibile cercare i moduli o le risorse dei moduli utilizzando una stringa di testo o una stringa di testo insieme ai caratteri jolly. Puoi anche limitare la ricerca utilizzando i criteri disponibili in varie categorie nel pannello Ricerca .

Quando selezioni uno o più criteri e specifichi anche una stringa di testo, viene restituita l’intersezione del testo e dei criteri come risultati di ricerca. I risultati della ricerca sono validi quanto i metadati del modulo e della risorsa forniti.

Fai clic su ![aem6forms_search](assets/aem6forms_search.png) per mostrare o nascondere il pannello di ricerca.

## Ricerca di base {#basic-search}

Una ricerca di base è la ricerca predefinita, eseguita senza specificare alcun filtro. AEM Forms esegue una ricerca full-text sulle proprietà dei metadati.

Per eseguire una ricerca di base, immetti la query di ricerca nel campo di testo e premi return. È inoltre possibile immettere il carattere jolly (*) per far corrispondere qualsiasi numero di caratteri.

Adobe Experience Manager cerca il testo immesso nelle proprietà dei metadati e restituisce i risultati corrispondenti. Se si digitano più parole, l&#39;operazione di ricerca corrisponde al testo completo per la ricerca.

Nota i seguenti punti sulla ricerca di base:

* La ricerca viene eseguita utilizzando le proprietà dei metadati del modulo e delle risorse.
* Se si digitano più parole, l&#39;operazione di ricerca corrisponde al testo completo per la ricerca.
* La ricerca non fa distinzione tra maiuscole e minuscole. Ad esempio, quando digiti `geometrixx`, nei risultati della ricerca vengono visualizzate le risorse con titoli `Geometrixx`, `GEOMETRIXX` e `GeoMetRixx`.

* Le corrispondenze parziali di una parola non sono supportate. Per eseguire la ricerca utilizzando stringhe parziali, utilizzare il carattere jolly * . Tuttavia, se la query di ricerca corrisponde a una parola completa, viene visualizzato il modulo o la risorsa corrispondente.
* Gli spazi aggiuntivi vengono rispettati e non vengono tagliati durante la ricerca. Ad esempio, `My form` non è la stessa query di ricerca di `My form`.

* Se i dati e i valori di visualizzazione dei campi nelle proprietà dei metadati sono diversi, non è possibile utilizzare i valori di visualizzazione come parametri di ricerca. Ad esempio, non è possibile eseguire ricerche in base a uno stato, ad esempio Modificato o Pubblicato, poiché queste proprietà sono memorizzate in un formato diverso.

## Ricerca avanzata {#advanced-search}

Nei criteri di ricerca, oltre alla query è possibile specificare alcuni parametri di ricerca per rendere la ricerca di base più efficiente e mirata.

![Campo di ricerca e parametri o filtri per la ricerca AEM moduli e risorse](assets/search_forms_assets.png)

Campo di ricerca e parametri o filtri per la ricerca AEM moduli e risorse

### Percorso risorsa {#asset-path}

Utilizzando il filtro del percorso della risorsa, puoi limitare i risultati della ricerca alla directory corrente. Se l&#39;opzione Cerca nella directory corrente non è selezionata, i risultati della ricerca contengono le risorse della directory di base. Se la pagina corrente non è una directory e l’opzione &quot;Cerca nella directory corrente&quot; è selezionata, la ricerca restituisce le risorse presenti nella directory principale.

### Modifica risorsa {#asset-modification}

Seleziona una delle seguenti opzioni per eseguire ricerche in tutte le risorse modificate in un determinato periodo di tempo.

| **Opzione** | **Descrizione** |
|---|---|
| Due ore fa | Cerca in tutte le risorse modificate nelle ultime due ore. |
| Una settimana fa | Cerca in tutte le risorse modificate nell’ultima settimana. |
| Un mese fa | Cerca in tutte le risorse modificate nell’ultimo mese. |
| Un anno fa | Cerca in tutte le risorse modificate nell’ultimo anno. |

### Stato risorsa {#asset-status}

Puoi cercare le risorse utilizzando uno dei seguenti stati:

* **Pubblicato**: Cerca tutte le risorse pubblicate e non modificate dopo la pubblicazione.

* **Non pubblicato**: Cerca in tutte le risorse che non vengono mai pubblicate.

* **Modificato**: Cerca in tutte le risorse modificate o non pubblicate dopo la pubblicazione.

### Tipo risorsa {#asset-type}

Puoi selezionare un numero qualsiasi di tipi di risorse. La ricerca restituisce l’unione di tutti i tipi di risorse selezionati.

<table>
 <tbody>
  <tr>
   <th>Opzione</th> 
   <th>Descrizione</th> 
  </tr>
  <tr>
   <td>Modello di modulo<br /> </td> 
   <td>Cerca in tutti i modelli di modulo.<br /> </td> 
  </tr>
  <tr>
   <td>Modulo PDF</td> 
   <td>Cerca in tutti i documenti PDF.</td> 
  </tr>
  <tr>
   <td>Documento</td> 
   <td>Cerca in tutti i documenti.</td> 
  </tr>
  <tr>
   <td>Modulo adattivo<br /> </td> 
   <td>Cerca in tutti i moduli adattivi.</td> 
  </tr>
  <tr>
   <td>Risorsa</td> 
   <td>Cerca in tutte le risorse.<br /> </td> 
  </tr>
 </tbody>
</table>

### Tag {#tags}

I tag sono etichette collegate alle risorse per l’identificazione. Durante la ricerca, seleziona un numero qualsiasi di tag dal menu a discesa o aggiungi tag personalizzati, se necessario. Un risultato della ricerca contiene l’intersezione dei tag selezionati.
