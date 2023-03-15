---
title: Disattiva UAC per la configurazione PDFG applicabile sia a JEE che a OSGI
description: Passaggi per disabilitare l'UAC per la configurazione PDFG
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# Impossibile convertire il file Word o Excel in PDF su Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema   {#issue}

Quando l&#39;utente prova a convertire i file Word o Excel in PDF su Microsoft Windows Server, si verifica il seguente errore:

*Messaggio di errore dal convertitore principale: ALC-PDG-015-003-Il sistema non può aprire il file di input. Invia nuovamente il file o contatta l&#39;amministratore di sistema.*


## Soluzione {#solution}

Esegui i seguenti passaggi per risolvere il problema:
1. Per accedere all&#39;Utilità di configurazione del sistema, vai a **[!UICONTROL Start > Esegui]** e quindi inserisci **[!UICONTROL MSCONFIG]**.
1. Fai clic sul pulsante **[!UICONTROL Strumenti]** scorri verso il basso e seleziona **[!UICONTROL Modifica impostazioni UAC]**. Fai clic su **[!UICONTROL Launch]** per eseguire il comando in una nuova finestra.
1. Regolare il cursore sul livello di notifica Mai. Al termine, chiudere la finestra del comando e chiudere la finestra Configurazione di sistema.
1. Verifica che l&#39;impostazione del Registro di sistema per UAC sia impostata su 0 (zero). Esegui i seguenti passaggi per verificare:

   1. Microsoft® consiglia di eseguire il backup del registro prima di modificarlo. Per i passaggi dettagliati vedi [Come eseguire il backup e il ripristino del Registro di sistema in Windows](https://support.microsoft.com/en-us/help/322756).
   1. Apri l&#39;editor del Registro di sistema di Microsoft® Windows. Per aprire l&#39;editor del Registro di sistema, vai a Start > Esegui, digita regedit e fai clic su OK.
   1. Accedi a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assicurarsi che il valore di EnableLUA sia impostato su 0 (zero).
   1. Assicurare il valore di **EnableLUA** è impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudi l’editor del Registro di sistema.

1. Riavvia il computer.

## Si applica a {#appliesto}

Questa soluzione si applica ai seguenti elementi:
* AEM Forms sul server JEE
* AEM Forms sul server OSGi
