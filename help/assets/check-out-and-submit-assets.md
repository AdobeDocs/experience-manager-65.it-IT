---
title: Archiviare e archiviare le risorse digitali per la modifica
description: Scoprite come estrarre le risorse per la modifica e archiviarle nuovamente al termine delle modifiche.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# Archiviazione e estrazione di file in AEM DAM {#check-in-and-check-out-files-in-assets}

Risorse Adobe Experience Manager (AEM) consente di estrarre le risorse per la modifica e archiviarle nuovamente dopo aver completato le modifiche. Dopo aver estratto una risorsa, potete solo modificare, annotare, pubblicare, spostare o eliminare la risorsa. Il check-out di una risorsa blocca la risorsa. Altri utenti non possono eseguire nessuna di queste operazioni sulla risorsa finché non riaccedi a Risorse AEM. Tuttavia, possono comunque modificare i metadati della risorsa bloccata.

Per poter estrarre/archiviare le risorse, è necessario disporre dell&#39;accesso in scrittura.

Questa funzione consente di impedire ad altri utenti di ignorare le modifiche apportate da un autore, in cui più utenti collaborano ai flussi di lavoro di modifica tra più team.

## Estrarre le risorse {#checking-out-assets}

1. Nell’interfaccia utente Risorse, seleziona la risorsa da estrarre. Potete anche selezionare più risorse da estrarre.
1. Dalla barra degli strumenti, fare clic o toccare **[!UICONTROL Checkout]**.
L&#39;opzione **[!UICONTROL Checkout]** (Checkout **[!UICONTROL ) consente di passare a]**Check.
Per verificare se altri utenti possono modificare la risorsa estratta, effettuate l’accesso come un altro utente. Sulla miniatura della risorsa estratta viene visualizzato un simbolo di blocco.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Selezionate la risorsa. Nella barra degli strumenti non sono visualizzate opzioni che consentono di modificare, annotare, pubblicare o eliminare la risorsa.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Potete tuttavia toccare **[!UICONTROL Visualizza proprietà]** per modificare i metadati della risorsa bloccata.

1. Toccate **[!UICONTROL Modifica]** per aprire la risorsa in modalità di modifica.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Modificate la risorsa e salvate le modifiche. Ad esempio, ritagliate l’immagine e salvate.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Potete anche scegliere di inserire delle annotazioni o pubblicare la risorsa.

1. Selezionate la risorsa modificata dall’interfaccia utente Risorse e toccate **[!UICONTROL Controllo]** dalla barra degli strumenti. La risorsa modificata viene archiviata in Risorse AEM ed è disponibile per la modifica da parte di altri utenti.

## Check-in forzato {#forced-check-in}

Gli amministratori possono archiviare le risorse sottoposte a Check-Out da altri utenti.

1. Accedi a Risorse AEM come amministratore.
1. Nell’interfaccia utente delle risorse, seleziona una o più risorse che sono state sottoposte a check-out da parte di altri utenti.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dalla barra degli strumenti, toccate **[!UICONTROL Rilascia blocco]**. La risorsa viene archiviata e può essere modificata da altri utenti.

>[!MORELIKETHIS]
>
>* [Informazioni sull’archiviazione e il check-out nell’app desktop AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Esercitazione video per comprendere l’archiviazione e il check-in di Risorse AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

