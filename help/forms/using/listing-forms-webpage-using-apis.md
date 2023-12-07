---
title: Elencare moduli su una pagina web utilizzando le API
description: Eseguire query a livello di codice su Forms Manager per recuperare un elenco filtrato di moduli e visualizzarli nelle proprie pagine Web.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: cfca6656-d2db-476d-a734-7a1d1e44894e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# Elencare moduli su una pagina web utilizzando le API {#listing-forms-on-a-web-page-using-apis}

AEM Forms fornisce un’API di ricerca basata su REST che gli sviluppatori web possono utilizzare per eseguire query e recuperare un set di moduli che soddisfano i criteri di ricerca. Puoi utilizzare le API per cercare i moduli in base a vari filtri. L’oggetto di risposta contiene attributi del modulo, proprietà e punti finali del rendering dei moduli.

Per cercare moduli utilizzando l’API REST, invia una richiesta GET al server all’indirizzo `https://'[server]:[port]'/libs/fd/fm/content/manage.json` con i parametri di query descritti di seguito.

## Parametri di query {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nome attributo<br /> </strong></td>
   <td><strong>Descrizione<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>Specifica la funzione da chiamare. Per cercare i moduli, imposta il valore di <code>func </code>attribuire a <code>searchForms</code>.</p> <p>Ad esempio: <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>Nota:</strong> <em>Questo parametro è obbligatorio.</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>Specifica il percorso dell'applicazione per la ricerca dei moduli. Per impostazione predefinita, l’attributo appPath cerca tutte le applicazioni disponibili a livello di nodo principale.<br /> </p> <p>È possibile specificare più percorsi di applicazione in una singola query di ricerca. Separare più percorsi con il carattere barra verticale (|). </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>Specifica le proprietà da recuperare con le risorse. Puoi usare l’asterisco (*) per recuperare tutte le proprietà contemporaneamente. Utilizzare l'operatore pipe (|) per specificare più proprietà. </p> <p>Ad esempio: <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>Nota</strong>: </p>
    <ul>
     <li><em>Le proprietà come ID, percorso e nome vengono sempre recuperate. </em></li>
     <li><em>Ogni risorsa ha un set diverso di proprietà. Proprietà come formUrl, pdfUrl e guideUrl non dipendono dall’attributo cutpoints. Queste proprietà dipendono dal tipo di risorsa e vengono recuperate di conseguenza. </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relazione<br /> </td>
   <td>Specifica le risorse correlate da recuperare insieme ai risultati della ricerca. Per recuperare le risorse correlate, puoi scegliere una delle seguenti opzioni:
    <ul>
     <li><strong>NO_RELATION</strong>: non recuperare le risorse correlate.</li>
     <li><strong>IMMEDIATO</strong>: recupera le risorse direttamente correlate ai risultati della ricerca.</li>
     <li><strong>TUTTI</strong>: recupera le risorse direttamente e indirettamente correlate.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>Specifica il numero massimo di moduli da recuperare.</td>
  </tr>
  <tr>
   <td>offset</td>
   <td>Specifica il numero di moduli da saltare dall'inizio.</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>Specifica se restituire o meno i risultati della ricerca che corrispondono ai criteri specificati. </td>
  </tr>
  <tr>
   <td>istruzioni</td>
   <td><p>Specifica l'elenco di istruzioni. Le query vengono eseguite nell’elenco delle istruzioni specificate nel formato JSON. </p> <p>Ad esempio:</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>Nell’esempio precedente, </p>
    <ul>
     <li><strong>nome</strong>: specifica il nome della proprietà da cercare.</li>
     <li><strong>valore</strong>: specifica il valore della proprietà da cercare.</li>
     <li><strong>operatore</strong>: specifica l’operatore da applicare durante la ricerca. Sono supportati i seguenti operatori:
      <ul>
       <li>EQ - Uguale a </li>
       <li>NEQ - Non uguale a</li>
       <li>GT - Maggiore di</li>
       <li>LT - Minore di</li>
       <li>GTEQ - Maggiore o uguale a</li>
       <li>LTEQ - Minore o uguale a</li>
       <li>CONTAINS - A contiene B se B fa parte di A</li>
       <li>FULL-TEXT - Ricerca full-text</li>
       <li>STARTSWITH - A inizia con B se B è la parte iniziale di A</li>
       <li>ENDSWITH: A termina con B se B è la parte finale di A</li>
       <li>LIKE - Implementa l’operatore LIKE</li>
       <li>AND - Combinare più istruzioni</li>
      </ul> <p><strong>Nota:</strong> <em>Gli operatori GT, LT, GTEQ e LTEQ sono applicabili a proprietà di tipo lineare come LONG, DOUBLE e DATE.</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>ordini<br /> </td>
   <td><p>Specifica i criteri di ordine per i risultati della ricerca. I criteri sono definiti in formato JSON. È possibile ordinare i risultati di ricerca in più campi. I risultati vengono ordinati in base all'ordine di visualizzazione dei campi nella query.</p> <p>Ad esempio:</p> <p>Per recuperare i risultati della query ordinati per proprietà titolo in ordine crescente, aggiungi il seguente parametro: </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>nome</strong>: specifica il nome della proprietà da utilizzare per ordinare i risultati della ricerca.</li>
     <li><strong>criteri</strong>: specifica l'ordine dei risultati. L'attributo order accetta i seguenti valori:
      <ul>
       <li>ASC: utilizza ASC per disporre i risultati in ordine crescente.<br /> </li>
       <li>DES: utilizza DES per disporre i risultati in ordine decrescente.</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>Specifica se recuperare il contenuto binario. Il <code>includeXdp</code> l'attributo è applicabile per le attività di tipo <code>FORM</code>, <code>PDFFORM</code>, e <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>Specifica i tipi di risorse da recuperare da tutte le risorse pubblicate. Utilizza l’operatore pipe (|) per specificare più tipi di risorse. I tipi di risorse validi sono FORM, PDFFORM, PRINTFORM, RESOURCE e GUIDE.</td>
  </tr>
 </tbody>
</table>

## Richiesta di esempio {#sample-request}

```json
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :"lastModifiedDate":"order":"ASC"}]
```

## Risposta di esempio {#sample-response}

```json
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## Articoli correlati

* [Abilitare i componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* [Crea pagina portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale Forms](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
