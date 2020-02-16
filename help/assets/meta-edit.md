---
title: Come modificare o aggiungere metadati
description: Scopri i metadati delle risorse in Risorse AEM e vari modi per modificare i metadati delle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Come modificare o aggiungere metadati {#how-to-edit-or-add-metadata}

I metadati sono informazioni aggiuntive sulla risorsa ricercabile. Viene estratto automaticamente quando caricate un’immagine. Potete modificare i metadati esistenti o aggiungere nuove proprietà di metadati ai campi esistenti (ad esempio, quando un campo di metadati è vuoto).

Poiché le aziende necessitano di vocabolari di metadati controllati e affidabili, AEM Assets non consente l’aggiunta ad hoc di nuove proprietà di metadati. Sebbene gli autori non possano aggiungere nuovi campi di metadati per le risorse, gli sviluppatori possono farlo. Consultate [Creare nuove proprietà di metadati per le risorse](meta-edit.md#editing-metadata-schema).

## Modificare i metadati di una risorsa {#editing-metadata-for-an-asset}

Per modificare i metadati:

1. Effettua una delle operazioni seguenti:

   * Nell’interfaccia utente Risorse, seleziona la risorsa e tocca o fai clic sull’icona **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti.
   * Dalla miniatura della risorsa, selezionate l’azione rapida **[!UICONTROL Visualizza proprietà]** .
   * Dalla pagina della risorsa, tocca o fai clic sull’icona **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti.
      ![chlimage_1-168](assets/chlimage_1-168.png)
   Nella pagina della risorsa vengono visualizzati tutti i metadati della risorsa. Questi metadati sono stati estratti automaticamente al momento del caricamento (caricamento) in Risorse AEM.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Apportate le modifiche necessarie ai metadati sotto le varie schede e, al termine, toccate o fate clic su **[!UICONTROL Salva]** dalla barra degli strumenti per salvare le modifiche. Tocca o fai clic su **[!UICONTROL Chiudi]** per tornare all’interfaccia Web Risorse.

   >[!NOTE]
   >
   >Se un campo di testo è vuoto, non esiste alcun set di metadati. Potete immettere un valore nel campo e salvarlo per aggiungere la proprietà dei metadati.

Qualsiasi modifica ai metadati di una risorsa viene riscritta nel binario originale come parte dei dati XMP. Questo avviene tramite il flusso di lavoro di riscrittura dei metadati AEM. Le modifiche apportate alle proprietà esistenti (ad esempio `dc:title`) vengono sovrascritte e le proprietà create di recente (comprese le proprietà personalizzate come `cq:tags`) vengono aggiunte insieme allo schema.

La funzione di riscrittura XMP è supportata e abilitata per le piattaforme e i formati di file descritti nei requisiti [tecnici.](/help/sites-deploying/technical-requirements.md)

## Modifica schema metadati {#editing-metadata-schema}

Per informazioni dettagliate su come modificare lo schema di metadati, vedere [Modificare i moduli](metadata-schemas.md#edit-metadata-schema-forms)dello schema di metadati.

## Registrazione di uno spazio nomi personalizzato in AEM {#registering-a-custom-namespace-within-aem}

Potete aggiungere spazi dei nomi personalizzati in AEM. Così come esistono spazi dei nomi predefiniti come cq, jcr e sling, potete avere uno spazio dei nomi per i metadati dell&#39;archivio e l&#39;elaborazione xml.

1. Vai alla pagina di amministrazione del tipo di nodo `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Tocca o fai clic su **[!UICONTROL Spazi dei nomi]** nella parte superiore della pagina. La pagina di amministrazione dello spazio dei nomi viene visualizzata in una finestra.

1. Per aggiungere uno spazio nomi, fate clic o toccate **[!UICONTROL Nuovo]** in basso.
1. Specificate uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML (specificate l’ID nel modulo di un URI e un prefisso associato per l’ID), quindi toccate o fate clic su **[!UICONTROL Salva]**.
