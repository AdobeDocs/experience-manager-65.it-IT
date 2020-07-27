---
title: Introduzione alla personalizzazione dell'area di lavoro dei moduli AEM
seo-title: Introduzione alla personalizzazione dell'area di lavoro dei moduli AEM
description: Breve introduzione, con informazioni concettuali e tecniche, alla personalizzazione dell'area di lavoro AEM Forms LiveCycle per la gestione dei processi.
seo-description: Breve introduzione, con informazioni concettuali e tecniche, alla personalizzazione dell'area di lavoro AEM Forms LiveCycle per la gestione dei processi.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 0%

---


# Introduzione alla personalizzazione dell&#39;area di lavoro dei moduli AEM{#introduction-to-customizing-aem-form-workspace}

L’area di lavoro dei moduli di AEM offre funzionalità per modificare la semantica di presentazione e la funzionalità dell’interfaccia. Di seguito sono descritti i tipi di personalizzazioni per modificare lo stile, il layout, la formattazione, il marchio e le funzionalità di base.

![cu_custom_workspace_example](assets/cu_customized_workspace_example.png)

Esempio di un’area di lavoro personalizzata

## Tipi di personalizzazioni {#types-of-customizations}

L’area di lavoro AEM Forms supporta un’ampia varietà di personalizzazioni per aggiornare il layout dell’interfaccia utente, il suo aspetto, la sua funzionalità e molto altro ancora. Le personalizzazioni richiedono l&#39;aggiornamento di uno o più dei seguenti elementi:

* Aspetto dell’interfaccia utente
* Funzionalità mediante personalizzazioni semantiche
* Riutilizzo di componenti HTML in altre applicazioni

### Modifiche all&#39;interfaccia utente {#user-interface-changes}

Potete modificare l’aspetto, il layout e altre semantica delle presentazioni dell’area di lavoro AEM Forms. Modificate l&#39;area di lavoro personalizzando i file CSS, HTML e JavaScript™. Tutti i file predefiniti vengono forniti nell’installazione predefinita.

I passaggi più comuni sono descritti nei passaggi [Generici per la personalizzazione](../../forms/using/generic-steps-html-workspace-customization.md)dell’area di lavoro AEM Forms. Per esempi specifici di tali personalizzazioni, compresi i passaggi dettagliati, consultate gli articoli correlati alla fine di questo articolo.

#### Informazioni sul foglio di stile {#understanding-the-style-sheet}

Prima di personalizzare l&#39;area di lavoro, è necessario avere familiarità con il foglio di stile predefinito fornito con i AEM Forms all&#39;indirizzo /libs/ws/css/style.css.

Per personalizzare l&#39;area di lavoro, è consigliabile acquisire familiarità con il foglio di stile esistente, style.css, che si trova nella cartella /libs/ws/css. Alcuni componenti importanti sono descritti di seguito.

<table>
 <tbody>
  <tr>
   <th><p>Elemento CSS</p> </th>
   <th><p>Componente interfaccia utente modificato</p> </th>
  </tr>
  <tr>
   <td><p>#intestazione</p> </td>
   <td><p>Intestazione dell'area di lavoro AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Elenco categorie</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList.header</p> </td>
   <td><p>Intestazione dell'elenco delle categorie</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filtri</p> </td>
   <td><p>Spazio sotto l'elenco delle categorie</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Categoria</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>Categoria selezionata e stile del mouse sopra la categoria</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar.tool, categoryListBar.content</p> </td>
   <td><p>Pagina del processo iniziale (elenco delle categorie chiuso)</p> </td>
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
   <td><p>.startPointList, .asklist</p> </td>
   <td><p>L'elenco di punti di avvio o l'elenco delle attività</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .asklist .header</p> </td>
   <td><p>Intestazione di un elenco di punti di avvio o di un elenco di attività</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>Punto di inizio o attività selezionato</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected .description</p> </td>
   <td><p>Descrizione del punto di partenza o dell'attività selezionato</p> </td>
  </tr>
  <tr>
   <td><p>#task</p> </td>
   <td><p>Area Attività</p> </td>
  </tr>
  <tr>
   <td><p>#header.dropdown</p> </td>
   <td><p>Menu a discesa dell'utente nell'intestazione</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Elenco a discesa Ordina attività</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

L’aspetto dell’area di lavoro AEM Forms ne limita l’aspetto da un CSS. Personalizzando il CSS, potete modificare la semantica di presentazione dell&#39;area di lavoro come font, colori, marchio e layout.

I passaggi di primo livello per la personalizzazione CSS sono:

* Create un file CSS.
* Aggiungete elementi di stile a questo CSS. Per ulteriori informazioni, consultate Stili CSS.
* Aggiorna i relativi riferimenti in `html.jsp`.

Per i passaggi esatti per eseguire queste personalizzazioni, consultate Passaggi [generici per la personalizzazione](../../forms/using/generic-steps-html-workspace-customization.md)dell&#39;area di lavoro AEM Forms. Il file CSS fornito con l&#39;area di lavoro AEM Forms è in /libs/ws/css/. Per le personalizzazioni relative ai CSS, utilizzate il pacchetto [Spedizione](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Per esempi specifici di personalizzazioni relative ai CSS, consultate i relativi argomenti della guida alla fine di questo articolo.

#### Immagine {#image}

Potete personalizzare l’area di lavoro AEM Forms per aggiungere avatar di utenti o per aggiungere il logo dell’organizzazione. Per queste personalizzazioni, utilizzate Pacchetto [](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)spedizione.

I passaggi principali per la personalizzazione delle immagini sono:

* Installare e configurare WebDAV.
* Aggiungete nuove immagini.
* Aggiungete nuovi stili corrispondenti alle immagini aggiunte.
* Collegate il nuovo file CSS nel `html.jsp` file.

Per iniziare a personalizzare le immagini nell’area di lavoro AEM Forms, seguite i passaggi [Generici per la personalizzazione](../../forms/using/generic-steps-html-workspace-customization.md)dell’area di lavoro AEM Forms. Per esempi specifici di personalizzazioni relative alle immagini, consultate gli argomenti della guida correlati alla fine di questo articolo.

#### HTML template {#html-template}

I modelli HTML consentono di definire l’aspetto e il layout dell’interfaccia utente dell’area di lavoro. Aggiornando i modelli HTML predefiniti potete personalizzare l&#39;interfaccia utente predefinita del layout.

I passaggi principali per le personalizzazioni al modello HTML sono:

* In una cartella creata dall’utente, effettuate copie dei file predefiniti richiesti.
* Aggiungere nuovi modelli in una cartella definita dall’utente.
* Apportate ai file copiati aggiornamenti rilevanti, ad esempio il percorso del nuovo modello.

Per esempi specifici di tali personalizzazioni, consultate gli argomenti della guida forniti alla fine di questo articolo. Scegliete tra il pacchetto [](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) spedizione o il pacchetto [](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)sviluppatore, a seconda del modello da personalizzare.

### Modifiche semantiche {#semantic-changes}

Per modificare la funzionalità dell&#39;area di lavoro AEM Forms, modificate il codice sorgente JavaScript. Le modifiche nella funzionalità di base sono etichettate come modifiche semantiche. Potete modificare modelli, viste e modelli forniti come parte del codice sorgente dell’area di lavoro AEM Forms.

I passaggi di livello principale per apportare modifiche semantiche per modificare la funzionalità dell’area di lavoro dei AEM Forms sono:

* In una cartella creata dall’utente, effettuate copie dei file predefiniti appropriati.
* Aggiungere nuovi modelli e nuove viste nella cartella definita dall’utente.
* Apportate aggiornamenti importanti come l&#39;aggiornamento dei percorsi dei modelli e delle visualizzazioni appena aggiunti nei file JavaScript predefiniti.
* Riducete il pacchetto per ottimizzare le prestazioni.

Per ulteriori informazioni concettuali sui componenti che fanno parte del codice sorgente, vedere la [Descrizione dei componenti](/help/forms/using/description-reusable-components.md)riutilizzabili. Per queste personalizzazioni, utilizzate il pacchetto Dev.

### Componenti riutilizzabili {#reusable-components}

Poiché l&#39;area di lavoro AEM Forms è un software basato su componenti, può essere facilmente personalizzato e riutilizzato. È possibile integrare facilmente i componenti dell’area di lavoro con le applicazioni Web.

Per ulteriori informazioni concettuali, vedere [Descrizione dei componenti](/help/forms/using/description-reusable-components.md) riutilizzabili e per istruzioni sull’uso dei componenti, vedere [Integrazione dei componenti dell’area di lavoro AEM Forms nelle applicazioni](/help/forms/using/description-reusable-components.md)Web.

## Creazione del codice dell’area di lavoro AEM Forms {#building-html-workspace-code}

### pacchetto SDK {#sdk-package}

Il pacchetto contiene il codice sorgente dell’area di lavoro AEM Forms. Il pacchetto è disponibile all&#39;indirizzo `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

È principalmente destinato alle personalizzazioni, in quanto fornisce la capacità di generare:

* Pacchetti CRX per i profili Spedizione, Debug e Sviluppo (indicati di seguito nei pacchetti [](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)CRX).
* Versione ridotta del codice personalizzato (per modifiche semantiche).

#### Contenuto WS {#ws-content}

* client-pkg:

   * src - Contiene artefatti necessari per creare nodi CRX.
   * pom.xml - Script per creare pacchetti di distribuzione per vari profili WS-Deploy Package

* client-html:

   * assembly - Contiene zip.xml utilizzato dallo script per la creazione dell&#39;SDK dell&#39;area di lavoro AEM Forms.
   * src/main/webapp -

      * css - Contiene fogli di stile per l&#39;area di lavoro AEM Forms.
      * immagini - Contiene immagini utilizzate nell&#39;area di lavoro AEM Forms.
      * js:

         * libs - Contiene tutte le librerie di terze parti utilizzate nell&#39;area di lavoro AEM Forms.
         * licenze - Contiene le licenze per i file HTML e JS, nonché il codice per assegnare il prefisso a queste licenze per i rispettivi file sorgente.
         * minifier - Utilizzato per la combinazione, la minificazione e la regolificazione del codice JavaScript personalizzato.
         * resourcesjs_Optimizer - Utilizzato per la combinazione, la riduzione e la regolificazione dell&#39;origine JavaScript.
         * resource_generator - Utilizzato per generare register.js e modelcontrol.path.js.
         * runtime:

            * inizializzatore - Contiene Initializer.js utilizzato per inizializzare le viste e i modelli di backbone utilizzati nell&#39;area di lavoro AEM Forms.
            * modelli - Contiene modelli di dorsale di tutti i componenti presenti nell&#39;area di lavoro AEM Forms.
            * route - Contiene i file JavaScript e HTML che caricano il processo di avvio, lo strumento, il tracciamento e le preferenze nell&#39;area di lavoro AEM Forms.
            * services - Contiene service.js utilizzato nell&#39;area di lavoro AEM Forms. Tutte le chiamate al server vengono effettuate tramite service.js.
            * modelli - Contiene tutti i modelli, ovvero file HTML di tutte le viste nell&#39;area di lavoro AEM Forms.
            * util - Contiene tutti i file di utilità (javascript) utilizzati nell&#39;area di lavoro AEM Forms.
            * viste - Contiene le viste della colonna vertebrale di tutti i componenti nell&#39;area di lavoro AEM Forms.
         * main.js
         * router.js
      * libs/ws: pdf.html e pluginPing.pdf vengono utilizzati per caricare PDF forms nell&#39;area di lavoro AEM Forms e WSNextAdapter.swf viene utilizzato per caricare moduli SWF e Guide nell&#39;area di lavoro AEM Forms.
      * impostazioni internazionali:

         * de-DE - Contiene translate.json per il tedesco.
         * en-US - Contiene translate.json per l&#39;inglese.
         * fr-FR - Contiene translate.json per il francese.
         * ja-JP - Contiene translate.json per il giapponese.
         * html.jsp - Contiene il codice per conoscere le impostazioni internazionali correnti del browser.
      * html.jsp
      * GET.jsp




### Pacchetto CRX {#crx-package}

Il pacchetto CRX può essere distribuito nell&#39;archivio CRX™. È disponibile all&#39;indirizzo `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Questo pacchetto può essere creato utilizzando i tre profili descritti di seguito.

| **Profilo** | **Descrizione** | **Utilizzo** |
|---|---|---|
| Profilo di spedizione | Questo profilo crea un pacchetto CRX di dimensioni ridotte, utilizzando la riduzione. Questo pacchetto è il più efficiente. Tutti i file JavaScript™ vengono combinati e ridotti in un unico file JS. | Utilizzate questo profilo quando non sono necessarie ulteriori modifiche semantiche nei file JS. |
| Debug, profilo | Questo profilo crea un pacchetto CRX moderatamente efficiente. La dimensione del pacchetto è leggermente superiore a quella del pacchetto creato utilizzando il profilo di spedizione. Questo pacchetto include la maggior parte dei file JavaScript combinati in un unico file JS. | Utilizzate questo profilo per il debug. |
| Profilo sviluppatore | Questo profilo crea un pacchetto CRX della dimensione massima possibile. Tutti i file JavaScript sono disponibili separatamente, così come si trovano nel pacchetto SDK. | Utilizzate questo profilo quando incorporate modifiche semantiche. |

#### Profilo di spedizione {#ship-profile}

#### Comando {#command}

* mvn Clean -P Ship install sulla cartella client-pkg del pacchetto Source spedito al client.
* L&#39;esecuzione del comando del profilo di spedizione funziona solo su una JVM a 64 bit.

#### Contenuto WS {#ws-content-1}

* css - Contiene style.css, ie.css e jquery-ui.css.
* immagini - Contiene tutte le immagini.
* js:

   * libs:

      * request - Contiene request.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.
   * runtime:

      * modelli - Contiene tutti i modelli, ovvero file HTML di tutti i componenti nell’area di lavoro AEM Forms.
   * main.js (combinato, minificato e non specificato).
   * registry.js



* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Impostazioni internazionali - Contiene .content.xml.
* impostazioni internazionali:

   * de-DE - Contiene translate.json per il tedesco.
   * en-US - Contiene translate.json per l&#39;inglese.
   * fr-FR - Contiene translate.json per il francese.
   * ja-JP - Contiene translate.json per il giapponese.
   * html.jsp - Contiene il codice per conoscere le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Debug Profile {#debug-profile}

#### Comando {#command-1}

* mvn Clean -P Debug install su client-pkg
* L&#39;esecuzione del comando del profilo di debug funziona solo su JVM a 64 bit.

#### Contenuto WS {#ws-content-2}

* css - Contiene style.css, ie.css e jqueri-ui.css.
* immagini - Contiene tutte le immagini.
* js:

   * libs:

      * request - Contiene request.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.
   * runtime:

      * modelli - Contiene tutti i modelli, ovvero file HTML di tutti i componenti nell’area di lavoro AEM Forms.
   * main.js (combinato).
   * registry.js



* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Impostazioni internazionali - Contiene .content.xml.
* impostazioni internazionali:

   * de-DE - Contiene translate.json per il tedesco.
   * en-US - Contiene translate.json per l&#39;inglese.
   * fr-FR - Contiene translate.json per il francese.
   * ja-JP - Contiene translate.json per il giapponese.
   * html.jsp - Contiene il codice per conoscere le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Profilo sviluppatore {#dev-profile}

#### Comando {#command-2}

mvn clean -P Dev install su client-pkg

#### Contenuto WS {#ws-content-3}

* css - Contiene style.css, ie.css e jqueri-ui.css.
* immagini - Contiene tutte le immagini.
* js:

   * libs - Contiene tutte le librerie utilizzate nell&#39;area di lavoro AEM Forms.
   * request - Contiene request.js
   * jqueryui - Contiene jquery.ui.datepicker.ja.js
   * runtime:

      * inizializzatore - Contiene Initializer.js e modelcontrollerpath.js.
      * modelli - Contiene modelli di tutti i componenti nell&#39;area di lavoro AEM Forms.
      * route - Contiene i file JavaScript e HTML che caricano il processo di avvio, lo strumento, il tracciamento e le preferenze nell&#39;area di lavoro AEM Forms.
      * services - Contiene service.js utilizzato nell&#39;area di lavoro AEM Forms.
      * modelli - Contiene tutti i modelli, ovvero file HTML di tutti i componenti nell’area di lavoro AEM Forms.
      * util - Contiene tutti i file di utilità (JavaScript) utilizzati nell&#39;area di lavoro AEM Forms.
      * viste - Contiene le viste di tutti i componenti nell’area di lavoro AEM Forms.
   * main.js
   * registry.js
   * router.js


* libs:

   * ws - Contiene pluginPing.pdf, pdf.html e WSNextAdapter.swf.

* Impostazioni internazionali - Contiene .content.xml.
* impostazioni internazionali:

   * de-DE - Contiene translate.json per il tedesco.
   * en-US - Contiene translate.json per l&#39;inglese.
   * fr-FR - Contiene translate.json per il francese.
   * ja-JP - Contiene translate.json per il giapponese.
   * html.jsp - Contiene il codice per conoscere le impostazioni internazionali correnti del browser.

* Indice - Contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
