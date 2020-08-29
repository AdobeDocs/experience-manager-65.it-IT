---
title: Procedura dettagliata sul sito di riferimento We.Gov e We.Finance
seo-title: Procedura dettagliata sul sito di riferimento We.Gov e We.Finance
description: Utilizzate utenti e gruppi fittizi per eseguire  attività AEM Forms utilizzando il pacchetto dimostrativo We.Gov e We.Finance.
seo-description: Utilizzate utenti e gruppi fittizi per eseguire  attività AEM Forms utilizzando il pacchetto dimostrativo We.Gov e We.Finance.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: c6b8e184042394d99ceb099c918b81e2cce49497
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 1%

---


# Procedura dettagliata sul sito di riferimento We.Gov e We.Finance {#we-gov-reference-site-walkthrough}

## Prerequisiti {#pre-requisites}

Configurate il sito di riferimento come descritto in [Impostazione e configurazione del sito](../../forms/using/forms-install-configure-gov-reference-site.md)di riferimento We.Gov e We.Finance.

## Storia utente {#user-story}

* AEM Forms

   * Conversione moduli automatica
   * Authoring  
   * Modelli dati modulo/Origini dati

* AEM Forms

   * Acquisizione dati
   * (Facoltativo) Integrazione dei dati (MS Dynamics)
   * (Facoltativo)  Adobe Sign

* Flusso di lavoro
* Notifiche e-mail
* (Facoltativo) Comunicazione con i clienti

   * Stampa canale
   * Canale web

* Adobe Analytics
* Integrazioni origini dati

### Fictitious users and groups {#fictitious-users-and-groups}

Il pacchetto dimostrativo We.Gov include i seguenti utenti fittizi incorporati:

* **Aya Tan**: Cittadino idoneo a un servizio da un ente governativo

![Utente fittizio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Agenzia governativa Business Analytics

![Utente fittizio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: We.Gov Agenzia CX

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

1. **Impersona**: Utenti e gruppi definiti in AEM demo.
1. **Pulsante**: Rettangolo colorato o freccia cerchiata per la navigazione.
1. **Fate clic**: Per eseguire un&#39;azione nel brano dell&#39;utente.
1. **Collegamenti**: Situato nella parte superiore del menu principale nel sito We.Gov.
1. **Istruzioni** utente: Una serie di passaggi numerici da seguire per navigare nel racconto dell&#39;utente.
1. **Forms Portal**: *https://&lt;aemserver>:&lt;porta>/content/we-gov/formsportal.html*
1. **Vista** mobile:We.Gov utente per replicare una visualizzazione mobile con un browser ridimensionato.
1. **Vista** desktop: L&#39;utente We.gov può visualizzare la dimostrazione su un computer portatile o desktop.
1. **Modulo** pre-screener: Modulo sulla home page del sito We.Gov.
1. **Modulo** adattivo: Modulo di richiesta di iscrizione per la demo di We.gov.

   *https://&lt;aemserver>:&lt;porta>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe Sito Web** Di We.Gov: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. **Casella in entrata** Adobe : Posizione della barra dei menu principale Icona [Bell nella barra dei menu](assets/bell.svg) AEM backend.

   *https://&lt;aemserver>:&lt;porta>/aem/start.html*

1. **Client** e-mail: Metodo preferito per visualizzare le e-mail (Gmail, Outlook)
1. **CTA**: Invito all&#39;azione
1. **Naviga**: Per individuare un punto di riferimento specifico nella pagina del browser.
1. **AFC**: Conversione automatica di Forms

## Conversione automatizzata Forms (Camila) {#automated-forms-conversion}

**Questa sezione**: Camila il lead CX dispone di un modulo PDF esistente che è stato utilizzato come parte di un processo basato su carta. Nell&#39;ambito di un&#39;attività di modernizzazione, l&#39;utente desidera utilizzare il modulo PDF per creare automaticamente un nuovo Forms adattivo.

### Conversione automatizzata di Forms - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Andate a *https://&lt;aemserver>:&lt;porta>/aem/start.html*

1. Effettua l’accesso con:
   * **Utente**: camila.santos
   * **Password**: password
1. Dalla pagina principale selezionate Forms > Forms e documenti >  AEM Forms We.gov Forms > AFC.
1. Camila carica il PDF su  AEM Forms.

   ![Carica modulo](assets/aftia-upload-form.jpg)

1. Camilla seleziona quindi il modulo PDF e fa clic su **Avvia conversione** automatica per avviare il processo di conversione. Se il modulo è stato convertito, potrebbe essere necessario fare clic su **Sovrascrivi conversione** .

   >[!NOTE]
   >
   >Le impostazioni in AFC sono preconfigurate per l&#39;utente finale, il che significa che non devono essere modificate.

   * **Facoltativo**: Se si desidera utilizzare il tema Accessible Ultramarine, fare clic sul tema Specificare un modulo adattivo e selezionare il tema Accessible-Ultramarine che viene visualizzato nell&#39;elenco delle opzioni.

   ![Avvia conversione](assets/aftia-start-conversion.jpg)

   ![Tema ultramarino](assets/aftia-upload-conversion-settings.jpg)

   Durante la conversione viene visualizzato lo stato di completamento della percentuale. Una volta visualizzato lo stato **Convertito**, fare clic sulla cartella di **output** , selezionare il modulo adattivo e fare clic su **Modifica** per aprire il modulo convertito.

1. Camilla quindi esamina il modulo e verifica che tutti i campi siano presenti

   ![Verifica conversione](assets/aftia-review-conversion.jpg)

1. Camilla inizia quindi a modificare il modulo. Seleziona Pannello principale > Modifica (chiave inglese) > seleziona Tabulazioni in alto dal menu a discesa Layout pannello > seleziona la casella di controllo.

   ![Proprietà revisione](assets/aftia-review-properties.jpg)

1. Camilla aggiunge quindi tutte le modifiche necessarie CSS e sul campo per produrre il prodotto finale.

   ![Aggiungi CSS](assets/aftia-add-css.jpg)

### Modello dati modulo e origini dati (Camila) {#data-sources}

**Questa sezione**: Una volta convertito il documento e prodotto un modulo adattivo, Camila deve collegare il modulo adattivo a un&#39;origine dati.

1. Camila apre le Proprietà sul modulo che è stato convertito in Conversione Forms [automatizzata - We.Gov](#automated-forms-conversion-wegov).

1. Camila seleziona quindi Modello modulo > Seleziona modello dati modulo dal menu a discesa Seleziona da > Seleziona FDM iscrizione We.gov dall&#39;elenco di opzioni.

1. Fate clic sul pulsante Salva e chiudi.

   ![Selezione FDM](assets/aftia-select-fdm.jpg)

1. Camila fa clic sulla cartella di **output** , seleziona il modulo adattivo e fa clic su **Modifica** per aprire il modulo We.Gov completato.
1. Camila seleziona un campo modulo adattivo e fa clic sull’icona ![](assets/configure-icon.svg)Configura. Crea un binding con le entità del modello dati del modulo utilizzando il campo Riferimento **** binding. Ripete questo passaggio per tutti i campi del modulo adattivo.

### Test di accessibilità del modulo (Camila) {#form-accessibility-testing}

Camila inoltre verifica che i contenuti creati siano creati correttamente e completamente accessibili in base agli standard aziendali.

1. Camila fa clic sulla cartella di **output** , seleziona il modulo adattivo e fa clic su **Anteprima** per aprire il modulo We.Gov completato.

1. Apre la scheda Audit in Chrome Developer Tool.

1. Esegue un controllo di accessibilità per convalidare il modulo adattivo.

   ![Controllo accesso facilitato](assets/aftia-accessibility.jpg)

## Demo Di Visualizzazione Mobile Modulo Adattivo (Aya) {#mobile-view-demo}

**Questa sezione deve essere eseguita prima della dimostrazione.**

**Istruzioni utente:**

1. Passa a: *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Effettua l’accesso con:

   1. **Utente**: aya.tan
   1. **Password**: password

1. Ridimensionate nuovamente la finestra del browser o utilizzate l&#39;emulatore del browser per replicare le dimensioni di un dispositivo mobile.

### Sito Web We.Gov (Aya) {#aya-user-story-we-gov-website}

![Utente fittizio](/help/forms/using/assets/aya_tan_new-1.png)

**Questa sezione**: Aya è un cittadino. Ha sentito da un&#39;amica che potrebbe essere idonea a ricevere un Servizio da un&#39;agenzia governativa. Aya naviga sul sito Web We.Gov dal suo cellulare per saperne di più sui servizi a cui è idonea.

### Pre-Screener We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya risponde ad alcune domande per confermare la sua idoneità compilando un breve modulo adattivo sul suo cellulare.

**Istruzioni utente:**

1. Effettuare una selezione in ciascun campo a discesa.

   >[!NOTE]
   >
   >Se l’utente guadagna più di $200.000/anno, non è idoneo.

1. Fare clic su &quot;**Sono idoneo?**” pulsante.
1. Fare clic sul pulsante &quot;**Applica ora**&quot; per proseguire.

   ![Collegamento Applica ora](/help/forms/using/assets/apply_now_link.png)

### Modulo Adattivo We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya scopre di essere idonea e inizia a compilare la sua applicazione per richiedere il servizio sul suo dispositivo mobile.

È necessario rivedere alcuni documenti a casa prima di poter completare l&#39;applicazione di richiesta del servizio. Salva ed esce dall’applicazione dal suo dispositivo mobile.

**Istruzioni utente:**

1. Compila i campi delle informazioni di base, i campi e i menu a discesa seguenti sono obbligatori:

   1. Informazioni di base

      1. Nome
      1. Cognome
      1. DOB
      1. E-mail

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

## Demo sul desktop {#desktop-demo}

**Questa sezione:** Tornando a casa, Aya ha trovato le informazioni di cui aveva bisogno e riprende l&#39;applicazione dal suo desktop. Aya passa al portale dei moduli online per riprendere l&#39;applicazione. Con una semplice personalizzazione, le agenzie possono anche generare automaticamente e inviare via e-mail un collegamento per riprendere l&#39;applicazione.

### Modulo Adattivo Continuato (Aya) {#aya-user-story-continued-adaptive-form}

**Istruzioni utente:**

1. Andate a *https://&lt;aemserver>:&lt;porta>/content/we-gov/home.html*
1. Dalla barra di navigazione, selezionate click on &quot;**Online Services**&quot; (Servizionline).
1. Nel pannello &quot;Bozza Forms&quot;, selezionate la &quot;Domanda di iscrizione per benefici sanitari&quot; esistente.

   ![Domanda di iscrizione per i benefici per la salute](/help/forms/using/assets/enrollment_application.png)

   L&#39;aspetto e la sensazione sono gli stessi, e non ha bisogno di reimmettere dati.

   **Istruzioni utente:**

1. Fate clic su CTA cerchio destro per passare alla sezione successiva.

   ![CTA cerchio RIght](/help/forms/using/assets/right_circle_cta_new.png)

   Il modulo viene compilato fino al punto dell&#39;ultima voce di Aya. Aya ha inserito tutte le sue informazioni ed è pronta a inviare.

   ![Invio del modulo adattivo](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Quando Aya riempie il campo del numero di telefono deve riempirlo come numero continuo di 11 cifre senza trattini, spazi o trattini.

   Dopo l&#39;invio di Aya riceve una pagina di ringraziamento. Facoltativamente, riceverà anche un messaggio e-mail che potrà aprire per firmare elettronicamente il documento di registrazione con  Adobe Sign.

### Facoltativo:  Adobe Sign (Aya) {#adobe-sign}

**Istruzioni utente:**

1. Andate al client e-mail e cercate il  e-mail Adobe Sign.
1. Fate clic sul collegamento per  Adobe Sign.

   ![Collegamento del Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Istruzioni utente:**

1. Selezionare la casella &quot;**Sono d&#39;accordo**&quot;.
1. Fate clic su &quot;**Accetto**&quot;.
1. Scorrete fino in fondo al documento rivisto.
1. Fare clic sulla scheda evidenziata gialla per firmare il documento.

   ![Firmare il documento](/help/forms/using/assets/sign_document_new.png) ![Firmare il documento di prova](/help/forms/using/assets/sign_test_document.png)

## Agente governativo (George) {#government-agent-george}

![Agente governativo George](/help/forms/using/assets/george_lang-1.png)

**Questa sezione:** George è un analista d&#39;affari dell&#39;agenzia governativa Aya, che chiede un servizio. George dispone di un&#39;unica dashboard in cui può vedere tutte le applicazioni di richiesta di servizio che gli sono state assegnate per la revisione.

### Casella in entrata AEM (George) {#george-user-story-aem-inbox}

**Istruzioni utente:**

1. Andate a *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Fate clic sull&#39;icona dell&#39;utente (nell&#39;angolo in alto a destra) e utilizzate &quot;**Disconnetti**&quot;, oppure l&#39;opzione di menu &quot;**Impersona come**&quot; se avete attualmente eseguito l&#39;accesso con un utente amministrativo.

   1. Effettua l’accesso con:

      1. **Utente:** george.lang
      1. **Password:** password
   1. O Impersona:

      1. Digitare &quot;**George**&quot; nel campo &quot;**Impersonate as**&quot;.

      1. Fare clic su OK per impersonare.


1. Dall’angolo in alto a destra, fate clic sull’icona Notifica (campana).
1. Fare clic su &quot;**Visualizza tutto**&quot; per passare alla casella in entrata.
1. Dalla casella in entrata, aprire l&#39;ultima operazione &quot;**Health Benefits Application Review**&quot;.

   ![Revisione dell&#39;applicazione dei vantaggi per la salute](/help/forms/using/assets/health_benefits.png)

### Facoltativo: AEM Posta in arrivo e MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Grazie alle integrazioni di dati e ai flussi di lavoro automatizzati, viene visualizzata l&#39;applicazione di Aya, insieme a un record CRM che è stato generato automaticamente al momento dell&#39;invio dei dati.

**Istruzioni utente:**

1. Aprire ed esaminare il modulo adattivo di sola lettura.
1. Fare clic sul pulsante &quot;**Open MS Dynamics**&quot; per aprire il record MS Dynamics in una nuova finestra.
1. In CRM è possibile vedere tutte le informazioni possono essere aggiornate

   1. Facoltativamente, aggiungi alcune note di revisione direttamente in Dynamics.

1. Chiudete e tornate AEM Posta in arrivo.

   ![Record MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Torna a AEM Posta in arrivo (George) {#george-user-story-back-to-aem-inbox}

George approva l’applicazione di Aya e grazie a un flusso di lavoro automatizzato esistente, ad Aya viene inviato anche un messaggio e-mail di conferma.

**Istruzioni utente:**

1. Andate in alto a sinistra e fate clic su &quot;**Approva**&quot; per approvare l&#39;applicazione.
1. Nella modalità, potete lasciare un messaggio per il lead CX.
1. Fate clic su Fine.
1. (Ruolo cittadino) Aprite il client di posta elettronica per visualizzare l’e-mail inviata ad Aya.

   ![Visualizza l&#39;e-mail inviata ad Aya](/help/forms/using/assets/email_client.png)

## Piombo CX (Camila) {#cx-lead-camila}

![Camila (CX lead)](/help/forms/using/assets/camila_santos-1.png)

**Questa sezione:** Camila il lead CX ha organizzato una telefonata di benvenuto con Aya per spiegare come utilizzare i servizi governativi per i quali è stata approvata.

### (Facoltativo) AEM Inbox e MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Istruzioni utente:**

1. Andate a *https://&lt;aemserver>:&lt;porta>/aem/start.html*
1. Fate clic sull&#39;icona dell&#39;utente (nell&#39;angolo in alto a destra) e utilizzate &quot;**Disconnetti**&quot;, oppure l&#39;opzione di menu &quot;**Impersona come**&quot; se avete attualmente eseguito l&#39;accesso con un utente amministrativo.

   1. Effettua l’accesso con:

      1. **Utente**: camila.santos
      1. **Password**: password
   1. O Impersona:

      1. Digitare &quot;**Camila**&quot; nel campo &quot;**Impersonate as**&quot;.

      1. Fare clic su OK per impersonare.


1. Dall’angolo in alto a destra, fate clic sull’icona Notifica (campana).
1. Fare clic su &quot;**Visualizza tutto**&quot; per passare alla casella in entrata.
1. Dalla casella in entrata, aprire l&#39;ultima operazione &quot;**Nuova approvazione** contatto&quot;.

![Nuova approvazione contatto](/help/forms/using/assets/new_contact_approval.png)

**(Facoltativo) Istruzioni utente:**

1. Aprire ed esaminare il modulo adattivo di sola lettura.
1. Fare clic sul pulsante &quot;**Open MS Dynamics**&quot; per aprire il record MS Dynamics in una nuova finestra.
1. In CRM è possibile vedere tutte le informazioni possono essere aggiornate

   1. Facoltativamente, aggiungi una nuova attività di chiamata direttamente in Dynamics.
   1. Aprite la sezione &quot;**Attività**&quot;.
   1. Fate clic sull&#39;opzione &quot;**Nuova chiamata** telefonica&quot;.
   1. Aggiungete i dettagli delle chiamate telefoniche.
   1. Salvare e chiudere la finestra.

1. Tornare in AEM, andare nell&#39;angolo superiore sinistro e fare clic su &quot;**Invia**&quot; per inviare l&#39;applicazione.
1. Nella finestra modale puoi lasciare un messaggio.
1. Fate clic su Fine.

   ![Scheda](/help/forms/using/assets/activities_tab.png) Attività ![Conferma nuovo contatto](/help/forms/using/assets/confirm_new_contact.png)

## (Facoltativo) Kit Di Benvenuto Cittadino (Aya) {#welcome-kit-citizen-aya}

**Questa sezione:** Aya riceve un messaggio e-mail contenente un collegamento a una comunicazione interattiva che riepiloga i vantaggi e include anche campi modulo da compilare. Con l&#39;indicazione dei vantaggi PDF allegata e il collegamento alla lettera di comunicazione interattiva nella posta (con lo stesso tema/marchio della comunicazione interattiva).

### Notifica Client E-Mail (Aya) {#aya-user-story-email-client}

**Istruzioni utente:**

1. Individuate e aprite il messaggio e-mail del kit di benvenuto.
1. Scorrete fino all’allegato PDF nella parte inferiore della pagina.
1. Fare clic per aprire l&#39;allegato PDF.
1. Scorri verso l&#39;alto nel tuo client di posta elettronica e clicca su &quot;**Visualizza kit di benvenuto online**&quot;.

   1. Viene aperta la versione per il canale Web dello stesso documento.

1. Per un riferimento rapido direttamente al PDF:

   *https://&lt;server aemserver>:&lt;porta>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Per un riferimento rapido a IC direttamente:

   *https://&lt;aemserver>:&lt;porta>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Benvenuto Manuale](/help/forms/using/assets/welcome_benefits_handbook.png) sulle comunicazioni ![interattive](/help/forms/using/assets/interactive_communication.png)

## Renewal Promemoria Citizen (Aya) {#renewal-reminder-citizen-aya}

**Questa sezione:** Camila pianifica anche un promemoria di comunicazione così un anno dopo. (Procedura del flusso di lavoro che automatizza/esegue e invia per e-mail).

### Notifica Client E-Mail (Aya) {#aya-user-story-email-client-updated}

**Istruzioni utente:**

1. Andate al client di posta elettronica.
1. Individuate e aprite il messaggio e-mail di promemoria rinnovo.
1. Fare clic sul pulsante &quot;**Invia una nuova applicazione**&quot; per aprire il modulo adattivo.

   1. Questa sezione viene lasciata intenzionalmente vuota per supportare la precompilazione dei dati nella fase 2.

   ![E-mail promemoria rinnovamento](/help/forms/using/assets/renewal_reminder_email.png)

## (Facoltativo) Modello dati modulo (Camila) {#form-data-model}

**Questa sezione**: Camila passa a  AEM Forms Data Integrations dove può eseguire un test rapido per verificare che le informazioni inviate all&#39;origine dati esterna tramite l&#39;integrazione con Form Data Model siano effettivamente presenti.

### Modello dati modulo (Camila) {#form-data-model-camila}

**Questa sezione**: Camila passa alla pagina Origini dati per convalidare i dati replicati dal server all&#39;interno del database Derby.

1. Una volta completata l&#39;esperienza utente e l&#39;invio dell&#39;utente, Camila passa alla scheda Origini dati all&#39;interno  AEM Forms (**Forms** > Integrazioni **** dati)

1. Camila seleziona quindi  AEM Forms **We.gov FDM** e modifica il FDM **di iscrizione** We.gov.

1. Camila seleziona quindi **Contatto** > Servizio **di** lettura da testare.

   ![Servizio lettura contatti](assets/aftia-contact-read-service.jpg)

1. Camila fornisce quindi al servizio di prova un ID contatto e fa clic sul pulsante Test. Ad esempio, 1 o 2, se il modulo è stato inviato. Se il modulo non è stato inviato, non viene restituito alcun dato.

   ![Servizio lettura contatti](assets/aftia-test-service.jpg)

1. Camila può quindi verificare che i dati siano stati inseriti correttamente nell&#39;origine dati.

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

## (Facoltativo) Analisi (Camila) {#analytics-cx-lead-camila}

**Questa sezione:** Camila passa a un dashboard in cui può vedere i KPI dell&#39;agenzia, come la percentuale di cittadini che iniziano a compilare un modulo di richiesta di servizio e abbandonano, la durata media del tempo che trascorre tra la richiesta di invio e la risposta di approvazione/rifiuto e le statistiche di coinvolgimento per i manuali sui benefici che ha inviato ai cittadini.

### Reporting  siti Adobe Analytics (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Andate a *https://&lt;aemserver>:&lt;porta>/sites.html/content*
1. Selezionate &quot;**sito** AEM Forms We.Gov&quot; per visualizzare le pagine del sito.
1. Selezionate una delle pagine del sito (ad esempio Home) e scegliete &quot;**Analytics &amp; Recommendations**&quot;.

   ![Analisi e raccomandazione](/help/forms/using/assets/analytics_recommendation.jpg)

1. In questa pagina verranno visualizzate le informazioni recuperate da  Adobe Analytics relative alla pagina AEM Sites  (NOTA: in base alla progettazione, queste informazioni vengono aggiornate periodicamente da  Adobe Analytics e non vengono visualizzate in tempo reale).

   ![metriche chiave Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. Tornando alla pagina di visualizzazione della pagina (a cui si accede al punto 3.3), è possibile visualizzare anche le informazioni di visualizzazione della pagina modificando l&#39;impostazione di visualizzazione per visualizzare gli elementi nella &quot;Vista **** a elenco&quot;.
1. Individuate il menu a discesa &quot;**Visualizza**&quot; e selezionate &quot;Visualizzazione **** elenco&quot;.

   ![Visualizzazione a elenco nel menu a discesa Visualizza](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Nello stesso menu, selezionate &quot;**Visualizza impostazione**&quot; e selezionate le colonne da visualizzare nella sezione &quot;**Analytics**&quot;.

   ![Configurare la visualizzazione delle colonne](/help/forms/using/assets/view_setting_analytics.jpg)

1. Fare clic su &quot;**Aggiorna**&quot; per rendere disponibili le nuove colonne.

   ![Nuove colonne disponibili](/help/forms/using/assets/new_columns_available.jpg)

###  Forms Reporting (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Accedi a

   *https://&lt;aemserver>:&lt;porta>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Selezionate il modulo adattivo &quot;**Iscrizione applicazione per benefici** sanitari&quot; e selezionate l&#39;opzione &quot;Rapporto **** analisi&quot;.

   ![Domanda di iscrizione per i benefici per la salute](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Attendete che la pagina venga caricata e visualizzate i dati del rapporto di Analytics.

   ![Dati report di Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)

