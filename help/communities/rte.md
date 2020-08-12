---
title: Editor Rich Text Essentials
seo-title: Editor Rich Text Essentials
description: Panoramica delle funzioni Editor Rich Text
seo-description: Panoramica delle funzioni Editor Rich Text
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
translation-type: tm+mt
source-git-commit: 4b6311cbfe11a61b74f68bf5a25ad1f5faef5358
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---


# Rich Text Editor Essentials {#rich-text-editor-essentials}

## Panoramica {#overview}

Un editor Rich Text (RTE) consente di immettere testo con la marcatura.

Per i componenti Community, anche se simili all’editor di testo [RTF nell’ambiente](../../help/sites-authoring/rich-text-editor.md)di authoring, questo incide sul testo immesso nell’ambiente di pubblicazione.

![editor Rich Text](assets/rich-text-editor.png)

## Abilitazione dell&#39;editor Rich Text {#enabling-rich-text-editor}

È possibile abilitare i componenti community che consentono l’editor Rich Text per contenuti generati dall’utente (UGC). A seconda che il componente sia stato aggiunto a una pagina o incluso in una [funzione](functions.md), per impostazione predefinita l’editor Rich Text potrebbe non essere abilitato.

Se non è abilitata, è sufficiente attivare la modalità [di modifica](sites-console.md#authoring-site-content)dell’autore, selezionare il componente per la modifica e selezionare la `Rich Text Editor` casella di controllo.

L&#39;editor Rich Text è disponibile per i seguenti componenti Community:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Commenti](comments.md)
* [Filelibrio](file-library.md)
* [Forum](forum.md)
* [Messaggi](configure-messaging.md)
* [D/R](working-with-qna.md)
* [Recensioni](reviews.md)

## Personalizzazione {#customization}

È possibile personalizzare l’editor Rich Text in quanto l’implementazione è basata su [CKEditor](https://www.ckeditor.com/).

La configurazione corrente per i componenti Community si trova nel `cq.social.  scf   clientlib`, nella directory archivio all&#39;indirizzo

`/libs/clientlibs/social/commons/scf/ckrte.js`

La modifica della clientlib cq.social.scf non è consigliata in quanto gli aggiornamenti futuri potrebbero ignorare qualsiasi modifica.

### Esempio di personalizzazione: Collegamenti in linea {#example-customization-inline-links}

A causa di problemi di sicurezza, le opzioni del collegamento ipertestuale non sono incluse nel set di icone RTF presentate ai membri per impostazione predefinita. La capacità di generare errori è ampia quando gli hrefs sono consentiti in UGC.

Per aggiungere le opzioni relative al collegamento ipertestuale alla barra degli strumenti:

* Aggiungere una barra degli strumenti denominata &quot; `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* Seleziona **[!UICONTROL Salva tutto]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```

