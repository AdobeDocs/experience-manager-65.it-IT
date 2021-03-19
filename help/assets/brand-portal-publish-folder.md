---
title: Pubblicare cartelle su Brand Portal
seo-title: Pubblicare cartelle su Brand Portal
description: Scopri come pubblicare e annullare la pubblicazione delle cartelle su Brand Portal.
seo-description: Scopri come pubblicare e annullare la pubblicazione delle cartelle su Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: Professionista
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 38%

---


# Pubblicare cartelle su Brand Portal{#publish-folders-to-brand-portal}

In qualità di amministratore di Adobe Experience Manager (AEM) Assets, puoi pubblicare risorse e cartelle nell’istanza di AEM Assets Brand Portal (o pianificare il flusso di lavoro di pubblicazione in una data/ora successiva) per la tua organizzazione. Tuttavia, devi prima integrare AEM Assets con Brand Portal. Per ulteriori dettagli, consulta [Configurare AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Dopo aver pubblicato una risorsa o una cartella, questa è disponibile per gli utenti in Brand Portal.

Se apporti modifiche successive alla risorsa o alla cartella originale in AEM Assets, le modifiche non verranno applicate in Brand Portal finché non ripubblichi la risorsa o la cartella. Questa funzione garantisce che le modifiche in corso d’opera non siano disponibili in Brand Portal. Solo le modifiche approvate pubblicate da un amministratore sono infatti disponibili in Brand Portal.

## Pubblicare cartelle su Brand Portal {#publish-folders-to-brand-portal-1}

1. Nell’interfaccia di AEM Assets, passa il puntatore del mouse sulla cartella desiderata e seleziona l’opzione **Pubblica** dalle azioni rapide.

   In alternativa, seleziona la cartella desiderata e segui i passaggi successivi.

   ![publish2bp](assets/publish2bp.png)

1. **Pubblicare subito le cartelle**

   Per pubblicare le cartelle selezionate su Brand Portal, effettua una delle seguenti operazioni:

   * Dalla barra degli strumenti, seleziona **Pubblicazione rapida**. Dal menu, seleziona **Pubblica su Brand Portal**.

   * Dalla barra degli strumenti, seleziona **Gestisci pubblicazione**.
   1. In **Azione** seleziona **Pubblica su Brand Portal**, in **Pianificazione** seleziona **Ora** e fai clic su **Avanti.**
   1. Conferma la selezione in **Ambito** e fai clic su **Pubblica su Brand Portal**.

   Viene visualizzato un messaggio per informare che la cartella è stata accodata per la pubblicazione su Brand Portal. Accedi all’interfaccia di Brand Portal per visualizzare la cartella pubblicata.

   **Pubblicare le cartelle in un secondo momento**

   Per pianificare il flusso di lavoro per la pubblicazione su Brand Portal delle cartelle di risorse in una data o un’ora successiva:

   1. Dopo aver selezionato le risorse o le cartelle da pubblicare, seleziona **Gestisci pubblicazione** dalla barra degli strumenti in alto.
   1. In **Azione** seleziona **Pubblica su Brand Portal**, in **Pianificazione** seleziona **Più tardi**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Seleziona un valore per **Data di attivazione** e specifica l’ora. Fai clic su **Avanti**.
   1. Conferma la selezione in **Ambito**. Fai clic su **Avanti**.
   1. Specifica un titolo del flusso di lavoro in **Flussi di lavoro**. Fai clic su **Pubblica più tardi**.

      ![manageschedulepub](assets/manageschedulepub.png)



## Annullare la pubblicazione di cartelle su Brand Portal {#unpublish-folders-from-brand-portal}

Per rimuovere una cartella di risorse pubblicata su Brand Portal, annullane la pubblicazione dall’istanza di AEM Author. Dopo l’annullamento della pubblicazione della cartella originale, la relativa copia non sarà più disponibile per gli utenti di Brand Portal.

Puoi annullare rapidamente la pubblicazione delle cartelle su Brand Portal oppure programmarle per una data e un’ora successive. Per annullare la pubblicazione delle cartelle di risorse su Brand Portal:

1. Dall’interfaccia di AEM Assets nell’istanza di AEM Author, seleziona la cartella di cui vuoi annullare la pubblicazione.

   ![publish2bp-1](assets/publish2bp.png)

1. Dalla barra degli strumenti, fai clic su **Gestisci pubblicazione**.

1. **Annullare subito la pubblicazione su Brand Portal**

   Per annullare rapidamente la pubblicazione della cartella desiderata su Brand Portal:

   1. Dalla barra degli strumenti, seleziona **Gestisci pubblicazione**.
   1. In **Azione** seleziona **Annulla pubblicazione su Brand Portal**, in **Pianificazione** seleziona **Ora** e fai clic su **Avanti.**
   1. Conferma la selezione in **Ambito** e fai clic su **Annulla pubblicazione su Brand Portal**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Annulla pubblicazione su Brand Portal in un secondo momento**

   Per pianificare la pubblicazione di una cartella da Brand Portal in una data e un’ora successive:

   1. Dalla barra degli strumenti, seleziona **Gestisci pubblicazione**.
   1. In **Azione** seleziona **Annulla pubblicazione su Brand Portal**, quindi in **Pianificazione** seleziona **Più tardi**.
   1. Seleziona un valore per **Data di attivazione** e specifica l’ora. Fai clic su **Avanti**.
   1. Conferma la selezione in **Ambito** e fai clic su **Avanti**.
   1. Specifica un valore per **Titolo flusso di lavoro** in **Flussi di lavoro**. Fai clic su **Annulla pubblicazione più tardi.**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>La procedura per pubblicare/annullare la pubblicazione di una risorsa su/da Brand Portal è simile alla procedura di corresponsing per una cartella.

