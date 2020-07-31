---
title: Personalizzazione dei modelli per i componenti del portale moduli
seo-title: Personalizzazione dei modelli per i componenti del portale moduli
description: Visualizzazione di metadati personalizzati nell'elenco dei moduli
seo-description: Visualizzazione di metadati personalizzati nell'elenco dei moduli
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# Personalizzazione dei modelli per i componenti del portale moduli{#customizing-templates-for-forms-portal-components}

## Prerequisiti {#prerequisites}

[Gestione dei metadati dei moduli](../../forms/using/manage-form-metadata.md)

Conoscenza di base di HTML e CSS

## Panoramica {#overview}

L&#39;interfaccia utente AEM Forms consente di aggiungere metadati a qualsiasi modulo. I metadati personalizzati possono migliorare l&#39;esperienza utente durante l&#39;elencazione e la ricerca di moduli all&#39;interno dell&#39;organizzazione.

Forms Portal consente di utilizzare i metadati personalizzati negli elenchi dei moduli. Durante la creazione di modelli personalizzati per le risorse, potete modificarne il layout e utilizzare i metadati personalizzati con il set di stili CSS.

Per creare un modello personalizzato per vari componenti di Forms Portal, effettuate le seguenti operazioni.

## Creating a custom template {#creating-a-nbsp-custom-template}

1. Creare un nodo sling:Folder in /apps

   Aggiungete una proprietà &quot;fpContentType&quot;. Specificate i valori appropriati per la proprietà a seconda del componente per il quale state definendo il modello personalizzato.

   * Componente Search &amp; Lister: &quot;/libs/fd/fp/formTemplate&quot;
   * Componente Bozze e invii:

      * Sezione Bozze: /libs/fd/fp/draftTemplate
      * Sezione Invii: /libs/fd/fp/submitTemplate
   * Collegamento componente: /libs/fd/fp/linkTemplate

   Aggiungete un titolo da visualizzare durante la selezione dei modelli di layout.

   >[!NOTE]
   >
   >Il titolo può essere diverso dal nome del nodo sling:Folder creato.

   Nell’immagine seguente è illustrata la configurazione del componente Ricerca e filtro.
   ![Creazione di una sling:Folder](assets/1.png)

1. Create un modello di file.html in questa cartella da usare come modello personalizzato.
1. Scrivete il modello personalizzato e utilizzate i metadati personalizzati come descritto di seguito.

## Esempio di lavoro {#working-example}

Di seguito è riportato un esempio di implementazione di un modello personalizzato in cui Forms Portal acquisisce un layout scheda Geometrixx personalizzato per il componente Ricerca e verifica.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## Specifiche tecniche per i modelli personalizzati {#technical-specifications-for-custom-templates}

Un modello personalizzato per qualsiasi componente di Forms Portal include voci ripetibili e non ripetibili. Le voci ripetibili sono entità di base per l&#39;elenco. Alcuni esempi di voci ripetibili sono i componenti Cerca e nascondi, Bozze e invii e Collegamento.

Forms Portal fornisce una sintassi per i segnaposto per la visualizzazione di metadati OOTB/personalizzati. I segnaposto vengono compilati dopo la visualizzazione dei risultati di moduli, bozze o invii.

Per includere una voce ripetibile, configurate il valore dell&#39;attributo **ripetibile** su **true**.

*Nell&#39;esempio illustrato, due elementi Div sono presenti nella parte superiore del modello personalizzato. La prima, con la classe CSS &quot;_FP_boxes-container&quot;, funziona come un elemento contenitore per i moduli elencati. Il secondo, con la classe CSS &quot;_FP_boxes&quot;, è un modello per le entità di base, in questo caso un modulo. L&#39;attributo **ripetibile**di dati presente nell&#39;elemento Div ha il valore **true**.*

Ogni segnaposto dispone di un set di metadati OOTB esclusivo. Per visualizzare i metadati personalizzati in una posizione specifica del modulo, aggiungere la proprietà **** ${metadata_prop} in tale posizione.

*Nell&#39;esempio, la proprietà metadata viene utilizzata in più istanze. Ad esempio, viene utilizzato in **descrizione**,**nome**,**formUrl**,**htmlStyle**,**pdfUrl**********, pdfStyle, percorso, come prescritto.*

## Metadati forniti {#out-of-the-box-metadata}

Diversi componenti di Forms Portal forniscono set esclusivi di metadati OOTB utilizzabili per l’elenco.

### Ricerca e filtro, componente {#search-amp-lister-component}

* **Titolo:** Titolo del modulo
* **name**: Nome del modulo (in genere corrisponde al titolo)
* **descrizione**: Descrizione del modulo
* **formUrl**: URL per il rendering del modulo come HTML
* **pdfUrl**: URL per il rendering del modulo come PDF
* **assetType**: Tipo di risorsa. I valori validi includono **Modulo**, Modulo **** PDF, Modulo **** stampa e Modulo **adattivo**

* **htmlStyle**&amp; **pdfStyle**: Stile di visualizzazione per le icone HTML e PDF utilizzate rispettivamente per il rendering. I valori validi sono &quot;**__FP_display_none**&quot; o blank.

>[!NOTE]
>
>Ricordare di utilizzare la classe __FP_display_none nel foglio di stile personalizzato.

* **downloadUrl**: URL per scaricare una risorsa.

Supporto per localizzazione, ordinamento e utilizzo delle proprietà di configurazione nell’interfaccia utente (solo ricerca e filtro):

1. **Supporto** per la localizzazione: Per localizzare qualsiasi testo statico, utilizzate l&#39;attributo `${localize-YOUR_TEXT}` e rendete disponibile il valore localizzato, se non esiste già.
   *Nell’esempio illustrato, gli attributi`${localize-Apply}`e`${localize-Download}`vengono utilizzati per localizzare il testo Applica e Scarica.*

1. **Supporto per l&#39;ordinamento**: Fate clic sull’elemento HTML per ordinare i risultati della ricerca. Per implementare l’ordinamento in un layout depositato, aggiungete l’attributo &quot;data-sortKey&quot; nella particolare intestazione della tabella. Inoltre, aggiungete il valore come metadati per i quali desiderate ordinare i dati.
Ad esempio, per l’intestazione &quot;Titolo&quot; nella vista griglia, il valore dell’intestazione &quot;data-sortKey&quot; è &quot;title&quot;. Fate clic sull’intestazione per ordinare i valori in una particolare colonna.

1. **Utilizzo delle proprietà** di configurazione: Il componente Ricerca e filtro presenta diverse configurazioni utilizzabili nell’interfaccia utente. Ad esempio, per visualizzare il testo HTML della descrizione comandi salvato tramite la finestra di dialogo di modifica, utilizzare l’ `${config-htmlLinkText}` attributo . **Analogamente, per il testo della descrizione comandi PDF, utilizzate l’attributo** `${config-pdfLinkText}` .

### Collegamento, componente {#link-component}

* **Titolo:** Titolo del modulo
* **formUrl**: URL per il rendering del modulo come HTML
* **target**: Attributo Target del collegamento. I valori validi sono &quot;_blank&quot; e &quot;_self.&quot;
* **linkText**: Didascalia collegamento

### Bozze e invii, componente {#drafts-amp-submissions-component}

* **Percorso**: Percorso del nodo di metadati bozza/invio. Utilizzatelo con l&#39;estensione .HTML come URL per aprire una bozza o per inviarla.
* **contextPath**: Percorso di contesto dell&#39;istanza AEM
* **firstLetter**: Prima lettera (maiuscola) del titolo del modulo adattivo, salvata come bozza o inviata.
* **formName**: Titolo del modulo adattivo, salvato come Bozza o inviato.
* **draftID**: ID per la bozza elencata (Utilizzate solo nel modello per la sezione Bozza).
* **submitID**: ID per l&#39;invio elencato (Usa solo nel modello per la sezione Invio).
* **status**: Stato del modulo inviato. Utilizzate solo nel modello per la sezione Invio.
* **descrizione**: Descrizione del modulo adattivo associato alla bozza o all&#39;invio.
* **diffTime**: Differenza tra l&#39;ora corrente e l&#39;ultima azione di salvataggio per la bozza. In alternativa, la differenza tra l&#39;ora corrente e l&#39;ultima azione di invio per l&#39;invio.
* **iconClass**: Classe CSS utilizzata per visualizzare la prima lettera della bozza/invio. Forms Portal include le classi seguenti, che forniscono sfondi colorati diversi.
* **proprietario**: Utente che ha creato la bozza/invio.
* **Oggi**: Data di creazione della bozza o di invio in formato GG:MM:AAAA.
* **Ora**: Ora di creazione della bozza o di invio in formato HH:MM:SS 24 ore

*Nota:*

1. Per l&#39;opzione di eliminazione nella sezione Bozze del componente Bozze e invii, assegnate alla classe CSS il nome &quot;_FP_deleteDraft&quot;. Inoltre, includete l&#39;attributo &quot;draftID&quot; con il valore **${draftID}**, che è l&#39;ID bozza della bozza corrispondente.

1. Durante la creazione di collegamenti per l&#39;apertura di bozze e invii, potete specificare **${path}.html** come valore dell&#39;attributo **href** per il tag di ancoraggio.

![Nodo Bozze e invio](assets/raw-image-with-index.png)

**A**. Elemento contenitore

**B.** metadati &quot;percorso&quot; con una gerarchia fissa per ottenere la miniatura memorizzata per ciascun modulo.

**C.** Attributo ripetibile ai dati utilizzato per la sezione del modello per ciascun modulo

**D.** Per localizzare la stringa &quot;Applica&quot;

**E.** Utilizzo della proprietà di configurazione pdfLinkText

**F.** Utilizzo dei metadati &quot;pdfUrl&quot;

## Suggerimenti, trucchi e problemi noti {#tips-tricks-and-known-issues}

1. Non utilizzate virgolette singole (&#39;) in alcun modello personalizzato.
1. Per i metadati personalizzati, memorizzate questa proprietà solo nel nodo **jcr:content/metadata** . Se li archiviate in qualsiasi altro luogo, Forms Portal non può visualizzare i metadati.
1. Accertatevi che il nome di eventuali metadati personalizzati o metadati esistenti non contenga due punti ( : ). In caso contrario, non è possibile visualizzarlo nell&#39;interfaccia utente.
1. **la ripetizione** dei dati non ha alcun significato per un componente **Link** .  Adobe consiglia di evitare di utilizzare questa proprietà nel modello per un componente Collegamento.

## Articoli correlati

* [Abilitare i componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina del portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare i moduli in una pagina Web utilizzando le API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzazione dell&#39;archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per l’integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale moduli](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)