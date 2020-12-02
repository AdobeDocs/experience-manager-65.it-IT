---
title: Utilizzo di Sling Resource Merger in AEM
seo-title: Utilizzo di Sling Resource Merger in AEM
description: Sling Resource Merger fornisce servizi per accedere e unire le risorse
seo-description: Sling Resource Merger fornisce servizi per accedere e unire le risorse
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 1%

---


# Utilizzo di Sling Resource Merger in AEM{#using-the-sling-resource-merger-in-aem}

## Scopo {#purpose}

Sling Resource Merger fornisce servizi per accedere e unire le risorse. Fornisce meccanismi di diff (differenziazione) per entrambi:

* **[Sovrapposizioni](/help/sites-developing/overlays.md)** di risorse tramite i percorsi [ di ricerca ](/help/sites-developing/overlays.md#configuring-the-search-paths)configurati.

* **Sovrapposizioni** di finestre di dialogo dei componenti per l’interfaccia touch (`cq:dialog`), utilizzando la gerarchia dei tipi di risorse (tramite la proprietà  `sling:resourceSuperType`).

Con Sling Resource Merger, le risorse e/o le proprietà di sovrapposizione/esclusione vengono unite con le risorse/proprietà originali:

* Il contenuto della definizione personalizzata ha una priorità maggiore rispetto a quella dell&#39;originale (ovvero *sovrapposizioni* o *sostituiscono*).

* Se necessario, le [proprietà](#properties) definite nella personalizzazione indicano in che modo verrà utilizzato il contenuto unito dall&#39;originale.

>[!CAUTION]
>
>La Fusione risorse Sling e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa anche che è adatto solo per l’interfaccia standard touch; in particolare, le sostituzioni definite in questo modo sono applicabili solo alla finestra di dialogo attivata dal tocco di un componente.
>
>Le sovrapposizioni/sostituzioni per altre aree (compresi altri aspetti di un componente touch o dell’interfaccia classica) richiedono la copia del nodo e della struttura appropriati dall’originale alla posizione in cui verrà definita la personalizzazione.

### Obiettivi per AEM {#goals-for-aem}

Gli obiettivi per l&#39;utilizzo di Sling Resource Merger in AEM sono:

* assicurarsi che le modifiche alla personalizzazione non vengano effettuate in `/libs`.
* ridurre la struttura replicata da `/libs`.

   Quando si utilizza Sling Resource Merger, non è consigliabile copiare l&#39;intera struttura da `/libs`, in quanto ciò comporterebbe la conservazione di troppe informazioni nella personalizzazione (in genere `/apps`). Duplicare le informazioni aumenta inutilmente la possibilità di problemi quando il sistema viene aggiornato in qualsiasi modo.

>[!NOTE]
>
>Le sostituzioni non dipendono dai percorsi di ricerca, ma utilizzano la proprietà `sling:resourceSuperType` per stabilire la connessione.
>
>Tuttavia, le sostituzioni sono spesso definite in `/apps`, in quanto la best practice in AEM consiste nel definire le personalizzazioni in `/apps`; questo perché non è necessario modificare nulla in `/libs`.

>[!CAUTION]
>
>***non è necessario*** modificare nulla nel percorso `/libs`.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
   >
   >
1. Apportare modifiche all&#39;interno di `/apps`

>



### Proprietà {#properties}

La fusione delle risorse fornisce le seguenti proprietà:

* `sling:hideProperties` (  `String` o  `String[]`)

   Specifica la proprietà, o l&#39;elenco di proprietà, da nascondere.

   Il carattere jolly `*` nasconde tutti.

* `sling:hideResource` ( `Boolean`)

   Indica se le risorse devono essere completamente nascoste, inclusi i relativi elementi figlio.

* `sling:hideChildren` (  `String` o  `String[]`)

   Contiene il nodo secondario, o elenco di nodi secondari, da nascondere. Le proprietà del nodo verranno mantenute.

   Il carattere jolly `*` nasconde tutti.

* `sling:orderBefore` ( `String`)

   Contiene il nome del nodo di pari livello al quale il nodo corrente deve essere posizionato davanti.

Queste proprietà influiscono sul modo in cui le risorse/proprietà corrispondenti/originali (da `/libs`) vengono utilizzate dalla sovrapposizione/sostituzione (spesso in `/apps`).

### Creazione della struttura {#creating-the-structure}

Per creare una sovrapposizione o una sostituzione, è necessario ricreare il nodo originale, con la struttura equivalente, sotto la destinazione (in genere `/apps`). Esempio:

* Sovrapposizione

   * La definizione della voce di navigazione per la console Siti, come illustrato nella barra laterale, è definita in:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Per sovrapporre questo, create il seguente nodo:

      `/apps/cq/core/content/nav/sites`

      Quindi aggiornate la proprietà `jcr:title` come necessario.

* Override

   * La definizione della finestra di dialogo touch per la console Testo è definita in:

      `/libs/foundation/components/text/cq:dialog`

   * Per ignorare questo problema, create il seguente nodo, ad esempio:

      `/apps/the-project/components/text/cq:dialog`

Per creare una di queste è sufficiente ricreare la struttura dell&#39;ossatura. Per semplificare la ricreazione della struttura, tutti i nodi intermedi possono essere di tipo `nt:unstructured` (non devono riflettere il tipo di nodo originale; ad esempio, in `/libs`).

Nell&#39;esempio di sovrapposizione riportato sopra, sono necessari i seguenti nodi:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Quando si utilizza la funzione Sling Resource Merger (ovvero quando si utilizza l&#39;interfaccia touch standard), si consiglia di non copiare l&#39;intera struttura da `/libs`, in quanto ciò comporterebbe la memorizzazione di troppe informazioni in `/apps`. Ciò può causare problemi quando il sistema viene aggiornato in qualsiasi modo.

### Casi di utilizzo {#use-cases}

Questi, insieme alle funzionalità standard, consentono di:

* **Aggiunta di una proprietà**

   La proprietà non esiste nella definizione `/libs`, ma è necessaria nella sovrapposizione/esclusione `/apps`.

   1. Crea il nodo corrispondente all&#39;interno di `/apps`
   1. Crea la nuova proprietà su questo nodo &quot;

* **Ridefinire una proprietà (proprietà non create automaticamente)**

   La proprietà è definita in `/libs`, ma è necessario un nuovo valore nella sovrapposizione/sostituzione di `/apps`.

   1. Crea il nodo corrispondente all&#39;interno di `/apps`
   1. Creare la proprietà corrispondente su questo nodo (in / `apps`)

      * La proprietà avrà una priorità in base alla configurazione di Sling Resource Resolver.
      * È supportata la modifica del tipo di proprietà.

         Se si utilizza un tipo di proprietà diverso da quello utilizzato in `/libs`, verrà utilizzato il tipo di proprietà definito.
   >[!NOTE]
   >
   >È supportata la modifica del tipo di proprietà.

* **Ridefinire una proprietà creata automaticamente**

   Per impostazione predefinita, le proprietà create automaticamente (come `jcr:primaryType`) non sono soggette a sovrapposizione/override per garantire che il tipo di nodo attualmente sotto `/libs` sia rispettato. Per imporre una sovrapposizione/sostituzione è necessario ricreare il nodo in `/apps`, nascondere esplicitamente la proprietà e ridefinirla:

   1. Crea il nodo corrispondente sotto `/apps` con la `jcr:primaryType` desiderata
   1. Creare la proprietà `sling:hideProperties` su tale nodo, con il valore impostato su quello della proprietà creata automaticamente; ad esempio, `jcr:primaryType`

      Questa proprietà, definita in `/apps`, ha ora priorità rispetto a quella definita in `/libs`

* **Ridefinire un nodo e i relativi elementi secondari**

   Il nodo e i relativi elementi secondari sono definiti in `/libs`, ma è necessaria una nuova configurazione nella sovrapposizione/esclusione `/apps`.

   1. Combinare le azioni di:

      1. Nascondere gli elementi secondari di un nodo (mantenendo le proprietà del nodo)
      1. Ridefinire proprietà/proprietà

* **Nascondere una proprietà**

   La proprietà è definita in `/libs`, ma non è necessaria nella sovrapposizione/sostituzione di `/apps`.

   1. Crea il nodo corrispondente all&#39;interno di `/apps`
   1. Creare una proprietà `sling:hideProperties` di tipo `String` o `String[]`. Utilizzate questa opzione per specificare le proprietà da nascondere o ignorare. È inoltre possibile utilizzare i caratteri jolly. Esempio:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Nascondere un nodo e i relativi elementi secondari**

   Il nodo e i relativi elementi secondari sono definiti in `/libs`, ma non sono richiesti nella sovrapposizione/esclusione `/apps`.

   1. Crea il nodo corrispondente in /apps
   1. Creare una proprietà `sling:hideResource`

      * tipo: `Boolean`
      * valore: `true`

* **Nascondere gli elementi secondari di un nodo (mantenendo le proprietà del nodo)**

   Il nodo, le relative proprietà e i relativi elementi secondari sono definiti in `/libs`. Il nodo e le relative proprietà sono obbligatori nella `/apps` sovrapposizione/esclusione, ma alcuni o tutti i nodi secondari non sono richiesti nella `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente sotto `/apps`
   1. Creare la proprietà `sling:hideChildren`:

      * tipo: `String[]`
      * value: un elenco dei nodi secondari (come definito in `/libs`) da nascondere/ignorare

      Il carattere jolly &amp;ast; può essere utilizzato per nascondere/ignorare tutti i nodi figlio.


* **Riordinare i nodi**

   Il nodo e i relativi elementi di pari livello sono definiti in `/libs`. È necessaria una nuova posizione per ricreare il nodo nella sovrapposizione/esclusione `/apps`, dove la nuova posizione viene definita in riferimento al nodo di pari livello appropriato in `/libs`.

   * Utilizzare la proprietà `sling:orderBefore`:

      1. Crea il nodo corrispondente sotto `/apps`
      1. Creare la proprietà `sling:orderBefore`:

         Questo specifica il nodo (come in `/libs`) in cui il nodo corrente deve essere posizionato prima:

         * tipo: `String`
         * valore: `<before-SiblingName>`

### Richiamo di Sling Resource Merger dal codice {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger include due provider di risorse personalizzate, uno per le sovrapposizioni e l&#39;altro per le sostituzioni. Ognuno di questi può essere richiamato all&#39;interno del codice utilizzando un punto di montaggio:

>[!NOTE]
>
>Quando accedete alla risorsa, si consiglia di utilizzare il punto di montaggio appropriato.
>
>In questo modo viene richiamato Sling Resource Merger e viene restituita la risorsa completamente unita (riducendo la struttura da replicare da `/libs`).

* Sovrapposizione:

   * finalità: unire risorse in base al percorso di ricerca
   * punto di montaggio: `/mnt/overlay`
   * usage: `mount point + relative path`
   * esempio:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Ignora:

   * finalità: unire le risorse in base al relativo super-type
   * punto di montaggio: `/mnt/overide`
   * usage: `mount point + absolute path`
   * esempio:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Esempio di utilizzo {#example-of-usage}

Alcuni esempi:

* Sovrapposizione:

   * [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
   * [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)

* Ignora:

   * [Configurazione delle proprietà pagina](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

