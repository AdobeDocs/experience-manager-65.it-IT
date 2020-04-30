---
title: Aggiungi una filigrana alle risorse digitali.
description: Scoprite come usare la funzione Filigrana per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Filigrana le risorse digitali {#watermarking}

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle risorse per consentire agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. [!DNL Experience Manager Assets] supporta il testo da usare come filigrana nei file PNG e JPEG.

Per applicare una filigrana alle risorse, aggiungi la filigrana nel flusso di lavoro Aggiorna risorsa  DAM.

1. Accedere all&#39;interfaccia [!DNL Experience Manager] utente e passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli **[!UICONTROL di]** flusso di lavoro, selezionate il flusso di lavoro Aggiorna risorsa **[!UICONTROL DAM e fate clic su]** Modifica ****.

1. Dal pannello laterale, trascinate il passaggio **[!UICONTROL Aggiungi filigrana]** nel flusso di lavoro Aggiorna risorsa  DAM.

   ![Trascinate il passaggio [!UICONTROL Aggiungi filigrana] e aggiungete al flusso di lavoro [!UICONTROL Aggiorna risorsa] DAM](assets/add_watermark_step_aem_assets.png)2
   *Figura: Trascinate il passaggio[!UICONTROL Aggiungi filigrana]e aggiungete al flusso di lavoro Aggiorna risorsaDAM.*

   >[!NOTE]
   >
   >Posizionate il passaggio [!UICONTROL Aggiungi filigrana] ovunque prima del passaggio Miniatura  processo.

1. Aprite il passaggio **[!UICONTROL Aggiungi filigrana]** per visualizzarne le proprietà.
1. Nella scheda **[!UICONTROL Argomenti]** , specificate valori validi nei vari campi, inclusi testo, tipo di font, dimensione, colore, posizione, orientamento e così via. Per confermare le modifiche, fate clic su **[!UICONTROL Fine]**.

   ![Fornire gli argomenti nel passaggio Aggiungi filigrana in Risorse](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Fornire gli argomenti nel passaggio Aggiungi filigrana in[!DNL Assets].*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. Dall’interfaccia [!DNL Assets] utente, caricate una risorsa di esempio. La filigrana viene visualizzata con la dimensione del font, il colore e così via, nella posizione configurata nei passaggi precedenti.
