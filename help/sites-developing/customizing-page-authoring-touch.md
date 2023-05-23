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
ht-degree: 1%

---

# Personalizzazione dell’authoring delle pagine{#customizing-page-authoring}

>[!CAUTION]
>
>Questo documento descrive come personalizzare l’authoring delle pagine nella moderna interfaccia touch e non si applica all’interfaccia classica.

AEM offre diversi meccanismi per personalizzare la funzionalità di authoring delle pagine (e [console](/help/sites-developing/customizing-consoles-touch.md)) della tua istanza di authoring.

* Clientlibs

   Le clientlibs consentono di estendere l’implementazione predefinita per realizzare nuove funzionalità, riutilizzando le funzioni, gli oggetti e i metodi standard. Durante la personalizzazione, puoi creare una libreria client personalizzata in `/apps.` La nuova libreria client deve:

   * dipende dalla libreria client di authoring `cq.authoring.editor.sites.page`
   * fa parte del programma `cq.authoring.editor.sites.page.hook` categoria

* Sovrapposizioni

   Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre le funzionalità standard (in `/libs`) con funzionalità personalizzate (in `/apps`). Quando si crea una sovrapposizione, non è necessaria una copia 1:1 dell&#39;originale, in quanto [sling resource merger](/help/sites-developing/sling-resource-merger.md) consente l’ereditarietà.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Set di documentazione JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

Questi possono essere utilizzati in molti modi per estendere la funzionalità di authoring delle pagine nell’istanza AEM. Di seguito è riportata una selezione (ad alto livello).

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Utilizzo e creazione di [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilizzo e creazione di [sovrapposizioni](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Struttura dell’interfaccia utente touch dell’AEM](/help/sites-developing/touch-ui-structure.md) per informazioni dettagliate sulle aree strutturali utilizzate per l’authoring delle pagine.
>



>[!CAUTION]
>
>Tu ***deve*** non modificare nulla in `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe benissimo essere sovrascritto quando applichi un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricrea l’elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
>1. Apporta le modifiche in `/apps`


## Aggiungi nuovo livello (modalità) {#add-new-layer-mode}

Quando modifichi una pagina, sono disponibili vari [modalità](/help/sites-authoring/author-environment-tools.md#page-modes) disponibile. Queste modalità sono implementate utilizzando [livelli](/help/sites-developing/touch-ui-structure.md#layer). Consentono di accedere a diversi tipi di funzionalità per lo stesso contenuto della pagina. I livelli standard sono: modifica, anteprima, annota, sviluppatore e targeting.

### Esempio di livello: stato Live Copy {#layer-example-live-copy-status}

Un&#39;istanza AEM standard fornisce il livello MSM. Consente di accedere ai dati relativi a [gestione multisito](/help/sites-administering/msm.md) e lo evidenzia nel livello.

Per vederlo in azione puoi modificare qualsiasi [Copia lingua We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) pagina (o qualsiasi altra pagina live copy) e seleziona la **Stato Live Copy** modalità.

Puoi trovare la definizione del livello MSM (per riferimento) in:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Esempio di codice {#code-sample}

Questo è un pacchetto di esempio che mostra come creare un nuovo livello (modalità), che è un nuovo livello per la vista MSM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-authoring-new-layer-mode su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Aggiungi nuova categoria selezione al browser risorse {#add-new-selection-category-to-asset-browser}

Il browser Risorse mostra risorse di vari tipi/categorie (ad esempio immagini, documenti, ecc.). Le risorse possono essere filtrate anche in base a queste categorie di risorse.

### Esempio di codice {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` è un pacchetto di esempio che mostra come aggiungere un nuovo gruppo a asset finder. Questo esempio si connette a [Flickr](https://www.flickr.com)Il flusso pubblico di e li mostra nel pannello laterale.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-assetfinder-flickr su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrare le risorse {#filtering-resources}

Durante l’authoring delle pagine, l’utente deve spesso selezionare tra le risorse (ad esempio pagine, componenti, risorse, ecc.). Può assumere la forma di un elenco, ad esempio, dal quale l’autore deve scegliere un elemento.

Al fine di mantenere l’elenco a una dimensione ragionevole e pertinente al caso d’uso, un filtro può essere implementato sotto forma di predicato personalizzato. Ad esempio, se [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) Il componente viene utilizzato per consentire all’utente di selezionare il percorso di una particolare risorsa. I percorsi presentati possono essere filtrati nel modo seguente:

* Implementare il predicato personalizzato implementando [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) di rete.
* Specifica un nome per il predicato e fai riferimento a tale nome quando utilizzi il `pathbrowser`.

Per ulteriori dettagli sulla creazione di un predicato personalizzato, vedi [questo articolo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Implementazione di un predicato personalizzato tramite l’implementazione di `com.day.cq.commons.predicate.AbstractNodePredicate` L&#39;interfaccia di funziona anche nell&#39;interfaccia classica.
>
>Consulta [questo articolo della knowledge base](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) Ad esempio, puoi implementare un predicato personalizzato nell’interfaccia classica.

## Aggiungere una nuova azione alla barra degli strumenti di un componente {#add-new-action-to-a-component-toolbar}

Ogni componente dispone (in genere) di una barra degli strumenti che consente di accedere a una serie di azioni che possono essere eseguite su tale componente.

### Esempio di codice {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` è un pacchetto di esempio che mostra come creare un’azione personalizzata della barra degli strumenti per eseguire il rendering dei componenti.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-toolbar-screenshot su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

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

            Definisce il tipo di editor in linea che verrà utilizzato quando viene attivata la modifica diretta per quel componente; ad esempio `text`, `textimage`, `image`, `title`.

1. Ulteriori dettagli di configurazione dell’editor possono essere configurati utilizzando una `config` nodo contenente configurazioni e un ulteriore `plugin` per contenere i dettagli necessari della configurazione del plug-in.

   Di seguito è riportato un esempio di definizione delle proporzioni per il plug-in di ritaglio immagine del componente immagine. Tieni presente che a causa delle dimensioni dello schermo potenzialmente molto limitate, i rapporti di aspetto del ritaglio sono stati spostati nell’editor a schermo intero e possono essere visualizzati solo lì.

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
   >Si noti che nei rapporti di ritaglio AEM, come stabilito dal `ratio` proprietà, sono definiti come **altezza/larghezza**. Questo differisce dalla definizione tradizionale di larghezza/altezza e viene fatto per motivi di compatibilità con le versioni precedenti. Gli utenti che creano i file non noteranno alcuna differenza, purché sia stata definita la `name` chiaramente, poiché questo è ciò che viene visualizzato nell’interfaccia utente.

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

`aem-authoring-extension-inplace-editor` è un pacchetto di esempio che mostra come creare un nuovo editor locale in AEM.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-inplace-editor su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configurazione di più editor locali {#configuring-multiple-in-place-editors}

È possibile configurare un componente in modo che abbia più editor locali. Quando sono configurati più editor locali, puoi selezionare il contenuto appropriato e aprire l’editor appropriato. Consulta la [Configurazione di più editor locali](/help/sites-developing/multiple-inplace-editors.md) per ulteriori informazioni.

## Aggiungi un&#39;azione Nuova pagina {#add-a-new-page-action}

Per aggiungere una nuova azione di pagina alla barra degli strumenti della pagina, ad esempio **Torna a Sites** (console).

### Esempio di codice {#code-sample-3}

`aem-authoring-extension-header-backtosites` è un pacchetto di esempio che mostra come creare un’azione personalizzata della barra dell’intestazione per tornare alla console Sites.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-header-backtosites su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizzazione del flusso di lavoro Richiesta attivazione {#customizing-the-request-for-activation-workflow}

Il flusso di lavoro preconfigurato, **Richiesta di attivazione**:

* Appare automaticamente nel menu appropriato quando un autore di contenuti **non ha** i diritti di replica appropriati, ma **ha** iscrizione a DAM-Users e Authors.

* In caso contrario, non verrà visualizzato nulla, poiché i diritti di replica sono stati rimossi.

Per avere un comportamento personalizzato durante tale attivazione, puoi sovrapporre **Richiesta di attivazione** workflow:

1. In entrata `/apps` sovrapporre **Sites** procedura guidata:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Questo stesso sovrascriverà l’istanza comune di:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Aggiornare il [modello di flusso di lavoro](/help/sites-developing/workflows-models.md) e configurazioni/script correlati, in base alle esigenze.
1. Rimuovi il diritto al [ `replicate` azione](/help/sites-administering/security.md#actions) da tutti gli utenti appropriati per tutte le pagine rilevanti; affinché questo flusso di lavoro venga attivato come azione predefinita quando uno qualsiasi degli utenti tenta di pubblicare (o replicare) una pagina.
