---
title: Configura l’editor Rich Text per creare pagine web e siti accessibili.
description: Configura l’editor Rich Text per creare pagine web e siti accessibili.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Configurare l’editor Rich Text per creare pagine web e siti accessibili {#configure-rte-for-accessibility}

Adobe Experience Manager supporta molte funzioni di accessibilità standard in conformità ai vari standard di accessibilità. Inoltre, gli sviluppatori possono personalizzare o estendere per fornire funzionalità che facilitano la creazione di contenuti accessibili tramite componenti di Experience Manager che utilizzano l’Editor Rich Text.

Durante la progettazione di pagine web e l’aggiunta di contenuti alle pagine, gli sviluppatori di contenuti e gli autori possono utilizzare le funzioni dell’editor Rich Text per fornire informazioni relative all’accessibilità. Ad esempio, è possibile aggiungere informazioni strutturali tramite intestazioni ed elementi paragrafo.

Per configurare e personalizzare queste funzioni, [configurare i plug-in RTE](#configure-the-plugin-features) per il componente. Ad esempio, il `paraformat` il plug-in ti consente di aggiungere elementi semantici a livello di blocco aggiuntivi, inclusa l’estensione del numero di livelli di intestazione supportati oltre la base `H1`, `H2`e `H3` fornito per impostazione predefinita.

L’editor Rich Text è disponibile in diversi componenti per l’interfaccia utente touch e classica. Tuttavia, il componente principale per utilizzare l’editor Rich Text è la variabile **Testo** componente disponibile per entrambe le interfacce. Le immagini seguenti mostrano l’editor Rich Text con una serie di plug-in abilitati, tra cui `paraformat`:

![Componente testo (Editor Rich Text) in modalità a schermo intero nell’interfaccia touch.](assets/chlimage_1-206.png)

*Figura: Il componente Testo nell’interfaccia utente touch.*

![Finestra di dialogo Modifica (RTE) del componente testo nell’interfaccia classica.](assets/chlimage_1-207.png)

*Figura: Il componente Testo nell’interfaccia utente classica.*

Per le differenze tra le funzioni dell’editor Rich Text disponibili nelle varie interfacce, consulta [Plug-in e relative funzioni](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configurare le funzioni del plug-in {#configure-the-plugin-features}

Per istruzioni complete su come configurare l’editor Rich Text, consulta [configurare l’editor Rich Text](/help/sites-administering/rich-text-editor.md) pagina. Vengono trattati tutti i problemi, compresi i passaggi chiave:

* [Plug-in e funzioni](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Posizioni di configurazione](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Attivare un plug-in e configurare la proprietà funzionalità](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configurare altre funzionalità dell’editor Rich Text](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Configurando un plug-in all’interno del `rtePlugins` in CRXDE Lite è possibile attivare tutte le funzioni o specifiche del plug-in.

![CRXDE Lite mostra un esempio rtePlugin.](assets/chlimage_1-208.png)

### Esempio: specificare i formati paragrafo disponibili nel campo di selezione dell’editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocchi semantici possono essere messi a disposizione per la selezione:

1. A seconda dell’editor Rich Text, determina e naviga fino al [percorso di configurazione](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Attiva il campo di selezione Paragrafi](/help/sites-administering/rich-text-editor.md); da [attivazione del plug-in](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati che si desidera rendere disponibili nel campo di selezione Paragrafi](/help/sites-administering/rich-text-editor.md).
1. I formati di paragrafo sono quindi disponibili per l’autore del contenuto dai campi di selezione nell’editor Rich Text. Sono accessibili:

   * Utilizzo dell’icona a forma di pilotaggio di un paragrafo nell’interfaccia touch.
   * Utilizzo della **Formato** (selettore a comparsa) nell’interfaccia classica.

Con gli elementi strutturali disponibili nell’editor Rich Text tramite le opzioni del formato paragrafo, AEM fornisce una buona base per lo sviluppo di contenuti accessibili. Gli autori di contenuti non possono utilizzare l’editor Rich Text per formattare la dimensione del font o i colori o altri attributi correlati, impedendo la creazione di formattazione in linea. Devono invece selezionare gli elementi strutturali appropriati, ad esempio i titoli, e utilizzare gli stili globali selezionati dall’opzione Stili. In questo modo si garantisce un markup pulito, opzioni più ampie per gli utenti che navigano con i propri fogli di stile e contenuti strutturati correttamente.

## Utilizzo della funzione di modifica sorgente {#use-of-the-source-edit-feature}

In alcuni casi, gli autori di contenuti dovranno esaminare e regolare il codice sorgente HTML creato utilizzando l’editor Rich Text. Ad esempio, per garantire la conformità alle linee guida WCAG 2.0, un contenuto creato all’interno dell’editor Rich Text può richiedere tag aggiuntivi. Questo può essere fatto con [modifica sorgente](/help/sites-administering/rich-text-editor.md#aboutplugins) opzione dell’editor Rich Text. Puoi specificare la [ `sourceedit` sulla `misctools` plugin](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizza la `sourceedit` con attenzione. La digitazione di errori e/o funzioni non supportate può causare altri problemi.

## Aggiungi supporto per altri elementi e attributi di HTML {#add-support-for-more-html-elements-and-attributes}

Per estendere ulteriormente le funzioni di accessibilità di AEM, è possibile estendere i componenti esistenti in base all’editor Rich Text (come **Testo** e **Tabella** componenti) con elementi e attributi aggiuntivi.

La procedura seguente illustra come estendere il **Tabella** componente con un **Didascalia** elemento che fornisce informazioni su una tabella di dati agli utenti di tecnologie per l’accessibilità:

### Esempio: aggiungere la didascalia alla finestra di dialogo Proprietà tabella {#example-adding-the-caption-to-the-table-properties-dialog}

Nel costruttore del `TablePropertiesDialog`, aggiungi un campo di immissione testo aggiuntivo utilizzato per modificare la didascalia. Tieni presente che `itemId` deve essere impostato su `caption` (ovvero il nome dell’attributo DOM) per gestire automaticamente il contenuto.

In **Tabella**, imposta esplicitamente o rimuove l’attributo in/dall’elemento DOM. Il valore viene passato dalla finestra di dialogo nel `config` oggetto. Gli attributi DOM devono essere impostati/rimossi utilizzando il corrispondente `CQ.form.rte.Common` metodi ( `com` è una scorciatoia per `CQ.form.rte.Common`) per evitare problematiche comuni con le implementazioni del browser.

>[!NOTE]
>
>Questa procedura è adatta solo all&#39;interfaccia utente classica.

### Esempio: creare un HTML accessibile quando si utilizza l’enfasi nel testo {#create-accessible-html-for-text}

L’editor Rich Text può utilizzare `strong` e `em` al posto di `b` e `i`. Aggiungi il seguente nodo come nodo di pari livello al `uiSettings` e `rtePlugins` nella finestra di dialogo.

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

1. Avvia CRXDE Lite. Ad esempio: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copia:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   a:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Potrebbe essere necessario creare cartelle intermedie se non esistono già.

1. Copia:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   a:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Apri il file seguente per la modifica (apri con doppio clic):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. In `constructor` prima della lettura della riga:

   ```
   var dialogRef = this;
   ```

   Aggiungi il codice seguente:

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Apri il file seguente:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. Aggiungi il seguente codice alla fine del `transferConfigToTable` metodo:

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

1. Salva le modifiche utilizzando **Salva tutto...**

>[!NOTE]
>
>Un campo di testo normale non è l’unico tipo di input consentito per il valore dell’elemento didascalia. È possibile utilizzare qualsiasi widget ExtJS che fornisce il valore della didascalia attraverso la relativa `getValue()` metodo .
>
>Per aggiungere funzionalità di modifica per altri elementi e attributi, assicurati che:
>
>* La `itemId` per ogni campo corrispondente viene impostata sul nome dell&#39;attributo DOM appropriato (`TablePropertiesDialog`).
>* L’attributo viene impostato e/o rimosso esplicitamente sull’elemento DOM (`Table`).


>[!MORELIKETHIS]
>
>* [Guida rapida alle linee guida WCAG 2.0](/help/managing/qg-wcag.md)
>* [Creare contenuto accessibile (conformità WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

