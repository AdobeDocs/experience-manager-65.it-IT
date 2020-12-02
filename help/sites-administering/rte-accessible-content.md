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


# Configurare l&#39;editor Rich Text per creare pagine Web e siti con accesso facilitato {#configure-rte-for-accessibility}

Adobe Experience Manager supporta molte funzioni di accessibilità standard in conformità ai vari standard di accessibilità. Inoltre, gli sviluppatori possono personalizzare o estendere per fornire funzionalità utili alla creazione di contenuti accessibili utilizzando  componenti di Experience Manager che utilizzano l’editor Rich Text (RTE).

Durante la progettazione di pagine Web e l’aggiunta di contenuti alle pagine, gli sviluppatori di contenuti e gli autori possono utilizzare le funzioni dell’editor Rich Text per fornire informazioni relative all’accessibilità. Ad esempio, aggiungere informazioni strutturali attraverso titoli ed elementi di paragrafo.

Per configurare e personalizzare queste funzioni, [configurare i plug-in RTE](#configure-the-plugin-features) per il componente. Ad esempio, il plug-in `paraformat` consente di aggiungere elementi semantici a livello di blocco aggiuntivi, inclusa l&#39;estensione del numero di livelli di intestazione supportati oltre i livelli di base `H1`, `H2` e `H3` forniti per impostazione predefinita.

L’editor Rich Text è disponibile in diversi componenti per l’interfaccia Touch e per l’interfaccia utente Classic. Tuttavia, il componente principale da usare nell’editor Rich Text è il componente **Text** disponibile per entrambe le interfacce. Le immagini seguenti mostrano l&#39;editor Rich Text con una serie di plug-in abilitati, tra cui `paraformat`:

![Componente testo (RTE) in modalità a schermo intero nell’interfaccia touch.](assets/chlimage_1-206.png)

*Figura: Il componente Testo nell’interfaccia Touch.*

![Finestra di dialogo di modifica (RTE) del componente di testo nell’interfaccia classica.](assets/chlimage_1-207.png)

*Figura: Il componente Testo nell’interfaccia utente classica.*

Per le differenze tra le funzioni RTE disponibili nelle varie interfacce, vedere [Plugins e le relative funzionalità](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configurare le funzionalità del plug-in {#configure-the-plugin-features}

Per istruzioni complete sulla configurazione dell&#39;editor Rich Text, vedere [configurare la pagina Editor Rich Text](/help/sites-administering/rich-text-editor.md). Vengono trattati tutti i problemi, compresi i passi chiave:

* [Plug-in e funzioni](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Posizioni](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations) di configurazione.
* [Attivate un plug-in e configurate la proprietà](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins) features.
* [Configurare altre funzionalità dell’editor Rich Text](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Configurando un plug-in all&#39;interno del sottoramo `rtePlugins` appropriato nel CRXDE Lite, potete attivare tutte le funzioni o specifiche per quel plug-in.

![CRXDE Lite che mostra un esempio rtePlugin.](assets/chlimage_1-208.png)

### Esempio: specificare i formati di paragrafo disponibili nel campo di selezione dell&#39;editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocco semantico possono essere resi disponibili per la selezione tramite:

1. A seconda dell&#39;editor Rich Text, determinare e passare alla [posizione di configurazione](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Attiva il campo](/help/sites-administering/rich-text-editor.md) di selezione Paragrafi; attivando  [il plug-in](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati che si desidera rendere disponibili nel campo](/help/sites-administering/rich-text-editor.md) di selezione Paragrafi.
1. I formati di paragrafo sono quindi disponibili per l’autore del contenuto dai campi di selezione nell’editor Rich Text. È possibile accedervi:

   * Utilizzo dell’icona a forma di cuscino di paragrafo nell’interfaccia touch.
   * Utilizzo del campo **Formato** (selettore a comparsa) nell&#39;interfaccia classica.

Con gli elementi strutturali disponibili nell’editor Rich Text tramite le opzioni di formato del paragrafo, AEM fornisce una buona base per lo sviluppo di contenuto accessibile. Gli autori dei contenuti non possono utilizzare l’editor Rich Text per formattare la dimensione del font o i colori o altri attributi correlati, impedendo la creazione di formattazione in linea. Devono invece selezionare gli elementi strutturali appropriati, ad esempio le intestazioni, e utilizzare gli stili globali scelti dall&#39;opzione Stili. In questo modo, gli utenti che sfogliano con i propri fogli di stile e con contenuti strutturati correttamente possono usufruire di una marcatura pulita e di opzioni maggiori.

## Utilizzo della funzione di modifica sorgente {#use-of-the-source-edit-feature}

In alcuni casi, gli autori dei contenuti dovranno esaminare e regolare il codice sorgente HTML creato mediante l’editor Rich Text. Ad esempio, un contenuto creato all’interno dell’editor Rich Text potrebbe richiedere una marcatura aggiuntiva per garantire la conformità a WCAG 2.0. Questo può essere fatto con l&#39;opzione [modifica sorgente](/help/sites-administering/rich-text-editor.md#aboutplugins) dell&#39;editor Rich Text. È possibile specificare la funzione [ `sourceedit` sul plug-in `misctools`](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizzate attentamente la funzione `sourceedit`. Gli errori di digitazione e/o le funzioni non supportate possono causare altri problemi.

## Supporto per altri elementi e attributi HTML {#add-support-for-more-html-elements-and-attributes}

Per ampliare ulteriormente le funzioni di accessibilità di AEM, è possibile estendere i componenti esistenti in base all&#39;editor Rich Text (come i componenti **Text** e **Table**) con elementi e attributi aggiuntivi.

La procedura seguente illustra come estendere il componente **Table** con un elemento **Caption** che fornisce informazioni su una tabella di dati per aiutare gli utenti della tecnologia:

### Esempio: aggiungere la didascalia alla finestra di dialogo Proprietà tabella {#example-adding-the-caption-to-the-table-properties-dialog}

Nella funzione di costruzione della `TablePropertiesDialog`, aggiungere un campo di testo aggiuntivo utilizzato per modificare la didascalia. Tenere presente che `itemId` deve essere impostato su `caption` (ovvero il nome dell&#39;attributo DOM) per gestire automaticamente il contenuto.

In **Table**, impostare esplicitamente o rimuovere l&#39;attributo dall&#39;elemento DOM. Il valore viene passato dalla finestra di dialogo nell&#39;oggetto `config`. Gli attributi DOM devono essere impostati/rimossi utilizzando i metodi `CQ.form.rte.Common` corrispondenti ( `com` è una scelta rapida per `CQ.form.rte.Common`) per evitare le comuni insidie con le implementazioni del browser.

>[!NOTE]
>
>Questa procedura è adatta solo all&#39;interfaccia utente classica.

### Esempio: creare codice HTML accessibile quando si utilizza l&#39;enfasi nel testo {#create-accessible-html-for-text}

L&#39;editor Rich Text può utilizzare i tag `strong` e `em` al posto di `b` e `i`. Aggiungete il seguente nodo come elemento di pari livello ai nodi `uiSettings` e `rtePlugins` nella finestra di dialogo.

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

1. Inizia CRXDE Lite. Ad esempio: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
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

1. Nel metodo `constructor`, prima della lettura della riga:

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

1. Aggiungete il seguente codice alla fine del metodo `transferConfigToTable`:

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

1. Salvare le modifiche utilizzando **Salva tutto...**

>[!NOTE]
>
>Un campo di testo normale non è l&#39;unico tipo di input consentito per il valore dell&#39;elemento caption. È possibile utilizzare qualsiasi widget ExtJS, che fornisce il valore della didascalia tramite il metodo `getValue()`.
>
>Per aggiungere funzionalità di modifica per altri elementi e attributi, accertatevi che:
>
>* La proprietà `itemId` di ciascun campo corrispondente viene impostata sul nome dell&#39;attributo DOM appropriato (`TablePropertiesDialog`).
>* L&#39;attributo viene impostato e/o rimosso in modo esplicito sull&#39;elemento DOM (`Table`).


>[!MORELIKETHIS]
>
>* [Guida rapida a WCAG 2.0](/help/managing/qg-wcag.md)
>* [Creare contenuto accessibile (conformità WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

