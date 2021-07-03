---
title: Flusso di attività delle risorse digitali nella visualizzazione timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse nella timeline.
contentOwner: AG
feature: Gestione risorse
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 21%

---

# Flusso di attività nella timeline {#activity-stream-in-timeline}

Questa funzione visualizza i registri attività per le risorse nella timeline. Se esegui una delle seguenti operazioni relative alle risorse in [!DNL Adobe Experience Manager Assets], la funzione di flusso di attività aggiorna la timeline per riflettere l’attività.

Le seguenti operazioni vengono registrate nel flusso di attività:

* Crea
* Elimina
* Download (incluse le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approva
* Rifiuta
* Sposta

I registri attività da visualizzare nella timeline vengono recuperati dalla posizione `/var/audit/com.day.cq.dam/content/dam` di CRX, dove vengono memorizzati i file di registro. Inoltre, l’attività timeline viene registrata al caricamento di nuove risorse o quando le risorse esistenti vengono modificate e archiviate in [!DNL Experience Manager] tramite [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) o [app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>I flussi di lavoro transitori non vengono visualizzati nella timeline, perché per questi flussi di lavoro non vengono salvate informazioni sulla cronologia.

Per visualizzare il flusso di attività, esegui una o più operazioni sulla risorsa, seleziona la risorsa, quindi scegli **[!UICONTROL Timeline]** dall’elenco Navigazione globale.

![timeline-2](assets/timeline-2.png)

La timeline mostra il flusso di attività per le operazioni eseguite sulle risorse.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>La posizione predefinita dell’archivio del registro per le attività di tipo **[!UICONTROL Pubblica]** e **[!UICONTROL Annulla pubblicazione]** è `/var/audit/com.day.cq.replication/content`. Per le attività di tipo **[!UICONTROL Sposta]**, la posizione predefinita è `/var/audit/com.day.cq.wcm.core.page`.
