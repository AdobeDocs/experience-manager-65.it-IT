---
title: Aggiunta di azioni personalizzate agli elementi del lister del modulo
seo-title: Adding custom action on form lister items
description: Gli sviluppatori di moduli possono aggiungere ulteriori azioni all'elenco dei moduli nella pagina del portale moduli. Per impostazione predefinita, l’elenco dei moduli consente di accedere al modulo, compilarlo e inviarlo.
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing allows you to access the form, fill it, and submit it.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Aggiunta di azioni personalizzate agli elementi del lister del modulo{#adding-custom-action-on-form-lister-items}

In AEM Forms puoi creare una pagina portale in cui sono elencati i moduli disponibili. Per impostazione predefinita, è possibile cercare ed elencare i moduli in una pagina del portale. È possibile aprire i moduli per la compilazione e l&#39;invio delle informazioni. Per i moduli elencati in una pagina del portale vengono fornite solo le azioni di rendering predefinite. Per ulteriori informazioni sulle azioni disponibili in una pagina del portale, consulta [Creazione di una pagina del portale dei moduli](../../forms/using/creating-form-portal-page.md).

È possibile aggiungere altre opzioni alla pagina del portale. Queste opzioni o azioni possono essere personalizzate personalizzando il modello del portale dei moduli.

In questo articolo viene illustrato come creare un pulsante per inviare il collegamento di un modulo direttamente da una pagina del portale moduli. Questa personalizzazione richiede l’aggiornamento del modello per il componente Ricerca ed elenco.

Il codice necessario per aggiungere l’azione al modello è disponibile di seguito. Il `onclick` l&#39;attributo nel frammento di codice dispone di uno script per inviare un collegamento di un modulo tramite e-mail.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

Puoi aggiungere azioni simili nel modello personalizzato. Per definire una funzione JavaScript, aggiungi la funzione a uno script a livello di pagina e collegala all’elemento HTML richiesto. Nell’esempio precedente, il `onclick` expression è la funzione collegata.

Dopo aver apportato le modifiche al modello, la pagina del portale di esempio contiene un pulsante per inviare il collegamento del modulo tramite e-mail, come illustrato di seguito.

![email](assets/email.png)
