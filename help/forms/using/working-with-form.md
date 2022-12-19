---
title: Uso di un modulo
seo-title: Working with a Form
description: Visualizza e aggiorna il modulo associato a un’attività o a un punto iniziale nell’app AEM Forms
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: eb71119474f03a969a721c792b6f1ac330f9dbf3
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Uso di un modulo {#working-with-a-form}

Se un modulo è abilitato per la sincronizzazione nell’app dei moduli, il modulo viene scaricato e puoi utilizzarlo direttamente.

I moduli vengono scaricati nell’app e sono disponibili offline. Ad esempio, si esegue un&#39;azienda bancaria e un cliente compila un&#39;applicazione sul sito. L’applicazione è un modulo adattivo che accetta le informazioni dei clienti e le memorizza per la revisione. L’amministratore rivede il modulo e crea un modulo di verifica nell’istanza AEM autore. L’amministratore abilita la sincronizzazione del modulo con l’app AEM Forms. Se il modulo di verifica è disponibile nell’app AEM Forms, l’agente di campo può utilizzare un dispositivo mobile per verificare i dettagli del cliente. Il dispositivo mobile si sincronizza con il server e il modulo di verifica viene caricato nell’app. L’agente del campo può visitare il cliente, verificare i dettagli, salvare i dati come bozza o inviare il modulo di verifica. Il modulo viene sincronizzato con il server ogni volta che l’app è online.

Per sincronizzare il modulo nell’app AEM Forms:

1. Nell’istanza di authoring, seleziona un modulo e fai clic su **Visualizza proprietà**.
1. Nella pagina delle proprietà, fai clic su **Avanzate.**
1. In Avanzate, abilita l&#39;opzione: **Sincronizzazione con l’app AEM Forms**, e tocca **Salva**.

Per sincronizzare più moduli, nell’istanza di authoring, seleziona più moduli in Forms Manager e tocca **Sincronizzazione con l’app AEM Forms**. Quando il modulo viene pubblicato, l’app AEM Forms può connettersi al server di pubblicazione e recuperare i moduli.

Se la sincronizzazione dell&#39;app Android AFA (AEM Form Application) non riesce, procedi come segue per risolvere il problema di sincronizzazione:

1. Vai a **https://[server]:[porta]/system/console/configMgr**.
1. Cerca il **[!UICONTROL Gestore autenticazione token di Granite Adobe]** e fai clic su **[!UICONTROL Modifica]**.
1. Seleziona la **[!UICONTROL Nessuno]** dal menu a discesa per **[!UICONTROL Attributo SameSite per il cookie login-token]** attributo.
1. Fai clic su **[!UICONTROL Salva]**.

![Sincronizza immagine con l’app Android AFA](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>Moduli supportati:
>
>* Moduli adattivi (senza caricamento lento)
>* Moduli mobili
>
>Gli allegati a livello di modulo non sono supportati nei moduli adattivi recuperati nell’app AEM Forms sincronizzati con il server OSGi di AEM Forms. Gli utenti possono allegare file in un campo se l’autore ha abilitato allegati a livello di campo al momento della creazione del modulo.


**Apertura e aggiornamento di un modulo**

1. Per aprire un modulo, toccare il pulsante **[!UICONTROL Modulo]** nella schermata iniziale.
1. È possibile aggiornare i campi del modulo, aggiungere allegati, salvare come bozza e inviarlo.
