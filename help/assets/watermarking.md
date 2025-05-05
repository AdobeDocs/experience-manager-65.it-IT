---
title: Aggiungere una filigrana alle risorse digitali
description: Scopri come utilizzare la funzione Filigrana per aggiungere una filigrana digitale alle risorse.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# Applicare una filigrana alle risorse digitali {#watermarking}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=it) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle risorse per consentire agli utenti di verificare l&#39;autenticità e la proprietà del copyright delle risorse. [!DNL Experience Manager Assets] supporta il testo da utilizzare come filigrana nei file PNG e JPEG.

Per applicare una filigrana alle risorse, aggiungi il passaggio della filigrana nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM].

1. Accedi all&#39;interfaccia utente [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]** e fai clic su **[!UICONTROL Modifica]**.

1. Dal pannello laterale, trascina il passaggio **[!UICONTROL Aggiungi filigrana]** nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM].

   ![Trascina il passaggio [!UICONTROL Aggiungi filigrana] e aggiungi al flusso di lavoro [!UICONTROL Aggiorna risorsa DAM]](assets/add_watermark_step_aem_assets.png)

   *Figura: trascina il passaggio [!UICONTROL Aggiungi filigrana] e aggiungi al flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM].*

   >[!NOTE]
   >
   >Posiziona il passaggio [!UICONTROL Aggiungi filigrana] in un punto qualsiasi prima del passaggio [!UICONTROL Elabora miniatura].

1. Apri il passaggio **[!UICONTROL Aggiungi filigrana]** per visualizzarne le proprietà.
1. Nella scheda **[!UICONTROL Argomenti]**, specifica valori validi nei vari campi, tra cui testo, tipo di carattere, dimensioni, colore, posizione, orientamento e così via. Per confermare le modifiche, fare clic su **[!UICONTROL Fine]**.

   ![Specificare gli argomenti nel passaggio Aggiungi filigrana in [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: fornire gli argomenti nel passaggio Aggiungi filigrana in [!DNL Assets].*

1. Salva il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]** con il passaggio filigrana.
1. Dall&#39;interfaccia utente [!DNL Assets], carica una risorsa di esempio. La filigrana viene visualizzata con la dimensione del carattere, il colore e così via, nella posizione configurata nei passaggi precedenti.

Per applicare una filigrana ai documenti PDF a livello di programmazione o con informazioni dinamiche, è consigliabile utilizzare l&#39;offerta [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).

## Suggerimenti e limitazioni {#tips-limitations}

* Sono supportate solo le filigrane basate su testo. Le immagini non vengono utilizzate come filigrane, anche se è possibile caricarle durante la creazione del [!UICONTROL processo Aggiungi filigrana].
* Solo i file PNG e JPEG sono supportati per la filigrana. Altri formati di risorse non sono filigranati.
