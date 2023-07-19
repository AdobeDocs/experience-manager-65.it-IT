---
title: Modelli di pagina - Statici
description: Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
source-git-commit: 2810e34f642f4643fa4dc24b31a57a68e9194e39
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 1%

---

# Modelli di pagina - Statici{#page-templates-static}

Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato. Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Ogni Modello presenta una selezione di componenti disponibili per l’uso.

* I modelli sono costituiti da [Componenti](/help/sites-developing/components.md);
* I componenti utilizzano i widget e ne consentono l’accesso; questi vengono utilizzati per eseguire il rendering del contenuto.

>[!NOTE]
>
>[Modelli modificabili](/help/sites-developing/page-templates-editable.md) sono anche disponibili e sono il tipo di modelli consigliato per la maggior parte della flessibilità e le funzioni più recenti.

## Proprietà e nodi figlio di un modello {#properties-and-child-nodes-of-a-template}

Un modello è un nodo di tipo cq:Template e presenta le seguenti proprietà e nodi figlio:

<table>
 <tbody>
  <tr>
   <td><strong>Nome <br /> </strong></td>
   <td><strong>Tipo <br /> </strong></td>
   <td><strong>Descrizione <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>Modello corrente. Un modello è di tipo nodo cq:Template.<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> Stringa[]</td>
   <td>Percorso di un modello che può essere figlio di questo modello.<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> Stringa[]</td>
   <td>Percorso di un modello che può essere padre di questo modello.<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> Stringa[]</td>
   <td>Percorso di una pagina che può essere basata su questo modello.<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> Data</td>
   <td>Data di creazione del modello.<br /> </td>
  </tr>
  <tr>
   <td> jcr:descrizione</td>
   <td> Stringa</td>
   <td>Descrizione del modello.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> Stringa</td>
   <td>Titolo del modello.<br /> </td>
  </tr>
  <tr>
   <td> classificazione</td>
   <td> Lungo</td>
   <td>Classificazione del modello. Utilizzato per visualizzare il modello nell’interfaccia utente.<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>Nodo contenente il contenuto del modello.<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:file</td>
   <td>Miniatura del modello.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:file</td>
   <td>Icona del modello.<br /> </td>
  </tr>
 </tbody>
</table>

Un modello è la base di una pagina.

Per creare una pagina, è necessario copiare il modello (albero dei nodi) `/apps/<myapp>/template/<mytemplate>`) alla posizione corrispondente nella struttura del sito: questo è ciò che accade se una pagina viene creata utilizzando **Siti Web** scheda.

Questa azione di copia fornisce anche alla pagina il suo contenuto iniziale (in genere solo Contenuto di primo livello) e la proprietà sling:resourceType, il percorso del componente pagina utilizzato per il rendering della pagina (tutto ciò che si trova nel nodo figlio jcr:content).

## Struttura dei modelli {#how-templates-are-structured}

Vi sono due aspetti da considerare:

* la struttura del modello stesso
* la struttura del contenuto prodotto quando viene utilizzato un modello

### Struttura di un modello {#the-structure-of-a-template}

Un modello viene creato sotto un nodo di tipo **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

È possibile impostare varie proprietà, in particolare:

* **jcr:title** - titolo del modello; viene visualizzato nella finestra di dialogo durante la creazione di una pagina.
* **jcr:descrizione** : descrizione del modello; viene visualizzata nella finestra di dialogo durante la creazione di una pagina.

Questo nodo contiene un nodo jcr:content (cq:PageContent) che viene utilizzato come base per il nodo del contenuto delle pagine risultanti; questo fa riferimento, utilizzando sling:resourceType, al componente da utilizzare per il rendering del contenuto effettivo di una nuova pagina.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Questo componente viene utilizzato per definire la struttura del contenuto quando viene creata una nuova pagina.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### Contenuto prodotto da un modello {#the-content-produced-by-a-template}

I modelli vengono utilizzati per creare pagine di tipo `cq:Page` (come accennato in precedenza, una pagina è un tipo speciale di componente). Ogni pagina AEM ha un nodo strutturato `jcr:content`. Tale comportamento:

* è di tipo cq:PageContent
* è un tipo di nodo strutturato contenente una definizione di contenuto definita
* ha una proprietà `sling:resourceType` per fare riferimento al componente contenente gli script sling utilizzati per il rendering del contenuto

### Modelli predefiniti {#default-templates}

AEM viene fornito con vari modelli predefiniti disponibili. A volte può essere utile utilizzare i modelli così come sono. In tal caso, è necessario assicurarsi che il modello sia disponibile per il sito Web.

Ad esempio, l’AEM viene fornito con diversi modelli, tra cui una pagina di contenuto e una pagina Home.

| **Titolo** | **Component** | **Dove si trova** | **Scopo** |
|---|---|---|---|
| Home page | homepage | geometrix | Il modello della home page del Geometrixx. |
| Pagina contenuto | contentpage | geometrix | Il modello della pagina di contenuto del Geometrixx. |

#### Visualizzazione dei modelli predefiniti {#displaying-default-templates}

Per visualizzare un elenco di tutti i modelli nel repository, procedere come segue:

1. In CRXDE Lite, apri **Strumenti** e fai clic su **Query**.

1. Nella scheda Query
1. As **Tipo**, seleziona **XPath**.

1. In **Query** campo di input, immetti la seguente stringa: //element(&#42;, cq:Template)

1. Clic **Esegui**. L&#39;elenco viene visualizzato nella casella dei risultati.

Di solito, si prende un modello esistente e ne si sviluppa uno nuovo per il proprio uso. Consulta [Sviluppo di modelli di pagina](#developing-page-templates) per ulteriori informazioni.

Per attivare un modello esistente per il sito Web e si desidera che venga visualizzato nel **Crea pagina** durante la creazione di una pagina direttamente in **Siti Web** dal **Siti Web** , impostare la proprietà allowedPaths del nodo modello su: **/content(/.&#42;)?**

## Applicazione delle progettazioni dei modelli {#how-template-designs-are-applied}

Quando gli stili vengono definiti nell’interfaccia utente tramite [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md), la progettazione viene mantenuta nel percorso esatto del nodo di contenuto per il quale viene definito lo stile.

>[!CAUTION]
>
>L’Adobe consiglia di applicare le progettazioni solo tramite [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md).
>
>La modifica dei progetti in CRXDE Lite, ad esempio, non è una best practice e l’applicazione di tali progetti può variare rispetto al comportamento previsto.

Se le progettazioni vengono applicate solo utilizzando la modalità Progettazione, le sezioni seguenti [Risoluzione percorso progettazione](/help/sites-developing/page-templates-static.md#design-path-resolution), [Albero decisionale](/help/sites-developing/page-templates-static.md#decision-tree)e [Esempio](/help/sites-developing/page-templates-static.md#example) non sono applicabili.

### Risoluzione percorso progettazione {#design-path-resolution}

Quando si esegue il rendering del contenuto basato su un modello statico, AEM tenta di applicare la progettazione e gli stili più rilevanti al contenuto in base a un attraversamento della gerarchia dei contenuti.

L’AEM determina lo stile più rilevante per un nodo di contenuto nel seguente ordine:

* Se è presente una progettazione per il percorso completo ed esatto del nodo di contenuto (come quando la progettazione è definita in modalità Progettazione), utilizza tale progettazione.
* Se è presente una progettazione per il nodo di contenuto dell’elemento padre, utilizza tale progettazione.
* Se esiste una progettazione per qualsiasi nodo sul percorso del nodo di contenuto, utilizza tale progettazione.

Negli ultimi due casi, se è presente più di una progettazione applicabile, utilizza quella più vicina al nodo del contenuto.

### Albero decisionale {#decision-tree}

Si tratta di una rappresentazione grafica del [Risoluzione percorso progettazione](/help/sites-developing/page-templates-static.md#design-path-resolution) logica.

![design_path_resolution](assets/design_path_resolution.png)

### Esempio {#example}

Considera una semplice struttura di contenuto come segue, in cui una progettazione può essere applicata a uno qualsiasi dei nodi:

`/root/branch/leaf`

Nella tabella seguente viene descritto il modo in cui l&#39;AEM sceglie una struttura.

<table>
 <tbody>
  <tr>
   <td><strong>Ricerca di un design per<br /> </strong></td>
   <td><strong>I design esistono per<br /> </strong></td>
   <td><strong>Progettazione scelta<br /> </strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>Viene sempre considerata la corrispondenza più esatta.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>Tornare alla corrispondenza più vicina nella parte inferiore dell'albero.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>Se tutto il resto non va a buon fine, prendi quello che rimane.<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>Se non c'è una corrispondenza esatta, prenda quella più in basso nell'albero.</p> <p>L'ipotesi è che questo sarà sempre applicabile, ma più in alto l'albero può essere troppo specifico.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Sviluppo di modelli di pagina {#developing-page-templates}

I modelli di pagina AEM sono semplicemente modelli utilizzati per creare pagine. Possono contenere il minimo o il massimo contenuto iniziale necessario, in quanto il loro ruolo è quello di creare le strutture di nodo iniziali corrette, con le proprietà richieste (principalmente sling:resourceType) impostate per consentire la modifica e il rendering.

### Creazione di un modello (basato su un modello esistente) {#creating-a-new-template-based-on-an-existing-template}

Un nuovo modello può essere creato completamente da zero, ma spesso viene copiato e aggiornato un modello esistente per risparmiare tempo e fatica. Ad esempio, puoi utilizzare i modelli all’interno di Geometrixx per iniziare.

Per creare un modello basato su un modello esistente:

1. Copiare un modello esistente (preferibilmente con una definizione il più simile possibile a quella desiderata) in un nuovo nodo.

   I modelli sono memorizzati in **/apps/&lt;website-name>/templates/&lt;template-name>**.

   >[!NOTE]
   >
   >L’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni sul posizionamento specificate in ciascun modello. Consulta [Disponibilità dei modelli](#templateavailibility).

1. Modificare il **jcr:title** del nuovo nodo modello per riflettere il suo nuovo ruolo. È inoltre possibile aggiornare **jcr:descrizione** se del caso. Assicurati di modificare la disponibilità del modello della pagina in modo appropriato.

   >[!NOTE]
   >
   >Se desideri che il modello venga visualizzato in **Crea pagina** durante la creazione di una pagina direttamente in **Siti Web** dal **Siti Web** , impostare `allowedPaths` del nodo del modello per: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Copia il componente su cui si basa il modello (indicato dalla **sling:resourceType** proprietà del **jcr:content** all&#39;interno del modello) per creare un&#39;istanza.

   I componenti sono memorizzati in **/apps/&lt;website-name>/components/&lt;component-name>**.

1. Aggiornare il **jcr:title** e **jcr:descrizione** del nuovo componente.
1. Sostituire thumbnail.png se si desidera visualizzare una nuova miniatura nell&#39;elenco di selezione del modello (dimensioni 128 x 98 px).
1. Aggiornare il **sling:resourceType** del modello **jcr:content** per fare riferimento al nuovo componente.
1. Apportare ulteriori modifiche alla funzionalità o alla struttura del modello, del componente sottostante o di entrambi.

   >[!NOTE]
   >
   >Modifiche apportate al **/apps/&lt;website>/templates/&lt;template-name>** influisce sull’istanza del modello (come nell’elenco di selezione).
   >
   >
   Modifiche apportate al **/apps/&lt;website>/components/&lt;component-name>** influisce sulla pagina di contenuto creata quando viene utilizzato il modello.

   Ora puoi creare una pagina all’interno del sito web utilizzando il nuovo modello.

>[!NOTE]
>
La libreria client dell’editor presuppone la presenza di `cq.shared` nelle pagine di contenuto e, se è assente, l’errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` risultati.
>
Tutte le pagine di contenuto di esempio contengono `cq.shared`, pertanto qualsiasi contenuto basato su di essi include automaticamente `cq.shared`. Tuttavia, se decidi di creare pagine di contenuto personalizzate da zero senza basarle su contenuti di esempio, devi assicurarti di includere `cq.shared` spazio dei nomi.
>
Consulta [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md) per ulteriori informazioni.

## Come rendere disponibile un modello esistente {#making-an-existing-template-available}

Questo esempio illustra come consentire l’utilizzo di un modello per determinati percorsi di contenuto. I modelli disponibili per l’autore della pagina durante la creazione di pagine sono determinati dalla logica definita in [Disponibilità dei modelli](/help/sites-developing/templates.md#template-availability).

1. In CRXDE Lite, individua il modello da utilizzare per la pagina, ad esempio il modello Newsletter.
1. Modificare il `allowedPaths` proprietà e altre proprietà utilizzate per [disponibilità dei modelli](/help/sites-developing/templates.md#template-availability). Ad esempio: `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` significa che questo modello è consentito in qualsiasi percorso in `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
