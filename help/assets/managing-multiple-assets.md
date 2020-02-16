---
title: Gestione di più risorse e raccolte
description: Scoprite come modificare i metadati di più risorse e raccolte contemporaneamente per diffondere rapidamente le comuni modifiche ai metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Gestione di risorse e raccolte {#managing-multiple-assets-and-collections}

Risorse Adobe Enterprise Manager (AEM) consente di modificare simultaneamente i metadati di più risorse, in modo da poter rapidamente estendere le comuni modifiche ai metadati alle risorse in blocco. Potete anche modificare i metadati per più raccolte in blocco.

Utilizzate la pagina delle proprietà per eseguire modifiche ai metadati su più risorse o raccolte:

* Cambiare le proprietà dei metadati impostando un valore comune
* Aggiunta o modifica di tag

Per personalizzare la pagina delle proprietà dei metadati, ad esempio aggiungere, modificare, eliminare proprietà dei metadati, utilizzate l&#39;editor dello schema.

>[!NOTE]
>
>I metodi di modifica collettiva funzionano per le risorse disponibili in una cartella o in una raccolta. Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è possibile aggiornare [in massa i metadati dopo la ricerca](search-assets.md#metadataupdates).

## Modificare le proprietà dei metadati di più risorse {#editing-metadata-properties-of-multiple-assets}

1. Nell’interfaccia utente Risorse, passa alla posizione delle risorse che desideri modificare.
1. Selezionate le risorse per le quali desiderate modificare le proprietà comuni.
1. Dalla barra degli strumenti, toccate o fate clic sull’icona **[!UICONTROL Proprietà]** per aprire la pagina delle proprietà relativa alle risorse selezionate.

   >[!NOTE]
   >
   >Quando selezionate più risorse, per le risorse viene selezionato il modulo padre più basso comune. In altre parole, nella pagina delle proprietà vengono visualizzati solo i campi di metadati comuni nelle pagine delle proprietà di tutte le singole risorse.

1. Modificate le proprietà dei metadati per le risorse selezionate nelle varie schede.
1. Per visualizzare l’editor di metadati per una risorsa specifica, deselezionate le risorse rimanenti nell’elenco. I campi dell’editor di metadati vengono compilati con i metadati della risorsa in questione.

   >[!NOTE]
   >
   >* Nella pagina delle proprietà potete rimuovere le risorse dall’elenco delle risorse deselezionandole. Per impostazione predefinita, nell’elenco delle risorse sono selezionate tutte le risorse. I metadati delle risorse rimosse dall’elenco non vengono aggiornati.
   >* Nella parte superiore dell’elenco delle risorse, selezionate la casella di controllo accanto a **[!UICONTROL Titolo]** per alternare tra la selezione delle risorse e la cancellazione dell’elenco.


1. Per selezionare uno schema di metadati diverso per le risorse, toccate o fate clic sull’icona **[!UICONTROL Impostazioni]** nella barra degli strumenti, quindi selezionate lo schema desiderato.
1. Salva le modifiche.
1. Per aggiungere i nuovi metadati ai metadati esistenti nei campi contenenti più valori, selezionate **[!UICONTROL Aggiungi modalità]**. Se non selezionate questa opzione, i nuovi metadati sostituiranno quelli esistenti nei campi. Toccate o fate clic su **[!UICONTROL Invia]**.

   >[!CAUTION]
   >
   >Per i campi con valore singolo, i nuovi metadati non vengono aggiunti al valore esistente nel campo, anche se selezionate la modalità **** Aggiungi.

## Modifica delle proprietà dei metadati di più raccolte {#editing-metadata-properties-of-multiple-collections}

1. Dalla console Raccolte, selezionate le raccolte da modificare.
1. Dalla barra degli strumenti, toccate o fate clic su **[!UICONTROL Proprietà]** per aprire la pagina delle proprietà per le raccolte selezionate.
1. Modificate le proprietà dei metadati per le raccolte selezionate nelle varie schede.

   >[!NOTE]
   >
   >I metadati aggiunti per le raccolte selezionate sovrascrivono i metadati precedenti per queste raccolte, ad eccezione dei tag. Eventuali tag aggiunti nel campo **[!UICONTROL Tag]** vengono aggiunti all’elenco esistente di tag presenti nei metadati.

1. Per visualizzare le proprietà dei metadati per una raccolta specifica, deselezionate le raccolte rimanenti nell&#39;elenco delle raccolte. I campi dell&#39;editor di metadati vengono compilati con i metadati per la raccolta specifica.

   >[!NOTE]
   >
   >* Nella pagina delle proprietà della raccolta, potete rimuovere le raccolte dall&#39;elenco delle raccolte deselezionandole. L&#39;elenco delle raccolte include tutte le raccolte selezionate per impostazione predefinita. I metadati per le raccolte rimosse non vengono aggiornati.
   >* Nella parte superiore dell&#39;elenco, selezionate la casella di controllo accanto a **[!UICONTROL Titolo]** per alternare tra la selezione delle raccolte e la cancellazione dell&#39;elenco.


1. Salva le modifiche.

## Configurare il limite per l&#39;aggiornamento in massa dei metadati {#configlimit}

Per evitare situazioni simili a DOS, AEM limita il numero di parametri supportati in una richiesta Sling. Quando aggiornate i metadati di molte risorse in una sola volta, potete raggiungere il limite massimo e i metadati non vengono aggiornati per altre risorse. AEM genera il seguente avviso nei registri:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Per modificare il limite, accedete alla console Web ( **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web) e modificate il valore dei parametri **[!UICONTROL POST]** massimi nella configurazione **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi.
