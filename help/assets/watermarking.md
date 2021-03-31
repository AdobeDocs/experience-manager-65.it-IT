---
title: Aggiungi una filigrana alle risorse digitali
description: Scopri come utilizzare la funzione Watermarking per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
role: Business Practices, amministratore
feature: Gestione risorse
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Filigrana le risorse digitali {#watermarking}

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle risorse, per consentire agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. [!DNL Experience Manager Assets] supporta il testo da utilizzare come filigrana nei file PNG e JPEG.

Per applicare una filigrana alle risorse, aggiungi il passaggio di filigrana nel flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] .

1. Accedi all&#39;interfaccia utente [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli di flusso di lavoro]**, seleziona il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** e fai clic su **[!UICONTROL Modifica]**.

1. Dal pannello laterale, trascina il passaggio **[!UICONTROL Aggiungi filigrana]** nel flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] .

   ![Trascina il passaggio  [!UICONTROL Aggiungi ] filigrana e aggiungi al flusso di lavoro Aggiorna risorsa  [!UICONTROL DAM ] ](assets/add_watermark_step_aem_assets.png)

   *Figura: Trascina il passaggio  [!UICONTROL Aggiungi ] filigrana e aggiungi al flusso di lavoro Aggiorna risorsa  [!UICONTROL DAM ] .*

   >[!NOTE]
   >
   >Posiziona il passaggio [!UICONTROL Aggiungi filigrana] in un punto qualsiasi prima del passaggio [!UICONTROL Elabora miniatura] .

1. Apri il passaggio **[!UICONTROL Aggiungi filigrana]** per visualizzarne le proprietà.
1. Nella scheda **[!UICONTROL Argomenti]** , specifica valori validi nei vari campi, compresi testo, tipo di font, dimensioni, colore, posizione, orientamento e così via. Per confermare le modifiche, fai clic su **[!UICONTROL Fine]**.

   ![Fornisci gli argomenti nel passaggio Aggiungi filigrana in  [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Fornisci gli argomenti nel passaggio aggiungi filigrana in  [!DNL Assets].*

1. Salva il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** con il passaggio della filigrana.
1. Dall’interfaccia utente di [!DNL Assets] , carica una risorsa di esempio. La filigrana viene visualizzata con le dimensioni del font, il colore e così via, nella posizione configurata nei passaggi precedenti.

Per applicare una filigrana ai documenti PDF a livello di programmazione o con informazioni dinamiche, è consigliabile utilizzare l&#39;offerta [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).

## Suggerimenti e limitazioni {#tips-limitations}

* Sono supportate solo le filigrane basate su testo. Le immagini non vengono utilizzate come filigrane, anche se è possibile caricare le immagini durante la creazione di [!UICONTROL Aggiungi processo filigrana].
* Solo i file PNG e JPEG sono supportati per essere contrassegnati con filigrana. Gli altri formati di risorse non sono contrassegnati con filigrana.
