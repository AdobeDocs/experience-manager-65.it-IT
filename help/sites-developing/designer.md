---
title: Progettazioni e designer
seo-title: Designs and the Designer
description: Sarà necessario creare una progettazione per il sito web e in AEM è possibile farlo utilizzando Designer
seo-description: You will need to create a design for your website and in AEM, you do so by using the Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Progettazioni e designer{#designs-and-the-designer}

>[!CAUTION]
>
>Questo articolo descrive come creare un sito web basato sull’interfaccia classica. L’Adobe consiglia di utilizzare le tecnologie AEM più recenti per i siti web come descritto in dettaglio nell’articolo [Guida introduttiva allo sviluppo per AEM Sites](/help/sites-developing/getting-started.md).

Designer viene utilizzato per creare una progettazione per il sito web utilizzando la [Interfaccia classica](/help/release-notes/touch-ui-features-status.md) in AEM.

>[!NOTE]
>
>Per ulteriori informazioni sull’accessibilità web, consulta [Linee guida sull’accessibilità dei AEM e dei contenuti web](/help/managing/web-accessibility.md).

## Utilizzo di Designer {#using-the-designer}

La progettazione può essere definita nella **progettazioni** della sezione **Strumenti** scheda:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Qui puoi creare la struttura necessaria per memorizzare la progettazione, quindi caricare i fogli di stile CSS e le immagini necessarie.

I disegni sono memorizzati in `/apps/<your-project>`. Il percorso della progettazione da utilizzare per un sito web viene specificato utilizzando il `cq:designPath` proprietà `jcr:content` nodo.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Tutte le modifiche apportate a una pagina in modalità progettazione vengono mantenute sotto il nodo di progettazione del sito e vengono applicate automaticamente a tutte le pagine che hanno la stessa progettazione.

## Di cosa avrete bisogno {#what-you-will-need}

Per realizzare il tuo progetto avrai bisogno di:

**CSS** - I fogli di stile a cascata definiscono i formati di aree specifiche delle pagine.
**Immagini** - Qualsiasi immagine utilizzata per funzioni quali sfondi, pulsanti.

### Considerazioni Sulla Progettazione Del Sito Web {#considerations-when-designing-your-website}

Quando si sviluppa un sito web, si consiglia vivamente di memorizzare immagini e file CSS in `/apps/<your-project>` puoi fare riferimento alle risorse in base al progetto corrente, come descritto dal frammento seguente.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

L&#39;esempio precedente offre diversi vantaggi:

* I componenti possono avere un aspetto/aspetto diverso in base a ciascun sito utilizzando un percorso di progettazione diverso.
* La riprogettazione del sito web può essere semplicemente effettuata puntando il percorso di progettazione a un nodo diverso nella radice del sito da `design/v1` a `design/v2.`

* `/etc/designs` e `/content` sono gli unici URL esterni che il browser vede proteggersi di un utente esterno incuriosito su ciò che si trova sotto il tuo `/apps` albero. I vantaggi di cui sopra aiutano anche l’amministratore di sistema a impostare una maggiore sicurezza perché si limita l’esposizione delle risorse a poche posizioni distinte.
