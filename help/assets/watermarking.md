---
title: Aggiungere una filigrana alle risorse digitali
description: Scopri come utilizzare la funzione Filigrana per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---

# Applicare una filigrana alle risorse digitali {#watermarking}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle risorse per consentire agli utenti di verificare l’autenticità e la proprietà del copyright delle risorse. [!DNL Experience Manager Assets] supporta il testo da utilizzare come filigrana nei file PNG e JPEG.

Per poter applicare una filigrana alle risorse, aggiungi il passaggio filigrana in [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro.

1. Accedere a [!DNL Experience Manager] e passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla sezione **[!UICONTROL Modelli flusso di lavoro]** , seleziona la **[!UICONTROL Aggiorna risorsa DAM]** workflow e clic su **[!UICONTROL Modifica]**.

1. Dal pannello laterale, trascina **[!UICONTROL Aggiungi filigrana]** passa a [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro.

   ![Trascina [!UICONTROL Aggiungi filigrana] e aggiungi al [!UICONTROL Aggiorna risorsa DAM] workflow](assets/add_watermark_step_aem_assets.png)

   *Figura: Trascinare [!UICONTROL Aggiungi filigrana] e aggiungi al [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro.*

   >[!NOTE]
   >
   >Posiziona [!UICONTROL Aggiungi filigrana] un passaggio qualsiasi prima del [!UICONTROL Elabora miniatura] passaggio.

1. Apri **[!UICONTROL Aggiungi filigrana]** per visualizzarne le proprietà.
1. In **[!UICONTROL Argomenti]** , specificare valori validi nei vari campi, inclusi testo, tipo di carattere, dimensioni, colore, posizione, orientamento e così via. Per confermare le modifiche, fai clic su **[!UICONTROL Fine]**.

   ![Fornisci gli argomenti nel passaggio Aggiungi filigrana in [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Fornire gli argomenti nel passaggio Aggiungi filigrana in [!DNL Assets].*

1. Salva il **[!UICONTROL Aggiorna risorsa DAM]** con il passaggio filigrana.
1. Dalla sezione [!DNL Assets] interfaccia utente, carica una risorsa di esempio. La filigrana viene visualizzata con la dimensione del carattere, il colore e così via, nella posizione configurata nei passaggi precedenti.

Per applicare una filigrana ai documenti PDF a livello di programmazione o con informazioni dinamiche, è consigliabile utilizzare [Experience Manager servizi documentali](/help/forms/using/overview-aem-document-services.md) offerta.

## Suggerimenti e limitazioni {#tips-limitations}

* Sono supportate solo le filigrane basate su testo. Le immagini non vengono utilizzate come filigrane, anche se è possibile caricarle durante la creazione di [!UICONTROL Processo Aggiungi filigrana].
* Solo i file PNG e JPEG sono supportati per la filigrana. Altri formati di risorse non sono filigranati.
