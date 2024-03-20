---
title: Configurare Editor Rich Text per creare pagine Web e siti accessibili.
description: Configurare Editor Rich Text per creare pagine Web e siti accessibili.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Configurare l’editor Rich Text per creare pagine web e siti accessibili {#configure-rte-for-accessibility}

Adobe Experience Manager supporta molte funzioni di accessibilità standard in conformità con vari standard di accessibilità. Inoltre, gli sviluppatori possono personalizzare o estendere per fornire funzionalità che consentono di creare contenuto accessibile utilizzando componenti di Experience Manager che utilizzano l’editor Rich Text (RTE).

Durante la progettazione di pagine web e l’aggiunta di contenuto alle pagine, gli sviluppatori e gli autori di contenuti possono utilizzare le funzioni dell’editor Rich Text per fornire informazioni relative all’accessibilità. Ad esempio, aggiungi informazioni strutturali tramite intestazioni ed elementi di paragrafo.

Per configurare e personalizzare queste funzioni: [configurare i plug-in dell’editor Rich Text](#configure-the-plugin-features) per il componente. Ad esempio, il `paraformat` Il plug-in consente di aggiungere ulteriori elementi semantici a livello di blocco, inclusa l’estensione del numero di livelli di intestazione supportati oltre il `H1`, `H2`, e `H3` fornite per impostazione predefinita.

L’editor Rich Text è disponibile in diversi componenti per l’interfaccia touch e l’interfaccia utente classica. Tuttavia, il componente principale per utilizzare l’editor Rich Text è **Testo** componente disponibile per entrambe le interfacce. Le immagini seguenti mostrano l’editor Rich Text con una serie di plug-in abilitati, tra cui `paraformat`:

![Componente testo (RTE) in modalità a tutto schermo nell’interfaccia touch.](assets/chlimage_1-206.png)

*Figura: Il componente Testo nell’interfaccia utente touch.*

![Finestra di dialogo per modifica (Editor Rich Text) del componente testo nell’interfaccia classica.](assets/chlimage_1-207.png)

*Figura: Il componente Testo nell’interfaccia utente classica.*

Per informazioni sulle differenze tra le funzioni RTE disponibili nelle varie interfacce, vedere [Plug-in e relative funzioni](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configurare le funzioni del plug-in {#configure-the-plugin-features}

Per istruzioni complete sulla configurazione dell’editor Rich Text, consulta [configurare l’editor Rich Text](/help/sites-administering/rich-text-editor.md) pagina. In questo documento vengono trattati tutti i problemi, incluse le fasi principali:

* [Plug-in e funzioni](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Posizioni di configurazione](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Attiva un plug-in e configura la proprietà features](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configurare altre funzionalità dell’editor Rich Text](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Configurando un plug-in all’interno del `rtePlugins` sub-branch in CRXDE Liti, puoi attivare tutte o funzionalità specifiche per quel plug-in.

![CRXDE Liti che mostra un esempio di rtePlugin.](assets/chlimage_1-208.png)

### Esempio: specificare i formati di paragrafo disponibili nel campo di selezione dell’Editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocchi semantici possono essere resi disponibili per la selezione:

1. A seconda dell’editor Rich Text, determina e accedi al [percorso di configurazione](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Abilita il campo di selezione Paragrafi](/help/sites-administering/rich-text-editor.md); per [attivazione del plug-in](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati da rendere disponibili nel campo di selezione Paragrafi](/help/sites-administering/rich-text-editor.md).
1. I formati di paragrafo sono quindi disponibili per l’autore di contenuto dai campi di selezione nell’editor Rich Text. È possibile accedervi:

   * Utilizzo dell’icona del cursore paragrafo nell’interfaccia utente touch.
   * Utilizzo di **Formato** (selettore popup) nell’interfaccia classica.

Con gli elementi strutturali disponibili nell’editor Rich Text attraverso le opzioni di formato dei paragrafi, l’AEM fornisce una buona base per lo sviluppo di contenuti accessibili. Gli autori dei contenuti non possono utilizzare l’editor Rich Text per formattare le dimensioni o i colori dei caratteri o altri attributi correlati, impedendo la creazione di formattazione in linea. Devono invece selezionare gli elementi strutturali appropriati, ad esempio le intestazioni, e utilizzare gli stili globali scelti dall’opzione Stili. In questo modo si garantisce un markup più ordinato, maggiori opzioni per gli utenti che navigano con i propri fogli di stile e contenuti correttamente strutturati.

## Utilizzo della funzione di modifica dell&#39;origine {#use-of-the-source-edit-feature}

In alcuni casi, gli autori di contenuti dovranno esaminare e regolare il codice sorgente HTML creato con l’editor Rich Text. Ad esempio, un contenuto creato nell’editor Rich Text può richiedere un markup aggiuntivo per garantire la conformità a WCAG 2.0. Questa operazione può essere eseguita con [modifica origine](/help/sites-administering/rich-text-editor.md#aboutplugins) dell&#39;editor Rich Text. È possibile specificare [`sourceedit` funzionalità in `misctools` plugin](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizza il `sourceedit` con attenzione. Errori di digitazione e/o funzioni non supportate possono introdurre ulteriori problemi.

## Aggiungi supporto per altri elementi e attributi di HTML {#add-support-for-more-html-elements-and-attributes}

Per estendere ulteriormente le funzioni di accessibilità dell’AEM, è possibile estendere i componenti esistenti in base all’editor Rich Text (come **Testo** e **Tabella** componenti) con elementi e attributi aggiuntivi.

La procedura seguente illustra come estendere **Tabella** componente con **Didascalia** elemento che fornisce informazioni su una tabella dati agli utenti di tecnologie per l’accessibilità:

### Esempio: aggiungere la didascalia alla finestra di dialogo Proprietà tabella {#example-adding-the-caption-to-the-table-properties-dialog}

Nel costruttore del `TablePropertiesDialog`, aggiungi un campo di immissione testo aggiuntivo utilizzato per modificare la didascalia. Tieni presente che `itemId` deve essere impostato su `caption` (ovvero il nome dell’attributo DOM) per gestirne automaticamente il contenuto.

In entrata **Tabella**, imposta o rimuove esplicitamente l&#39;attributo dall&#39;elemento DOM o viceversa. Il valore viene passato dalla finestra di dialogo nella sezione `config` oggetto. Gli attributi DOM devono essere impostati/rimossi utilizzando il `CQ.form.rte.Common` metodi ( `com` è un collegamento per `CQ.form.rte.Common`) per evitare problemi comuni con le implementazioni del browser.

>[!NOTE]
>
>Questa procedura è adatta solo per l’interfaccia utente classica.

### Esempio: creare HTML accessibili quando si utilizza l’enfasi nel testo {#create-accessible-html-for-text}

L’editor Rich Text può utilizzare `strong` e `em` tag al posto di `b` e `i`. Aggiungi il seguente nodo come elemento di pari livello al `uiSettings` e `rtePlugins` nella finestra di dialogo.

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

1. Avvia CRXDE Liti. Ad esempio: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copia:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   a:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Se non esistono già, potrebbe essere necessario creare cartelle intermedie.

1. Copia:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   a:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Apri il seguente file per la modifica (apri con doppio clic):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. In `constructor` metodo, prima della lettura della riga:

   ```
   var dialogRef = this;
   ```

   Aggiungi il seguente codice:

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Apri il seguente file:

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

1. Salva le modifiche tramite **Salva tutto...**

>[!NOTE]
>
>Un campo di testo normale non è l&#39;unico tipo di input consentito per il valore dell&#39;elemento caption. Puoi utilizzare qualsiasi widget ExtJS, che fornisce il valore della didascalia attraverso i `getValue()` metodo.
>
>Per aggiungere funzionalità di modifica per ulteriori elementi e attributi aggiuntivi, assicurati che:
>
>* Il `itemId` per ogni campo corrispondente viene impostata sul nome dell&#39;attributo DOM appropriato (`TablePropertiesDialog`).
>* L&#39;attributo viene impostato e/o rimosso esplicitamente dall&#39;elemento DOM (`Table`).

>[!MORELIKETHIS]
>
>* [Guida rapida alle linee guida WCAG 2.0](/help/managing/qg-wcag.md)
>* [Creare contenuti accessibili (conformità WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)
