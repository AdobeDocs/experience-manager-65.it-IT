---
title: Disabilita Controllo dell’account utente per la configurazione PDFG applicabile sia a JEE che a OSGI
description: Scopri come disabilitare il Controllo dell’account utente per la configurazione PDFG per correggere la conversione da Word a PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Impossibile convertire file Word o Excel in PDF su Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema   {#issue}

Quando l’utente cerca di convertire i file Word o Excel in PDF su Microsoft® Windows Server, si verifica il seguente errore:

*Messaggio di errore del convertitore primario:*
*ALC-PDG-015-003-Impossibile aprire il file di input. Invia di nuovo il file o contatta l&#39;amministratore di sistema.*


## Soluzione {#solution}

Effettua le seguenti operazioni:

1. Per accedere all&#39;Utilità Configurazione di sistema, passare a **[!UICONTROL Start > Esegui]** e quindi immettere **[!UICONTROL MSCONFIG]**.
1. Fai clic sulla scheda **[!UICONTROL Strumenti]**, scorri verso il basso e seleziona **[!UICONTROL Modifica impostazioni Controllo dell&#39;account utente]**. Fare clic su **[!UICONTROL Avvia]** per eseguire il comando in una nuova finestra.
1. Regolare il dispositivo di scorrimento al livello di notifica Mai. Al termine, chiudere la finestra dei comandi e la finestra Configurazione di sistema.
1. Verificare che l&#39;impostazione del Registro di sistema per Controllo account utente sia impostata su 0 (zero). Per verificare, effettua le seguenti operazioni:

   1. Microsoft® consiglia di eseguire il backup del Registro di sistema prima di modificarlo. Per i passaggi dettagliati, vedere [Eseguire il backup e il ripristino del Registro di sistema in Windows](https://support.microsoft.com/en-us/help/322756).
   1. Aprire l&#39;editor del Registro di sistema di Microsoft® Windows. Per aprire l&#39;editor del Registro di sistema, passare a Start > Esegui, digitare regedit e fare clic su OK.
   1. Passa a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verificare che il valore di EnableLUA sia impostato su 0 (zero).
   1. Assicurarsi che il valore di **EnableLUA** sia impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudi l’editor del Registro di sistema.

1. Riavvia il computer.

## Si applica a {#appliesto}

Questa soluzione è applicabile ad AEM Forms su JEE Server e AEM Forms su OSGi Server.
