---
title: Aggiungere una filigrana alle risorse digitali
description: Scoprite come usare la funzione Filigrana per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Filigrana le risorse digitali {#watermarking}

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle risorse per consentire agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. [!DNL Experience Manager Assets] supporta il testo da usare come filigrana nei file PNG e JPEG.

Per applicare una filigrana alle risorse, aggiungi la filigrana nel flusso di lavoro [!UICONTROL Aggiornamento risorsa DAM].

1. Accedete all&#39;interfaccia utente [!DNL Experience Manager] e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli di workflow]**, selezionare il flusso di lavoro **[!UICONTROL Aggiornamento DAM Asset]** e fare clic su **[!UICONTROL Modifica]**.

1. Dal pannello laterale, trascinate il passaggio **[!UICONTROL Aggiungi filigrana]** nel flusso di lavoro [!UICONTROL Aggiorna risorsa DAM].

   ![Trascinate il passaggio  [!UICONTROL Aggiungi ] filigrana e aggiungete a  [!UICONTROL DAM Update ] Assetworkflow](assets/add_watermark_step_aem_assets.png)
2
   *Figura: Trascina il passaggio  [!UICONTROL Aggiungi ] filigrana e aggiungi al flusso di lavoro  [!UICONTROL DAM Update ] Assets.*

   >[!NOTE]
   >
   >Posizionare il passaggio [!UICONTROL Aggiungi filigrana] in un punto qualsiasi prima del passaggio [!UICONTROL Miniatura processo].

1. Aprire il passaggio **[!UICONTROL Aggiungi filigrana]** per visualizzarne le proprietà.
1. Nella scheda **[!UICONTROL Argomenti]**, specificare valori validi nei vari campi, quali testo, tipo di font, dimensione, colore, posizione, orientamento e così via. Per confermare le modifiche, fare clic su **[!UICONTROL Fine]**.

   ![Fornire gli argomenti nel passaggio Aggiungi filigrana in Risorse](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Fornire gli argomenti nel passaggio Aggiungi filigrana in  [!DNL Assets].*

1. Salva il flusso di lavoro **[!UICONTROL DAM Update Asset]** con il passaggio della filigrana.
1. Dall&#39;interfaccia utente di [!DNL Assets], caricate una risorsa di esempio. La filigrana viene visualizzata con la dimensione del font, il colore e così via, nella posizione configurata nei passaggi precedenti.

Per applicare la filigrana ai documenti PDF a livello di programmazione o con informazioni dinamiche, è consigliabile utilizzare l&#39;offerta [ Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).
