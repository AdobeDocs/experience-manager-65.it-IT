---
title: Disabilita Controllo dell’account utente per la configurazione PDFG applicabile sia a JEE che a OSGI
description: Passaggi per disabilitare l'account utente per la configurazione PDFG per correggere la conversione da Word a PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# Impossibile convertire file Word o Excel in PDF su Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema   {#issue}

Quando l&#39;utente cerca di convertire i file Word o Excel in PDF in Microsoft Windows Server, si verifica il seguente errore:

*Messaggio di errore del convertitore primario: ALC-PDG-015-003-Il sistema non può aprire il file di input. Invia di nuovo il file o contatta l’amministratore di sistema.*


## Soluzione {#solution}

Per risolvere il problema, effettua le seguenti operazioni:
1. Per accedere all&#39;Utilità Configurazione di sistema, passare a **[!UICONTROL Start > Esegui]** e quindi immetti **[!UICONTROL MSCONFIG]**.
1. Fai clic su **[!UICONTROL Strumenti]** , scorri verso il basso e seleziona **[!UICONTROL Modifica impostazioni Controllo account utente]**. Clic **[!UICONTROL Launch]** per eseguire il comando in una nuova finestra.
1. Regolare il dispositivo di scorrimento al livello di notifica Mai. Al termine, chiudere la finestra dei comandi e la finestra Configurazione di sistema.
1. Verificare che l&#39;impostazione del Registro di sistema per Controllo account utente sia impostata su 0 (zero). Per verificare, effettua le seguenti operazioni:

   1. Microsoft® consiglia di eseguire il backup del Registro di sistema prima di modificarlo. Per i passaggi dettagliati, consulta [Eseguire il backup e il ripristino del Registro di sistema in Windows](https://support.microsoft.com/en-us/help/322756).
   1. Aprire l&#39;editor del Registro di sistema di Microsoft® Windows. Per aprire l&#39;editor del Registro di sistema, passare a Start > Esegui, digitare regedit e fare clic su OK.
   1. Accedi a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assicurarsi che il valore di EnableLUA sia impostato su 0 (zero).
   1. Assicurati che il valore di **EnableLUA** è impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudi l’editor del Registro di sistema.

1. Riavvia il computer.

## Si applica a {#appliesto}

Questa soluzione si applica ai seguenti elementi:
* AEM Forms sul server JEE
* AEM Forms sul server OSGi
