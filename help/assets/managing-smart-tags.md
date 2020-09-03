---
title: Gestione di smart tag e ricerche
description: Aggiornare o rimuovere gli smart tag non accurati per migliorare la pertinenza dei tag
contentOwner: AG
translation-type: tm+mt
source-git-commit: deb8ce3c6758efa9a127bfad4163ebd1c0f6f97a
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Gestione di smart tag e ricerche {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

Potete curare i tag avanzati per rimuovere eventuali tag non accurati eventualmente assegnati alle immagini del vostro marchio, in modo da visualizzare solo i tag più rilevanti.

La moderazione degli smart tag consente inoltre di perfezionare le ricerche basate sui tag per le immagini, assicurando che l’immagine venga visualizzata nei risultati di ricerca per i tag più rilevanti. In sostanza, elimina la possibilità che immagini non collegate vengano visualizzate nei risultati della ricerca.

Potete anche assegnare un rango più alto a un tag per aumentarne la rilevanza rispetto a un’immagine. La promozione di un tag per un’immagine aumenta le probabilità che l’immagine venga visualizzata nei risultati di ricerca quando viene eseguita una ricerca in base al tag specifico.

1. Nella casella di ricerca Omnico, cercate le risorse in base a un tag.
1.  Inspect i risultati della ricerca per identificare un’immagine che non si trova rilevante ai fini della ricerca.
1. Selezionate l’immagine e fate clic su **[!UICONTROL Gestisci tag]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Gestisci tag]** , ispezionate i tag. Se non desiderate che l’immagine venga cercata in base a un tag specifico, selezionate il tag e fate clic su **[!UICONTROL Elimina]** nella barra degli strumenti. In alternativa, fare clic sul `X` simbolo visualizzato accanto all&#39;etichetta.
1. Per assegnare un rango più alto a un tag, selezionatelo e fate clic su **[!UICONTROL Promuovi]** nella barra degli strumenti. Il tag promosso viene spostato nella sezione **[!UICONTROL Tag]** .
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. Passate alla pagina delle proprietà dell’immagine. Osservate che al tag promosso è stata assegnata un’elevata rilevanza e, di conseguenza, appare più alta nei risultati della ricerca.

## Comprendere i risultati [!DNL Experience Manager] di ricerca con gli smart tag {#understandsearch}

Per impostazione predefinita, [!DNL Experience Manager] la ricerca combina i termini di ricerca con una `AND` clausola. L&#39;utilizzo di smart tag non modifica questo comportamento predefinito. L&#39;utilizzo di smart tag aggiunge una `OR` clausola aggiuntiva per individuare qualsiasi termine di ricerca negli smart tag applicati. For example, consider searching for `woman running`. Per impostazione predefinita, le risorse con una sola parola chiave `woman` o una sola `running` parola chiave nei metadati non vengono visualizzate nei risultati della ricerca. Tuttavia, in una query di ricerca di questo tipo viene visualizzata una risorsa con `woman` o `running` tramite smart tag. Quindi i risultati della ricerca sono una combinazione di:

* risorse con `woman` e `running` parole chiave nei metadati.

* assets smart tag con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a uno qualsiasi dei termini di ricerca negli smart tag. Nell&#39;esempio precedente, l&#39;ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. corrispondenze di `woman running` nei vari campi di metadati.
1. corrispondenze di `woman running` in smart tag.
1. corrispondenze di `woman` o di `running` in smart tag.

>[!CAUTION]
>
>Se l&#39;indicizzazione Lucene viene effettuata [!DNL Adobe Experience Manager] quindi la ricerca basata sugli smart tag non funziona come previsto.
