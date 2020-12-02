---
title: Progettazione e Designer
seo-title: Progettazione e Designer
description: Sarà necessario creare una progettazione per il sito Web e, in AEM, utilizzare Designer
seo-description: Sarà necessario creare una progettazione per il sito Web e, in AEM, utilizzare Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Designer e Designer{#designs-and-the-designer}

>[!CAUTION]
>
>Questo articolo descrive come creare un sito Web basato sull’interfaccia classica.  Adobe consiglia di utilizzare le tecnologie AEM più recenti per i siti Web, come descritto in dettaglio nell&#39;articolo [Guida introduttiva allo sviluppo  AEM Sites](/help/sites-developing/getting-started.md).

Sarà necessario creare una progettazione per il sito Web e, in AEM, utilizzare Designer.

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;accessibilità Web, vedere [AEM e le linee guida sull&#39;accessibilità Web](/help/managing/web-accessibility.md).

## Utilizzo di Designer {#using-the-designer}

La progettazione può essere definita nella sezione **progettazioni** della scheda **Strumenti**:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Qui è possibile creare la struttura necessaria per memorizzare la progettazione, quindi caricare i fogli di stile CSS e le immagini richieste.

Le progettazioni sono memorizzate in `/etc/designs`. Il percorso della progettazione da utilizzare per un sito Web è specificato utilizzando la proprietà `cq:designPath` del nodo `jcr:content`.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Tutte le modifiche apportate a una pagina in modalità di progettazione vengono mantenute sotto il nodo di progettazione del sito e vengono applicate automaticamente a tutte le pagine con la stessa struttura.

## Cosa ti serve {#what-you-will-need}

Per realizzare il progetto, è necessario:

**CSS**  - I fogli di stile a cascata definiscono i formati di aree specifiche delle pagine.
**Immagini**  - Qualsiasi immagine utilizzata per funzioni quali sfondi e pulsanti.

### Considerazioni sulla progettazione del sito Web {#considerations-when-designing-your-website}

Durante lo sviluppo di un sito Web, si consiglia vivamente di memorizzare immagini e file CSS in `/etc/design/<project>` in modo da poter fare riferimento alle risorse in base al progetto corrente, come descritto dal frammento di codice seguente.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

L&#39;esempio precedente offre diversi vantaggi:

* I componenti possono avere un aspetto o un aspetto diverso in base a ciascun sito utilizzando un percorso di progettazione diverso.
* La riprogettazione del sito Web può essere eseguita semplicemente indicando il percorso di progettazione a un altro nodo nella radice del sito da `design/v1` a `design/v2.`

* `/etc/designs` e  `/content` sono gli unici URL esterni che il browser vede proteggersi da un utente esterno incuriosito da ciò che si trova sotto la vostra  `/apps` struttura. I vantaggi dell’URL riportati sopra consentono inoltre all’amministratore di sistema di impostare una maggiore sicurezza, in quanto l’esposizione delle risorse viene limitata a poche posizioni distinte.

