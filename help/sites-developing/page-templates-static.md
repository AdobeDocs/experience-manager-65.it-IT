---
title: Modelli di pagina - Statici
seo-title: Page Templates - Static
description: Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato
seo-description: A Template is used to create a Page and defines which components can be used within the selected scope
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 6%

---

# Modelli di pagina - Statici{#page-templates-static}

Un modello viene utilizzato per creare una pagina e definisce quali componenti possono essere utilizzati all’interno dell’ambito selezionato. Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Ogni modello presenta una selezione di componenti disponibili per l’uso.

* I modelli sono costituiti da [Componenti](/help/sites-developing/components.md);
* I componenti utilizzano e consentono l’accesso ai Widget e questi vengono utilizzati per il rendering del contenuto.

>[!NOTE]
>
>[Modelli modificabili](/help/sites-developing/page-templates-editable.md) sono inoltre disponibili e sono il tipo consigliato di modelli per la maggior flessibilità e le funzioni più recenti.

## Proprietà e nodi secondari di un modello {#properties-and-child-nodes-of-a-template}

Un modello è un nodo di tipo cq:Template e ha le seguenti proprietà e nodi figlio:

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
   <td>Percorso di un modello che può essere un elemento secondario di questo modello.<br /> </td>
  </tr>
  <tr>
   <td> allowedGenents</td>
   <td> Stringa[]</td>
   <td>Percorso di un modello che può essere un elemento padre di questo modello.<br /> </td>
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
   <td> jcr:description</td>
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

Per creare una pagina, il modello deve essere copiato (node-tree `/apps/<myapp>/template/<mytemplate>`) nella posizione corrispondente nell&#39;albero del sito: questo è ciò che accade se una pagina viene creata utilizzando **Siti Web** scheda .

Questa azione di copia dà alla pagina anche il suo contenuto iniziale (di solito solo contenuto di livello principale) e la proprietà sling:resourceType, il percorso del componente della pagina che viene utilizzato per eseguire il rendering della pagina (tutto nel nodo figlio jcr:content).

## Struttura dei modelli {#how-templates-are-structured}

Ci sono due aspetti da considerare:

* la struttura del modello stesso
* la struttura del contenuto prodotto quando viene utilizzato un modello

### La struttura di un modello {#the-structure-of-a-template}

Un modello viene creato sotto un nodo di tipo **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

È possibile impostare varie proprietà, in particolare:

* **jcr:title** - titolo del modello; viene visualizzata nella finestra di dialogo durante la creazione di una pagina.
* **jcr:description** - descrizione del modello; viene visualizzata nella finestra di dialogo durante la creazione di una pagina.

Questo nodo contiene un nodo jcr:content (cq:PageContent) che può essere utilizzato come base per il nodo di contenuto delle pagine risultanti; fa riferimento, utilizzando sling:resourceType, al componente da utilizzare per il rendering del contenuto effettivo di una nuova pagina.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Questo componente viene utilizzato per definire la struttura e la progettazione del contenuto quando viene creata una nuova pagina.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### Contenuto prodotto da un modello {#the-content-produced-by-a-template}

I modelli vengono utilizzati per creare pagine di tipo `cq:Page` (come indicato in precedenza, una pagina è un tipo speciale di componente). Ogni pagina AEM ha un nodo strutturato `jcr:content`. Tale comportamento:

* è di tipo cq:PageContent
* è un tipo di nodo strutturato contenente una definizione di contenuto definita
* ha una proprietà `sling:resourceType` per fare riferimento al componente contenente gli script sling utilizzati per il rendering del contenuto

### Modelli predefiniti {#default-templates}

AEM viene fornito con una serie di modelli predefiniti disponibili. In alcuni casi, è possibile utilizzare i modelli così come sono. In tal caso, è necessario assicurarsi che il modello sia disponibile per il sito web.

Ad esempio, AEM viene fornito con diversi modelli, tra cui una pagina di contenuto e una home page.

| **Titolo** | **Component** | **Dove si trova** | **Scopo** |
|---|---|---|---|
| Home page | homepage | geometrixx | Modello della home page di Geometrixx. |
| Pagina contenuto | contentpage | geometrixx | Modello della pagina di contenuto di Geometrixx. |

#### Visualizzazione dei modelli predefiniti {#displaying-default-templates}

Per visualizzare un elenco di tutti i modelli nel repository, procedere come segue:

1. In CRXDE Lite, aprite il menu **Strumenti** e fate clic su **Query**.

1. Nella scheda Query
1. Per **Tipo** selezionate **XPath**.

1. Nel campo di inserimento **Query** immettete la stringa seguente:
//element()&#42;, cq:Template)

1. Fate clic su **Esegui**. Nella casella dei risultati viene visualizzato l’elenco di modelli disponibili.

Nella maggior parte dei casi, si prende un modello esistente e ne si sviluppa uno nuovo per il proprio uso. Vedi [Sviluppo di modelli di pagina](#developing-page-templates) per ulteriori informazioni.

Per abilitare un modello esistente per il sito web e desideri che venga visualizzato nel **Crea pagina** finestra di dialogo durante la creazione di una pagina in **Siti Web** dal **Siti Web** imposta la proprietà allowedPaths del nodo del modello su: **/content(/.&#42;)?**

## Modalità di applicazione delle progettazioni di modelli {#how-template-designs-are-applied}

Quando gli stili vengono definiti nell’interfaccia utente tramite [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md), la progettazione viene mantenuta nel percorso esatto del nodo di contenuto per il quale viene definito lo stile.

>[!CAUTION]
>
>L&#39;Adobe consiglia di applicare i disegni solo attraverso [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md).
>
>Ad esempio, la modifica dei progetti in CRX DE non è consigliata e l’applicazione di tali progetti può variare da un comportamento all’altro.

Se le progettazioni vengono applicate solo utilizzando la modalità Progettazione, le sezioni seguenti: [Risoluzione del percorso di progettazione](/help/sites-developing/page-templates-static.md#design-path-resolution), [Albero decisionale](/help/sites-developing/page-templates-static.md#decision-tree)e [Esempio](/help/sites-developing/page-templates-static.md#example) non sono applicabili.

### Risoluzione del percorso di progettazione {#design-path-resolution}

Quando esegui il rendering del contenuto basato su un modello statico, AEM tenterà di applicare la progettazione e gli stili più rilevanti al contenuto in base a un attraversamento della gerarchia dei contenuti.

AEM determina lo stile più pertinente per un nodo di contenuto nel seguente ordine:

* Se esiste una progettazione per il percorso completo ed esatto del nodo di contenuto (come quando la progettazione è definita in modalità Progettazione), utilizza tale progettazione.
* Se esiste una progettazione per il nodo di contenuto del padre, utilizza tale progettazione.
* Se esiste una progettazione per qualsiasi nodo sul percorso del nodo di contenuto, utilizza tale progettazione.

Negli ultimi due casi, se è presente più di una progettazione applicabile, utilizza quella più vicina al nodo del contenuto.

### Albero decisionale {#decision-tree}

Questa è una rappresentazione grafica del [Risoluzione del percorso di progettazione](/help/sites-developing/page-templates-static.md#design-path-resolution) logica.

![design_path_resolution](assets/design_path_resolution.png)

### Esempio {#example}

Considera una semplice struttura di contenuto come segue, in cui una progettazione può essere applicata a uno qualsiasi dei nodi:

`/root/branch/leaf`

Nella tabella seguente viene descritto come AEM scegliere una progettazione.

<table>
 <tbody>
  <tr>
   <td><strong>Ricerca Di Design Per<br /> </strong></td>
   <td><strong>Sono Presenti Progettazioni Per<br /> </strong></td>
   <td><strong>Progettazione scelta<br /> </strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>La corrispondenza più esatta è sempre presa.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>Ritornate alla corrispondenza più vicina nella parte inferiore dell'albero.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>Se tutto il resto fallisce, prendi quello che rimane.<br /> </td>
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
   <td><p>Se non c'è una corrispondenza esatta, prendere quella più in basso nell'albero.</p> <p>Il presupposto è che questo sarà sempre applicabile, ma più in alto l'albero può essere troppo specifico.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Sviluppo di modelli di pagina {#developing-page-templates}

AEM modelli di pagina sono semplicemente modelli utilizzati per creare nuove pagine. Possono contenere il contenuto iniziale necessario o il contenuto necessario, il cui ruolo consiste nel creare le strutture dei nodi iniziali corrette, con le proprietà richieste (principalmente sling:resourceType) impostate per consentire la modifica e il rendering.

### Creazione di un nuovo modello (basato su un modello esistente) {#creating-a-new-template-based-on-an-existing-template}

Inutile dire che un nuovo modello può essere creato completamente da zero, ma spesso un modello esistente verrà copiato e aggiornato per risparmiare tempo e fatica. Ad esempio, i modelli all’interno di Geometrixx possono essere utilizzati per iniziare a usarli.

Per creare un nuovo modello basato su un modello esistente:

1. Copiare un modello esistente (preferibilmente con una definizione il più simile possibile a quello che si desidera ottenere) in un nuovo nodo.

   In genere, i modelli sono memorizzati in **/apps/&lt;website-name>/templates/&lt;template-name>**.

   >[!NOTE]
   >
   >L’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni di posizionamento specificate in ciascun modello. Vedi [Disponibilità del modello](#templateavailibility).

1. Modificare la **jcr:title** del nuovo nodo del modello per riflettere il suo nuovo ruolo. È inoltre possibile aggiornare **jcr:description** se del caso. Modifica la disponibilità del modello della pagina come appropriato.

   >[!NOTE]
   >
   >Se desideri che il modello sia visualizzato nella **Crea pagina** finestra di dialogo durante la creazione di una pagina in **Siti Web** dal **Siti Web** imposta la `allowedPaths` proprietà del nodo del modello a: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Copia il componente su cui si basa il modello (indicato dalla **sling:resourceType** proprietà **jcr:content** nodo all&#39;interno del modello) per creare una nuova istanza.

   In genere, i componenti sono memorizzati in **/apps/&lt;website-name>/components/&lt;component-name>**.

1. Aggiorna **jcr:title** e **jcr:description** del nuovo componente.
1. Sostituire il file thumbnail.png se si desidera visualizzare una nuova immagine thumbnail nell&#39;elenco di selezione del modello (dimensioni 128 x 98 px).
1. Aggiorna **sling:resourceType** del modello **jcr:content** per fare riferimento al nuovo componente.
1. Apporta ulteriori modifiche alla funzionalità o alla progettazione del modello e/o del relativo componente sottostante.

   >[!NOTE]
   >
   >Modifiche apportate al **/apps/&lt;website>/templates/&lt;template-name>** il nodo influenzerà l’istanza del modello (come nell’elenco di selezione).
   Modifiche apportate al **/apps/&lt;website>/components/&lt;component-name>** il nodo influisce sulla pagina di contenuto creata quando viene utilizzato il modello.

   Ora puoi creare una pagina all’interno del sito web utilizzando il nuovo modello.

>[!NOTE]
La libreria client dell&#39;editor presuppone la presenza di `cq.shared` spazio dei nomi nelle pagine di contenuto e se è assente nell&#39;errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` risulterà.
Tutte le pagine di contenuto di esempio contengono `cq.shared`, quindi qualsiasi contenuto basato su di essi include automaticamente `cq.shared`. Tuttavia, se decidi di creare da zero pagine di contenuto personalizzate senza basarle su contenuti di esempio, devi assicurarti di includere il `cq.shared` spazio dei nomi.
Vedi [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md) per ulteriori informazioni.

## Rendere disponibile un modello esistente {#making-an-existing-template-available}

Questo esempio illustra come consentire l’utilizzo di un modello per determinati percorsi di contenuto. I modelli disponibili per l’autore della pagina durante la creazione di nuove pagine sono determinati dalla logica definita in [Disponibilità del modello](/help/sites-developing/templates.md#template-availability).

1. In CRXDE Lite, passa al modello da utilizzare per la pagina, ad esempio il modello Newsletter .
1. Modificare la `allowedPaths` proprietà e altre proprietà utilizzate per [disponibilità del modello](/help/sites-developing/templates.md#template-availability). Ad esempio: `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` significa che questo modello è consentito in qualsiasi percorso in `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
