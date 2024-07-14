---
title: Configurare Editor Rich Text per creare pagine Web e siti accessibili.
description: Configurare Editor Rich Text per creare pagine Web e siti accessibili.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Configurare l’editor Rich Text per creare pagine web e siti accessibili {#configure-rte-for-accessibility}

Adobe Experience Manager supporta molte funzioni di accessibilità standard in conformità con vari standard di accessibilità. Inoltre, gli sviluppatori possono personalizzare o estendere per fornire funzionalità che consentono di creare contenuto accessibile utilizzando componenti di Experience Manager che utilizzano l’editor Rich Text (RTE).

Durante la progettazione di pagine web e l’aggiunta di contenuto alle pagine, gli sviluppatori e gli autori di contenuti possono utilizzare le funzioni dell’editor Rich Text per fornire informazioni relative all’accessibilità. Ad esempio, aggiungi informazioni strutturali tramite intestazioni ed elementi di paragrafo.

Per configurare e personalizzare queste funzionalità, [configurare i plug-in dell&#39;editor Rich Text](#configure-the-plugin-features) per il componente. Ad esempio, il plug-in `paraformat` ti consente di aggiungere elementi semantici a livello di blocco aggiuntivi, inclusa l&#39;estensione del numero di livelli di intestazione supportati oltre i `H1`, `H2` e `H3` di base forniti per impostazione predefinita.

L’editor Rich Text è disponibile in diversi componenti per l’interfaccia touch e l’interfaccia utente classica. Tuttavia, il componente principale per utilizzare l&#39;editor Rich Text è il componente **Testo** disponibile per entrambe le interfacce. Le immagini seguenti mostrano l&#39;editor Rich Text con una serie di plug-in abilitati, incluso `paraformat`:

![Componente testo (RTE) in modalità a schermo intero nell&#39;interfaccia touch.](assets/chlimage_1-206.png)

*Figura: il componente Testo nell&#39;interfaccia utente touch.*

![Finestra di dialogo per modifica (Editor Rich Text) del componente testo nell&#39;interfaccia classica.](assets/chlimage_1-207.png)

*Figura: componente Testo nell&#39;interfaccia utente classica.*

Per informazioni sulle differenze tra le funzionalità dell&#39;editor Rich Text disponibili nelle varie interfacce, vedere [Plug-in e relative funzionalità](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configurare le funzioni del plug-in {#configure-the-plugin-features}

Per istruzioni complete sulla configurazione dell&#39;editor Rich Text, vedere [configurare la pagina Editor Rich Text](/help/sites-administering/rich-text-editor.md). In questo documento vengono trattati tutti i problemi, incluse le fasi principali:

* [Plug-in e funzionalità](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Percorsi di configurazione](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Attiva un plug-in e configura la proprietà delle funzionalità](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configurare altre funzionalità dell&#39;editor Rich Text](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Configurando un plug-in nel ramo secondario `rtePlugins` appropriato in CRXDE Lite, puoi attivare tutte o alcune funzionalità specifiche per quel plug-in.

![CRXDE Liti che mostra un rtePlugin di esempio.](assets/chlimage_1-208.png)

### Esempio: specificare i formati di paragrafo disponibili nel campo di selezione dell’Editor Rich Text {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nuovi formati di blocchi semantici possono essere resi disponibili per la selezione:

1. A seconda dell&#39;editor Rich Text, determinare e passare al [percorso di configurazione](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Abilitare il campo di selezione Paragraphs](/help/sites-administering/rich-text-editor.md); [attivando il plug-in](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Specificare i formati da rendere disponibili nel campo di selezione Paragrafi](/help/sites-administering/rich-text-editor.md).
1. I formati di paragrafo sono quindi disponibili per l’autore di contenuto dai campi di selezione nell’editor Rich Text. È possibile accedervi:

   * Utilizzo dell’icona del cursore paragrafo nell’interfaccia utente touch.
   * Utilizzo del campo **Formato** (selettore popup) nell&#39;interfaccia classica.

Con gli elementi strutturali disponibili nell’editor Rich Text attraverso le opzioni di formato dei paragrafi, l’AEM fornisce una buona base per lo sviluppo di contenuti accessibili. Gli autori dei contenuti non possono utilizzare l’editor Rich Text per formattare le dimensioni o i colori dei caratteri o altri attributi correlati, impedendo la creazione di formattazione in linea. Devono invece selezionare gli elementi strutturali appropriati, ad esempio le intestazioni, e utilizzare gli stili globali scelti dall’opzione Stili. In questo modo si garantisce un markup più ordinato, maggiori opzioni per gli utenti che navigano con i propri fogli di stile e contenuti correttamente strutturati.

## Utilizzo della funzione di modifica dell&#39;origine {#use-of-the-source-edit-feature}

In alcuni casi, gli autori di contenuti dovranno esaminare e regolare il codice sorgente HTML creato con l’editor Rich Text. Ad esempio, un contenuto creato nell’editor Rich Text può richiedere un markup aggiuntivo per garantire la conformità a WCAG 2.0. Questa operazione può essere eseguita con l&#39;opzione [modifica origine](/help/sites-administering/rich-text-editor.md#aboutplugins) dell&#39;editor Rich Text. È possibile specificare la funzionalità [`sourceedit` nel plug-in `misctools`](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilizza la funzione `sourceedit` con attenzione. Errori di digitazione e/o funzioni non supportate possono introdurre ulteriori problemi.

## Aggiungi supporto per altri elementi e attributi di HTML {#add-support-for-more-html-elements-and-attributes}

Per estendere ulteriormente le funzioni di accessibilità di AEM, è possibile estendere i componenti esistenti basati sull&#39;editor Rich Text (ad esempio i componenti **Text** e **Table**) con elementi e attributi aggiuntivi.

La procedura seguente illustra come estendere il componente **Table** con un elemento **Caption** che fornisce informazioni su una tabella dati agli utenti di tecnologie per l&#39;accessibilità:

### Esempio: aggiungere la didascalia alla finestra di dialogo Proprietà tabella {#example-adding-the-caption-to-the-table-properties-dialog}

Nel costruttore di `TablePropertiesDialog`, aggiungere un campo di immissione testo aggiuntivo utilizzato per modificare la didascalia. `itemId` deve essere impostato su `caption` (ovvero il nome dell&#39;attributo DOM) per gestire automaticamente il contenuto.

In **Tabella**, impostare o rimuovere esplicitamente l&#39;attributo da/verso l&#39;elemento DOM. Valore passato dalla finestra di dialogo nell&#39;oggetto `config`. Si noti che gli attributi DOM devono essere impostati/rimossi utilizzando i metodi `CQ.form.rte.Common` corrispondenti ( `com` è un collegamento per `CQ.form.rte.Common`) per evitare problemi comuni con le implementazioni del browser.

>[!NOTE]
>
>Questa procedura è adatta solo per l’interfaccia utente classica.

### Esempio: creare HTML accessibili quando si utilizza l’enfasi nel testo {#create-accessible-html-for-text}

L&#39;editor Rich Text può utilizzare `strong` e `em` tag invece di `b` e `i`. Aggiungere il nodo seguente come nodo di pari livello ai nodi `uiSettings` e `rtePlugins` nella finestra di dialogo.

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

1. Avvia CRXDE Lite. Esempio: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
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

1. Nel metodo `constructor`, prima della lettura della riga:

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

1. Aggiungere il codice seguente alla fine del metodo `transferConfigToTable`:

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
>Un campo di testo normale non è l&#39;unico tipo di input consentito per il valore dell&#39;elemento caption. È possibile utilizzare qualsiasi widget ExtJS che fornisce il valore della didascalia tramite il relativo metodo `getValue()`.
>
>Per aggiungere funzionalità di modifica per ulteriori elementi e attributi aggiuntivi, assicurati che:
>
>* La proprietà `itemId` per ogni campo corrispondente è impostata sul nome dell&#39;attributo DOM appropriato (`TablePropertiesDialog`).
>* Attributo impostato e/o rimosso in modo esplicito sull&#39;elemento DOM (`Table`).

>[!MORELIKETHIS]
>
>* [Guida rapida a WCAG 2.0](/help/managing/qg-wcag.md)
>* [Crea contenuto accessibile (conformità WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)
