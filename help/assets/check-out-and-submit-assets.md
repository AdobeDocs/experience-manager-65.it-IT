---
title: Archiviare e estrarre i file in [!DNL Assets]
description: Scopri come estrarre le risorse da modificare e archiviarle nuovamente al termine delle modifiche.
contentOwner: AG
role: Professionista
translation-type: tm+mt
source-git-commit: eb87d77e1366786e8574f84590dfe9a3303efda0
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%

---


# Archiviare e estrarre i file in [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] consente di estrarre le risorse da modificare e di archiviarle nuovamente dopo aver completato le modifiche. Dopo aver estratto una risorsa, puoi modificarla, annotarla, pubblicarla, spostarla o eliminarla. Il ritiro di una risorsa blocca la risorsa. Altri utenti non possono eseguire nessuna di queste operazioni sulla risorsa finché non ricontrolli la risorsa in [!DNL Assets]. Tuttavia, possono comunque modificare i metadati della risorsa bloccata.

Per poter estrarre/inserire le risorse, è necessario disporre dell’accesso in scrittura.

Questa funzione consente di impedire ad altri utenti di ignorare le modifiche apportate da un autore, in cui più utenti collaborano alla modifica dei flussi di lavoro tra più team.

## Estrarre risorse {#checking-out-assets}

1. Dall’interfaccia utente di [!DNL Assets] , seleziona la risorsa da estrarre. È inoltre possibile selezionare più risorse da estrarre.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Checkout]**. L&#39;opzione **[!UICONTROL Checkout]** passa a **[!UICONTROL Check-in]**.
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

1. Seleziona la risorsa modificata dall&#39;interfaccia [!DNL Assets] e fai clic su **[!UICONTROL Archivia]** nella barra degli strumenti. La risorsa modificata viene archiviata in [!DNL Assets] ed è disponibile per la modifica ad altri utenti.

## Check-in forzato {#forced-check-in}

Gli amministratori possono archiviare le risorse estratte da altri utenti.

1. Accedi a [!DNL Assets] come amministratore.
1. Dall’interfaccia utente di [!DNL Assets] , seleziona una o più risorse che sono state estratte da altri utenti.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Rilascia blocco]**. La risorsa viene archiviata ed è disponibile per la modifica ad altri utenti.

## Best practice e limitazioni {#tips-limitations}

* È possibile eliminare una *cartella* contenente file di risorse estratti. Prima di eliminare una cartella, accertati che gli utenti non abbiano estratto risorse digitali.

>[!MORELIKETHIS]
>
>* [Informazioni sull’app  [!DNL Experience Manager] indesktop di check-in e check-out](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [Esercitazione video per comprendere il check-in e il check-out [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

