---
title: Configurazione dei moduli di ricerca
description: Scopri come configurare Search Forms.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
translation-type: tm+mt
source-git-commit: b7be1ff0e842794511ffeb4fed60eed60796b4ff
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 12%

---


# Configurazione dei moduli di ricerca{#configuring-search-forms}

Utilizza **Ricerca in Forms** per personalizzare la selezione dei predicati di ricerca utilizzati nei pannelli di ricerca disponibili in varie console AEM e/o pannelli dell’ambiente di authoring. La personalizzazione di questi pannelli rende la funzionalità di ricerca versatile in base alle esigenze specifiche.

È disponibile un intervallo [di predicati](#predicates-and-their-settings)pronti all’uso. Puoi aggiungere più predicati, tra cui il predicato Proprietà per cercare le risorse che corrispondono a una singola proprietà specificata dall’utente, oppure il predicato Opzioni per cercare le risorse che corrispondono a uno o più valori specificati per una particolare proprietà.

Puoi [configurare i moduli di ricerca](#configuring-your-search-forms) utilizzati in diverse console e nel browser delle risorse (durante la modifica delle pagine). Le finestre di dialogo [per la configurazione di questi moduli](#configuring-your-search-forms) sono accessibili tramite:

* **Strumenti**

   * **Generale**

      * **Moduli di ricerca**

La prima volta che accedi a questa console puoi vedere che tutte le configurazioni hanno un simbolo a lucchetto. Indica che la configurazione appropriata è quella predefinita (preconfigurata) e non può essere eliminata. Una volta personalizzata la configurazione, il blocco scompare - a meno che tu [elimini la configurazione personalizzata](#deleting-a-configuration-to-reinstate-the-default), nel qual caso il valore predefinito (e l&#39;indicatore del lucchetto) verrà reinstallato.

![chlimage_1-374](assets/chlimage_1-374.png)

## Configurazioni {#configurations}

Le configurazioni predefinite disponibili sono:

* **Editor pagina (ricerca documenti):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di documenti nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca immagini):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di immagini nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca manoscritto):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di manoscritti nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca pagine):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di pagine nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca paragrafi):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di paragrafi nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca prodotti):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di prodotti nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (Dynamic Media Classic  [precedentemente Scene7] search)**:

   Questa configurazione definisce le opzioni disponibili per la ricerca di risorse Scene7 nel browser Risorse (durante la modifica di una pagina).

* **Barra di ricerca amministrazione sito**:

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente quando si utilizza la barra di ricerca della console Sites .

* **Editor pagina (ricerca video):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di video nel browser Risorse (durante la modifica di una pagina).

* **Barra di ricerca amministrazione risorse:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente quando si utilizza la console Assets.

* **Barra di ricerca amministrazione progetti:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca in un catalogo di e-commerce.

* **Barra di ricerca amministrazione ordini:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l&#39;utente durante la ricerca di ordini di e-commerce.

* **Barra di ricerca amministrazione raccolte prodotti:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca nelle raccolte di prodotti commerce.

* **Barra di ricerca amministrazione prodotti:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca di prodotti commerce.

* **Barra di ricerca amministrazione progetti:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente durante la ricerca di progetti.

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
   <td>Analytics </td>
   <td>Funzionalità di ricerca/filtro nel browser Sites quando vengono visualizzati i dati basati su Analytics. I filtri di ricerca di Analytics vengono caricati per corrispondere alle colonne di analisi personalizzate mappate.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ultima modifica risorsa </td>
   <td>Data dell'ultima modifica della risorsa.<br /> </td>
   <td>Un predicato personalizzato in base al predicato della data.</td>
  </tr>
  <tr>
   <td>Componenti </td>
   <td>Consente a un autore di cercare/filtrare le pagine che contengono un componente specifico. Ad esempio, una raccolta immagini.<br /> </td>
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
   <td>Ricerca basata su cursore delle risorse in base a una proprietà data .</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo date </td>
   <td>Cerca le risorse create all’interno di un intervallo specificato per una proprietà data. Nel pannello Ricerca, puoi specificare le date di inizio e fine.</td>
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
   <td>Filtro su proprietà e valore non visibile all'utente.</td>
   <td>
    <ul>
     <li>Nome proprietà</li>
     <li>Valore proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opzioni </td>
   <td><p>Le opzioni sono nodi di contenuto creati dall’utente.</p> <p>Per ulteriori informazioni, consulta <a href="#addinganoptionspredicate">Aggiunta di un predicato delle opzioni</a> .</p> </td>
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
   <td>Cerca una proprietà dell’opzione.</td>
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
   <td>Pagina Stato </td>
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
   <td>Cerca le risorse situate sotto un percorso specifico.</td>
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
   <td>Cerca risorse che si trovano in un intervallo specificato. Nel pannello Ricerca puoi specificare i valori minimo e massimo per l’intervallo.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opzioni intervallo </td>
   <td>Un predicato di ricerca specifico per le risorse e lo stesso predicato comune del cursore. È ancora disponibile a causa di problemi di compatibilità con versioni precedenti.</td>
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
   <td>Cerca le risorse in base al loro rating.<br /> </td>
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
   <td>Cerca le risorse in base alla data relativa della loro creazione<br /> </td>
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
   <td>Un predicato di ricerca comune che estende il predicato dell'intervallo con la funzionalità di scorrimento. Il valore della proprietà ricercata deve essere compreso tra i limiti del cursore.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Cerca le risorse in base ai tag. Puoi configurare la proprietà Path per popolare vari tag nell’elenco Tag .</td>
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
   >
   >

* I predicati di ricerca relativi solo all’amministrazione del sito (interfaccia classica) si trovano in:
   > `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
   >   * Sono obsoleti e sono disponibili solo per la compatibilità con le versioni precedenti.

>
>
Queste informazioni sono solo di riferimento, non è necessario apportare modifiche a `/libs`.

### Impostazioni predicato {#predicate-settings}

A seconda del predicato è disponibile una selezione di impostazioni per la configurazione:

* **Etichetta campo**

   Etichetta che verrà visualizzata come intestazione comprimibile o come etichetta di campo del predicato.

* **Descrizione**

   Dettagli descrittivi per l&#39;utente.

* **Segnaposto**

   Testo vuoto o il segnaposto del predicato nel caso in cui non venga inserito alcun testo di filtro.

* **Nome proprietà**

   Proprietà su cui eseguire la ricerca. Utilizza un percorso relativo e i caratteri jolly `*/*/*` specificano la profondità della proprietà relativa al nodo `jcr:content` (ogni asterisco rappresenta un livello di nodo).

   Se desideri eseguire la ricerca solo su un nodo figlio di primo livello della risorsa che dispone della proprietà `x` sul nodo `jcr:content`, utilizza `*/jcr:content/x`

* **Profondità proprietà**

   Profondità massima per la ricerca di tale proprietà all&#39;interno delle risorse. È quindi possibile eseguire una ricerca su tale proprietà su una risorsa e sugli elementi secondari ricorsivi fino a quando il livello degli elementi secondari non è uguale a profondità specificata.

* **Valore proprietà**

   Il valore della proprietà come stringa assoluta o come linguaggio di espressione; ad esempio, `cq:Page` o

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Testo intervallo**

   Etichetta del campo intervallo nel predicato **Intervallo date** .

* **Percorso opzione**

   L’utente può selezionare il percorso utilizzando il browser percorsi nella scheda delle impostazioni del predicato. Dopo aver selezionato l&#39;icona **+** viene utilizzata per aggiungere la selezione all&#39;elenco delle opzioni valide (quindi l&#39;icona **-** da rimuovere se necessario).

   Le opzioni sono nodi di contenuto creati dall’utente con la seguente struttura:

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Opzioni nodo**
pathEffettivamente lo stesso del 
**Percorso opzioni**, solo nel campo predicato comune, l’altro è specifico per le risorse.

* **Selezione singola**
Se questa opzione è selezionata, le opzioni vengono visualizzate come caselle di controllo che consentono una sola selezione. Se selezionata per errore, è possibile deselezionare una casella di controllo.

* **Nome/i proprietà Publish and Live Copy**
Le etichette per le caselle di controllo pubblica e Live Copy per il predicato specifico Sites.

* &amp;ast; sulle etichette dei campi nella scheda **Impostazioni** indica che i campi sono obbligatori e se lasciato vuoto viene visualizzato un messaggio di errore

## Configurazione del Forms di ricerca {#configuring-your-search-forms}

### Creazione/apertura di una configurazione personalizzata {#creating-opening-a-customized-configuration}

1. Passa a **Strumenti**, **Generale**, **Cerca in Forms**.

1. Seleziona la configurazione da personalizzare.
1. Utilizza l&#39;icona **Modifica** per aprire la configurazione da aggiornare.
1. Se vuoi aggiungere una nuova personalizzazione [aggiungi nuovi campi predicato e definisci le impostazioni](#add-edit-a-predicate-field-and-define-field-settings) come richiesto. Se hai una personalizzazione esistente puoi selezionare un campo esistente e [aggiornare le impostazioni](#add-edit-a-predicate-field-and-define-field-settings).
1. Seleziona **Fine** per salvare la configurazione.

   >[!NOTE]
   >
   >Le configurazioni personalizzate sono memorizzate (a seconda dei casi) in:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### Aggiungere/modificare un campo predicato e definire le impostazioni dei campi {#add-edit-a-predicate-field-and-define-field-settings}

Puoi aggiungere o modificare i campi e definirne/aggiornarne le impostazioni:

1. [Apri la ](#creating-opening-a-customized-configuration) configurazione personalizzata per l’aggiornamento.
1. Per aggiungere un nuovo campo, apri la scheda **Seleziona predicato** e trascina il predicato richiesto nella posizione desiderata. Ad esempio, il **predicato Intervallo date**:

   ![chlimage_1-375](assets/chlimage_1-375.png)

1. A seconda se:

   * Si sta aggiungendo un nuovo campo:

      Dopo aver aggiunto il predicato, si aprirà la scheda **Impostazioni** e mostrerà le proprietà che possono essere definite.

   * Aggiornare un predicato esistente:

      Seleziona il campo predicato (a destra), quindi apri la scheda **Impostazioni** .
   Ad esempio, le impostazioni per **Predicato intervallo date**:

   ![chlimage_1-376](assets/chlimage_1-376.png)

1. Apporta le modifiche necessarie e conferma con **Fine**.

### Anteprima della configurazione di ricerca {#previewing-the-search-configuration}

1. Seleziona l’icona Anteprima :

   ![](do-not-localize/chlimage_1-31.png)

1. In questo modo i moduli di ricerca vengono visualizzati (completamente espansi) nella colonna Ricerca della console appropriata.

   ![chlimage_1-377](assets/chlimage_1-377.png)

1. **** Chiude l’anteprima per restituire e completare la configurazione.

### Eliminazione di un campo predicato {#deleting-a-predicate-field}

1. [Apri la ](#creating-opening-a-customized-configuration) configurazione personalizzata per l’aggiornamento.
1. Seleziona il campo predicato (a destra), apri la scheda **Impostazioni** e seleziona l&#39;icona **Elimina** (in basso a sinistra).

   ![](do-not-localize/chlimage_1-32.png)

1. Viene visualizzata una finestra di dialogo per richiedere la conferma dell’azione di eliminazione.

1. Conferma questa e tutte le altre modifiche con **Fine**.

### Eliminazione di una configurazione (per ripristinare il valore predefinito) {#deleting-a-configuration-to-reinstate-the-default}

Una volta personalizzata una configurazione, le impostazioni predefinite verranno ignorate. È possibile ripristinare la configurazione predefinita eliminando la configurazione personalizzata.

>[!NOTE]
>
>Non è possibile eliminare nessuna delle configurazioni predefinite.

L’eliminazione di una configurazione personalizzata viene eseguita dalla console:

1. Seleziona la configurazione richiesta (ad esempio, **Editor pagina (ricerca paragrafi)**), quindi l’icona **Elimina** nella barra degli strumenti:

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. La configurazione personalizzata verrà eliminata e quella predefinita ripristinata (questo è indicato dalla riapparizione del simbolo del lucchetto nella console).

### Aggiunta di predicati opzioni {#adding-options-predicates}

I predicati di opzione (Opzioni, Proprietà Opzioni) consentono di configurare un elemento da cercare. Sono solitamente utilizzati per cercare qualcosa direttamente sotto la pagina; ad esempio, una proprietà sul nodo della pagina.

L’esempio seguente (per eseguire ricerche in base al modello utilizzato per creare una pagina) illustra i passaggi necessari:

1. Crea il nodo che definisce la proprietà su cui eseguire la ricerca.

   Sarà necessario un nodo principale che contenga le definizioni delle singole opzioni per renderle disponibili all&#39;utente.

   I nodi per le singole opzioni hanno bisogno delle proprietà:

   * `jcr:title` - l’etichetta del campo da visualizzare nella barra di ricerca
   * `value` - il valore della proprietà su cui eseguire la ricerca

   ![chlimage_1-379](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >***Non è necessario*** modificare nulla nel percorso `/libs`.
   >
   >Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un pacchetto di funzioni).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >1. Ricrea l&#39;elemento richiesto, così come esiste in `/libs`, in `/apps`. In questo caso da:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Apporta modifiche all&#39;interno di `/apps.`


1. Apri la console **Cerca Forms** e seleziona la configurazione da aggiornare. Ad esempio, **Barra di ricerca amministrazione siti**.

   Quindi tocca o fai clic sull&#39;icona **Modifica moduli di ricerca** .

1. A seconda della configurazione, aggiungi una **Opzioni** o **Proprietà** alla configurazione.
1. Aggiornare i campi, in particolare:

   * **Nome proprietà**

      Specifica la proprietà nodo da cercare sui nodi target. Esempio:

      `jcr:content/cq:template`

   * **Percorso nodo opzione**

      Seleziona il percorso in cui vengono mantenute le opzioni. Esempio:

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![chlimage_1-380](assets/chlimage_1-380.png)

1. Seleziona **Fine** per salvare la configurazione.
1. Passa alla console appropriata (in questo esempio, **Sites**) e apri la barra **Ricerca** . Saranno visibili i nuovi moduli di ricerca definiti e le varie opzioni disponibili. Seleziona l’opzione richiesta per visualizzare i risultati della ricerca:

   ![chlimage_1-381](assets/chlimage_1-381.png)

## Autorizzazioni utente {#user-permissions}

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire le azioni di modifica, eliminazione e visualizzazione in anteprima sui moduli di ricerca.

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
   <td>Autorizzazioni di lettura, scrittura, eliminazione sul nodo <code>/apps</code></td>
  </tr>
  <tr>
   <td>Anteprima</td>
   <td>Autorizzazioni di lettura, scrittura, eliminazione sul nodo <code>/var/dam/content</code>.<br /> Autorizzazioni di lettura e scrittura sul  <code>/apps</code> nodo.</td>
  </tr>
 </tbody>
</table>

