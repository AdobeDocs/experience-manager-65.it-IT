---
title: Configurazione dei moduli di ricerca
description: Scopri come utilizzare Search Forms per personalizzare la selezione dei predicati di ricerca utilizzati nei pannelli di ricerca disponibili nelle console e nei pannelli AEM dell’ambiente di authoring.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f82391d7-e30d-48d2-8f66-88fcae3dfb5f
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 7%

---


# Configurazione dei moduli di ricerca{#configuring-search-forms}

Utilizza **Cerca in Forms** per personalizzare la selezione dei predicati di ricerca utilizzati nei pannelli di ricerca disponibili in varie console e/o pannelli AEM dell&#39;ambiente di authoring. La personalizzazione di questi pannelli rende la funzionalità di ricerca versatile in base alle tue esigenze specifiche.

È disponibile un intervallo di [predicati](#predicates-and-their-settings) preconfigurati. Puoi aggiungere più predicati, tra cui il predicato Property, per cercare risorse che corrispondono a una singola proprietà specificata. In alternativa, il predicato Options cerca le risorse che corrispondono a uno o più valori specificati per una particolare proprietà.

Puoi [configurare i moduli di ricerca](#configuring-your-search-forms) utilizzati nelle varie console e nel browser risorse (durante la modifica delle pagine). Le [finestre di dialogo per la configurazione di questi moduli](#configuring-your-search-forms) sono accessibili tramite:

* **Strumenti**

   * **Generale**

      * **Cerca in Forms**

La prima volta che accedi a questa console puoi vedere che tutte le configurazioni hanno un simbolo lucchetto. Ciò indica che la configurazione appropriata è quella predefinita (predefinita) e non può essere eliminata. Dopo aver personalizzato la configurazione, il blocco scompare a meno che non si [elimini la configurazione personalizzata](#deleting-a-configuration-to-reinstate-the-default). In tal caso, viene ripristinato il valore predefinito (e l&#39;indicatore del lucchetto).

![Finestra moduli di ricerca](assets/chlimage_1-374.png)

## Configurazioni {#configurations}

Le configurazioni predefinite disponibili sono:

* **Editor pagina (ricerca documenti):**

  Questa configurazione definisce le opzioni disponibili durante la ricerca di un documento nel browser Risorse (quando si modifica una pagina).

* **Editor pagina (ricerca immagini):**

  Questa configurazione definisce le opzioni disponibili per la ricerca di immagini nel browser Risorse (quando si modifica una pagina).

* **Editor pagina (ricerca manoscritto):**

  Questa configurazione definisce le opzioni disponibili per la ricerca di manoscritti nel browser Risorse (quando si modifica una pagina).

* **Editor pagina (ricerca pagine):**

  Questa configurazione definisce le opzioni disponibili durante la ricerca di pagine nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca paragrafi):**

  Questa configurazione definisce le opzioni disponibili durante la ricerca di paragrafi nel browser Risorse (quando si modifica una pagina).

* **Editor pagina (ricerca prodotti):**

  Questa configurazione definisce le opzioni disponibili durante la ricerca di prodotti nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca di Dynamic Media Classic [precedentemente Scene7])**:

  Questa configurazione definisce le opzioni disponibili durante la ricerca di risorse Scene7 nel browser Risorse (durante la modifica di una pagina).

* **Barra di ricerca amministrazione siti**:

  Questa configurazione definisce le opzioni di ricerca disponibili per l’utente quando utilizza la barra di ricerca della console Sites.

* **Editor pagina (ricerca video):**

  Questa configurazione definisce le opzioni disponibili durante la ricerca di video nel browser Risorse (quando si modifica una pagina).

* **Barra di ricerca amministrazione Assets:**

  Questa configurazione definisce le opzioni di ricerca disponibili per l’utente quando utilizza la console Assets.

* **Barra di ricerca amministrazione cataloghi:**

  Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca in un catalogo di e-commerce.

* **Barra di ricerca amministrazione ordini:**

  Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca di ordini commerce.

* **Barra di ricerca amministrazione raccolte prodotti:**

  Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca nelle raccolte di prodotti commerce.

* **Barra di ricerca amministrazione prodotti:**

  Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca di prodotti commerce.

* **Barra di ricerca amministrazione progetto:**

  Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca nei progetti.

## Predicati e relative impostazioni {#predicates-and-their-settings}

### Predicati {#predicates}

Sono disponibili i seguenti predicati, a seconda della configurazione:

<table>
 <tbody>
  <tr>
   <th>Predicato</th>
   <th>Scopo</th>
   <th>Impostazioni</th>
  </tr>
  <tr>
   <td>Analisi </td>
   <td>Funzionalità di ricerca/filtro nel browser Sites quando vengono visualizzati i dati basati su Analytics. I filtri di ricerca di Analytics si caricano per corrispondere alle colonne di analisi personalizzate mappate.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ultima modifica risorsa </td>
   <td>Data dell'ultima modifica apportata alla risorsa.<br /> </td>
   <td>Un predicato personalizzato, basato sul predicato Data.</td>
  </tr>
  <tr>
   <td>Componenti </td>
   <td>Consente all’autore di cercare/filtrare le pagine contenenti un componente specifico. Ad esempio, una raccolta immagini.<br /> </td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Profondità proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data </td>
   <td>Ricerca delle risorse basata su cursore in base a una proprietà data.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo date </td>
   <td>Cerca le risorse create all’interno di un intervallo specificato per una proprietà di data. Nel pannello Ricerca, potete specificare le date di inizio e fine.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Testo intervallo (Da)*</li>
     <li>Testo intervallo (A)*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato scadenza </td>
   <td>Cerca le risorse in base allo stato di scadenza.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dimensione file </td>
   <td>Cerca le risorse in base alle loro dimensioni.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro nascosto</td>
   <td>Un filtro per proprietà e valore, non visibile all’utente.</td>
   <td>
    <ul>
     <li>Nome proprietà</li>
     <li>Valore proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opzioni </td>
   <td><p>Le opzioni sono nodi di contenuto creati dall’utente.</p> <p>Per ulteriori informazioni, vedere <a href="#addinganoptionspredicate">Aggiunta di un predicato opzioni</a>.</p> </td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Percorso JSON</li>
     <li>Nome proprietà*</li>
     <li>Selezione singola</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Proprietà Options </td>
   <td>Cerca in una proprietà dell’opzione.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso nodo opzioni<br /> </li>
     <li>Selezione singola</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato pagina </td>
   <td>Cerca le pagine in base al loro stato.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà pubblicazione</li>
     <li>Nome proprietà LiveCopy</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Percorso </td>
   <td>Cerca le risorse che si trovano in un percorso specifico.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Aggiungi percorso di ricerca</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Proprietà </td>
   <td>Cerca in una proprietà specificata.</td>
   <td>nessuno</td>
  </tr>
  <tr>
   <td>Stato pubblicazione </td>
   <td>Cercare le risorse in base al loro stato di pubblicazione</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo </td>
   <td>Cerca le risorse che si trovano all’interno di un intervallo specificato. Nel pannello Ricerca, potete specificare i valori minimo e massimo per l'intervallo.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opzioni intervallo </td>
   <td>Un predicato di ricerca specifico per Assets e lo stesso del predicato cursore comune. È ancora disponibile a causa di problemi di compatibilità con le versioni precedenti.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Valutazione </td>
   <td>Cerca le risorse in base alla loro valutazione.<br /> </td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data relativa </td>
   <td>Cerca le risorse in base alla data relativa di creazione<br /> </td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Data relativa</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo cursore </td>
   <td>Predicato di ricerca comune che estende il predicato di intervallo con la funzionalità del cursore. Il valore della proprietà ricercata deve essere compreso tra i limiti del cursore.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Cerca le risorse in base ai tag. È possibile configurare la proprietà Path per compilare vari tag nell'elenco Tag.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Cerca in base ai tag.</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* I predicati di ricerca comuni sono definiti in:
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>* I predicati di ricerca relativi solo a siteadmin (interfaccia classica) si trovano in:
>  `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * Sono obsoleti e disponibili solo per compatibilità con le versioni precedenti.
>
>Queste informazioni sono esclusivamente a scopo di riferimento. Non modificare `/libs`.

### Impostazioni predicato {#predicate-settings}

A seconda del predicato, è disponibile una selezione di impostazioni per la configurazione:

* **Etichetta campo**

  Etichetta visualizzata come intestazione comprimibile o come etichetta di campo del predicato.

* **Descrizione**

  Dettagli descrittivi per l’utente.

* **Segnaposto**

  Testo vuoto o il segnaposto del predicato se non viene immesso testo filtrante.

* **Nome proprietà**

  Proprietà su cui eseguire la ricerca. Utilizza un percorso relativo e i caratteri jolly `*/*/*` specificano la profondità della proprietà relativa al nodo `jcr:content` (ogni asterisco rappresenta un livello di nodo).

  Se si desidera eseguire ricerche solo in un nodo figlio di primo livello della risorsa con la proprietà `x` nel nodo `jcr:content`, utilizzare `*/jcr:content/x`

* **Profondità proprietà**

  Profondità massima per la ricerca di tale proprietà nelle risorse. Quindi una ricerca su quella proprietà può essere eseguita su una risorsa e su elementi figlio ricorsivi fino a quando il livello degli elementi figlio non è uguale alla profondità specificata.

* **Valore proprietà**

  Il valore della proprietà come stringa assoluta o come linguaggio di espressione, ad esempio `cq:Page` o

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Testo intervallo**

  Etichetta del campo intervallo nel predicato **Intervallo date**.

* **Percorso opzione**

  L’utente può selezionare il percorso utilizzando Browser percorsi nella scheda Impostazione predicati. Dopo aver selezionato **+**, l&#39;icona viene utilizzata per aggiungere la selezione all&#39;elenco di opzioni valide (quindi l&#39;icona **-** da rimuovere, se necessario).

  Le opzioni sono nodi di contenuto creati dall’utente con la seguente struttura:

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Percorso nodo opzioni**
Effettivamente come il **Percorso opzioni**, solo questo è nel campo predicato comune, l&#39;altro è specifico per le risorse.

* **Selezione singola**
Se questa opzione è selezionata, le opzioni vengono visualizzate come caselle di controllo che consentono una sola selezione. Se selezionata per errore, è possibile deselezionare una casella di controllo.

* **Nomi proprietà Publish e Live Copy**
Le etichette per le caselle di controllo di pubblicazione e Live Copy per il predicato specifico di Sites.

* Il &ast; sulle etichette dei campi nella scheda **Impostazioni** indica che i campi sono obbligatori e se lasciato vuoto, viene visualizzato un messaggio di errore.

## Configurazione del Forms di ricerca {#configuring-your-search-forms}

### Creazione/apertura di una configurazione personalizzata {#creating-opening-a-customized-configuration}

1. Passa a **Strumenti** >> **Generale** >> **Cerca in Forms**.

1. Seleziona la configurazione da personalizzare.
1. Utilizza l&#39;icona **Modifica** per aprire la configurazione per l&#39;aggiornamento.
1. Se si apporta una nuova personalizzazione, è probabile che si desideri [aggiungere nuovi campi predicato e definire le impostazioni](#add-edit-a-predicate-field-and-define-field-settings) come richiesto. Se esiste una personalizzazione, puoi selezionare un campo esistente e [aggiornare le impostazioni](#add-edit-a-predicate-field-and-define-field-settings).
1. Seleziona **Fine** per salvare la configurazione.

   >[!NOTE]
   >
   >Le configurazioni personalizzate vengono memorizzate (come appropriato) in:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### Aggiungere/modificare un campo predicato e definire le impostazioni dei campi {#add-edit-a-predicate-field-and-define-field-settings}

Puoi aggiungere o modificare i campi e definirne/aggiornarne le impostazioni:

1. [Apri la configurazione personalizzata](#creating-opening-a-customized-configuration) per l&#39;aggiornamento.
1. Se si desidera aggiungere un campo, aprire la scheda **Seleziona predicato** e trascinare il predicato richiesto nella posizione desiderata. Ad esempio, il predicato **Intervallo date**:

   ![Modifica di un modulo di ricerca](assets/chlimage_1-375.png)

1. A seconda che:

   * Stai aggiungendo un campo:

     Dopo aver aggiunto il predicato, si apre la scheda **Impostazioni** in cui sono visualizzate le proprietà che è possibile definire.

   * Desideri aggiornare un predicato esistente:

     Seleziona il campo del predicato (a destra), quindi apri la scheda **Impostazioni**.

   Ad esempio, le impostazioni per il predicato **Intervallo date**:

   ![Proprietà per predicato intervallo date](assets/chlimage_1-376.png)

1. Apporta le modifiche necessarie e conferma con **Fine**.

### Anteprima della configurazione della ricerca {#previewing-the-search-configuration}

1. Seleziona l’icona Anteprima:

   ![Anteprima moduli di ricerca](do-not-localize/chlimage_1-31.png)

1. In questo modo i moduli di ricerca vengono visualizzati come sono visualizzati (completamente espansi) nella colonna Ricerca della console appropriata.

   ![Anteprima del modulo di ricerca](assets/chlimage_1-377.png)

1. **Chiudi** l&#39;anteprima in modo da poter restituire e completare la configurazione.

### Eliminazione di un campo predicato {#deleting-a-predicate-field}

1. [Apri la configurazione personalizzata](#creating-opening-a-customized-configuration) per l&#39;aggiornamento.
1. Seleziona il campo del predicato (a destra), apri la scheda **Impostazioni**, quindi seleziona l&#39;icona **Elimina** (in basso a sinistra).

   ![Icona Elimina](do-not-localize/chlimage_1-32.png)

1. Una finestra di dialogo richiede la conferma dell’azione di eliminazione.

1. Conferma questa e altre modifiche con **Fine**.

### Eliminazione di una configurazione (per ripristinare il valore predefinito) {#deleting-a-configuration-to-reinstate-the-default}

Dopo aver personalizzato una configurazione, vengono ignorati i valori predefiniti. Puoi ripristinare la configurazione predefinita eliminando la configurazione personalizzata.

>[!NOTE]
>
>Non è possibile eliminare nessuna delle configurazioni predefinite.

L’eliminazione di una configurazione personalizzata viene eseguita dalla console:

1. Seleziona la configurazione richiesta (ad esempio, **Editor pagina (ricerca paragrafi)**) e quindi l&#39;icona **Elimina** nella barra degli strumenti:

   ![Eliminazione di un modulo](assets/chlimage_1-378.png)

1. La configurazione personalizzata viene eliminata e il valore predefinito viene ripristinato (questo viene indicato dalla ricomparsa del simbolo del lucchetto nella console).

### Aggiunta di predicati di opzioni {#adding-options-predicates}

I predicati di opzione (Opzioni, Proprietà opzioni) consentono di configurare un elemento da cercare. Vengono utilizzati per cercare elementi direttamente sotto la pagina, ad esempio una proprietà sul nodo della pagina.

L’esempio seguente (per eseguire ricerche in base al modello utilizzato per creare una pagina), illustra i passaggi necessari:

1. Crea il nodo che definisce la proprietà su cui eseguire la ricerca.

   Per essere disponibile per l’utente, è necessario un nodo principale contenente le definizioni delle singole opzioni.

   I nodi delle singole opzioni richiedono le proprietà seguenti:

   * `jcr:title` - etichetta del campo da visualizzare nella barra di ricerca
   * `value` - valore della proprietà in cui eseguire la ricerca

   ![Aggiunta di opzioni in CRXDE](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >***non*** modificare nulla nel percorso `/libs`.
   >
   >Il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >1. Ricreare l&#39;elemento richiesto, in quanto esiste in `/libs`, in `/apps`. In questo caso da:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Apporta le modifiche in `/apps.`

1. Apri la console **Cerca in Forms** e seleziona la configurazione da aggiornare. Ad esempio, **Barra di ricerca amministrazione siti**.

   Quindi fai clic sull&#39;icona **Modifica moduli di ricerca**.

1. A seconda della configurazione, aggiungere una **Opzioni** o **Proprietà opzioni** alla configurazione.
1. Aggiornare i campi, in particolare:

   * **Nome proprietà**

     Specifica la proprietà del nodo da cercare sui nodi di destinazione. Ad esempio:

     `jcr:content/cq:template`

   * **Percorso nodo opzione**

     Seleziona il percorso in cui si trovano le opzioni. Ad esempio:

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Aggiunta percorso proprietà](assets/chlimage_1-380.png)

1. Seleziona **Fine** per salvare la configurazione.
1. Passa alla console appropriata (in questo esempio, **Sites**) e apri la barra **Ricerca**. Sono visibili i nuovi moduli di ricerca definiti e le varie opzioni. Seleziona l’opzione desiderata per visualizzare i risultati della ricerca:

   ![Risultati finali](assets/chlimage_1-381.png)

## Autorizzazioni utente {#user-permissions}

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire azioni di modifica, eliminazione e anteprima sui moduli di ricerca.

<table>
 <tbody>
  <tr>
   <td><strong>Azione</strong></td>
   <td><strong>Autorizzazioni</strong></td>
  </tr>
  <tr>
   <td>Modifica </td>
   <td>Autorizzazioni di lettura e scrittura sul nodo <code>/apps </code>.</td>
  </tr>
  <tr>
   <td>Elimina</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione sul nodo <code>/apps</code></td>
  </tr>
  <tr>
   <td>Anteprima</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione sul nodo <code>/var/dam/content</code>.<br /> autorizzazioni di lettura e scrittura sul nodo <code>/apps</code>.</td>
  </tr>
 </tbody>
</table>
