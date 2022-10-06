---
title: Esportatore di pagine
description: Scopri come utilizzare AEM Page Exporter.
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# Esportatore di pagine{#the-page-exporter}

AEM consente di esportare una pagina come pagina web completa, incluse le immagini, `.js` e `.css` file.

Una volta configurata, richiedi l’esportazione di una pagina dal browser sostituendo `html` con `export.zip` nell’URL. Viene generato un file di archivio (zip) contenente la pagina di cui è stato effettuato il rendering in formato html, insieme alle risorse di riferimento. Tutti i percorsi nella pagina (ad esempio, i percorsi delle immagini) vengono riscritti in modo che puntino ai file inclusi nell’archivio o alle risorse sul server. Il file di archivio (zip) può quindi essere scaricato dal browser.

>[!NOTE]
>
>A seconda del browser e delle impostazioni, il download sarà:
>* un file di archivio (`<page-name>.export.zip`)
>* una cartella (`<page-name>`); efficacemente il file di archivio già espanso


## Esportazione di una pagina {#exporting-a-page}

I passaggi seguenti descrivono come esportare una pagina e presuppongono che esista un modello di esportazione per il sito. Un modello di esportazione definisce il modo in cui una pagina viene esportata ed è specifica per il sito. Per creare un modello di esportazione, fai riferimento alla sezione [Creazione di una configurazione di esportazione pagina per il sito](#creating-a-page-exporter-configuration-for-your-site) sezione .

Per esportare una pagina:

1. Passa alla pagina richiesta nella **Sites** console.

1. Seleziona la pagina, quindi apri la **Proprietà** finestra di dialogo.

1. Seleziona la **Avanzate** scheda .

1. Espandi la **Esporta** per selezionare un modello di esportazione.
Seleziona il modello richiesto per il sito, quindi conferma con **OK**.

1. Seleziona **Salva e chiudi** per chiudere la finestra di dialogo delle proprietà della pagina.

1. Richiedi l&#39;esportazione della pagina, sostituendo il suffisso `html` con `export.zip` nell’URL.

   Esempio:
   * localhost:4502/content/we-retail/language-masters/en.html

   È accessibile tramite:
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Scarica il file di archivio sul tuo file system.

1. Se necessario, decomprimi il file nel file system. Una volta espansa, sarà presente una cartella con lo stesso nome della pagina selezionata. Questa cartella contiene:

   * la sottocartella `content`, che è la directory principale di una serie di sottocartelle che riflettono il percorso della pagina nell’archivio

      * all’interno di questa struttura è presente il file html per la pagina selezionata (`<page-name>.html`)
   * altre risorse (`.js` file, `.css` file, immagini, ecc.) sono situati in base alle impostazioni nel modello di esportazione


1. Apri il file HTML della pagina (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) nel browser per controllare il rendering.

## Creazione di una configurazione di esportazione pagina per il sito {#creating-a-page-exporter-configuration-for-your-site}

L’esportatore di pagina si basa sul [Framework di sincronizzazione dei contenuti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). Le configurazioni disponibili nel **Proprietà pagina** Le finestre di dialogo sono modelli di esportazione che definiscono le dipendenze richieste per una pagina.

Quando si attiva l’esportazione di una pagina, viene fatto riferimento al modello di esportazione e vengono applicati dinamicamente sia il percorso della pagina che il percorso di progettazione. Il file zip viene quindi creato utilizzando la funzionalità standard Content Sync.

Un’installazione predefinita AEM include un modello predefinito in `/etc/contentsync/templates/default`.

* Questo modello è il modello di fallback quando non viene trovato alcun modello di esportazione nel repository.

* La `default` Questo modello mostra come è possibile configurare un’esportazione di pagina, in modo da fungere da base per un nuovo modello di esportazione.

* Per visualizzare la struttura del nodo del modello nel browser come formato JSON, richiedi il seguente URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

Il metodo più semplice per creare un nuovo modello di esportazione della pagina è:

* copia il `default` modello,

* assegnare un nuovo nome appropriato al sito,

* quindi effettua gli aggiornamenti richiesti.

Per creare un modello completamente nuovo:

1. In **CRXDE Lite**, crea un nodo qui sotto `/etc/contentsync/templates`:

   * `Name`: un nome appropriato al sito; ad esempio, `<mysite>`. Il nome viene visualizzato nella finestra di dialogo delle proprietà della pagina quando si sceglie il modello di esportazione della pagina.

   * `Type`: `nt:unstructured`

2. Sotto il nodo del modello, chiamato qui `mysite`, crea una struttura di nodo utilizzando i nodi di configurazione descritti di seguito.

## Attivazione di un modello di esportazione delle pagine per le pagine {#activating-a-page-exporter-configuration-for-your-pages}

Una volta configurato il modello, devi renderlo disponibile:

1. In CRXDE passa alla pagina richiesta nel `/content` ramo. Può trattarsi di una singola pagina o della pagina principale di un sottoalbero.

1. Sulla `jcr:content` nodo della pagina crea la proprietà:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: percorso del modello; ad esempio: `/etc/contentsync/templates/mysite`

### Nodi di configurazione dell’esportatore di pagine {#page-exporter-configuration-nodes}

Il modello è costituito da una struttura di nodo, in quanto utilizza il [Framework di sincronizzazione dei contenuti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  Ogni nodo ha un `type` che definisce un&#39;azione specifica nel processo di creazione del file zip.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

I seguenti nodi possono essere utilizzati per creare un modello di esportazione:

* `page`
Il nodo della pagina viene utilizzato per copiare l’html della pagina nel file zip. Ha le seguenti caratteristiche:

   * È un nodo obbligatorio.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * È definito con la proprietà `Name`impostato su `page`.
   * Il tipo di nodo è `nt:unstructured`

   La `page` il nodo ha le seguenti proprietà:

   * A `type` impostata con il valore `pages`.

   * Non ha un `path` come percorso della pagina corrente viene copiata in modo dinamico nella configurazione.

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
   * È definito con la proprietà `Name` impostato su `design`.
   * Il tipo di nodo è `nt:unstructured`.

   La `design` il nodo ha le seguenti proprietà:

   * A `type` impostato sul valore `copy`.

   * Non ha un `path` , poiché il percorso della pagina corrente viene copiato in modo dinamico nella configurazione.


* `generic`
Un nodo generico viene utilizzato per copiare risorse come clientlibs 
`.js` o `.css` file nel file zip. Ha le seguenti caratteristiche:

   * È facoltativo.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * Non ha un nome specifico.
   * Il tipo di nodo è `nt:unstructured`.
   * Ha `type` proprietà e `type` proprietà correlate. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   Ad esempio, il seguente nodo di configurazione copia il `mysite.clientlibs.js` file nel file zip:

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**Implementazione di una configurazione personalizzata**

Sono possibili anche configurazioni personalizzate.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Per soddisfare alcuni requisiti specifici, potrebbe essere necessario implementare un [handler di aggiornamento personalizzato](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Esportazione di una pagina a livello di programmazione {#programmatically-exporting-a-page}

Per esportare una pagina a livello di programmazione, puoi utilizzare la funzione [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) Servizio OSGI. Questo servizio consente di:

* Esporta una pagina e scrivi nella risposta del servlet HTTP.
* Esporta una pagina e salva il file zip in una posizione specifica.

Il servlet associato al `export` selettore e `zip` l&#39;estensione utilizza il servizio PageExporter.

## Risoluzione dei problemi {#troubleshooting}

Se si verifica un problema con il download del file zip, è possibile eliminare il `/var/contentsync` nel repository e invia nuovamente la richiesta di esportazione.
