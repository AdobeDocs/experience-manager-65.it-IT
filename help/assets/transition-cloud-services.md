---
title: Applicazione dei servizi di traduzione cloud alle cartelle
description: Applicazione dei servizi di traduzione cloud alle cartelle
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 43%

---


# Applicazione dei servizi di traduzione cloud alle cartelle {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager (AEM) consente di usufruire di servizi di traduzione basati su cloud dal provider di traduzione preferito per garantire che le risorse vengano tradotte in base alle tue esigenze.

Potete applicare il servizio di traduzione cloud direttamente alla cartella delle risorse in modo che possa essere utilizzato durante i flussi di lavoro di traduzione.

## Applicare i servizi di traduzione {#applying-the-translation-services}

L’applicazione dei servizi di traduzione cloud direttamente nella cartella delle risorse elimina la necessità di configurare i servizi di traduzione al momento della creazione o dell’aggiornamento dei flussi di lavoro di traduzione.

1. Dall’interfaccia utente di Risorse, selezionate la cartella a cui desiderate applicare i servizi di traduzione.
1. From the toolbar, click the **[!UICONTROL Properties]** icon to display the **[!UICONTROL Folder Properties]** page.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vai alla scheda **[!UICONTROL Cloud Services]**.
1. Dall’elenco Configurazioni servizio cloud, scegliete il provider di traduzione desiderato. Ad esempio, se desiderate utilizzare i servizi di traduzione di Microsoft, scegliete **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Scegliere il connettore per il provider di traduzione.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. From the toolbar, click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the dialog.The translation service is applied to the folder.

## Applica connettore conversione personalizzato  {#applying-custom-translation-connector}

Se vuoi applicare un connettore personalizzato per i servizi di traduzione che desideri utilizzare nei flussi di lavoro di traduzione, attieniti alla seguente procedura. Per applicare un connettore personalizzato, procedi prima con l’installazione del connettore da Gestione pacchetti. Quindi, configura il connettore dalla console Cloud Services. Dopo aver configurato il connettore, questo è disponibile nell’elenco dei connettori nella scheda Cloud Services descritta in [Applicazione dei servizi di traduzione](transition-cloud-services.md#applying-the-translation-services). Dopo aver applicato il connettore personalizzato e aver eseguito i flussi di lavoro di traduzione, nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione vengono visualizzati i dettagli del connettore, rispettivamente sotto le head **[!UICONTROL Provider]** e **[!UICONTROL Metodo]**.

1. Installare il connettore da Package Manager.
1. Fate clic sul logo AEM, quindi selezionate **[!UICONTROL Strumenti > Distribuzione > Servizi]** cloud.
1. Nella pagina **[!UICONTROL Cloud Services]**, individua il connettore installato in **[!UICONTROL Servizi di terze parti]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Fate clic sul collegamento **[!UICONTROL Configura ora]** per aprire la finestra di dialogo **[!UICONTROL Crea configurazione]** .

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specify a title and a name for the connector, and then click **[!UICONTROL Create]**. Il connettore personalizzato è disponibile nell’elenco dei connettori nella scheda **[!UICONTROL Cloud Services]** descritta nel passaggio 5 di [Applicazione dei servizi di traduzione](#applying-the-translation-services).
1. Dopo aver applicato il connettore personalizzato, esegui uno dei flussi di lavoro di traduzione descritti in [Creazione di progetti di traduzione](translation-projects.md). Puoi verificare i dettagli del connettore nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione della console **[!UICONTROL Progetti]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
