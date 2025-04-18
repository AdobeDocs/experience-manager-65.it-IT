---
title: Aggiunta di azioni personalizzate agli elementi del lister del modulo
description: Gli sviluppatori di moduli possono aggiungere ulteriori azioni all'elenco dei moduli nella pagina del portale moduli. Per impostazione predefinita, l’elenco dei moduli ti consente di accedere al modulo, compilarlo e inviarlo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Aggiunta di azioni personalizzate agli elementi del lister del modulo{#adding-custom-action-on-form-lister-items}

In AEM Forms puoi creare una pagina portale in cui sono elencati i moduli disponibili. Per impostazione predefinita, è possibile cercare ed elencare i moduli in una pagina del portale. È possibile aprire i moduli per la compilazione e l&#39;invio delle informazioni. Per i moduli elencati in una pagina del portale vengono fornite solo le azioni di rendering predefinite. Per ulteriori informazioni sulle azioni disponibili in una pagina del portale, vedere [Creazione di una pagina del portale moduli](../../forms/using/creating-form-portal-page.md).

È possibile aggiungere altre opzioni alla pagina del portale. Queste opzioni o azioni possono essere personalizzate personalizzando il modello del portale dei moduli.

In questo articolo viene illustrato come creare un pulsante per inviare il collegamento di un modulo direttamente da una pagina del portale moduli. Questa personalizzazione richiede l’aggiornamento del modello per il componente Ricerca ed elenco.

Il codice necessario per aggiungere l’azione al modello è disponibile di seguito. L&#39;attributo `onclick` nel frammento di codice dispone di uno script per inviare un collegamento di un modulo tramite e-mail.

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

Puoi aggiungere azioni simili nel modello personalizzato. Per definire una funzione di JavaScript, aggiungi la funzione in uno script a livello di pagina e collegala all’elemento HTML richiesto. Nell&#39;esempio precedente, l&#39;espressione `onclick` è la funzione collegata.

Dopo aver apportato le modifiche al modello, la pagina del portale di esempio contiene un pulsante per inviare il collegamento del modulo tramite e-mail, come illustrato di seguito.

![e-mail](assets/email.png)
