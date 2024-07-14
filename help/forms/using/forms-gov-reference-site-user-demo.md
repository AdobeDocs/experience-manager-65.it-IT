---
title: Procedura dettagliata sul sito di riferimento We.Gov e We.Finance
description: Utilizza utenti e gruppi fittizi per eseguire attività di AEM Forms utilizzando il pacchetto demo We.Gov e We.Finance.
contentOwner: anujkapo
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 1%

---

# Procedura dettagliata sul sito di riferimento We.Gov e We.Finance {#we-gov-reference-site-walkthrough}

## Prerequisiti {#pre-requisites}

Impostare il sito di riferimento come descritto in [Impostare e configurare il sito di riferimento We.Gov e We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## Storia utente {#user-story}

* AEM Forms

   * Conversione moduli automatica
   * Authoring
   * Modelli di dati modulo/Origini dati

* AEM Forms

   * Acquisizione dati
   * (Facoltativo) Integrazione dei dati (MS® Dynamics)
   * (Facoltativo) Adobe Sign

* Flusso di lavoro
* Notifiche e-mail
* (Facoltativo) Comunicazioni con i clienti

   * Canale di stampa
   * Canale web

* Adobe Analytics
* Integrazioni Data Source

### Utenti e gruppi fittizi {#fictitious-users-and-groups}

Il pacchetto demo We.Gov è dotato dei seguenti utenti fittizi incorporati:

* **Aya Tan**: cittadino idoneo a un servizio da un&#39;agenzia governativa

![Utente fittizio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: analista di business di We.Gov

![Utente fittizio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: lead CX dell&#39;agenzia We.Gov

![Utente fittizio](/help/forms/using/assets/camila_santos.png)

Sono inclusi anche i seguenti gruppi:

* **Utenti Forms We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)

* **Utenti We.Gov**

   * George Lang (membro)
   * Camila Santos (membro)
   * Aya Tan (membro)

### Legenda dei termini della panoramica della demo {#demo-overview-terms-legend}

1. **Rappresenta**: utenti e gruppi definiti nella demo AEM.
1. **Pulsante**: rettangolo colorato o freccia cerchiata per la navigazione.
1. **Fare clic**: per eseguire un&#39;azione nella storia utente.
1. **Collegamenti**: nella parte superiore del menu principale nel sito We.Gov.
1. **Istruzioni utente**: un insieme di passaggi numerici da seguire per spostarsi all&#39;interno del brano dell&#39;utente.
1. **Forms Portal**: *https://&lt;aemserver>:&lt;porta>/content/we-gov/formsportal.html*
1. **Visualizzazione mobile**:l&#39;utente We.Gov deve replicare una visualizzazione mobile con un browser ridimensionato.
1. **Vista desktop**: We.gov utente per visualizzare una demo su un laptop o desktop.
1. **Modulo pre-screening**: modulo nella home page del sito We.Gov.
1. **Modulo adattivo**: modulo di richiesta di registrazione per la demo We.gov.

   *https://&lt;aemserver>:&lt;porta>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Sito We.Gov Adobe**: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. **Casella in entrata Adobe**: barra dei menu superiore [icona campana](assets/bell.svg) nel backend AEM.

   *https://&lt;aemserver>:&lt;porta>/aem/start.html*

1. **Client e-mail**: metodo preferito per visualizzare le e-mail (Gmail, Outlook)
1. **CTA**: invito all&#39;azione
1. **Naviga**: per individuare un punto di riferimento specifico nella pagina del browser.
1. **AFC**: Automated forms conversion

## Automated forms conversion (Camila) {#automated-forms-conversion}

**Questa sezione**: Camila il lead CX ha un modulo esistente basato su PDF che è stato utilizzato come parte di un processo cartaceo. Come parte di un progetto di modernizzazione, Camila vuole utilizzare questo modulo PDF per creare automaticamente un moderno Forms adattivo.

### Automated forms conversion - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Passa a *https://&lt;aemserver>:&lt;porta>/aem/start.html*

1. Accedi con:
   * **Utente**: camila.santos
   * **Password**: password
1. Dalla pagina principale, seleziona Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC.
1. Camila carica il PDF su AEM Forms.

   ![Carica modulo](assets/aftia-upload-form.jpg)

1. Camilla seleziona quindi il modulo PDF e fa clic su **Avvia conversione automatica** per avviare il processo di conversione. Se il modulo è stato convertito, potrebbe essere necessario fare clic su **Sovrascrivi conversione**.

   >[!NOTE]
   >
   >Le impostazioni in AFC sono preconfigurate per l&#39;utente finale, il che significa che non devono essere modificate.

   * **Facoltativo**: se desideri utilizzare il tema Ultramarine accessibili, fai clic su Specifica un tema per moduli adattivi e seleziona il tema Ultramarine accessibili visualizzato nell&#39;elenco delle opzioni.

   ![Avvia conversione](assets/aftia-start-conversion.jpg)

   ![Tema Ultramarine](assets/aftia-upload-conversion-settings.jpg)

   Lo stato di completamento della percentuale viene visualizzato durante la conversione. Una volta visualizzato lo stato **Convertito**, fai clic sulla cartella **output**, seleziona il modulo adattivo e fai clic su **Modifica** per aprire il modulo convertito.

1. Camilla esamina il modulo e si accerta che tutti i campi siano presenti

   ![Rivedi conversione](assets/aftia-review-conversion.jpg)

1. Camilla inizia quindi a modificare il modulo e seleziona Root Panel (Pannello principale) > Edit (Modifica (chiave inglese) > select Tabs on Top (Schede in alto) dal menu a discesa Panel Layout (Layout pannello) > seleziona la casella di controllo.

   ![Rivedi proprietà](assets/aftia-review-properties.jpg)

1. Camilla aggiunge quindi tutte le modifiche CSS e sul campo necessarie per produrre il prodotto finale.

   ![Aggiungi CSS](assets/aftia-add-css.jpg)

### Modello dati modulo e origini dati (Camila) {#data-sources}

**Questa sezione**: dopo la conversione del documento e la generazione di un modulo adattivo, Camila deve connettere il modulo adattivo a un&#39;origine dati.

1. Camila apre le Proprietà nel modulo convertito in [Automated forms conversion - We.Gov](#automated-forms-conversion-wegov).

1. Camila seleziona quindi Modello modulo > Seleziona modello dati modulo dal menu a discesa Seleziona da > Seleziona FDM di iscrizione We.gov dall’elenco di opzioni.

1. Fai clic su Salva e chiudi.

   ![Selezione FDM](assets/aftia-select-fdm.jpg)

1. Camila fa clic sulla cartella **output**, seleziona il modulo adattivo e fa clic su **Modifica** per aprire il modulo We.Gov completato.
1. Camila seleziona un campo modulo adattivo, fa clic sull&#39;icona ![Configura](assets/configure-icon.svg) e crea un&#39;associazione con le entità del modello dati del modulo utilizzando il campo **Riferimento associazione**. Camila ripete questo passaggio per tutti i campi del modulo adattivo.

### Test di accessibilità dei moduli (Camila) {#form-accessibility-testing}

Camila verifica inoltre che il contenuto creato sia stato creato correttamente e completamente accessibile in base agli standard aziendali.

1. Camila fa clic sulla cartella **output**, seleziona il modulo adattivo e fa clic su **Anteprima** per aprire il modulo We.Gov completato.

1. Apre la scheda Audit in Chrome Developer Tool.

1. Esegue una verifica di accessibilità per convalidare il modulo adattivo.

   ![Verifica accessibilità](assets/aftia-accessibility.jpg)

## Demo Vista Mobile Modulo Adattivo (Aya) {#mobile-view-demo}

**Questa sezione deve essere eseguita prima della dimostrazione.**

**Istruzioni utente:**

1. Passa a: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Accedi con:

   1. **Utente**: aya.tan
   1. **Password**: password

1. Ridimensiona la finestra del browser o utilizza l’emulatore del browser per replicare le dimensioni di un dispositivo mobile.

### Sito Web We.Gov (Aya) {#aya-user-story-we-gov-website}

![Utente fittizio](/help/forms/using/assets/aya_tan_new-1.png)

**Questa sezione**: Aya è una cittadina e sente da un amico che potrebbe essere idonea a ricevere un Servizio da un&#39;agenzia governativa. Aya accede al sito web We.Gov dal suo telefono cellulare per saperne di più sui servizi a cui ha diritto.

### Pre-Screener We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya risponde ad alcune domande per confermare la sua idoneità compilando un breve modulo adattivo sul suo telefono cellulare.

**Istruzioni utente:**

1. Effettua una selezione in ciascun campo a discesa.

   >[!NOTE]
   >
   >Se l’utente guadagna più di $ 200.000/anno, non è idoneo.

1. Fare clic su **Sono idoneo?**.
1. Fare clic su **Applica** per continuare.

   ![Collegamento Applica](/help/forms/using/assets/apply_now_link.png)

### Modulo Adattivo We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya scopre di essere idonea e inizia a compilare la sua applicazione per richiedere il servizio sul suo dispositivo mobile.

Aya deve rivedere alcuni documenti a casa prima di poter completare l&#39;applicazione di richiesta di assistenza. Salva e chiude l’applicazione dal suo dispositivo mobile.

**Istruzioni utente:**

1. Compila i campi Informazioni di base. Di seguito sono riportati i campi obbligatori e i menu a discesa:

   1. Informazioni di base

      1. Nome
      1. Cognome
      1. Data di nascita
      1. E-mail

1. Utilizza la **logica dinamica** seguente per dimostrare la funzionalità dinamica utilizzando il menu a discesa **Stato famiglia**:

   1. **Singolo**: mostra pannello superiore
   1. **Sposato**: mostra pannello coniugale dipendente
   1. **Divorziato**: mostra pannello accanto
   1. **Vedovo**: mostra pannello vicino
   1. **Hai figli?**: pulsante di opzione (Sì/No) per visualizzare il pannello dipendente figlio.

      1. (Aggiungi/Rimuovi) per aggiungere/rimuovere più pannelli figlio dipendenti.

1. Fare clic sulla freccia destra nella barra dei menu grigia.
1. Fai clic sul pulsante Salva in basso.

   ![Dettagli modulo adattivo](/help/forms/using/assets/adaptive_form.png)

## Demo desktop {#desktop-demo}

**Questa sezione:** A casa, Aya ha trovato le informazioni necessarie e riprende l&#39;applicazione dal desktop. Aya passa al portale Forms online per riprendere l’applicazione. Con alcune semplici personalizzazioni, le agenzie possono anche generare automaticamente e inviare tramite e-mail un collegamento per riprendere l’applicazione.

### Modulo Adattivo Continuo (Aya) {#aya-user-story-continued-adaptive-form}

**Istruzioni utente:**

1. Passa a *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Dalla barra di spostamento, selezionare **Servizi in linea**.
1. Dal pannello &quot;Bozza Forms&quot;, selezionare la &quot;Applicazione di iscrizione per benefici per la salute&quot; esistente.

   ![Domanda di iscrizione per benefici per la salute](/help/forms/using/assets/enrollment_application.png)

   Il look and feel è lo stesso e non ha bisogno di inserire nuovamente alcun dato.

   **Istruzioni utente:**

1. Fate clic con il pulsante destro del mouse su Circle CTA (Circle CTA) per passare alla sezione successiva.

   ![CTA cerchio destro](/help/forms/using/assets/right_circle_cta_new.png)

   Il modulo viene compilato fino al punto dell&#39;ultima voce di Aya. Aya ha inserito tutte le sue informazioni ed è pronta a inviarle.

   ![Invia il modulo adattivo](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Quando Aya compila il campo del numero di telefono, deve compilarlo come numero continuo di 11 cifre senza trattini, spazi o trattini.

   Dopo l’invio, Aya riceve una pagina di ringraziamento. Facoltativamente, Aya riceve anche un’e-mail che può aprire per firmare il documento di record elettronicamente con Adobe Sign.

### Facoltativo: Adobe Sign (Aya) {#adobe-sign}

**Istruzioni utente:**

1. Passa al client e-mail e trova l’e-mail di Adobe Sign.
1. Fai clic sul collegamento ad Adobe Sign.

   ![Collegamento Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Istruzioni utente:**

1. Controlla **Accetto**.
1. Fare clic su **Accetta**.
1. Scorrere fino alla parte inferiore del documento revisionato.
1. Fare clic sulla scheda gialla evidenziata per firmare il documento.

   ![Firma il documento](/help/forms/using/assets/sign_document_new.png) ![Firma il documento di prova](/help/forms/using/assets/sign_test_document.png)

## Agente governativo (George) {#government-agent-george}

![Agente governativo George](/help/forms/using/assets/george_lang-1.png)

**Questa sezione:** George è un analista commerciale presso l&#39;agenzia governativa Aya richiede un servizio a. George dispone di un&#39;unica dashboard in cui è possibile visualizzare tutte le applicazioni di richiesta di servizio che gli sono state assegnate per la revisione.

### Casella in entrata AEM (George) {#george-user-story-aem-inbox}

**Istruzioni utente:**

1. Passa a *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Fai clic sull&#39;icona utente (in alto a destra) e utilizza **Disconnetti** oppure l&#39;opzione di menu **Impersona** se hai attualmente effettuato l&#39;accesso con un utente amministratore.

   1. Accedi con:

      1. **Utente:** george.lang
      1. **Password:** password

   1. Oppure rappresenta:

      1. Digitare `George` nel campo **Impersona**.

      1. Fai clic su OK per rappresentare.

1. Nell’angolo in alto a destra, fai clic sull’icona della notifica (campana).
1. Fare clic su **Visualizza tutto** per passare alla cartella Posta in arrivo.
1. Dalla Posta in arrivo, apri l&#39;ultima attività **Valutazione applicazione benefici per l&#39;integrità**.

   ![Analisi applicazione benefici per la salute](/help/forms/using/assets/health_benefits.png)

### Facoltativo: Casella in entrata AEM e MS® Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Grazie alle integrazioni di dati e ai flussi di lavoro automatizzati, viene visualizzata l’applicazione di Aya, insieme a un record di gestione delle relazioni con i clienti che è stato generato automaticamente al momento dell’invio dei dati.

**Istruzioni utente:**

1. Apri e controlla il modulo adattivo di sola lettura.
1. Fare clic su **Apri MS® Dynamics** per aprire il record MS® Dynamics in una nuova finestra.
1. Nel CRM, puoi visualizzare tutte le informazioni che possono essere aggiornate.

   1. Facoltativamente, aggiungi alcune note di revisione direttamente in Dynamics.

1. Chiudere e tornare alla casella in entrata AEM.

   ![Record MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Torna a Casella in entrata AEM (George) {#george-user-story-back-to-aem-inbox}

George approva l&#39;applicazione di Aya e, grazie a un flusso di lavoro automatico esistente, viene inviata anche un&#39;e-mail di conferma ad Aya.

**Istruzioni utente:**

1. Passa all&#39;angolo superiore sinistro e fai clic su **Approva** per approvare l&#39;applicazione.
1. Nella finestra modale, puoi lasciare un messaggio per il lead CX.
1. Fai clic su Fine.
1. (Ruolo cittadino) Apri il client e-mail per visualizzare l’e-mail inviata ad Aya.

   ![Visualizza l&#39;e-mail inviata ad Aya](/help/forms/using/assets/email_client.png)

## Lead CX (Camila) {#cx-lead-camila}

![Camila (lead CX)](/help/forms/using/assets/camila_santos-1.png)

**Questa sezione:** Camila il lead CX imposta una telefonata di benvenuto con Aya per spiegare come utilizzare i servizi governativi per i quali è approvata.

### (Facoltativo) Casella in entrata AEM e MS® Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Istruzioni utente:**

1. Passa a *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Fai clic sull&#39;icona utente (in alto a destra) e utilizza **Disconnetti** oppure l&#39;opzione di menu **Impersona** se hai attualmente effettuato l&#39;accesso con un utente amministratore.

   1. Accedi con:

      1. **Utente**: camila.santos
      1. **Password**: password

   1. Oppure rappresenta:

      1. Digitare `Camila` nel campo **Impersona**.

      1. Fai clic su OK per rappresentare.

1. Nell’angolo in alto a destra, fai clic sull’icona Notifica (campana).
1. Fare clic su **Visualizza tutto** per passare alla cartella Posta in arrivo.
1. Dalla Posta in arrivo, apri l&#39;ultima attività **Nuova approvazione contatto**.

![Approvazione nuovo contatto](/help/forms/using/assets/new_contact_approval.png)

**(Facoltativo) Istruzioni utente:**

1. Apri e controlla il modulo adattivo di sola lettura.
1. Fare clic su **Apri MS® Dynamics** per aprire il record MS® Dynamics in una nuova finestra.
1. Nel sistema di gestione delle relazioni con i clienti puoi visualizzare tutte le informazioni che possono essere aggiornate.

   1. Facoltativamente, aggiungi un’attività di chiamata direttamente in Dynamics.
   1. Apri la sezione **Attività**.
   1. Fai clic su **Nuova telefonata**.
   1. Aggiungi i dettagli della telefonata.
   1. Salvare e chiudere la finestra.

1. Torna a AEM, passa all&#39;angolo in alto a sinistra e fai clic su **Invia** per inviare l&#39;applicazione.
1. Nel modale, puoi lasciare un messaggio.
1. Fai clic su Fine.

   ![Scheda Attività](/help/forms/using/assets/activities_tab.png) ![Conferma nuovo contatto](/help/forms/using/assets/confirm_new_contact.png)

## (Facoltativo) Welcome Kit Citizen (Aya) {#welcome-kit-citizen-aya}

**Questa sezione:** Aya riceve un&#39;e-mail contenente un collegamento a una comunicazione interattiva che riassume i vantaggi e include anche campi modulo da compilare. Con l’istruzione sui vantaggi PDF allegata e il collegamento alla lettera di comunicazione interattiva nell’e-mail (con lo stesso tema/branding della comunicazione interattiva).

### Notifica Client E-Mail (Aya) {#aya-user-story-email-client}

**Istruzioni utente:**

1. Individua e apri l’e-mail del kit di benvenuto.
1. Scorri fino all’allegato PDF nella parte inferiore della pagina.
1. Fare clic per aprire l&#39;allegato PDF.
1. Scorri verso l&#39;alto nel client e-mail e fai clic su **Visualizza il kit di benvenuto online**.

   1. Viene aperta la versione del canale web dello stesso documento.

1. Per un rapido riferimento direttamente a PDF:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Per un rapido riferimento direttamente all&#39;IC:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Manuale dei benefici di benvenuto](/help/forms/using/assets/welcome_benefits_handbook.png) ![Collegamento di comunicazione interattiva](/help/forms/using/assets/interactive_communication.png)

## Cittadino Promemoria Rinnovo (Aya) {#renewal-reminder-citizen-aya}

**Questa sezione:** Camila pianifica anche un promemoria di comunicazione, quindi un anno dopo. (Passaggio del flusso di lavoro che automatizza/esegue e invia e-mail).

### Notifica Client E-Mail (Aya) {#aya-user-story-email-client-updated}

**Istruzioni utente:**

1. Passa al client e-mail.
1. Individua e apri l’e-mail di Promemoria per il rinnovo.
1. Fai clic su **Invia una nuova applicazione** per aprire il modulo adattivo.

   1. Questa sezione viene intenzionalmente lasciata vuota per supportare la precompilazione dei dati nella fase 2.

   ![E-mail di promemoria per il rinnovo](/help/forms/using/assets/renewal_reminder_email.png)

## (Facoltativo) Modello dati modulo (Camila) {#form-data-model}

**Questa sezione**: Camila passa a Integrazioni dati di AEM Forms dove può eseguire un test rapido per verificare che le informazioni inviate all&#39;origine dati esterna tramite l&#39;integrazione del modello dati del modulo siano effettivamente presenti.

### Modello dati modulo (Camila) {#form-data-model-camila}

**Questa sezione**: Camila passa alla pagina Origini dati per convalidare i dati replicati dal server nel database Derby.

1. Al termine dell&#39;esperienza utente e al termine dell&#39;invio da parte dell&#39;utente, Camila passa alla scheda Origini dati in AEM Forms (**Forms** > **Integrazioni dati**)

1. Camila seleziona quindi AEM Forms We.gov FDM e quindi modifica l&#39;FDM **We.gov registrazione**.

1. Camila seleziona quindi il **Contatto** > **Servizio di lettura** da testare.

   ![Contatta il servizio di lettura](assets/aftia-contact-read-service.jpg)

1. Camila fornisce quindi al servizio di test un ID contatto e quindi fa clic su **Test**. Ad esempio, 1 o 2, se il modulo è stato inviato. Se non hai inviato il modulo, non vengono restituiti dati.

   ![Contatta il servizio di lettura](assets/aftia-test-service.jpg)

1. Camila può quindi verificare che i dati siano stati inseriti correttamente nell’origine dati.

   * I dati all&#39;interno di Derby DS sono simili al seguente formato:

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## (Facoltativo) Analytics (Camila) {#analytics-cx-lead-camila}

**Questa sezione:** Camila passa a una dashboard in cui può vedere i KPI dell&#39;agenzia, ad esempio il numero di cittadini che iniziano a compilare un modulo di richiesta di assistenza e che abbandonano, il periodo di tempo medio tra l&#39;invio della richiesta e la risposta di approvazione/rifiuto e le statistiche di coinvolgimento per i manuali dei benefit inviati ai cittadini.

### Rapporti sui siti di Adobe Analytics (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Passa a *https://&lt;aemserver>:&lt;porta>/sites.html/content*
1. Seleziona **Sito AEM Forms We.Gov** per visualizzare le pagine del sito.
1. Selezionare una delle pagine del sito, ad esempio Home, e scegliere **Analytics &amp; Recommendations**.

   ![Analisi e consigli](/help/forms/using/assets/analytics_recommendation.jpg)

1. In questa pagina vengono visualizzate le informazioni recuperate da Adobe Analytics relative alla pagina di AEM Sites (NOTA: per progettazione queste informazioni vengono periodicamente aggiornate da Adobe Analytics e non vengono visualizzate in tempo reale).

   ![Metriche chiave di Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. Tornando alla pagina di visualizzazione della pagina (a cui si accede al passaggio 3.), è possibile visualizzare le informazioni di visualizzazione della pagina modificando l&#39;impostazione di visualizzazione in modo da visualizzare gli elementi nella **Vista a elenco**.
1. Individua il menu a discesa **Visualizza** e seleziona **Vista a elenco**.

   ![Visualizzazione elenco nel menu a discesa Visualizza](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Nello stesso menu, selezionare **Visualizza impostazione** e selezionare le colonne da visualizzare nella sezione **Analytics**.

   ![Configura la visualizzazione delle colonne](/help/forms/using/assets/view_setting_analytics.jpg)

1. Fai clic su **Aggiorna** per rendere disponibili le nuove colonne.

   ![Rendere disponibili nuove colonne](/help/forms/using/assets/new_columns_available.jpg)

### Rapporti di Adobe Analytics Forms (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Passa a

   *https://&lt;aemserver>:&lt;porta>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Selezionare il modulo adattivo **Applicazione di iscrizione per benefici per la salute** e selezionare l&#39;opzione **Report di Analytics**.

   ![Domanda di iscrizione per benefici per la salute](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Attendi che la pagina venga caricata e visualizza i dati del rapporto di Analytics.

   ![Dati report di Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
