---
title: Componenti AEM - Nozioni di base
seo-title: Componenti AEM - Nozioni di base
description: Quando si inizia a sviluppare nuovi componenti è necessario comprendere le nozioni di base della struttura e della configurazione
seo-description: Quando si inizia a sviluppare nuovi componenti è necessario comprendere le nozioni di base della struttura e della configurazione
uuid: 0225b34d-5ac4-40c3-b226-0c9b24bdf782
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 1f9867f1-5089-46d0-8e21-30d62dbf4f45
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '4718'
ht-degree: 1%

---


# Componenti AEM - Nozioni di base{#aem-components-the-basics}

Quando si inizia a sviluppare nuovi componenti è necessario comprendere le basi della loro struttura e configurazione.

Questo processo richiede la lettura della teoria e l&#39;analisi dell&#39;ampia gamma di implementazioni di componenti in un&#39;istanza AEM standard. Quest’ultimo approccio è leggermente complicato dal fatto che, sebbene AEM sia passata a una nuova interfaccia touch standard, moderna, continua a supportare l’interfaccia classica.

## Panoramica {#overview}

Questa sezione illustra i concetti e i problemi chiave come introduzione ai dettagli necessari per lo sviluppo di componenti personalizzati.

### Pianificazione {#planning}

Prima di iniziare a configurare o codificare il componente, è necessario chiedere:

* Quali operazioni sono necessarie esattamente per il nuovo componente?
   * Una specifica chiara aiuta in tutte le fasi di sviluppo, test e consegna. I dettagli possono cambiare nel tempo, ma la specifica può essere aggiornata (anche se le modifiche devono essere documentate).
* È necessario creare un componente da zero o ereditare le nozioni di base da un componente esistente?
   * Non c&#39;è bisogno di reinventare la ruota.
   * Esistono diversi meccanismi forniti da AEM per ereditare ed estendere i dettagli da un&#39;altra definizione di componente, tra cui override, overlay e la [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md).
* Il componente richiede logica per selezionare o manipolare il contenuto?
   * La logica deve essere separata dal livello dell&#39;interfaccia utente. HTL è progettato per contribuire a garantire che ciò avvenga.
* Il componente avrà bisogno di formattazione CSS?
   * La formattazione CSS deve essere separata dalle definizioni dei componenti. Definite le convenzioni per denominare gli elementi HTML in modo da poterli modificare tramite file CSS esterni.
* Quali aspetti di sicurezza devo prendere in considerazione?
   * Per ulteriori informazioni, vedere [Security Checklist - Development Best Practices](/help/sites-administering/security-checklist.md#development-best-practices).

### Interfaccia touch e interfaccia classica {#touch-enabled-vs-classic-ui}

Prima di iniziare qualsiasi discussione seria sullo sviluppo di componenti, è necessario conoscere l’interfaccia utente che gli autori utilizzeranno:

* **Interfaccia utente touch**
   [L&#39;](/help/sites-developing/touch-ui-concepts.md) interfaccia utente standard si basa sull&#39;esperienza utente unificata dell&#39;Adobe Marketing Cloud, utilizzando le tecnologie sottostanti dell&#39; [interfaccia ](/help/sites-developing/touch-ui-concepts.md#coral-ui) Coral [ e dell&#39;interfaccia utente ](/help/sites-developing/touch-ui-concepts.md#granite-ui)Granite.
* **Interfaccia classica**
UIUser basata sulla tecnologia ExtJS che era obsoleta con AEM 6.4.

Per ulteriori informazioni, vedere [Interfaccia utente Recommendations per clienti](/help/sites-deploying/ui-recommendations.md).

I componenti possono essere implementati per supportare l’interfaccia touch, l’interfaccia classica o entrambi. Se osservate un’istanza standard, vengono inoltre visualizzati i componenti forniti originariamente per l’interfaccia classica, l’interfaccia touch o entrambi.

Per questo motivo descriveremo le basi di entrambi, e come riconoscerli, in questa pagina.

>[!NOTE]
>
> Adobe consiglia di sfruttare l’interfaccia touch per trarre vantaggio dalle tecnologie più recenti. [AEM Modernization ](modernization-tools.md) Toolscan semplifica la migrazione.

### Logica dei contenuti e markup di rendering {#content-logic-and-rendering-markup}

È consigliabile mantenere il codice responsabile per la marcatura e il rendering separato dal codice che controlla la logica utilizzata per selezionare il contenuto del componente.

Questa filosofia è supportata da [HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html), un linguaggio di modello appositamente limitato per garantire che un linguaggio di programmazione reale venga utilizzato per definire la logica di business sottostante. Questa logica (facoltativa) viene richiamata da HTL con un comando specifico. Questo meccanismo evidenzia il codice richiesto per una vista specifica e, se necessario, consente logiche specifiche per diverse viste dello stesso componente.

### HTL vs JSP {#htl-vs-jsp}

HTL è un linguaggio HTML basato su modelli introdotto con AEM 6.0.

La discussione sull&#39;utilizzo di [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) o JSP (Java Server Pages) durante lo sviluppo dei componenti deve essere semplice, in quanto HTL è ora il linguaggio di script consigliato per AEM.

HTL e JSP possono essere utilizzati per lo sviluppo di componenti sia per l’interfaccia classica che per quella touch. Anche se può esserci la tendenza a supporre che HTL sia solo per l’interfaccia touch e che sia JSP per l’interfaccia classica, si tratta di un’erronea concezione e più a causa dei tempi. L’interfaccia touch e l’HTL sono stati incorporati in AEM nello stesso periodo. Poiché HTL è ora la lingua consigliata, viene utilizzato per i nuovi componenti, che di solito sono per l’interfaccia touch.

>[!NOTE]
>
>Le eccezioni sono i campi modulo Granite UI Foundation (utilizzati nelle finestre di dialogo). Questi richiedono ancora l&#39;utilizzo di JSP.

### Sviluppo dei propri componenti {#developing-your-own-components}

Per creare componenti personalizzati per l’interfaccia utente appropriata, consulta (dopo aver letto questa pagina):

* [Componenti AEM per l’interfaccia touch](/help/sites-developing/developing-components.md)
* [Componenti AEM per l’interfaccia classica](/help/sites-developing/developing-components-classic.md)

Un modo rapido per iniziare consiste nel copiare un componente esistente e quindi apportare le modifiche desiderate. Per informazioni su come creare componenti personalizzati e aggiungerli al sistema di paragrafi, consulta:

* [Sviluppo di componenti](/help/sites-developing/developing-components-samples.md)  (con particolare attenzione all’interfaccia touch)

### Spostamento dei componenti nell&#39;istanza di pubblicazione {#moving-components-to-the-publish-instance}

I componenti per il rendering del contenuto devono essere distribuiti nella stessa istanza AEM contenuto. Pertanto, tutti i componenti utilizzati per l’authoring e il rendering delle pagine nell’istanza di creazione devono essere distribuiti nell’istanza di pubblicazione. Una volta distribuiti, i componenti sono disponibili per il rendering delle pagine attivate.

Per spostare i componenti nell’istanza di pubblicazione, usate i seguenti strumenti:

* [Utilizzate Package ](/help/sites-administering/package-manager.md) Manager (Gestione pacchetti) per aggiungere i componenti a un pacchetto e spostarli in un&#39;altra istanza AEM.
* [Utilizzare lo ](/help/sites-authoring/publishing-pages.md#manage-publication) strumento di replica Attiva albero per replicare i componenti.

>[!NOTE]
>
>Questi meccanismi possono essere utilizzati anche per trasferire il componente tra altre istanze, ad esempio dallo sviluppo all’istanza di test.

### Componenti a cui si deve prestare attenzione dall&#39;avvio {#components-to-be-aware-of-from-the-start}

* Pagina:

   * AEM ha il componente *page* ( `cq:Page`).
   * Si tratta di un tipo specifico di risorsa importante per la gestione dei contenuti.
      * Una pagina corrisponde a una pagina Web con contenuti per il sito Web.

* Sistemi paragrafo:

   * Il sistema paragrafo è una parte chiave di un sito Web in quanto gestisce un elenco di paragrafi. Viene utilizzato per contenere e strutturare i singoli componenti che contengono il contenuto effettivo.
   * È possibile creare, spostare, copiare ed eliminare paragrafi nel sistema di paragrafi.
   * È inoltre possibile selezionare i componenti da utilizzare in un sistema paragrafo specifico.
   * All&#39;interno di un&#39;istanza standard sono disponibili diversi sistemi di paragrafi (ad esempio `parsys`, ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`).

## Struttura {#structure}

La struttura di un componente AEM è potente e flessibile, le considerazioni principali sono:

* Tipo risorsa
* Definizione componente
* Proprietà e nodi secondari di un componente
* Finestre di dialogo
* Finestre di dialogo Progettazione
* Disponibilità del componente
* Componenti e contenuti creati

### Tipo risorsa {#resource-type}

Un elemento chiave della struttura è il tipo di risorsa.

* La struttura del contenuto dichiara le intenzioni.
* Il tipo di risorsa li implementa.

Questa è un&#39;astrazione che aiuta a garantire che anche quando l&#39;aspetto e il sentire cambiano nel tempo, l&#39;intenzione rimane il tempo.

### Definizione del componente {#component-definition}

#### Nozioni di base sui componenti {#component-basics}

La definizione di un componente può essere ripartita come segue:

* AEM componenti si basano su [Sling](https://sling.apache.org/documentation.html).
* AEM componenti si trovano (in genere) in:

   * HTL: `/libs/wcm/foundation/components`
   * JSP: `/libs/foundation/components`

* I componenti specifici per progetto/sito si trovano (in genere) in:

   * `/apps/<myApp>/components`

* AEM componenti standard sono definiti come `cq:Component` e presentano gli elementi chiave:

   * proprietà JCR:

      Un elenco delle proprietà JCR; queste sono variabili e alcune possono essere facoltative attraverso la struttura di base di un nodo di componente, le sue proprietà e i suoi sottonodi sono definiti dalla definizione `cq:Component`

   * Riferimenti:

      Definiscono gli elementi statici usati dal componente.

   * Script:

   Sono utilizzati per implementare il comportamento dell’istanza risultante del componente.

* **Nodo principale**:

   * `<mycomponent> (cq:Component)` - Nodo gerarchico del componente.

* **Proprietà** vitali:

   * `jcr:title` - Titolo componente; ad esempio, utilizzato come etichetta quando il componente è elencato nel browser o nella barra laterale dei componenti.
   * `jcr:description` - Descrizione del componente; può essere utilizzato come hint di posizionamento del mouse nel browser o nella barra laterale dei componenti.
   * Interfaccia classica:

      * `icon.png` - Icona per questo componente.
      * `thumbnail.png` - Immagine visualizzata se questo componente è elencato nel sistema di paragrafi.
   * Interfaccia touch

      * Per ulteriori informazioni, vedere la sezione [Icona componente nell&#39;interfaccia touch](/help/sites-developing/components-basics.md#component-icon-in-touch-ui).


* **Nodi** secondari fondamentali:

   * `cq:editConfig (cq:EditConfig)` - Definisce le proprietà di modifica del componente e abilita la visualizzazione del componente nel browser Componenti o nella barra laterale.

      Nota: se il componente dispone di una finestra di dialogo, viene visualizzato automaticamente nel browser Componenti o nella barra laterale, anche se cq:editConfig non esiste.

   * `cq:childEditConfig (cq:EditConfig)` - Controlla gli aspetti dell’interfaccia utente dell’autore per i componenti secondari che non ne definiscono uno personalizzato  `cq:editConfig`.
   * Interfaccia utente touch:

      * `cq:dialog` (  `nt:unstructured`) - Finestra di dialogo per questo componente. Definisce l’interfaccia che consente all’utente di configurare il componente e/o di modificarne il contenuto.
      * `cq:design_dialog` (  `nt:unstructured`) - Modifica progettazione per questo componente
   * Interfaccia classica:

      * `dialog` (  `cq:Dialog`) - Finestra di dialogo per questo componente. Definisce l’interfaccia che consente all’utente di configurare il componente e/o di modificarne il contenuto.
      * `design_dialog` (  `cq:Dialog`) - Modifica progettazione per questo componente.


#### Icona componente nell&#39;interfaccia touch {#component-icon-in-touch-ui}

L’icona o l’abbreviazione del componente viene definita tramite le proprietà JCR del componente quando il componente viene creato dallo sviluppatore. Tali proprietà vengono valutate nell&#39;ordine seguente e viene utilizzata la prima proprietà valida trovata.

1. `cq:icon` - Proprietà String che punta a un&#39;icona standard nella libreria  [Coral UI ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) da visualizzare nel browser dei componenti
   * Utilizzate il valore dell&#39;attributo HTML dell&#39;icona Corallo.
1. `abbreviation` - Proprietà String per personalizzare l&#39;abbreviazione del nome del componente nel browser Componenti
   * L&#39;abbreviazione deve essere limitata a due caratteri.
   * Se si specifica una stringa vuota, l&#39;abbreviazione verrà generata dai primi due caratteri della proprietà `jcr:title`.
      * Ad esempio &quot;Im&quot; per &quot;Image&quot;
      * Il titolo localizzato verrà utilizzato per creare l’abbreviazione.
   * L&#39;abbreviazione viene tradotta solo se il componente dispone di una proprietà `abbreviation_commentI18n`, che viene quindi utilizzata come hint di traduzione.
1. `cq:icon.png` o  `cq:icon.svg` - Icona per questo componente, visualizzata nel browser Componenti
   * 20 x 20 pixel è la dimensione delle icone dei componenti standard.
      * Le icone più grandi verranno ridotte (lato client).
   * Il colore consigliato è rgb(112, 112, 112) > #707070
   * Lo sfondo delle icone dei componenti standard è trasparente.
   * Sono supportati solo i file `.png` e `.svg`.
   * Se si importa dal file system tramite il plug-in Eclipse, i nomi dei file devono essere sostituiti, ad esempio, come `_cq_icon.png` o `_cq_icon.svg`.
   * `.png` prende un precedente rispetto a  `.svg` se entrambi sono presenti

Se sul componente non viene trovata nessuna delle proprietà di cui sopra ( `cq:icon`, `abbreviation`, `cq:icon.png` o `cq:icon.svg`):

* Il sistema cercherà le stesse proprietà sui super componenti che seguono la proprietà `sling:resourceSuperType`.
* Se a livello di super componente non viene trovata alcuna abbreviazione o un&#39;abbreviazione vuota, il sistema genererà l&#39;abbreviazione dalle prime lettere della proprietà `jcr:title` del componente corrente.

Per annullare l&#39;ereditarietà delle icone dai super componenti, l&#39;impostazione di una proprietà vuota `abbreviation` sul componente ripristina il comportamento predefinito.

La [console dei componenti](/help/sites-authoring/default-components-console.md#component-details) mostra come viene definita l&#39;icona di un particolare componente.

#### Esempio di icona SVG {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### Proprietà e nodi secondari di un componente {#properties-and-child-nodes-of-a-component}

Molti dei nodi/proprietà necessari per definire un componente sono comuni a entrambe le interfacce e le differenze rimangono indipendenti, in modo che il componente possa funzionare in entrambi gli ambienti.

Un componente è un nodo di tipo `cq:Component` con le seguenti proprietà e nodi secondari:

<table>
 <tbody>
  <tr>
   <td><strong>Nome <br /> </strong></td>
   <td><strong>Tipo <br /> </strong></td>
   <td><strong>Descrizione <br /> </strong></td>
  </tr>
  <tr>
   <td>.<br /> </td>
   <td><code>cq:Component</code></td>
   <td>Componente corrente. Un componente è di tipo nodo <code>cq:Component</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>Gruppo in cui è possibile selezionare il componente nel browser Componenti (interfaccia touch) o nella barra laterale (interfaccia classica).<br /> Il valore di  <code>.hidden</code> è utilizzato per i componenti che non possono essere selezionati dall’interfaccia utente, ad esempio i sistemi paragrafo effettivi.</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>Indica se il componente è un componente contenitore e può quindi contenere altri componenti, ad esempio un sistema paragrafo.</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code> </td>
   <td>Definizione della finestra di dialogo di modifica per l’interfaccia touch.</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>Definizione della finestra di dialogo di modifica per l’interfaccia classica.</td>
  </tr>
  <tr>
   <td><code>cq:design_dialog</code></td>
   <td><code>nt:unstructured</code></td>
   <td>Definizione della finestra di dialogo di progettazione per l’interfaccia touch.</td>
  </tr>
  <tr>
   <td><code>design_dialog</code></td>
   <td><code>cq:Dialog </code></td>
   <td>Definizione della finestra di dialogo di progettazione per l'interfaccia classica.<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>Percorso di una finestra di dialogo che copre il caso in cui il componente non dispone di un nodo di dialogo.<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>Se impostata, questa proprietà viene impostata come ID cella. Per ulteriori informazioni, consultare l'articolo della Knowledge Base <a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">How are Design Cell IDs build</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>Quando il componente è un contenitore, come ad esempio un sistema paragrafo, questo determina la configurazione di modifica dei nodi secondari.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">Modificare la configurazione del componente</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>Restituisce attributi di tag aggiuntivi aggiunti al tag HTML circostante. Consente l'aggiunta di attributi ai div generati automaticamente.</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>Se true, il rendering del componente non viene eseguito con classi div e css generate automaticamente.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>Se trovato, questo nodo verrà utilizzato come modello di contenuto quando il componente viene aggiunto dal Browser componenti o dalla barra laterale.</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>Percorso di un nodo da utilizzare come modello di contenuto quando il componente viene aggiunto dal browser Componenti o dalla barra laterale. Deve essere un percorso assoluto, non relativo al nodo del componente.<br /> A meno che non desideriate riutilizzare il contenuto già disponibile altrove, questo non è necessario ed  <code>cq:template</code> è sufficiente (vedete di seguito).</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>Data di creazione del componente.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:description</code></td>
   <td><code>String</code></td>
   <td>Descrizione del componente.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:title</code></td>
   <td><code>String</code></td>
   <td>Titolo del componente.<br /> </td>
  </tr>
  <tr>
   <td><code>sling:resourceSuperType</code></td>
   <td><code>String</code></td>
   <td>Quando viene impostato, il componente eredita da questo componente.<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>Abilita la creazione di componenti virtuali. Per visualizzare un esempio, consultare il componente di contatto all'indirizzo:<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
  </tr>
  <tr>
   <td><code>&lt;breadcrumb.jsp&gt;</code></td>
   <td><code>nt:file</code> </td>
   <td>File di script.<br /> </td>
  </tr>
  <tr>
   <td><code>icon.png</code></td>
   <td><code>nt:file</code></td>
   <td>Icona del componente, visualizzata accanto al titolo nella barra laterale.<br /> </td>
  </tr>
  <tr>
   <td><code>thumbnail.png</code></td>
   <td><code>nt:file</code></td>
   <td>Miniatura opzionale visualizzata durante il trascinamento del componente dalla barra laterale.<br /> </td>
  </tr>
 </tbody>
</table>

Se osserviamo il componente **Testo** (una delle due versioni), è possibile vedere i seguenti elementi:

* HTL ( `/libs/wcm/foundation/components/text`)

   ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP ( `/libs/foundation/components/text`)

   ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

Le proprietà di particolare interesse comprendono:

* `jcr:title` - titolo del componente; può essere utilizzato per identificare il componente, ad esempio, nell’elenco dei componenti nel browser o nella barra laterale dei componenti
* `jcr:description` - descrizione del componente; può essere usato come hint di posizionamento del mouse nell’elenco dei componenti nella barra laterale
* `sling:resourceSuperType`: indica il percorso di ereditarietà quando si estende un componente (sostituendo una definizione)

I nodi secondari di particolare interesse includono:

* `cq:editConfig` ( `cq:EditConfig`) - questo controlla gli aspetti visivi; ad esempio, può definire l&#39;aspetto di una barra o di un widget, oppure aggiungere controlli personalizzati
* `cq:childEditConfig` ( `cq:EditConfig`) - controlla gli aspetti visivi dei componenti secondari che non hanno una propria definizione
* Interfaccia utente touch:
   * `cq:dialog` (  `nt:unstructured`) - definisce la finestra di dialogo per la modifica del contenuto di questo componente
   * `cq:design_dialog` (  `nt:unstructured`) - specifica le opzioni di modifica della progettazione per questo componente
* Interfaccia classica:
   * `dialog` (  `cq:Dialog`) - Definisce la finestra di dialogo per la modifica del contenuto di questo componente (specifica per l’interfaccia classica)
   * `design_dialog` (  `cq:Dialog`) - specifica le opzioni di modifica della progettazione per questo componente
   * `icon.png` - file di grafica da usare come icona per il componente nella barra laterale
   * `thumbnail.png` - file di grafica da usare come miniatura per il componente mentre lo trascinate dalla barra laterale

### Finestre di dialogo {#dialogs}

Le finestre di dialogo sono un elemento chiave del componente in quanto forniscono un’interfaccia che consente agli autori di configurare e fornire input a tale componente.

A seconda della complessità del componente, la finestra di dialogo può richiedere una o più schede, per contenere la lunghezza della finestra di dialogo e ordinare i campi di input.

Le definizioni delle finestre di dialogo sono specifiche dell’interfaccia:

>[!NOTE]
>
>* Per motivi di compatibilità, l’interfaccia touch può usare la definizione di una finestra di dialogo dell’interfaccia classica, se non è stata definita alcuna finestra di dialogo per l’interfaccia touch.
>* [Dialog Conversion Tool](/help/sites-developing/dialog-conversion.md) (Strumento di conversione finestra di dialogo) consente inoltre di estendere/convertire componenti che dispongono solo di finestre di dialogo definite per l&#39;interfaccia classica.

>



* Interfaccia utente touch
   * `cq:dialog` ( `nt:unstructured`) nodes:
      * definire la finestra di dialogo per la modifica del contenuto di questo componente
      * specifica per l’interfaccia touch
      * sono definiti utilizzando componenti dell’interfaccia utente Granite
      * hanno una proprietà `sling:resourceType`, come struttura di contenuto Sling standard
      * può disporre di una proprietà `helpPath` per definire la risorsa della guida sensibile al contesto (percorso assoluto o relativo) a cui si accede quando si utilizza l&#39;icona della Guida (l&#39;icona ? icon) è selezionata.
         * Per i componenti out-of-the-box questo fa spesso riferimento a una pagina nella documentazione.
         * Se non viene specificato `helpPath`, viene visualizzato l&#39;URL predefinito (pagina di panoramica della documentazione).

   ![chlimage_1-242](assets/chlimage_1-242.png)

   All’interno della finestra di dialogo, sono definiti i singoli campi:

   ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* Interfaccia classica
   * `dialog` ( `cq:Dialog`) nodes
      * definire la finestra di dialogo per la modifica del contenuto di questo componente
      * specifica per l’interfaccia classica
      * sono definiti utilizzando i widget ExtJS
      * hanno una proprietà `xtype` che fa riferimento a ExtJS
      * può disporre di una proprietà `helpPath` per definire la risorsa della guida sensibile al contesto (percorso assoluto o relativo) a cui si accede quando si seleziona il pulsante **Help**.
         * Per i componenti out-of-the-box questo fa spesso riferimento a una pagina nella documentazione.
         * Se non viene specificato `helpPath`, viene visualizzato l&#39;URL predefinito (pagina di panoramica della documentazione).

   ![chlimage_1-243](assets/chlimage_1-243.png)

   All’interno della finestra di dialogo, sono definiti i singoli campi:

   ![chlimage_1-244](assets/chlimage_1-244.png)

   In una finestra di dialogo classica:

   * potete creare la finestra di dialogo come `cq:Dialog`, che fornirà una singola scheda, come nel componente di testo, o se avete bisogno di più schede, come con il componente di testo, la finestra di dialogo può essere definita come `cq:TabPanel`.
   * viene utilizzato un `cq:WidgetCollection` ( `items`) per fornire una base per i campi di input ( `cq:Widget`) o per ulteriori schede ( `cq:Widget`). Questa gerarchia può essere estesa.


### Finestre di dialogo di progettazione {#design-dialogs}

Le finestre di dialogo di progettazione sono molto simili alle finestre di dialogo utilizzate per modificare e configurare il contenuto, ma forniscono agli autori l’interfaccia per configurare e fornire i dettagli di progettazione per quel componente.

[Le finestre di dialogo Progettazione sono disponibili in modalità](/help/sites-authoring/default-components-designmode.md) Progettazione, anche se non sono necessarie per tutti i componenti, ad esempio  **** Titolo e  **** Immagini, entrambe dispongono di finestre di dialogo di progettazione, mentre  **** Testo non lo è.

La finestra di dialogo di progettazione per il sistema paragrafo (ad esempio parsys) è un caso speciale in quanto consente all’utente di selezionare altri componenti specifici (dal browser dei componenti o dalla barra laterale) sulla pagina.

### Aggiunta del componente al sistema paragrafo {#adding-your-component-to-the-paragraph-system}

Una volta definito, il componente deve essere reso disponibile per l’uso. Per rendere un componente disponibile per l’uso in un sistema paragrafo, potete:

1. Aprite [Modalità progettazione](/help/sites-authoring/default-components-designmode.md) per una pagina e abilitate il componente richiesto.
1. Aggiungete i componenti richiesti alla proprietà `components` della definizione del modello in:

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   Ad esempio, vedete:

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### Componenti e contenuti creati {#components-and-the-content-they-create}

Se si crea e si configura un&#39;istanza del componente **Titolo** sulla pagina: `<content-path>/Prototype.html`

* Interfaccia utente touch

   ![chlimage_1-246](assets/chlimage_1-246.png)

* Interfaccia classica

   ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

Potete quindi visualizzare la struttura del contenuto creato all’interno della directory archivio:

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

In particolare, se si guarda il testo effettivo per un **Titolo**:

* la definizione (per entrambe le interfacce) ha la proprietà `name`= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* all&#39;interno del contenuto, viene generata la proprietà `jcr:title` che contiene il contenuto dell&#39;autore.

Le proprietà definite dipendono dalle singole definizioni. Anche se possono essere più complessi di quanto non lo siano in precedenza, seguono comunque gli stessi principi di base.

## Gerarchia e ereditarietà dei componenti {#component-hierarchy-and-inheritance}

I componenti all’interno di AEM sono soggetti a 3 gerarchie diverse:

* **Gerarchia tipo di risorsa**

   Viene utilizzato per estendere i componenti utilizzando la proprietà `sling:resourceSuperType`. Questo consente al componente di ereditare. Ad esempio, un componente di testo erediterà vari attributi dal componente standard.

   * script (risolti da Sling)
   * finestre di dialogo
   * descrizioni (comprese miniature, icone, ecc.)

* **Gerarchia contenitore**

   Viene utilizzato per compilare le impostazioni di configurazione per il componente secondario ed è utilizzato più comunemente in uno scenario parsys.

   Ad esempio, le impostazioni di configurazione per i pulsanti della barra di modifica, il layout del set di controlli (barre di modifica, rollover), il layout della finestra di dialogo (in linea, mobile) possono essere definiti sul componente principale e propagati ai componenti secondari.

   Le impostazioni di configurazione (relative alla funzionalità di modifica) in `cq:editConfig` e `cq:childEditConfig` vengono propagate.

* **Includi gerarchia**

   Questo viene imposto in fase di esecuzione dalla sequenza di include.

   Questa gerarchia è utilizzata da Designer, che a sua volta funge da base per vari aspetti di progettazione del rendering; incluse le informazioni sul layout, le informazioni css, i componenti disponibili in parsys tra gli altri.

## Modifica comportamento {#edit-behavior}

In questa sezione viene illustrato come configurare il comportamento di modifica di un componente. Sono inclusi attributi quali le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente.

La configurazione è comune sia all’interfaccia touch che all’interfaccia classica, anche se con alcune specifiche differenze.

Il comportamento di modifica di un componente è configurato aggiungendo un nodo `cq:editConfig` di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà specifiche e nodi secondari. Sono disponibili le seguenti proprietà e nodi secondari:

* [ `cq:editConfig` proprietà](#configuring-with-cq-editconfig-properties) nodo:

   * `cq:actions` (  `String array`): definisce le azioni che possono essere eseguite sul componente.
   * `cq:layout` (  `String`): : definisce la modalità di modifica del componente nell’interfaccia classica.
   * `cq:dialogMode` (  `String`): Definisce la modalità di apertura della finestra di dialogo del componente nell’interfaccia classica

      * Nell’interfaccia touch, le finestre di dialogo sono sempre mobili in modalità desktop e automaticamente aperte come schermo intero in dispositivi mobili.
   * `cq:emptyText` (  `String`): definisce il testo che viene visualizzato quando non è presente alcun contenuto visivo.
   * `cq:inherit` (  `Boolean`): definisce se i valori mancanti vengono ereditati dal componente da cui eredita.
   * `dialogLayout` (String): Definisce la modalità di apertura della finestra di dialogo.


* [ `cq:editConfig` nodi](#configuring-with-cq-editconfig-child-nodes) secondari:

   * `cq:dropTargets` (tipo di nodo  `nt:unstructured`): Definisce un elenco di destinazioni di rilascio che possono accettare un rilascio da una risorsa di Content Finder

      * Più destinazioni di rilascio sono disponibili solo nell’interfaccia classica.
      * Nell’interfaccia touch è consentita una singola destinazione di rilascio.
   * `cq:actionConfigs` (tipo di nodo  `nt:unstructured`): definisce un elenco di nuove azioni aggiunte all&#39;elenco cq:actions.
   * `cq:formParameters` (tipo di nodo  `nt:unstructured`): definisce parametri aggiuntivi aggiunti al modulo della finestra di dialogo.
   * `cq:inplaceEditing` (tipo di nodo  `cq:InplaceEditingConfig`): definisce una configurazione di modifica locale per il componente.
   * `cq:listeners` (tipo di nodo  `cq:EditListenersConfig`): definisce cosa accade prima o dopo un’azione sul componente.


>[!NOTE]
>
>In questa pagina, un nodo (proprietà e nodi secondari) è rappresentato come XML, come illustrato nell&#39;esempio seguente.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afteredit="REFRESH_PAGE"/>
</jcr:root>
```

Nella directory archivio sono presenti diverse configurazioni. È possibile cercare facilmente proprietà specifiche o nodi secondari:

* Per cercare una proprietà del nodo `cq:editConfig`, ad esempio `cq:actions`, è possibile utilizzare lo strumento Query in **CRXDE Lite** ed effettuare ricerche con la seguente stringa query XPath:

   `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* Per cercare un nodo figlio di `cq:editConfig`, ad esempio è possibile cercare `cq:dropTargets`, che è di tipo `cq:DropTargetConfig`; è possibile utilizzare lo strumento Query in** CRXDE Lite** ed effettuare ricerche con la seguente stringa di query XPath:

   `//element(cq:dropTargets, cq:DropTargetConfig)`

### Configurazione con cq:EditConfig Properties {#configuring-with-cq-editconfig-properties}

### cq:azioni {#cq-actions}

La proprietà `cq:actions` ( `String array`) definisce una o più azioni che è possibile eseguire sul componente. I seguenti valori sono disponibili per la configurazione:

<table>
 <tbody>
  <tr>
   <td><strong>Valore proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>Visualizza il valore di testo statico &lt;alcuni testo&gt;<br /> visibile solo nell'interfaccia classica. L’interfaccia touch non visualizza azioni in un menu contestuale, pertanto non è applicabile.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Aggiunge un distanziatore.<br /> Visibile solo nell’interfaccia classica. L’interfaccia touch non visualizza azioni in un menu contestuale, pertanto non è applicabile.</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>Aggiunge un pulsante per modificare il componente.</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>Aggiunge un pulsante per modificare il componente e consentire l'inserimento di <a href="/help/sites-authoring/annotations.md">annotazioni</a>.</td>
   </tr>
  <tr>
   <td><code>delete</code></td>
   <td>Aggiunge un pulsante per eliminare il componente</td>
  </tr>
  <tr>
   <td><code>insert</code></td>
   <td>Aggiunge un pulsante per inserire un nuovo componente prima di quello corrente</td>
  </tr>
  <tr>
   <td><code>copymove</code></td>
   <td>Aggiunge un pulsante per copiare e tagliare il componente.</td>
  </tr>
 </tbody>
</table>

La configurazione seguente aggiunge un pulsante di modifica, un distanziatore, un pulsante di eliminazione e un pulsante di inserimento alla barra di modifica del componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

Nella configurazione seguente viene aggiunto il testo &quot;Configurazioni ereditate da Base Framework&quot; alla barra di modifica del componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq:layout (solo interfaccia classica) {#cq-layout-classic-ui-only}

La proprietà `cq:layout` ( `String`) definisce il modo in cui il componente può essere modificato nell&#39;interfaccia classica. Sono disponibili i seguenti valori:

<table>
 <tbody>
  <tr>
   <td><strong>Valore proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>Valore predefinito. L’edizione del componente è accessibile "al passaggio del mouse" tramite clic e/o menu di scelta rapida.<br /> Per un uso avanzato, tenere presente che l'oggetto lato client corrispondente è:  <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>L’edizione del componente è accessibile tramite una barra degli strumenti.<br /> Per un uso avanzato, tenere presente che l'oggetto lato client corrispondente è:  <code>CQ.wcm.EditBar</code>.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>La scelta viene lasciata al codice lato client.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I concetti di rollover e barra di modifica non sono applicabili nell’interfaccia touch.

La configurazione seguente aggiunge un pulsante di modifica alla barra di modifica del componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:dialogMode (solo interfaccia classica) {#cq-dialogmode-classic-ui-only}

Il componente può essere collegato a una finestra di dialogo di modifica. La proprietà `cq:dialogMode` ( `String`) definisce il modo in cui la finestra di dialogo del componente verrà aperta nell&#39;interfaccia classica. Sono disponibili i seguenti valori:

<table>
 <tbody>
  <tr>
   <td><strong>Valore proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>Finestra di dialogo mobile.<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(valore predefinito). La finestra di dialogo è ancorata sul componente.<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>Se la larghezza del componente è inferiore al valore <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> lato client, la finestra di dialogo è mobile, altrimenti è in linea.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Nell’interfaccia touch, le finestre di dialogo sono sempre mobili in modalità desktop e automaticamente aperte come schermo intero nei dispositivi mobili.

La configurazione seguente definisce una barra di modifica con un pulsante di modifica e una finestra di dialogo mobile:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:emptyText {#cq-emptytext}

La proprietà `cq:emptyText` ( `String`) definisce il testo visualizzato quando non è presente alcun contenuto visivo. Per impostazione predefinita: `Drag components or assets here`.

### cq:inherit {#cq-inherit}

La proprietà `cq:inherit` ( `boolean`) definisce se i valori mancanti vengono ereditati dal componente da cui eredita. Il valore predefinito è `false`.

### dialogLayout {#dialoglayout}

La proprietà `dialogLayout` definisce come aprire una finestra di dialogo per impostazione predefinita.

* Un valore di `fullscreen` apre la finestra di dialogo a schermo intero.
* Per impostazione predefinita, un valore vuoto o l’assenza della proprietà determina l’apertura normale della finestra di dialogo.
* L’utente può sempre attivare o disattivare la modalità a schermo intero all’interno della finestra di dialogo.
* Non si applica all’interfaccia classica.

### Configurazione con cq:EditConfig Child Nodes {#configuring-with-cq-editconfig-child-nodes}

### cq:dropTargets {#cq-droptargets}

Il nodo `cq:dropTargets` (tipo di nodo `nt:unstructured`) definisce un elenco di destinazioni di rilascio che possono accettare un rilascio da una risorsa trascinata da Content Finder. Funge da raccolta di nodi di tipo `cq:DropTargetConfig`.

>[!NOTE]
>
>Più destinazioni di rilascio sono disponibili solo nell’interfaccia classica.
>
>Nell’interfaccia touch verrà utilizzata solo la prima destinazione.

Ogni nodo secondario di tipo `cq:DropTargetConfig` definisce una destinazione di rilascio nel componente. Il nome del nodo è importante perché deve essere utilizzato nella JSP, come segue, per generare il nome della classe CSS assegnato all&#39;elemento DOM che è la destinazione di rilascio effettiva:

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

La `<drag and drop prefix>` è definita dalla proprietà Java:

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`.

Ad esempio, il nome della classe è definito come segue nella JSP del componente Download
( `/libs/foundation/components/download/download.jsp`), dove `file` è il nome del nodo della destinazione di rilascio nella configurazione di modifica del componente Download:

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

Il nodo di tipo `cq:DropTargetConfig` deve avere le seguenti proprietà:

<table>
 <tbody>
  <tr>
   <td><strong>Nome proprietà</strong></td>
   <td><strong>Valore proprietà<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>Regex applicato al tipo di mime della risorsa per verificare se è consentito il rilascio.</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>Array di gruppi di destinazione di rilascio. Ogni gruppo deve corrispondere al tipo di gruppo definito nell’estensione di Content Finder e associato alle risorse.</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>Nome della proprietà che verrà aggiornata dopo un rilascio valido.</td>
  </tr>
 </tbody>
</table>

La configurazione seguente è tratta dal componente Download. Consente di rilasciare qualsiasi risorsa (il tipo mime può essere una qualsiasi stringa) dal gruppo `media` da Content Finder nel componente. Dopo il rilascio, la proprietà del componente `fileReference` viene aggiornata:

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq:actionConfigs (solo interfaccia classica) {#cq-actionconfigs-classic-ui-only}

Il nodo `cq:actionConfigs` (tipo di nodo `nt:unstructured`) definisce un elenco di nuove azioni aggiunte all&#39;elenco definito dalla proprietà `cq:actions`. Ogni nodo secondario di `cq:actionConfigs` definisce una nuova azione definendo un widget.

La seguente configurazione di esempio definisce un nuovo pulsante (con un separatore per l’interfaccia classica):

* un separatore, definito dal tipo xtype `tbseparator`;

   * Questa opzione è utilizzata solo dall’interfaccia classica.
   * Questa definizione viene ignorata dall’interfaccia touch in quanto i xtype vengono ignorati (e i separatori non sono necessari in quanto la barra degli strumenti delle azioni è costruita in modo diverso nell’interfaccia touch).

* un pulsante denominato **Gestisci commenti** che esegue la funzione del gestore `CQ_collab_forum_openCollabAdmin()`.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:actions="[EDIT,COPYMOVE,DELETE,INSERT]"
    jcr:primaryType="cq:EditConfig">
    <cq:actionConfigs jcr:primaryType="nt:unstructured">
        <separator0
            jcr:primaryType="nt:unstructured"
            xtype="tbseparator"/>
        <manage
            jcr:primaryType="nt:unstructured"
            handler="function(){CQ_collab_forum_openCollabAdmin();}"
            text="Manage comments"/>
    </cq:actionConfigs>
</jcr:root>
```

>[!NOTE]
>
>Consultate [Add New Action to a Component Toolbar](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) (Aggiungi nuova azione a una barra degli strumenti di un componente) come esempio per l&#39;interfaccia touch.

### cq:formParameters {#cq-formparameters}

Il nodo `cq:formParameters` (tipo di nodo `nt:unstructured`) definisce parametri aggiuntivi che vengono aggiunti al modulo della finestra di dialogo. Ogni proprietà viene mappata su un parametro modulo.

La seguente configurazione aggiunge al modulo della finestra di dialogo un parametro denominato `name`, impostato con il valore `photos/primary`:

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq:inplaceEditing {#cq-inplaceediting}

Il nodo `cq:inplaceEditing` (tipo di nodo `cq:InplaceEditingConfig`) definisce una configurazione di modifica locale per il componente. Può avere le seguenti proprietà:

<table>
 <tbody>
  <tr>
   <td><strong>Nome proprietà</strong></td>
   <td><strong>Valore proprietà<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>) True per abilitare la modifica locale del componente.</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>) Percorso della configurazione dell'editor. La configurazione può essere specificata da un nodo di configurazione.</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>(<code>String</code>) Tipo di editor. I tipi disponibili sono:</p>
    <ul>
     <li>testo normale: da utilizzare per contenuti non HTML.<br /> </li>
     <li>title: è un editor di testo in testo normale avanzato che converte i titoli grafici in testo in testo normale prima dell’inizio della modifica. Utilizzato dal componente titolo Geometrixx.<br /> </li>
     <li>text: da utilizzare per il contenuto HTML (utilizza l'Editor Rich Text).<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

La seguente configurazione abilita la modifica locale del componente e definisce `plaintext` come tipo di editor:

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq:listener {#cq-listeners}

Il nodo `cq:listeners` (tipo di nodo `cq:EditListenersConfig`) definisce cosa accade prima o dopo un&#39;azione sul componente. Nella tabella seguente sono definite le proprietà possibili.

<table>
 <tbody>
  <tr>
   <td><strong>Nome proprietà</strong></td>
   <td><strong>Valore proprietà<br /> </strong></td>
   <td><p><strong>Valore predefinito</strong></p> <p>(Solo interfaccia classica)</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>Il gestore viene attivato prima della rimozione del componente.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>Il gestore viene attivato prima della modifica del componente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>Il gestore viene attivato prima della copia del componente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>Il gestore viene attivato prima dello spostamento del componente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>Il gestore viene attivato prima dell'inserimento del componente.<br /> Solo per l’interfaccia touch.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>Il gestore viene attivato prima che il componente venga inserito in un altro componente (solo contenitori).</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>Il gestore viene attivato dopo la rimozione del componente.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>Il gestore viene attivato dopo la modifica del componente.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>Il gestore viene attivato dopo la copia del componente.</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>Il gestore viene attivato dopo l'inserimento del componente.</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>Il gestore viene attivato dopo lo spostamento del componente.</td>
   <td><code>REFRESH_SELFMOVED</code></td>
  </tr>
  <tr>
   <td><code>afterchildinsert</code></td>
   <td>Il gestore viene attivato dopo che il componente è stato inserito in un altro componente (solo contenitori).</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I gestori `REFRESH_INSERTED` e `REFRESH_SELFMOVED` sono disponibili solo nell&#39;interfaccia classica.

>[!NOTE]
>
>I valori predefiniti per i listener sono impostati solo nell&#39;interfaccia classica.

>[!NOTE]
>
>Nel caso di componenti nidificati, esistono alcune limitazioni alle azioni definite come proprietà sul nodo `cq:listeners`:
>
>* Per i componenti nidificati, i valori delle seguenti proprietà *devono essere*: >`REFRESH_PAGE`
>  * `aftermove`
>  * `aftercopy`


Il gestore eventi può essere implementato con un&#39;implementazione personalizzata. Ad esempio (dove `project.customerAction` è un metodo statico):

`afteredit = "project.customerAction"`

L&#39;esempio seguente è equivalente alla configurazione `REFRESH_INSERTED`:

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>Per l&#39;interfaccia classica, per vedere quali parametri possono essere utilizzati nei gestori, fare riferimento alla sezione degli eventi `before<action>` e `after<action>` di [ `CQ.wcm.EditBar`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar) e [ `CQ.wcm.EditRollover`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)&lt;a7/>.

Con la seguente configurazione, la pagina viene aggiornata dopo che il componente è stato eliminato, modificato, inserito o spostato:

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
