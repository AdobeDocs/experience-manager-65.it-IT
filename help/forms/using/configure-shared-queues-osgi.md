---
title: Configurare le code condivise
seo-title: Configure shared queues
description: Scopri come utilizzare le code condivise per i flussi di lavoro incentrati su Forms su AEM Forms su OSGi.
seo-description: Learn how to use shared queues for Forms-centric workflows on AEM Forms on OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 72cd0594-8b5e-4d14-bc6f-bca26bae50f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# Condividere e richiedere l’accesso agli elementi della casella in entrata di un utente {#share-and-request-access}

Una coda è un elenco di elementi nella casella in entrata AEM un utente. Possono essere elementi assegnati a un utente o elementi condivisi con il gruppo di cui un utente è membro. Puoi accedere alla casella in entrata per visualizzare e intervenire sull’elemento in entrata. Ad esempio, condividi un elemento con un altro utente.

È inoltre possibile condividere gli elementi della casella in entrata con un altro utente. Una volta che un altro utente ha accesso agli elementi della casella in entrata, può richiedere e intraprendere le azioni appropriate sugli elementi condivisi. Allo stesso modo, puoi richiedere l’accesso agli elementi della casella in entrata ad altri utenti.

## Prerequisiti {#pre-requisites}

L&#39;utente connesso deve essere un membro del `workflow-users` gruppo. L&#39;utente può condividere gli elementi o richiedere l&#39;accesso agli elementi solo agli utenti a cui l&#39;utente connesso ha accesso autorizzazioni di lettura o solo agli utenti che hanno abilitato il profilo pubblico.

## Condividere uno o tutti gli elementi della casella in entrata con un altro utente

AEM casella in entrata consente di condividere con un altro utente uno o tutti gli elementi della casella in entrata.

### Condividi tutti gli elementi della casella in entrata

Per condividere tutti gli elementi di una casella in entrata con un altro utente, effettua le seguenti operazioni:

1. Accedi alla tua istanza AEM. Tocca ![Inbox](assets/bell.svg) icona e tocco **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della casella in entrata.
1. Tocca ![Selettore vista](assets/viewlist.svg) o ![Selettore vista](assets/calendar.svg) accanto all’icona **[!UICONTROL Crea]** pulsante e tocco **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Apri **[!UICONTROL Condividi]** nella finestra di dialogo impostazioni.
1. Immetti il nome di un utente nel **[!UICONTROL Concedere l’accesso agli elementi della Posta in arrivo]** casella di testo e tocca **[!UICONTROL Concessione]**. Ripeti il passaggio per aggiungere altri utenti. Tutti gli utenti con accesso ai tuoi elementi vengono visualizzati sotto la **Nome utente** sezione .
1. Tocca **[!UICONTROL Salva]**.

>[!NOTE]
>
>(Solo per gli elementi del flusso di lavoro incentrati su Forms) Attiva la **[Consenti condivisione degli assegnatari tramite condivisione della casella in entrata](aem-forms-workflow-step-reference.md)** opzione **Assegna attività** nel flusso di lavoro. Solo gli articoli che hanno abilitato la suddetta opzione vengono visualizzati ad altri utenti.

### Condividere singoli elementi

Per condividere un elemento della casella in entrata con un altro utente, effettua le seguenti operazioni:

1. Accedi alla tua istanza AEM. Tocca ![Inbox](assets/bell.svg) icona e tocco **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della casella in entrata.
1. Seleziona un elemento e tocca **[!UICONTROL Condividi]**. Viene visualizzata una finestra di dialogo.
1. Immetti il nome di un utente nella casella di testo Aggiungi utenti per condividere questo elemento e tocca **[!UICONTROL Aggiungi]**. Ripeti il passaggio per aggiungere altri utenti. Tutti gli utenti con accesso ai tuoi elementi vengono visualizzati sotto la **[!UICONTROL Nome utente]** sezione .
1. Tocca **[!UICONTROL Salva]**.


>[!NOTE]
>
>(Solo per gli elementi del flusso di lavoro incentrati su Forms) Attiva la **[Consentire agli assegnatari di condividere esplicitamente nella casella in entrata](aem-forms-workflow-step-reference.md)** opzione **Assegna attività** nel flusso di lavoro. Solo gli articoli che hanno abilitato la suddetta opzione vengono visualizzati ad altri utenti.

## Richiedi accesso a elementi della casella in entrata {#request-access}

È possibile richiedere l’accesso agli elementi della casella in entrata di un altro utente. Una volta concesso l&#39;accesso, puoi visualizzare, reclamare e intraprendere le azioni appropriate sugli elementi condivisi. Esegui le seguenti operazioni per richiedere l’accesso agli elementi della casella in entrata di un altro utente:

1. Accedi alla tua istanza AEM. Tocca ![Selettore vista](assets/bell.svg) icona e tocco **[!UICONTROL Visualizza tutto]**.
1. Tocca ![Selettore vista](assets/viewlist.svg) o ![Selettore vista](assets/calendar.svg) accanto all’icona **[!UICONTROL Crea]** pulsante e tocco **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Immetti il nome di un utente nel **[!UICONTROL Richiedere l’accesso agli elementi della casella in entrata dell’utente]** casella di testo e tocca **[!UICONTROL Richiesta]**. Viene inviata una richiesta all’utente e lo stato della richiesta viene visualizzato in base al nome dell’utente. Ripeti il passaggio per aggiungere altri utenti.
1. Tocca **[!UICONTROL Salva]**. La richiesta viene inviata come elemento in entrata agli utenti. L’utente può selezionare l’elemento e toccare Approva o Rifiuta per concedere o rifiutare l’accesso.


## Articoli di attestazione condivisi da altri utenti {#claim-items}

Puoi iniziare a lavorare su un elemento condiviso solo dopo averlo reclamato. Impedisce a più utenti di lavorare su un singolo elemento. Esegui i seguenti passaggi per richiedere un elemento:

1. Accedi alla tua istanza AEM. Tocca Casella in entrata ![Inbox](assets/bell.svg) icona e tocco **[!UICONTROL Visualizza tutto]**.
1. Tocca ![Solo contenuto](assets/railleft.svg) per aprire il selettore del filtro.
1. Tocca **[!UICONTROL Seleziona assegnatario]** elenco a discesa per visualizzare e selezionare gli utenti che hanno condiviso con te i loro elementi Casella in entrata.
1. Seleziona un elemento e tocca **[!UICONTROL Richiesta]**. L’elemento viene aggiunto alla Posta in arrivo.

## Rilascia articoli reclamati {#release-items}

È possibile lavorare su un elemento condiviso solo dopo averlo reclamato. Altri utenti non possono visualizzare o lavorare su elementi registrati. Se non puoi continuare a lavorare su un elemento, puoi rilasciarlo nuovamente nel pool.   Dopo aver rilasciato l’elemento, altri possono reclamare e lavorare sull’elemento:

Esegui i seguenti passaggi per rilasciare un elemento:

1. Accedi alla tua istanza AEM. Tocca Casella in entrata ![Inbox](assets/bell.svg) icona e tocco **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della casella in entrata.
1. Seleziona l’elemento da rilasciare e tocca **[!UICONTROL Cancella]**. L&#39;elemento viene aggiunto nuovamente al pool. Altri possono ora reclamare l&#39;articolo.

## Limitazioni  {#limitations}

* La condivisione di elementi con un gruppo non è supportata.
* La condivisione di attività di progetto non è supportata.
