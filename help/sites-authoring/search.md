---
title: Ricerca completa
description: Trova i contenuti più rapidamente grazie a una ricerca completa.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: dd65b308-c449-4f64-9f46-0797b922910f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 57%

---

# Ricerca{#searching}

L’ambiente di authoring di AEM offre vari metodi per la ricerca dei contenuti, a seconda del tipo di risorsa.

>[!NOTE]
>
>All&#39;esterno dell&#39;ambiente di authoring sono disponibili altri meccanismi di ricerca, ad esempio [Query Builder](/help/sites-developing/querybuilder-api.md) e [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md).

## Informazioni di base sulla ricerca {#search-basics}

La funzione Ricerca è disponibile nella barra degli strumenti superiore:

![Ricerca](do-not-localize/chlimage_1-17.png)

La barra di ricerca consente di effettuare le seguenti operazioni:

* Cerca una parola chiave, un percorso o un tag specifico.
* Filtra in base a criteri specifici per le risorse, ad esempio date di modifica, stato della pagina, dimensione del file e così via.
* Definisci e utilizza una [ricerca salvata](#saved-searches) - in base ai criteri di cui sopra.

>[!NOTE]
>
>La ricerca può anche essere avviata mediante il tasto di scelta rapida `/` (barra) ogni volta che la barra di ricerca è visibile.

## Ricerca e filtro {#search-and-filter}

Per cercare e filtrare le risorse:

1. Apri la **Ricerca** (con la lente di ingrandimento nella barra degli strumenti) e immetti il termine da cercare. Saranno presentati dei suggerimenti che potranno essere selezionati:

   ![s-01](assets/s-01.png)

   Per impostazione predefinita, i risultati della ricerca sono limitati alla posizione corrente (ovvero, alla console e al tipo di risorsa correlato):

   ![schermata_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. Se necessario, è possibile rimuovere il filtro località (selezionare **X** sul filtro che si desidera rimuovere) per eseguire ricerche in tutte le console/i tipi di risorse.
1. I risultati visualizzati vengono raggruppati in base alla console e al tipo di risorsa corrispondente.

   È possibile selezionare una risorsa specifica (per ulteriori azioni) oppure eseguire il drill-down selezionando il tipo di risorsa richiesto, ad esempio **Visualizza tutti i siti**:

   ![schermata_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. Per approfondire la ricerca, seleziona il simbolo della barra laterale (in alto a sinistra) per aprire il pannello laterale **Filtri e opzioni**.

   ![Filtri e opzioni](do-not-localize/screen_shot_2018-03-23at101542.png)

   In base al tipo di risorsa, la funzione Ricerca mostrerà una selezione predefinita di criteri di ricerca/filtro.

   Il pannello laterale consente di selezionare:

   * Ricerche salvate
   * Directory di ricerca
   * Tag
   * Criteri di ricerca, ad esempio Date modificate, Stato Publish, Stato LiveCopy.

   >[!NOTE]
   >
   >I criteri di ricerca possono variare:
   >
   >
   >
   >    * A seconda del tipo di risorsa selezionato; ad esempio, i criteri di Risorse e Community sono chiaramente specifici.
   >    * È possibile personalizzare l&#39;istanza come [Forms di ricerca](/help/sites-administering/search-forms.md) (in base alla posizione all&#39;interno dell&#39;AEM).
   >
   >

   ![schermata_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. Puoi anche aggiungere altri termini di ricerca:

   ![schermata_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. Per chiudere la **Ricerca**, utilizza la **X** in alto a destra.

>[!NOTE]
>
>I criteri di ricerca vengono mantenuti quando selezioni un elemento nei risultati di ricerca.
>
>Quando selezioni un elemento nella pagina dei risultati, e quindi torni alla pagina di ricerca dopo avere utilizzato il pulsante indietro del browser, i criteri di ricerca rimangono.

## Ricerche salvate {#saved-searches}

Oltre a eseguire ricerche in base a un’ampia gamma di facet, puoi anche salvare una particolare configurazione di ricerca per riutilizzarla in una fase successiva:

1. Definisci i criteri di ricerca e seleziona **Salva**.

   ![schermata_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. Assegna un nome e seleziona **Salva** per confermare:

   ![schermata_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. La ricerca salvata sarà disponibile nel selettore alla successiva apertura del pannello di ricerca:

   ![schermata_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. Una volta salvato, è possibile:

   * Utilizza **x** (rispetto al nome della ricerca salvata) per avviare una nuova query (la ricerca salvata stessa non verrà eliminata).
   * **Modifica ricerca salvata**, modifica le condizioni di ricerca, quindi **Salva** di nuovo.

Per modificare le ricerche salvate, seleziona una ricerca e fai clic sull’opzione **Modifica ricerca salvata** nella parte inferiore del pannello di ricerca.

![schermata_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
