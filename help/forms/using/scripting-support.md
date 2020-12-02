---
title: Supporto degli script per i moduli HTML5
seo-title: Supporto degli script per i moduli HTML5
description: JavaScript, proprietà FormCalc e altri metodi supportati in HTML5 Forms.
seo-description: JavaScript, proprietà FormCalc e altri metodi supportati in HTML5 Forms.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '3909'
ht-degree: 36%

---


# Supporto degli script per i moduli HTML5 {#scripting-support-for-html-forms}

I metodi e le proprietà JavaScript, FormCalc supportati nei moduli HTML5 sono elencati di seguito:

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
   <td>Specifica il contenuto del campo prima che venga modificato in risposta alle azioni dell'utente. Questo valore può essere richiamato, in modo simile a una funzione di annullamento.</td>
   <td><p>Non funziona per i menu a discesa e le caselle di riepilogo. <code>PrevText </code>non funziona correttamente per i seguenti casi:</p>
    <ul>
     <li>Digitando alcune chiavi carattere speciali (ad esempio $, (,), &amp;, @ e altro) nei campi numerici dell'iPad e </li>
     <li>Per il campo Data (quando la data viene immessa attraverso il calendario).<br /> </li>
    </ul> <p>L'impostazione del valore tramite script non è supportata.</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>Specifica l'oggetto sul quale l'evento agisce.</td>
   <td>L'impostazione del valore tramite script non è supportata.<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>Specifica il contenuto del campo dopo che questo è stato modificato in risposta alle azioni dell'utente.</td>
   <td><p>La proprietà <code>newText</code> non funziona correttamente per i seguenti casi:</p>
    <ul>
     <li>Selezione e sostituzione dei testi</li>
     <li>Eliminando, copiando e incollando i testi.</li>
     <li>Digitando alcune chiavi carattere speciali (ad esempio $, (, ), &amp;, @ e altro) nei campi numerici<br /> </li>
     <li>Utilizzo di Maiusc+combinazione alfanumerica. </li>
     <li>Quando si utilizzano i campi data/ora.</li>
    </ul>
    <div>
      L'impostazione del valore tramite script non è supportata.
    </div> </td>
  </tr>
  <tr>
   <td>change</td>
   <td>Specifica il valore che l'utente digita o incolla in un campo immediatamente dopo avere eseguito l'azione. </td>
   <td><p>La proprietà change non funziona correttamente per i casi seguenti:</p>
    <ul>
     <li>Selezione e sostituzione dei testi</li>
     <li>Eliminando, copiando e incollando i testi.</li>
     <li>Digitando alcune chiavi carattere speciali (ad esempio $, (,), &amp;, @ e altro) nei campi numerici<br /> </li>
     <li>Utilizzo di Maiusc+combinazione alfanumerica. </li>
     <li>Quando si utilizzano i campi data/ora.</li>
    </ul> <p>L'impostazione del valore tramite script non è supportata.</p> </td>
  </tr>
  <tr>
   <td>keydown</td>
   <td>Determina se l'utente sta premendo un tasto di direzione per eseguire una selezione. Questa proprietà è disponibile solo per le caselle di riepilogo e per gli elenchi a discesa.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>modifier</td>
   <td>Determina se il tasto modificatore (ad esempio, Ctrl in Microsoft® Windows®) viene tenuto premuto durante l'esecuzione di un particolare evento.</td>
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
   <td>Restituisce il tipo di applicazione dell'host. Disponibile solo per le applicazioni client.</td>
   <td>Valore restituito <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Restituisce il nome dell'applicazione corrente.</td>
   <td>Restituisce il nome e la versione del browser. Ad esempio, nel browser Chrome, il valore restituito è <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>Restituisce il numero di pagine nel documento.</td>
   <td>I criteri di impaginazione dei moduli HTML5 non sono identici ai criteri di impaginazione degli PDF forms. Pertanto, l'API numPages può restituire valori diversi in entrambi i casi.</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>Restituisce una stringa che rappresenta la piattaforma del computer su cui è in esecuzione lo script.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>Specifica il titolo del documento. È disponibile solo per le applicazioni client.</td>
   <td>Restituisce il titolo del documento HTML nel modulo, anziché il titolo dei metadati del modulo, come nel caso dei PDF forms.</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>Restituisce una stringa che rappresenta il numero di versione dell'applicazione corrente.</td>
   <td>Restituisce la versione del modulo.</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>Specifica se verranno eseguiti gli script di calcolo.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>Specifica se gli script di convalida verranno eseguiti.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>Passa alla pagina precedente.</td>
   <td>I moduli HTML5 non seguono lo stesso criterio di impaginazione del modulo PDF, pertanto la pagina precedente di un modulo HTML5 è diversa dalla pagina precedente di un modulo PDF.</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>Consente di passare alla pagina successiva di un modulo. Utilizzare il metodo pageDown in fase di esecuzione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>Imposta lo stato attivo sul campo specificato. Il campo è specificato come oggetto o dall'espressione SOM del campo. È disponibile solo per le applicazioni client.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>Ripristina i valori predefiniti di tutti i campi all'interno di un documento.</td>
   <td>Cancella tutti i dati di un modulo con dati uniti, anziché ripristinarli ai valori predefiniti.</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>Visualizza una finestra di dialogo sullo schermo. È disponibile solo per le applicazioni client</td>
   <td>La casella del messaggio di tipo Sì/No è convertita in OK/Annulla. La finestra di messaggio con tre pulsanti non è supportata.</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>Imposta la pagina attualmente attiva di un documento in fase di esecuzione.</p> <p>I valori della pagina sono basati su 0, dunque la prima pagina di un documento restituisce un valore pari a 0.</p> <p>La proprietà currentPage è disponibile quando layout:ready viene eseguito su un client. Non è invece disponibile quando layout:ready viene eseguito sul server in quanto la proprietà non viene eseguita fino a quando viene eseguito il layout del modulo.</p> </td>
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
   <td>Controlla la partecipazione dell'oggetto associato nelle diverse fasi di elaborazione. Se l'oggetto è un contenitore, il contenuto del contenitore eredita le restrizioni applicate dal controllo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>Controlla l'accesso degli utenti ai contenuti.</td>
   <td>Non funziona per il gruppo di esclusione. Inoltre, i moduli HTML5 offrono lo stesso trattamento agli oggetti non interattivi e protetti.<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Identificatore utilizzato per identificare questo elemento nelle espressioni di script.</td>
   <td>I moduli HTML5 non consentono l'impostazione della proprietà name per gli oggetti. È una proprietà di sola lettura per i moduli HTML5.</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>Elemento di contenuto che racchiude una singola unità di contenuto dati.</td>
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
   <td>L'impostazione di <code>formattedValue</code> tramite script non è supportata.</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>Specifica il valore di modifica per questo campo.</td>
   <td>L'impostazione dello script <code>editValue </code>through non è supportata.</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>Specifica la stringa del messaggio di convalida del formato per il campo.</td>
   <td>L'impostazione dello script <code>formatMessage </code>through non è supportata.</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>Specifica il valore del colore di sfondo per il campo. È necessario impostare la proprietà border.fill.presence su visibile separatamente.</td>
   <td>Non restituisce correttamente il colore predefinito del campo.</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>L'oggetto border descrive i bordi che circondano un oggetto.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>L'oggetto ui racchiude la descrizione dell'interfaccia utente di un oggetto modulo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>Specifica il valore nullTest per il campo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>Specifica il valore del colore dei bordi per questo campo. È necessario impostare la proprietà border.edge.presence su visibile separatamente.</td>
   <td>Non restituisce correttamente il colore predefinito del bordo del campo.</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>Numero di elementi nell’elenco.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>Aggiunge nuove voci al campo corrente.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>Rimuove tutte le voci dal campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>Ottiene il valore associato di una specifica voce di visualizzazione di un elenco a discesa o di una casella di riepilogo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>Esegue lo script calculate del campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>Esegue lo script validate del campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>Esegue lo script di evento dell'oggetto.</td>
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
   <td>Recupera il testo visualizzato dell'elemento per l'indice dell'elemento specificato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>Recupera il valore dei dati per l'indice dell'elemento specificato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>Elimina l'elemento nella posizione di indice specificata.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>Imposta gli elementi specificati nel campo corrente. Sostituisce gli elementi preesistenti.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Misura dell'altezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Misura che specifica la larghezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Specifica la coordinata x del punto di ancoraggio del contenitore, rispetto all'angolo superiore sinistro del contenitore primario, quando viene inserito con un layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Specifica la coordinata y del punto di ancoraggio di un contenitore rispetto all'angolo superiore sinistro del contenitore primario quando viene inserito con un layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>L'oggetto caption descrive un'etichetta associata a un oggetto struttura del modulo.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>L'oggetto validate controlla la convalida dei dati immessi dall'utente in un modulo. L'oggetto validate può essere attivato più volte nella vita di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>Specifica il sottomodulo principale (pagina) del campo.</td>
   <td>Restituisce sempre il sottomodulo principale invece di restituire il primo sottomodulo primario non con ambito.<br /> </td>
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
| formNodes | Restituisce un elenco di tutti gli oggetti struttura del modulo associati ad uno specifico oggetto dati. |  |

## InstanceManager {#instancemanager}

| Proprietà | Descrizione |
|---|---|
| `name` | Identificatore utilizzato per identificare questo elemento nelle espressioni di script. |
| `occur` | Descrive i vincoli relativi al numero di istanze consentite per il relativo contenitore di inclusione. |
| `min` | Specifica il numero minimo di istanze su cui è possibile creare un&#39;istanza. |
| `max` | Specifica il numero massimo di istanze che è possibile creare. |
| `count` | Specifica il numero corrente di istanze create. |
| `setInstances` | Aggiunge o rimuove da questo nodo i sottomoduli o i set di sottomoduli specificati. |
| `addInstance` | Aggiunge al nodo una nuova istanza di un sottomodulo o di un set di sottomoduli. |
| `removeInstance` | Rimuove un sottomodulo o un set di sottomoduli da questo nodo. |
| `moveInstance` | Sposta un oggetto secondario di un oggetto modello di modulo in un&#39;altra posizione specificata all&#39;interno del modello di modulo. Anche le informazioni del modello dati corrispondente per l&#39;oggetto vengono spostate all&#39;interno del modello dati. |
| `insertInstance` | Inserisce una nuova istanza di un sottomodulo o di un set di sottomoduli in questo nodo. |

## elenco {#list}

| Proprietà | Descrizione |
|---|---|
| `length` | Il numero di elementi nell&#39;elenco. |
| `item` | Indice basato su zero nell&#39;insieme. |
| `append` | Aggiunge un nodo alla fine dell&#39;elenco di nodi. |
| `remove` | Rimuove un nodo da un elenco di nodi. |
| `insert` | Inserisce un nodo prima di un nodo specifico nell&#39;elenco dei nodi. |

## nodo {#node}

| Proprietà | Descrizione | Eccezione |
|---|---|---|
| createNode | Crea un nuovo nodo in base a un nome di classe valido. | Nessuno |
| `isContainer` | Specifica se l&#39;oggetto è un oggetto contenitore. | Nessuno |
| `isNull` | Indica se il valore corrente dei dati è un valore null. | Nessuno |
| `resolveNode` | Valuta l&#39;espressione SOM specificata, a partire dall&#39;oggetto modello di oggetto modulo XML corrente, e restituisce il valore dell&#39;oggetto specificato nell&#39;espressione SOM. | Nessuno |
| `resolveNodes` | Valuta l&#39;espressione SOM specificata, a partire dall&#39;oggetto modello di oggetto modulo XML corrente, e restituisce il valore dell&#39;oggetto specificato nell&#39;espressione SOM. | Nessuno |
| oneOfChild | Crea un nuovo nodo in base a un nome di classe valido. | Nessuno |
| getElement | Restituisce un oggetto secondario specificato. | Nessuno |
| getAttribute | Ottiene il valore di una proprietà specificata. | Nessuno |
| setAttribute | Imposta il valore della proprietà specificata. | Nessuno |

## modello {#model}

| Proprietà | Descrizione | Eccezione |
|---|---|---|
| NA | NA | NA |

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
   <td>Esegue lo script di evento dell'oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>Restituisce un elenco dei nodi contenuti nel sottomodulo (incluso) che non hanno superato il test di convalida.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>border</td>
   <td>L'oggetto border descrive i bordi che circondano un oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Specifica il valore del colore dei bordi per questo campo. È necessario impostare la proprietà border.edge.presence su visibile separatamente.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Misura dell'altezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Misura che specifica la larghezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Specifica la coordinata x del punto di ancoraggio del contenitore, rispetto all'angolo superiore sinistro del contenitore primario, quando viene inserito con un layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Specifica la coordinata y del punto di ancoraggio di un contenitore rispetto all'angolo superiore sinistro del contenitore primario quando viene inserito con un layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>L'oggetto validate controlla la convalida dei dati immessi dall'utente in un modulo. L'oggetto validate può essere attivato più volte nella vita di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Identificatore utilizzato per identificare questo elemento nelle espressioni di script.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>presence (presenza)</td>
   <td>Specifica la visibilità dell'oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controlla l’accesso degli utenti al contenuto di un contenitore. ad esempio un sottomodulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>Calcola l'indice di un sottomodulo o di un set di sottomoduli in base alla sua posizione rispetto alle altre istanze dello stesso oggetto modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>L'oggetto instanceManager gestisce la creazione delle istanze, la rimozione e lo spostamento degli oggetti struttura del modulo.<br /> </td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

### submit {#submit}

| Proprietà | Descrizione |
|---|---|
| target | L&#39;URL a cui vengono inviati i dati. L&#39;omissione di questo attributo implica che l&#39;applicazione di elaborazione XFA ottiene l&#39;URI utilizzando una tecnica specifica per il prodotto, come l&#39;accesso alle informazioni specifiche per il prodotto nell&#39;oggetto config. |

## struttura {#tree}

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
   <th>Eccezione</th>
  </tr>
  <tr>
   <td>nodes</td>
   <td>Restituisce un elenco di tutti gli oggetti secondari dell'oggetto corrente.</td>
   <td>
    <ul>
     <li>Non supportato per xfa.nodes, desc</li>
     <li>Il numero di nodi segnalati per PDF e HTML è diverso. </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Specifica il nome del nodo.</td>
   <td>L'impostazione del nome tramite script non è consentita in HTML.</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>Ottiene l'elemento padre per questo nodo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>index</td>
   <td>Restituisce la posizione di questo nodo nel relativo insieme di nodi di relazione omonimi, in-scope, simili a quelli secondari.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>Ottiene l'espressione SOM per questo nodo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>Valuta l'espressione SOM specificata, a partire dall'oggetto modello di oggetto modulo XML corrente, e restituisce il valore dell'oggetto specificato nell'espressione SOM.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>Valuta l'espressione SOM specificata, a partire dall'oggetto modello di oggetto modulo XML corrente, e restituisce il valore dell'oggetto specificato nell'espressione SOM.</td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| Proprietà | Descrizione | Eccezione |
|---|---|---|
| instanceManager | L&#39;oggetto instanceManager gestisce la creazione delle istanze, la rimozione e lo spostamento degli oggetti struttura del modulo. | Nessuno |

## content {#content}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| isNull | Indica se il valore corrente dei dati è il valore null. |  |

## dataValue {#datavalue}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| isNull | Indica se il valore corrente dei dati è il valore null. |  |

## edge {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà </strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto pattern.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## fill {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>Le proprietà del colore definiscono un colore di riempimento univoco.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## linear {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La proprietà color descrive un colore univoco per un riempimento con sfumatura lineare su un modulo.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## line {#line}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o rettangolo.<br /> </td>
   <td>Attributi come colore, cappuccio e altro non sono supportati.<br /> </td>
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
   <td>color</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto pattern. </td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## radial {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto radiale</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## stipple {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto stipple.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell’interfaccia utente.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>Proprietà</td>
   <td>Descrizione</td>
   <td>Eccezione</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>L'oggetto ui racchiude la descrizione dell'interfaccia utente di un oggetto modulo.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>didascalia</td>
   <td>L'oggetto caption descrive un'etichetta associata a un oggetto struttura del modulo.</td>
   <td> </td>
  </tr>
  <tr>
   <td>presence (presenza)</td>
   <td>Specifica la visibilità dell'oggetto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Specifica un identificatore che può essere utilizzato per specificare questo oggetto o evento nelle espressioni di script.</td>
   <td>L'impostazione del valore in fase di esecuzione non è supportata</td>
  </tr>
  <tr>
   <td>valore</td>
   <td>L'oggetto value racchiude una singola unità di contenuto dati.<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## corner {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La proprietà color descrive un colore univoco per l'oggetto corner.</td>
   <td>
    <ul>
     <li>Impossibile recuperare il valore predefinito. </li>
     <li>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell’interfaccia utente.</li>
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
   <td>border</td>
   <td>L'oggetto border descrive il bordo intorno all'oggetto checkButton. </td>
   <td>Le modifiche si riflettono nel modello e sono disponibili per lo scripting, ma non sono sincronizzate con gli elementi HTML. Di conseguenza, le modifiche non vengono riportate nell'interfaccia utente.<br /> </td>
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
   <td>border</td>
   <td>L'oggetto border descrive il bordo intorno all'oggetto choiceList.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| border | L&#39;oggetto border descrive il bordo intorno all&#39;oggetto dateTimeEdit. |  |

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
   <td>Specifica il tipo di contenuto del documento a cui viene fatto riferimento, espresso come tipo MIME.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>name<br /> </td>
   <td>Identificatore utilizzato per identificare questo elemento nelle espressioni di script.</td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## imageEdit  {#imageedit}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| border | L&#39;oggetto border descrive il bordo intorno all&#39;oggetto imageEdit. |  |

## numericEdit {#numericedit}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| border | L&#39;oggetto border descrive i bordi che circondano un oggetto. | nessuno |

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
   <td>Determina il nome della classe per l'oggetto.<br /> </td>
   <td>nessuno</td>
  </tr>
 </tbody>
</table>

## rectangle {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Eccezione</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o rettangolo.<br /> </td>
   <td>Gli attributi quali colore, cap e altro non sono supportati.</td>
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
   <td>border</td>
   <td>L'oggetto border descrive i bordi che circondano un oggetto.<br /> </td>
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
   <td>Specifica la strategia di layout da utilizzare con l'oggetto.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>border</td>
   <td>Specifica il bordo intorno al campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td>Specifica il valore nullTest per il campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Specifica il valore del colore del bordo per questo campo. Per poter modificare il colore mediante script, è necessario definire un bordo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>Specifica la larghezza dei bordi per questo campo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Misura dell'altezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>transient</td>
   <td>Specifica se l'applicazione di elaborazione deve salvare il valore del gruppo di esclusione nell'ambito di un'operazione di invio o di salvataggio del modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Misura che specifica la larghezza per il layout.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Specifica la coordinata x del punto di ancoraggio del contenitore, rispetto all'angolo superiore sinistro del contenitore primario, quando viene inserito con un layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Specifica la coordinata y del punto di ancoraggio di un contenitore rispetto all'angolo superiore sinistro del contenitore primario quando viene inserito con un layout posizionato.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>didascalia</td>
   <td>L'oggetto caption descrive un'etichetta associata a un oggetto struttura del modulo.<br /> </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>L'oggetto validate controlla la convalida dei dati immessi dall'utente in un modulo. L'oggetto validate può essere attivato più volte nella vita di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>Ottiene il nodo dei dati a cui viene legato il nodo di un modulo dopo l'unione.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>presence (presenza)</td>
   <td>Specifica la visibilità dell'oggetto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controlla l’accesso degli utenti al contenuto di un contenitore. ad esempio un sottomodulo.</td>
   <td>Per i singoli elementi nell'exclgrp, restituisce sempre open. </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Specifica un identificatore che può essere utilizzato per specificare questo oggetto o evento nelle espressioni di script.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>membri</td>
   <td>Specificare i membri del gruppo di esclusione. </td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>Restituisce il membro selezionato di un gruppo di esclusione.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>Esegue qualsiasi script nell'evento calculate associato all'oggetto specificato e a eventuali oggetti secondari.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>calculate</td>
   <td>L'oggetto calculate controlla il calcolo del valore di un campo.<br /> </td>
   <td>Nessuno</td>
  </tr>
 </tbody>
</table>

## arc {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<strong></strong></strong></td>
   <td><strong>Descrizione<strong></strong></strong></td>
   <td><strong>Eccezione<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o rettangolo.<br /> </td>
   <td>Gli attributi quali colore, cap e altro non sono supportati. </td>
  </tr>
 </tbody>
</table>

## border {#border}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà<strong></strong></strong></td>
   <td><strong>Descrizione<strong></strong></strong></td>
   <td><strong>Eccezione<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>L'oggetto edge descrive un arco, una linea o un lato di un bordo o rettangolo.<br /> </td>
   <td>Gli attributi quali colore, cap e altro non sono supportati. </td>
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
   <td>Determina l'altezza di un dato oggetto struttura del modulo.<br /> </td>
   <td>
    <ul>
     <li>La proprietà Height (h) non è supportata per l'area di pagina e l'area di contenuto. </li>
     <li>Il parametro 'Offset dalla prima area contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>Determina la larghezza dell'oggetto struttura del modulo specificato.</td>
   <td>
    <ul>
     <li>La proprietà Width (w) non è supportata per l'area della pagina e l'area contenuto. </li>
     <li>Il parametro 'Offset dalla prima area contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>Determina la coordinata x dell'oggetto struttura del modulo specificato rispetto all'oggetto principale.</td>
   <td>
    <ul>
     <li>La proprietà coordinata x (x) non è supportata per l'area della pagina e l'area contenuto. </li>
     <li>Il parametro 'Offset dalla prima area contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>Determina la coordinata y dell'oggetto struttura del modulo specificato rispetto all'oggetto principale.</td>
   <td>
    <ul>
     <li>La proprietà coordinata y (y) non è supportata per l'area della pagina e l'area contenuto. </li>
     <li>Il parametro 'Offset dalla prima area contenuto in cui si trova l'oggetto XFA-Form' non è supportato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>Determina il numero di pagine del modulo corrente.</td>
   <td>
    <ul>
     <li>il metodo layout.pageCount() restituisce valori diversi per i moduli PDF e HTML.</li>
     <li>Se il numero di pagine diminuisce nascondendo un oggetto, il metodo abspagecount restituisce un valore non corretto.<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>Recupera vari tipi di oggetti struttura del modulo da una pagina specifica di un modulo.</td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>Determina il conteggio pagine del modulo corrente.</td>
   <td>
    <ul>
     <li>il metodo layout.pageCount() restituisce valori diversi per i moduli PDF e HTML.</li>
     <li>Se il numero di pagine diminuisce nascondendo un oggetto, il metodo abspagecount restituisce un valore non corretto.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## items {#items}

| **Proprietà** | **Descrizione** | **Eccezione** |
|---|---|---|
| presence (presenza) | Specifica la visibilità dell&#39;oggetto. | Nessuno |

## FormCalc {#formcalc}

FormCalc è un linguaggio XFA specifico per la creazione di origini di logica e calcoli incentrati sui moduli elettronici. FormCalculation fornisce un potente set di funzioni di compilazione.

### Funzioni supportate da FormCalc {#formcalc-supported-functions}

### Supporto delle espressioni FormCalc {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>Categoria </strong></td>
   <td><strong>Descrizione </strong></td>
   <td><strong>Esempi </strong></td>
  </tr>
  <tr>
   <td>Espressione semplice</td>
   <td>Aggiungere, sottrarre, moltiplicare, dividere e aggiungere parentesi</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>Dichiarazione della variabile</td>
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
   <td>Espressione if</td>
   <td><br type="_moz" /> </td>
   <td>if (a&gt;b) then 2 endif</td>
  </tr>
  <tr>
   <td>while</td>
   <td><br type="_moz" /> </td>
   <td>while (i lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>per</td>
   <td><br type="_moz" /> </td>
   <td>per i = 100 fino a 1 <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>per ogni</td>
   <td><br type="_moz" /> </td>
   <td>per ogni i in (1, 2, 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>dichiarazione di funzione</td>
   <td>Definire una funzione personalizzata in FormCalc</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

###  Supporto API Acrobat {#acrobat-api-support}

1. **Funzioni aritmetiche**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. Conteggio()
   1. Floor()
   1. Max()
   1. Min()
   1. Mod()
   1. Round()
   1. Somma()

1. **Funzioni scientifiche**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Tan()
   1. Exp()
   1. Registro()
   1. Pow()
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

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **Funzioni stringa**

   1. In/il()
   1. Concat()
   1. Sinistra()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. Sostituisci()
   1. Destra()
   1. Rtrim()
   1. Space()
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
   <td>Questa API acrobat scarica l’output nella console JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>Questa API di acrobat invia un messaggio di avviso tramite la finestra a comparsa JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>Comporta la produzione di un segnale sonoro da parte del sistema.</td>
   <td>Non viene eseguita alcuna azione.</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>Visualizza una finestra di dialogo modale per l'utente. Le finestre di dialogo modali devono essere chiuse dall'utente prima che l'applicazione host possa essere nuovamente utilizzata direttamente.</td>
   <td>Nessuna azione eseguita.<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>Avvia un URL in una finestra del browser.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>Specifica uno script JavaScript e un periodo di tempo. Lo script viene eseguito ogni volta che termina il periodo. Il valore restituito da questo metodo deve essere mantenuto in una variabile JavaScript. In caso contrario, l'oggetto intervallo è soggetto alla raccolta dei rifiuti, il che causerebbe l'arresto dell'orologio. Per terminare l'esecuzione periodica, passare l'oggetto intervallo restituito a clearInterval.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>Specifica uno script JavaScript e un periodo di tempo. Lo script viene eseguito una sola volta, dopo la scadenza del periodo. Il valore restituito da questo metodo deve essere mantenuto in una variabile JavaScript. In caso contrario, l'oggetto timeout è soggetto alla raccolta dei rifiuti, che causerebbe l'arresto dell'orologio. Per annullare l'evento timeout, passare l'oggetto timeout restituito a clearTimeOut.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>Annulla un intervallo registrato in precedenza impostato inizialmente dal metodo setInterval.</td>
   <td>Nei moduli HTML5 l'API non funziona correttamente.</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>Annulla un intervallo di timeout precedentemente registrato. Tale intervallo viene inizialmente impostato da setTimeOut.</td>
   <td>Nei moduli HTML5 l'API non funziona correttamente.<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>Esegue uno script specificato.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>Un array contenente l'oggetto Doc per ciascun documento attivo. Se non sono attivi documenti, activeDocs non restituisce nulla; ovvero ha lo stesso comportamento di d = nuovo Array(0) nel codice JavaScript di base.</td>
   <td>Restituisce un array vuoto per i moduli HTMl5.</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>Se true (il valore predefinito), è possibile eseguire i calcoli. Se false, i calcoli non sono consentiti.</td>
   <td>Sempre true per HTMl5 Forms.</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>Un oggetto wrapper che contiene vari valori costanti. Attualmente, questa proprietà restituisce un oggetto con una singola proprietà, align.</td>
   <td>I moduli HTML5 restituiscono un oggetto align vuoto.</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>Attiva e disattiva il rettangolo di selezione. Il rettangolo di attivazione è costituito dalla debole linea punteggiata intorno a pulsanti, caselle di controllo, pulsanti di scelta e firme per indicare che il campo modulo è attivo. Il valore true attiva il rettangolo di selezione.</td>
   <td>Sempre true per i moduli HTML5.</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>Il numero di versione del software per moduli visualizzatore. Selezionare questa proprietà per determinare se sono disponibili oggetti, proprietà o metodi nelle versioni più recenti del software per mantenere la compatibilità con le versioni precedenti degli script.</td>
   <td>11.001 sempre.</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>Lingua del visualizzatore  Acrobat in esecuzione.</td>
   <td>Sempre "ENU" per i moduli HTMl5.</td>
  </tr>
 </tbody>
</table>

## Eventi XFA supportati {#supported-xfa-events}

Sono supportati i seguenti eventi XFA lato client:

* Inizializza
* Convalida
* Calcola
* Clic
* Invio
* Esci
* Cambia
* ValidationState

>[!NOTE]
>
>Il rendering dei moduli HTML5 viene eseguito sul lato client (browser). Si consiglia di utilizzare script sul lato client **validate** e **calculate** invece di script sul lato server.
