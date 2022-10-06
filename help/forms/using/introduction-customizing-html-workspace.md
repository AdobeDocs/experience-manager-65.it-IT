---
title: Introduzione alla personalizzazione dell’area di lavoro AEM modulo
seo-title: Introduction to Customizing AEM form workspace
description: Introduzione rapida, con informazioni concettuali e tecniche, per personalizzare l’area di lavoro LiveCycle AEM Forms per la gestione dei processi.
seo-description: A quick introduction, with conceptual and technical information, to customize LiveCycle AEM Forms workspace for process management.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# Introduzione alla personalizzazione dell’area di lavoro AEM modulo{#introduction-to-customizing-aem-form-workspace}

AEM’area di lavoro dei moduli offre la possibilità di modificare la semantica e la funzionalità della presentazione dell’interfaccia. Di seguito sono descritti i tipi di personalizzazioni per modificare lo stile, il layout, la formattazione, il branding e le funzionalità di base.

![cu_custom_workspace_example](assets/cu_customized_workspace_example.png)

Esempio di area di lavoro personalizzata

## Tipi di personalizzazioni {#types-of-customizations}

L’area di lavoro di AEM Forms supporta un’ampia varietà di personalizzazioni per aggiornare il layout dell’interfaccia utente, il suo aspetto, le sue funzionalità e molto altro. Le personalizzazioni comportano l’aggiornamento di uno o più dei seguenti elementi:

* Aspetto dell’interfaccia utente
* Funzionalità tramite personalizzazioni semantiche
* Riutilizzo dei componenti di HTML in altre applicazioni

### Modifiche all&#39;interfaccia utente {#user-interface-changes}

È possibile modificare l’aspetto, il layout e altre semantiche della presentazione di AEM Forms Workspace. Modifica l’area di lavoro personalizzando i file CSS, HTML e JavaScript™. Tutti i file predefiniti vengono forniti nell&#39;installazione predefinita.

Le fasi più comunemente applicabili sono trattate in [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Per esempi specifici di tali personalizzazioni, inclusi i passaggi dettagliati, vedi gli articoli correlati alla fine di questo articolo.

#### Informazioni sul foglio di stile {#understanding-the-style-sheet}

Prima di personalizzare l’area di lavoro, acquisire familiarità con il foglio di stile predefinito fornito con AEM Forms all’indirizzo /libs/ws/css/style.css.

Per personalizzare l&#39;area di lavoro, è consigliabile acquisire familiarità con il foglio di stile esistente, style.css, che si trova nella cartella /libs/ws/css. Di seguito sono descritti alcuni componenti importanti.

<table>
 <tbody>
  <tr>
   <th><p>Elemento CSS</p> </th>
   <th><p>Componente dell’interfaccia utente modificato</p> </th>
  </tr>
  <tr>
   <td><p>#intestazione</p> </td>
   <td><p>Intestazione dell’area di lavoro di AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Elenco categorie</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList.header</p> </td>
   <td><p>Intestazione dell’elenco delle categorie</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>Spazio sotto l'elenco delle categorie</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Categoria</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>Categoria selezionata e stile del mouse sulla categoria</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>Pagina del processo iniziale (elenco categorie chiuso)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar.tool, filterListBar.content</p> </td>
   <td><p>Pagina Da fare (elenco Filtro chiuso)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar.tool, processNameListBar.content</p> </td>
   <td><p>Pagina di tracciamento (elenco dei nomi dei processi chiusi)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>Elenco dei punti di partenza o elenco delle attività</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList.header, .tasklist.header</p> </td>
   <td><p>Intestazione di un elenco di punti iniziali o di un elenco di task</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>Punto iniziale o attività selezionati</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected .description</p> </td>
   <td><p>Descrizione del punto iniziale o dell'attività selezionata</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>Area attività</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>Menu a discesa dell’utente nell’intestazione</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Menu a discesa Ordina attività</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

L’aspetto dell’area di lavoro AEM Forms ne prende in prestito l’aspetto da un CSS. Personalizzando il CSS, puoi modificare la semantica di presentazione di workspace come font, colori, branding e layout.

I passaggi principali per la personalizzazione CSS sono:

* Crea un file CSS.
* Aggiungi elementi di stile a questo CSS. Per ulteriori informazioni, consulta Informazioni sugli stili CSS .
* Aggiorna i relativi riferimenti in `html.jsp`.

Per i passaggi esatti per eseguire queste personalizzazioni, vedi [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Il file CSS fornito con l’area di lavoro AEM Forms si trova in /libs/ws/css/. Per le personalizzazioni relative ai CSS, utilizza il [Pacchetto di spedizione](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Per esempi specifici di personalizzazioni relative a CSS, consulta gli argomenti correlati dell’Aiuto alla fine di questo articolo.

#### Immagine {#image}

Puoi personalizzare l’area di lavoro AEM Forms per aggiungere avatar di utenti o per aggiungere il logo della tua organizzazione. Per queste personalizzazioni, utilizza [Pacchetto di spedizione](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

I passaggi principali per le personalizzazioni alle immagini sono:

* Installa e configura WebDAV.
* Aggiungi nuove immagini.
* Aggiungi nuovi stili corrispondenti alle immagini aggiunte.
* Collega al nuovo file CSS in `html.jsp` file.

Per iniziare a personalizzare le immagini nell’area di lavoro di AEM Forms, segui la [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Per esempi specifici di personalizzazioni relative alle immagini, consulta gli argomenti della Guida correlati alla fine di questo articolo.

#### Modello HTML {#html-template}

I modelli di HTML consentono di definire l’aspetto e il layout dell’interfaccia utente dell’area di lavoro. Aggiornando i modelli predefiniti di HTML è possibile personalizzare l’interfaccia utente predefinita del layout.

I passaggi principali per le personalizzazioni al modello HTML sono i seguenti:

* In una cartella creata dall’utente, effettuare copie dei file predefiniti richiesti.
* Aggiungi nuovi modelli in una cartella definita dall’utente.
* Apporta aggiornamenti rilevanti ai file copiati, come il percorso del nuovo modello.

Per esempi specifici di tali personalizzazioni, consulta gli argomenti della Guida forniti alla fine di questo articolo. Scegli tra [Pacchetto di spedizione](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) o [Pacchetto di sviluppo](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), a seconda del modello da personalizzare.

### Modifiche semantiche {#semantic-changes}

Per modificare la funzionalità dell&#39;area di lavoro AEM Forms, modifica il codice sorgente JavaScript. Le modifiche alla funzionalità di base sono etichettate come modifiche semantiche. Puoi modificare modelli, visualizzazioni e modelli forniti come parte del codice sorgente dell’area di lavoro AEM Forms.

I passaggi principali per apportare modifiche semantiche per modificare la funzionalità dell’area di lavoro di AEM Forms sono i seguenti:

* In una cartella creata dall’utente, effettuare copie dei file predefiniti appropriati.
* Aggiungi nuovi modelli e visualizzazioni nella cartella definita dall’utente.
* Effettua aggiornamenti rilevanti come l&#39;aggiornamento dei percorsi dei modelli e delle visualizzazioni appena aggiunti nei file JavaScript predefiniti.
* Riduci il pacchetto per ottimizzare le prestazioni.

Per ulteriori informazioni concettuali sui componenti che fanno parte del codice sorgente, consulta [Descrizione dei componenti riutilizzabili](/help/forms/using/description-reusable-components.md). Per queste personalizzazioni, utilizza il pacchetto di sviluppo.

### Componenti riutilizzabili {#reusable-components}

Poiché AEM Forms Workspace è un software basato su componenti, può essere facilmente personalizzato e riutilizzato. È possibile integrare facilmente i componenti dell’area di lavoro con le applicazioni web.

Per ulteriori informazioni concettuali, consulta la sezione [Descrizione dei componenti riutilizzabili](/help/forms/using/description-reusable-components.md) e per istruzioni sull&#39;utilizzo dei componenti, consulta [Integrazione dei componenti dell’area di lavoro AEM Forms nelle applicazioni web](/help/forms/using/description-reusable-components.md).

## Creazione del codice dell’area di lavoro di AEM Forms {#building-html-workspace-code}

### pacchetto SDK {#sdk-package}

Il pacchetto contiene il codice sorgente dell’area di lavoro AEM Forms. Il pacchetto è disponibile all&#39;indirizzo `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

È destinato principalmente alle personalizzazioni, in quanto fornisce la capacità di generare:

* Pacchetti CRX per profili di spedizione, debug e sviluppo (menzionati di seguito in [Pacchetti CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Versione ridotta del codice personalizzato (per modifiche semantiche).

#### Contenuto WS {#ws-content}

* client-pkg:

   * src - Contiene gli artefatti necessari per creare i nodi CRX.
   * pom.xml - Script per creare pacchetti di distribuzione per vari profili Pacchetto WS-Deploy

* client-html:

   * assembly - Contiene zip.xml utilizzato dallo script per la creazione dell&#39;SDK dell&#39;area di lavoro AEM Forms.
   * src/main/webapp -

      * css - Contiene fogli di stile per l&#39;area di lavoro AEM Forms.
      * immagini - Contiene immagini utilizzate nell’area di lavoro di AEM Forms.
      * js:

         * libs - Contiene tutte le librerie di terze parti utilizzate nell&#39;area di lavoro di AEM Forms.
         * licenze - Contiene le licenze per i file HTML e JS e il codice per assegnare il prefisso a queste licenze per i rispettivi file sorgente.
         * minifier - Utilizzato per la combinazione, la minimizzazione e la regolificazione del codice JavaScript personalizzato.
         * resourcejs_optimizer : utilizzato per la combinazione, la minimizzazione e la regolarizzazione dell&#39;origine JavaScript.
         * resource_generator - Utilizzato per generare register.js e modelcontrollerpath.js.
         * runtime:

            * inizializzatore - Contiene initializer.js utilizzato per inizializzare le visualizzazioni della spina dorsale e i modelli utilizzati nell&#39;area di lavoro di AEM Forms.
            * modelli : contiene modelli di backbone di tutti i componenti presenti nell’area di lavoro di AEM Forms.
            * route - Contiene file JavaScript e file HTML che caricano il processo di avvio, lo strumento, il tracciamento e le preferenze nell&#39;area di lavoro di AEM Forms.
            * services - Contiene service.js utilizzato nell&#39;area di lavoro di AEM Forms. Tutte le chiamate al server vengono effettuate tramite service.js.
            * modelli : contiene tutti i modelli, ovvero i file HTML di tutte le visualizzazioni nell’area di lavoro di AEM Forms.
            * util - Contiene tutti i file di utilità (javascript) utilizzati nell&#39;area di lavoro di AEM Forms.
            * viste - Contiene le visualizzazioni della spina dorsale di tutti i componenti nell’area di lavoro di AEM Forms.
         * main.js
         * router.js
      * libs/ws: pdf.html e pluginPing.pdf vengono utilizzati per caricare PDF forms nell&#39;area di lavoro di AEM Forms e WSNextAdapter.swf viene utilizzato per caricare moduli e guide di SWF nell&#39;area di lavoro di AEM Forms.
      * impostazioni internazionali:

         * de-DE - Contiene translation.json per il tedesco.
         * en-US - Contiene translation.json per l&#39;inglese.
         * fr-FR - Contiene translation.json per francese.
         * ja-JP - Contiene translation.json per giapponese.
         * html.jsp - Contiene il codice per scoprire le impostazioni internazionali correnti del browser.
      * html.jsp
      * GET.jsp




### Pacchetto CRX {#crx-package}

Il pacchetto CRX può essere distribuito sull&#39;archivio CRX™. È disponibile all&#39;indirizzo `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Questo pacchetto può essere generato utilizzando i tre profili descritti di seguito.

| **Profilo** | **Descrizione** | **Utilizzo** |
|---|---|---|
| Profilo di spedizione | Questo profilo crea un pacchetto CRX della dimensione più piccola possibile utilizzando la minimizzazione. Questo pacchetto è il più efficiente. Tutti i file JavaScript™ vengono combinati e ridotti in un unico file JS. | Utilizza questo profilo quando non sono necessarie ulteriori modifiche semantiche nei file JS. |
| Profilo di debug | Questo profilo crea un pacchetto CRX moderatamente efficiente. La dimensione del pacchetto è leggermente superiore a quella del pacchetto creato utilizzando il profilo di spedizione. Questo pacchetto include la maggior parte dei file JavaScript combinati in un unico file JS. | Utilizza questo profilo per il debug. |
| Profilo di sviluppo | Questo profilo crea un pacchetto CRX della dimensione massima possibile. Tutti i file JavaScript sono disponibili separatamente, in quanto si trovano nel pacchetto SDK. | Utilizza questo profilo quando incorpori modifiche semantiche. |

#### Profilo di spedizione {#ship-profile}

#### Comando {#command}

* mvn clean -P Ship install sulla cartella client-pkg del pacchetto Origine spedito al cliente.
* L&#39;esecuzione del comando del profilo di spedizione funziona solo su una JVM a 64 bit.

#### Contenuto WS {#ws-content-1}

* css - Contiene style.css, ie.css e jquery-ui.css.
* immagini - Contiene tutte le immagini.
* js:

   * libs:

      * required - Contiene request.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.
   * runtime:

      * modelli : contiene tutti i modelli, ovvero i file HTML di tutti i componenti nell’area di lavoro di AEM Forms.
   * main.js (combinato, minimizzato e non modificato).
   * registry.js



* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Locale - Contiene .content.xml.
* impostazioni internazionali:

   * de-DE - Contiene translation.json per il tedesco.
   * en-US - Contiene translation.json per l&#39;inglese.
   * fr-FR - Contiene translation.json per francese.
   * ja-JP - Contiene translation.json per giapponese.
   * html.jsp - Contiene il codice per scoprire le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Profilo di debug {#debug-profile}

#### Comando {#command-1}

* mvn clean -P Debug install su client-pkg
* L&#39;esecuzione del comando di profilo di debug funziona solo su JVM a 64 bit.

#### Contenuto WS {#ws-content-2}

* css - Contiene style.css, ie.css e jqueri-ui.css.
* immagini - Contiene tutte le immagini.
* js:

   * libs:

      * required - Contiene request.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.
   * runtime:

      * modelli : contiene tutti i modelli, ovvero i file HTML di tutti i componenti nell’area di lavoro di AEM Forms.
   * main.js (combinato).
   * registry.js



* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Locale - Contiene .content.xml.
* impostazioni internazionali:

   * de-DE - Contiene translation.json per il tedesco.
   * en-US - Contiene translation.json per l&#39;inglese.
   * fr-FR - Contiene translation.json per francese.
   * ja-JP - Contiene translation.json per giapponese.
   * html.jsp - Contiene il codice per scoprire le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Profilo di sviluppo {#dev-profile}

#### Comando {#command-2}

mvn clean -P Dev install su client-pkg

#### Contenuto WS {#ws-content-3}

* css - Contiene style.css, ie.css e jqueri-ui.css.
* immagini - Contiene tutte le immagini.
* js:

   * libs - Contiene tutte le librerie utilizzate nell&#39;area di lavoro di AEM Forms.
   * required - Contiene request.js
   * jqueryui - Contiene jquery.ui.datepicker.ja.js
   * runtime:

      * inizializzatore - Contiene initializer.js e modelcontrollerpath.js.
      * Modelli : contiene modelli di tutti i componenti nell’area di lavoro di AEM Forms.
      * route - Contiene file JavaScript e file HTML che caricano il processo di avvio, lo strumento, il tracciamento e le preferenze nell&#39;area di lavoro di AEM Forms.
      * services - Contiene service.js utilizzato nell&#39;area di lavoro di AEM Forms.
      * modelli : contiene tutti i modelli, ovvero i file HTML di tutti i componenti nell’area di lavoro di AEM Forms.
      * util - Contiene tutti i file di utilità (JavaScript) utilizzati nell&#39;area di lavoro di AEM Forms.
      * viste - Contiene le visualizzazioni di tutti i componenti nell’area di lavoro di AEM Forms.
   * main.js
   * registry.js
   * router.js


* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Locale - Contiene .content.xml.
* impostazioni internazionali:

   * de-DE - Contiene translation.json per il tedesco.
   * en-US - Contiene translation.json per l&#39;inglese.
   * fr-FR - Contiene translation.json per francese.
   * ja-JP - Contiene translation.json per giapponese.
   * html.jsp - Contiene il codice per scoprire le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
