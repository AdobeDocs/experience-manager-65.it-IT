---
title: Aggiunta di azioni personalizzate agli elementi dell’elenco del modulo
description: Gli sviluppatori di moduli possono aggiungere ulteriori azioni all'elenco dei moduli nella pagina del portale moduli. Per impostazione predefinita, l’elenco dei moduli ti consente di accedere al modulo, compilarlo e inviarlo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 5%
---
# Aggiunta di azioni personalizzate agli elementi dell’elenco del modulo{#adding-custom-action-on-form-lister-items}

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

Puoi aggiungere azioni simili nel modello personalizzato. Per definire una funzione di JavaScript, aggiungi la funzione a uno script a livello di pagina e collegala all’elemento HTML richiesto. Nell&#39;esempio precedente, l&#39;espressione `onclick` è la funzione collegata.

Dopo aver apportato le modifiche al modello, la pagina del portale di esempio contiene un pulsante per inviare il collegamento del modulo tramite e-mail, come illustrato di seguito.

![e-mail](assets/email.png)
