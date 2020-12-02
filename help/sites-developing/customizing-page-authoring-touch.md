---
title: Personalizzazione dell’authoring delle pagine
seo-title: Personalizzazione dell’authoring delle pagine
description: AEM offre diversi metodi per personalizzare la funzionalità di authoring delle pagine
seo-description: AEM offre diversi metodi per personalizzare la funzionalità di authoring delle pagine
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---


# Personalizzazione dell&#39;authoring delle pagine{#customizing-page-authoring}

>[!CAUTION]
>
>Questo documento descrive come personalizzare l’authoring delle pagine nell’interfaccia touch moderna e non applicabile all’interfaccia classica.

AEM offre diversi metodi per personalizzare la funzionalità di authoring delle pagine (e le [console](/help/sites-developing/customizing-consoles-touch.md)) dell’istanza di authoring.

* Clientlibs

   Clientlibs consente di estendere l&#39;implementazione predefinita per realizzare nuove funzionalità, riutilizzando le funzioni, gli oggetti e i metodi standard. Quando personalizzate, potete creare una clientlib personalizzata in `/apps.` La nuova clientlib deve:

   * dipendono dalla clientlib di authoring `cq.authoring.editor.sites.page`
   * far parte della categoria `cq.authoring.editor.sites.page.hook` appropriata

* Sovrapposizioni

   Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre la funzionalità standard (in `/libs`) con la propria funzionalità personalizzata (in `/apps`). Quando create una sovrapposizione, non è necessaria una copia 1:1 dell&#39;originale, in quanto la [fusione delle risorse sling](/help/sites-developing/sling-resource-merger.md) consente l&#39;ereditarietà.

>[!NOTE]
>
>Per ulteriori informazioni, vedere la documentazione [JS set](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

che possono essere utilizzati in molti modi per estendere la funzionalità di authoring delle pagine nell’istanza AEM. Di seguito è riportata una selezione (ad alto livello).

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Utilizzo e creazione di [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilizzo e creazione di [sovrapposizioni](/help/sites-developing/overlays.md).
>* [GRANITE](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Struttura dell’](/help/sites-developing/touch-ui-structure.md) interfaccia AEM touch per informazioni dettagliate sulle aree strutturali utilizzate per l’authoring delle pagine.

>
>
Questo argomento è trattato anche nella sessione [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) - [Personalizzazione dell&#39;interfaccia utente per AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html).

>[!CAUTION]
>
>***non è necessario*** modificare nulla nel percorso `/libs`.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
>1. Apportare modifiche all&#39;interno di `/apps`


## Aggiungi nuovo livello (modalità) {#add-new-layer-mode}

Durante la modifica di una pagina, sono disponibili diverse [modalità](/help/sites-authoring/author-environment-tools.md#page-modes). Queste modalità sono implementate utilizzando [livelli](/help/sites-developing/touch-ui-structure.md#layer). che consentono di accedere a diversi tipi di funzionalità per lo stesso contenuto della pagina. I livelli standard sono: modifica, anteprima, annotazione, sviluppatore e targeting.

### Esempio di livello: Stato Live Copy {#layer-example-live-copy-status}

Un&#39;istanza AEM standard fornisce il livello MSM. Questo consente di accedere ai dati relativi a [gestione multisito](/help/sites-administering/msm.md) e li evidenzia nel livello.

Per visualizzarlo in azione è possibile modificare qualsiasi pagina [Copia lingua We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) (o qualsiasi altra pagina Live Copy) e selezionare la modalità **Stato Live Copy**.

È possibile trovare la definizione del livello MSM (per riferimento) in:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Esempio di codice {#code-sample}

Si tratta di un pacchetto di esempio che mostra come creare un nuovo livello (modalità), un nuovo livello per la visualizzazione MSM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il nuovo progetto di authoring Aem-layer-mode su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Aggiungi nuova categoria di selezione al browser delle risorse {#add-new-selection-category-to-asset-browser}

Il browser delle risorse mostra risorse di vari tipi/categorie (ad esempio immagini, documenti, ecc.). Le risorse possono essere filtrate in base a queste categorie di risorse.

### Esempio di codice {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` è un pacchetto di esempio che mostra come aggiungere un nuovo gruppo a Asset Finder. Questo esempio si collega al flusso pubblico di [Flickr](https://www.flickr.com) e lo visualizza nel pannello laterale.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Aprire il progetto Aem-authoring-extension-setfinder-flickr su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Risorse filtro {#filtering-resources}

Durante l’authoring delle pagine, l’utente deve spesso selezionare tra le risorse (ad esempio pagine, componenti, risorse ecc.). Può assumere la forma di un elenco, ad esempio da cui l’autore deve scegliere un elemento.

Per mantenere l&#39;elenco a dimensioni ragionevoli e anche pertinente al caso d&#39;uso, è possibile implementare un filtro sotto forma di predicato personalizzato. Ad esempio, se il componente [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) viene utilizzato per consentire all&#39;utente di selezionare il percorso di una determinata risorsa, i percorsi presentati possono essere filtrati nel modo seguente:

* Implementate il predicato personalizzato implementando l&#39;interfaccia [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Specificate un nome per il predicato e fate riferimento a tale nome quando utilizzate il percorso `pathbrowser`.

Per ulteriori dettagli sulla creazione di un predicato personalizzato, consultate [questo articolo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>L&#39;implementazione di un predicato personalizzato mediante l&#39;implementazione dell&#39;interfaccia `com.day.cq.commons.predicate.AbstractNodePredicate` funziona anche nell&#39;interfaccia classica.
>
>Per un esempio di implementazione di un predicato personalizzato nell&#39;interfaccia classica, consultate [questo articolo della knowledge base](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html).

## Aggiungi nuova azione a una barra degli strumenti di un componente {#add-new-action-to-a-component-toolbar}

Ogni componente (in genere) dispone di una barra degli strumenti che consente di accedere a una serie di azioni che possono essere eseguite su tale componente.

### Esempio di codice {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` è un pacchetto di esempio che mostra come creare un’azione personalizzata per la barra degli strumenti per il rendering dei componenti.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Aprire il progetto Aem-authoring-extension-toolbar-screenshot su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Aggiungi nuovo editor locale {#add-new-in-place-editor}

### Editor locale standard {#standard-in-place-editor}

In un’installazione standard di AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contiene le definizioni dei vari editor disponibili.

1. Esiste una connessione tra l’editor e ciascun tipo di risorsa (come nel componente) che può essere utilizzata:

   * `cq:inplaceEditing`

      ad esempio:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * proprietà: `editorType`

            Definisce il tipo di editor in linea che verrà utilizzato quando viene attivata la modifica locale per quel componente; ad esempio `text`, `textimage`, `image`, `title`.

1. Ulteriori dettagli di configurazione dell&#39;editor possono essere configurati utilizzando un nodo `config` contenente configurazioni e un altro nodo `plugin` per contenere i necessari dettagli di configurazione del plug-in.

   Di seguito è riportato un esempio di definizione delle proporzioni per il plug-in di ritaglio dell’immagine per il componente immagine. Tenete presente che, a causa del potenziale di dimensioni dello schermo molto limitate, le proporzioni del ritaglio sono state spostate nell’editor a schermo intero e possono essere visualizzate solo in questo caso.

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >Tenere presente che AEM rapporti di ritaglio, come impostato dalla proprietà `ratio`, sono definiti come **height/width**. Questo differisce dalla definizione tradizionale di larghezza/altezza, per ragioni di compatibilità con versioni precedenti. Gli utenti che creano contenuti non saranno a conoscenza di alcuna differenza, a condizione che definiate chiaramente la proprietà `name`, in quanto questo è ciò che viene visualizzato nell&#39;interfaccia utente.

#### Creazione di un nuovo editor locale {#creating-a-new-in-place-editor}

Per implementare un nuovo editor locale (all&#39;interno della clientlib):

>[!NOTE]
>
>Ad esempio, vedete:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementa:

   * `setUp`
   * `tearDown`

1. Registra l’editor (include il costruttore):

   * `editor.register`

1. Specifica la connessione tra l’editor e ogni tipo di risorsa (come nel componente) che può essere utilizzata.

#### Esempio di codice per la creazione di un nuovo editor locale {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` è un pacchetto di esempio che mostra come creare un nuovo editor locale in AEM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto Aem-authoring-extension-in-place-editor su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configurazione di più editor interni {#configuring-multiple-in-place-editors}

È possibile configurare un componente in modo che abbia più editor locali. Quando sono configurati più editor interni, potete selezionare il contenuto appropriato e aprire l&#39;editor appropriato. Per ulteriori informazioni, consultare la documentazione [Configuring Multiple In-Place Editors](/help/sites-developing/multiple-inplace-editors.md).

## Aggiungere una nuova azione pagina {#add-a-new-page-action}

Per aggiungere una nuova azione di pagina alla barra degli strumenti della pagina, ad esempio un&#39;azione **Torna a siti** (console).

### Esempio di codice {#code-sample-3}

`aem-authoring-extension-header-backtosites` è un pacchetto di esempio che mostra come creare un&#39;azione personalizzata per la barra dell&#39;intestazione per tornare alla console Siti.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto Aem-authoring-extension-header-backtosites su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizzazione del flusso di lavoro di richiesta di attivazione {#customizing-the-request-for-activation-workflow}

Il flusso di lavoro out-of-the-box, **Request for Activation**, viene attivato automaticamente quando un autore del contenuto non dispone dei diritti di replica appropriati.

Per ottenere un comportamento personalizzato in seguito a tale attivazione, è possibile sovrapporre il flusso di lavoro **Request for Activation**:

1. In `/apps` sovrapporre la procedura guidata **Siti**:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >In questo modo, sostituisce l’istanza comune di:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Aggiornate il modello di flusso di lavoro [](/help/sites-developing/workflows-models.md) e le configurazioni/script correlate, a seconda delle necessità.
1. rimuovere il diritto all&#39; [ `replicate` action](/help/sites-administering/security.md#actions) da tutti gli utenti appropriati per tutte le pagine pertinenti; affinché questo flusso di lavoro venga attivato come azione predefinita quando un utente tenta di pubblicare (o replicare) una pagina.

