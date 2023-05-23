---
title: Sovrapponi componenti community
seo-title: Overlay communities components
description: Sovrapponi componenti community
seo-description: Overlay communities components
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Sovrapponi componenti community {#overlay-communities-components}

L&#39;intenzione di [sovrapposizione](/help/communities/client-customize.md#overlays) un componente di default consiste nel modificare l&#39;aspetto o il comportamento di un componente a livello globale, per tutti i riferimenti relativi al componente. Si basa sulla natura di sling per risolvere nella cartella /apps prima di effettuare la ricerca nella cartella /libs. Pertanto, il percorso del componente è identico al percorso del componente predefinito, tranne per il fatto che si trova nella cartella /apps e non nella cartella /libs.

## Esempio {#example}

**Componente per commenti di sovrapposizione**

Supponiamo di voler modificare la funzione di commento in modo che corrisponda alla progettazione del sito web, modificando l’intestazione del commento in modo che non visualizzi più l’avatar per alcun commento. Le soluzioni per nascondere l’avatar utilizzano CSS o, come descritto qui, sovrappongono header.jsp nella cartella apps in modo che il HTML contenente l’avatar non venga mai inviato al client.

Per sovrapporre i commenti è necessario:

1. [Pagina Commenti](/help/communities/overlay-create-comments-page.md)
1. [Crea nodi](/help/communities/overlay-create-nodes.md)
1. [Modificare l&#39;aspetto](/help/communities/overlay-alter-appearance.md)

**Sovrapponi e-mail notifiche**

Se desideri personalizzare il messaggio delle notifiche e-mail, puoi farlo tramite [sovrapposizione](/help/communities/client-customize.md#overlays) i modelli in **/libs/settings/community/templates/email/html**.

Ad esempio, per modificare le menzioni e-mail di notifica (per un componente community specifico in cui viene creato ugc) aggiungi un **se** condizione per verbo **menzione** nei modelli dei componenti per i quali hai abilitato la funzione **@mentions** supporto.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Per modificare il modello di notifiche e-mail da @mention nei commenti di blog, inserisci il modello predefinito in: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
