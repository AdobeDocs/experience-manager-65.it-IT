---
title: Componenti AEM - Nozioni di base
seo-title: AEM Components - The Basics
description: Quando inizi a sviluppare nuovi componenti devi comprendere le nozioni di base della loro struttura e configurazione
seo-description: When you start to develop new components you need to understand the basics of their structure and configuration
uuid: 0225b34d-5ac4-40c3-b226-0c9b24bdf782
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 1f9867f1-5089-46d0-8e21-30d62dbf4f45
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
exl-id: 7ff92872-697c-4e66-b654-15314a8cb429
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '4948'
ht-degree: 1%

---

# Componenti AEM - Nozioni di base{#aem-components-the-basics}

Quando si inizia a sviluppare nuovi componenti è necessario comprendere le nozioni di base della loro struttura e configurazione.

Questo processo comporta la lettura della teoria e l&#39;analisi dell&#39;ampia gamma di implementazioni di componenti in un&#39;istanza AEM standard. Quest’ultimo approccio è leggermente complicato dal fatto che, sebbene AEM sia passato a una nuova interfaccia utente standard, moderna e touch, continua a supportare l’interfaccia classica.

## Panoramica {#overview}

Questa sezione descrive i concetti e i problemi chiave come introduzione ai dettagli necessari allo sviluppo dei tuoi componenti.

### Pianificazione {#planning}

Prima di iniziare effettivamente a configurare o codificare il componente, è necessario chiedere:

* Cosa devi fare esattamente con il nuovo componente?
   * Una specifica chiara aiuta in tutte le fasi di sviluppo, test e consegna. I dettagli possono cambiare nel tempo, ma la specifica può essere aggiornata (anche se le modifiche devono essere documentate).
* È necessario creare un componente da zero o è possibile ereditare le nozioni di base da un componente esistente?
   * Non c&#39;è bisogno di reinventare la ruota.
   * Sono disponibili diversi meccanismi forniti da AEM per ereditare ed estendere i dettagli da un’altra definizione di componente, tra cui override, sovrapposizione e [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md).
* Il componente richiederà una logica per selezionare/manipolare il contenuto?
   * La logica deve essere mantenuta separata dal livello dell’interfaccia utente. HTL è progettato per garantire che ciò accada.
* Il componente avrà bisogno della formattazione CSS?
   * La formattazione CSS deve essere mantenuta separata dalle definizioni dei componenti. Definisci le convenzioni per denominare gli elementi di HTML in modo da poterli modificare tramite file CSS esterni.
* Quali aspetti di sicurezza devo prendere in considerazione?
   * Vedi [Lista di controllo sicurezza - Best practice per lo sviluppo](/help/sites-administering/security-checklist.md#development-best-practices) per ulteriori dettagli.

### Interfaccia touch e interfaccia classica {#touch-enabled-vs-classic-ui}

Prima di iniziare una discussione seria sullo sviluppo di componenti è necessario sapere quale interfaccia utente utilizzeranno gli autori:

* **Interfaccia utente touch**
   [Interfaccia utente standard](/help/sites-developing/touch-ui-concepts.md) si basa sull’esperienza utente unificata di Adobe Marketing Cloud, utilizzando le tecnologie di base di [Interfaccia Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [Interfaccia Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui).
* **Interfaccia classica**
Interfaccia utente basata sulla tecnologia ExtJS obsoleta con AEM 6.4.

Vedi [Interfaccia utente Recommendations per clienti](/help/sites-deploying/ui-recommendations.md) per ulteriori dettagli.

I componenti possono essere implementati per supportare l’interfaccia touch, l’interfaccia classica o entrambe. Quando osservi un’istanza standard, vengono anche visualizzati i componenti predefiniti originariamente progettati per l’interfaccia classica, l’interfaccia touch o entrambi.

Per questo motivo descriveremo le nozioni di base di entrambi e come riconoscerli in questa pagina.

>[!NOTE]
>
>Adobe consiglia di utilizzare l’interfaccia touch per sfruttare le tecnologie più recenti. [Strumenti di modernizzazione AEM](modernization-tools.md) può semplificare la migrazione.

### Logica dei contenuti e markup di rendering  {#content-logic-and-rendering-markup}

Si consiglia di mantenere il codice responsabile del markup e del rendering separato dal codice che controlla la logica utilizzata per selezionare il contenuto del componente.

Questa filosofia è sostenuta da [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html), un linguaggio di template appositamente limitato per garantire un linguaggio di programmazione reale viene utilizzato per definire la logica di business sottostante. Questa logica (facoltativa) viene richiamata da HTL con un comando specifico. Questo meccanismo evidenzia il codice richiesto per una determinata visualizzazione e, se necessario, consente una logica specifica per diverse visualizzazioni dello stesso componente.

### HTL vs JSP {#htl-vs-jsp}

HTL è un linguaggio per modelli HTML introdotto con AEM 6.0.

La discussione sull&#39;utilizzo [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) o JSP (Java Server Pages) quando si sviluppano i propri componenti deve essere semplice, in quanto HTL è ora il linguaggio di script consigliato per AEM.

HTL e JSP possono essere utilizzati per lo sviluppo di componenti sia per l’interfaccia classica che per quella touch. Anche se si può presumere che HTL sia solo per l’interfaccia touch e JSP per l’interfaccia classica, si tratta di un’errata concezione e più a causa dei tempi. L’interfaccia touch e HTL sono stati incorporati in AEM per circa lo stesso periodo. Poiché HTL è ora la lingua consigliata, viene utilizzato per i nuovi componenti, che tendono a essere per l’interfaccia touch.

>[!NOTE]
>
>Le eccezioni sono i campi modulo di base dell’interfaccia utente Granite (utilizzati nelle finestre di dialogo). Questi richiedono ancora l&#39;utilizzo di JSP.

### Sviluppo di componenti personalizzati {#developing-your-own-components}

Per creare componenti personalizzati per l’interfaccia utente appropriata, consulta (dopo aver letto questa pagina):

* [Componenti AEM per l’interfaccia touch](/help/sites-developing/developing-components.md)
* [Componenti AEM per l’interfaccia classica](/help/sites-developing/developing-components-classic.md)

Un modo rapido per iniziare consiste nel copiare un componente esistente e quindi apportare le modifiche desiderate. Per informazioni su come creare i propri componenti e aggiungerli al sistema paragrafo, consulta:

* [Sviluppo di componenti](/help/sites-developing/developing-components-samples.md) (con particolare attenzione all’interfaccia touch)

### Spostamento dei componenti nell’istanza di pubblicazione {#moving-components-to-the-publish-instance}

I componenti che eseguono il rendering del contenuto devono essere distribuiti nella stessa istanza AEM del contenuto. Pertanto, tutti i componenti utilizzati per l’authoring e il rendering delle pagine nell’istanza di authoring devono essere distribuiti nell’istanza di pubblicazione. Quando vengono distribuiti, i componenti sono disponibili per il rendering delle pagine attivate.

Utilizza i seguenti strumenti per spostare i componenti nell’istanza di pubblicazione:

* [Utilizzo di Gestione pacchetti](/help/sites-administering/package-manager.md) per aggiungere i componenti a un pacchetto e spostarli in un&#39;altra istanza AEM.
* [Utilizzare lo strumento di replica Attiva albero](/help/sites-authoring/publishing-pages.md#manage-publication) per replicare i componenti.

>[!NOTE]
>
>Questi meccanismi possono essere utilizzati anche per trasferire il componente tra altre istanze, ad esempio dallo sviluppo all’istanza di test.

### Componenti di cui tenere conto dall’avvio {#components-to-be-aware-of-from-the-start}

* Pagina:

   * AEM *page* component ( `cq:Page`).
   * Si tratta di un tipo specifico di risorsa importante per la gestione dei contenuti.
      * Una pagina corrisponde a una pagina web che contiene il contenuto del sito web.

* Sistemi paragrafo:

   * Il sistema paragrafo è una parte chiave di un sito web in quanto gestisce un elenco di paragrafi. Viene utilizzato per contenere e strutturare i singoli componenti che contengono il contenuto effettivo.
   * È possibile creare, spostare, copiare ed eliminare paragrafi nel sistema paragrafo.
   * È inoltre possibile selezionare i componenti disponibili per l’uso all’interno di un sistema paragrafo specifico.
   * Sono disponibili diversi sistemi di paragrafi all’interno di un’istanza standard (ad esempio `parsys`, ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`).

## Struttura {#structure}

La struttura di un componente AEM è potente e flessibile, le principali considerazioni sono:

* Tipo risorsa
* Definizione del componente
* Proprietà e nodi secondari di un componente
* Finestre di dialogo
* Finestre di dialogo di progettazione
* Disponibilità dei componenti
* Componenti e contenuti creati

### Tipo risorsa {#resource-type}

Un elemento chiave della struttura è il tipo di risorsa.

* La struttura del contenuto dichiara le intenzioni.
* Il tipo di risorsa li implementa.

Questa è un&#39;astrazione che aiuta a garantire che anche quando l&#39;aspetto e l&#39;aspetto cambiano nel tempo, l&#39;intenzione rimanga nel tempo.

### Definizione del componente {#component-definition}

#### Nozioni di base sui componenti {#component-basics}

La definizione di un componente può essere suddivisa come segue:

* I componenti AEM sono basati su [Sling](https://sling.apache.org/documentation.html).
* I componenti AEM si trovano in genere in:

   * HTL: `/libs/wcm/foundation/components`
   * JSP: `/libs/foundation/components`

* I componenti specifici per progetto/sito si trovano (in genere) in:

   * `/apps/<myApp>/components`

* AEM componenti standard sono definiti come `cq:Component` e hanno gli elementi chiave:

   * proprietà jcr:

      Un elenco delle proprietà di jcr; queste sono variabili e alcune possono essere facoltative anche se la struttura di base di un nodo componente, le sue proprietà e i suoi sottonodi sono definiti da `cq:Component` definizione

   * Riferimenti:

      Definiscono gli elementi statici utilizzati dal componente.

   * Script:

   Vengono utilizzati per implementare il comportamento dell’istanza risultante del componente.

* **Nodo principale**:

   * `<mycomponent> (cq:Component)` - Nodo gerarchico del componente.

* **Proprietà vitali**:

   * `jcr:title` - Titolo del componente; ad esempio, utilizzato come etichetta quando il componente è elencato nel browser o nella barra laterale dei componenti.
   * `jcr:description` - Descrizione del componente; può essere utilizzato come hint di passaggio del mouse nel browser componenti o nella barra laterale.
   * Interfaccia classica:

      * `icon.png` - Icona per questo componente.
      * `thumbnail.png` - Immagine mostrata se questo componente è elencato all’interno del sistema paragrafo.
   * Interfaccia utente touch

      * Vedi la sezione [Icona componente nell’interfaccia touch](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) per i dettagli.


* **Nodi figlio fondamentali**:

   * `cq:editConfig (cq:EditConfig)` - Definisce le proprietà di modifica del componente e consente al componente di essere visualizzato nel browser Componenti o nella barra laterale.

      Nota: se il componente dispone di una finestra di dialogo, viene visualizzato automaticamente nel browser Componenti o nella barra laterale, anche se cq:editConfig non esiste.

   * `cq:childEditConfig (cq:EditConfig)` - Controlla gli aspetti dell’interfaccia utente dell’autore per i componenti secondari che non definiscono i propri `cq:editConfig`.
   * Interfaccia utente touch:

      * `cq:dialog` ( `nt:unstructured`) - Finestra di dialogo per questo componente. Definisce l’interfaccia che consente all’utente di configurare il componente e/o modificare il contenuto.
      * `cq:design_dialog` ( `nt:unstructured`) - Modifica di progettazione per questo componente
   * Interfaccia classica:

      * `dialog` ( `cq:Dialog`) - Finestra di dialogo per questo componente. Definisce l’interfaccia che consente all’utente di configurare il componente e/o modificare il contenuto.
      * `design_dialog` ( `cq:Dialog`): modifica di progettazione per questo componente.


#### Icona componente nell’interfaccia touch {#component-icon-in-touch-ui}

L’icona o l’abbreviazione del componente viene definita tramite le proprietà JCR del componente quando il componente viene creato dallo sviluppatore. Queste proprietà vengono valutate nell&#39;ordine seguente e viene utilizzata la prima proprietà valida trovata.

1. `cq:icon` - Proprietà di stringa che punta a un&#39;icona standard nel [Libreria dell’interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) da visualizzare nel browser componenti
   * Utilizza il valore dell’attributo HTML dell’icona Coral.
1. `abbreviation` - Proprietà String per personalizzare l&#39;abbreviazione del nome del componente nel browser componenti
   * L&#39;abbreviazione deve essere limitata a due caratteri.
   * Specificando una stringa vuota verrà generata l&#39;abbreviazione dei primi due caratteri del `jcr:title` proprietà.
      * Ad esempio &quot;Im&quot; per &quot;Image&quot;
      * Il titolo localizzato verrà utilizzato per creare l’abbreviazione.
   * L’abbreviazione viene tradotta solo se il componente ha una `abbreviation_commentI18n` , che viene quindi utilizzato come hint di traduzione.
1. `cq:icon.png` o `cq:icon.svg` - Icona per questo componente, visualizzata nel browser Componenti
   * 20 x 20 pixel è la dimensione delle icone dei componenti standard.
      * Verranno ridimensionate le icone più grandi (lato client).
   * Il colore consigliato è rgb(112, 112, 112) > #707070
   * Lo sfondo delle icone dei componenti standard è trasparente.
   * Solo `.png` e `.svg` i file sono supportati.
   * Se si importa dal file system tramite il plugin Eclipse, i nomi dei file devono essere preceduti da `_cq_icon.png` o `_cq_icon.svg` ad esempio.
   * `.png` sostituisce `.svg` se sono presenti entrambi

Se nessuna delle proprietà di cui sopra ( `cq:icon`, `abbreviation`, `cq:icon.png` o `cq:icon.svg`) si trovano sul componente:

* Il sistema cercherà le stesse proprietà sui componenti avanzati che seguono `sling:resourceSuperType` proprietà.
* Se non viene trovata alcuna abbreviazione o un&#39;abbreviazione vuota a livello di super componente, il sistema costruirà l&#39;abbreviazione dalle prime lettere della `jcr:title` del componente corrente.

Per annullare l’ereditarietà di icone da super componenti, impostare un valore vuoto `abbreviation` sul componente viene ripristinato il comportamento predefinito.

La [Console Componenti](/help/sites-authoring/default-components-console.md#component-details) mostra come è definita l’icona di un particolare componente.

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

Molti dei nodi/proprietà necessari per definire un componente sono comuni a entrambe le interfacce, con differenze che rimangono indipendenti in modo che il componente possa funzionare in entrambi gli ambienti.

Un componente è un nodo di tipo `cq:Component` e dispone delle seguenti proprietà e nodi secondari:

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
   <td>Gruppo in cui è possibile selezionare il componente nel browser Componenti (interfaccia touch) o nella barra laterale (interfaccia classica).<br /> Un valore di <code>.hidden</code> viene utilizzato per i componenti che non sono disponibili per la selezione dall’interfaccia utente, ad esempio i sistemi paragrafo effettivi.</td>
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
   <td>Definizione della finestra di dialogo di progettazione per l’interfaccia classica.<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>Percorso di una finestra di dialogo che copre il caso in cui il componente non ha un nodo di dialogo.<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>Se impostata, questa proprietà viene presa come ID cella. Per ulteriori informazioni, consulta l’articolo della Knowledge Base <a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">Come vengono costruiti gli ID delle celle di progettazione</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>Quando il componente è un contenitore, come ad esempio un sistema paragrafo, questa guida la configurazione di modifica dei nodi figlio.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">Modifica la configurazione del componente</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>Restituisce attributi di tag aggiuntivi aggiunti al tag HTML circostante. Abilita l’aggiunta di attributi ai div generati automaticamente.</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>Se true, non viene eseguito il rendering del componente con classi div e css generate automaticamente.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>Se trovato, questo nodo verrà utilizzato come modello di contenuto quando il componente viene aggiunto dal browser Componenti o dalla barra laterale.</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>Percorso di un nodo da utilizzare come modello di contenuto quando il componente viene aggiunto dal browser Componenti o dalla barra laterale. Deve essere un percorso assoluto, non relativo al nodo del componente.<br /> A meno che non si desideri riutilizzare il contenuto già disponibile altrove, questo non è necessario e <code>cq:template</code> è sufficiente (vedi di seguito).</td>
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
   <td>Quando è impostato, il componente eredita da questo componente.<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>Abilita la creazione di componenti virtuali. Per vedere un esempio, si prega di guardare il componente di contatto in:<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
  </tr>
  <tr>
   <td><code>&lt;breadcrumb.jsp&gt;</code></td>
   <td><code>nt:file</code> </td>
   <td>File di script.<br /> </td>
  </tr>
  <tr>
   <td><code>icon.png</code></td>
   <td><code>nt:file</code></td>
   <td>L’icona del componente viene visualizzata accanto al titolo nella barra laterale.<br /> </td>
  </tr>
  <tr>
   <td><code>thumbnail.png</code></td>
   <td><code>nt:file</code></td>
   <td>Miniatura opzionale mostrata mentre il componente viene trascinato nella posizione desiderata dalla barra laterale.<br /> </td>
  </tr>
 </tbody>
</table>

Se guardiamo al **Testo** in una delle due versioni, sono disponibili i seguenti elementi:

* HTL ( `/libs/wcm/foundation/components/text`)

   ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP ( `/libs/foundation/components/text`)

   ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

Le proprietà di particolare interesse comprendono:

* `jcr:title` - titolo del componente; può essere utilizzato per identificare il componente, ad esempio, viene visualizzato nell’elenco dei componenti all’interno del browser Componenti o della barra laterale
* `jcr:description` - descrizione del componente; può essere utilizzato come hint di passaggio del mouse nell’elenco dei componenti nella barra laterale
* `sling:resourceSuperType`: indica il percorso di ereditarietà quando si estende un componente (ignorando una definizione)

I nodi figlio di particolare interesse includono:

* `cq:editConfig` ( `cq:EditConfig`) - controlla gli aspetti visivi; ad esempio, può definire l&#39;aspetto di una barra o di un widget, oppure può aggiungere controlli personalizzati
* `cq:childEditConfig` ( `cq:EditConfig`): controlla gli aspetti visivi dei componenti secondari privi di proprie definizioni
* Interfaccia utente touch:
   * `cq:dialog` ( `nt:unstructured`): definisce la finestra di dialogo per la modifica del contenuto di questo componente
   * `cq:design_dialog` ( `nt:unstructured`) - specifica le opzioni di modifica della progettazione per questo componente
* Interfaccia classica:
   * `dialog` ( `cq:Dialog`): definisce la finestra di dialogo per la modifica del contenuto di questo componente (specifica dell’interfaccia classica)
   * `design_dialog` ( `cq:Dialog`) - specifica le opzioni di modifica della progettazione per questo componente
   * `icon.png` - file grafico da usare come icona per il componente nella barra laterale
   * `thumbnail.png` - file grafico da usare come miniatura del componente durante il trascinamento dalla barra laterale

### Finestre di dialogo {#dialogs}

Le finestre di dialogo sono un elemento chiave del componente, in quanto forniscono un’interfaccia che consente agli autori di configurare e fornire input a tale componente.

A seconda della complessità del componente, potrebbe essere necessaria una o più schede per mantenere breve la finestra di dialogo e per ordinare i campi di input.

Le definizioni delle finestre di dialogo sono specifiche dell’interfaccia utente:

>[!NOTE]
>
>* Per motivi di compatibilità, l’interfaccia touch può utilizzare la definizione di una finestra di dialogo dell’interfaccia classica, se non è stata definita alcuna finestra di dialogo per l’interfaccia touch.
>* La [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) sono inoltre disponibili per facilitare l’estensione/la conversione di componenti che hanno solo finestre di dialogo definite per l’interfaccia classica.
>


* Interfaccia utente touch
   * `cq:dialog` ( `nt:unstructured`) nodes:
      * definire la finestra di dialogo per la modifica del contenuto di questo componente
      * specifica per l’interfaccia touch
      * sono definiti utilizzando i componenti dell’interfaccia Granite
      * hanno una proprietà `sling:resourceType`, come struttura di contenuto Sling standard
      * può avere una proprietà `helpPath` per definire la risorsa della guida sensibile al contesto (percorso assoluto o relativo) a cui si accede quando si utilizza l’icona della Guida ( ? (icona).
         * Per i componenti predefiniti, questo fa spesso riferimento a una pagina nella documentazione.
         * Se no `helpPath` viene specificato, viene visualizzato l’URL predefinito (pagina di panoramica della documentazione).

   ![chlimage_1-242](assets/chlimage_1-242.png)

   All’interno della finestra di dialogo, vengono definiti i singoli campi:

   ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* Interfaccia classica
   * `dialog` ( `cq:Dialog`) nodes
      * definire la finestra di dialogo per la modifica del contenuto di questo componente
      * specifiche dell’interfaccia classica
      * sono definiti utilizzando i widget ExtJS
      * hanno una proprietà `xtype`, che si riferisce a ExtJS
      * può avere una proprietà `helpPath` per definire la risorsa della guida sensibile al contesto (percorso assoluto o relativo) a cui si accede quando **Aiuto** è selezionato.
         * Per i componenti predefiniti, questo fa spesso riferimento a una pagina nella documentazione.
         * Se no `helpPath` viene specificato, viene visualizzato l’URL predefinito (pagina di panoramica della documentazione).

   ![chlimage_1-243](assets/chlimage_1-243.png)

   All’interno della finestra di dialogo, vengono definiti i singoli campi:

   ![chlimage_1-244](assets/chlimage_1-244.png)

   In una finestra di dialogo classica:

   * puoi creare la finestra di dialogo come `cq:Dialog`, che fornisce una singola scheda - come nel componente testo, o se hai bisogno di più schede, come nel componente textimage, la finestra di dialogo può essere definita come `cq:TabPanel`.
   * a `cq:WidgetCollection` ( `items`) viene utilizzata per fornire una base per entrambi i campi di input ( `cq:Widget`) o ulteriori schede ( `cq:Widget`). Questa gerarchia può essere estesa.


### Finestre di dialogo di progettazione {#design-dialogs}

Le finestre di dialogo di progettazione sono molto simili alle finestre di dialogo utilizzate per modificare e configurare i contenuti, ma forniscono agli autori l’interfaccia per configurare e fornire dettagli di progettazione per quel componente.

[Le finestre di dialogo di progettazione sono disponibili in modalità Progettazione](/help/sites-authoring/default-components-designmode.md), anche se non sono necessarie per tutti i componenti, ad esempio **Titolo** e **Immagine** entrambi hanno finestre di dialogo di progettazione, mentre **Testo** No.

La finestra di dialogo Progettazione per il sistema paragrafo (ad esempio, parsys) è un caso particolare in quanto consente all’utente di selezionare altri componenti specifici (dal browser Componenti o dalla barra laterale) nella pagina.

### Aggiunta del componente al sistema paragrafo {#adding-your-component-to-the-paragraph-system}

Una volta definito un componente, questo deve essere reso disponibile per l’uso. Per rendere un componente disponibile per l’uso in un sistema paragrafo, potete effettuare le seguenti operazioni:

1. Apri [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) per una pagina e abilita il componente richiesto.
1. Aggiungi i componenti richiesti al `components` proprietà della definizione del modello in:

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   Ad esempio, vedi:

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### Componenti e contenuti creati {#components-and-the-content-they-create}

Se creiamo e configuriamo un&#39;istanza del **Titolo** nella pagina: `<content-path>/Prototype.html`

* Interfaccia utente touch

   ![chlimage_1-246](assets/chlimage_1-246.png)

* Interfaccia classica

   ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

A questo punto è possibile vedere la struttura del contenuto creato all’interno dell’archivio:

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

In particolare, se si guarda il testo effettivo per un **Titolo**:

* la definizione (per entrambe le interfacce) presenta la proprietà `name`= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* all’interno del contenuto, genera la proprietà `jcr:title` contenuto dell&#39;autore.

Le proprietà definite dipendono dalle singole definizioni. Anche se possono essere più complessi di quanto sopra, seguono comunque gli stessi principi di base.

## Gerarchia e ereditarietà dei componenti {#component-hierarchy-and-inheritance}

I componenti all’interno di AEM sono soggetti a 3 gerarchie diverse:

* **Gerarchia dei tipi di risorsa**

   Viene utilizzato per estendere i componenti utilizzando la proprietà `sling:resourceSuperType`. Questo consente al componente di ereditare. Ad esempio, un componente testo erediterà vari attributi dal componente standard.

   * script (risolti da Sling)
   * finestre di dialogo
   * descrizioni (incluse immagini in miniatura, icone, ecc.)

* **Gerarchia dei contenitori**

   Viene utilizzato per popolare le impostazioni di configurazione per il componente figlio ed è utilizzato più comunemente in uno scenario parsys.

   Ad esempio, le impostazioni di configurazione per i pulsanti della barra di modifica, il layout del set di controllo (barre di modifica, rollover), il layout della finestra di dialogo (in linea, mobile) possono essere definiti sul componente principale e propagati ai componenti secondari.

   Impostazioni di configurazione (relative alla funzionalità di modifica) in `cq:editConfig` e `cq:childEditConfig` sono propagati.

* **Includi gerarchia**

   Questo viene imposto in fase di runtime dalla sequenza di &quot;include&quot;.

   Questa gerarchia è utilizzata da Designer, che a sua volta funge da base per vari aspetti di progettazione del rendering; tra cui informazioni sul layout, informazioni css, i componenti disponibili in un parsys tra gli altri.

## Modifica comportamento {#edit-behavior}

Questa sezione spiega come configurare il comportamento di modifica di un componente. Ciò include attributi come le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente.

La configurazione è comune sia all’interfaccia touch che all’interfaccia classica, anche se con alcune specifiche differenze.

Il comportamento di modifica di un componente viene configurato aggiungendo un `cq:editConfig` nodo di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà specifiche e nodi secondari. Sono disponibili le seguenti proprietà e nodi figlio:

* [ `cq:editConfig` proprietà nodo](#configuring-with-cq-editconfig-properties):

   * `cq:actions` ( `String array`): definisce le azioni che possono essere eseguite sul componente.
   * `cq:layout` ( `String`): : definisce la modalità di modifica del componente nell’interfaccia classica.
   * `cq:dialogMode` ( `String`): definisce le modalità di apertura della finestra di dialogo dei componenti nell’interfaccia classica

      * Nell’interfaccia touch, le finestre di dialogo sono sempre mobili in modalità desktop e vengono automaticamente aperte come schermo intero in dispositivi mobili.
   * `cq:emptyText` ( `String`): definisce il testo che viene visualizzato quando non è presente alcun contenuto visivo.
   * `cq:inherit` ( `Boolean`): definisce se i valori mancanti vengono ereditati dal componente da cui eredita.
   * `dialogLayout` (Stringa): definisce come deve essere aperta la finestra di dialogo.


* [ `cq:editConfig` nodi figlio](#configuring-with-cq-editconfig-child-nodes):

   * `cq:dropTargets` (tipo di nodo) `nt:unstructured`): definisce un elenco di destinazioni di rilascio che possono accettare un rilascio da una risorsa di Content Finder

      * Le destinazioni di rilascio multiple sono disponibili solo nell’interfaccia classica.
      * Nell’interfaccia touch è consentita una singola destinazione di rilascio.
   * `cq:actionConfigs` (tipo di nodo) `nt:unstructured`): definisce un elenco di nuove azioni che vengono aggiunte all’elenco cq:actions .
   * `cq:formParameters` (tipo di nodo) `nt:unstructured`): definisce parametri aggiuntivi aggiunti al modulo di dialogo.
   * `cq:inplaceEditing` (tipo di nodo) `cq:InplaceEditingConfig`): definisce una configurazione di modifica locale per il componente.
   * `cq:listeners` (tipo di nodo) `cq:EditListenersConfig`): definisce cosa accade prima o dopo un’azione sul componente.


>[!NOTE]
>
>In questa pagina, un nodo (proprietà e nodi secondari) è rappresentato come XML, come mostrato nell&#39;esempio seguente.

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

Nell’archivio sono presenti molte configurazioni esistenti. È possibile cercare facilmente proprietà specifiche o nodi secondari:

* Per cercare una proprietà del `cq:editConfig` nodo, ad esempio `cq:actions`, puoi utilizzare lo strumento Query in **CRXDE Lite** e cerca con la seguente stringa di query XPath:

   `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* Per cercare un nodo figlio di `cq:editConfig`, ad esempio puoi cercare `cq:dropTargets`, che è di tipo `cq:DropTargetConfig`; puoi utilizzare lo strumento Query in** CRXDE Lite** e cercare con la seguente stringa di query XPath:

   `//element(cq:dropTargets, cq:DropTargetConfig)`

### Segnaposto Componente {#component-placeholders}

I componenti devono sempre eseguire il rendering di alcuni HTML visibili all’autore, anche quando il componente non ha contenuto. In caso contrario, potrebbe scomparire visivamente dall’interfaccia dell’editor, rendendola tecnicamente presente ma invisibile sulla pagina e nell’editor. In tal caso, gli autori non potranno selezionare e interagire con il componente vuoto.

Per questo motivo, i componenti devono eseguire il rendering di un segnaposto purché non rendano alcun output visibile quando la pagina viene sottoposta a rendering nell’editor di pagine (quando la modalità WCM è `edit` o `preview`).
Il markup tipico di HTML per un segnaposto è il seguente:

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

Lo script HTL tipico che esegue il rendering del segnaposto HTML di cui sopra è il seguente:

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

Nell&#39;esempio precedente, `isEmpty` è una variabile che è true solo quando il componente non ha contenuto ed è invisibile all’autore.

Per evitare ripetizioni, l’Adobe consiglia agli implementatori di componenti di utilizzare un modello HTL per questi segnaposto, [come quello fornito dai componenti core.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

L’utilizzo del modello nel collegamento precedente viene quindi fatto con la seguente riga di HTL:

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

Nell&#39;esempio precedente, `model.text` è la variabile che è true solo quando il contenuto ha contenuto ed è visibile.

Un esempio di utilizzo di questo modello può essere visualizzato nei componenti core, [come nel componente Titolo .](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### Configurazione con cq:EditConfig Properties {#configuring-with-cq-editconfig-properties}

### cq:azioni {#cq-actions}

La `cq:actions` proprietà ( `String array`) definisce una o più azioni che possono essere eseguite sul componente. Per la configurazione sono disponibili i seguenti valori:

<table>
 <tbody>
  <tr>
   <td><strong>Valore proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>Visualizza il valore del testo statico &lt;some text=""&gt;<br /> Visibile solo nell’interfaccia classica. L’interfaccia touch non visualizza le azioni in un menu contestuale, pertanto non è applicabile.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Aggiunge un distanziatore.<br /> Visibile solo nell’interfaccia classica. L’interfaccia touch non visualizza le azioni in un menu contestuale, pertanto non è applicabile.</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>Aggiunge un pulsante per modificare il componente.</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>Aggiunge un pulsante per modificare il componente e consentire <a href="/help/sites-authoring/annotations.md">annotazioni</a>.</td>
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

Nella configurazione seguente vengono aggiunti un pulsante di modifica, un distanziatore, un pulsante di eliminazione e un pulsante di inserimento alla barra di modifica del componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

Nella configurazione seguente viene aggiunto il testo &quot;Configurazioni ereditate dal framework di base&quot; alla barra di modifica del componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq:layout (solo interfaccia classica) {#cq-layout-classic-ui-only}

La `cq:layout` proprietà ( `String`) definisce come modificare il componente nell’interfaccia classica. Sono disponibili i seguenti valori:

<table>
 <tbody>
  <tr>
   <td><strong>Valore proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>Valore predefinito. L’edizione del componente è accessibile "al passaggio del mouse" tramite clic e/o menu di scelta rapida.<br /> Per un uso avanzato, tieni presente che l’oggetto lato client corrispondente è: <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>L’edizione dei componenti è accessibile tramite una barra degli strumenti.<br /> Per un uso avanzato, tieni presente che l’oggetto lato client corrispondente è: <code>CQ.wcm.EditBar</code>.</td>
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

Nella configurazione seguente viene aggiunto un pulsante di modifica alla barra di modifica del componente:

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:dialogMode (solo interfaccia classica) {#cq-dialogmode-classic-ui-only}

Il componente può essere collegato a una finestra di dialogo di modifica. La `cq:dialogMode` proprietà ( `String`) definisce le modalità di apertura della finestra di dialogo dei componenti nell’interfaccia classica. Sono disponibili i seguenti valori:

<table>
 <tbody>
  <tr>
   <td><strong>Valore proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>La finestra di dialogo è mobile.<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(valore predefinito). La finestra di dialogo viene ancorata al componente.<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>Se la larghezza del componente è inferiore al lato client <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> la finestra di dialogo è mobile, altrimenti è in linea.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Nell’interfaccia touch, le finestre di dialogo sono sempre mobili in modalità desktop e vengono automaticamente aperte a schermo intero in dispositivi mobili.

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

La `cq:emptyText` proprietà ( `String`) definisce il testo visualizzato quando non è presente alcun contenuto visivo. Per impostazione predefinita: `Drag components or assets here`.

### cq:inherit {#cq-inherit}

La `cq:inherit` proprietà ( `boolean`) definisce se i valori mancanti vengono ereditati dal componente da cui eredita. Per impostazione predefinita `false`.

### dialogLayout {#dialoglayout}

La `dialogLayout` La proprietà definisce come aprire una finestra di dialogo per impostazione predefinita.

* Un valore di `fullscreen` apre la finestra di dialogo a schermo intero.
* Per impostazione predefinita, un valore vuoto o l’assenza della proprietà aprono normalmente la finestra di dialogo.
* L’utente può sempre attivare la modalità a tutto schermo all’interno della finestra di dialogo.
* Non si applica all’interfaccia classica.

### Configurazione con i nodi figlio cq:EditConfig {#configuring-with-cq-editconfig-child-nodes}

### cq:dropTargets {#cq-droptargets}

La `cq:dropTargets` nodo (tipo nodo) `nt:unstructured`) definisce un elenco di destinazioni di rilascio che possono accettare un rilascio da una risorsa trascinata da Content Finder. Funge da raccolta di nodi di tipo `cq:DropTargetConfig`.

>[!NOTE]
>
>Le destinazioni di rilascio multiple sono disponibili solo nell’interfaccia classica.
>
>Nell’interfaccia touch verrà utilizzata solo la prima destinazione.

Ogni nodo figlio di tipo `cq:DropTargetConfig` definisce un target di rilascio nel componente. Il nome del nodo è importante perché deve essere utilizzato nel JSP, come segue, per generare il nome della classe CSS assegnato all&#39;elemento DOM che è il target di rilascio effettivo:

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

La `<drag and drop prefix>` è definito dalla proprietà Java :

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`.

Ad esempio, il nome della classe è definito come segue nel JSP del componente Download ( `/libs/foundation/components/download/download.jsp`), dove `file` è il nome del nodo della destinazione di rilascio nella configurazione di modifica del componente Download:

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
   <td>Regex applicato al tipo di MIME della risorsa per convalidare se è consentito il rilascio.</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>Array di gruppi di destinazione di rilascio. Ogni gruppo deve corrispondere al tipo di gruppo definito nell’estensione Content Finder e allegato alle risorse.</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>Nome della proprietà che verrà aggiornata dopo un rilascio valido.</td>
  </tr>
 </tbody>
</table>

La seguente configurazione viene presa dal componente Scarica . Abilita qualsiasi risorsa (il tipo mime può essere una stringa qualsiasi) dal `media` gruppo da rilasciare da Content Finder al componente. Dopo il rilascio, la proprietà del componente `fileReference` è in corso l&#39;aggiornamento:

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

La `cq:actionConfigs` nodo (tipo nodo) `nt:unstructured`) definisce un elenco di nuove azioni aggiunte all’elenco definito dalla `cq:actions` proprietà. Ogni nodo figlio di `cq:actionConfigs` definisce una nuova azione definendo un widget.

La seguente configurazione di esempio definisce un nuovo pulsante (con un separatore per l’interfaccia classica):

* un separatore, definito dall&#39;xtype `tbseparator`;

   * Viene utilizzato solo dall’interfaccia classica.
   * Questa definizione viene ignorata dall’interfaccia touch in quanto gli xtype vengono ignorati (e i separatori non sono necessari in quanto la barra delle azioni è costruita in modo diverso nell’interfaccia touch).

* un pulsante denominato **Gestire i commenti** che esegue la funzione handler `CQ_collab_forum_openCollabAdmin()`.

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
>Vedi [Aggiungere una nuova azione a una barra degli strumenti di un componente](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) come esempio per l’interfaccia touch.

### cq:formParameters {#cq-formparameters}

La `cq:formParameters` nodo (tipo nodo) `nt:unstructured`) definisce parametri aggiuntivi aggiunti al modulo di dialogo. Ogni proprietà viene mappata su un parametro di modulo.

La seguente configurazione aggiunge un parametro chiamato `name`, impostato con il valore `photos/primary` al modulo di dialogo:

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq:inplaceEditing {#cq-inplaceediting}

La `cq:inplaceEditing` nodo (tipo nodo) `cq:InplaceEditingConfig`) definisce una configurazione di modifica locale per il componente. Può avere le seguenti proprietà:

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
     <li>titolo: è un editor di testo normale avanzato che converte i titoli grafici in un testo normale prima dell'inizio della modifica. Utilizzato dal componente Titolo Geometrixx.<br /> </li>
     <li>testo: da utilizzare per il contenuto HTML (utilizza l’editor Rich Text).<br /> </li>
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

La `cq:listeners` nodo (tipo nodo) `cq:EditListenersConfig`) definisce cosa accade prima o dopo un’azione sul componente. Nella tabella seguente sono definite le proprietà possibili.

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
   <td>Il gestore viene attivato prima dell’inserimento del componente.<br /> Operativo solo per l’interfaccia touch.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>Il gestore viene attivato prima che il componente venga inserito all’interno di un altro componente (solo contenitori).</td>
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
   <td>Il gestore viene attivato dopo l’inserimento del componente.</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>Il gestore viene attivato dopo lo spostamento del componente.</td>
   <td><code>REFRESH_SELFMOVED</code></td>
  </tr>
  <tr>
   <td><code>afterchildinsert</code></td>
   <td>Il gestore viene attivato dopo che il componente è stato inserito all’interno di un altro componente (solo contenitori).</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La `REFRESH_INSERTED` e `REFRESH_SELFMOVED` I gestori sono disponibili solo nell’interfaccia classica.

>[!NOTE]
>
>I valori predefiniti per i listener sono impostati solo nell&#39;interfaccia classica.

>[!NOTE]
>
>Nel caso di componenti nidificati, ci sono alcune restrizioni alle azioni definite come proprietà nel `cq:listeners` nodo:
>
>* Per i componenti nidificati, i valori delle seguenti proprietà *deve* essere `REFRESH_PAGE`: >
>  * `aftermove`
>  * `aftercopy`


Il gestore eventi può essere implementato con un&#39;implementazione personalizzata. Ad esempio, dove `project.customerAction` è un metodo statico):

`afteredit = "project.customerAction"`

L’esempio seguente è equivalente al `REFRESH_INSERTED` configurazione:

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>Per informazioni sull’interfaccia classica, per vedere quali parametri possono essere utilizzati nei gestori, consulta `before<action>` e `after<action>` sezione eventi [ `CQ.wcm.EditBar`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar) e [ `CQ.wcm.EditRollover`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover) documentazione del widget.

Con la seguente configurazione, la pagina viene aggiornata dopo che il componente è stato eliminato, modificato, inserito o spostato:

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
