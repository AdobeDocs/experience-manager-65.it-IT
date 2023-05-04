---
title: Archiviare e estrarre i file in [!DNL Assets]
description: Scopri come estrarre le risorse da modificare e archiviarle nuovamente al termine delle modifiche.
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 3%

---

# Archiviazione e estrazione dei file [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di estrarre le risorse da modificare e di archiviarle nuovamente dopo aver completato le modifiche. Dopo aver estratto una risorsa, puoi modificarla, annotarla, pubblicarla, spostarla o eliminarla. Il ritiro di una risorsa blocca la risorsa. Altri utenti non possono eseguire nessuna di queste operazioni sulla risorsa finché non accedi nuovamente a [!DNL Assets]. Tuttavia, possono comunque modificare i metadati della risorsa bloccata.

Per poter estrarre/inserire le risorse, è necessario disporre dell’accesso in scrittura.

Questa funzione consente di impedire ad altri utenti di ignorare le modifiche apportate da un autore, in cui più utenti collaborano alla modifica dei flussi di lavoro tra più team.

## Estrarre risorse {#checking-out-assets}

1. Da [!DNL Assets] interfaccia utente, seleziona la risorsa da estrarre. È inoltre possibile selezionare più risorse da estrarre.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Pagamento]**. La **[!UICONTROL Pagamento]** consente di passare da un&#39;opzione all&#39;altra **[!UICONTROL Controllo]**.
Per verificare se altri utenti possono modificare la risorsa estratta, accedi come un altro utente. Un simbolo a forma di lucchetto viene visualizzato sulla miniatura della risorsa estratta.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Seleziona la risorsa. Nella barra degli strumenti non sono visualizzate opzioni che consentono di modificare, annotare, pubblicare o eliminare la risorsa.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Per modificare i metadati della risorsa bloccata, fai clic su **[!UICONTROL Visualizza proprietà]**.

1. Fai clic su **[!UICONTROL Modifica]** per aprire la risorsa in modalità di modifica.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Modifica la risorsa e salva le modifiche. Ad esempio, ritaglia l’immagine e salva.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Puoi anche scegliere di annotare o pubblicare la risorsa.

1. Seleziona la risorsa modificata dalla [!DNL Assets] e fai clic su **[!UICONTROL Controllo]** dalla barra degli strumenti. La risorsa modificata viene archiviata in [!DNL Assets] ed è disponibile per la modifica ad altri utenti.

## Check-in forzato {#forced-check-in}

Gli amministratori possono archiviare le risorse estratte da altri utenti.

1. Accedi a [!DNL Assets] come amministratore.
1. Da [!DNL Assets] l’interfaccia utente seleziona una o più risorse che sono state estratte da altri utenti.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Blocco versione]**. La risorsa viene archiviata ed è disponibile per la modifica ad altri utenti.

## Best practice e limitazioni {#tips-limitations}

* È possibile eliminare un *cartella* che contiene file di risorse estratti. Prima di eliminare una cartella, accertati che gli utenti non abbiano estratto risorse digitali.

>[!MORELIKETHIS]
>
>* [Comprendere il check-in e il check-out [!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Esercitazione video per comprendere il check-in e il check-out [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

