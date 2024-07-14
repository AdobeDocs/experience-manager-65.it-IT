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

Adobe Experience Manager (AEM) consente di esportare una pagina come pagina Web completa che include immagini, `.js` e `.css` file.

Una volta configurata, si richiede un&#39;esportazione di pagina dal browser sostituendo `html` con `export.zip` nell&#39;URL. Questo genera un file di archivio (zip), contenente la pagina sottoposta a rendering in formato html, insieme alle risorse di riferimento. Tutti i percorsi nella pagina (ad esempio, percorsi alle immagini) vengono riscritti in modo da puntare ai file inclusi nell’archivio o alle risorse sul server. Il file di archivio (zip) può quindi essere scaricato dal browser.

>[!NOTE]
>
>A seconda del browser e delle impostazioni, il download è:
>
>* un file di archivio (`<page-name>.export.zip`)
>* una cartella (`<page-name>`); il file di archivio è già stato espanso

## Esportazione di una pagina {#exporting-a-page}

I passaggi seguenti descrivono come esportare una pagina e presumono che esista un modello di esportazione per il sito. Un modello di esportazione definisce il modo in cui una pagina viene esportata ed è specifico per il sito. Per creare un modello di esportazione, vedere [Creazione di una configurazione di esportazione pagine per il sito](#creating-a-page-exporter-configuration-for-your-site).

Per esportare una pagina:

1. Passa alla pagina richiesta nella console **Sites**.

1. Seleziona la pagina, quindi apri la finestra di dialogo **Proprietà**.

1. Selezionare la scheda **Avanzate**.

1. Espandi il campo **Esporta** per selezionare un modello di esportazione.
Seleziona il modello richiesto per il sito, quindi conferma con **OK**.

1. Seleziona **Salva e chiudi** per chiudere la finestra di dialogo delle proprietà della pagina.

1. Richiedere l&#39;esportazione della pagina, sostituendo il suffisso `html` con `export.zip` nell&#39;URL.

   Ad esempio:
   * localhost:4502/content/we-retail/language-masters/en.html

   Accesso effettuato tramite:
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. Scarica il file di archivio nel file system.

1. Se necessario, decomprimi il file nel file system. Quando viene espansa, esiste una cartella con lo stesso nome della pagina selezionata. Questa cartella contiene:

   * la sottocartella `content`, che è la radice di una serie di sottocartelle che riflettono il percorso della pagina nell&#39;archivio

      * in questa struttura è presente il file html per la pagina selezionata (`<page-name>.html`)

   * altre risorse (`.js` file, `.css` file, immagini e così via) si trovano in base alle impostazioni nel modello di esportazione

1. Aprire il file HTML della pagina (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) nel browser in modo da poter controllare il rendering.

## Creazione di una configurazione di Page Exporter per il sito {#creating-a-page-exporter-configuration-for-your-site}

L&#39;utilità di esportazione delle pagine si basa sul [framework di sincronizzazione dei contenuti](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Le configurazioni disponibili nella finestra di dialogo **Proprietà pagina** sono modelli di esportazione che definiscono le dipendenze richieste per una pagina.

Quando viene attivata un’esportazione di pagine, viene fatto riferimento al modello di esportazione. Sia il percorso della pagina che il percorso della progettazione vengono applicati in modo dinamico. Il file zip viene quindi creato utilizzando la funzionalità standard di sincronizzazione dei contenuti.

Un&#39;installazione standard di AEM include un modello predefinito in `/etc/contentsync/templates/default`.

* Questo modello è il modello di fallback quando non viene trovato alcun modello di esportazione nel repository.

* Il modello `default` mostra come configurare un&#39;esportazione di pagine, in modo che possa fungere da base per un nuovo modello di esportazione.

* Per visualizzare la struttura dei nodi del modello nel browser in formato JSON, richiedi il seguente URL:
  `http://localhost:4502/etc/contentsync/templates/default.json`

Il metodo più semplice per creare un modello di esportazione pagine consiste nel:

* copia il modello `default`,

* assegnare un nuovo nome appropriato al sito,

* quindi apporta gli aggiornamenti necessari.

Per creare un modello completamente nuovo:

1. In **CRXDE Liti**, creare un nodo sotto `/etc/contentsync/templates`:

   * `Name`: nome appropriato per il sito, ad esempio `<mysite>`. Il nome viene visualizzato nella finestra di dialogo delle proprietà della pagina quando si sceglie il modello di esportazione della pagina.

   * `Type`: `nt:unstructured`

2. Sotto il nodo del modello, denominato qui `mysite`, creare una struttura di nodi utilizzando i nodi di configurazione descritti di seguito.

## Attivazione di un modello di esportazione pagina per le pagine {#activating-a-page-exporter-configuration-for-your-pages}

Quando il modello è configurato, lo rendi disponibile:

1. In CRXDE passa alla pagina richiesta nel ramo `/content`. Può trattarsi di una singola pagina o della pagina principale di una sottostruttura.

1. Nel nodo `jcr:content` della pagina, crea la proprietà:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: percorso del modello; ad esempio: `/etc/contentsync/templates/mysite`

### Nodi di configurazione di Page Exporter {#page-exporter-configuration-nodes}

Il modello è costituito da una struttura di nodi, in quanto utilizza il framework [Content Sync](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Ogni nodo ha una proprietà `type` che definisce un&#39;azione specifica nel processo di creazione del file zip.

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

Per creare un modello di esportazione è possibile utilizzare i seguenti nodi:

* `page`
Il nodo della pagina viene utilizzato per copiare il codice HTML della pagina nel file zip. Presenta le seguenti caratteristiche:

   * Un nodo obbligatorio.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * Definito con la proprietà `Name` impostata su `page`.
   * Il tipo di nodo è `nt:unstructured`

  Il nodo `page` ha le seguenti proprietà:

   * Una proprietà `type` impostata con il valore `pages`.

   * Non dispone di una proprietà `path` poiché il percorso della pagina corrente viene copiato dinamicamente nella configurazione.
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
   * Definito con la proprietà `Name` impostata su `design`.
   * Il tipo di nodo è `nt:unstructured`.

  Il nodo `design` ha le seguenti proprietà:

   * Una proprietà `type` impostata sul valore `copy`.

   * Non dispone di una proprietà `path`, poiché il percorso della pagina corrente viene copiato dinamicamente nella configurazione.

* `generic`
Un nodo generico viene utilizzato per copiare risorse come clientlibs `.js` o `.css` file nel file zip. Presenta le seguenti caratteristiche:

   * Facoltativo.
   * Si trova sotto `/etc/contentsync/templates/<mysite>`.
   * Nessun nome specifico.
   * Il tipo di nodo è `nt:unstructured`.
   * Ha una proprietà `type` e `type` proprietà correlate. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  Ad esempio, il seguente nodo di configurazione copia i file `mysite.clientlibs.js` nel file zip:

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

Per soddisfare alcuni requisiti specifici, implementa un [gestore di aggiornamento personalizzato](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## Esportazione di una pagina a livello di programmazione {#programmatically-exporting-a-page}

Per esportare una pagina a livello di programmazione, puoi utilizzare il servizio OSGI [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html). Questo servizio consente di:

* Esporta una pagina e scrivi nella risposta del servlet HTTP.
* Esporta una pagina e salva il file zip in una posizione specifica.

Il servlet associato al selettore `export` e all&#39;estensione `zip` utilizza il servizio PageExporter.

## Risoluzione dei problemi {#troubleshooting}

Se si verifica un problema con il download del file zip, è possibile eliminare il nodo `/var/contentsync` nell&#39;archivio e inviare nuovamente la richiesta di esportazione.
