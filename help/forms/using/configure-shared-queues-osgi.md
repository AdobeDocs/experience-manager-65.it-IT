---
title: Configurare le code condivise
description: Scopri come utilizzare le code condivise per flussi di lavoro incentrati su Forms su AEM Forms su OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 72cd0594-8b5e-4d14-bc6f-bca26bae50f2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, OSGI
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---

# Condividere e richiedere l’accesso agli elementi della casella in entrata di un utente {#share-and-request-access}

Una coda è un elenco di elementi nella casella in entrata AEM di un utente. Possono essere elementi assegnati a un utente o elementi condivisi con il gruppo di cui un utente è membro. Puoi accedere alla tua casella in entrata per visualizzare e intervenire sull’elemento della casella in entrata. Ad esempio, condividere un elemento con un altro utente.

Puoi anche condividere gli elementi della tua casella in entrata con un altro utente. Una volta che un altro utente ha accesso agli elementi della tua casella in entrata, può richiedere e intraprendere azioni appropriate sugli elementi condivisi. Analogamente, è possibile richiedere l&#39;accesso agli elementi della casella in entrata ad altri utenti.

## Prerequisiti {#pre-requisites}

L&#39;utente connesso deve essere membro di `workflow-users` gruppo. L’utente può condividere elementi o richiedere l’accesso agli elementi solo agli utenti per i quali ha eseguito l’accesso e per i quali dispone delle autorizzazioni di lettura oppure solo agli utenti per i quali è stato abilitato il profilo pubblico.

## Condividere un solo elemento della casella in entrata o tutti gli elementi di essa con un altro utente

Casella in entrata AEM consente di condividere un singolo o tutti gli elementi della casella in entrata con un altro utente.

### Condividi tutti gli elementi casella in entrata

Per condividere tutti gli elementi di una casella in entrata con un altro utente, effettua le seguenti operazioni:

1. Accedi all’istanza AEM. Seleziona la ![Casella in entrata](assets/bell.svg) e seleziona **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della casella in entrata.
1. Seleziona la ![Selettore vista](assets/viewlist.svg) o ![Selettore vista](assets/calendar.svg) accanto al simbolo **[!UICONTROL Crea]** e seleziona **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Apri **[!UICONTROL Condividi]** nella finestra di dialogo delle impostazioni.
1. Immetti il nome di un utente in **[!UICONTROL Concedi l’accesso agli elementi della tua casella in entrata]** e selezionare **[!UICONTROL Concedi]**. Ripeti il passaggio per aggiungere altri utenti. Tutti gli utenti con accesso agli elementi vengono visualizzati sotto **Nome utente** sezione.
1. Seleziona **[!UICONTROL Salva]**.

>[!NOTE]
>
>(Solo per elementi del flusso di lavoro incentrati su Forms) Abilita **[Consenti all’assegnatario di condividere tramite la casella in entrata](aem-forms-workflow-step-reference.md)** opzione del **Assegna attività** nel flusso di lavoro. Solo gli elementi per i quali è attivata l&#39;opzione sopra indicata vengono visualizzati agli altri utenti.

### Condividere singoli elementi

Per condividere un elemento della Casella in entrata con un altro utente, effettuare le seguenti operazioni:

1. Accedi all’istanza AEM. Seleziona la ![Casella in entrata](assets/bell.svg) e seleziona **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della casella in entrata.
1. Seleziona un elemento e seleziona **[!UICONTROL Condividi]**. Viene visualizzata una finestra di dialogo.
1. Immettere il nome di un utente nella casella di testo Aggiungi utenti per condividere l&#39;elemento e selezionare **[!UICONTROL Aggiungi]**. Ripeti il passaggio per aggiungere altri utenti. Tutti gli utenti con accesso agli elementi vengono visualizzati sotto **[!UICONTROL Nome utente]** sezione.
1. Seleziona **[!UICONTROL Salva]**.


>[!NOTE]
>
>(Solo per elementi del flusso di lavoro incentrati su Forms) Abilita **[Consenti all’assegnatario di condividere in modo esplicito nella casella in entrata](aem-forms-workflow-step-reference.md)** opzione del **Assegna attività** nel flusso di lavoro. Solo gli elementi per i quali è attivata l&#39;opzione sopra indicata vengono visualizzati agli altri utenti.

## Richiedi accesso a elementi casella in entrata {#request-access}

Puoi richiedere l’accesso agli elementi della casella in entrata di un altro utente. Una volta concesso l’accesso, puoi visualizzare, richiedere e intraprendere azioni appropriate sugli elementi condivisi. Per richiedere l’accesso agli elementi della casella in entrata di un altro utente, effettua le seguenti operazioni:

1. Accedi all’istanza AEM. Seleziona la ![Selettore vista](assets/bell.svg) e seleziona **[!UICONTROL Visualizza tutto]**.
1. Seleziona la ![Selettore vista](assets/viewlist.svg) o ![Selettore vista](assets/calendar.svg) accanto al simbolo **[!UICONTROL Crea]** e seleziona **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Immetti il nome di un utente in **[!UICONTROL Richiedi accesso agli elementi della casella in entrata dell&#39;utente]** e selezionare **[!UICONTROL Richiesta]**. Viene inviata una richiesta all’utente, il cui stato viene visualizzato in base al nome dell’utente. Ripeti il passaggio per aggiungere altri utenti.
1. Seleziona **[!UICONTROL Salva]**. La richiesta viene inviata come elemento della casella in entrata agli utenti. L’utente può selezionare l’elemento e selezionare Approva o Rifiuta per concedere o rifiutare l’accesso.


## Richieste di rimborso condivise da altri utenti {#claim-items}

Puoi iniziare a lavorare su un elemento condiviso solo dopo averlo richiesto. Impedisce a più utenti di lavorare su un singolo elemento. Per richiedere un oggetto, effettuare le seguenti operazioni:

1. Accedi all’istanza AEM. Seleziona la casella in entrata ![Casella in entrata](assets/bell.svg) e seleziona **[!UICONTROL Visualizza tutto]**.
1. Seleziona la ![Solo contenuto](assets/railleft.svg) per aprire il selettore dei filtri.
1. Seleziona la **[!UICONTROL Seleziona assegnatario]** per visualizzare e selezionare gli utenti che hanno condiviso con te i propri elementi della casella in entrata.
1. Seleziona un elemento e seleziona **[!UICONTROL Richiesta di rimborso]**. L&#39;elemento viene aggiunto alla Posta in arrivo.

## Rilascia articoli richiesti {#release-items}

Puoi lavorare su un elemento condiviso solo dopo averlo richiesto. Gli altri utenti non possono visualizzare o lavorare su un oggetto che hai richiesto. Se non è possibile continuare a lavorare su un elemento, è possibile rilasciarlo nuovamente nel pool.   Dopo il rilascio dell&#39;oggetto, gli altri utenti potranno richiedere e lavorare sull&#39;oggetto:

Per rilasciare un elemento, effettua le seguenti operazioni:

1. Accedi all’istanza AEM. Seleziona la casella in entrata ![Casella in entrata](assets/bell.svg) e seleziona **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della casella in entrata.
1. Seleziona l’elemento da rilasciare e fai clic su **[!UICONTROL Annulla richiesta di rimborso]**. L&#39;elemento viene aggiunto nuovamente al pool. Gli altri utenti possono richiedere l&#39;oggetto.

## Limitazioni {#limitations}

* La condivisione di elementi con un gruppo non è supportata.
* La condivisione delle attività del progetto non è supportata.
