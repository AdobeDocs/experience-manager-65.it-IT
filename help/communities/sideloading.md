---
title: Caricamento laterale componente
seo-title: Component Sideloading
description: Il sideloading dei componenti di Communities è utile quando una pagina web è progettata come una semplice app a pagina singola che modifica dinamicamente ciò che viene visualizzato a seconda di ciò che è selezionato dal visitatore del sito
seo-description: Communities component sideloading is useful when a web page is designed as a simple, single page app that dynamically alters what is displayed depending on what is selected by the site visitor
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Caricamento laterale componente {#component-sideloading}

## Panoramica {#overview}

Il sideloading dei componenti di Communities è utile quando una pagina web è progettata come una semplice app a pagina singola che modifica dinamicamente ciò che viene visualizzato a seconda di ciò che è selezionato dal visitatore del sito.

Questa operazione viene eseguita quando i componenti di Communities non esistono nel modello di pagina, ma vengono aggiunti in modo dinamico dopo la selezione di un visitatore del sito.

Poiché il framework dei componenti social (SCF) ha una presenza leggera, vengono registrati solo i componenti SCF esistenti al momento del caricamento iniziale della pagina. Affinché un componente SCF aggiunto in modo dinamico possa essere registrato dopo il caricamento della pagina, è necessario richiamare SCF per &quot;effettuare il caricamento in parallelo&quot; del componente.

Quando una pagina è progettata per effettuare il sideload dei componenti di Communities, è possibile memorizzare nella cache l’intera pagina.

I passaggi per aggiungere in modo dinamico componenti SCF sono i seguenti:

1. [Aggiungi il componente al DOM](#dynamically-add-component-to-dom)

1. [Caricare in parallelo il componente](#sideload-by-invoking-scf) utilizzando uno dei due metodi seguenti:

* [Inclusione dinamica](#dynamic-inclusion)
   * Blocca tutti i componenti aggiunti dinamicamente
* [Caricamento dinamico](#dynamic-loading)
   * Aggiungi un componente specifico su richiesta

>[!NOTE]
>
>Carico laterale di [risorse non esistenti](scf.md#add-or-include-a-communities-component) non è supportato.

## Aggiungi dinamicamente un componente a DOM {#dynamically-add-component-to-dom}

Che il componente sia incluso in modo dinamico o caricato in modo dinamico, deve prima essere aggiunto al DOM.

Quando si aggiunge il componente SCF, il tag più comune da utilizzare è il tag DIV, ma possono essere utilizzati anche altri tag. Poiché SCF esamina il DOM solo quando la pagina viene inizialmente caricata, questa aggiunta al DOM passerà inosservata fino a quando SCF non viene esplicitamente richiamato.

Qualsiasi tag viene utilizzato, come minimo, l’elemento deve essere conforme al normale pattern dell’elemento principale SCF, contenente questi due attributi:

* **data-component-id**

   Percorso effettivo del componente aggiunto.

* **data-scf-component**

   Il resourceType del componente.

Di seguito è riportato un esempio di componente per commenti aggiunti:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Caricamento a margine richiamando SCF {#sideload-by-invoking-scf}

### Inclusione dinamica {#dynamic-inclusion}

L’inclusione dinamica utilizza una richiesta boostrap che si traduce in SCF che esamina il DOM e avvia il rapping di tutti i componenti SCF presenti nella pagina.

Per inizializzare i componenti SCF in qualsiasi momento dopo il caricamento della pagina, è sufficiente attivare un evento JQuery come riportato di seguito:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Caricamento dinamico {#dynamic-loading}

Il caricamento dinamico consente di controllare il caricamento dei componenti SCF.

Invece di avviare tutti i componenti SCF presenti nel DOM, è possibile specificare un componente SCF specifico da caricare utilizzando questo metodo JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Dove `someId` è il valore del `data-component-id` attributo.
