---
title: Componenti per community di sovrapposizioni
seo-title: Componenti per community di sovrapposizioni
description: Componenti per community di sovrapposizioni
seo-description: Componenti per community di sovrapposizioni
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Componenti per community di sovrapposizioni {#overlay-communities-components}

L&#39;intenzione di [overlay](/help/communities/client-customize.md#overlays) di un componente predefinito è di modificare l&#39;aspetto o il comportamento di un componente a livello globale, per tutti i riferimenti relativi al componente. Si basa sulla natura di sling per risolvere nella cartella /apps prima di cercare nella cartella /libs. Il percorso del componente è quindi identico al percorso del componente predefinito, ma si trova nella cartella /apps e non nella cartella /libs.

## Esempio {#example}

**Componente Commenti overlay**

Supponete di voler modificare la funzione del commento in modo che corrisponda alla progettazione del sito Web, modificando l’intestazione del commento in modo che non venga più visualizzato l’avatar per i commenti. Le soluzioni per nascondere l&#39;avatar utilizzano CSS o, come descritto qui, sovrappongono header.jsp nella cartella delle app in modo che l&#39;HTML che contiene l&#39;avatar non venga mai inviato al client.

Per sovrapporre i commenti è necessario:

1. [Pagina Commenti](/help/communities/overlay-create-comments-page.md)
1. [Crea nodi](/help/communities/overlay-create-nodes.md)
1. [Modifica dell&#39;aspetto](/help/communities/overlay-alter-appearance.md)

**E-mail di notifiche overlay**

Supponiamo che desideriate personalizzare il messaggio delle notifiche e-mail, potete farlo sovrapponendo [i modelli in **/libs/settings/community/templates/email/html**.](/help/communities/client-customize.md#overlays)

Ad esempio, per modificare le notifiche e-mail di menzioni (per un componente community specifico in cui viene creato ugc) aggiungere una condizione **if** per il verbo **speak** nei modelli dei componenti per i quali è stato abilitato il supporto **@menzioni**.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Per modificare il modello di notifiche e-mail per @Menzioni nei commenti del blog, posizionate fuori dalla casella in: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
