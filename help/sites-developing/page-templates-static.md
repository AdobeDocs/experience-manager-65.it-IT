---
title: Modelli di pagina - Statici
description: Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# Modelli di pagina - Statici{#page-templates-static}

Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato. Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Ogni Modello presenta una selezione di componenti disponibili per l’uso.

* I modelli sono costituiti da [Componenti](/help/sites-developing/components.md);
* I componenti utilizzano i widget e ne consentono l’accesso; questi vengono utilizzati per eseguire il rendering del contenuto.

>[!NOTE]
>
>Sono inoltre disponibili [modelli modificabili](/help/sites-developing/page-templates-editable.md), che rappresentano il tipo di modelli consigliato per la massima flessibilità e per le funzionalità più recenti.

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
   <td> String[]</td>
   <td>Percorso di un modello che può essere figlio di questo modello.<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> String[]</td>
   <td>Percorso di un modello che può essere un elemento padre di questo modello.<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> String[]</td>
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
   <td>Classificazione del modello. Utilizzato per visualizzare il modello nell'interfaccia utente.<br /> </td>
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

Per creare una pagina, è necessario copiare il modello (albero dei nodi `/apps/<myapp>/template/<mytemplate>`) nella posizione corrispondente nell&#39;albero del sito: questo è ciò che accade se una pagina viene creata utilizzando la scheda **Siti Web**.

Questa azione di copia fornisce anche alla pagina il suo contenuto iniziale (in genere solo Contenuto di primo livello) e la proprietà sling:resourceType, il percorso del componente pagina utilizzato per il rendering della pagina (tutto ciò che si trova nel nodo figlio jcr:content).

## Struttura dei modelli {#how-templates-are-structured}

Vi sono due aspetti da considerare:

* la struttura del modello stesso
* la struttura del contenuto prodotto quando viene utilizzato un modello

### Struttura di un modello {#the-structure-of-a-template}

Un modello viene creato in un nodo di tipo **cq:Template**.

![schermata_shot_2012-02-13alle63646pm](assets/screen_shot_2012-02-13at63646pm.png)

È possibile impostare varie proprietà, in particolare:

* **jcr:title** - titolo del modello; viene visualizzato nella finestra di dialogo durante la creazione di una pagina.
* **jcr:description** - descrizione del modello; viene visualizzato nella finestra di dialogo durante la creazione di una pagina.

Questo nodo contiene un nodo jcr:content (cq:PageContent) che viene utilizzato come base per il nodo del contenuto delle pagine risultanti; questo fa riferimento, utilizzando sling:resourceType, al componente da utilizzare per il rendering del contenuto effettivo di una nuova pagina.

![schermata_shot_2012-02-13alle64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Questo componente viene utilizzato per definire la struttura del contenuto quando viene creata una nuova pagina.

![schermata_shot_2012-02-13alle64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### Contenuto prodotto da un modello {#the-content-produced-by-a-template}

I modelli vengono utilizzati per creare pagine di tipo `cq:Page` (come indicato in precedenza, una pagina è un tipo speciale di componente). Ogni pagina AEM ha un nodo strutturato `jcr:content`. Tale comportamento:

* è di tipo cq:PageContent
* è un tipo di nodo strutturato contenente una definizione di contenuto definita
* ha una proprietà `sling:resourceType` per fare riferimento al componente contenente gli script sling utilizzati per il rendering del contenuto

### Modelli predefiniti {#default-templates}

AEM viene fornito con vari modelli predefiniti disponibili. A volte può essere utile utilizzare i modelli così come sono. In tal caso, è necessario assicurarsi che il modello sia disponibile per il sito Web.

Ad esempio, l’AEM viene fornito con diversi modelli, tra cui una pagina di contenuto e una pagina Home.

| **Titolo** | **Component** | **Dove si trova** | **Scopo** |
|---|---|---|---|
| Pagina home | homepage | geometrix | Il modello della home page del Geometrixx. |
| Pagina contenuto | contentpage | geometrix | Il modello della pagina di contenuto del Geometrixx. |

#### Visualizzazione dei modelli predefiniti {#displaying-default-templates}

Per visualizzare un elenco di tutti i modelli nel repository, procedere come segue:

1. In CRXDE Lite aprire il menu **Strumenti** e fare clic su **Query**.

1. Nella scheda Query
1. Come **Tipo**, selezionare **XPath**.

1. Nel campo di input **Query** immettere la stringa seguente:
//element(&#42;, cq:Template)

1. Fare clic su **Esegui**. L&#39;elenco viene visualizzato nella casella dei risultati.

Di solito, si prende un modello esistente e ne si sviluppa uno nuovo per il proprio uso. Per ulteriori informazioni, vedere [Sviluppo di modelli di pagina](#developing-page-templates).

Per abilitare un modello esistente per il sito Web e visualizzarlo nella finestra di dialogo **Crea pagina** durante la creazione di una pagina direttamente in **Siti Web** dalla console **Siti Web**, impostare la proprietà allowedPaths del nodo del modello su: **/content(/.&#42;)?**

## Applicazione delle progettazioni dei modelli {#how-template-designs-are-applied}

Quando gli stili vengono definiti nell&#39;interfaccia utente tramite [Modalità progettazione](/help/sites-authoring/default-components-designmode.md), la progettazione viene mantenuta nel percorso esatto del nodo di contenuto per il quale viene definito lo stile.

>[!CAUTION]
>
>L&#39;Adobe consiglia di applicare solo le progettazioni tramite [Modalità progettazione](/help/sites-authoring/default-components-designmode.md).
>
>La modifica dei progetti in CRXDE Lite, ad esempio, non è una best practice e l’applicazione di tali progetti può variare rispetto al comportamento previsto.

Se le progettazioni vengono applicate solo utilizzando la modalità Progettazione, le sezioni seguenti, [Design Path Resolution](/help/sites-developing/page-templates-static.md#design-path-resolution), [Decision Tree](/help/sites-developing/page-templates-static.md#decision-tree) e [Example](/help/sites-developing/page-templates-static.md#example) non sono applicabili.

### Risoluzione percorso progettazione {#design-path-resolution}

Quando si esegue il rendering del contenuto basato su un modello statico, AEM tenta di applicare la progettazione e gli stili più rilevanti al contenuto in base a un attraversamento della gerarchia dei contenuti.

L’AEM determina lo stile più rilevante per un nodo di contenuto nel seguente ordine:

* Se è presente una progettazione per il percorso completo ed esatto del nodo di contenuto (come quando la progettazione è definita in modalità Progettazione), utilizza tale progettazione.
* Se è presente una progettazione per il nodo di contenuto dell’elemento padre, utilizza tale progettazione.
* Se esiste una progettazione per qualsiasi nodo sul percorso del nodo di contenuto, utilizza tale progettazione.

Negli ultimi due casi, se è presente più di una progettazione applicabile, utilizza quella più vicina al nodo del contenuto.

### Albero decisionale {#decision-tree}

Rappresentazione grafica della logica [Design Path Resolution](/help/sites-developing/page-templates-static.md#design-path-resolution).

![risoluzione percorso_progettazione](assets/design_path_resolution.png)

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
   <td>La corrispondenza più esatta viene sempre accettata.<br /> </td>
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
   <td>Se tutti gli altri errori non riescono, prendere ciò che rimane.<br /> </td>
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
   <td><p>Se non c'è una corrispondenza esatta, prenda quella più in basso nell'albero.</p> <p>Si presume che questo sarà sempre applicabile, ma più in alto nella struttura può essere troppo specifico.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Sviluppo di modelli di pagina {#developing-page-templates}

I modelli di pagina AEM sono semplicemente modelli utilizzati per creare pagine. Possono contenere il minimo o il massimo contenuto iniziale necessario, in quanto il loro ruolo è quello di creare le strutture di nodo iniziali corrette, con le proprietà richieste (principalmente sling:resourceType) impostate per consentire la modifica e il rendering.

### Creazione di un modello (basato su un modello esistente) {#creating-a-new-template-based-on-an-existing-template}

Un nuovo modello può essere creato completamente da zero, ma spesso viene copiato e aggiornato un modello esistente per risparmiare tempo e fatica. Ad esempio, puoi utilizzare i modelli all’interno di Geometrixx per iniziare.

Per creare un modello basato su un modello esistente:

1. Copiare un modello esistente (preferibilmente con una definizione il più simile possibile a quella desiderata) in un nuovo nodo.

   I modelli sono archiviati in **/apps/&lt;nome-sito Web>/templates/&lt;nome-modello>**.

   >[!NOTE]
   >
   >L’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni sul posizionamento specificate in ciascun modello. Vedi [Disponibilità del modello](#templateavailibility).

1. Modifica il **jcr:title** del nuovo nodo modello in modo che rifletta il nuovo ruolo. Se necessario, puoi anche aggiornare **jcr:description**. Assicurati di modificare la disponibilità del modello della pagina in modo appropriato.

   >[!NOTE]
   >
   >Se si desidera visualizzare il modello nella finestra di dialogo **Crea pagina** durante la creazione di una pagina direttamente in **Siti Web** dalla console **Siti Web**, impostare la proprietà `allowedPaths` del nodo del modello su: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Copia il componente su cui si basa il modello (indicato dalla proprietà **sling:resourceType** del nodo **jcr:content** all&#39;interno del modello) per creare un&#39;istanza.

   I componenti sono archiviati in **/apps/&lt;nome-sito Web>/components/&lt;nome-componente>**.

1. Aggiorna **jcr:title** e **jcr:description** del nuovo componente.
1. Sostituire thumbnail.png se si desidera visualizzare una nuova miniatura nell&#39;elenco di selezione del modello (dimensioni 128 x 98 px).
1. Aggiorna **sling:resourceType** del nodo **jcr:content** del modello per fare riferimento al nuovo componente.
1. Apportare ulteriori modifiche alla funzionalità o alla struttura del modello, del componente sottostante o di entrambi.

   >[!NOTE]
   >
   >Le modifiche apportate al nodo **/apps/&lt;sito Web>/templates/&lt;nome-modello>** hanno effetto sull&#39;istanza del modello (come nell&#39;elenco di selezione).
   >
   >
   Le modifiche apportate al nodo **/apps/&lt;sito Web>/components/&lt;nome-componente>** interessano la pagina del contenuto creata quando si utilizza il modello.

   Ora puoi creare una pagina all’interno del sito web utilizzando il nuovo modello.

>[!NOTE]
>
La libreria client dell&#39;editor presuppone la presenza dello spazio dei nomi `cq.shared` nelle pagine di contenuto e, se è assente, l&#39;errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` restituisce i risultati.
>
Tutte le pagine di contenuto di esempio contengono `cq.shared`, pertanto qualsiasi contenuto basato su di esse include automaticamente `cq.shared`. Tuttavia, se decidi di creare pagine di contenuto personalizzate da zero senza basarle su contenuto di esempio, devi assicurarti di includere lo spazio dei nomi `cq.shared`.
>
Per ulteriori informazioni, vedere [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md).

## Come rendere disponibile un modello esistente {#making-an-existing-template-available}

Questo esempio illustra come consentire l’utilizzo di un modello per determinati percorsi di contenuto. I modelli disponibili per l&#39;autore della pagina durante la creazione delle pagine sono determinati dalla logica definita in [Disponibilità modello](/help/sites-developing/templates.md#template-availability).

1. In CRXDE Lite, individua il modello da utilizzare per la pagina, ad esempio il modello Newsletter.
1. Modificare la proprietà `allowedPaths` e altre proprietà utilizzate per [disponibilità modello](/help/sites-developing/templates.md#template-availability). Ad esempio, `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` significa che questo modello è consentito in qualsiasi percorso in `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
