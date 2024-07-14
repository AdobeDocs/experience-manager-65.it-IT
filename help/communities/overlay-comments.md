---
title: Componenti Sovrapponi community
description: Scopri come sovrapporre un componente predefinito in modo da poter modificare l’aspetto o il comportamento di un componente a livello globale, per tutti i riferimenti relativi al componente.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Componenti Sovrapponi community {#overlay-communities-components}

L&#39;intenzione di [sovrapporsi](/help/communities/client-customize.md#overlays) a un componente predefinito è di alterare l&#39;aspetto o il comportamento di un componente a livello globale, per tutti i riferimenti relativi al componente. Si basa sulla natura di sling per risolvere nella cartella /apps prima di effettuare la ricerca nella cartella /libs. Pertanto, il percorso del componente è identico al percorso del componente predefinito, tranne per il fatto che si trova nella cartella /apps e non nella cartella /libs.

## Esempio {#example}

**Componente commenti sovrapposizione**

Supponiamo di voler modificare la funzione di commento in modo che corrisponda alla progettazione del sito web, modificando l’intestazione del commento in modo che non visualizzi più l’avatar per alcun commento. Le soluzioni per nascondere l’avatar utilizzano CSS o, come descritto qui, sovrappongono header.jsp nella cartella apps in modo che il HTML contenente l’avatar non venga mai inviato al client.

Per sovrapporre i commenti, è necessario:

1. [Pagina Crea commenti](/help/communities/overlay-create-comments-page.md)
1. [Crea nodi](/help/communities/overlay-create-nodes.md)
1. [Modificare l&#39;aspetto](/help/communities/overlay-alter-appearance.md)

**Sovrapponi e-mail notifiche**

Se desideri personalizzare il messaggio delle notifiche e-mail, puoi farlo [sovrapponendo](/help/communities/client-customize.md#overlays) i modelli in `/libs/settings/community/templates/email/html`.

Ad esempio, supponiamo che tu voglia modificare le menzioni notifiche e-mail (per un componente specifico di Communities in cui viene creato UGC). In questi casi, aggiungere una condizione **if** per il verbo **mentisci** nei modelli dei componenti per i quali è stato abilitato il supporto di **@mentions**.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Per modificare il modello di notifiche e-mail per @mention nei commenti del blog, inserisci il modello predefinito in: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
