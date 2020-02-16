---
title: Page Exporter
seo-title: Page Exporter
description: Scoprite come utilizzare AEM Page Exporter.
seo-description: Scoprite come utilizzare AEM Page Exporter.
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Page Exporter{#the-page-exporter}

AEM consente di esportare una pagina come pagina Web completa con immagini, file .js e .css.

Una volta configurata l’esportazione, è sufficiente richiedere una pagina nel browser sostituendola `html` con `export.zip` nell’URL e ottenere un file ZIP contenente la pagina rappresentata in formato html e le risorse a cui si fa riferimento. Tutti i percorsi della pagina, ad esempio i percorsi delle immagini, vengono riscritti in modo da puntare ai file inclusi nel file zip o alle risorse sul server.

## Esportazione di una pagina {#exporting-a-page}

Nei passaggi seguenti viene descritto come esportare una pagina e si presuppone che esista un modello di configurazione per l’esportazione per il sito. Un modello di configurazione definisce il modo in cui una pagina viene esportata ed è specifica per il sito. Per creare un modello di configurazione, fare riferimento alla sezione [Creazione di una configurazione di esportazione di pagina per il sito](#creating-a-page-exporter-configuration-for-your-site) .

Per esportare una pagina:

1. Nel browser, aprite la pagina. Esempio:
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. Aprite la finestra di dialogo delle proprietà della pagina, selezionate la scheda **Avanzate** ed espandete il set di campi **Esporta** .

1. Fate clic sull&#39;icona Lente di ingrandimento e selezionate un modello di configurazione. Selezionate il modello **geometrixx** , in quanto è quello predefinito per il sito Geometrixx. Fai clic su **OK**. 

1. Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà della pagina.
1. Richiedete la pagina sostituendo `html` con `export.zip` l’URL.

1. Scaricate il `<page-name>.export.zip` file nel file system.

1. Nel file system, decomprimete il file:

   * il file html della pagina ( `<page-name>.html`) è disponibile di seguito `<unzip-dir>/<page-path>`
   * altre risorse (file .js, file .css, immagini, ...) si trovano in base alle impostazioni nel modello di esportazione. In questo esempio, alcune risorse sono riportate di seguito `<unzip-dir>/etc`, altre `<unzip-dir>/<page-path>`.

1. Aprite il file html della pagina ( `<unzip-dir>/<page-path>.html`) nel browser per controllare il rendering.

## Creazione di una configurazione di esportazione di pagine per il sito {#creating-a-page-exporter-configuration-for-your-site}

L&#39;esportatore di pagine si basa sul framework Content Sync (Sincronizzazione contenuti). Le configurazioni disponibili nella finestra di dialogo delle proprietà della pagina sono modelli di configurazione. Definiscono tutte le dipendenze richieste per una pagina. Quando viene attivata l’esportazione di una pagina, viene utilizzato il modello di configurazione e sia il percorso della pagina che il percorso di progettazione vengono applicati dinamicamente alla configurazione. Il file zip viene quindi creato utilizzando la funzionalità standard di sincronizzazione dei contenuti.

AEM incorpora alcuni modelli, tra cui:

* Uno predefinito a `/etc/contentsync/templates/default`. Modello:

   * È il modello di fallback quando non viene trovato alcun modello di configurazione nella directory archivio.
   * Può fungere da base per un nuovo modello di configurazione.

* Uno dedicato al sito **Geometrixx** , all’indirizzo `/etc/contentsync/templates/geometrixx`. Questo modello può essere utilizzato come esempio per crearne uno nuovo.

Per creare un modello di configurazione di esportazione pagina:

1. In **CRXDE Lite**, create un nodo sotto `/etc/contentsync/templates`:

   * Nome:ad esempio `mysite`. Il nome viene visualizzato nella finestra di dialogo delle proprietà della pagina quando si sceglie il modello di esportazione della pagina.
   * Tipo: `nt:unstructured`

1. Sotto il nodo del modello, chiamato qui `mysite`, create una struttura di nodi utilizzando i nodi di configurazione descritti di seguito.

### Nodi di configurazione per l&#39;esportazione delle pagine {#page-exporter-configuration-nodes}

Il modello di configurazione è costituito da una struttura di nodi. Ogni nodo ha una `type` proprietà che definisce un&#39;azione specifica nel processo di creazione del file zip. Per ulteriori dettagli sulla proprietà type, consultate la sezione Panoramica dei tipi di configurazione nella pagina Framework Content Sync.

Per creare un modello di configurazione di esportazione è possibile utilizzare i nodi seguenti:

**nodo** pagina Il nodo pagina viene utilizzato per copiare il codice HTML della pagina nel file zip. Ha le seguenti caratteristiche:

* È un nodo obbligatorio.
* Si trova sotto `/etc/contentsync/templates/<sitename>`.
* Il suo nome è `page`.
* Il tipo di nodo è `nt:unstructured`

Il `page` nodo ha le seguenti proprietà:

* Una `type` proprietà impostata con il valore `pages`.

* Non dispone di una `path` proprietà poiché il percorso della pagina corrente viene copiato in modo dinamico nella configurazione.

* Le altre proprietà sono descritte nella sezione Panoramica dei tipi di configurazione del framework Content Sync.

**nodo** di riscrittura Il nodo di riscrittura definisce il modo in cui i collegamenti vengono riscritti nella pagina esportata. I collegamenti riscritti possono puntare ai file inclusi nel file zip o alle risorse sul server.

Fate riferimento alla pagina Content Sync (Sincronizzazione contenuto) per una descrizione completa del `rewrite` nodo.

**nodo** di progettazione Il nodo di progettazione viene utilizzato per copiare la progettazione utilizzata per la pagina esportata. Ha le seguenti caratteristiche:

* È facoltativo.
* Si trova sotto `/etc/contentsync/templates/<sitename>`.
* Il suo nome è `design`.
* Il tipo di nodo è `nt:unstructured`.

Il `design` nodo ha le seguenti proprietà:

* Una `type` proprietà impostata sul valore `copy`.

* Non dispone di una `path` proprietà poiché il percorso della pagina corrente viene copiato in modo dinamico nella configurazione.

**nodo** generico Un nodo generico viene utilizzato per copiare le risorse come file clientlibs .js o .css nel file zip. Ha le seguenti caratteristiche:

* È facoltativo.
* Si trova sotto `/etc/contentsync/templates/<sitename>`.
* Non ha un nome specifico.
* Il tipo di nodo è `nt:unstructured`.
* Dispone di una `type` proprietà ed eventuali proprietà `type` correlate, come definito nella sezione Panoramica dei tipi di configurazione del framework Content Sync.

Ad esempio, il seguente nodo di configurazione copia i file clientlibs .js geometrixx nel file zip:

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

Il modello di configurazione per l’esportazione delle pagine **Geometrixx** mostra come è possibile configurare un’esportazione di pagine. Per visualizzare la struttura dei nodi del modello nel browser come formato json, richiedi il seguente URL:

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**Implementazione di una configurazione personalizzata**

Come avrete notato nella struttura del nodo, il modello di configurazione per l’esportazione delle pagine **Geometrixx** include un `logo` nodo con una `type` proprietà impostata su `image`. Si tratta di un tipo di configurazione speciale creato per copiare il logo immagine nel file zip. Per soddisfare alcuni requisiti specifici, potrebbe essere necessario implementare una `type` proprietà personalizzata: a tal fine, fate riferimento alla sezione Implementazione di un gestore di aggiornamenti personalizzato nella pagina Content Sync (Sincronizzazione contenuti).

## Esportazione di una pagina a livello di programmazione {#programmatically-exporting-a-page}

Per esportare una pagina a livello di programmazione, potete utilizzare il servizio [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI. Questo servizio consente di:

* Esportate una pagina e scrivete la risposta del servlet HTTP.
* Esportate una pagina e salvate il file zip in un percorso specifico.

Il servlet associato al `export` selettore e all&#39; `zip` estensione utilizza il servizio PageExporter.

## Risoluzione dei problemi {#troubleshooting}

Se si verifica un problema con il download del file zip, è possibile eliminare il `/var/contentsync` nodo nella directory archivio e inviare di nuovo la richiesta di esportazione.

