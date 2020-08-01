---
title: Gestire i metadati di molte risorse e raccolte in [!DNL Adobe Enterprise Manager].
description: Modificate simultaneamente i metadati di molte risorse e raccolte per diffondere rapidamente le comuni modifiche ai metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 12%

---


# Gestione di risorse e raccolte {#managing-multiple-assets-and-collections}

[!DNL Adobe Enterprise Manager Assets] consente di modificare simultaneamente i metadati di più risorse, in modo da poter rapidamente estendere le comuni modifiche ai metadati alle risorse in gruppo. Potete anche modificare i metadati per più raccolte in blocco.

Utilizzate la pagina delle proprietà per eseguire modifiche ai metadati su più risorse o raccolte:

* Cambiare le proprietà dei metadati impostando un valore comune
* Aggiunta o modifica di tag

Per personalizzare la pagina delle proprietà dei metadati, incluse l’aggiunta, la modifica, l’eliminazione delle proprietà dei metadati, utilizzate l’editor dello schema.

>[!NOTE]
>
>I metodi di modifica collettiva funzionano per le risorse disponibili in una cartella o in una raccolta. Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è possibile aggiornare [in massa i metadati dopo la ricerca](search-assets.md#metadataupdates).

## Modificare le proprietà dei metadati di più risorse {#editing-metadata-properties-of-multiple-assets}

1. Nell’interfaccia [!DNL Assets] utente, individuate la posizione delle risorse da modificare.
1. Selezionate le risorse per le quali desiderate modificare le proprietà comuni.
1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Proprietà]** per aprire la pagina delle proprietà relativa alle risorse selezionate.

   >[!NOTE]
   >
   >Quando selezionate più risorse, per le risorse viene selezionato il modulo padre più basso comune. In altre parole, nella pagina delle proprietà vengono visualizzati solo i campi di metadati comuni nelle pagine delle proprietà di tutte le singole risorse.

1. Modificate le proprietà dei metadati per le risorse selezionate nelle varie schede.
1. Per visualizzare l’editor di metadati per una risorsa specifica, deselezionate le risorse rimanenti nell’elenco. I campi dell’editor di metadati vengono compilati con i metadati della risorsa in questione.

   >[!NOTE]
   >
   >* Nella pagina delle proprietà potete rimuovere le risorse dall’elenco delle risorse deselezionandole. Per impostazione predefinita, nell’elenco delle risorse sono selezionate tutte le risorse. I metadati delle risorse rimosse dall’elenco non vengono aggiornati.
   >* Nella parte superiore dell’elenco delle risorse, selezionate la casella di controllo accanto a **[!UICONTROL Titolo]** per alternare tra la selezione delle risorse e la cancellazione dell’elenco.


1. Per selezionare uno schema di metadati diverso per le risorse, fate clic su **[!UICONTROL Impostazioni]** nella barra degli strumenti, quindi selezionate lo schema desiderato.
1. Salva le modifiche.
1. Per aggiungere i nuovi metadati a quelli esistenti nei campi che contengono più valori, seleziona **[!UICONTROL Modalità di aggiunta]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Fate clic su **[!UICONTROL Invia]**.

   >[!CAUTION]
   >
   >Per i campi con valore singolo, i nuovi metadati non vengono aggiunti al valore esistente nel campo, nemmeno se selezioni **[!UICONTROL Modalità di aggiunta]**.

## Configurare il limite per l&#39;aggiornamento in massa dei metadati {#configlimit}

Per evitare situazioni simili a DOS, Enterprise Manager limita il numero di parametri supportati in una richiesta Sling. Quando aggiornate i metadati di molte risorse in una sola volta, potete raggiungere il limite massimo e i metadati non vengono aggiornati per altre risorse. Enterprise Manager genera il seguente avviso nei registri:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

>[!MORELIKETHIS]
>
>* [Modifica delle proprietà dei metadati di più raccolte](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)

