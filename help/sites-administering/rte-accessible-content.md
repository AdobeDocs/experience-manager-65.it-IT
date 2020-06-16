---
title: Configurare l’editor Rich Text per creare pagine Web e siti con accesso facilitato.
description: Configurare l’editor Rich Text per creare pagine Web e siti con accesso facilitato.
contentOwner: AG
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# Configurare l’editor Rich Text per creare pagine Web e siti con accesso facilitato {#configure-rte-for-accessibility}

 Adobe Experience Manager supporta molte funzioni di accessibilità standard in conformità ai vari standard di accessibilità. Inoltre, gli sviluppatori possono personalizzare o estendere le funzionalità per la creazione di contenuti accessibili tramite  componenti Experience Manager che utilizzano l’editor Rich Text (RTE).

Durante la progettazione di pagine Web e l’aggiunta di contenuti alle pagine, gli sviluppatori di contenuti e gli autori possono utilizzare le funzioni dell’editor Rich Text per fornire informazioni relative all’accessibilità. Ad esempio, aggiungere informazioni strutturali attraverso titoli ed elementi di paragrafo.

Per configurare e personalizzare queste funzioni, [configurate i plug-in](#configure-the-plugin-features) RTE per il componente. Ad esempio, il `paraformat` plug-in consente di aggiungere altri elementi semantici a livello di blocco, inclusa l&#39;estensione del numero di livelli di intestazione supportati oltre il livello di base `H1`, `H2`e `H3` forniti per impostazione predefinita.

L’editor Rich Text è disponibile in diversi componenti per l’interfaccia Touch e per l’interfaccia utente Classic. Tuttavia, il componente principale da usare nell’editor Rich Text è il componente **Testo** disponibile per entrambe le interfacce. Le immagini seguenti mostrano l’editor Rich Text con una serie di plug-in abilitati, tra cui `paraformat`:

![Componente testo (RTE) in modalità a schermo intero nell’interfaccia touch.](assets/chlimage_1-206.png)

*Figura: Il componente Testo nell’interfaccia Touch.*

![Finestra di dialogo di modifica (RTE) del componente di testo nell’interfaccia classica.](assets/chlimage_1-207.png)

*Figura: Il componente Testo nell’interfaccia utente classica.*

Per le differenze tra le funzioni RTE disponibili nelle varie interfacce, vedere [Plugins e le relative funzioni](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configurare le funzioni del plug-in {#configure-the-plugin-features}

Per istruzioni complete sulla configurazione dell’editor Rich Text, consultate [Configurare la pagina Editor](/help/sites-administering/rich-text-editor.md) Rich Text. Vengono trattati tutti i problemi, compresi i passi chiave:

* [Plug-in e funzioni](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Posizioni](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)di configurazione.
* [Attivate un plug-in e configurate la proprietà](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)features.
* [Configurare altre funzionalità dell’editor Rich Text](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Configurando un plug-in all&#39;interno del `rtePlugins` sottoramo appropriato in CRXDE Lite, è possibile attivare tutte le funzioni o specifiche per quel plug-in.

![CRXDE Lite che mostra un esempio rtePlugin.](assets/chlimage_1-208.png)

### Esempio: specificare i formati di paragrafo disponibili nel campo di selezione dell&#39;editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocco semantico possono essere resi disponibili per la selezione tramite:

1. A seconda dell’editor Rich Text, determina e passa al percorso [di](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)configurazione.
1. [Attiva il campo](/help/sites-administering/rich-text-editor.md)di selezione Paragrafi; attivando [il plug-in](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati che si desidera rendere disponibili nel campo](/help/sites-administering/rich-text-editor.md)di selezione Paragrafi.
1. I formati di paragrafo sono quindi disponibili per l’autore del contenuto dai campi di selezione nell’editor Rich Text. È possibile accedervi:

   * Utilizzo dell’icona a forma di cuscino di paragrafo nell’interfaccia touch.
   * Utilizzo del campo **Formato** (selettore a comparsa) nell’interfaccia classica.

Con gli elementi strutturali disponibili nell’editor Rich Text tramite le opzioni del formato di paragrafo, AEM offre una buona base per lo sviluppo di contenuti accessibili. Gli autori dei contenuti non possono utilizzare l’editor Rich Text per formattare la dimensione del font o i colori o altri attributi correlati, impedendo la creazione di formattazione in linea. Devono invece selezionare gli elementi strutturali appropriati, ad esempio le intestazioni, e utilizzare gli stili globali scelti dall&#39;opzione Stili. In questo modo, gli utenti che sfogliano con i propri fogli di stile e con contenuti strutturati correttamente possono usufruire di una marcatura pulita e di opzioni maggiori.

## Utilizzo della funzione di modifica sorgente {#use-of-the-source-edit-feature}

In alcuni casi, gli autori dei contenuti dovranno esaminare e regolare il codice sorgente HTML creato mediante l’editor Rich Text. Ad esempio, un contenuto creato all’interno dell’editor Rich Text potrebbe richiedere una marcatura aggiuntiva per garantire la conformità a WCAG 2.0. Questa operazione può essere eseguita con l’opzione di modifica [](/help/sites-administering/rich-text-editor.md#aboutplugins) sorgente dell’editor Rich Text. Potete specificare la [`sourceedit` funzione sul `misctools` plug-in](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizzate la `sourceedit` funzione con attenzione. Gli errori di digitazione e/o le funzioni non supportate possono causare altri problemi.

## Supporto per più elementi e attributi HTML {#add-support-for-more-html-elements-and-attributes}

Per ampliare ulteriormente le funzioni di accessibilità di AEM, è possibile estendere i componenti esistenti in base all’editor Rich Text (come i componenti **Testo** e **Tabella** ) con elementi e attributi aggiuntivi.

La procedura seguente illustra come estendere il componente **Tabella** con un elemento **Didascalia** che fornisce informazioni su una tabella di dati per aiutare gli utenti della tecnologia:

### Esempio: aggiungere la didascalia alla finestra di dialogo Proprietà tabella {#example-adding-the-caption-to-the-table-properties-dialog}

Nella funzione di costruzione della didascalia, `TablePropertiesDialog`aggiungere un campo di testo aggiuntivo da utilizzare per la modifica della didascalia. Per gestire automaticamente il contenuto, `itemId` è necessario impostare `caption` (ovvero il nome dell’attributo DOM).

Nella **tabella**, impostate esplicitamente o rimuovete l’attributo dall’elemento DOM. Il valore viene passato dalla finestra di dialogo nell&#39; `config` oggetto. Tenete presente che gli attributi DOM devono essere impostati/rimossi utilizzando i `CQ.form.rte.Common` metodi corrispondenti ( `com` è un collegamento per `CQ.form.rte.Common`) per evitare i comuni errori con le implementazioni del browser.

>[!NOTE]
>
>Questa procedura è adatta solo all&#39;interfaccia utente classica.

### Esempio: creazione di HTML con accesso facilitato quando si utilizza l&#39;enfasi nel testo {#create-accessible-html-for-text}

L’editor Rich Text può utilizzare `strong` e `em` i tag al posto di `b` e `i`. Aggiungete il seguente nodo come nodo di pari livello ai `uiSettings` nodi e `rtePlugins` ai nodi della finestra di dialogo.

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### Istruzioni dettagliate {#step-by-step-instructions}

1. Avviare CRXDE Lite. Ad esempio: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copia:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   a:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Se non esistono già, potrebbe essere necessario creare delle cartelle intermedie.

1. Copia:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   a:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Aprite il file seguente per la modifica (aprite con un doppio clic):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. Nel `constructor` metodo, prima della lettura della riga:

   ```
   var dialogRef = this;
   ```

   Aggiungete il seguente codice:

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Aprite il file seguente:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. Aggiungete il codice seguente alla fine del `transferConfigToTable` metodo:

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. Salva le modifiche con **Salva tutto...**

>[!NOTE]
>
>Un campo di testo normale non è l&#39;unico tipo di input consentito per il valore dell&#39;elemento caption. È possibile utilizzare qualsiasi widget ExtJS, che fornisce il valore della didascalia tramite il relativo `getValue()` metodo.
>
>Per aggiungere funzionalità di modifica per altri elementi e attributi, accertatevi che:
>
>* La `itemId` proprietà per ciascun campo corrispondente viene impostata sul nome dell&#39;attributo DOM appropriato (`TablePropertiesDialog`).
>* L&#39;attributo viene impostato e/o rimosso in modo esplicito sull&#39;elemento DOM (`Table`).


>[!MORELIKETHIS]
>
>* [Guida rapida a WCAG 2.0](/help/managing/qg-wcag.md)
>* [Creare contenuto accessibile (conformità WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

