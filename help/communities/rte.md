---
title: Nozioni di base sull’editor Rich Text
seo-title: Rich Text Editor Essentials
description: Panoramica della funzione Editor Rich Text
seo-description: Rich text Editor feature overview
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# Nozioni di base sull’editor Rich Text {#rich-text-editor-essentials}

## Panoramica {#overview}

Un editor Rich Text consente di immettere testo con markup.

Per i componenti Communities, anche se simile al [editor rich text nell’ambiente di authoring](../../help/sites-authoring/rich-text-editor.md), influisce sul testo immesso nell’ambiente di pubblicazione.

![editor rich-text](assets/rich-text-editor.png)

## Abilitazione dell’editor Rich Text {#enabling-rich-text-editor}

Per consentire l’editor Rich Text, è possibile abilitare i componenti delle community che consentono contenuti generati dagli utenti (UGC, User Generated Content). A seconda che il componente sia stato aggiunto a una pagina o incluso in una [funzione](functions.md), l’editor Rich Text può essere abilitato o meno per impostazione predefinita.

Se non è abilitata, immetti semplicemente [modalità modifica autore](sites-console.md#authoring-site-content), seleziona il componente da modificare e quindi fai clic su `Rich Text Editor` casella di controllo.

L’editor Rich Text è disponibile per i seguenti componenti Community:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Commenti](comments.md)
* [Libreria file](file-library.md)
* [Forum](forum.md)
* [Messaggi](configure-messaging.md)
* [D/R](working-with-qna.md)
* [Recensioni](reviews.md)

## Personalizzazione {#customization}

È possibile personalizzare l’editor Rich Text perché l’implementazione si basa su [CKEditor](https://www.ckeditor.com/).

La configurazione corrente per i componenti Communities si trova in `cq.social.  scf   clientlib`, che si trova nell’archivio in

`/libs/clientlibs/social/commons/scf/ckrte.js`

La modifica della libreria client cq.social.scf non è consigliata in quanto gli aggiornamenti futuri potrebbero ignorare eventuali modifiche.

### Esempio di personalizzazione: collegamenti in linea {#example-customization-inline-links}

Per motivi di sicurezza, le opzioni del collegamento ipertestuale non sono incluse nel set di icone RTF presentate ai membri per impostazione predefinita. La possibilità di danno è ampia quando gli hrefs sono consentiti in UGC.

Per aggiungere le opzioni del collegamento ipertestuale alla barra degli strumenti:

* Aggiungi una barra degli strumenti denominata &quot; `links`&quot;
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
