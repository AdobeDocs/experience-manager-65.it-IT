---
title: Supporto di script per moduli HTML5
seo-title: Scripting support for HTML5 forms
description: JavaScript, proprietà FormCalc e altri metodi supportati in HTML Forms.
seo-description: JavaScript, FormCalc properties, and other methods that are supported in HTML5 Forms.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
feature: Mobile Forms
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '3887'
ht-degree: 7%

---

# Supporto di script per moduli HTML5 {#scripting-support-for-html-forms}

Di seguito sono elencati i metodi e le proprietà JavaScript, FormCalc supportati nei moduli HTML5:

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>Proprietà </th>
   <th>Descrizione<br /> </th>
   <th>Eccezione</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>Specifica il contenuto del campo prima che venga modificato in risposta alle azioni di un utente. Questo valore può essere richiamato, in modo simile a una feature di annullamento.</td>
   <td><p>Non funziona per menu a discesa e caselle di riepilogo. <code>PrevText </code>non funziona correttamente nei seguenti casi:</p>
    <ul>
     <li>Quando si digitano alcuni tasti carattere speciali (ad esempio, $, (,), &amp;, @ e altro) nei campi Numerici di iPad e </li>
     <li>Per il campo Data (quando la data viene immessa nel calendario).<br /> </li>
    </ul> <p>L'impostazione del valore tramite script non è supportata.</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>Specifica l'oggetto su cui agisce l'evento.</td>
   <td>L'impostazione del valore tramite script non è supportata.<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>Specifica il contenuto del campo dopo la modifica in risposta alle azioni dell'utente.</td>
   <td><p>Il <code>newText</code> La proprietà non funziona correttamente nei seguenti casi:</p>
    <ul>
     <li>Selezione-sostituzione di testi</li>
     <li>Per eliminare, copiare e incollare i testi.</li>
     <li>Quando si digitano alcuni tasti carattere speciali (ad esempio, $, (, ), &amp;, @ e altro) nei campi numerici<br /> </li>
     <li>Quando si utilizza la combinazione maiusc+alfanumerico. </li>
     <li>Quando si utilizzano i campi data/ora.</li>
    </ul>
    <div>
      L'impostazione del valore tramite script non è supportata.
    </div> </td>
  </tr>
  <tr>
   <td>cambia</td>
   <td>Specifica il valore digitato o incollato da un utente in un campo subito dopo l'esecuzione dell'azione. </td>
   <td><p>La proprietà di modifica non funziona correttamente nei casi seguenti:</p>
    <ul>
     <li>Selezione-sostituzione di testi</li>
     <li>Per eliminare, copiare e incollare i testi.</li>
     <li>Quando si digitano alcuni tasti carattere speciali (ad esempio, $, (,), &amp;, @ e altro) nei campi numerici<br /> </li>
     <li>Quando si utilizza la combinazione maiusc+alfanumerico. </li>
     <li>Quando si utilizzano i campi data/ora.</li>
    </ul> <p>L'impostazione del valore tramite script non è supportata.</p> </td>
  </tr>
  <tr>
   <td>keydown</td>
   <td>Determina se un utente sta premendo un tasto freccia per effettuare una selezione. Questa proprietà è disponibile solo per caselle di riepilogo ed elenchi a discesa.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>modificatore</td>
   <td>Determina se tenere premuto il tasto modificatore (ad esempio, Ctrl su Microsoft® Windows®) durante l'esecuzione di un evento specifico.</td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
   <th>Eccezione</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>Restituisce il tipo di applicazione dell'host. Disponibile solo per applicazioni client.</td>
   <td>Restituisce <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Restituisce il nome dell'applicazione corrente.</td>
   <td>Restituisce il nome del browser e la relativa versione. Ad esempio, nel browser Chrome, il valore restituito è <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>Restituisce il numero di pagine del documento.</td>
   <td>Il criterio di paginazione dei moduli HTML5 non è identico al criterio di paginazione dei PDF forms. Pertanto, l’API numPages può restituire valori diversi in entrambi i casi.</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>Restituisce una stringa che rappresenta la piattaforma del computer che esegue lo script.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>Specifica il titolo del documento. È disponibile solo per le applicazioni client.</td>
   <td>Restituisce il titolo del documento HTML nel modulo, anziché il titolo dei metadati del modulo come se fossero presenti PDF forms.</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>Restituisce una stringa che rappresenta il numero di versione dell'applicazione corrente.</td>
   <td>Restituisce la versione del modulo.</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>Specifica se gli script di calcolo verranno eseguiti.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>Specifica se gli script di convalida verranno eseguiti.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>Consente di passare alla pagina precedente.</td>
   <td>I moduli HTML5 non seguono lo stesso criterio di impaginazione di PDF Form, pertanto la pagina precedente di un modulo HTML5 è diversa dalla pagina precedente di un modulo PDF.</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>Consente di passare alla pagina successiva di un modulo. Utilizzare il metodo pageDown in fase di esecuzione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>Imposta lo stato attivo della tastiera sul campo specificato. Il campo viene specificato come oggetto o dall'espressione SOM del campo. È disponibile solo per le applicazioni client.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>Reimposta i campi sui valori predefiniti all'interno di un documento.</td>
   <td>Cancella tutti i dati di un modulo con dati uniti, anziché ripristinarli ai valori predefiniti.</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>Visualizza una finestra di dialogo. È disponibile solo per le applicazioni client</td>
   <td>La finestra di messaggio di tipo Sì/No viene convertita in OK/Annulla. La finestra di messaggio con tre pulsanti non è supportata.</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>Imposta la pagina attualmente attiva di un documento in fase di esecuzione.</p> <p>I valori di pagina sono basati su 0, pertanto la prima pagina di un documento restituisce il valore 0.</p> <p>La proprietà currentPage è disponibile quando layout:ready viene eseguito su un client. Tuttavia, non è disponibile quando layout:ready viene eseguito sul server, perché la proprietà non verrà eseguita fino all'esecuzione del layout del modulo.</p> </td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

### o in un altro campo {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>Proprietà</span></strong></th>
   <th><strong><span>Descrizione<br /> </span></strong></th>
   <th><strong><span>Eccezione</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>Controlla la partecipazione dell'oggetto associato in diverse fasi di elaborazione. Se l'oggetto è un contenitore, il contenuto del contenitore eredita tutte le restrizioni applicate dal controllo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>Controlla l'accesso degli utenti ai contenuti.</td>
   <td>Non funziona per il gruppo di esclusione. Inoltre, i moduli HTML5 riservano lo stesso trattamento agli oggetti non interattivi e protetti.<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Identificatore utilizzato per identificare questo elemento nelle espressioni di script.</td>
   <td>I moduli HTML5 non consentono l'impostazione della proprietà name per gli oggetti. Si tratta di una proprietà di sola lettura per i moduli HTML5.</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>Elemento di contenuto che racchiude una singola unità di contenuto di dati.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>Specifica il valore non formattato per il campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>Specifica il valore formattato per il campo.</td>
   <td>Impostazione <code>formattedValue</code> tramite script non supportato.</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>Specifica il valore di modifica per questo campo.</td>
   <td>Impostazione <code>editValue </code>tramite script non supportato.</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>Specifica la stringa del messaggio di convalida del formato per questo campo.</td>
   <td>Impostazione <code>formatMessage </code>tramite script non supportato.</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>Specifica il valore del colore di sfondo per questo campo. È necessario impostare la proprietà border.fill.presence affinché sia visibile separatamente.</td>
   <td>Non restituisce correttamente il colore predefinito del campo.</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>L'oggetto border descrive il bordo che circonda un oggetto.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>L’oggetto ui racchiude la descrizione dell’interfaccia utente di un oggetto modulo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>Specifica il valore nullTest per il campo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>Specifica il valore del colore del bordo per questo campo. È necessario impostare la proprietà border.edge.presence affinché sia visibile separatamente.</td>
   <td>Non restituisce correttamente il colore predefinito del bordo del campo.</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>Il numero di elementi nell'elenco.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>Aggiunge nuovi elementi al campo corrente.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>Rimuove tutti gli elementi dal campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>Ottiene il valore associato di un elemento di visualizzazione specifico di un elenco a discesa o di una casella di riepilogo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>Esegue lo script di calcolo del campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>Esegue lo script di convalida del campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>Esegue lo script evento dell'oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>Restituisce lo stato di selezione dell'elemento specificato</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>Imposta lo stato di selezione dell'elemento specificato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>Recupera il testo da visualizzare per l'indice dell'elemento specificato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>Recupera il valore di dati per l'indice dell'elemento specificato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>Elimina l'elemento nell'indice specificato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>Imposta gli elementi specificati nel campo corrente. Sostituisce gli elementi preesistenti.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Misurazione dell'altezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>l</td>
   <td>Misurazione che specifica la larghezza del layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Specifica la coordinata x del punto di ancoraggio del contenitore rispetto all'angolo superiore sinistro del contenitore padre quando posizionato con il layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Specifica la coordinata y del punto di ancoraggio di un contenitore rispetto all'angolo superiore sinistro del contenitore padre quando posizionato con il layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>L'oggetto caption descrive un'etichetta descrittiva associata a un oggetto di progettazione del modulo.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>convalida</td>
   <td>L'oggetto validate controlla la convalida dei dati forniti dall'utente in un modulo. L’oggetto di convalida può essere attivato più volte durante la durata di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>Specifica la sottomaschera padre (pagina) di questo campo.</td>
   <td>Restituisce sempre la sottomaschera padre anziché la prima sottomaschera padre non di ambito.<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>Indice del primo elemento selezionato.</td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## Modulo {#form}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| formNodes | Restituisce un elenco di tutti gli oggetti modello modulo associati a un oggetto dati specificato. |  |

## InstanceManager {#instancemanager}

| Proprietà | Descrizione |
|---|---|
| `name` | Identificatore utilizzato per identificare questo elemento nelle espressioni di script. |
| `occur` | Descrive i vincoli sul numero di istanze consentite per il contenitore che lo racchiude. |
| `min` | Specifica il numero minimo di istanze che è possibile creare. |
| `max` | Specifica il numero massimo di istanze che è possibile creare. |
| `count` | Specifica il numero corrente di istanze create. |
| `setInstances` | Aggiunge o rimuove dal nodo le sottomaschere o i set di sottomaschere specificati. |
| `addInstance` | Aggiunge una nuova istanza di una sottomaschera o di un set di sottomaschere a questo nodo. |
| `removeInstance` | Rimuove una sottomaschera o un set di sottomaschere da questo nodo. |
| `moveInstance` | Sposta un oggetto figlio di un oggetto modello modulo in un&#39;altra posizione specificata all&#39;interno del modello modulo. Anche le informazioni del modello dati corrispondenti per l’oggetto vengono spostate all’interno del modello dati. |
| `insertInstance` | Inserisce una nuova istanza di una sottomaschera o di un set di sottomaschere in questo nodo. |

## list {#list}

| Proprietà | Descrizione |
|---|---|
| `length` | Il numero di elementi nell’elenco. |
| `item` | Un indice a base zero nella raccolta. |
| `append` | Aggiunge un nodo alla fine dell&#39;elenco dei nodi. |
| `remove` | Rimuove un nodo dall&#39;elenco dei nodi. |
| `insert` | Inserisce un nodo prima di un nodo specifico nell&#39;elenco dei nodi. |

## nodo {#node}

| Proprietà | Descrizione | Eccezione |
|---|---|---|
| createNode | Crea un nuovo nodo basato su un nome di classe valido. | Nessuno |
| `isContainer` | Specifica se l&#39;oggetto è un oggetto contenitore. | Nessuno |
| `isNull` | Indica se il valore dati corrente è un valore Null. | Nessuno |
| `resolveNode` | Valuta l&#39;espressione SOM specificata, a partire dall&#39;oggetto modello di oggetti del modulo XML corrente, e restituisce il valore dell&#39;oggetto specificato nell&#39;espressione SOM. | Nessuno |
| `resolveNodes` | Valuta l&#39;espressione SOM specificata, a partire dall&#39;oggetto modello di oggetti del modulo XML corrente, e restituisce il valore dell&#39;oggetto specificato nell&#39;espressione SOM. | Nessuno |
| oneOfChild | Crea un nuovo nodo basato su un nome di classe valido. | Nessuno |
| getElement | Restituisce un oggetto figlio specificato. | Nessuno |
| getAttribute | Ottiene un valore di proprietà specificato. | Nessuno |
| setAttribute | Imposta il valore di una proprietà specificata. | Nessuno |

## modello {#model}

| Proprietà | Descrizione | Eccezione |
|---|---|---|
| ND | ND | ND |

## Sottomodulo {#subform}

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
   <th>Eccezione</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>Specifica l'indice dell'oggetto, relativo alle altre istanze create.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>Esegue lo script evento dell'oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>Restituisce un elenco di nodi contenuti nella sottomaschera (inclusi) che non hanno superato il test di convalida.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>bordo</td>
   <td>L'oggetto border descrive il bordo che circonda un oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Specifica il valore del colore del bordo per questo campo. È necessario impostare la proprietà border.edge.presence affinché sia visibile separatamente.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Misurazione dell'altezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>l</td>
   <td>Misurazione che specifica la larghezza del layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Specifica la coordinata x del punto di ancoraggio del contenitore rispetto all'angolo superiore sinistro del contenitore padre quando posizionato con il layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Specifica la coordinata y del punto di ancoraggio di un contenitore rispetto all'angolo superiore sinistro del contenitore padre quando posizionato con il layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>convalida</td>
   <td>L'oggetto validate controlla la convalida dei dati forniti dall'utente in un modulo. L’oggetto di convalida può essere attivato più volte durante la durata di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Identificatore utilizzato per identificare questo elemento nelle espressioni di script.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>presenza</td>
   <td>Specifica la visibilità di un oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>accesso</td>
   <td>Controlla l'accesso dell'utente al contenuto di un oggetto contenitore, ad esempio una sottomaschera.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>Calcola l'indice di una sottomaschera o di un set di sottomaschere in base alla posizione in cui si trova rispetto ad altre istanze dello stesso oggetto modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>L'oggetto instanceManager gestisce la creazione, la rimozione e lo spostamento di istanze di oggetti modello modulo.<br /> </td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

### invia {#submit}

| Proprietà | Descrizione |
|---|---|
| destinazione | L’URL a cui vengono inviati i dati. L’omissione di questo attributo implica che l’applicazione di elaborazione XFA ottenga l’URI utilizzando una tecnica specifica per il prodotto, ad esempio l’accesso a informazioni specifiche per il prodotto nell’oggetto di configurazione. |

## albero {#tree}

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
   <th>Eccezione</th>
  </tr>
  <tr>
   <td>nodi</td>
   <td>Restituisce un elenco di tutti gli oggetti figlio dell'oggetto corrente.</td>
   <td>
    <ul>
     <li>Non supportato per xfa.nodes, desc</li>
     <li>Il numero di nodi segnalati per PDF e HTML è diverso. </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Specifica il nome del nodo.</td>
   <td>L’impostazione del nome tramite script non è consentita in HTML.</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>Ottiene l'elemento padre per questo nodo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>index</td>
   <td>Restituisce la posizione del nodo nell'insieme di nodi di relazione like-named, in-scope, like-child.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>Ottiene l'espressione SOM per questo nodo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>Valuta l'espressione SOM specificata, a partire dall'oggetto modello di oggetti del modulo XML corrente, e restituisce il valore dell'oggetto specificato nell'espressione SOM.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>Valuta l'espressione SOM specificata, a partire dall'oggetto modello di oggetti del modulo XML corrente, e restituisce il valore dell'oggetto specificato nell'espressione SOM.</td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| Proprietà | Descrizione | Eccezione |
|---|---|---|
| instanceManager | L&#39;oggetto instanceManager gestisce la creazione, la rimozione e lo spostamento di istanze di oggetti modello modulo. | Nessuno |

## content {#content}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| isNull | Indica se il valore dati corrente è il valore null. |  |

## dataValue {#datavalue}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| isNull | Indica se il valore dati corrente è il valore null. |  |

## spigolo {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà </strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>colore</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto pattern.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche vengono riportate in Modello e sono disponibili per la creazione di script, ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## riempimento {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>colore</td>
   <td>Le proprietà colore definiscono un colore di riempimento univoco.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche vengono riportate in Modello e sono disponibili per la creazione di script, ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## lineare {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>colore</td>
   <td>La proprietà color descrive un colore univoco per un riempimento a gradiente lineare in un modulo.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche vengono riportate in Modello e sono disponibili per la creazione di script, ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## riga {#line}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>spigolo</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o di un rettangolo.<br /> </td>
   <td>Attributi come colore, cap e altro non sono supportati.<br /> </td>
  </tr>
 </tbody>
</table>

## pattern {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>colore</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto pattern. </td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche vengono riportate in Modello e sono disponibili per la creazione di script, ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## radiale {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>colore</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto radiale</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche vengono riportate in Modello e sono disponibili per la creazione di script, ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## stoppino {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>colore</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto stipple.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per la creazione di script ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## disegnare {#draw}

<table>
 <tbody>
  <tr>
   <td>Proprietà</td>
   <td>Descrizione</td>
   <td>Eccezione</td>
  </tr>
  <tr>
   <td>interfaccia utente</td>
   <td>L’oggetto ui racchiude la descrizione dell’interfaccia utente di un oggetto modulo.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
   <td>L'oggetto caption descrive un'etichetta descrittiva associata a un oggetto di progettazione del modulo.</td>
   <td> </td>
  </tr>
  <tr>
   <td>presenza</td>
   <td>Specifica la visibilità di un oggetto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Specifica un identificatore che può essere utilizzato per specificare questo oggetto o evento nelle espressioni di script.</td>
   <td>L’impostazione del valore in fase di esecuzione non è supportata</td>
  </tr>
  <tr>
   <td>valore</td>
   <td>L’oggetto value racchiude una singola unità di contenuto di dati.<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## angolo {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>colore</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto corner.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per la creazione di script ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>bordo</td>
   <td>L'oggetto border descrive il bordo che circonda l'oggetto checkButton. </td>
   <td>Le modifiche si riflettono nel modello e sono disponibili per la creazione di script ma non vengono sincronizzate con gli elementi HTML. Pertanto, le modifiche non vengono riportate nell’interfaccia utente.<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<br /> </strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>bordo</td>
   <td>L'oggetto border descrive il bordo che circonda l'oggetto choiceList.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| bordo | L&#39;oggetto border descrive il bordo che circonda l&#39;oggetto dateTimeEdit. |  |

## Immagine {#image}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>Specifica il tipo di contenuto nel documento di riferimento, espresso come tipo MIME.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>name<br /> </td>
   <td>Identificatore utilizzato per identificare questo elemento nelle espressioni di script.</td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| bordo | L&#39;oggetto border descrive il bordo che circonda l&#39;oggetto imageEdit. |  |

## numericEdit {#numericedit}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| bordo | L&#39;oggetto border descrive il bordo che circonda un oggetto. | nessuno |

## oggetto {#object}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>Determina il nome della classe dell'oggetto.<br /> </td>
   <td>nessuno</td>
  </tr>
 </tbody>
</table>

## rettangolo {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>spigolo</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o di un rettangolo.<br /> </td>
   <td>Attributi come colore, cap e altro non sono supportati.</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>bordo</td>
   <td>L'oggetto border descrive il bordo che circonda un oggetto.<br /> </td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>layout</td>
   <td>Specifica la strategia di layout da utilizzare per l'oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>bordo</td>
   <td>Specifica il bordo che circonda il campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>obbligatorio</td>
   <td>Specifica il valore nullTest per il campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Specifica il valore del colore del bordo per questo campo. È necessario definire un bordo prima di modificare il colore mediante script.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>Specifica lo spessore del bordo del campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Misurazione dell'altezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>transitorio</td>
   <td>Specifica se l’applicazione di elaborazione deve salvare il valore del gruppo di esclusione come parte di un’operazione di invio o salvataggio di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>l</td>
   <td>Misurazione che specifica la larghezza del layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Specifica la coordinata x del punto di ancoraggio del contenitore rispetto all'angolo superiore sinistro del contenitore padre quando posizionato con il layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Specifica la coordinata y del punto di ancoraggio di un contenitore rispetto all'angolo superiore sinistro del contenitore padre quando posizionato con il layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>L'oggetto caption descrive un'etichetta descrittiva associata a un oggetto di progettazione del modulo.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>convalida</td>
   <td>L'oggetto validate controlla la convalida dei dati forniti dall'utente in un modulo. L’oggetto di convalida può essere attivato più volte durante la durata di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>Ottiene il nodo dati a cui è associato un nodo modulo dopo l'unione.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>presenza</td>
   <td>Specifica la visibilità di un oggetto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>accesso</td>
   <td>Controlla l'accesso dell'utente al contenuto di un oggetto contenitore, ad esempio una sottomaschera.</td>
   <td>Per i singoli elementi nell'exclgrp, restituisce sempre aperto. </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Specifica un identificatore che può essere utilizzato per specificare questo oggetto o evento nelle espressioni di script.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>membri</td>
   <td>Specifica i membri del gruppo di esclusione. </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>Restituisce il membro selezionato di un gruppo di esclusione.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>Esegue tutti gli script sull'evento di calcolo dell'oggetto specificato e tutti gli oggetti figlio.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>calcola</td>
   <td>L’oggetto di calcolo controlla il calcolo del valore di un campo.<br /> </td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## arco {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<strong></strong></strong></td>
   <td><strong>Descrizione<strong></strong></strong></td>
   <td><strong>Eccezione<strong></strong></strong></td>
  </tr>
  <tr>
   <td>spigolo</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o di un rettangolo.<br /> </td>
   <td>Attributi come colore, cap e altro non sono supportati. </td>
  </tr>
 </tbody>
</table>

## bordo {#border}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<strong></strong></strong></td>
   <td><strong>Descrizione<strong></strong></strong></td>
   <td><strong>Eccezione<strong></strong></strong></td>
  </tr>
  <tr>
   <td>spigolo</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o di un rettangolo.<br /> </td>
   <td>Attributi come colore, cap e altro non sono supportati. </td>
  </tr>
 </tbody>
</table>

## $layout {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>Determina l'altezza di un determinato oggetto di progettazione del modulo.<br /> </td>
   <td>
    <ul>
     <li>La proprietà Height (h) non è supportata per l'area pagina e l'area contenuto. </li>
     <li>Il parametro 'Offset dalla prima area di contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>l</td>
   <td>Determina la larghezza di un determinato oggetto di progettazione del modulo.</td>
   <td>
    <ul>
     <li>La proprietà Width (w) non è supportata per l'area pagina e l'area contenuto. </li>
     <li>Il parametro 'Offset dalla prima area di contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>Determina la coordinata x di un determinato oggetto di progettazione modulo rispetto al relativo oggetto padre.</td>
   <td>
    <ul>
     <li>la proprietà della coordinata x (x) non è supportata per l'area pagina e l'area contenuto. </li>
     <li>Il parametro 'Offset dalla prima area di contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>Determina la coordinata y di un determinato oggetto di progettazione modulo rispetto al relativo oggetto padre.</td>
   <td>
    <ul>
     <li>La proprietà della coordinata y (y) non è supportata per l'area pagina e l'area contenuto. </li>
     <li>Il parametro 'Offset dalla prima area di contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>Determina il numero di pagine del modulo corrente.</td>
   <td>
    <ul>
     <li>Il metodo layout.pageCount() restituisce valori diversi per i moduli PDF e HTML.</li>
     <li>Quando si diminuisce il conteggio delle pagine nascondendo un oggetto, il metodo abspagecount restituisce un valore errato.<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>Recupera i tipi di oggetti di progettazione di un modulo da una pagina specificata di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>Determina il numero di pagine del modulo corrente.</td>
   <td>
    <ul>
     <li>Il metodo layout.pageCount() restituisce valori diversi per i moduli PDF e HTML.</li>
     <li>Quando si diminuisce il conteggio delle pagine nascondendo un oggetto, il metodo abspagecount restituisce un valore errato.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## elementi {#items}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| presenza | Specifica la visibilità di un oggetto. | Nessuno |

## FormCalc {#formcalc}

FormCalc è un linguaggio specifico di XFA per la creazione di logiche e radici di calcolo incentrate sui moduli elettronici. FormCalculation fornisce un potente set di funzioni di generazione.

### Funzioni supportate da FormCalc {#formcalc-supported-functions}

### Supporto espressioni FormCalc {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>Categoria </strong></td>
   <td><strong>Descrizione </strong></td>
   <td><strong>Esempio </strong></td>
  </tr>
  <tr>
   <td>Espressione semplice</td>
   <td>Aggiungi, sottrai, moltiplica, divide e parentesi</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>Dichiarazione variabile</td>
   <td>Definire una variabile</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>Espressione logica</td>
   <td>
    <ul>
     <li>Logica (e/o)</li>
     <li>Confronto (maggiore/minore/uguale)</li>
    </ul> </td>
   <td>A o 1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A o 1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>Espressione If</td>
   <td><br type="_moz" /> </td>
   <td>se (a&gt;b) allora 2 endif</td>
  </tr>
  <tr>
   <td>durante</td>
   <td><br type="_moz" /> </td>
   <td>mentre (i lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>per</td>
   <td><br type="_moz" /> </td>
   <td>per i = 100 fino a 1 <br /> do s = s + i end for</td>
  </tr>
  <tr>
   <td>per ogni</td>
   <td><br type="_moz" /> </td>
   <td>per ogni i in (1, 2, 3) <br /> do s = s + i end for</td>
  </tr>
  <tr>
   <td>dichiarazione di funzione</td>
   <td>Definire una funzione personalizzata in FormCalc</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Supporto API di Acrobat {#acrobat-api-support}

1. **Funzioni aritmetiche**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. Conteggio()
   1. Floor()
   1. Max()
   1. Min()
   1. Mod()
   1. Arrotonda()
   1. Somma()

1. **Funzioni scientifiche**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Cannella()
   1. Exp()
   1. Registro()
   1. Poa()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **Funzioni finanziarie**

   1. Apr()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. Termine()

1. **Funzioni logiche**

   1. Scegli()
   1. If()
   1. Oneof()
   1. In()

1. **Funzioni stringa**

   1. In/il()
   1. Concat()
   1. A sinistra()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. Sostituisci()
   1. A destra()
   1. Rtrim()
   1. Spazio()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **Data e ora**

   1. Data()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Aberrazione</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>Questa API acrobat esegue il dump dell’output nella console JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>Questa API acrobat invia un messaggio di avviso tramite popup JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>Fa sì che il sistema riproduca un suono.</td>
   <td>Non viene eseguita alcuna azione.</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>Visualizza una finestra di dialogo modale. Le finestre di dialogo modali devono essere chiuse dall'utente prima che l'applicazione host possa essere riutilizzata direttamente.</td>
   <td>Non viene eseguita alcuna azione.<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>Avvia un URL in una finestra del browser.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>Specifica uno script JavaScript e un periodo di tempo. Lo script viene eseguito ogni volta che viene trascorso il periodo. Il valore restituito da questo metodo deve essere contenuto in una variabile JavaScript. In caso contrario, l'oggetto intervallo è soggetto a Garbage Collection, che causerebbe l'arresto dell'orologio. Per terminare l'esecuzione periodica, passare l'oggetto intervallo restituito a clearInterval.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>Specifica uno script JavaScript e un periodo di tempo. Lo script viene eseguito una sola volta, dopo la scadenza del periodo. Il valore restituito di questo metodo deve essere contenuto in una variabile JavaScript. In caso contrario, l’oggetto timeout è soggetto a Garbage Collection, che causerebbe l’arresto dell’orologio. Per annullare l'evento timeout, passare l'oggetto timeout restituito a clearTimeOut.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>Annulla un intervallo registrato in precedenza inizialmente impostato dal metodo setInterval.</td>
   <td>Nei moduli di HTML5, l’API non funziona correttamente.</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>Annulla un intervallo di timeout registrato in precedenza. Tale intervallo viene inizialmente impostato da setTimeOut.</td>
   <td>Nei moduli di HTML5, l’API non funziona correttamente.<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>Esegue uno script specificato.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>Matrice contenente l'oggetto Doc per ogni documento attivo. Se non è attivo alcun documento, activeDocs non restituisce alcun risultato, ovvero ha lo stesso comportamento di d = new Array(0) in JavaScript di base.</td>
   <td>Restituisce una matrice vuota per i moduli HTMl5.</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>Se è true (valore predefinito), è possibile eseguire i calcoli. Se false, i calcoli non sono consentiti.</td>
   <td>Sempre true per Forms HTMl5.</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>Oggetto wrapper per contenere vari valori costanti. Attualmente, questa proprietà restituisce un oggetto con una singola proprietà, align.</td>
   <td>I moduli HTML5 restituiscono un oggetto align vuoto.</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>Attiva e disattiva il rettangolo di attivazione. Il rettangolo di attivazione è costituito da una linea punteggiata debole attorno a pulsanti, caselle di controllo, pulsanti di scelta e firme per indicare che il campo modulo è attivo da tastiera. Il valore true attiva il rettangolo di attivazione.</td>
   <td>Sempre true per i moduli HTML5.</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>Il numero di versione del software del visualizzatore moduli. Selezionare questa proprietà per determinare se sono disponibili oggetti, proprietà o metodi nelle versioni più recenti del software se si desidera mantenere la compatibilità con le versioni precedenti negli script.</td>
   <td>11.001 sempre.</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>Lingua del visualizzatore Acrobat in esecuzione.</td>
   <td>Sempre "ENU" per moduli HTMl5.</td>
  </tr>
 </tbody>
</table>

## Eventi XFA supportati {#supported-xfa-events}

Sono supportati i seguenti eventi XFA lato client:

* Inizializza
* Convalida
* Calcola
* Fai clic su
* Inserisci
* Esci
* Cambia
* ValidationState

>[!NOTE]
>
>I moduli HTML5 vengono sottoposti a rendering sul lato client (browser). Usa lato client **convalida** e **calcola** script anziché script lato server.
