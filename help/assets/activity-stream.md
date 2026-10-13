---
title: Flusso di attività delle risorse digitali nella vista timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse sulla timeline.
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 22%
---
# Flusso di attività nella timeline {#activity-stream-in-timeline}

Questa funzione visualizza i registri attività per le risorse sulla timeline. Se in [!DNL Adobe Experience Manager Assets] si esegue una delle seguenti operazioni relative alle risorse, la funzione di flusso attività aggiorna la timeline in modo che rifletta l&#39;attività.

Nel flusso di attività vengono registrate le seguenti operazioni:

* Creare
* Eliminare
* Download (incluse le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approvazione
* Rifiuta
* Spostare

I registri attività da visualizzare nella timeline vengono recuperati dalla posizione `/var/audit/com.day.cq.dam/content/dam` di CRX, dove vengono memorizzati i file di registro. Inoltre, l&#39;attività timeline viene registrata al caricamento di nuove risorse o quando le risorse esistenti vengono modificate e archiviate in [!DNL Experience Manager] tramite [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) o [l&#39;app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=it).

>[!NOTE]
>
>I flussi di lavoro transitori non vengono visualizzati nella timeline perché per tali flussi di lavoro non vengono salvate informazioni sulla cronologia.

Per visualizzare il flusso di attività, esegui una o più operazioni sulla risorsa, seleziona la risorsa, quindi scegli **[!UICONTROL Timeline]** dall&#39;elenco GlobalNav.

![timeline-2](assets/timeline-2.png)

La timeline mostra il flusso di attività per le operazioni eseguite sulle risorse.

![flusso_attività](assets/activity_stream.png)

>[!NOTE]
>
>La posizione predefinita dell’archivio del registro per le attività di tipo **[!UICONTROL Pubblica]** e **[!UICONTROL Annulla pubblicazione]** è `/var/audit/com.day.cq.replication/content`. Per le attività di tipo **[!UICONTROL Sposta]**, la posizione predefinita è `/var/audit/com.day.cq.wcm.core.page`.
