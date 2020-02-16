---
title: Flusso di attività nella timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse nella timeline.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Flusso di attività nella timeline {#activity-stream-in-timeline}

Questa funzione consente di visualizzare i registri attività per le risorse nella timeline. Se esegui una delle seguenti operazioni relative alle risorse in Risorse Adobe Experience Manager (AEM), la funzione del flusso di attività aggiorna la timeline per riflettere l’attività.

Le seguenti operazioni vengono registrate nel flusso di attività:

* Crea
* Elimina
* Download (comprese le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approva
* Rifiuta
* Sposta

I registri attività da visualizzare nella timeline vengono estratti dalla posizione `/var/audit/com.day.cq.dam/content/dam` in CRX, dove vengono memorizzati i file di registro.  Inoltre, l’attività timeline viene registrata quando vengono caricate nuove risorse o le risorse esistenti vengono modificate e archiviate in AEM tramite [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) o l’app [desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)AEM.

>[!NOTE]
>
>I flussi di lavoro transitori non vengono visualizzati nella timeline, perché per questi flussi di lavoro non vengono salvate informazioni sulla cronologia.

Per visualizzare il flusso di attività, eseguite una o più operazioni sulla risorsa, selezionate la risorsa, quindi scegliete **[!UICONTROL Timeline]** dall&#39;elenco Navigazione globale.

![timeline-2](assets/timeline-2.png)

La timeline mostra il flusso di attività per le operazioni eseguite sulle risorse.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>Il percorso di memorizzazione del registro predefinito per le attività **[!UICONTROL Pubblica]** e **[!UICONTROL Annulla pubblicazione]** è `/var/audit/com.day.cq.replication/content`. Per le attività **[!UICONTROL Sposta]** , la posizione predefinita è `/var/audit/com.day.cq.wcm.core.page`.
