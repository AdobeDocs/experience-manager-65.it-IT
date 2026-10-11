---
title: Applicare predefiniti per immagini Dynamic Media
description: Scopri come abilitare le risorse per distribuire dinamicamente immagini di dimensioni diverse, in formati diversi o con altre proprietà dell’immagine generate dinamicamente.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: a16e03b7-8456-4383-8860-31ab5ab00e9e
    internal-label: Image presets
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%
---
# Applicare i predefiniti per le immagini Dynamic Media {#applying-image-presets}

I predefiniti per immagini consentono alle risorse di distribuire dinamicamente immagini di diverse dimensioni, in formati diversi o con altre proprietà dell’immagine generate dinamicamente. Potete scegliere un predefinito quando esportate le immagini. Il predefinito riformerà le immagini in base alle specifiche specificate dall&#39;amministratore.

Inoltre, puoi scegliere un predefinito immagine reattivo (indicato dal pulsante **[!UICONTROL RESS]** dopo averlo selezionato).

Questa sezione descrive come utilizzare i predefiniti per immagini. [Gli amministratori possono creare e configurare predefiniti immagine](managing-image-presets.md).

>[!NOTE]
>
>L&#39;imaging avanzato funziona con i predefiniti immagine esistenti e utilizza l&#39;intelligenza all&#39;ultimo millisecondo di consegna per ridurre ulteriormente le dimensioni del file immagine in base alla velocità di connessione del browser o della rete. Per ulteriori informazioni, vedere [Smart Imaging](imaging-faq.md).

Potete applicare un predefinito immagine a un&#39;immagine in qualsiasi momento.

>[!NOTE]
>
>In modalità Dynamic Media - Scene7, i predefiniti per immagini sono supportati solo per le risorse immagini.

**Per applicare i predefiniti immagine Dynamic Media:**

1. Apri la risorsa e, nella barra a sinistra, seleziona il menu a discesa, quindi seleziona **[!UICONTROL Rappresentazioni]**.

   >[!NOTE]
   >
   >* Le rappresentazioni statiche vengono visualizzate nella metà superiore del riquadro. Le rappresentazioni dinamiche vengono visualizzate nella metà inferiore. Solo con le rappresentazioni dinamiche, puoi utilizzare l’URL per visualizzare l’immagine. Il pulsante **[!UICONTROL URL]** viene visualizzato solo se si seleziona una rappresentazione dinamica. Il pulsante **[!UICONTROL RESS]** viene visualizzato solo se si seleziona un predefinito immagine reattivo.
   >
   >* Il sistema mostra numerose rappresentazioni quando selezioni **[!UICONTROL Rappresentazioni]** nella visualizzazione Dettaglio di una risorsa. Puoi aumentare il numero di predefiniti visualizzati. Vedere [Aumentare il numero di predefiniti immagine visualizzati](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Effettua una delle seguenti operazioni:

   * Seleziona una rappresentazione dinamica per visualizzare in anteprima il predefinito immagine.
   * Per visualizzare il popup, selezionare **[!UICONTROL URL]**, **[!UICONTROL Incorpora]** o **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Se la risorsa *e* il predefinito immagine non è ancora stato pubblicato, il pulsante **[!UICONTROL URL]** (o **[!UICONTROL URL]** e **[!UICONTROL RESS]**, se applicabile) non è disponibile.
   >
   >Inoltre, i predefiniti immagine vengono pubblicati automaticamente su un server Dynamic Media.
