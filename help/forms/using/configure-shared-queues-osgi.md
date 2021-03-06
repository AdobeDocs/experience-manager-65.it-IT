---
title: Configurare le code condivise
seo-title: Configurare le code condivise
description: Scopri come utilizzare le code condivise per i flussi di lavoro Forms-centric su  AEM Forms su OSGi.
seo-description: Scopri come utilizzare le code condivise per i flussi di lavoro Forms-centric su  AEM Forms su OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 1%

---


# Condivisione e richiesta dell&#39;accesso agli elementi Inbox di un utente {#share-and-request-access}

Una coda è un elenco di elementi AEM Casella in entrata di un utente. Possono essere elementi assegnati a un utente o elementi condivisi con il gruppo di cui un utente è membro. È possibile accedere alla Casella in entrata per visualizzare e intervenire sull&#39;elemento Posta in arrivo. Ad esempio, condividere un elemento con un altro utente.

È inoltre possibile condividere gli elementi Inbox con un altro utente. Quando un altro utente ha accesso agli elementi della Casella in entrata, può richiedere e intervenire sugli elementi condivisi. Allo stesso modo, potete richiedere l’accesso agli elementi della casella in entrata ad altri utenti.

## Prerequisiti {#pre-requisites}

L&#39;utente connesso deve essere membro del gruppo `workflow-users`. L&#39;utente può condividere elementi o richiedere l&#39;accesso agli elementi solo agli utenti a cui è stato effettuato l&#39;accesso, oppure solo agli utenti che hanno attivato il profilo pubblico.

## Condivisione di uno o tutti gli elementi della inbox con un altro utente

AEM Posta in arrivo consente di condividere con un altro utente uno o tutti gli elementi della inbox.

### Condivisione di tutti gli elementi della inbox

Per condividere tutti gli elementi di una inbox con un altro utente, effettuate le seguenti operazioni:

1. Accedete all&#39;istanza AEM. Toccate l&#39;icona ![Inbox](assets/bell.svg) e toccate **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della inbox.
1. Toccate l&#39;icona ![Selettore vista](assets/viewlist.svg) o ![Selettore vista](assets/calendar.svg) accanto al pulsante **[!UICONTROL Crea]** e toccate **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Aprite la scheda **[!UICONTROL Condividi]** nella finestra di dialogo delle impostazioni.
1. Immettete il nome di un utente nella casella di testo **[!UICONTROL Concedi l&#39;accesso agli elementi in entrata]** e toccate **[!UICONTROL Concedi]**. Ripetete il passaggio per aggiungere altri utenti. Tutti gli utenti con accesso ai vostri elementi vengono visualizzati nella sezione **Nome utente**.
1. Toccate **[!UICONTROL Salva]**.

>[!NOTE]
>
>(Solo per gli elementi del flusso di lavoro basati su Forms) Abilitare l&#39;opzione **[Consenti al cessionario di condividere tramite Inbox sharing](aem-forms-workflow-step-reference.md)** del passaggio **Assegna attività** nel flusso di lavoro. Solo gli elementi con l&#39;opzione sopra abilitata vengono visualizzati agli altri utenti.

### Condivisione di singoli elementi

Per condividere un elemento in entrata con un altro utente, effettuate le seguenti operazioni:

1. Accedete all&#39;istanza AEM. Toccate l&#39;icona ![Inbox](assets/bell.svg) e toccate **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della inbox.
1. Selezionate un elemento e toccate **[!UICONTROL Condividi]**. Viene visualizzata una finestra di dialogo.
1. Immettete il nome di un utente nella casella di testo Aggiungi utenti per condividere questo elemento e toccate **[!UICONTROL Aggiungi]**. Ripetete il passaggio per aggiungere altri utenti. Tutti gli utenti con accesso ai vostri elementi vengono visualizzati nella sezione **[!UICONTROL Nome utente]**.
1. Toccate **[!UICONTROL Salva]**.


>[!NOTE]
>
>(Solo per gli elementi del flusso di lavoro basati su Forms) Abilitare l&#39;opzione **[Consenti al cessionario di condividere in modo esplicito in Inbox](aem-forms-workflow-step-reference.md)** del passaggio **Assegna attività** nel flusso di lavoro. Solo gli elementi con l&#39;opzione sopra abilitata vengono visualizzati agli altri utenti.

## Richiedi accesso a elementi della casella in entrata {#request-access}

È possibile richiedere l&#39;accesso agli elementi Inbox di un altro utente. Una volta concesso l&#39;accesso, potete visualizzare, richiedere e intraprendere le azioni appropriate sugli elementi condivisi. Per richiedere l’accesso agli elementi Inbox di un altro utente, effettuate le seguenti operazioni:

1. Accedete all&#39;istanza AEM. Toccate l&#39;icona ![Visualizza selettore](assets/bell.svg) e toccate **[!UICONTROL Visualizza tutto]**.
1. Toccate l&#39;icona ![Selettore vista](assets/viewlist.svg) o ![Selettore vista](assets/calendar.svg) accanto al pulsante **[!UICONTROL Crea]** e toccate **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Immettete il nome di un utente nella casella di testo **[!UICONTROL Richiedi l&#39;accesso agli elementi in entrata dell&#39;utente]** e toccate **[!UICONTROL Request]**. Una richiesta viene inviata all’utente e lo stato della richiesta viene visualizzato rispetto al nome dell’utente. Ripetete il passaggio per aggiungere altri utenti.
1. Toccate **[!UICONTROL Salva]**. La richiesta viene inviata agli utenti come elemento Inbox. L&#39;utente può selezionare l&#39;elemento e toccare Approva o Rifiuta per concedere o rifiutare l&#39;accesso.


## Rivedere elementi condivisi da altri utenti {#claim-items}

Potete iniziare a lavorare su un elemento condiviso solo dopo averlo reclamato. Impedisce a più utenti di lavorare su un singolo elemento. Effettuate le seguenti operazioni per reclamare un elemento:

1. Accedete all&#39;istanza AEM. Toccare l&#39;icona Inbox ![Inbox](assets/bell.svg) e toccare **[!UICONTROL Visualizza tutto]**.
1. Toccate l&#39;icona ![Solo contenuto](assets/railleft.svg) per aprire il selettore del filtro.
1. Toccate il menu a discesa **[!UICONTROL Seleziona assegnatario]** per visualizzare e selezionare gli utenti che hanno condiviso con voi i loro elementi in entrata.
1. Selezionare un elemento e toccare **[!UICONTROL Claim]**. L’elemento viene aggiunto alla casella in entrata.

## Rilascia gli elementi richiesti {#release-items}

Potete lavorare su un elemento condiviso solo dopo averlo reclamato. Altri utenti non possono visualizzare o utilizzare gli elementi richiesti. Se non potete continuare a lavorare su un elemento, potete rilasciarlo nuovamente nel pool.   Dopo aver rilasciato l’elemento, altri possono reclamare e lavorare sull’elemento:

Per rilasciare un elemento, effettuate le seguenti operazioni:

1. Accedete all&#39;istanza AEM. Toccare l&#39;icona Inbox ![Inbox](assets/bell.svg) e toccare **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della inbox.
1. Selezionare l&#39;elemento da rilasciare e toccare **[!UICONTROL UnClaim]**. L&#39;elemento viene aggiunto nuovamente al pool. Altri possono ora reclamare l’elemento.

## Limitazioni  {#limitations}

* La condivisione di elementi con un gruppo non è supportata.
* La condivisione di attività di progetto non è supportata.
