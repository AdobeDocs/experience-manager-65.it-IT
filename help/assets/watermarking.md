---
title: Aggiungi una filigrana alle risorse digitali.
description: Scoprite come usare la funzione Filigrana per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Filigrana le risorse digitali {#watermarking}

Risorse Adobe Experience Manager (AEM) consente di aggiungere una filigrana digitale alle risorse per consentire agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. Risorse AEM supporta il testo da usare come filigrana nei file PNG e JPEG.

Per applicare una filigrana alle risorse, aggiungi la filigrana nel flusso di lavoro Aggiorna risorsa  DAM.

1. Accedete all&#39;interfaccia utente di AEM e andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli **[!UICONTROL di]** flusso di lavoro, selezionate il flusso di lavoro Aggiorna risorsa **[!UICONTROL DAM e fate clic su]** Modifica ****.

1. Dal pannello laterale, trascinate il passaggio **[!UICONTROL Aggiungi filigrana]** nel flusso di lavoro Aggiorna risorsa  DAM.

   ![Trascina il passaggio Aggiungi filigrana e aggiungi al flusso di lavoro della risorsa di aggiornamento DAM](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >Posizionate il passaggio [!UICONTROL Aggiungi filigrana] ovunque prima del passaggio Miniatura  processo.

1. Aprite il passaggio **[!UICONTROL Aggiungi filigrana]** per visualizzarne le proprietà.
1. Nella scheda **[!UICONTROL Argomenti]** , specificate valori validi nei vari campi, inclusi testo, tipo di font, dimensione, colore, posizione, orientamento e così via. Per confermare le modifiche, toccate o fate clic sull’icona Fine.

   ![Fornire gli argomenti nel passaggio Aggiungi filigrana in Risorse](assets/arguments_add_watermark_aem_assets.png)

1. Salva il flusso di lavoro Aggiorna risorsa **** DAM con il passaggio della filigrana.
1. Dall’interfaccia utente Risorse, caricate una risorsa di esempio. La filigrana viene visualizzata con la dimensione del font, il colore e così via, nella posizione configurata nei passaggi precedenti.
