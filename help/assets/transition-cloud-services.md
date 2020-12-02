---
title: Applicazione dei servizi di traduzione cloud alle cartelle
description: Applicazione dei servizi di traduzione cloud alle cartelle
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 45%

---


# Applica servizi cloud di traduzione alle cartelle {#applying-translation-cloud-services-to-folders}

[!DNL Adobe Experience Manager] consente di utilizzare servizi di traduzione basati su cloud dal provider di traduzione di vostra scelta per garantire che le risorse vengano tradotte in base alle vostre esigenze.

Potete applicare il servizio di traduzione cloud direttamente alla cartella delle risorse in modo che possa essere utilizzato durante i flussi di lavoro di traduzione.

## Applicare i servizi di traduzione {#applying-the-translation-services}

L’applicazione dei servizi di traduzione cloud direttamente nella cartella delle risorse elimina la necessità di configurare i servizi di traduzione al momento della creazione o dell’aggiornamento dei flussi di lavoro di traduzione.

1. Dall&#39;interfaccia utente [!DNL Assets], selezionate la cartella alla quale desiderate applicare i servizi di traduzione.
1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Proprietà]** per visualizzare la pagina **[!UICONTROL Proprietà cartella]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vai alla scheda **[!UICONTROL Cloud Services]**.
1. Dall’elenco Configurazioni Cloud Service, scegliete il provider di traduzione desiderato. Ad esempio, se desiderate utilizzare i servizi di traduzione di Microsoft, scegliete **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Scegliere il connettore per il provider di traduzione.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Salva]**, quindi fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. Il servizio di traduzione viene applicato alla cartella.

## Applica connettore di traduzione personalizzato {#applying-custom-translation-connector}

Se vuoi applicare un connettore personalizzato per i servizi di traduzione che desideri utilizzare nei flussi di lavoro di traduzione, attieniti alla seguente procedura. Per applicare un connettore personalizzato, procedi prima con l’installazione del connettore da Gestione pacchetti. Quindi, configura il connettore dalla console Cloud Services. Dopo aver configurato il connettore, questo è disponibile nell’elenco dei connettori nella scheda Cloud Services descritta in [Applicazione dei servizi di traduzione](transition-cloud-services.md#applying-the-translation-services). Dopo aver applicato il connettore personalizzato e aver eseguito i flussi di lavoro di traduzione, nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione vengono visualizzati i dettagli del connettore, rispettivamente sotto le head **[!UICONTROL Provider]** e **[!UICONTROL Metodo]**.

1. Installare il connettore da Package Manager.
1. Fare clic sul logo [!DNL Experience Manager] e passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud Services]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, individua il connettore installato in **[!UICONTROL Servizi di terze parti]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Fare clic sul collegamento **[!UICONTROL Configura ora]** per aprire la finestra di dialogo **[!UICONTROL Crea configurazione]**.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specificare un titolo e un nome per il connettore, quindi fare clic su **[!UICONTROL Crea]**. Il connettore personalizzato è disponibile nell’elenco dei connettori nella scheda **[!UICONTROL Cloud Services]** descritta nel passaggio 5 di [Applicazione dei servizi di traduzione](#applying-the-translation-services).
1. Dopo aver applicato il connettore personalizzato, esegui uno dei flussi di lavoro di traduzione descritti in [Creazione di progetti di traduzione](translation-projects.md). Puoi verificare i dettagli del connettore nella sezione **[!UICONTROL Riepilogo di traduzione]** del progetto di traduzione della console **[!UICONTROL Progetti]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
