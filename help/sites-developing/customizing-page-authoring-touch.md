---
title: Personalizzazione dell’authoring delle pagine
seo-title: Customizing Page Authoring
description: AEM offre diversi meccanismi per personalizzare la funzionalità di authoring delle pagine
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 2%

---

# Personalizzazione dell’authoring delle pagine{#customizing-page-authoring}

>[!CAUTION]
>
>Questo documento descrive come personalizzare l’authoring delle pagine nell’interfaccia touch e moderna e non si applica all’interfaccia classica.

AEM offre vari meccanismi per personalizzare la funzionalità di authoring delle pagine (e la [console](/help/sites-developing/customizing-consoles-touch.md)) dell’istanza di authoring.

* Clientlibs

   Le clientlibs consentono di estendere l’implementazione predefinita per realizzare nuove funzionalità, riutilizzando al contempo le funzioni, gli oggetti e i metodi standard. Quando personalizzi, puoi creare la tua clientlib in `/apps.` La nuova clientlib deve:

   * dipende da authoring clientlib `cq.authoring.editor.sites.page`
   * far parte del `cq.authoring.editor.sites.page.hook` categoria

* Sovrapposizioni

   Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre le funzionalità standard (in `/libs`) con funzionalità personalizzate (in `/apps`). Quando si crea una sovrapposizione, non è necessaria una copia 1:1 dell&#39;originale, in quanto la [fusione di risorse sling](/help/sites-developing/sling-resource-merger.md) consente l’ereditarietà.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Set di documentazione JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

Questi possono essere utilizzati in molti modi per estendere la funzionalità di authoring delle pagine nell’istanza di AEM. Di seguito è riportata una selezione (ad alto livello).

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Utilizzo e creazione [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilizzo e creazione [sovrapposizioni](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Struttura dell’interfaccia utente AEM touch](/help/sites-developing/touch-ui-structure.md) per informazioni dettagliate sulle aree strutturali utilizzate per l’authoring delle pagine.
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
>1. Apporta modifiche a `/apps`


## Aggiungi nuovo livello (modalità) {#add-new-layer-mode}

Quando modifichi una pagina, sono disponibili varie [modalità](/help/sites-authoring/author-environment-tools.md#page-modes) disponibile. Queste modalità sono implementate utilizzando [livelli](/help/sites-developing/touch-ui-structure.md#layer). Questi consentono di accedere a tipi diversi di funzionalità per lo stesso contenuto della pagina. I livelli standard sono: modifica, anteprima, annotazione, sviluppatori e targeting.

### Esempio di livello: Stato Live Copy {#layer-example-live-copy-status}

Un&#39;istanza AEM standard fornisce il livello MSM. Consente di accedere ai dati relativi a [gestione multisito](/help/sites-administering/msm.md) e lo evidenzia nel livello.

Per visualizzarlo in azione è possibile modificare qualsiasi [Copia della lingua di We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) pagina (o qualsiasi altra pagina Live Copy) e seleziona la **Stato Live Copy** modalità.

Puoi trovare la definizione del livello MSM (per riferimento) in:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Esempio di codice {#code-sample}

Questo è un pacchetto di esempio che mostra come creare un nuovo livello (modalità), che è un nuovo livello per la visualizzazione MSM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-authoring-new-layer-mode su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Aggiungi nuova categoria di selezione al browser risorse {#add-new-selection-category-to-asset-browser}

Il browser delle risorse mostra risorse di vari tipi/categorie (ad esempio immagini, documenti, ecc.). Le risorse possono anche essere filtrate in base a queste categorie di risorse.

### Esempio di codice {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` è un pacchetto di esempio che mostra come aggiungere un nuovo gruppo a Asset Finder. Questo esempio si collega a [Flickr](https://www.flickr.com)Il flusso pubblico e lo mostra nel pannello laterale.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-asset-flickr su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Risorse di filtro {#filtering-resources}

Durante l’authoring delle pagine, l’utente deve spesso selezionare tra le risorse (ad esempio pagine, componenti, risorse, ecc.). Questo può assumere la forma di un elenco, ad esempio da cui l’autore deve scegliere un elemento.

Per mantenere l’elenco a una dimensione ragionevole e pertinente al caso d’uso, è possibile implementare un filtro sotto forma di predicato personalizzato. Ad esempio, se [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) viene utilizzato per consentire all’utente di selezionare il percorso di una particolare risorsa. I percorsi presentati possono essere filtrati nel modo seguente:

* Implementa il predicato personalizzato implementando [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) interfaccia.
* Specifica un nome per il predicato e fai riferimento a tale nome quando utilizzi il `pathbrowser`.

Per ulteriori dettagli sulla creazione di un predicato personalizzato, consulta [articolo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Implementazione di un predicato personalizzato tramite implementazione `com.day.cq.commons.predicate.AbstractNodePredicate` L’interfaccia di funziona anche nell’interfaccia classica.
>
>Vedi [questo articolo della knowledge base](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) per un esempio di implementazione di un predicato personalizzato nell’interfaccia classica.

## Aggiungere una nuova azione a una barra degli strumenti di un componente {#add-new-action-to-a-component-toolbar}

Ogni componente (in genere) dispone di una barra degli strumenti che consente di accedere a una serie di azioni che possono essere eseguite su quel componente.

### Esempio di codice {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` è un pacchetto di esempio che mostra come creare un’azione personalizzata della barra degli strumenti per eseguire il rendering dei componenti.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-authoring-extension-toolbar-screenshot su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Aggiungi nuovo editor locale {#add-new-in-place-editor}

### Editor locale standard {#standard-in-place-editor}

In un’installazione standard di AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contiene le definizioni dei vari editor disponibili.

1. Esiste una connessione tra l’editor e ogni tipo di risorsa (come nel componente) che può utilizzarlo:

   * `cq:inplaceEditing`

      Esempio:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * proprietà: `editorType`

            Definisce il tipo di editor in linea che verrà utilizzato quando viene attivata la modifica in linea per quel componente; ad esempio `text`, `textimage`, `image`, `title`.

1. Ulteriori dettagli di configurazione dell’editor possono essere configurati utilizzando un `config` nodo contenente configurazioni e ulteriori `plugin` nodo per contenere i dettagli di configurazione del plug-in necessari.

   Di seguito è riportato un esempio di definizione delle proporzioni per il plug-in di ritaglio immagine del componente immagine. A causa del potenziale di dimensioni dello schermo molto limitate, le proporzioni di ritaglio sono state spostate nell’editor a schermo intero e possono essere visualizzate solo in questo caso.

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
   >In AEM rapporti di ritaglio, come impostato da `ratio` sono definite come **altezza/larghezza**. Questo differisce dalla definizione tradizionale di larghezza/altezza, per ragioni di compatibilità con versioni precedenti. Gli utenti che creano contenuti non noteranno alcuna differenza, a condizione che tu definisca il `name` , poiché questo è ciò che viene visualizzato nell&#39;interfaccia utente.

#### Creazione di un nuovo editor diretto {#creating-a-new-in-place-editor}

Per implementare un nuovo editor locale (all’interno della clientlib):

>[!NOTE]
>
>Ad esempio, vedi:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementa:

   * `setUp`
   * `tearDown`

1. Registra l&#39;editor (include il costruttore):

   * `editor.register`

1. Specifica la connessione tra l’editor e ogni tipo di risorsa (come nel componente) che può utilizzarlo.

#### Esempio di codice per la creazione di un nuovo editor locale {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` è un pacchetto di esempio che mostra come creare un nuovo editor locale in AEM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-authoring-extension-inplace-editor su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configurazione di più editor in-place {#configuring-multiple-in-place-editors}

È possibile configurare un componente in modo che abbia più editor locali. Quando sono configurati più editor locali, puoi selezionare il contenuto appropriato e aprire l’editor appropriato. Consulta la sezione [Configurazione di più editor in-place](/help/sites-developing/multiple-inplace-editors.md) documentazione per ulteriori informazioni.

## Aggiungere una nuova azione pagina {#add-a-new-page-action}

Per aggiungere una nuova azione pagina alla barra degli strumenti della pagina, ad esempio un **Torna a Sites** (console).

### Esempio di codice {#code-sample-3}

`aem-authoring-extension-header-backtosites` è un pacchetto di esempio che mostra come creare un’azione di barra di intestazione personalizzata per tornare alla console Sites .

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-header-backtosites su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizzazione del flusso di lavoro di richiesta di attivazione {#customizing-the-request-for-activation-workflow}

Il flusso di lavoro preconfigurato, **Richiesta di attivazione**:

* Verrà visualizzato automaticamente nel menu appropriato quando un autore di contenuti **non ha** i diritti di replica appropriati, ma **ha** iscrizione a DAM-Users e Authors.

* In caso contrario non verrà visualizzato nulla, in quanto i diritti di replica sono stati rimossi.

Per avere un comportamento personalizzato su tale attivazione è possibile sovrapporre il **Richiesta di attivazione** flusso di lavoro:

1. In `/apps` sovrapporre **Sites** procedura guidata:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Questo sostituisce l’istanza comune di:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Aggiorna [modello di flusso di lavoro](/help/sites-developing/workflows-models.md) e configurazioni/script correlati, a seconda delle necessità.
1. Rimuovi il diritto alla [ `replicate` action](/help/sites-administering/security.md#actions) da tutti gli utenti appropriati per tutte le pagine pertinenti; far sì che questo flusso di lavoro venga attivato come azione predefinita quando uno degli utenti tenta di pubblicare (o replicare) una pagina.
