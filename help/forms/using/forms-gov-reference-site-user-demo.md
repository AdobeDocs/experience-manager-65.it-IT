---
title: Procedura dettagliata sul sito di riferimento We.Gov
seo-title: Procedura dettagliata sul sito di riferimento We.Gov
description: Utilizza utenti e gruppi fittizi per eseguire attività AEM Forms tramite il pacchetto dimostrativo We.Gov.
seo-description: Utilizza utenti e gruppi fittizi per eseguire attività AEM Forms tramite il pacchetto dimostrativo We.Gov.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Procedura dettagliata sul sito di riferimento We.Gov{#we-gov-reference-site-walkthrough}

## Prerequisiti {#pre-requisites}

Configurate il sito di riferimento come descritto in [Impostazione e configurazione del sito](../../forms/using/forms-install-configure-gov-reference-site.md)di riferimento We.Gov.

## Storia utente {#user-story}

* AEM Forms

   * Acquisizione dati
   * Integrazione dei dati (MS Dynamics)
   * Adobe Sign

* Flusso di lavoro
* Comunicazione con i clienti

   * Stampa canale
   * Canale web

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

Il pacchetto dimostrativo We.Gov include i seguenti utenti fittizi incorporati:

* **Aya Tan**: Cittadino idoneo a un servizio da un ente governativo

![Utente fittizio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Agenzia governativa Business Analytics

![Utente fittizio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: We.Gov Agenzia CX

![Utente fittizio](/help/forms/using/assets/camila_santos.png)

Sono inclusi anche i seguenti gruppi:

* **Utenti Di We.Gov Forms**

   * George Lang (membro)
   * Camila Santos (membro)

* **Utenti We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)
   * Aya Tan (membro)

### Legenda dei termini della panoramica della demo {#demo-overview-terms-legend}

1. **Impersona**: Utenti e gruppi definiti nella demo di AEM.
1. **Pulsante**: Rettangolo colorato o freccia cerchiata per la navigazione.
1. **Fate clic**: Per eseguire un&#39;azione nel brano dell&#39;utente.
1. **Collegamenti**: Situato nella parte superiore del menu principale nel sito We.Gov.
1. **Istruzioni** utente: Una serie di passaggi numerici da seguire per navigare nel racconto dell&#39;utente.
1. **Portale** moduli: *https://&lt;aemserver>:&lt;porta>/content/we-gov/formsportal.html*
1. **Vista** mobile:We.Gov utente per replicare una visualizzazione mobile con un browser ridimensionato.
1. **Vista** desktop: L&#39;utente We.gov può visualizzare la dimostrazione su un computer portatile o desktop.
1. **Modulo** pre-screener: Modulo sulla home page del sito We.Gov.
1. **Modulo** adattivo: Modulo di richiesta di iscrizione per la demo di We.gov.

   *https://&lt;aemserver>:&lt;porta>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Sito** Adobe We.Gov: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. **Adobe Inbox**: Posizione dell’icona [Bell nella barra dei menu principale nella parte posteriore] di AEM.

   *https://&lt;aemserver>:&lt;porta>/aem/start.html*

1. **Client** e-mail: Metodo preferito per visualizzare le e-mail (Gmail, Outlook)
1. **CTA**: Invito all&#39;azione
1. **Naviga**: Per individuare un punto di riferimento specifico nella pagina del browser.

## Demo della vista mobile {#mobile-view-demo}

**Questa sezione deve essere eseguita prima della dimostrazione.**

**Istruzioni utente:**

1. Passa a: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Effettua l’accesso con:

   1. **Utente**: aya.tan
   1. **Password**:password

1. Ridimensionate nuovamente la finestra del browser o utilizzate l&#39;emulatore del browser per replicare le dimensioni di un dispositivo mobile.

### Aya User Story (sito web We.Gov) {#aya-user-story-we-gov-website}

![Utente fittizio](/help/forms/using/assets/aya_tan_new-1.png)

**Questa sezione**: Aya è un cittadino. Ha sentito da un&#39;amica che potrebbe essere idonea a ricevere un Servizio da un&#39;agenzia governativa. Aya naviga sul sito Web We.Gov dal suo cellulare per saperne di più sui servizi a cui è idonea.

### Aya User Story (Pre-screener di We.Gov) {#aya-user-story-we-gov-pre-screener}

Aya risponde ad alcune domande per confermare la sua idoneità compilando un breve modulo adattivo sul suo cellulare.

**Istruzioni utente:**

1. Effettuare una selezione in ciascun campo a discesa.

   1. Nota: Se l’utente guadagna più di $200.000/anno, non è idoneo.

1. Fare clic su &quot;**Sono idoneo?**” pulsante.
1. Fare clic sul pulsante &quot;**Applica ora**&quot; per proseguire.

   ![Collegamento Applica ora](/help/forms/using/assets/apply_now_link.png)

### Storia utente Aya (modulo adattivo We.Gov) {#aya-user-story-we-gov-adaptive-form}

Aya scopre di essere idonea e inizia a compilare la sua applicazione per richiedere il servizio sul suo dispositivo mobile.

È necessario rivedere alcuni documenti a casa prima di poter completare l&#39;applicazione di richiesta del servizio. Salva ed esce dall&#39;applicazione.

**Istruzioni utente:**

1. Compila i campi delle informazioni di base, i campi e i menu a discesa seguenti sono obbligatori:

   1. Informazioni di base

      1. Nome
      1. Secondo nome
      1. Cognome
      1. Nome preferito
      1. DOB
      1. Genere
   1. Informazioni di contatto

      1. Indirizzo
      1. Città
      1. Numero di telefono
      1. CAP
      1. E-mail
      1. Stadio
   1. Stato Marziale

      1. Stato famiglia



1. Utilizzate la seguente logica **** dinamica per mostrare la funzione dinamica utilizzando il menu a discesa Stato **** famiglia:

   1. **Singolo**: Mostra il pannello di collegamento successivo
   1. **Sposato**: Mostra pannello familiare
   1. **Divorziato**: Mostra il pannello di collegamento successivo
   1. **Vedovo**: Mostra il pannello di collegamento successivo
   1. **Hai dei figli?**: (Sì/No) pulsante di scelta per visualizzare il pannello figlio dipendente.

      1. (Aggiungi/Rimuovi) per aggiungere o rimuovere più pannelli figlio dipendenti.

1. Fate clic sulla freccia destra nella barra dei menu grigia.
1. Fate clic sul pulsante Salva in basso.

   ![Dettagli modulo adattivo](/help/forms/using/assets/adaptive_form.png)

## Demo desktop {#desktop-demo}

**** Questa sezione: Tornando a casa, Aya ha trovato le informazioni necessarie e riprende l&#39;applicazione dal suo desktop. Aya passa al portale dei moduli online per riprendere l&#39;applicazione. Con una semplice personalizzazione, le agenzie possono anche generare automaticamente e inviare via e-mail un collegamento per riprendere l&#39;applicazione.

### Storia utente Aya (modulo adattivo continuo) {#aya-user-story-continued-adaptive-form}

**Istruzioni utente:**

1. Andate a *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Dalla barra di navigazione, selezionate &quot;**Online Services**&quot;.
1. Nel pannello &quot;Bozze di moduli&quot;, selezionare l&#39;esistente &quot;Iscrizione applicazione per benefici sanitari&quot;.

   ![Domanda di iscrizione per benefici per la salute](/help/forms/using/assets/enrollment_application.png)

   L&#39;aspetto e la sensazione sono gli stessi, e non ha bisogno di reimmettere dati.

   **Istruzioni utente:**

1. Fate clic su CTA cerchio destro per passare alla sezione successiva.

   ![CTA cerchio RIght](/help/forms/using/assets/right_circle_cta_new.png)

   Il modulo viene compilato fino al punto dell&#39;ultima voce di Aya. Aya ha inserito tutte le sue informazioni ed è pronta a inviare.

   ![Invio del modulo adattivo](/help/forms/using/assets/submit_adaptive_form.png)

   Dopo l&#39;invio, Aya riceve un&#39;e-mail che apre ed è pronta a firmare elettronicamente con Adobe Sign.

**Istruzioni utente:**

1. Dopo l’invio viene visualizzata una pagina di ringraziamento.
1. Accedi al client e-mail e trova il messaggio e-mail di Adobe Sign.
1. Fare clic sul collegamento ad Adobe Sign.

   ![Collegamento Adobe Sign](/help/forms/using/assets/adobe_sign_link.png)

**Istruzioni utente:**

1. Selezionare la casella &quot;**Sono d&#39;accordo**&quot;.
1. Fate clic su &quot;**Accetto**&quot;.
1. Scorrete fino in fondo al documento rivisto.
1. Fare clic sulla scheda evidenziata gialla per firmare il documento.

   ![Firmare il documento](/help/forms/using/assets/sign_document_new.png) ![Firmare il documento di prova](/help/forms/using/assets/sign_test_document.png)

## Agente governativo (George) {#government-agent-george}

![Agente governativo George](/help/forms/using/assets/george_lang-1.png)

**** Questa sezione: George è un analista d&#39;affari dell&#39;agenzia governativa Aya, che chiede un servizio. George dispone di un&#39;unica dashboard in cui può vedere tutte le applicazioni di richiesta di servizio che gli sono state assegnate per la revisione.

### George User Story (inbox AEM) {#george-user-story-aem-inbox}

**Istruzioni utente:**

1. Andate a *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Fate clic sull&#39;icona dell&#39;utente (nell&#39;angolo in alto a destra) e utilizzate &quot;**Disconnetti**&quot;, oppure l&#39;opzione di menu &quot;**Impersona come**&quot; se avete attualmente eseguito l&#39;accesso con un utente amministrativo.

   1. Effettua l’accesso con:

      1. **** Utente: george.lang
      1. **** Password:password
   1. O Impersona:

      1. Digitare &quot;**George**&quot; nel campo &quot;**Impersonate as**&quot;.

      1. Fare clic su OK per impersonare.


1. Dall’angolo in alto a destra, fate clic sull’icona Notifica (campana).
1. Fare clic su &quot;**Visualizza tutto**&quot; per passare alla casella in entrata.
1. Dalla casella in entrata, aprire l&#39;ultima operazione &quot;**Health Benefits Application Review**&quot;.

   ![Revisione dell&#39;applicazione dei vantaggi per la salute](/help/forms/using/assets/health_benefits.png)

### George User Story (inbox AEM e MS Dynamics) {#george-user-story-aem-inbox-and-ms-dynamics}

Grazie alle integrazioni di dati e ai flussi di lavoro automatizzati, viene visualizzata l&#39;applicazione di Aya, insieme a un record CRM generato automaticamente al momento dell&#39;invio dei dati.

**Istruzioni utente:**

1. Aprire ed esaminare il modulo adattivo di sola lettura.
1. Fare clic sul pulsante &quot;**Open MS Dynamics**&quot; per aprire il record MS Dynamics in una nuova finestra.
1. In CRM è possibile vedere tutte le informazioni possono essere aggiornate

   1. Facoltativamente, aggiungi alcune note di revisione direttamente in Dynamics.

1. Chiudete e tornate alla Casella in entrata AEM.

   ![Record MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### George User Story (torna alla inbox di AEM) {#george-user-story-back-to-aem-inbox}

George approva l’applicazione di Aya e grazie a un flusso di lavoro automatizzato esistente, ad Aya viene inviato anche un messaggio e-mail di conferma.

**Istruzioni utente:**

1. Andate in alto a sinistra e fate clic su &quot;**Approva**&quot; per approvare l&#39;applicazione.
1. Nella modalità, potete lasciare un messaggio per il lead CX.
1. Fate clic su Fine.
1. (Ruolo cittadino) Aprite il client di posta elettronica per visualizzare l’e-mail inviata ad Aya.

   ![Visualizza l&#39;e-mail inviata ad Aya](/help/forms/using/assets/email_client.png)

## Piombo CX (Camila) {#cx-lead-camila}

![Camila (CX lead)](/help/forms/using/assets/camila_santos-1.png)

**** Questa sezione: Camila il lead CX ha creato una telefonata di benvenuto con Aya per spiegare come utilizzare i servizi governativi per i quali è stata approvata.

### Storia utente di Camila (inbox AEM e MS Dynamics) {#camila-user-story-aem-inbox-ms-dynamics}

**Istruzioni utente:**

1. Andate a *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Fate clic sull&#39;icona dell&#39;utente (nell&#39;angolo in alto a destra) e utilizzate &quot;**Disconnetti**&quot;, oppure l&#39;opzione di menu &quot;**Impersona come**&quot; se avete attualmente eseguito l&#39;accesso con un utente amministrativo.

   1. Effettua l’accesso con:

      1. **Utente**: camila.santos
      1. **Password**:password
   1. O Impersona:

      1. Digitare &quot;**Camila**&quot; nel campo &quot;**Impersonate as**&quot;.

      1. Fare clic su OK per impersonare.


1. Dall’angolo in alto a destra, fate clic sull’icona Notifica (campana).
1. Fare clic su &quot;**Visualizza tutto**&quot; per passare alla casella in entrata.
1. Dalla casella in entrata, aprire l&#39;ultima operazione &quot;**Nuova approvazione** contatto&quot;.

   ![Nuova approvazione contatto](/help/forms/using/assets/new_contact_approval.png)

   **Istruzioni utente:**

1. Aprire ed esaminare il modulo adattivo di sola lettura.
1. Fare clic sul pulsante &quot;**Open MS Dynamics**&quot; per aprire il record MS Dynamics in una nuova finestra.
1. In CRM è possibile vedere tutte le informazioni possono essere aggiornate

   1. Facoltativamente, aggiungi una nuova attività di chiamata direttamente in Dynamics.
   1. Aprite la sezione &quot;**Attività**&quot;.
   1. Fate clic sull&#39;opzione &quot;**Nuova chiamata** telefonica&quot;.
   1. Aggiungete i dettagli della chiamata telefonica.
   1. Salvare e chiudere la finestra.

1. In AEM, andate in alto a sinistra e fate clic su &quot;**Invia**&quot; per inviare l’applicazione.
1. Nella finestra modale puoi lasciare un messaggio.
1. Fate clic su Fine.

   ![Scheda](/help/forms/using/assets/activities_tab.png) Attività ![Conferma nuovo contatto](/help/forms/using/assets/confirm_new_contact.png)

## Welcome Kit Citizen (Aya) {#welcome-kit-citizen-aya}

**** Questa sezione: Aya riceve un messaggio e-mail contenente un collegamento a una comunicazione interattiva che riepiloga i vantaggi e include anche campi modulo da compilare. Con l&#39;indicazione dei vantaggi PDF allegata e collegamento alla lettera di comunicazione interattiva nella posta (con lo stesso tema/marchio della comunicazione interattiva).

### Aya User Story (client e-mail) {#aya-user-story-email-client}

**Istruzioni utente:**

1. Individuate e aprite il messaggio e-mail del kit di benvenuto.
1. Scorrete fino all’allegato PDF nella parte inferiore della pagina.
1. Fare clic per aprire l&#39;allegato PDF.
1. Scorri verso l&#39;alto nel client di posta elettronica e fai clic su &quot;**Visualizza kit di benvenuto online**&quot;.

   1. Viene aperta la versione per il canale Web dello stesso documento.

1. Per un riferimento rapido direttamente al PDF:

   *https://&lt;aemserver>:&lt;porta>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Per un riferimento rapido a IC direttamente:

   *https://&lt;aemserver>:&lt;porta>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Benvenuto Manuale](/help/forms/using/assets/welcome_benefits_handbook.png) sulle comunicazioni ![interattive](/help/forms/using/assets/interactive_communication.png)

## Renewal Promemoria Citizen (Aya) {#renewal-reminder-citizen-aya}

**** Questa sezione: Camila pianifica anche un promemoria di comunicazione così un anno dopo. (Procedura del flusso di lavoro che automatizza/esegue e invia per e-mail).

### Aya User Story (client e-mail) {#aya-user-story-email-client-1}

**Istruzioni utente:**

1. Andate al client di posta elettronica.
1. Individuate e aprite il messaggio e-mail di promemoria rinnovo.
1. Fare clic sul pulsante &quot;**Invia una nuova applicazione**&quot; per aprire il modulo adattivo.

   1. Questa sezione viene lasciata intenzionalmente vuota per supportare la precompilazione dei dati nella fase 2.
   ![E-mail promemoria rinnovo](/help/forms/using/assets/renewal_reminder_email.png)

## Lead CX di Analytics (Camila) {#analytics-cx-lead-camila}

**** Questa sezione: Camila passa a un dashboard in cui può vedere i KPI dell&#39;agenzia, come la percentuale di cittadini che iniziano a compilare un modulo di richiesta di servizio e abbandonano, la durata media del tempo che trascorre tra la richiesta di invio e la risposta di approvazione/rifiuto e le statistiche di coinvolgimento per i manuali sui benefici che ha inviato ai cittadini.

### Recensioni di Camila Sites reporting (We.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Andate a *https://&lt;aemserver>:&lt;porta>/sites.html/content*
1. Selezionate il sito Web &quot;**AEM Forms We.Gov Site**&quot; per visualizzare le pagine del sito.
1. Selezionate una delle pagine del sito (ad esempio Home) e scegliete &quot;**Analytics &amp; Recommendations**&quot;.

   ![Analisi e raccomandazione](/help/forms/using/assets/analytics_recommendation.jpg)

1. In questa pagina, vedrai le informazioni recuperate da Adobe Analytics relative alla pagina Siti AEM (NOTA: in base alla progettazione, queste informazioni vengono aggiornate periodicamente da Adobe Analytics e non vengono visualizzate in tempo reale).

   ![Metriche chiave di Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. Tornando alla pagina di visualizzazione della pagina (a cui si accede al punto 3.3), è possibile visualizzare anche le informazioni di visualizzazione della pagina modificando l&#39;impostazione di visualizzazione per visualizzare gli elementi nella &quot;Vista **** elenco&quot;.
1. Individuate il menu a discesa &quot;**Visualizza**&quot; e selezionate &quot;Visualizzazione **** elenco&quot;.

   ![Visualizzazione a elenco nel menu a discesa Visualizza](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Nello stesso menu, selezionate &quot;**Visualizza impostazione**&quot; e selezionate le colonne da visualizzare nella sezione &quot;**Analytics**&quot;.

   ![Configurare la visualizzazione delle colonne](/help/forms/using/assets/view_setting_analytics.jpg)

1. Fare clic su &quot;**Aggiorna**&quot; per rendere disponibili le nuove colonne.

   ![Nuove colonne disponibili](/help/forms/using/assets/new_columns_available.jpg)

### Camila esamina i rapporti sui moduli (We.Gov Adobe Analytics) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Accedi a

   *https://&lt;aemserver>:&lt;porta>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Selezionate il modulo adattivo &quot;**Iscrizione applicazione per benefici** sanitari&quot; e selezionate l&#39;opzione &quot;Rapporto **** analisi&quot;.

   ![Domanda di iscrizione per benefici per la salute](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Attendete che la pagina venga caricata e visualizzate i dati del rapporto di Analytics.

   ![Dati report di Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)

