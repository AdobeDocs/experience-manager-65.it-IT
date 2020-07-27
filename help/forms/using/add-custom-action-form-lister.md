---
title: Aggiunta di un'azione personalizzata agli elementi del modulo
seo-title: Aggiunta di un'azione personalizzata agli elementi del modulo
description: Gli sviluppatori di moduli possono aggiungere ulteriori azioni all'elenco dei moduli nella pagina del portale dei moduli. Per impostazione predefinita, l'elenco dei moduli consente di accedere al modulo, compilarlo e inviarlo.
seo-description: Gli sviluppatori di moduli possono aggiungere ulteriori azioni all'elenco dei moduli nella pagina del portale dei moduli. Per impostazione predefinita, l'elenco dei moduli consente di accedere al modulo, compilarlo e inviarlo.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Aggiunta di un&#39;azione personalizzata agli elementi del modulo{#adding-custom-action-on-form-lister-items}

In AEM Forms, è possibile creare una pagina del portale in cui sono elencati i moduli disponibili. Per impostazione predefinita, è possibile cercare ed elencare i moduli in una pagina del portale. È possibile aprire i moduli da compilare e inviare le informazioni. Solo le azioni di rendering vengono fornite al di fuori della casella per i moduli elencati in una pagina del portale. Per ulteriori informazioni sulle azioni disponibili in una pagina del portale, vedere [Creazione di una pagina](../../forms/using/creating-form-portal-page.md)del portale dei moduli.

È possibile aggiungere altre opzioni alla pagina del portale. Queste opzioni o azioni possono essere personalizzate personalizzando il modello del portale dei moduli.

In questo articolo viene illustrato come creare un pulsante per inviare il collegamento di un modulo, direttamente dalla pagina del portale dei moduli. Questa personalizzazione richiede l’aggiornamento del modello per il componente Ricerca e filtro.

Il codice richiesto per aggiungere l’azione al modello è disponibile di seguito. L&#39; `onclick` attributo nello snippet di codice ha uno script per inviare un collegamento di un modulo tramite e-mail.

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

Potete aggiungere azioni simili nel modello personalizzato. Per definire una funzione JavaScript, aggiungere la funzione su uno script a livello di pagina e collegarla con l&#39;elemento HTML richiesto. Nell&#39;esempio precedente, l&#39; `onclick` espressione è la funzione collegata.

Dopo aver apportato le modifiche al modello, la pagina del portale di esempio contiene un pulsante per inviare il collegamento del modulo tramite e-mail, come mostrato di seguito.

![email](assets/email.png)

