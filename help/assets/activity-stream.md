---
title: Flusso di attività delle risorse digitali nella visualizzazione timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse nella timeline.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 23%

---


# Flusso di attività nella cronologia {#activity-stream-in-timeline}

Questa funzione consente di visualizzare i registri attività per le risorse nella timeline. Se eseguite una delle seguenti operazioni relative alle risorse in [!DNL Adobe Experience Manager Assets], la funzione del flusso di attività aggiorna la cronologia per riflettere l&#39;attività.

Le seguenti operazioni vengono registrate nel flusso di attività:

* Crea
* Elimina
* Download (comprese le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approva
* Rifiuta
* Sposta

I registri attività da visualizzare nella timeline vengono recuperati dalla posizione `/var/audit/com.day.cq.dam/content/dam` di CRX, dove vengono memorizzati i file di registro. Inoltre, l&#39;attività della cronologia viene registrata quando vengono caricate nuove risorse o le risorse esistenti vengono modificate e sottoposte a Check-In in [ collegamento risorsa Adobe](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) o [&#39;app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).[!DNL Experience Manager]

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
