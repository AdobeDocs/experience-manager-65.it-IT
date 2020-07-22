---
title: Page Exporter
description: Scoprite come utilizzare AEM Page Exporter.
translation-type: tm+mt
source-git-commit: b0126894dec33648a24c0308972aa5b47d7e4b84
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---


# Page Exporter{#the-page-exporter}

AEM consente di esportare una pagina come pagina Web completa con immagini `.js` e `.css` file.

Una volta configurata, richiedete l’esportazione di una pagina dal browser sostituendola `html` con `export.zip` l’URL. Questo genera un file di archivio (zip) contenente la pagina di cui è stato effettuato il rendering in formato html, insieme alle risorse a cui viene fatto riferimento. Tutti i percorsi della pagina (ad esempio, i percorsi delle immagini) vengono riscritti in modo da puntare ai file inclusi nell&#39;archivio o alle risorse sul server. Il file di archivio (zip) può quindi essere scaricato dal browser.

>!![NOTE]
A seconda del browser e delle impostazioni, il download sarà:
* un file di archivio (`<page-name>.export.zip`)
* una cartella (`<page-name>`); effettivamente il file di archivio già espanso


## Esportazione di una pagina {#exporting-a-page}

Nei passaggi seguenti viene descritto come esportare una pagina e si presuppone che esista un modello di esportazione per il sito. Un modello di esportazione definisce il modo in cui una pagina viene esportata ed è specifica per il sito. Per creare un modello di esportazione, fare riferimento alla sezione [Creazione di una configurazione per l’esportazione di pagine per il sito](#creating-a-page-exporter-configuration-for-your-site) .

Per esportare una pagina:

1. Andate alla pagina desiderata nella console **Siti** .

1. Selezionate la pagina, quindi aprite la finestra di dialogo **Proprietà** .

1. Select the **Advanced** tab.

1. Espandete il campo **Esporta** per selezionare un modello di esportazione.
Selezionate il modello richiesto per il sito, quindi confermate con **OK**.

1. Selezionate **Salva e chiudi** per chiudere la finestra di dialogo delle proprietà della pagina.

1. Richiedete l’esportazione della pagina, sostituendo il suffisso `html` con `export.zip` nell’URL.

   Ad esempio:
   * localhost:4502/content/we-retail/language-masters/en.html

   Accesso tramite:
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Scaricare il file di archivio nel file system.

1. Nel file system, decomprimete il file se necessario. Una volta espansa, una cartella avrà lo stesso nome della pagina selezionata. Questa cartella contiene:

   * la sottocartella `content`, ovvero il livello principale di una serie di sottocartelle che riflettono il percorso della pagina nella directory archivio

      * all&#39;interno di questa struttura è presente il file html per la pagina selezionata (`<page-name>.html`)
   * altre risorse (`.js` file, `.css` file, immagini ecc.) sono situati in base alle impostazioni nel modello di esportazione


1. Aprite il file html della pagina (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) nel browser per controllare il rendering.

## Creazione di una configurazione di esportazione di pagine per il sito {#creating-a-page-exporter-configuration-for-your-site}

L&#39;esportatore di pagine si basa sul framework [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)Content Sync. Le configurazioni disponibili nella finestra di dialogo Proprietà **di** pagina sono modelli di esportazione che definiscono le dipendenze richieste per una pagina.

Quando viene attivata l’esportazione di una pagina, viene fatto riferimento al modello di esportazione e sia il percorso della pagina che il percorso di progettazione vengono applicati in modo dinamico. Il file zip viene quindi creato utilizzando la funzionalità standard di sincronizzazione dei contenuti.

Un’installazione standard di AEM include un modello predefinito in `/etc/contentsync/templates/default`.

* Questo modello è il modello di fallback quando non viene trovato alcun modello di esportazione nella directory archivio.

* Il `default` modello mostra come è possibile configurare l’esportazione di una pagina, in modo da fungere da base per un nuovo modello di esportazione.

* Per visualizzare la struttura dei nodi del modello nel browser come formato JSON, richiedi il seguente URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

Il metodo più semplice per creare un nuovo modello di esportazione delle pagine è:

* copiare il `default` modello,

* assegnare un nuovo nome appropriato al sito,

* quindi eseguite gli aggiornamenti richiesti.

Per creare un modello completamente nuovo:

1. In **CRXDE Lite**, create un nodo sotto `/etc/contentsync/templates`:

   * `Name`: un nome appropriato per il sito; ad esempio, `<mysite>`. Il nome viene visualizzato nella finestra di dialogo delle proprietà della pagina quando si sceglie il modello di esportazione della pagina.

   * `Type`: `nt:unstructured`

2. Sotto il nodo del modello, chiamato qui `mysite`, create una struttura di nodi utilizzando i nodi di configurazione descritti di seguito.

## Attivazione di un modello di esportazione delle pagine {#activating-a-page-exporter-configuration-for-your-pages}

Una volta configurato il modello, è necessario renderlo disponibile:

1. In CRXDE andate alla pagina richiesta nel `/content` ramo.

1. Sul `jcr:content` nodo della pagina create la proprietà:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: percorso del modello; ad esempio: `/etc/contentsync/templates/mysite`

### Nodi di configurazione per l&#39;esportazione delle pagine {#page-exporter-configuration-nodes}

Il modello è costituito da una struttura di nodi, in quanto utilizza il framework [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)Content Sync.  Ogni nodo ha una `type` proprietà che definisce un&#39;azione specifica nel processo di creazione del file zip.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Per creare un modello di esportazione è possibile utilizzare i nodi seguenti:

* `page`
Il nodo pagina viene utilizzato per copiare il codice HTML della pagina nel file zip. Ha le seguenti caratteristiche:

   * È un nodo obbligatorio.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * È definito con la proprietà `Name`impostata su `page`.
   * Il tipo di nodo è `nt:unstructured`

   Il `page` nodo ha le seguenti proprietà:

   * Una `type` proprietà impostata con il valore `pages`.

   * Non dispone di una `path` proprietà poiché il percorso della pagina corrente viene copiato in modo dinamico nella configurazione.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
Il nodo di riscrittura definisce il modo in cui i collegamenti vengono riscritti nella pagina esportata. I collegamenti riscritti possono puntare ai file inclusi nel file zip o alle risorse sul server.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
Il nodo di progettazione viene utilizzato per copiare la progettazione utilizzata per la pagina esportata. Ha le seguenti caratteristiche:

   * È facoltativo.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * È definito con la proprietà `Name` impostata su `design`.
   * Il tipo di nodo è `nt:unstructured`.

   Il `design` nodo ha le seguenti proprietà:

   * Una `type` proprietà impostata sul valore `copy`.

   * Non dispone di una `path` proprietà, in quanto il percorso della pagina corrente viene copiato in modo dinamico nella configurazione.


* `generic`
Un nodo generico viene utilizzato per copiare risorse come clientlibs 
`.js` o `.css` i file nel file zip. Ha le seguenti caratteristiche:

   * È facoltativo.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * Non ha un nome specifico.
   * Il tipo di nodo è `nt:unstructured`.
   * Ha una `type` proprietà e proprietà `type` correlate. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   Ad esempio, il seguente nodo di configurazione copia i `mysite.clientlibs.js` file nel file zip:

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**Implementazione di una configurazione personalizzata**

Sono anche possibili configurazioni personalizzate.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Per soddisfare alcuni requisiti specifici, potrebbe essere necessario implementare un gestore [di aggiornamenti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)personalizzato.

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Esportazione di una pagina a livello di programmazione {#programmatically-exporting-a-page}

Per esportare una pagina a livello di programmazione, potete utilizzare il servizio [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI. Questo servizio consente di:

* Esportate una pagina e scrivete la risposta del servlet HTTP.
* Esportate una pagina e salvate il file zip in un percorso specifico.

Il servlet associato al `export` selettore e all&#39; `zip` estensione utilizza il servizio PageExporter.

## Risoluzione dei problemi {#troubleshooting}

Se si verifica un problema con il download del file zip, è possibile eliminare il `/var/contentsync` nodo nella directory archivio e inviare di nuovo la richiesta di esportazione.
