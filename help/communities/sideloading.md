---
title: Sideloading componente
seo-title: Sideloading componente
description: Il sideloading dei componenti di Communities è utile quando una pagina Web è progettata come un'app semplice a pagina singola che modifica dinamicamente ciò che viene visualizzato a seconda di ciò che è selezionato dal visitatore del sito
seo-description: Il sideloading dei componenti di Communities è utile quando una pagina Web è progettata come un'app semplice a pagina singola che modifica dinamicamente ciò che viene visualizzato a seconda di ciò che è selezionato dal visitatore del sito
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Sideloading componente {#component-sideloading}

## Panoramica {#overview}

Il sideloading dei componenti di Communities è utile quando una pagina Web è progettata come un&#39;app semplice a pagina singola che modifica dinamicamente ciò che viene visualizzato a seconda di ciò che è selezionato dal visitatore del sito.

Questo si ottiene quando i componenti Community non esistono nel modello di pagina, ma vengono aggiunti dinamicamente dopo la selezione di un visitatore del sito.

Poiché il framework dei componenti social (SCF) ha una presenza leggera, vengono registrati solo i componenti SCF esistenti al momento del caricamento iniziale della pagina. Affinché un componente SCF aggiunto in modo dinamico possa essere registrato dopo il caricamento della pagina, è necessario richiamare SCF per &quot;trasferire localmente&quot; il componente.

Quando una pagina è progettata per trasferire localmente componenti di Communities, è possibile memorizzare nella cache l’intera pagina.

I passaggi per aggiungere dinamicamente i componenti SCF sono i seguenti:

1. [Aggiungere il componente al DOM](#dynamically-add-component-to-dom)

1. [Ricaricare localmente il componente](#sideload-by-invoking-scf) utilizzando uno dei due metodi seguenti:

* [Integrazione dinamica](#dynamic-inclusion)
   * Boostrap tutti i componenti aggiunti dinamicamente
* [Caricamento dinamico](#dynamic-loading)
   * Aggiunta di un componente specifico su richiesta

>[!NOTE]
>
>Il sideloading delle risorse [](scf.md#add-or-include-a-communities-component) non esistenti non è supportato.

## Aggiunta dinamica di un componente a DOM {#dynamically-add-component-to-dom}

Sia che il componente sia incluso in modo dinamico o caricato in modo dinamico, deve prima essere aggiunto al DOM.

Quando aggiungete il componente SCF, il tag più comune da usare è il tag DIV, ma possono essere utilizzati anche altri tag. Poiché SCF esamina il DOM solo quando la pagina viene inizialmente caricata, l’aggiunta al DOM passerà inosservata fino a quando SCF non viene richiamato in modo esplicito.

Qualsiasi tag viene utilizzato, come minimo, l&#39;elemento deve essere conforme al normale pattern dell&#39;elemento principale SCF, contenente i due attributi seguenti:

* **data-component-id**

   Percorso effettivo del componente aggiunto.

* **data-scf-component**

   Il resourceType del componente.

Esempio di un componente per commenti aggiunto:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Trasferimento locale tramite chiamata SCF {#sideload-by-invoking-scf}

### Inclusione dinamica {#dynamic-inclusion}

L’inclusione dinamica utilizza una richiesta boostrap che consente a SCF di esaminare il DOM e avviare il rapping di tutti i componenti SCF presenti nella pagina.

Per inizializzare i componenti SCF in qualsiasi momento dopo il caricamento della pagina, è sufficiente attivare un evento JQuery come indicato di seguito:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Caricamento dinamico {#dynamic-loading}

Il caricamento dinamico consente di controllare il caricamento dei componenti SCF.

Invece di avviare tutti i componenti SCF presenti nel DOM, è possibile specificare un componente SCF specifico da caricare utilizzando questo metodo JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Dove `someId` è il valore dell&#39; `data-component-id` attributo.
