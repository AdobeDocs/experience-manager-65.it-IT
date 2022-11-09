---
title: Personalizzazione delle console
seo-title: Customizing the Consoles
description: AEM offre diversi meccanismi per personalizzare le console dell’istanza di authoring
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# Personalizzazione delle console {#customizing-the-consoles}

>[!CAUTION]
>
>Questo documento descrive come personalizzare le console nell’interfaccia touch moderna e non applicabile all’interfaccia classica.

AEM offre diversi meccanismi per personalizzare le console (e [funzionalità di authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)) dell’istanza di authoring.

* Clientlibs Clientlibs consente di estendere l&#39;implementazione predefinita per realizzare nuove funzionalità, riutilizzando al contempo le funzioni, gli oggetti e i metodi standard. Quando personalizzi, puoi creare la tua clientlib in `/apps.` Ad esempio, può contenere il codice richiesto per il componente personalizzato.

* Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre la funzionalità standard (in `/libs`) con funzionalità personalizzate (in `/apps`). Quando si crea una sovrapposizione non è necessaria una copia 1:1 dell&#39;originale, in quanto la fusione delle risorse sling consente l&#39;ereditarietà.

che possono essere utilizzati in diversi modi per estendere le console AEM. Di seguito è riportata una piccola selezione (ad alto livello).

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Utilizzo e creazione [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilizzo e creazione [sovrapposizioni](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>



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


Ad esempio, la seguente posizione all’interno della `/libs` La struttura può essere sovrapposta:

* console (tutte le console basate sulle pagine dell’interfaccia utente Granite); ad esempio:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Vedi l&#39;articolo della Knowledge Base, [Risoluzione dei problemi AEM TouchUI](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html), per ulteriori suggerimenti e strumenti.

## Personalizzazione della visualizzazione predefinita per una console {#customizing-the-default-view-for-a-console}

Puoi personalizzare la visualizzazione predefinita (colonna, scheda, elenco) per una console:

1. Puoi riordinare le visualizzazioni sovrapponendo la voce richiesta da sotto:

   `/libs/wcm/core/content/sites/jcr:content/views`

   La prima voce è l’impostazione predefinita.

   I nodi disponibili sono correlati alle opzioni di visualizzazione disponibili:

   * `column`
   * `card`
   * `list`

1. Ad esempio, in una sovrapposizione per un elenco:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Definisci la seguente proprietà:

   * **Nome**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valore**: `column`

### Aggiungi nuova azione alla barra degli strumenti {#add-new-action-to-the-toolbar}

1. Puoi creare componenti personalizzati e includere le librerie client corrispondenti per le azioni personalizzate. Ad esempio, un **Promozione a Twitter** all&#39;indirizzo:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Questo può essere collegato a un elemento della barra degli strumenti nella console:

   `/apps/<yourProject>/admin/ext/launches`

   Ad esempio, in modalità Selezione:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Limitare un’azione barra degli strumenti a un gruppo specifico {#restrict-a-toolbar-action-to-a-specific-group}

1. Puoi utilizzare una condizione di rendering personalizzata per sovrapporre l’azione standard e imporre condizioni specifiche che devono essere soddisfatte prima che venga renderizzata.

   Ad esempio, crea un componente per controllare le condizioni di rendering in base al gruppo:

   `/apps/myapp/components/renderconditions/group`

1. Per applicarle all’azione Crea sito nella console Sites :

   `/libs/wcm/core/content/sites`

   Crea la sovrapposizione:

   `/apps/wcm/core/content/sites`

1. Quindi aggiungi la condizione di rendering per l’azione:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Utilizzando le proprietà di questo nodo è possibile definire le `groups` consentire l&#39;esecuzione dell&#39;azione specifica; ad esempio, `administrators`

### Personalizzazione delle colonne nella vista a elenco {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Questa funzione è ottimizzata per le colonne di campi di testo; per altri tipi di dati è possibile sovrapporre `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

Per personalizzare le colonne nella vista a elenco:

1. Sovrapponi l’elenco delle colonne disponibili.

   * Sul nodo:

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * Aggiungi le nuove colonne o rimuovine quelle esistenti.
   Vedi [Utilizzo delle sovrapposizioni (e di Sling Resource Merger)](/help/sites-developing/overlays.md) per ulteriori informazioni.

1. Facoltativamente:

   * Se desideri collegare dati aggiuntivi, devi scrivere un [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con
      `pageInfoProviderType` proprietà.

   Ad esempio, vedi la classe/bundle collegata (da GitHub) di seguito.

1. È ora possibile selezionare la colonna nel configuratore colonna della vista a elenco.

### Risorse di filtro {#filtering-resources}

Quando si utilizza una console, un caso d’uso comune si verifica quando l’utente deve selezionare una delle risorse (ad esempio pagine, componenti, risorse, ecc.). Questo può assumere la forma di un elenco, ad esempio da cui l’autore deve scegliere un elemento.

Per mantenere l’elenco a una dimensione ragionevole e pertinente al caso d’uso, è possibile implementare un filtro sotto forma di predicato personalizzato. Vedi [articolo](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) per i dettagli.
