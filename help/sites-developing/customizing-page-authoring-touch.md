---
title: Personalizzazione dell’authoring delle pagine
description: Adobe Experience Manager (AEM) offre diversi meccanismi per personalizzare la funzionalità di authoring delle pagine.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 1%

---

# Personalizzazione dell’authoring delle pagine{#customizing-page-authoring}

>[!CAUTION]
>
>Questo documento descrive come personalizzare l’authoring delle pagine nella moderna interfaccia touch e non si applica all’interfaccia classica.

Adobe Experience Manager (AEM) offre diversi meccanismi per personalizzare la funzionalità di authoring delle pagine (e le [console](/help/sites-developing/customizing-consoles-touch.md)) dell&#39;istanza di authoring.

* Clientlibs

  Le clientlibs consentono di estendere l’implementazione predefinita per realizzare nuove funzionalità, riutilizzando le funzioni, gli oggetti e i metodi standard. Durante la personalizzazione, puoi creare la tua libreria client in `/apps.`. La nuova libreria client deve:

   * dipende dalla libreria client di authoring `cq.authoring.editor.sites.page`
   * fai parte della categoria `cq.authoring.editor.sites.page.hook` appropriata

* Sovrapposizioni

  Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre la funzionalità standard (in `/libs`) con la funzionalità personalizzata (in `/apps`). Durante la creazione di una sovrapposizione, non è necessaria una copia 1:1 dell&#39;originale, in quanto la [sling resource merger](/help/sites-developing/sling-resource-merger.md) consente l&#39;ereditarietà.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Set di documentazione JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Questi possono essere utilizzati in molti modi per estendere la funzionalità di authoring delle pagine nell’istanza AEM. Di seguito è riportata una selezione (ad alto livello).

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Utilizzo e creazione di [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilizzo e creazione di [sovrapposizioni](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Struttura dell&#39;interfaccia utente touch dell&#39;AEM](/help/sites-developing/touch-ui-structure.md) per i dettagli delle aree strutturali utilizzate per l&#39;authoring delle pagine.
>


>[!CAUTION]
>
>***Non*** modificare nulla nel percorso `/libs`.
>
>Il motivo è che il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l&#39;istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricrea l&#39;elemento richiesto (ovvero, poiché esiste in `/libs`) in `/apps`
>1. Apporta le modifiche in `/apps`

## Aggiungi nuovo livello (modalità) {#add-new-layer-mode}

Quando modifichi una pagina, sono disponibili varie [modalità](/help/sites-authoring/author-environment-tools.md#page-modes). Queste modalità sono implementate utilizzando [livelli](/help/sites-developing/touch-ui-structure.md#layer). Consentono di accedere a diversi tipi di funzionalità per lo stesso contenuto della pagina. I livelli standard sono: modifica, anteprima, annota, sviluppatore e targeting.

### Esempio di livello: stato Live Copy {#layer-example-live-copy-status}

Un&#39;istanza AEM standard fornisce il livello MSM. Consente di accedere ai dati relativi alla [gestione multisito](/help/sites-administering/msm.md) e di evidenziarli nel livello.

Per vederla in azione, puoi modificare qualsiasi [copia per lingua We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) pagina (o qualsiasi altra pagina Live Copy) e selezionare la modalità **Stato Live Copy**.

Puoi trovare la definizione del livello MSM (per riferimento) in:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Esempio di codice {#code-sample}

Questo è un pacchetto di esempio che mostra come creare un livello (modalità), che è un nuovo livello per la vista MSM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-authoring-new-layer-mode su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Aggiungi nuova categoria selezione al browser risorse {#add-new-selection-category-to-asset-browser}

Il browser Risorse mostra risorse di vari tipi/categorie (ad esempio, immagini e documenti). Le risorse possono essere filtrate anche in base a queste categorie di risorse.

### Esempio di codice {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` è un pacchetto di esempio che mostra come aggiungere un gruppo a Asset Finder. Questo esempio si connette al flusso pubblico di [Flickr](https://www.flickr.com) e lo mostra nel pannello laterale.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-assetfinder-flickr su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrare le risorse {#filtering-resources}

Durante l’authoring delle pagine, l’utente deve spesso selezionare tra le risorse (ad esempio pagine, componenti e risorse). Può assumere la forma di un elenco, ad esempio, dal quale l’autore deve scegliere un elemento.

Per mantenere l’elenco a una dimensione ragionevole e pertinente al caso d’uso, un filtro può essere implementato sotto forma di predicato personalizzato. Ad esempio, se il componente [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) viene utilizzato per consentire all&#39;utente di selezionare il percorso di una particolare risorsa, i percorsi presentati possono essere filtrati nel modo seguente:

* Implementare il predicato personalizzato implementando l&#39;interfaccia [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Specificare un nome per il predicato e fare riferimento a tale nome quando si utilizza `pathbrowser`.

Per ulteriori dettagli sulla creazione di un predicato personalizzato, vedi [questo articolo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>L&#39;implementazione di un predicato personalizzato tramite l&#39;implementazione dell&#39;interfaccia `com.day.cq.commons.predicate.AbstractNodePredicate` funziona anche nell&#39;interfaccia classica.
>
>Consulta [questo articolo della knowledge base](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) per un esempio di implementazione di un predicato personalizzato nell&#39;interfaccia classica.

## Aggiungere una nuova azione alla barra degli strumenti di un componente {#add-new-action-to-a-component-toolbar}

Ogni componente dispone (in genere) di una barra degli strumenti che consente di accedere a una serie di azioni che possono essere eseguite su tale componente.

### Esempio di codice {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` è un pacchetto di esempio che mostra come creare un&#39;azione della barra degli strumenti personalizzata per eseguire il rendering dei componenti.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-toolbar-screenshot su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Aggiungi nuovo editor locale {#add-new-in-place-editor}

### Editor locale standard {#standard-in-place-editor}

In un’installazione standard di AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contiene le definizioni dei vari editor disponibili.

1. Esiste una connessione tra l’editor e ogni tipo di risorsa (come nel componente) che può utilizzarla:

   * `cq:inplaceEditing`

     ad esempio:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * proprietà: `editorType`

           Definisce il tipo di editor in linea utilizzato quando viene attivata la modifica diretta per quel componente, ad esempio `text`, `textimage`, `image`, `title`.

1. Ulteriori dettagli di configurazione dell&#39;editor possono essere configurati utilizzando un nodo `config` contenente configurazioni e un nodo `plugin` per contenere i dettagli di configurazione del plug-in necessari.

   Di seguito è riportato un esempio di definizione delle proporzioni per il plug-in di ritaglio immagine del componente immagine. A causa del potenziale delle dimensioni limitate dello schermo, le proporzioni del ritaglio sono state spostate nell’editor a schermo intero e possono essere visualizzate solo lì.

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
   >I rapporti di ritaglio AEM, impostati dalla proprietà `ratio`, sono definiti come **altezza/larghezza**. Ciò differisce dalla definizione tradizionale di larghezza/altezza e viene fatto per ragioni di compatibilità con le versioni precedenti. Gli utenti che creano i file non noteranno alcuna differenza, a condizione che tu definisca chiaramente la proprietà `name`, in quanto questo è ciò che viene visualizzato nell&#39;interfaccia utente.

#### Creazione di un nuovo editor locale {#creating-a-new-in-place-editor}

Per implementare un nuovo editor locale (nella libreria client):

>[!NOTE]
>
>Ad esempio, consulta:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementare:

   * `setUp`
   * `tearDown`

1. Registra l’editor (include il costruttore):

   * `editor.register`

1. Fornisci la connessione tra l’editor e ogni tipo di risorsa (come nel componente) che può utilizzarlo.

#### Esempio di codice per la creazione di un nuovo editor locale {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` è un pacchetto di esempio che mostra come creare un editor locale in AEM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-inplace-editor in GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configurazione di più editor locali {#configuring-multiple-in-place-editors}

È possibile configurare un componente in modo che abbia più editor locali. Quando sono configurati più editor locali, puoi selezionare il contenuto appropriato e aprire l’editor appropriato. Per ulteriori informazioni, consulta la documentazione [Configurazione di più editor locali](/help/sites-developing/multiple-inplace-editors.md).

## Aggiungi un&#39;azione Nuova pagina {#add-a-new-page-action}

Per aggiungere una nuova azione di pagina alla barra degli strumenti della pagina, ad esempio, **Torna a Sites** (console).

### Esempio di codice {#code-sample-3}

`aem-authoring-extension-header-backtosites` è un pacchetto di esempio che mostra come creare un&#39;azione personalizzata della barra di intestazione per tornare alla console Sites.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-header-backtosites su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizzazione del flusso di lavoro Richiesta attivazione {#customizing-the-request-for-activation-workflow}

Flusso di lavoro predefinito, **Richiesta di attivazione**:

* Verrà visualizzato automaticamente nel menu appropriato quando un autore di contenuti **non dispone** dei diritti di replica appropriati, ma **non dispone di** appartenenze a DAM-Users e Author.

* In caso contrario, non viene visualizzato nulla, poiché i diritti di replica sono stati rimossi.

Per personalizzare il comportamento di questa attivazione, puoi sovrapporre il flusso di lavoro **Richiesta di attivazione**:

1. In `/apps` sovrapporre la procedura guidata **Sites**:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Questo stesso sovrascriverà l’istanza comune di:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Aggiornare il [modello di flusso di lavoro](/help/sites-developing/workflows-models.md) e le configurazioni/script correlati in base alle esigenze.
1. Rimuovere il diritto all&#39;azione [`replicate`](/help/sites-administering/security.md#actions) da tutti gli utenti appropriati per tutte le pagine rilevanti; per attivare questo flusso di lavoro come azione predefinita quando uno degli utenti tenta di pubblicare (o replicare) una pagina.
