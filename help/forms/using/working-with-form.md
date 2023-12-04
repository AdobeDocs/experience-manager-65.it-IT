---
title: Utilizzo di un modulo
seo-title: Working with a Form
description: Visualizzare e aggiornare il modulo associato a un’attività o a un punto d’inizio nell’app AEM Forms
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Utilizzo di un modulo {#working-with-a-form}

Se un modulo è abilitato per la sincronizzazione nell’app Forms, viene scaricato e puoi utilizzarlo direttamente.

I moduli vengono scaricati nell’app e sono disponibili offline. Si supponga ad esempio di gestire una società bancaria e che un cliente riempia un&#39;applicazione sul sito. L’applicazione è un modulo adattivo che accetta informazioni dai clienti e le memorizza per la revisione. L’amministratore rivede il modulo e crea un modulo di verifica nell’istanza di authoring AEM. L’amministratore abilita la sincronizzazione del modulo con l’app AEM Forms. Se il modulo di verifica è disponibile nell’app AEM Forms, l’agente sul campo può utilizzare un dispositivo mobile per verificare i dettagli del cliente. Il dispositivo mobile si sincronizza con il server e il modulo di verifica viene caricato nell’app. L’agente sul campo può visitare il cliente, verificare i dettagli, salvare i dati come bozza o inviare il modulo di verifica. Il modulo viene sincronizzato con il server ogni volta che l&#39;app è online.

Per sincronizzare il modulo nell’app AEM Forms:

1. Nell’istanza di authoring, seleziona un modulo e fai clic su **Visualizza proprietà**.
1. Nella pagina delle proprietà, fai clic su **Avanzato.**
1. In Avanzate, abilita opzione: **Sincronizza con l’app AEM Forms**, e seleziona **Salva**.

Per sincronizzare più moduli, nell’istanza di authoring seleziona più moduli in Forms Manager e seleziona **Sincronizza con l’app AEM Forms**. Quando il modulo viene pubblicato, l’app AEM Forms può connettersi al server di pubblicazione e recuperare i moduli.

Se la sincronizzazione dell’app Android AFA (AEM Form Application) non riesce, effettua le seguenti operazioni per risolvere il problema di sincronizzazione:

1. Vai a **https://[server]:[porta]/system/console/configMgr**.
1. Cerca **[!UICONTROL Adobe Gestore autenticazione token Granite]** e fai clic su **[!UICONTROL Modifica]**.
1. Seleziona la **[!UICONTROL Nessuno]** dal menu a discesa per il **[!UICONTROL Attributo SameSite per il cookie token di accesso]** attributo.
1. Fai clic su **[!UICONTROL Salva]**.

![Sincronizza immagine con app AFA Android](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>Moduli supportati:
>
>* Moduli adattivi (senza caricamento lento)
>* Moduli per dispositivi mobili
>
>Gli allegati a livello di modulo non sono supportati nei moduli adattivi recuperati nell’app AEM Forms sincronizzata con il server AEM Forms OSGi. Gli utenti possono allegare file in un campo, se l’autore ha abilitato allegati a livello di campo al momento della creazione del modulo.


**Per aprire e aggiornare un modulo**

1. Per aprire una maschera, selezionare **[!UICONTROL Modulo]** nella schermata iniziale.
1. È possibile aggiornare i campi del modulo, aggiungere allegati, salvare come bozza e inviarlo.
