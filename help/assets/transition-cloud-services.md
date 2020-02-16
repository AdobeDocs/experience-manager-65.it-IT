---
title: Applicazione dei servizi di traduzione cloud alle cartelle
description: Applicazione dei servizi di traduzione cloud alle cartelle
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Applicazione dei servizi di traduzione cloud alle cartelle {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager (AEM) consente di usufruire di servizi di traduzione basati su cloud dal provider di traduzione preferito per garantire che le risorse vengano tradotte in base alle tue esigenze.

Potete applicare il servizio di traduzione cloud direttamente alla cartella delle risorse in modo che possa essere utilizzato durante i flussi di lavoro di traduzione.

## Applicare i servizi di traduzione {#applying-the-translation-services}

L’applicazione dei servizi di traduzione cloud direttamente nella cartella delle risorse elimina la necessità di configurare i servizi di traduzione al momento della creazione o dell’aggiornamento dei flussi di lavoro di traduzione.

1. Dall’interfaccia utente di Risorse, selezionate la cartella a cui desiderate applicare i servizi di traduzione.
1. Dalla barra degli strumenti, tocca o fai clic sull’icona **[!UICONTROL Proprietà]** per visualizzare la pagina Proprietà **** cartella.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vai alla scheda Servizi **** cloud.
1. Dall’elenco Configurazioni servizio cloud, scegliete il provider di traduzione desiderato. Ad esempio, se desiderate utilizzare i servizi di traduzione di Microsoft, scegliete **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Scegliere il connettore per il provider di traduzione.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Dalla barra degli strumenti, fare clic o toccare **[!UICONTROL Salva]**, quindi fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. Il servizio di traduzione viene applicato alla cartella.

## Applica connettore conversione personalizzato {#applying-custom-translation-connector}

Se si desidera applicare un connettore personalizzato per i servizi di traduzione che si desidera utilizzare nei flussi di lavoro di traduzione. Per applicare un connettore personalizzato, installate prima il connettore da Package Manager. Quindi, configura il connettore dalla console Servizi cloud. Dopo aver configurato il connettore, questo è disponibile nell&#39;elenco dei connettori nella scheda Servizi cloud descritta in [Applicazione dei servizi](transition-cloud-services.md#applying-the-translation-services)di traduzione. Dopo aver applicato il connettore personalizzato e aver eseguito i flussi di lavoro di traduzione, nella sezione Riepilogo **** conversione del progetto di traduzione vengono visualizzati i dettagli del connettore sotto le testine **[!UICONTROL Provider]** e **[!UICONTROL Metodo]**.

1. Installare il connettore da Package Manager.
1. Tocca o fai clic sul logo AEM, quindi passa a **[!UICONTROL Strumenti > Distribuzione > Servizi]** cloud.
1. Individuare il connettore installato in Servizi **[!UICONTROL di]** terze parti nella pagina Servizi **** cloud.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Tocca o fai clic sul collegamento **[!UICONTROL Configura ora]** per aprire la finestra di dialogo **[!UICONTROL Crea configurazione]** .

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specificare un titolo e un nome per il connettore, quindi fare clic o toccare **[!UICONTROL Crea]**. Il connettore personalizzato è disponibile nell&#39;elenco dei connettori nella scheda Servizi **** cloud descritta nel passaggio 5 di [Applicazione dei servizi](#applying-the-translation-services)di traduzione.
1. Eseguite qualsiasi flusso di lavoro di traduzione descritto in [Creazione di progetti](translation-projects.md) di traduzione dopo aver applicato il connettore personalizzato. Verificare i dettagli del connettore nella sezione Riepilogo **** traduzione del progetto di traduzione nella console **[!UICONTROL Progetti]** .

   ![chlimage_1-220](assets/chlimage_1-220.png)
