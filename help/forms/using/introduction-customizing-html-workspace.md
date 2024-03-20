---
title: Introduzione alla personalizzazione dell’area di lavoro dei moduli AEM
description: Introduzione rapida, con informazioni concettuali e tecniche, per personalizzare lo spazio di lavoro LiveCycle AEM Forms per la gestione dei processi.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 0%

---

# Introduzione alla personalizzazione dell’area di lavoro dei moduli AEM{#introduction-to-customizing-aem-form-workspace}

L’area di lavoro dei moduli AEM offre funzionalità per modificare la semantica delle presentazioni e la funzionalità della relativa interfaccia. Di seguito sono descritti i tipi di personalizzazioni per modificare lo stile, il layout, la formattazione, il branding e le funzionalità di base.

![cu_custom_workspace_example](assets/cu_customized_workspace_example.png)

Esempio di area di lavoro personalizzata

## Tipi di personalizzazioni {#types-of-customizations}

AEM Forms Workspace supporta un’ampia gamma di personalizzazioni per aggiornare il layout dell’interfaccia utente, il suo aspetto, la sua funzionalità e molto altro. Le personalizzazioni implicano l’aggiornamento di uno o più dei seguenti elementi:

* Aspetti dell&#39;interfaccia utente
* Funzionalità con personalizzazioni semantiche
* Riutilizzo dei componenti HTML in altre applicazioni

### Modifiche all’interfaccia utente {#user-interface-changes}

Puoi modificare l’aspetto, il layout e altre semantiche di presentazione dell’area di lavoro AEM Forms. Modifica l’area di lavoro personalizzando i file CSS, HTML e JavaScript™. Tutti i file predefiniti vengono forniti nell&#39;installazione predefinita.

I passaggi più comunemente applicabili sono descritti in [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Per esempi specifici di tali personalizzazioni, inclusi i passaggi dettagliati, consulta gli articoli correlati alla fine di questo articolo.

#### Informazioni sul foglio di stile {#understanding-the-style-sheet}

Prima di personalizzare l’area di lavoro, acquisisci familiarità con il foglio di stile predefinito fornito con AEM Forms all’indirizzo /libs/ws/css/style.css.

Per personalizzare l&#39;area di lavoro, è consigliabile familiarizzare con il foglio di stile esistente, style.css, nella cartella /libs/ws/css. Di seguito sono descritti alcuni componenti importanti.

<table>
 <tbody>
  <tr>
   <th><p>Elemento CSS</p> </th>
   <th><p>Componente dell’interfaccia utente modificato</p> </th>
  </tr>
  <tr>
   <td><p>#header</p> </td>
   <td><p>Intestazione dell’area di lavoro di AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Elenco categorie</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>Intestazione dell’elenco delle categorie</p> </td>
  </tr>
  <tr>
   <td><p>.categorie, .filtri</p> </td>
   <td><p>Spazio sotto l’elenco delle categorie</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Categoria</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>Categoria selezionata e passaggio del mouse sullo stile della categoria</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>Pagina Avvia processo (elenco categorie chiuso)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>Pagina Da fare (elenco filtri chiuso)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>Pagina di tracciamento (elenco chiuso dei nomi dei processi)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>L'elenco dei punti d'inizio o l'elenco delle attività</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>Intestazione di un elenco di punti iniziali o di un elenco di attività</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>Il punto d'inizio o l'attività selezionata</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected .description</p> </td>
   <td><p>Descrizione del punto d'inizio o dell'attività selezionata</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>L’area Attività</p> </td>
  </tr>
  <tr>
   <td><p>#header a discesa</p> </td>
   <td><p>Menu a discesa utente nell’intestazione</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Menu a discesa Ordina attività</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

L’aspetto dell’area di lavoro di AEM Forms deriva da un CSS. Personalizzando il CSS, puoi modificare la semantica di presentazione dell’area di lavoro, ad esempio font, colori, branding e layout.

I passaggi principali per la personalizzazione CSS sono:

* Crea un file CSS.
* Aggiungi elementi di stile a questo CSS. Per ulteriori informazioni, consulta Informazioni sugli stili CSS.
* Aggiornare i relativi riferimenti in `html.jsp`.

Per i passaggi esatti per eseguire queste personalizzazioni, consulta [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Il file CSS fornito con l’area di lavoro di AEM Forms si trova in /libs/ws/css/. Per le personalizzazioni relative ai CSS, utilizza [Spedisci pacchetto](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Per esempi specifici di personalizzazioni relative a CSS, consulta gli argomenti della Guida correlati alla fine di questo articolo.

#### Immagine {#image}

Puoi personalizzare l’area di lavoro di AEM Forms per aggiungere avatar di utenti o il logo della tua organizzazione. Per queste personalizzazioni, utilizza [Spedisci pacchetto](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

I passaggi principali per la personalizzazione delle immagini sono i seguenti:

* Installare e configurare WebDAV.
* Aggiungere nuove immagini.
* Aggiungi nuovi stili corrispondenti alle immagini aggiunte.
* Collegamento al nuovo file CSS in `html.jsp` file.

Per iniziare a personalizzare le immagini nell’area di lavoro di AEM Forms, segui la [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Per esempi specifici di personalizzazioni relative alle immagini, consulta gli argomenti della Guida correlati alla fine di questo articolo.

#### Modello HTML {#html-template}

I modelli di HTML consentono di definire l&#39;aspetto e il layout dell&#39;interfaccia utente del workspace. Aggiornando i modelli di HTML predefiniti è possibile personalizzare l&#39;interfaccia utente predefinita del layout.

I passaggi di primo livello per le personalizzazioni del modello di HTML sono:

* In una cartella creata dall&#39;utente, creare copie dei file predefiniti richiesti.
* Aggiungere nuovi modelli nella cartella definita dall&#39;utente.
* Apporta aggiornamenti rilevanti ai file copiati come, il percorso del nuovo modello.

Per esempi specifici di tali personalizzazioni, consulta gli argomenti dell’Aiuto forniti alla fine di questo articolo. Scegli tra [Spedisci pacchetto](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) o [Pacchetto di sviluppo](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), a seconda del modello da personalizzare.

### Modifiche semantiche {#semantic-changes}

Per modificare la funzionalità dell’area di lavoro di AEM Forms, modifica il codice sorgente JavaScript. Le modifiche apportate alle funzionalità di base sono etichettate come modifiche semantiche. Puoi modificare modelli, viste e modelli forniti come parte del codice sorgente dell’area di lavoro di AEM Forms.

I passaggi di primo livello per apportare modifiche semantiche per modificare le funzionalità dell’area di lavoro di AEM Forms sono i seguenti:

* In una cartella creata dall&#39;utente, creare copie dei file predefiniti appropriati.
* Aggiungere nuovi modelli e viste nella cartella definita dall&#39;utente.
* Effettua aggiornamenti rilevanti come l’aggiornamento dei percorsi dei modelli e delle viste appena aggiunti nei file JavaScript predefiniti.
* Minimizza il pacchetto per ottimizzare le prestazioni.

Per ulteriori informazioni sui componenti che fanno parte del codice sorgente, vedi [Descrizione dei componenti riutilizzabili](/help/forms/using/description-reusable-components.md). Per queste personalizzazioni, utilizza il pacchetto di sviluppo.

### Componenti riutilizzabili {#reusable-components}

Poiché AEM Forms Workspace è un software basato su componenti, può essere facilmente personalizzato e riutilizzato. Puoi integrare facilmente i componenti di Workspace con le applicazioni web.

Per ulteriori informazioni concettuali, vedere [Descrizione dei componenti riutilizzabili](/help/forms/using/description-reusable-components.md) e per istruzioni sull’utilizzo dei componenti, consulta [Integrazione dei componenti dell’area di lavoro di AEM Forms nelle applicazioni web](/help/forms/using/description-reusable-components.md).

## Creazione del codice dell’area di lavoro di AEM Forms {#building-html-workspace-code}

### Pacchetto SDK {#sdk-package}

Il pacchetto contiene il codice sorgente dell’area di lavoro AEM Forms. Il pacchetto è disponibile all’indirizzo `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

È destinato principalmente alle personalizzazioni, in quanto fornisce la capacità di generare:

* Pacchetti CRX per profili di spedizione, debug e sviluppo (menzionati di seguito in [Pacchetti CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Versione ridotta del codice personalizzato (per modifiche semantiche).

#### Contenuto WS {#ws-content}

* client-pkg:

   * src - Contiene gli artefatti necessari per creare i nodi CRX.
   * pom.xml - Script per la generazione di pacchetti di distribuzione per vari profili Pacchetto di distribuzione WS

* client-html:

   * assembly: contiene il file zip.xml utilizzato dallo script per la creazione dell’SDK di AEM Forms Workspace.
   * src/main/webapp -

      * css: contiene fogli di stile per l’area di lavoro di AEM Forms.
      * immagini: contiene le immagini utilizzate nell’area di lavoro di AEM Forms.
      * js:

         * libs: contiene tutte le librerie di terze parti utilizzate nell’area di lavoro di AEM Forms.
         * licenze: contiene le licenze per i file HTML e JS e il codice per anteporre queste licenze ai rispettivi file sorgente.
         * minifier: utilizzato per la combinazione, la minimizzazione e l’aggiornamento del codice JavaScript personalizzato.
         * resourcejs_optimizer - Utilizzato per la combinazione, la minimizzazione e l’aggiornamento dell’origine JavaScript.
         * resource_generator - Utilizzato per generare register.js e modelcontrollerpath.js.
         * runtime:

            * inizializzatore: contiene il file initializer.js utilizzato per inizializzare le viste e i modelli della struttura principale utilizzati nell’area di lavoro di AEM Forms.
            * modelli: contiene i modelli di struttura di tutti i componenti presenti nell’area di lavoro di AEM Forms.
            * route: contiene file JavaScript e HTML che caricano il processo iniziale, le attività, il tracciamento e le preferenze nell’area di lavoro AEM Forms.
            * services: contiene service.js utilizzato nell’area di lavoro di AEM Forms. Tutte le chiamate al server vengono effettuate tramite service.js.
            * modelli: contiene tutti i modelli, ovvero i file HTML di tutte le visualizzazioni nell’area di lavoro di AEM Forms.
            * util: contiene tutti i file di utilità (javascript) utilizzati nell’area di lavoro di AEM Forms.
            * visualizzazioni: contiene le visualizzazioni principali di tutti i componenti nell’area di lavoro di AEM Forms.

         * main.js
         * router.js

      * libs/ws: pdf.html e pluginPing.pdf vengono utilizzati per caricare i PDF forms nell’area di lavoro di AEM Forms e WSNextAdapter.swf viene utilizzato per caricare i moduli e le guide di SWF nell’area di lavoro di AEM Forms.
      * lingue:

         * de-DE - Contiene translation.json per il tedesco.
         * en-US - Contiene translation.json per inglese.
         * fr-FR - Contiene translation.json per il francese.
         * ja-JP - Contiene translation.json per il giapponese.
         * html.jsp - Contiene il codice per individuare le impostazioni internazionali correnti del browser.

      * html.jsp
      * GET.jsp

### Pacchetto CRX {#crx-package}

Il pacchetto CRX può essere distribuito nell’archivio CRX™. È disponibile all’indirizzo `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Questo pacchetto può essere creato utilizzando i tre profili descritti di seguito.

| **Profilo** | **Descrizione** | **Utilizzo** |
|---|---|---|
| Profilo di spedizione | Questo profilo crea un pacchetto CRX delle dimensioni più piccole possibili utilizzando la minimizzazione. Questo pacchetto è il più efficiente. Tutti i file JavaScript™ vengono combinati e minimizzati in un singolo file JS. | Utilizza questo profilo quando nei file JS non sono necessarie ulteriori modifiche semantiche. |
| Debug profilo | Questo profilo crea un pacchetto CRX moderatamente efficiente. La dimensione del pacchetto è leggermente superiore a quella del pacchetto creato mediante il profilo di spedizione. Questo pacchetto contiene la maggior parte dei file JavaScript combinati in un singolo file JS. | Usa questo profilo per il debug. |
| Profilo di sviluppo | Questo profilo crea un pacchetto CRX delle dimensioni più grandi possibili. Tutti i file JavaScript sono disponibili separatamente, come nel pacchetto SDK. | Utilizza questo profilo per incorporare modifiche semantiche. |

#### Profilo di spedizione {#ship-profile}

#### Comando {#command}

* mvn clean -P Ship install nella cartella client-pkg del pacchetto di origine spedito al client.
* L&#39;esecuzione del comando del profilo di spedizione funziona solo su una JVM a 64 bit.

#### Contenuto WS {#ws-content-1}

* css: contiene style.css, ie.css e jquery-ui.css.
* images - Contiene tutte le immagini.
* js:

   * libs:

      * require - Contiene require.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.

   * runtime:

      * modelli: contiene tutti i modelli, ovvero i file HTML di tutti i componenti nell’area di lavoro di AEM Forms.

   * main.js (combinato, minimizzato e semplificato).
   * registry.js

* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Impostazioni internazionali - Contiene .content.xml.
* lingue:

   * de-DE - Contiene translation.json per il tedesco.
   * en-US - Contiene translation.json per inglese.
   * fr-FR - Contiene translation.json per il francese.
   * ja-JP - Contiene translation.json per il giapponese.
   * html.jsp - Contiene il codice per individuare le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Debug profilo {#debug-profile}

#### Comando {#command-1}

* mvn clean -P Debug install on client-pkg
* L&#39;esecuzione del comando Debug Profile funziona solo su JVM a 64 bit.

#### Contenuto WS {#ws-content-2}

* css: contiene style.css, ie.css e jqueri-ui.css.
* images - Contiene tutte le immagini.
* js:

   * libs:

      * require - Contiene require.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.

   * runtime:

      * modelli: contiene tutti i modelli, ovvero i file HTML di tutti i componenti nell’area di lavoro di AEM Forms.

   * main.js (combinato).
   * registry.js

* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Impostazioni internazionali - Contiene .content.xml.
* lingue:

   * de-DE - Contiene translation.json per il tedesco.
   * en-US - Contiene translation.json per inglese.
   * fr-FR - Contiene translation.json per il francese.
   * ja-JP - Contiene translation.json per il giapponese.
   * html.jsp - Contiene il codice per individuare le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Profilo di sviluppo {#dev-profile}

#### Comando {#command-2}

mvn clean -P Dev install su pkg client

#### Contenuto WS {#ws-content-3}

* css: contiene style.css, ie.css e jqueri-ui.css.
* images - Contiene tutte le immagini.
* js:

   * libs: contiene tutte le librerie utilizzate nell’area di lavoro di AEM Forms.
   * require - Contiene require.js
   * jqueryui - Contiene jquery.ui.datepicker.ja.js
   * runtime:

      * initializer: contiene initializer.js e modelcontrollerpath.js.
      * modelli: contiene modelli di tutti i componenti nell’area di lavoro di AEM Forms.
      * route: contiene file JavaScript e HTML che caricano il processo iniziale, le attività, il tracciamento e le preferenze nell’area di lavoro AEM Forms.
      * services: contiene service.js utilizzato nell’area di lavoro di AEM Forms.
      * modelli: contiene tutti i modelli, ovvero i file HTML di tutti i componenti nell’area di lavoro di AEM Forms.
      * util: contiene tutti i file di utilità (JavaScript) utilizzati nell’area di lavoro di AEM Forms.
      * visualizzazioni: contiene le visualizzazioni di tutti i componenti nell’area di lavoro di AEM Forms.

   * main.js
   * registry.js
   * router.js

* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Impostazioni internazionali - Contiene .content.xml.
* lingue:

   * de-DE - Contiene translation.json per il tedesco.
   * en-US - Contiene translation.json per inglese.
   * fr-FR - Contiene translation.json per il francese.
   * ja-JP - Contiene translation.json per il giapponese.
   * html.jsp - Contiene il codice per individuare le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
