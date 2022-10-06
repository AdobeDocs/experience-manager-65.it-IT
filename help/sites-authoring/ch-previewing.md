---
title: Visualizzare l’anteprima delle pagine utilizzando i dati di ContextHub
seo-title: Previewing Pages Using ContextHub Data
description: La barra degli strumenti di ContextHub visualizza dati dagli archivi di ContextHub, ti consente di modificare i dati archiviati ed è utile per visualizzare in anteprima il contenuto
seo-description: The ContextHub toolbar displays data from ContextHub stores and enables you to change store data and  is useful for previewing content
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
exl-id: 78673609-8cbc-4b4b-953e-56c31ea1b4ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 96%

---

# Visualizzare l’anteprima delle pagine utilizzando i dati di ContextHub{#previewing-pages-using-contexthub-data}

La barra degli strumenti di [ContextHub](/help/sites-developing/contexthub.md) mostra i dati provenienti dagli archivi di ContextHub e consente di modificare i dati store. La barra degli strumenti ContextHub è utile per visualizzare in anteprima il contenuto determinato dai dati di uno Store ContextHub.

La barra degli strumenti è composta da una serie di modalità di interfaccia utente che contengono uno o più moduli di interfaccia utente.

* Le modalità di interfaccia utente sono icone che vengono visualizzate sul lato sinistro della barra degli strumenti. Quando fai clic o tocchi un’icona, la barra degli strumenti rivela i moduli di interfaccia utente che contiene.
* I moduli di interfaccia utente visualizzano dati da uno o più archivi di ContextHub. Alcuni moduli di interfaccia utente ti consentono inoltre di manipolare i dati archiviati.

ContextHub installa varie modalità di interfaccia utente e moduli di interfaccia utente. L’amministratore può aver [configurato ContextHub](/help/sites-developing/ch-configuring.md) per visualizzarne di diversi.

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## Visualizzare la barra degli strumenti di ContextHub {#revealing-the-contexthub-toolbar}

La barra degli strumenti di ContextHub è disponibile nella modalità di anteprima. La barra degli strumenti è disponibile solo nelle istanze dell’autore e solo se l’amministratore l’ha abilitata.

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. Con la pagina aperta per la modifica, fai clic o tocca Anteprima nella barra degli strumenti.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Per visualizzare la barra degli strumenti, fai clic o tocca l’icona di ContextHub.

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## Funzioni dei moduli di interfaccia utente {#ui-module-features}

Ogni modulo di interfaccia utente fornisce un diverso insieme di funzioni, ma i seguenti tipi di funzioni sono comuni. Poiché i moduli di interfaccia utente sono estensibili, lo sviluppatore può implementare altre funzioni, a seconda delle necessità.

### Contenuto della barra degli strumenti {#toolbar-content}

I moduli di interfaccia utente possono visualizzare dati da uno o più archivi di ContextHub nella barra degli strumenti. I moduli di interfaccia utente utilizzano un’icona e un titolo per identificarsi. 

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### Contenuto a comparsa {#popup-content}

Alcuni moduli di interfaccia utente visualizzano una finestra a comparsa quando l’utente fa clic su di essi o li seleziona mediante un tocco. In genere, la finestra a comparsa contiene informazioni aggiuntive rispetto a quelle visualizzate nella barra degli strumenti.

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### Moduli a comparsa {#popup-forms}

La finestra a comparsa di un modulo può includere elementi modulo che ti consentono di modificare i dati nell’archivio di ContextHub. Se il contenuto della pagina viene determinato dai dati archiviati, puoi utilizzare il modulo e visualizzare le modifiche apportate al contenuto della pagina.

### Modalità a schermo intero {#fullscreen-mode}

Le finestre a comparsa possono includere un’icona su cui fare clic o toccare per espandere il contenuto a comparsa fino a coprire l’intera finestra del browser o schermata.

![](do-not-localize/chlimage_1-18.png)
