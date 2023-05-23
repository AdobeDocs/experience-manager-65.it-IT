---
title: Personalizzazione dei modelli per i componenti del portale Forms
seo-title: Customizing templates for forms portal components
description: Visualizzare metadati personalizzati nell’elenco dei moduli
seo-description: Display custom metadata in form listing
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
feature: Forms Portal
exl-id: f889d996-77f7-4a4f-a637-da43fe1343c5
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# Personalizzazione dei modelli per i componenti del portale Forms{#customizing-templates-for-forms-portal-components}

## Prerequisiti {#prerequisites}

[Gestione dei metadati del modulo](../../forms/using/manage-form-metadata.md)

Conoscenza pratica di HTML e CSS

## Panoramica {#overview}

L’interfaccia utente di AEM Forms consente di aggiungere metadati a qualsiasi modulo. I metadati personalizzati possono migliorare l’esperienza utente nell’elencare e cercare i moduli dell’organizzazione.

Forms Portal consente di utilizzare metadati personalizzati negli elenchi dei moduli. Durante la creazione di modelli personalizzati per le risorse, puoi modificarne il layout e utilizzare metadati personalizzati con il set di stili CSS.

Per creare un modello personalizzato per vari componenti di Forms Portal, effettua le seguenti operazioni.

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
   ![Creazione di una sling:cartella](assets/1.png)

1. Crea un file template.html in questa cartella da utilizzare come modello personalizzato.
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

Forms Portal fornisce una sintassi per i segnaposto per visualizzare metadati personalizzati/OOTB. I segnaposto vengono compilati dopo la visualizzazione dei risultati di maschere, bozze o invii.

Per includere una voce ripetibile, configura il valore dell&#39;attributo **dati ripetibili** a **true**.

*Nell’esempio discusso, due elementi Div sono presenti nella parte superiore del modello personalizzato. La prima, con classe CSS &quot;__FP_boxes-container&quot;, funziona come elemento contenitore per i moduli elencati. La seconda, con la classe CSS &quot;__FP_boxes&quot;, è un modello per le entità di base, in questo caso un modulo. Il **dati ripetibili**l&#39;attributo presente nell&#39;elemento Div ha il valore **true**.*

Ogni segnaposto dispone di un set di metadati OOTB esclusivo. Per visualizzare i metadati personalizzati in una posizione specifica del modulo, aggiungere **${metadata_prop}, proprietà** sul posto.

*Nell’esempio, la proprietà dei metadati viene utilizzata in più istanze. Ad esempio, viene utilizzato in **descrizione**,**nome**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**, e **percorso**nel modo prescritto.*

## Metadati pronti all’uso {#out-of-the-box-metadata}

Diversi componenti di Forms Portal forniscono set esclusivi di metadati OOTB che è possibile utilizzare per l’elenco.

### Componente Ricerca ed elenco {#search-amp-lister-component}

* **Titolo:** Titolo del modulo
* **nome**: nome del modulo (per lo più lo stesso del titolo)
* **descrizione**: descrizione del modulo
* **formUrl**: URL per riprodurre il modulo come HTML
* **pdfUrl**: URL per riprodurre il modulo come PDF
* **assetType**: tipo di risorsa. I valori validi includono **Modulo**,**Modulo PDF**, **Stampa modulo**, e **Modulo adattivo**

* **htmlStyle** E **pdfStyle**: stile di visualizzazione rispettivamente delle icone HTML e PDF utilizzate per il rendering. I valori validi sono &quot;**__FP_display_none**&quot; o vuoto.

>[!NOTE]
>
>Ricordarsi di utilizzare la classe __FP_display_none nel foglio di stile personalizzato.

* **downloadUrl**: URL per scaricare una risorsa.

Supporto per la localizzazione, l&#39;ordinamento e l&#39;utilizzo delle proprietà di configurazione nell&#39;interfaccia utente (solo Search&amp;List):

1. **Supporto per la localizzazione**: per localizzare qualsiasi testo statico, utilizza l’attributo `${localize-YOUR_TEXT}` e rende disponibile il valore localizzato, se non esiste già.
   *Nell’esempio discusso, gli attributi `${localize-Apply}` e `${localize-Download}` vengono utilizzati per localizzare il testo Applica e Scarica.*

1. **Supporto per l’ordinamento**: fai clic sull’elemento HTML per ordinare i risultati della ricerca. Per implementare l’ordinamento in un layout compresso, aggiungi l’attributo &quot;data-sortKey&quot; nell’intestazione della tabella specifica. Inoltre, aggiungi il relativo valore come metadati per i quali desideri ordinare.
Ad esempio, per l’intestazione &quot;Title&quot; (Titolo) nella visualizzazione a griglia, il valore dell’intestazione &quot;data-sortKey&quot; è &quot;title&quot;. Fai clic sull’intestazione per ordinare i valori in una particolare colonna.

1. **Utilizzo delle proprietà di configurazione**: il componente Ricerca ed elenco dispone di diverse configurazioni che è possibile utilizzare nell’interfaccia utente. Ad esempio, per visualizzare il testo della descrizione HTML salvato nella finestra di dialogo per modifica, utilizzare `${config-htmlLinkText}` attributo. **Analogamente, per il testo della descrizione comandi di PDF, utilizzate** `${config-pdfLinkText}` attributo.

### Componente collegamento {#link-component}

* **Titolo:** Titolo del modulo
* **formUrl**: URL per riprodurre il modulo come HTML
* **destinazione**: attributo target del collegamento. I valori validi sono &quot;_blank&quot; e &quot;_self&quot;.
* **linkText**: didascalia del collegamento

### Componente Bozze e invii {#drafts-amp-submissions-component}

* **Percorso**: percorso del nodo dei metadati bozze/invii. Utilizzala con l’estensione .HTML come URL per aprire una bozza o un invio.
* **contextPath**: percorso contestuale dell’istanza AEM
* **firstLetter**: prima lettera (maiuscola) del titolo del modulo adattivo, che è stata salvata come bozza o inviata.
* **formName**: titolo del modulo adattivo salvato come bozza o inviato.
* **draftID**: ID della bozza elencata (da utilizzare solo nel modello per la sezione Bozza).
* **submitID**: ID per l’invio elencato (da utilizzare solo nel modello per la sezione Invio).
* **stato**: stato del modulo inviato. (Da utilizzare solo nel modello per la sezione Invio ).
* **descrizione**: descrizione del modulo adattivo associato alla bozza o all’invio.
* **diffTime**: differenza tra l’ora corrente e l’ultima azione di salvataggio della bozza. In alternativa, differenza tra l&#39;ora corrente e l&#39;ultima azione di invio per la sottomissione.
* **iconClass**: classe CSS utilizzata per visualizzare la prima lettera della bozza/invio. Forms Portal include le seguenti classi, che forniscono sfondi di diversi colori.
* **proprietario**: utente che ha creato la bozza/l’invio.
* **Oggi**: data di creazione della bozza o di presentazione in GG:MM:Formato AAAA.
* **TimeNow**: momento della creazione della bozza o della presentazione in HH:MM:Formato SS 24 ore

*Nota:*

1. Per l’opzione Elimina nella sezione Bozze del componente Bozze e invii, assegna alla classe CSS il nome &quot;__FP_deleteDraft&quot;. Inoltre, includi l’attributo &quot;draftID&quot; con il valore **${draftID}**, che è l’ID bozza della bozza corrispondente.

1. Durante la creazione di collegamenti per aprire bozze e invii, è possibile specificare **${path}.html** come valore del **href** per il tag di ancoraggio.

![Bozze e nodo Invio](assets/raw-image-with-index.png)

**A**. Elemento contenitore

**B.** Metadati &quot;path&quot; con una gerarchia fissa per ottenere la miniatura memorizzata per ciascun modulo.

**C.** Attributo dati ripetibili utilizzato per la sezione del modello per ciascun modulo

**D.** Per localizzare la stringa &quot;Apply&quot;

**E.** Utilizzo della proprietà di configurazione pdfLinkText

**F.** Utilizzo dei metadati &quot;pdfUrl&quot;

## Suggerimenti, trucchi e problemi noti {#tips-tricks-and-known-issues}

1. Non utilizzare virgolette singole (&#39;) in alcun modello personalizzato.
1. Per i metadati personalizzati, memorizza questa proprietà in **jcr:content/metadata** solo nodo. Se si archivia in qualsiasi altro luogo, Forms Portal non può visualizzare i metadati.
1. Assicurati che il nome di eventuali metadati personalizzati o esistenti non includa i due punti ( : ). In tal caso, non è possibile visualizzarlo nell’interfaccia utente.
1. **dati ripetibili** non ha alcun significato per un **Collegamento** componente. L’Adobe consiglia di evitare di utilizzare questa proprietà nel modello per un componente Collegamento.

## Articoli correlati

* [Abilitare i componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md)
* [Crea pagina portale moduli](/help/forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](/help/forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](/help/forms/using/draft-submission-component.md)
* [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale Forms](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md)
