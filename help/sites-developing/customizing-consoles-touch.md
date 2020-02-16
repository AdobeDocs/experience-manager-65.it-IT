---
title: Personalizzazione delle console
seo-title: Personalizzazione delle console
description: AEM offre diversi metodi per personalizzare le console dell’istanza di authoring
seo-description: AEM offre diversi metodi per personalizzare le console dell’istanza di authoring
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Personalizzazione delle console {#customizing-the-consoles}

>[!CAUTION]
>
>Questo documento descrive come personalizzare le console nell’interfaccia touch moderna e non applicabile all’interfaccia classica.

AEM offre diversi metodi per personalizzare le console (e la funzionalità [di authoring delle](/help/sites-developing/customizing-page-authoring-touch.md)pagine) dell’istanza di authoring.

* ClientlibsClientlibs consente di estendere l&#39;implementazione predefinita per realizzare nuove funzionalità, riutilizzando al contempo le funzioni, gli oggetti e i metodi standard. Quando personalizzate, potete creare clientlib personalizzate in `/apps.` Ad esempio, può contenere il codice richiesto per il componente personalizzato.

* OverlaysOverlays Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre la funzionalità standard (in `/libs`) con la propria funzionalità personalizzata (in `/apps`). Quando create una sovrapposizione, non è necessaria una copia 1:1 dell’originale, in quanto la fusione delle risorse di sling consente l’ereditarietà.

che possono essere utilizzati in molti modi per estendere le console AEM. Di seguito è riportata una piccola selezione (ad alto livello).

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Utilizzo e creazione di [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilizzo e creazione di [sovrapposizioni](/help/sites-developing/overlays.md).
>* [GRANITE](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>
>
Questo argomento è trattato anche nella sessione [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) - Personalizzazione dell&#39;interfaccia [utente per AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).

>[!CAUTION]
>
>Non ***devi*** cambiare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
   >
   >
1. Apportare modifiche all&#39;interno `/apps`
>



Ad esempio, è possibile sovrapporre la seguente posizione all’interno della `/libs` struttura:

* console (qualsiasi console basata sulle pagine dell’interfaccia Granite); ad esempio:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Per ulteriori suggerimenti e strumenti, consulta l’articolo della Knowledge Base [Risoluzione di problemi](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)relativi all’interfaccia utente AEM Touch.

## Personalizzazione della visualizzazione predefinita per una console {#customizing-the-default-view-for-a-console}

Potete personalizzare la visualizzazione predefinita (colonna, scheda, elenco) per una console:

1. Potete riordinare le viste sovrapponendo la voce richiesta da sotto:

   `/libs/wcm/core/content/sites/jcr:content/views`

   La prima voce sarà quella predefinita.

   I nodi disponibili sono correlati alle opzioni di visualizzazione disponibili:

   * `column`
   * `card`
   * `list`

1. Ad esempio, in una sovrapposizione per un elenco:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Definire la proprietà seguente:

   * **Nome**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valore**: `column`

### Aggiungi nuova azione alla barra degli strumenti {#add-new-action-to-the-toolbar}

1. Potete creare componenti personalizzati e includere le librerie client corrispondenti per le azioni personalizzate. Ad esempio, un&#39;azione **Promote to Twitter** all&#39;indirizzo:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   È quindi possibile collegarlo a un elemento della barra degli strumenti presente nella console:

   `/apps/<yourProject>/admin/ext/launches`

   Ad esempio, in modalità di selezione:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Limitare un&#39;azione barra degli strumenti a un gruppo specifico {#restrict-a-toolbar-action-to-a-specific-group}

1. Potete utilizzare una condizione di rendering personalizzata per sovrapporre l&#39;azione standard e imporre condizioni specifiche che devono essere soddisfatte prima del rendering.

   Ad esempio, create un componente per controllare le condizioni di rendering in base al gruppo:

   `/apps/myapp/components/renderconditions/group`

1. Per applicare queste opzioni all’azione Crea sito nella console Siti:

   `/libs/wcm/core/content/sites`

   Create la sovrapposizione:

   `/apps/wcm/core/content/sites`

1. Quindi aggiungete la condizione di rendering per l’azione:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Utilizzando le proprietà di questo nodo è possibile definire le `groups` autorizzazioni per eseguire l&#39;azione specifica; ad esempio, `administrators`

### Personalizzazione delle colonne nella vista Elenco {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Questa funzione è ottimizzata per le colonne di campi di testo; per altri tipi di dati è possibile sovrapporre `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

Per personalizzare le colonne nella vista a elenco:

1. Sovrapporre l’elenco delle colonne disponibili.

   * Sul nodo:

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * Aggiungete le nuove colonne o rimuovete quelle esistenti.
   Per ulteriori informazioni, consultate [Utilizzo delle sovrapposizioni (e Sling Resource Merger)](/help/sites-developing/overlays.md) .

1. Facoltativamente:

   * Se si desidera collegare dati aggiuntivi, è necessario scrivere una pagina [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con un
      `pageInfoProviderType` proprietà.
   Ad esempio, vedete la classe/pacchetto collegato (da GitHub) di seguito.

1. È ora possibile selezionare la colonna nel configuratore colonna della vista a elenco.

### Risorse filtro {#filtering-resources}

Quando si utilizza una console, un caso comune è quando l’utente deve selezionare una delle risorse (ad esempio pagine, componenti, risorse ecc.). Può assumere la forma di un elenco, ad esempio da cui l’autore deve scegliere un elemento.

Per mantenere l&#39;elenco a dimensioni ragionevoli e anche pertinente al caso d&#39;uso, è possibile implementare un filtro sotto forma di predicato personalizzato. Consultate [questo articolo](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) per i dettagli.
