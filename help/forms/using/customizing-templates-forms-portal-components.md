---
title: Personalizzazione dei modelli per i componenti di Forms Portal
description: Scopri in che modo l’interfaccia utente di AEM Forms consente agli utenti di aggiungere metadati ai moduli. I metadati personalizzati migliorano l’esperienza utente nell’elenco dei moduli e nella ricerca.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
feature: Forms Portal
exl-id: f889d996-77f7-4a4f-a637-da43fe1343c5
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---

# Personalizzazione dei modelli per i componenti di Forms Portal{#customizing-templates-for-forms-portal-components}

## Prerequisiti {#prerequisites}

[Gestione dei metadati del modulo](../../forms/using/manage-form-metadata.md)

Conoscenza pratica di HTML e CSS

## Panoramica {#overview}

L’interfaccia utente di AEM Forms consente di aggiungere metadati a qualsiasi modulo. I metadati personalizzati possono migliorare l’esperienza utente nell’elencare e cercare i moduli dell’organizzazione.

Forms Portal consente di utilizzare metadati personalizzati negli elenchi dei moduli. Durante la creazione di modelli personalizzati per le risorse, puoi modificarne il layout e utilizzare metadati personalizzati con il set di stili CSS.

Effettua le seguenti operazioni per creare un modello personalizzato per vari componenti di Forms Portal.

## Creazione di un modello personalizzato {#creating-a-nbsp-custom-template}

1. Creare un nodo sling:Folder in /apps

   Aggiungi una proprietà &quot;fpContentType&quot;. Specifica i valori appropriati per la proprietà a seconda del componente per il quale stai definendo il modello personalizzato.

   * Componente Ricerca ed elenco: &quot;/libs/fd/fp/formTemplate&quot;
   * Componente Bozze e invii:

      * Sezione bozze: /libs/fd/fp/draftTemplate
      * Sezione invii: /libs/fd/fp/submissionsTemplate

   * Componente collegamento: /libs/fd/fp/linkTemplate

   Aggiungi un titolo da visualizzare durante la selezione dei modelli di layout.

   >[!NOTE]
   >
   >Il titolo può essere diverso dal nome del nodo sling:Folder creato.

   L’immagine seguente illustra la configurazione del componente Ricerca ed elenco.
   ![Creazione di una cartella sling:Folder](assets/1.png)

1. Crea un file template.html in questa cartella affinché possa fungere da modello personalizzato.
1. Scrivi il modello personalizzato e utilizza i metadati personalizzati come descritto di seguito.

## Esempio di lavoro {#working-example}

Di seguito è riportato un esempio di implementazione di un modello personalizzato in cui Forms Portal acquisisce un layout personalizzato per la scheda Geometrixx per il componente Ricerca ed elenco.

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

Un modello personalizzato per qualsiasi componente di Forms Portal include voci ripetibili e non ripetibili. Le voci ripetibili sono entità di base per l&#39;inserimento nell&#39;elenco. Esempi di voci ripetibili sono Search &amp; Lister (Ricerca e elenco), Bozze e invii e Componenti link.

Forms Portal fornisce una sintassi per i segnaposto per visualizzare metadati personalizzati/preconfigurati. I segnaposto vengono compilati dopo la visualizzazione dei risultati di maschere, bozze o invii.

Per includere una voce ripetibile, configurare il valore dell&#39;attributo **dati-ripetibili** su **true**.

*Nell&#39;esempio discusso, due elementi Div sono presenti nella parte superiore del modello personalizzato. La prima, con classe CSS &quot;__FP_boxes-container&quot;, funziona come elemento contenitore per i moduli elencati. La seconda, con la classe CSS &quot;__FP_boxes&quot;, è un modello per le entità di base, in questo caso un modulo. L&#39;attributo **data-Repeable**presente nell&#39;elemento Div ha il valore **true**.*

Ogni segnaposto dispone di un set di metadati predefinito esclusivo. Per visualizzare i metadati personalizzati in una posizione specifica del modulo, aggiungere la proprietà **${metadata_prop}** nella posizione desiderata.

*Nell&#39;esempio, la proprietà dei metadati viene utilizzata in più istanze. Ad esempio, viene utilizzato in **description**,**name**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**e **path**nel modo prescritto.*

## Metadati pronti all’uso {#out-of-the-box-metadata}

Diversi componenti di Forms Portal forniscono set esclusivi di metadati predefiniti che è possibile utilizzare per l’elenco.

### Componente Ricerca ed elenco {#search-amp-lister-component}

* **Titolo:** Titolo del modulo
* **nome**: nome del modulo (per lo più è lo stesso del titolo)
* **descrizione**: descrizione del modulo
* **formUrl**: URL per il rendering del modulo come HTML
* **pdfUrl**: URL per il rendering del modulo come PDF
* **assetType**: tipo di risorsa. I valori validi includono **Modulo**, **Modulo PDF**, **Modulo di stampa** e **Modulo adattivo**

* **htmlStyle**&amp; **pdfStyle**: stile di visualizzazione rispettivamente per le icone HTML e PDF utilizzate per il rendering. I valori validi sono &quot;**__FP_display_none**&quot; o vuoti.

>[!NOTE]
>
>Ricordarsi di utilizzare la classe __FP_display_none nel foglio di stile personalizzato.

* **downloadUrl**: URL per scaricare una risorsa.

Supporto per la localizzazione, l&#39;ordinamento e l&#39;utilizzo delle proprietà di configurazione nell&#39;interfaccia utente (solo Search&amp;List):

1. **Supporto localizzazione**: per localizzare qualsiasi testo statico, utilizzare l&#39;attributo `${localize-YOUR_TEXT}` e rendere disponibile il valore localizzato, se non esiste già.
   *Nell&#39;esempio discusso, gli attributi `${localize-Apply}` e `${localize-Download}` vengono utilizzati per localizzare il testo Applica e Scarica.*

1. **Supporto per l&#39;ordinamento**: fare clic sull&#39;elemento HTML per ordinare i risultati della ricerca. Per implementare l’ordinamento in un layout di tabella, aggiungi l’attributo &quot;data-sortKey&quot; nell’intestazione della tabella specifica. Inoltre, aggiungi il relativo valore come metadati per i quali desideri ordinare.
Ad esempio, per l’intestazione &quot;Title&quot; (Titolo) nella visualizzazione a griglia, il valore dell’intestazione &quot;data-sortKey&quot; è &quot;title&quot;. Fai clic sull’intestazione per ordinare i valori in una particolare colonna.

1. **Utilizzo delle proprietà di configurazione**: il componente Search &amp; Lister dispone di diverse configurazioni che è possibile utilizzare nell&#39;interfaccia utente. Per visualizzare ad esempio il testo della descrizione comandi HTML salvato nella finestra di dialogo di modifica, utilizzare l&#39;attributo `${config-htmlLinkText}`. **Analogamente, per il testo della descrizione comandi di PDF, utilizzare l&#39;attributo** `${config-pdfLinkText}`.

### Componente collegamento {#link-component}

* **Titolo:** Titolo del modulo
* **formUrl**: URL per il rendering del modulo come HTML
* **target**: attributo target del collegamento. I valori validi sono &quot;_blank&quot; e &quot;_self&quot;.
* **linkText**: didascalia collegamento

### Componente Bozze e invii {#drafts-amp-submissions-component}

* **Percorso**: percorso del nodo metadati bozze/invii. Utilizzalo con l’estensione .HTML come URL per aprire una bozza o inviare.
* **contextPath**: percorso contestuale dell&#39;istanza AEM
* **primaLettera**: prima lettera (maiuscola) del titolo del modulo adattivo, salvata come bozza o inviata.
* **formName**: titolo del modulo adattivo, salvato come bozza o inviato.
* **draftID**: ID per la bozza elencata (da utilizzare solo nel modello per la sezione Bozza).
* **submitID**: ID per l&#39;invio elencato (da utilizzare solo nel modello per la sezione Invio).
* **stato**: stato del modulo inviato. (Da utilizzare solo nel modello per la sezione Invio ).
* **descrizione**: descrizione del modulo adattivo associato alla bozza o all&#39;invio.
* **diffTime**: differenza tra l&#39;ora corrente e l&#39;ultima azione di salvataggio per la bozza. In alternativa, la differenza tra l&#39;ora corrente e l&#39;ultima azione inviata per l&#39;invio.
* **iconClass**: classe CSS utilizzata per visualizzare la prima lettera della bozza/invio. Forms Portal include le seguenti classi, che forniscono sfondi di diversi colori.
* **proprietario**: utente che ha creato la bozza/invio.
* **Oggi**: data di creazione della bozza o di invio nel formato `DD:MM:YYYY`.
* **Ora**: ora di creazione della bozza o di invio nel formato `HH:MM:SS` di 24 ore

*Nota:*

1. Per l’opzione Elimina nella sezione Bozze del componente Bozze e invii, assegna alla classe CSS il nome &quot;__FP_deleteDraft&quot;. Inoltre, includi l&#39;attributo &quot;draftID&quot; con il valore **${draftID}**, che è l&#39;ID bozza della bozza corrispondente.

1. Durante la creazione di collegamenti per aprire bozze e invii, è possibile specificare **${path}.html** come valore dell&#39;attributo **href** per il tag di ancoraggio.

![Bozze e nodo di invio](assets/raw-image-with-index.png)

**A**. Elemento contenitore

Metadati &quot;path&quot; di **B.** con una gerarchia fissa per ottenere la miniatura archiviata per ciascun modulo.

Attributo **C.** Data-Repeable utilizzato per la sezione del modello per ogni modulo

**D.** Localizzare la stringa &quot;Apply&quot;

**E.** Utilizzo della proprietà di configurazione pdfLinkText

**F.** Utilizzo dei metadati &quot;pdfUrl&quot;

## Suggerimenti, trucchi e problemi noti {#tips-tricks-and-known-issues}

1. Non utilizzare virgolette singole (&#39;) in alcun modello personalizzato.
1. Per i metadati personalizzati, memorizzare questa proprietà solo nel nodo **jcr:content/metadata**. Se viene archiviato in un&#39;altra posizione, Forms Portal non può visualizzare i metadati.
1. Assicurati che il nome di eventuali metadati personalizzati o esistenti non includa i due punti ( : ). In tal caso, non è possibile visualizzarlo nell’interfaccia utente.
1. **dati-ripetibili** non ha alcun significato per un componente **Link**. L’Adobe consiglia di evitare di utilizzare questa proprietà nel modello per un componente Collegamento.

## Articoli correlati

* [Abilitare i componenti di Forms Portal](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina Crea portale Forms](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per l’integrazione del componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti di Forms Portal](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
