---
title: Personalizzazione delle console
description: AEM offre diversi meccanismi per personalizzare le console dell’istanza di authoring
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---

# Personalizzazione delle console {#customizing-the-consoles}

>[!CAUTION]
>
>Questo documento descrive come personalizzare le console nella moderna interfaccia touch e non si applica all’interfaccia classica.

AEM offre diversi meccanismi per consentirti di personalizzare le console (e la funzionalità di [authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)) dell&#39;istanza di authoring.

* Clientlibs
Le clientlibs consentono di estendere l’implementazione predefinita per realizzare nuove funzionalità, riutilizzando le funzioni, gli oggetti e i metodi standard. Durante la personalizzazione, puoi creare una libreria client personalizzata in `/apps.`. Ad esempio, può contenere il codice necessario per il componente personalizzato.

* Sovrapposizioni
Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre la funzionalità standard (in `/libs`) con la funzionalità personalizzata (in `/apps`). Quando crei una sovrapposizione, non è necessaria una copia 1:1 dell’originale, in quanto la fusione di risorse sling consente l’ereditarietà.

Questi possono essere utilizzati in molti modi per estendere le console AEM. Di seguito è riportata una piccola selezione (ad alto livello).

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Utilizzo e creazione di [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilizzo e creazione di [sovrapposizioni](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>


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

Ad esempio, è possibile sovrapporre la seguente posizione all&#39;interno della struttura `/libs`:

* console (tutte le console basate sulle pagine dell’interfaccia utente Granite); ad esempio:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Per ulteriori suggerimenti e strumenti, consulta l&#39;articolo della Knowledge Base [Risoluzione dei problemi relativi all&#39;interfaccia utente touch di AEM](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-16935).

## Personalizzazione della vista predefinita per una console {#customizing-the-default-view-for-a-console}

Puoi personalizzare la vista predefinita (colonna, scheda, elenco) per una console:

1. È possibile riordinare le viste sovrapponendo la voce richiesta da in:

   `/libs/wcm/core/content/sites/jcr:content/views`

   La prima voce sarà quella predefinita.

   I nodi disponibili sono correlati alle opzioni di visualizzazione disponibili:

   * `column`
   * `card`
   * `list`

1. Ad esempio, in un elenco di sovrapposizione per:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Definisci la seguente proprietà:

   * **Nome**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valore**: `column`

### Aggiungi nuova azione alla barra degli strumenti {#add-new-action-to-the-toolbar}

1. Puoi creare componenti personalizzati e includere le librerie client corrispondenti per le azioni personalizzate. Ad esempio, un&#39;azione **Promuovi a Twitter** in:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Questa può quindi essere collegata a un elemento della barra degli strumenti nella console:

   `/apps/<yourProject>/admin/ext/launches`

   Ad esempio, in modalità di selezione:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Limitare un&#39;azione della barra degli strumenti a un gruppo specifico {#restrict-a-toolbar-action-to-a-specific-group}

1. Puoi utilizzare una condizione di rendering personalizzata per sovrapporre l’azione standard e imporre condizioni specifiche che devono essere soddisfatte prima che venga eseguito il rendering.

   Ad esempio, crea un componente per controllare le condizioni di rendering in base al gruppo:

   `/apps/myapp/components/renderconditions/group`

1. Per applicare questi elementi all’azione Crea sito nella console Sites:

   `/libs/wcm/core/content/sites`

   Crea la sovrapposizione:

   `/apps/wcm/core/content/sites`

1. Quindi aggiungi la condizione di rendering per l’azione:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Utilizzando le proprietà in questo nodo è possibile definire il `groups` consentito per eseguire l&#39;azione specifica, ad esempio `administrators`

### Personalizzazione delle colonne nella vista a elenco {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Questa funzionalità è ottimizzata per colonne di campi di testo; per altri tipi di dati è possibile sovrapporre `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

Per personalizzare le colonne nella vista a elenco:

1. Sovrapponi l’elenco delle colonne disponibili.

   * Sul nodo:

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * Aggiungi le nuove colonne o rimuovi quelle esistenti.

   Per ulteriori informazioni, consulta [Utilizzo di sovrapposizioni (e Sling Resource Merger)](/help/sites-developing/overlays.md).

1. Facoltativamente:

   * Se si desidera inserire dati aggiuntivi, è necessario scrivere un [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con un
     Proprietà `pageInfoProviderType`.

   Ad esempio, consulta la classe/bundle allegato (da GitHub) di seguito.

1. Ora puoi selezionare la colonna nel configuratore di colonne della vista a elenco.

### Filtrare le risorse {#filtering-resources}

Quando si utilizza una console, un caso d’uso comune si verifica quando l’utente deve selezionare tra le risorse (ad esempio pagine, componenti, risorse e così via). Può assumere la forma di un elenco, ad esempio, dal quale l’autore deve scegliere un elemento.

Per mantenere l’elenco a una dimensione ragionevole e pertinente al caso d’uso, un filtro può essere implementato sotto forma di predicato personalizzato. Per ulteriori informazioni, vedere [Personalizzazione dell&#39;authoring delle pagine - Filtraggio delle risorse](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources).
