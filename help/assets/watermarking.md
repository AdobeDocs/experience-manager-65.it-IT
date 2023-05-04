---
title: Aggiungi una filigrana alle risorse digitali
description: Scopri come utilizzare la funzione Watermarking per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 2%

---

# Filigrana le risorse digitali {#watermarking}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle risorse, per consentire agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. [!DNL Experience Manager Assets] supporta il testo da utilizzare come filigrana nei file PNG e JPEG.

Per applicare una filigrana alle risorse, aggiungi la fase di filigrana nel [!UICONTROL Risorsa di aggiornamento DAM] workflow.

1. Accedere al [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Da **[!UICONTROL Modelli di flusso di lavoro]** , seleziona la **[!UICONTROL Risorsa di aggiornamento DAM]** workflow e fai clic su **[!UICONTROL Modifica]**.

1. Dal pannello laterale, trascina la **[!UICONTROL Aggiungi filigrana]** passaggio al [!UICONTROL Risorsa di aggiornamento DAM] workflow.

   ![Trascina [!UICONTROL Aggiungi filigrana] e aggiungi al [!UICONTROL Risorsa di aggiornamento DAM] workflow](assets/add_watermark_step_aem_assets.png)

   *Figura: Trascina [!UICONTROL Aggiungi filigrana] e aggiungi al [!UICONTROL Risorsa di aggiornamento DAM] workflow.*

   >[!NOTE]
   >
   >Posiziona il [!UICONTROL Aggiungi filigrana] prima di [!UICONTROL Miniatura processo] passo.

1. Apri **[!UICONTROL Aggiungi filigrana]** per visualizzare le relative proprietà.
1. In **[!UICONTROL Argomenti]** specificare valori validi nei vari campi, ad esempio testo, tipo di font, dimensioni, colore, posizione, orientamento e così via. Per confermare le modifiche, fai clic su **[!UICONTROL Fine]**.

   ![Fornisci gli argomenti nel passaggio Aggiungi filigrana in [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Fornisci gli argomenti nel passaggio Aggiungi filigrana in [!DNL Assets].*

1. Salva il **[!UICONTROL Risorsa di aggiornamento DAM]** con il passaggio della filigrana.
1. Da [!DNL Assets] interfaccia utente, carica una risorsa di esempio. La filigrana viene visualizzata con le dimensioni del font, il colore e così via, nella posizione configurata nei passaggi precedenti.

Per applicare una filigrana ai documenti PDF a livello di programmazione o con informazioni dinamiche, è consigliabile utilizzare [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md) offerta.

## Suggerimenti e limitazioni {#tips-limitations}

* Sono supportate solo le filigrane basate su testo. Le immagini non vengono utilizzate come filigrane, anche se è possibile caricare le immagini durante la creazione del [!UICONTROL Aggiungi processo filigrana].
* Solo i file PNG e JPEG sono supportati per essere contrassegnati con filigrana. Gli altri formati di risorse non sono contrassegnati con filigrana.
