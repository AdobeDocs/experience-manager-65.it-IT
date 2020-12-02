---
title: Pubblicare cartelle su Brand Portal
seo-title: Pubblicare cartelle su Brand Portal
description: Scoprite come pubblicare e annullare la pubblicazione delle cartelle in Brand Portal.
seo-description: Scoprite come pubblicare e annullare la pubblicazione delle cartelle in Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 38%

---


# Pubblicare cartelle su Brand Portal{#publish-folders-to-brand-portal}

In qualità di amministratore di Adobe Experience Manager (AEM) Assets, puoi pubblicare risorse e cartelle nell’istanza  AEM Assets Brand Portal (o pianificare il flusso di lavoro di pubblicazione in una data/ora successiva) per la tua organizzazione. Tuttavia, è prima necessario integrare  AEM Assets con il Portale marchio. Per ulteriori dettagli, consulta [Configurare AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Dopo aver pubblicato una risorsa o una cartella, questa è disponibile per gli utenti in Brand Portal.

Se apportate modifiche successive alla risorsa o alla cartella originale in  AEM Assets, le modifiche non verranno applicate al Portale marchio finché non ripubblicate la risorsa o la cartella. Questa funzione garantisce che le modifiche in corso d’opera non siano disponibili in Brand Portal. Solo le modifiche approvate pubblicate da un amministratore sono infatti disponibili in Brand Portal.

## Pubblicare cartelle su Brand Portal {#publish-folders-to-brand-portal-1}

1. Dall&#39;interfaccia AEM Assets , passate il puntatore del mouse sulla cartella desiderata e selezionate l&#39;opzione **Pubblica** dalle azioni rapide.

   In alternativa, selezionate la cartella desiderata e seguite i passaggi successivi.

   ![publish2bp](assets/publish2bp.png)

1. **Pubblicare subito le cartelle**

   Per pubblicare le cartelle selezionate su Brand Portal, effettua una delle seguenti operazioni:

   * Dalla barra degli strumenti, seleziona **Pubblicazione rapida**. Dal menu, selezionate **Pubblica su Brand Portal**.

   * Dalla barra degli strumenti, seleziona **Gestisci pubblicazione**.
   1. In **Action** selezionare **Pubblica su Brand Portal**, in **Scheduling** selezionare **Now** e fare clic su **Avanti.**
   1. Conferma la selezione in **Ambito** e fai clic su **Pubblica su Brand Portal**.

   Viene visualizzato un messaggio per informare che la cartella è stata accodata per la pubblicazione su Brand Portal. Accedete all’interfaccia Brand Portal per visualizzare la cartella pubblicata.

   **Pubblicare le cartelle in un secondo momento**

   Per pianificare il flusso di lavoro di pubblicazione in Brand Portal delle cartelle di risorse in una data o ora successiva:

   1. Dopo aver selezionato le risorse o le cartelle da pubblicare, selezionate **Gestisci pubblicazione** dalla barra degli strumenti nella parte superiore.
   1. In **Action** selezionare **Pubblica su Brand Portal**, in **Scheduling** selezionare **Successivo**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Seleziona un valore per **Data di attivazione** e specifica l’ora. Fai clic su **Avanti**.
   1. Conferma la selezione in **Ambito**. Fai clic su **Avanti**.
   1. Specifica un titolo del flusso di lavoro in **Flussi di lavoro**. Fai clic su **Pubblica più tardi**.

      ![manageschedulepub](assets/manageschedulepub.png)



## Annullare la pubblicazione di cartelle su Brand Portal {#unpublish-folders-from-brand-portal}

Potete rimuovere qualsiasi cartella di risorse pubblicata nel Portale marchio annullandone la pubblicazione dall’istanza di AEM Author. Dopo l’annullamento della pubblicazione della cartella originale, la relativa copia non sarà più disponibile per gli utenti di Brand Portal.

Potete annullare la pubblicazione delle cartelle da Brand Portal in modo rapido oppure pianificarle in un secondo momento. Per annullare la pubblicazione delle cartelle di risorse su Brand Portal:

1. Dall&#39;interfaccia AEM Assets  nell&#39;istanza di AEM Author, selezionate la cartella da annullare la pubblicazione.

   ![publish2bp-1](assets/publish2bp.png)

1. Dalla barra degli strumenti, fare clic su **Gestisci pubblicazione**.

1. **Annulla pubblicazione da Brand Portal**

   Per annullare rapidamente la pubblicazione della cartella desiderata da Brand Portal:

   1. Dalla barra degli strumenti, seleziona **Gestisci pubblicazione**.
   1. In **Action** selezionare **Annulla pubblicazione da Brand Portal**, in **Scheduling** selezionare **Now** e fare clic su **Avanti.**
   1. Conferma la selezione in **Ambito** e fai clic su **Annulla pubblicazione su Brand Portal**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Annulla pubblicazione da Brand Portal in un secondo momento**

   Per pianificare la pubblicazione di una cartella da Brand Portal a una data e un’ora successive:

   1. Dalla barra degli strumenti, seleziona **Gestisci pubblicazione**.
   1. In **Action** selezionare **Annulla pubblicazione da Brand Portal**, quindi in **Scheduling** selezionare **Successivo**.
   1. Seleziona un valore per **Data di attivazione** e specifica l’ora. Fai clic su **Avanti**.
   1. Conferma la selezione in **Ambito** e fai clic su **Avanti**.
   1. Specifica un valore per **Titolo flusso di lavoro** in **Flussi di lavoro**. Fai clic su **Annulla pubblicazione più tardi.**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>La procedura per pubblicare/annullare la pubblicazione di una risorsa in/da Brand Portal è simile alla procedura corrispondente per una cartella.

