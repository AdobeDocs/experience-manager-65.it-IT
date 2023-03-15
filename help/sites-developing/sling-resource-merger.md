---
title: Utilizzo di Sling Resource Merger in AEM
seo-title: Using the Sling Resource Merger in AEM
description: Sling Resource Merger fornisce servizi per accedere e unire le risorse
seo-description: The Sling Resource Merger provides services to access and merge resources
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: c07fa148054b69b0da7bb402ef96a50d0895abfa
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 1%

---

# Utilizzo di Sling Resource Merger in AEM{#using-the-sling-resource-merger-in-aem}

## Scopo {#purpose}

Sling Resource Merger fornisce servizi per accedere e unire le risorse. Fornisce meccanismi di differenziazione per:

* **[Sovrapposizioni](/help/sites-developing/overlays.md)** delle risorse che utilizzano [percorsi di ricerca configurati](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **Sostituzioni** delle finestre di dialogo dei componenti per l’interfaccia touch (`cq:dialog`), utilizzando la gerarchia dei tipi di risorsa (tramite la proprietà `sling:resourceSuperType`).

Con Sling Resource Merger, le risorse e/o le proprietà di sovrapposizione/override vengono unite alle risorse/proprietà originali:

* Il contenuto della definizione personalizzata ha una priorità più alta di quella dell&#39;originale (cioè *sovrapposizioni* o *sostituzioni* it).

* Se necessario, [proprietà](#properties) definito nella personalizzazione, indica in che modo verrà utilizzato il contenuto unito dall’originale.

>[!CAUTION]
>
>Sling Resource Merger e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa anche che è adatto solo per l’interfaccia utente standard con funzioni touch; in particolare, le sostituzioni definite in questo modo sono applicabili solo alla finestra di dialogo touch di un componente.
>
>Le sovrapposizioni/sostituzioni per altre aree (inclusi altri aspetti di un componente touch o dell’interfaccia classica) comportano la copia del nodo e della struttura appropriati dall’originale al punto in cui verrà definita la personalizzazione.

### Obiettivi di AEM {#goals-for-aem}

Gli obiettivi per l’utilizzo di Sling Resource Merger in AEM sono i seguenti:

* assicurati che non vengano apportate modifiche alla personalizzazione in `/libs`.
* ridurre la struttura replicata da `/libs`.

   Quando si utilizza Sling Resource Merger, si sconsiglia di copiare l’intera struttura da `/libs` in quanto ciò porterebbe a tenere troppe informazioni nella personalizzazione (di solito `/apps`). La duplicazione delle informazioni aumenta inutilmente la possibilità di problemi quando il sistema viene aggiornato in qualsiasi modo.

>[!NOTE]
>
>Le sostituzioni non dipendono dai percorsi di ricerca, ma utilizzano la proprietà `sling:resourceSuperType` per effettuare la connessione.
>
>Tuttavia, le sostituzioni sono spesso definite in `/apps`, come best practice in AEM è definire le personalizzazioni in `/apps`; questo è perché non deve cambiare nulla sotto `/libs`.

>[!CAUTION]
>
>You ***deve*** non modificare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricrea l&#39;elemento richiesto (ovvero così come esiste in `/libs`) `/apps`
>
>1. Apporta modifiche a `/apps`

>


### Proprietà {#properties}

La fusione delle risorse fornisce le seguenti proprietà:

* `sling:hideProperties` ( `String` oppure `String[]`)

   Specifica la proprietà o l&#39;elenco di proprietà da nascondere.

   Il carattere jolly `*` nasconde tutto.

* `sling:hideResource` ( `Boolean`)

   Indica se le risorse devono essere completamente nascoste, inclusi gli elementi secondari.

* `sling:hideChildren` ( `String` oppure `String[]`)

   Contiene il nodo figlio o l&#39;elenco dei nodi figlio da nascondere. Le proprietà del nodo verranno mantenute.

   Il carattere jolly `*` nasconde tutto.

* `sling:orderBefore` ( `String`)

   Contiene il nome del nodo di pari livello sul quale deve essere posizionato il nodo corrente.

Queste proprietà influiscono sul modo in cui le risorse/proprietà corrispondenti/originali (da `/libs`) viene utilizzata dalla sovrapposizione/override (spesso in `/apps`).

### Creazione della struttura {#creating-the-structure}

Per creare una sovrapposizione o una sostituzione è necessario ricreare il nodo originale, con la struttura equivalente, sotto la destinazione (di solito `/apps`). Esempio:

* Sovrapposizione

   * La definizione della voce di navigazione per la console Sites , come illustrato nella barra a sinistra, è definita in:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Per sovrapporre, crea il seguente nodo:

      `/apps/cq/core/content/nav/sites`

      Quindi aggiorna la proprietà `jcr:title` se necessario.

* Sostituisci

   * La definizione della finestra di dialogo touch per la console Testo è definita in:

      `/libs/foundation/components/text/cq:dialog`

   * Per eseguire l&#39;override, crea il nodo seguente, ad esempio:

      `/apps/the-project/components/text/cq:dialog`

Per creare una di queste è sufficiente ricreare la struttura dello scheletro. Per semplificare la ricreazione della struttura tutti i nodi intermedi possono essere di tipo `nt:unstructured` (non devono riflettere il tipo di nodo originale; ad esempio, in `/libs`).

Nell’esempio di sovrapposizione riportato sopra, sono necessari i seguenti nodi:

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
>Quando si utilizza lo Sling Resource Merger (ovvero quando si gestisce l’interfaccia utente standard abilitata per il tocco), si sconsiglia di copiare l’intera struttura da `/libs` in quanto ciò comporterebbe la detenzione di troppe informazioni `/apps`. Questo può causare problemi quando il sistema viene aggiornato in qualsiasi modo.

### Casi d&#39;uso {#use-cases}

Oltre alle funzionalità standard, queste consentono di:

* **Aggiungi una proprietà**

   La proprietà non esiste nel `/libs` , ma è richiesto nel `/apps` sovrapposizione/override.

   1. Crea il nodo corrispondente all&#39;interno di `/apps`
   1. Crea la nuova proprietà su questo nodo &quot;

* **Ridefinire una proprietà (proprietà non create automaticamente)**

   La proprietà è definita in `/libs`, ma è necessario un nuovo valore nel `/apps` sovrapposizione/override.

   1. Crea il nodo corrispondente all&#39;interno di `/apps`
   1. Crea la proprietà corrispondente su questo nodo (sotto / `apps`)

      * La proprietà avrà una priorità in base alla configurazione di Sling Resource Resolver.
      * È supportata la modifica del tipo di proprietà.

         Se utilizzi un tipo di proprietà diverso da quello utilizzato in `/libs`, verrà quindi utilizzato il tipo di proprietà definito.
   >[!NOTE]
   >
   >È supportata la modifica del tipo di proprietà.

* **Ridefinire una proprietà creata automaticamente**

   Per impostazione predefinita, le proprietà create automaticamente (ad esempio `jcr:primaryType`) non sono soggette a sovrapposizione/override per garantire che il tipo di nodo sia attualmente in `/libs` è rispettato. Per imporre una sovrapposizione/override devi ricreare il nodo in `/apps`, nasconde esplicitamente la proprietà e ridefiniscila:

   1. Crea il nodo corrispondente sotto `/apps` con il `jcr:primaryType`
   1. Creare la proprietà `sling:hideProperties` su quel nodo, con il valore impostato su quello della proprietà creata automaticamente; ad esempio, `jcr:primaryType`

      Questa proprietà, definita in `/apps`, assumerà la priorità rispetto a quello definito in `/libs`

* **Ridefinire un nodo e i relativi figli**

   Il nodo e i relativi figli sono definiti in `/libs`, ma è necessaria una nuova configurazione nel `/apps` sovrapposizione/override.

   1. Combinare le azioni di:

      1. Nascondi elementi secondari di un nodo (mantenendo le proprietà del nodo)
      1. Ridefinire proprietà/proprietà

* **Nascondere una proprietà**

   La proprietà è definita in `/libs`, ma non è richiesto nel `/apps` sovrapposizione/override.

   1. Crea il nodo corrispondente all&#39;interno di `/apps`
   1. Creare una proprietà `sling:hideProperties` di tipo `String` o `String[]`. Utilizza questa opzione per specificare le proprietà da nascondere o ignorare. Possono essere utilizzati anche i caratteri jolly. Esempio:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Nascondere un nodo e i relativi elementi secondari**

   Il nodo e i relativi figli sono definiti in `/libs`, ma non è richiesto nel `/apps` sovrapposizione/override.

   1. Crea il nodo corrispondente sotto /apps
   1. Creare una proprietà `sling:hideResource`

      * tipo: `Boolean`
      * valore: `true`

* **Nascondi elementi secondari di un nodo (mantenendo le proprietà del nodo)**

   Il nodo, le sue proprietà e i suoi elementi secondari sono definiti in `/libs`. Il nodo e le relative proprietà sono obbligatori nel `/apps` sovrapposizione/override, ma alcuni o tutti i nodi figlio non sono necessari nel `/apps` sovrapposizione/override.

   1. Crea il nodo corrispondente sotto `/apps`
   1. Creare la proprietà `sling:hideChildren`:

      * tipo: `String[]`
      * valore: un elenco dei nodi secondari (come definito in `/libs`) per nascondere/ignorare

      Il carattere jolly &amp;ast; può essere utilizzato per nascondere/ignorare tutti i nodi figlio.


* **Riordinare i nodi**

   Il nodo e i relativi elementi di pari livello sono definiti in `/libs`. È necessaria una nuova posizione in modo che il nodo venga ricreato nel `/apps` sovrapposizione/override, dove la nuova posizione è definita in riferimento al nodo di pari livello appropriato in `/libs`.

   * Utilizza la `sling:orderBefore` proprietà:

      1. Crea il nodo corrispondente sotto `/apps`
      1. Creare la proprietà `sling:orderBefore`:

         Specifica il nodo (come in `/libs`) che il nodo corrente deve essere posizionato prima di:

         * tipo: `String`
         * valore: `<before-SiblingName>`

### Richiamare Sling Resource Merger dal codice {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger include due provider di risorse personalizzati, uno per le sovrapposizioni e l’altro per le sostituzioni. Ognuno di questi può essere richiamato all&#39;interno del codice utilizzando un punto di montaggio:

>[!NOTE]
>
>Quando accedi alla risorsa, si consiglia di utilizzare il punto di montaggio appropriato.
>
>In questo modo viene richiamato Sling Resource Merger e viene restituita la risorsa completamente unita (riducendo la struttura da cui deve essere replicata) `/libs`).

* Sovrapposizione:

   * finalità: unire le risorse in base al relativo percorso di ricerca
   * punto di montaggio: `/mnt/overlay`
   * usage: `mount point + relative path`
   * esempio:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Sostituisci:

   * finalità: unire le risorse in base al loro super-type
   * punto di montaggio: `/mnt/overide`
   * usage: `mount point + absolute path`
   * esempio:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Esempio di utilizzo {#example-of-usage}

Alcuni esempi:

* Sovrapposizione:

   * [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
   * [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)

* Sostituisci:

   * [Configurazione delle proprietà di pagina](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
