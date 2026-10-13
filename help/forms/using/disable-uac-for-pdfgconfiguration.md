---
title: Disabilita Controllo dell’account utente per la configurazione PDFG applicabile sia a JEE che a OSGI
description: Scopri come disabilitare il Controllo dell’account utente per la configurazione PDFG per correggere la conversione da Word a PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 8%
---
# Impossibile convertire file Word o Excel in PDF sul server Windows {#unable-to-convert-word-excel-files-PDF}

## Problema {#issue}

Quando l&#39;utente cerca di convertire i file Word o Excel in PDF su Microsoft® Windows Server, si verifica il seguente errore:

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
   1. Accedi a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verificare che il valore di EnableLUA sia impostato su 0 (zero).
   1. Assicurarsi che il valore di **EnableLUA** sia impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudi l’editor del Registro di sistema.

1. Riavvia il computer.

## Si applica a {#appliesto}

Questa soluzione è applicabile ad AEM Forms su JEE Server e AEM Forms su OSGi Server.
