---
title: Utilizzo di Sling Resource Merger in AEM
description: Sling Resource Merger fornisce servizi per accedere e unire le risorse
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Utilizzo di Sling Resource Merger in AEM{#using-the-sling-resource-merger-in-aem}

## Scopo {#purpose}

Sling Resource Merger fornisce servizi per accedere e unire le risorse. Fornisce meccanismi di differenze per entrambi:

* **[Sovrapposizioni](/help/sites-developing/overlays.md)** di risorse utilizzando [percorsi di ricerca configurati](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **Esegue l&#39;override** delle finestre di dialogo dei componenti per l&#39;interfaccia utente touch (`cq:dialog`), utilizzando la gerarchia dei tipi di risorsa (tramite la proprietà `sling:resourceSuperType`).

Con Sling Resource Merger, le risorse e/o le proprietà di sovrapposizione/sostituzione vengono unite alle risorse/proprietà originali:

* Il contenuto della definizione personalizzata ha una priorità più alta di quella dell&#39;originale (ovvero *sovrapposizioni* o *sostituzioni*).

* Se necessario, [proprietà](#properties) definite nella personalizzazione, indicano come deve essere utilizzato il contenuto unito dall&#39;originale.

>[!CAUTION]
>
>Sling Resource Merger e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa anche che è appropriato solo per l’interfaccia utente touch standard; in particolare, le sostituzioni definite in questo modo sono applicabili solo alla finestra di dialogo touch di un componente.
>
>Le sovrapposizioni/sostituzioni per altre aree (compresi altri aspetti di un componente touch o dell’interfaccia classica) implicano la copia del nodo e della struttura appropriati dall’originale al punto in cui verrà definita la personalizzazione.

### Obiettivi per l&#39;AEM {#goals-for-aem}

Gli obiettivi per utilizzare Sling Resource Merger in AEM sono i seguenti:

* assicurarsi che le modifiche di personalizzazione non vengano apportate in `/libs`.
* ridurre la struttura replicata da `/libs`.

  Quando si utilizza Sling Resource Merger, non è consigliabile copiare l&#39;intera struttura da `/libs` in quanto ciò comporterebbe la memorizzazione di troppe informazioni nella personalizzazione (in genere `/apps`). La duplicazione delle informazioni aumenta inutilmente la possibilità di problemi quando il sistema viene aggiornato in qualsiasi modo.

>[!NOTE]
>
>Le sostituzioni non dipendono dai percorsi di ricerca e utilizzano la proprietà `sling:resourceSuperType` per stabilire la connessione.
>
>Tuttavia, le sostituzioni sono spesso definite in `/apps`, poiché la best practice in AEM è quella di definire personalizzazioni in `/apps`, in quanto non è necessario modificare nulla in `/libs`.

>[!CAUTION]
>
>***must*** non modificare nulla nel percorso `/libs`.
>
>Il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricrea l&#39;elemento richiesto (ovvero, poiché esiste in `/libs`) in `/apps`
>
>1. Apporta le modifiche in `/apps`
>

### Proprietà {#properties}

La fusione delle risorse fornisce le seguenti proprietà:

* `sling:hideProperties` ( `String` o `String[]`)

  Specifica la proprietà o l&#39;elenco di proprietà da nascondere.

  Il carattere jolly `*` nasconde tutto.

* `sling:hideResource` ( `Boolean`)

  Indica se le risorse devono essere completamente nascoste, inclusi i relativi elementi secondari.

* `sling:hideChildren` ( `String` o `String[]`)

  Contiene il nodo figlio, o elenco di nodi figlio, da nascondere. Le proprietà del nodo verranno mantenute.

  Il carattere jolly `*` nasconde tutto.

* `sling:orderBefore` ( `String`)

  Contiene il nome del nodo di pari livello che deve essere posizionato davanti al nodo corrente.

Queste proprietà influiscono sul modo in cui le risorse/proprietà corrispondenti/originali (da `/libs`) vengono utilizzate dalla sovrapposizione/esclusione (spesso in `/apps`).

### Creazione della struttura {#creating-the-structure}

Per creare una sovrapposizione o una sostituzione è necessario ricreare il nodo originale, con la struttura equivalente, nella destinazione (in genere `/apps`). Ad esempio:

* Sovrapposizione

   * La definizione della voce di navigazione per la console Sites, come mostrato nella barra, è definita in:

     `/libs/cq/core/content/nav/sites/jcr:title`

   * Per sovrapporsi, crea il seguente nodo:

     `/apps/cq/core/content/nav/sites`

     Quindi aggiornare la proprietà `jcr:title` come richiesto.

* Sostituisci

   * La definizione della finestra di dialogo touch per la console Testi è definita in:

     `/libs/foundation/components/text/cq:dialog`

   * Per evitare questo problema, crea il seguente nodo, ad esempio:

     `/apps/the-project/components/text/cq:dialog`

Per creare uno di questi elementi è sufficiente ricreare la struttura dell&#39;ossatura. Per semplificare la ricreazione della struttura, tutti i nodi intermedi possono essere di tipo `nt:unstructured` (non devono necessariamente riflettere il tipo di nodo originale; ad esempio, in `/libs`).

Nell’esempio di sovrapposizione precedente, sono necessari i seguenti nodi:

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
>Quando si utilizza Sling Resource Merger (ovvero quando si tratta dell&#39;interfaccia utente standard touch) non è consigliabile copiare l&#39;intera struttura da `/libs` in quanto si otterrebbe una quantità eccessiva di informazioni in `/apps`. Questo può causare problemi quando il sistema viene aggiornato in qualsiasi modo.

### Casi d’uso {#use-cases}

Queste funzionalità, insieme a quelle standard, consentono di:

* **Aggiungi una proprietà**

  La proprietà non esiste nella definizione `/libs`, ma è obbligatoria nella sovrapposizione/sostituzione `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Crea la nuova proprietà su questo nodo &quot;

* **Ridefinire una proprietà (proprietà non create automaticamente)**

  La proprietà è definita in `/libs`, ma è necessario un nuovo valore nella sovrapposizione/sostituzione `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Crea la proprietà corrispondente su questo nodo (in / `apps`)

      * La proprietà avrà una priorità in base alla configurazione di Sling Resource Resolver.
      * È supportata la modifica del tipo di proprietà.

        Se si utilizza un tipo di proprietà diverso da quello utilizzato in `/libs`, verrà utilizzato il tipo di proprietà definito.

  >[!NOTE]
  >
  >È supportata la modifica del tipo di proprietà.

* **Ridefinire una proprietà creata automaticamente**

  Per impostazione predefinita, le proprietà create automaticamente (come `jcr:primaryType`) non sono soggette a sovrapposizione/sostituzione per garantire che il tipo di nodo attualmente in `/libs` sia rispettato. Per imporre una sovrapposizione/sostituzione è necessario ricreare il nodo in `/apps`, nascondere esplicitamente la proprietà e ridefinirla:

   1. Crea il nodo corrispondente in `/apps` con `jcr:primaryType` desiderato
   1. Creare la proprietà `sling:hideProperties` su tale nodo, con il valore impostato su quello della proprietà creata automaticamente, ad esempio `jcr:primaryType`

      Questa proprietà, definita in `/apps`, avrà ora la priorità rispetto a quella definita in `/libs`

* **Ridefinire un nodo e i relativi elementi secondari**

  Il nodo e i relativi nodi secondari sono definiti in `/libs`, ma è necessaria una nuova configurazione nella sovrapposizione/esclusione di `/apps`.

   1. Combina le azioni di:

      1. Nascondi elementi figlio di un nodo (mantenendo le proprietà del nodo)
      1. Ridefinisci la/le proprietà

* **Nascondi una proprietà**

  La proprietà è definita in `/libs`, ma non è richiesta nella sostituzione/sovrapposizione di `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Creare una proprietà `sling:hideProperties` di tipo `String` o `String[]`. Utilizzare questa opzione per specificare le proprietà da nascondere/ignorare. È inoltre possibile utilizzare i caratteri jolly. Ad esempio:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Nascondi un nodo e i relativi elementi secondari**

  Il nodo e i relativi nodi secondari sono definiti in `/libs`, ma non sono obbligatori nella sovrapposizione/esclusione di `/apps`.

   1. Crea il nodo corrispondente in /apps
   1. Crea una proprietà `sling:hideResource`

      * tipo: `Boolean`
      * valore: `true`

* **Nascondi elementi figlio di un nodo (mantenendo le proprietà del nodo)**

  Il nodo, le relative proprietà e i relativi elementi figlio sono definiti in `/libs`. Il nodo e le relative proprietà sono obbligatori nella sovrapposizione/sostituzione `/apps`, ma alcuni o tutti i nodi figlio non sono obbligatori nella sovrapposizione/sostituzione `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Creare la proprietà `sling:hideChildren`:

      * tipo: `String[]`
      * valore: elenco dei nodi figlio (come definiti in `/libs`) da nascondere/ignorare

      Il carattere jolly &amp;ast; può essere utilizzato per nascondere/ignorare tutti i nodi figlio.

* **Riordina nodi**

  Nodo e relativi elementi di pari livello definiti in `/libs`. È necessaria una nuova posizione in modo che il nodo venga ricreato nella sovrapposizione/sostituzione `/apps`, dove la nuova posizione viene definita in riferimento al nodo di pari livello appropriato in `/libs`.

   * Utilizzare la proprietà `sling:orderBefore`:

      1. Crea il nodo corrispondente in `/apps`
      1. Creare la proprietà `sling:orderBefore`:

         Specifica il nodo (come in `/libs`) in cui posizionare il nodo corrente prima di:

         * tipo: `String`
         * valore: `<before-SiblingName>`

### Richiamare Sling Resource Merger dal codice {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger include due provider di risorse personalizzati: uno per le sovrapposizioni e l’altro per le sostituzioni. Ognuna di queste può essere richiamata all’interno del codice utilizzando un punto di montaggio:

>[!NOTE]
>
>Quando si accede alla risorsa, si consiglia di utilizzare il punto di montaggio appropriato.
>
>In questo modo viene richiamato Sling Resource Merger e viene restituita la risorsa completamente unita, riducendo la struttura che deve essere replicata da `/libs`.

* Sovrapposizione:

   * finalità: unire le risorse in base al relativo percorso di ricerca
   * punto di montaggio: `/mnt/overlay`
   * utilizzo: `mount point + relative path`
   * esempio:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Sostituisci:

   * finalità: unire le risorse in base al loro super tipo
   * punto di montaggio: `/mnt/overide`
   * utilizzo: `mount point + absolute path`
   * esempio:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Esempio di utilizzo {#example-of-usage}

Alcuni esempi sono trattati:

* Sovrapposizione:

   * [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
   * [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)

* Sostituisci:

   * [Configurazione delle proprietà della pagina](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
