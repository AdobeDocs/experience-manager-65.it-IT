---
title: Esportatore pagina
description: Scopri come utilizzare Adobe Experience Manager (AEM) Page Exporter.
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# Esportatore pagina{#the-page-exporter}

Adobe Experience Manager (AEM) consente di esportare una pagina come pagina web completa, con immagini, `.js`, e `.css` file.

Una volta configurata, richiedi un’esportazione di pagina dal browser sostituendo `html` con `export.zip` nell’URL. Questo genera un file di archivio (zip), contenente la pagina sottoposta a rendering in formato html, insieme alle risorse di riferimento. Tutti i percorsi nella pagina (ad esempio, percorsi alle immagini) vengono riscritti in modo da puntare ai file inclusi nell’archivio o alle risorse sul server. Il file di archivio (zip) può quindi essere scaricato dal browser.

>[!NOTE]
>
>A seconda del browser e delle impostazioni, il download è:
>
>* un file di archivio (`<page-name>.export.zip`)
>* una cartella (`<page-name>`); di fatto il file di archivio è già stato espanso

## Esportazione di una pagina {#exporting-a-page}

I passaggi seguenti descrivono come esportare una pagina e presumono che esista un modello di esportazione per il sito. Un modello di esportazione definisce il modo in cui una pagina viene esportata ed è specifico per il sito. Per creare un modello di esportazione, vedi [Creazione di una configurazione di Page Exporter per il sito](#creating-a-page-exporter-configuration-for-your-site).

Per esportare una pagina:

1. Passa alla pagina richiesta in **Sites** console.

1. Seleziona la pagina, quindi apri la **Proprietà** .

1. Seleziona la **Avanzate** scheda.

1. Espandi **Esporta** per selezionare un modello di esportazione.
Seleziona il modello richiesto per il sito, quindi conferma con **OK**.

1. Seleziona **Salva e chiudi** per chiudere la finestra di dialogo proprietà pagina.

1. Richiedi la pagina per l’esportazione, sostituendo il suffisso `html` con `export.zip` nell’URL.

   Ad esempio:
   * localhost:4502/content/we-retail/language-masters/en.html

   Accesso effettuato tramite:
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. Scarica il file di archivio nel file system.

1. Se necessario, decomprimi il file nel file system. Quando viene espansa, esiste una cartella con lo stesso nome della pagina selezionata. Questa cartella contiene:

   * la sottocartella `content`, che è la radice di una serie di sottocartelle che riflettono il percorso della pagina nell’archivio

      * all&#39;interno di questa struttura è presente il file html per la pagina selezionata (`<page-name>.html`)

   * altre risorse (`.js` file, `.css` file, immagini e così via) si trovano in base alle impostazioni nel modello di esportazione

1. Apri il file HTML della pagina (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) nel browser in modo da poter controllare il rendering.

## Creazione di una configurazione di Page Exporter per il sito {#creating-a-page-exporter-configuration-for-your-site}

L’esportatore di pagine si basa sulla [Framework di sincronizzazione contenuti](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Le configurazioni disponibili nel **Proprietà pagina** Le finestre di dialogo sono modelli di esportazione che definiscono le dipendenze richieste per una pagina.

Quando viene attivata un’esportazione di pagine, viene fatto riferimento al modello di esportazione. Sia il percorso della pagina che il percorso della progettazione vengono applicati in modo dinamico. Il file zip viene quindi creato utilizzando la funzionalità standard di sincronizzazione dei contenuti.

Un’installazione standard di AEM include un modello predefinito in `/etc/contentsync/templates/default`.

* Questo modello è il modello di fallback quando non viene trovato alcun modello di esportazione nel repository.

* Il `default` Il modello mostra come configurare un’esportazione di pagine, in modo da fungere da base per un nuovo modello di esportazione.

* Per visualizzare la struttura dei nodi del modello nel browser in formato JSON, richiedi il seguente URL:
  `http://localhost:4502/etc/contentsync/templates/default.json`

Il metodo più semplice per creare un modello di esportazione pagine consiste nel:

* copia `default` modello,

* assegnare un nuovo nome appropriato al sito,

* quindi apporta gli aggiornamenti necessari.

Per creare un modello completamente nuovo:

1. In entrata **CRXDE Liti**, crea un nodo sotto `/etc/contentsync/templates`:

   * `Name`: nome appropriato per il sito; ad esempio, `<mysite>`. Il nome viene visualizzato nella finestra di dialogo delle proprietà della pagina quando si sceglie il modello di esportazione della pagina.

   * `Type`: `nt:unstructured`

2. Sotto il nodo del modello, chiamato qui `mysite`, crea una struttura di nodi utilizzando i nodi di configurazione descritti di seguito.

## Attivazione di un modello di esportazione pagina per le pagine {#activating-a-page-exporter-configuration-for-your-pages}

Quando il modello è configurato, lo rendi disponibile:

1. In CRXDE passa alla pagina richiesta in `/content` filiale. Può trattarsi di una singola pagina o della pagina principale di una sottostruttura.

1. Il giorno `jcr:content` della pagina, crea la proprietà:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: percorso del modello, ad esempio: `/etc/contentsync/templates/mysite`

### Nodi di configurazione di Page Exporter {#page-exporter-configuration-nodes}

Il modello è costituito da una struttura di nodi, in quanto utilizza [Framework di sincronizzazione contenuti](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Ogni nodo ha una `type` che definisce un’azione specifica nel processo di creazione del file zip.

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

Per creare un modello di esportazione è possibile utilizzare i seguenti nodi:

* `page`
Il nodo della pagina viene utilizzato per copiare il codice HTML della pagina nel file zip. Presenta le seguenti caratteristiche:

   * Un nodo obbligatorio.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * Definito con la proprietà `Name`imposta su `page`.
   * Il tipo di nodo è `nt:unstructured`

  Il `page` Il nodo ha le seguenti proprietà:

   * A `type` proprietà impostata con il valore `pages`.

   * Non ha un `path` come il percorso della pagina corrente viene copiato dinamicamente nella configurazione.
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
Il nodo di riscrittura definisce come vengono riscritti i collegamenti nella pagina esportata. I collegamenti riscritti possono puntare ai file inclusi nel file zip o alle risorse sul server.
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
Il nodo di progettazione viene utilizzato per copiare la progettazione utilizzata per la pagina esportata. Presenta le seguenti caratteristiche:

   * Facoltativo.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * Definito con la proprietà `Name` imposta su `design`.
   * Il tipo di nodo è `nt:unstructured`.

  Il `design` Il nodo ha le seguenti proprietà:

   * A `type` proprietà impostata sul valore `copy`.

   * Non ha un `path` , poiché il percorso della pagina corrente viene copiato dinamicamente nella configurazione.

* `generic`
Un nodo generico viene utilizzato per copiare risorse come clientlibs `.js` o `.css` file nel file zip. Presenta le seguenti caratteristiche:

   * Facoltativo.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * Nessun nome specifico.
   * Il tipo di nodo è `nt:unstructured`.
   * Ha un `type` proprietà e `type` proprietà correlate. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  Ad esempio, il seguente nodo di configurazione copia `mysite.clientlibs.js` file nel file zip:

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

Per soddisfare alcuni requisiti specifici, implementa una [gestore di aggiornamento personalizzato](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## Esportazione di una pagina a livello di programmazione {#programmatically-exporting-a-page}

Per esportare una pagina a livello di programmazione, puoi utilizzare [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) Servizio OSGI. Questo servizio consente di:

* Esporta una pagina e scrivi nella risposta del servlet HTTP.
* Esporta una pagina e salva il file zip in una posizione specifica.

Il servlet associato al `export` e il `zip` utilizza il servizio PageExporter.

## Risoluzione dei problemi {#troubleshooting}

Se si verifica un problema con il download del file zip, è possibile eliminare `/var/contentsync` nell’archivio e invia nuovamente la richiesta di esportazione.
