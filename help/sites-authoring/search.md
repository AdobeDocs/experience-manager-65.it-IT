---
title: Ricerca
seo-title: Search
description: Individua il contenuto più velocemente con funzionalità complete di ricerca
seo-description: Find your content faster with comprehensive search
uuid: 21605b96-b467-4d01-9a64-9d0648d539f1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 4ec15013-f7ab-44d6-8053-ed28b14f95e2
docset: aem65
exl-id: dd65b308-c449-4f64-9f46-0797b922910f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 96%

---

# Ricerca  {#searching}

L’ambiente di authoring di AEM offre vari metodi per la ricerca dei contenuti, a seconda del tipo di risorsa.

>[!NOTE]
>
>Fuori dall’ambiente di authoring sono disponibili anche altri strumenti di ricerca, come [Query Builder](/help/sites-developing/querybuilder-api.md) e [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Informazioni di base sulla ricerca {#search-basics}

La funzione Ricerca è disponibile nella barra degli strumenti superiore:

![](do-not-localize/chlimage_1-17.png)

La barra di ricerca consente di effettuare le seguenti operazioni:

* Cercare una parola chiave, un percorso o un tag specifico.
* Filtrare in base a criteri specifici per le risorse come date di modifica, stato della pagina, dimensione del file e così via
* Definire e utilizzare una [ricerca salvata](#saved-searches) in base ai criteri impostati.

>[!NOTE]
>
>La ricerca può anche essere avviata mediante il tasto di scelta rapida `/` (barra) ogni volta che la barra di ricerca è visibile.

## Ricerca e filtro {#search-and-filter}

Per cercare e filtrare le risorse:

1. Apri la **Ricerca** (con la lente di ingrandimento nella barra degli strumenti) e immetti il termine da cercare. I suggerimenti verranno visualizzati e possono essere selezionati:

   ![s-01](assets/s-01.png)

   Per impostazione predefinita, i risultati della ricerca sono limitati alla posizione corrente (ovvero alla console e al tipo di risorsa corrispondente):

   ![screen_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. Se necessario, è possibile rimuovere il filtro posizione (seleziona la **X** sul filtro da rimuovere) per eseguire la ricerca in tutte le console e i tipi di risorse.
1. I risultati visualizzati saranno raggruppati in base alla console e al tipo di risorsa corrispondente.

   Puoi selezionare una risorsa specifica (sulla quale eseguire ulteriori azioni) oppure approfondire la ricerca selezionando il tipo di risorsa richiesto, ad esempio **Visualizza tutti i siti**:

   ![screen-shot_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. Per approfondire la ricerca, seleziona il simbolo della barra laterale (in alto a sinistra) per aprire il pannello laterale **Filtri e opzioni**.

   ![](do-not-localize/screen_shot_2018-03-23at101542.png)

   A seconda del tipo di risorsa, nella finestra di ricerca viene visualizzata una selezione predefinita di criteri di ricerca/filtro.

   Il pannello laterale consente di selezionare:

   * Ricerche salvate
   * Directory di ricerca
   * Tag
   * Criteri di ricerca, ad esempio Data di modifica, Stato pubblicazione, Stato LiveCopy.

   >[!NOTE]
   >
   >I criteri di ricerca possono variare:
   >
   >
   >
   >    * A seconda del tipo di risorsa selezionato; ad esempio, i criteri Risorse e Community sono comprensibilmente specifici.
   >    * La tua istanza, nonché i [moduli di ricerca](/help/sites-administering/search-forms.md), possono essere personalizzati (in base alla posizione all’interno di AEM).


   ![screen-shot_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. Puoi anche aggiungere altri termini di ricerca:

   ![screen-shot_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. Per chiudere la **Ricerca**, utilizza la **X** in alto a destra.

>[!NOTE]
>
>I criteri di ricerca vengono mantenuti quando selezioni un oggetto nei risultati di ricerca.
>
>Quando selezioni un elemento nella pagina dei risultati, e quindi torni alla pagina di ricerca dopo avere utilizzato il pulsante indietro del browser, i criteri di ricerca rimangono.

## Ricerche salvate {#saved-searches}

Oltre ad eseguire ricerche per un’ampia gamma di facet, è possibile salvare una specifica configurazione di ricerca per riutilizzarla in un secondo momento.

1. Definisci i criteri di ricerca e seleziona **Salva**.

   ![screen-shot_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. Assegna un nome e seleziona **Salva** per confermare:

   ![screen-shot_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. La ricerca salvata sarà disponibile nel selettore alla successiva apertura del pannello di ricerca:

   ![screen-shot_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. Dopo aver salvato una ricerca, puoi:

   * Utilizzare la **x** (in corrispondenza del nome di una ricerca salvata) per avviare una nuova ricerca (la ricerca salvata non verrà eliminata).
   * Seleziona **Modifica ricerca salvata**, modifica le condizioni di ricerca e seleziona nuovamente **Salva**.

Per modificare le ricerche salvate, seleziona una ricerca e fai clic sull’opzione **Modifica ricerca salvata** nella parte inferiore del pannello di ricerca.

![screen-shot_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
