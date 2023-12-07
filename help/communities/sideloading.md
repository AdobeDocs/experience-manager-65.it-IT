---
title: Caricamento laterale componente
description: Il sideload del componente Communities è utile quando una pagina web è progettata come una semplice app a pagina singola che modifica dinamicamente ciò che viene visualizzato a seconda di ciò che è selezionato dal visitatore del sito
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Caricamento laterale componente {#component-sideloading}

## Panoramica {#overview}

Il sideload del componente Communities è utile quando una pagina web è progettata come una semplice app a pagina singola che modifica dinamicamente ciò che viene visualizzato a seconda di ciò che è selezionato dal visitatore del sito.

Questa operazione viene eseguita quando i componenti Community non esistono nel modello della pagina, ma vengono aggiunti in modo dinamico in seguito alla selezione di un visitatore del sito.

Poiché il framework dei componenti social (SCF) è presente in modo leggero, vengono registrati solo i componenti SCF esistenti al momento del caricamento iniziale della pagina. Affinché un componente SCF aggiunto in modo dinamico possa essere registrato dopo il caricamento della pagina, è necessario richiamare SCF per &quot;sideload&quot; il componente.

Quando una pagina è progettata per scaricare i componenti di Communities, è possibile memorizzare in cache l’intera pagina.

I passaggi per aggiungere dinamicamente i componenti SCF sono i seguenti:

1. [Aggiungere il componente al DOM](#dynamically-add-component-to-dom)

1. [Sideload del componente](#sideload-by-invoking-scf) utilizzando uno dei due metodi seguenti:

* [Inclusione dinamica](#dynamic-inclusion)
   * Aumenta il limite di tutti i componenti aggiunti in modo dinamico
* [Caricamento dinamico](#dynamic-loading)
   * Aggiungere un componente specifico on-demand

>[!NOTE]
>
>Sideload di [risorse non esistenti](scf.md#add-or-include-a-communities-component) non è supportato.

## Aggiungi componente in modo dinamico a DOM {#dynamically-add-component-to-dom}

Che il componente sia incluso dinamicamente o caricato dinamicamente, deve prima essere aggiunto al DOM.

Quando si aggiunge il componente SCF, il tag più comune da utilizzare è il tag DIV, ma è possibile utilizzare anche altri tag. Poiché SCF esamina il DOM solo al caricamento iniziale della pagina, questa aggiunta al DOM passerà inosservata fino a quando SCF non verrà esplicitamente richiamato.

Indipendentemente dal tag utilizzato, l’elemento deve essere conforme almeno al pattern di elemento principale SCF normale, contenente i due attributi seguenti:

* **data-component-id**

  Percorso effettivo del componente aggiunto.

* **data-scf-component**

  Il resourceType del componente.

Di seguito è riportato un esempio di un componente commenti aggiunto:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Caricamento secondario richiamando SCF {#sideload-by-invoking-scf}

### Inclusione dinamica {#dynamic-inclusion}

L’inclusione dinamica utilizza una richiesta di boostrap che induce l’SCF ad esaminare il DOM e ad avviare tutti i componenti SCF presenti nella pagina.

Per inizializzare i componenti SCF in qualsiasi momento dopo il caricamento della pagina, è sufficiente attivare un evento JQuery come segue:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Caricamento dinamico {#dynamic-loading}

Il caricamento dinamico consente di controllare il caricamento dei componenti SCF.

Invece di avviare tutti i componenti SCF presenti nel DOM, è possibile specificare un componente SCF specifico da caricare utilizzando questo metodo JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Dove `someId` è il valore del `data-component-id` attributo.
