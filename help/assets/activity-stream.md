---
title: Flusso di attività delle risorse digitali nella visualizzazione timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse nella timeline.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 27%

---


# Flusso di attività nella timeline {#activity-stream-in-timeline}

Questa funzione consente di visualizzare i registri attività per le risorse nella timeline. Se eseguite una delle seguenti operazioni relative alle risorse in [!DNL Adobe Experience Manager Assets], la funzione del flusso di attività aggiorna la timeline per riflettere l&#39;attività.

Le seguenti operazioni vengono registrate nel flusso di attività:

* Crea
* Elimina
* Download (comprese le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approva
* Rifiuta
* Sposta

I registri attività da visualizzare nella timeline vengono recuperati dalla posizione `/var/audit/com.day.cq.dam/content/dam` di CRX, dove vengono memorizzati i file di registro. In addition, timeline activity is logged when new assets are uploaded or existing asses are modified and checked into [!DNL Experience Manager] via [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) or [Experience Manager desktop app](https://docs.adobe.com/content/help/it-IT/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>I flussi di lavoro transitori non vengono visualizzati nella timeline, perché per questi flussi di lavoro non vengono salvate informazioni sulla cronologia.

Per visualizzare il flusso di attività, eseguite una o più operazioni sulla risorsa, selezionate la risorsa, quindi scegliete **[!UICONTROL Timeline]** dall&#39;elenco Navigazione globale.

![timeline-2](assets/timeline-2.png)

La timeline mostra il flusso di attività per le operazioni eseguite sulle risorse.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>La posizione predefinita dell’archivio del registro per le attività di tipo **[!UICONTROL Pubblica]** e **[!UICONTROL Annulla pubblicazione]** è `/var/audit/com.day.cq.replication/content`. Per le attività di tipo **[!UICONTROL Sposta]**, la posizione predefinita è `/var/audit/com.day.cq.wcm.core.page`.
