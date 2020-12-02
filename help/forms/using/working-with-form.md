---
title: Uso di un modulo
seo-title: Uso di un modulo
description: Visualizzare e aggiornare il modulo associato a un'attività o a un punto iniziale nell'app  AEM Forms
seo-description: Visualizzare e aggiornare il modulo associato a un'attività o a un punto iniziale nell'app  AEM Forms
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# Uso di un modulo {#working-with-a-form}

Se un modulo è abilitato per la sincronizzazione nell&#39;app dei moduli, il modulo viene scaricato e l&#39;utente può utilizzarlo direttamente.

I moduli vengono scaricati nell&#39;app e sono disponibili offline. Ad esempio, si esegue un&#39;azienda bancaria e un cliente compila un&#39;applicazione sul sito. L&#39;applicazione è un modulo adattivo che accetta le informazioni dei clienti e le memorizza per la revisione. L&#39;amministratore rivede il modulo e crea un modulo di verifica nell&#39;istanza AEM autore. L&#39;amministratore abilita la sincronizzazione del modulo con  app AEM Forms. Se il modulo di verifica è disponibile &#39;app AEM Forms, l&#39;agente del campo può utilizzare un dispositivo mobile per verificare i dettagli del cliente. Il dispositivo mobile si sincronizza con il server e il modulo di verifica viene caricato nell&#39;app. L&#39;agente del campo può visitare il cliente, verificare i dettagli, salvare i dati come bozza o inviare il modulo di verifica. Il modulo viene sincronizzato con il server ogni volta che l&#39;app è online.

Per sincronizzare il modulo &#39;app AEM Forms:

1. Nell&#39;istanza di creazione, selezionare un modulo e fare clic su **Visualizza proprietà**.
1. Nella pagina delle proprietà fare clic su **Avanzate.**
1. In Avanzate, abilita opzione: **Sincronizza con  AEM Forms App** e tocca **Salva**.

Per sincronizzare più moduli, nell&#39;istanza di creazione selezionare più moduli in Forms Manager e toccare **Sincronizza con  AEM Forms App**. Quando il modulo viene pubblicato, l&#39;app AEM Forms  può connettersi al server di pubblicazione e recuperare i moduli.

>[!NOTE]
>
>Moduli supportati:
>
>* Moduli adattivi (senza caricamento pigro)
>* Moduli mobili

>
>
Gli allegati a livello di modulo non sono supportati nei moduli adattivi recuperati nell&#39;app AEM Forms  sincronizzata con  server AEM Forms OSGi. Gli utenti possono allegare file a un campo, se l&#39;autore ha attivato gli allegati a livello di campo al momento della creazione del modulo.

**Apertura e aggiornamento di un modulo**

1. Per aprire un modulo, toccate il modulo nella schermata iniziale.
1. È possibile aggiornare i campi del modulo, aggiungere allegati, salvare come bozza e inviarlo.
