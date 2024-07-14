---
title: Utilizzo di un modulo
description: Visualizzare e aggiornare il modulo associato a un’attività o a un punto d’inizio nell’app AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Utilizzo di un modulo {#working-with-a-form}

Se un modulo è abilitato per la sincronizzazione nell’app Forms, viene scaricato e puoi utilizzarlo direttamente.

I moduli vengono scaricati nell’app e sono disponibili offline. Si supponga ad esempio di gestire una società bancaria e che un cliente riempia un&#39;applicazione sul sito. L’applicazione è un modulo adattivo che accetta informazioni dai clienti e le memorizza per la revisione. L’amministratore rivede il modulo e crea un modulo di verifica nell’istanza di authoring AEM. L’amministratore abilita la sincronizzazione del modulo con l’app AEM Forms. Se il modulo di verifica è disponibile nell’app AEM Forms, l’agente sul campo può utilizzare un dispositivo mobile per verificare i dettagli del cliente. Il dispositivo mobile si sincronizza con il server e il modulo di verifica viene caricato nell’app. L’agente sul campo può visitare il cliente, verificare i dettagli, salvare i dati come bozza o inviare il modulo di verifica. Il modulo viene sincronizzato con il server ogni volta che l&#39;app è online.

Per sincronizzare il modulo nell’app AEM Forms:

1. Nell&#39;istanza Autore, selezionare un modulo e fare clic su **Visualizza proprietà**.
1. Nella pagina delle proprietà, fare clic su **Avanzate.**
1. In Avanzate abilitare l&#39;opzione **Sincronizza con l&#39;app AEM Forms** e selezionare **Salva**.

Per sincronizzare più moduli, nell&#39;istanza di authoring selezionare più moduli in Gestione moduli e selezionare **Sincronizza con l&#39;app AEM Forms**. Quando il modulo viene pubblicato, l’app AEM Forms può connettersi al server di pubblicazione e recuperare i moduli.

Se la sincronizzazione dell’app Android AFA (AEM Form Application) non riesce, per risolvere il problema di sincronizzazione effettua le seguenti operazioni:

1. Vai a **https://[server]:[porta]/system/console/configMgr**.
1. Cerca il **[!UICONTROL gestore Adobe di autenticazione token Granite]** e fai clic su **[!UICONTROL Modifica]**.
1. Selezionare l&#39;opzione **[!UICONTROL Nessuno]** dal menu a discesa per l&#39;attributo **[!UICONTROL SameSite per l&#39;attributo cookie del token di accesso]**.
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

1. Per aprire un modulo, selezionare il **[!UICONTROL Modulo]** nella schermata iniziale.
1. È possibile aggiornare i campi del modulo, aggiungere allegati, salvare come bozza e inviarlo.
