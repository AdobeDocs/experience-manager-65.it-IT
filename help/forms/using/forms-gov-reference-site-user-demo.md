---
title: Procedura dettagliata sul sito di riferimento We.Gov e We.Finance
seo-title: We.Gov and We.Finance reference site walkthrough
description: Utilizza utenti e gruppi fittizi per eseguire attività di AEM Forms utilizzando il pacchetto demo We.Gov e We.Finance.
seo-description: Use fictitious users and groups to perform AEM Forms tasks using We.Gov and We.Finance demo package.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---

# Procedura dettagliata sul sito di riferimento We.Gov e We.Finance {#we-gov-reference-site-walkthrough}

## Prerequisiti {#pre-requisites}

Configura il sito di riferimento come descritto in [Impostare e configurare il sito di riferimento We.Gov e We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## Storia utente {#user-story}

* AEM Forms

   * Conversione moduli automatica
   * Authoring  
   * Modelli di dati modulo/Origini dati

* AEM Forms

   * Acquisizione dati
   * (Facoltativo) Integrazione dei dati (MS Dynamics)
   * (Facoltativo) Adobe Sign

* Flusso di lavoro
* Notifiche e-mail
* (Facoltativo) Comunicazioni con i clienti

   * Canale di stampa
   * Canale web

* Adobe Analytics
* Integrazioni di origini dati

### Utenti e gruppi fittizi {#fictitious-users-and-groups}

Il pacchetto demo We.Gov è dotato dei seguenti utenti fittizi incorporati:

* **Aya Tan**: Cittadino idoneo a ricevere un Servizio da un&#39;agenzia governativa

![Utente fittizio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: analista aziendale di We.Gov

![Utente fittizio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Lead CX di We.Gov Agency

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

1. **Impersona**: definizione di utenti e gruppi nella demo dell’AEM.
1. **Pulsante**: rettangolo colorato o freccia circolare per la navigazione.
1. **Clic**: per eseguire un’azione nella storia utente.
1. **Collegamenti**: si trova nella parte superiore del menu principale nel sito We.Gov.
1. **Istruzioni utente**: set di passaggi numerici da seguire per spostarsi all’interno del brano dell’utente.
1. **Forms Portal**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Visualizzazione mobile**:We.Gov consente all&#39;utente di replicare una visualizzazione mobile con un browser ridimensionato.
1. **Vista desktop**: utente We.gov per visualizzare una demo su un laptop o desktop.
1. **Modulo di pre-screening**: modulo nella home page del sito We.Gov.
1. **Modulo adattivo**: modulo di iscrizione per la demo We.gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe del sito We.Gov**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Casella in entrata Adobe**: barra dei menu superiore [Icona Campana](assets/bell.svg) nel back-end AEM.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Client e-mail**: metodo preferito per visualizzare le e-mail (Gmail, Outlook)
1. **CTA**: Invito all’azione
1. **Naviga**: per individuare un punto di riferimento specifico nella pagina del browser.
1. **AFC**: AUTOMATED FORMS CONVERSION

## Automated forms conversion (Camila) {#automated-forms-conversion}

**Questa sezione**: Camila il lead CX ha un modulo esistente basato su PDF che è stato utilizzato come parte di un processo cartaceo. Come parte di uno sforzo di modernizzazione, vuole utilizzare questo modulo PDF per creare automaticamente un nuovo Forms adattivo moderno.

### Automated forms conversion - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Accedi a *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Accedi con:
   * **Utente**: camila.santos
   * **Password**: password
1. Dalla pagina principale, seleziona Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC.
1. Camila carica il PDF su AEM Forms.

   ![Carica modulo](assets/aftia-upload-form.jpg)

1. Camilla seleziona quindi il modulo PDF e fa clic su **Avvia conversione automatica** per avviare il processo di conversione. Potrebbe essere necessario fare clic su **Sovrascrivi conversione** se il modulo è stato convertito.

   >[!NOTE]
   >
   >Si noti che le impostazioni in AFC sono preconfigurate per l&#39;utente finale, il che significa che non devono essere modificate.

   * **Facoltativo**: se desideri utilizzare il tema Ultramarine accessibile, fai clic su Specifica un tema per moduli adattivi e seleziona il tema Ultramarine accessibile visualizzato nell’elenco delle opzioni.

   ![Avvia conversione](assets/aftia-start-conversion.jpg)

   ![Tema Ultramarino](assets/aftia-upload-conversion-settings.jpg)

   Lo stato di completamento della percentuale viene visualizzato durante la conversione. Una volta visualizzato lo stato **Convertito**, fare clic su **output** cartella, seleziona il modulo adattivo e fai clic su **Modifica** per aprire il modulo convertito.

1. Camilla esamina il modulo e si accerta che tutti i campi siano presenti

   ![Rivedi conversione](assets/aftia-review-conversion.jpg)

1. Camilla inizia quindi a modificare il modulo. Seleziona Pannello principale > Modifica (chiave inglese) > seleziona Schede in alto dal menu a discesa Layout pannello > seleziona la casella di controllo.

   ![Rivedi proprietà](assets/aftia-review-properties.jpg)

1. Camilla aggiunge quindi tutte le modifiche CSS e sul campo necessarie per produrre il prodotto finale.

   ![Aggiungi CSS](assets/aftia-add-css.jpg)

### Modello dati modulo e origini dati (Camila) {#data-sources}

**Questa sezione**: dopo aver convertito il documento e prodotto un modulo adattivo, Camila deve collegare il modulo adattivo a un’origine dati.

1. Camila apre le Proprietà nel modulo convertito in [Automated forms conversion - We.Gov](#automated-forms-conversion-wegov).

1. Camila seleziona quindi Modello modulo > Seleziona modello dati modulo dal menu a discesa Seleziona da > Seleziona FDM di iscrizione We.gov dall’elenco di opzioni.

1. Fai clic sul pulsante Salva e chiudi.

   ![Selezione FDM](assets/aftia-select-fdm.jpg)

1. Camila fa clic su **output** seleziona il modulo adattivo e fa clic su **Modifica** per aprire il modulo We.Gov completato.
1. Camila seleziona un campo di modulo adattivo e fa clic su ![Icona Configura](assets/configure-icon.svg). Crea l’associazione con le entità del modello di dati del modulo utilizzando **Riferimento binding** campo. Ripete questo passaggio per tutti i campi del modulo adattivo.

### Test di accessibilità dei moduli (Camila) {#form-accessibility-testing}

Camila verifica inoltre che il contenuto creato sia stato creato correttamente e completamente accessibile in base agli standard aziendali.

1. Camila fa clic su **output** seleziona il modulo adattivo e fa clic su **Anteprima** per aprire il modulo We.Gov completato.

1. Apre la scheda Audit nello strumento Chrome Developer Tool.

1. Esegue una verifica di accessibilità per convalidare il modulo adattivo.

   ![Verifica accessibilità](assets/aftia-accessibility.jpg)

## Demo Vista Mobile Modulo Adattivo (Aya) {#mobile-view-demo}

**Questa sezione deve essere eseguita prima della dimostrazione.**

**Istruzioni utente:**

1. Accedi a: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Accedi con:

   1. **Utente**: aya.tan
   1. **Password**: password

1. Ridimensiona la finestra del browser o utilizza l’emulatore del browser per replicare le dimensioni di un dispositivo mobile.

### Sito Web We.Gov (Aya) {#aya-user-story-we-gov-website}

![Utente fittizio](/help/forms/using/assets/aya_tan_new-1.png)

**Questa sezione**: Aya è una cittadina. Sente da un amico che potrebbe essere idonea a ricevere un Servizio da un&#39;agenzia governativa. Aya accede al sito web We.Gov dal suo telefono cellulare per saperne di più sui servizi a cui ha diritto.

### Pre-Screener We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya risponde ad alcune domande per confermare la sua idoneità compilando un breve modulo adattivo sul suo telefono cellulare.

**Istruzioni utente:**

1. Effettua una selezione in ciascun campo a discesa.

   >[!NOTE]
   >
   >Se l’utente guadagna più di $ 200.000/anno, non è idoneo.

1. Fai clic su &quot;**Sono Idoneo?**&quot; pulsante.
1. Fai clic su &quot;**Applica ora**&quot; per procedere.

   ![Collegamento Applica ora](/help/forms/using/assets/apply_now_link.png)

### Modulo Adattivo We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya scopre di essere idonea e inizia a compilare la sua applicazione per richiedere il servizio sul suo dispositivo mobile.

Aya deve rivedere alcuni documenti a casa prima di poter completare l’applicazione di richiesta del servizio. Salva e chiude l’applicazione dal suo dispositivo mobile.

**Istruzioni utente:**

1. Compila i campi Informazioni di base. Di seguito sono riportati i campi obbligatori e i menu a discesa:

   1. Informazioni di base

      1. Nome
      1. Cognome
      1. Data di nascita
      1. E-mail

1. Utilizza quanto segue **logica dinamica** per illustrare una feature dinamica utilizzando **Stato della famiglia** elenco a discesa:

   1. **Singolo**: mostra pannello superiore
   1. **Coniugato**: Mostra pannello dipendente da matrimonio
   1. **Divorziato**: mostra pannello superiore
   1. **Vedovo**: mostra pannello superiore
   1. **Ha dei figli?**: (Sì/No) per visualizzare il pannello dipendente dall’elemento secondario.

      1. (Aggiungi/Rimuovi) per aggiungere/rimuovere più pannelli figlio dipendenti.

1. Fare clic sulla freccia destra nella barra dei menu grigia.
1. Fai clic sul pulsante Salva in basso.

   ![Dettagli modulo adattivo](/help/forms/using/assets/adaptive_form.png)

## Demo desktop {#desktop-demo}

**Questa sezione:** Tornata a casa, Aya ha trovato le informazioni necessarie e riprende l&#39;applicazione dal suo desktop. Aya passa al portale dei moduli online per riprendere l’applicazione. Con alcune semplici personalizzazioni, le agenzie possono anche generare automaticamente e inviare tramite e-mail un collegamento per riprendere l’applicazione.

### Modulo Adattivo Continuo (Aya) {#aya-user-story-continued-adaptive-form}

**Istruzioni utente:**

1. Accedi a *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Dalla barra di navigazione, seleziona fai clic su &quot;**Servizi online**&quot;.
1. Dal pannello &quot;Bozza Forms&quot;, selezionare la &quot;Applicazione di iscrizione per benefici per la salute&quot; esistente.

   ![Richiesta di iscrizione per benefici per la salute](/help/forms/using/assets/enrollment_application.png)

   Il look and feel è lo stesso e non ha bisogno di inserire nuovamente alcun dato.

   **Istruzioni utente:**

1. Fai clic su Circle CTA (CTA cerchio) a destra per passare alla sezione successiva.

   ![Cerchio destro CTA](/help/forms/using/assets/right_circle_cta_new.png)

   Il modulo viene compilato fino al punto dell’ultima voce di Aya. Aya ha inserito tutte le sue informazioni ed è pronta a inviarle.

   ![Inviare il modulo adattivo](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Quando Aya compila il campo del numero di telefono deve compilarlo come numero continuo di 11 cifre senza trattini, spazi o trattini.

   Dopo l’invio Aya riceve una pagina di ringraziamento. Facoltativamente, riceverà anche un’e-mail che potrà aprire per firmare il documento record elettronicamente con Adobe Sign.

### Facoltativo: Adobe Sign (Aya) {#adobe-sign}

**Istruzioni utente:**

1. Passa al client e-mail e trova l’e-mail di Adobe Sign.
1. Fai clic sul collegamento ad Adobe Sign.

   ![Collegamento al segno Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Istruzioni utente:**

1. Controlla la sezione &quot;**Accetto**&quot;.
1. Fai clic su &quot;**Accetta**&quot;.
1. Scorrere fino alla parte inferiore del documento revisionato.
1. Fare clic sulla scheda gialla evidenziata per firmare il documento.

   ![Firma il documento](/help/forms/using/assets/sign_document_new.png) ![Firma il documento di prova](/help/forms/using/assets/sign_test_document.png)

## Agente governativo (George) {#government-agent-george}

![Agente governativo George](/help/forms/using/assets/george_lang-1.png)

**Questa sezione:** George è un analista commerciale presso l&#39;agenzia governativa Aya richiede un servizio a. George dispone di un&#39;unica dashboard in cui è possibile visualizzare tutte le applicazioni di richiesta di servizio che gli sono state assegnate per la revisione.

### Casella in entrata AEM (George) {#george-user-story-aem-inbox}

**Istruzioni utente:**

1. Accedi a *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Fai clic sull’icona utente (in alto a destra) e utilizza l’icona &quot;**Esci**&quot;, o &quot;**Impersona** Opzione di menu &quot; se si è attualmente connessi con un utente amministratore.

   1. Accedi con:

      1. **Utente:** george.lang
      1. **Password:** password
   1. Oppure rappresenta:

      1. Digita &quot;**George**&quot; in &quot;**Impersona**&quot;.

      1. Fai clic su OK per rappresentare.


1. Nell’angolo in alto a destra, fai clic sull’icona della notifica (campana).
1. Fai clic su &quot;**Visualizza tutto**&quot; per passare alla casella in entrata.
1. Dalla casella in entrata, apri la sezione &quot;**Valutazione dell&#39;applicazione Health Benefits**&quot;.

   ![Valutazione dell&#39;applicazione Health Benefits](/help/forms/using/assets/health_benefits.png)

### Facoltativo: Casella in entrata AEM e MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Grazie alle integrazioni di dati e ai flussi di lavoro automatizzati, viene visualizzata l’applicazione di Aya, insieme a un record di gestione delle relazioni con i clienti che è stato generato automaticamente al momento dell’invio dei dati.

**Istruzioni utente:**

1. Apri e controlla il modulo adattivo di sola lettura.
1. Fai clic sul pulsante &quot;**Apri MS Dynamics**&quot; per aprire il record MS Dynamics in una nuova finestra.
1. Nel sistema di gestione delle relazioni con i clienti puoi vedere che tutte le informazioni possono essere aggiornate

   1. Facoltativamente, aggiungi alcune note di revisione direttamente in Dynamics.

1. Chiudere e tornare alla casella in entrata AEM.

   ![Record MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Torna a Casella in entrata AEM (George) {#george-user-story-back-to-aem-inbox}

George approva l’applicazione di Aya e, grazie a un flusso di lavoro automatizzato esistente, viene inviata anche un’e-mail di conferma ad Aya.

**Istruzioni utente:**

1. Passa all’angolo in alto a sinistra e fai clic su &quot;**Approva**&quot; per approvare l’applicazione.
1. Nella finestra modale, puoi lasciare un messaggio per il lead CX.
1. Fai clic su Fine.
1. (Ruolo cittadino) Apri il client e-mail per visualizzare l’e-mail inviata ad Aya.

   ![Visualizza l’e-mail inviata ad Aya](/help/forms/using/assets/email_client.png)

## Lead CX (Camila) {#cx-lead-camila}

![Camila (lead CX)](/help/forms/using/assets/camila_santos-1.png)

**Questa sezione:** Camila the CX Lead stabilisce una telefonata di benvenuto con Aya per spiegare come utilizzare i servizi governativi per i quali è stata approvata.

### (Facoltativo) Casella in entrata AEM e MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Istruzioni utente:**

1. Accedi a *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Fai clic sull’icona utente (in alto a destra) e utilizza l’icona &quot;**Esci**&quot;, o &quot;**Impersona** Opzione di menu &quot; se si è attualmente connessi con un utente amministratore.

   1. Accedi con:

      1. **Utente**: camila.santos
      1. **Password**: password
   1. Oppure rappresenta:

      1. Digita &quot;**Camila**&quot; in &quot;**Impersona**&quot;.

      1. Fai clic su OK per rappresentare.


1. Nell’angolo in alto a destra, fai clic sull’icona Notifica (campana).
1. Fai clic su &quot;**Visualizza tutto**&quot; per passare alla casella in entrata.
1. Dalla casella in entrata, apri la sezione &quot;**Approvazione nuovo contatto**&quot;.

![Approvazione nuovo contatto](/help/forms/using/assets/new_contact_approval.png)

**(Facoltativo) Istruzioni utente:**

1. Apri e controlla il modulo adattivo di sola lettura.
1. Fai clic sul pulsante &quot;**Apri MS Dynamics**&quot; per aprire il record MS Dynamics in una nuova finestra.
1. Nel sistema di gestione delle relazioni con i clienti puoi vedere che tutte le informazioni possono essere aggiornate

   1. Facoltativamente, aggiungi una nuova attività di chiamata direttamente in Dynamics.
   1. Apri il &quot;**Attività**&quot;.
   1. Fai clic sul pulsante &quot;**Nuova telefonata**&quot;.
   1. Aggiungi i dettagli della telefonata.
   1. Salvare e chiudere la finestra.

1. Tornando all’AEM, passa all’angolo in alto a sinistra e fai clic su &quot;**Invia**&quot; per inviare la richiesta.
1. Nel modale, puoi lasciare un messaggio.
1. Fai clic su Fine.

   ![Scheda Attività](/help/forms/using/assets/activities_tab.png) ![Conferma nuovo contatto](/help/forms/using/assets/confirm_new_contact.png)

## (Facoltativo) Welcome Kit Citizen (Aya) {#welcome-kit-citizen-aya}

**Questa sezione:** Aya riceve un’e-mail contenente un collegamento a una comunicazione interattiva che riassume i suoi vantaggi e include anche campi modulo da compilare. Con l’istruzione sui vantaggi PDF allegata e il collegamento alla lettera di comunicazione interattiva nell’e-mail (con lo stesso tema/branding della comunicazione interattiva).

### Notifica Client E-Mail (Aya) {#aya-user-story-email-client}

**Istruzioni utente:**

1. Individua e apri l’e-mail del kit di benvenuto.
1. Scorri fino all’allegato PDF nella parte inferiore della pagina.
1. Fare clic per aprire l&#39;allegato PDF.
1. Scorri verso l’alto nel client e-mail e fai clic su &quot;**Visualizza il kit di benvenuto online**&quot;.

   1. Verrà aperta la versione del canale web dello stesso documento.

1. Per un rapido riferimento direttamente a PDF:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Per un rapido riferimento direttamente all&#39;IC:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Manuale di benvenuto sui vantaggi](/help/forms/using/assets/welcome_benefits_handbook.png) ![Collegamento di comunicazione interattiva](/help/forms/using/assets/interactive_communication.png)

## Cittadino Promemoria Rinnovo (Aya) {#renewal-reminder-citizen-aya}

**Questa sezione:** Camila pianifica anche un promemoria di comunicazione così un anno dopo. (Passaggio del flusso di lavoro che automatizza/esegue e invia e-mail).

### Notifica Client E-Mail (Aya) {#aya-user-story-email-client-updated}

**Istruzioni utente:**

1. Passa al client e-mail.
1. Individua e apri l’e-mail di Promemoria per il rinnovo.
1. Fai clic sul pulsante &quot;**Inviare una nuova domanda**&quot; per aprire il modulo adattivo.

   1. Questa sezione viene intenzionalmente lasciata vuota per supportare la precompilazione dei dati nella fase 2.

   ![E-mail di promemoria per il rinnovo](/help/forms/using/assets/renewal_reminder_email.png)

## (Facoltativo) Modello dati modulo (Camila) {#form-data-model}

**Questa sezione**: Camila passa a Integrazioni dati di AEM Forms dove può eseguire un test rapido per verificare che le informazioni inviate all’origine dati esterna tramite l’integrazione del modello dati del modulo siano effettivamente presenti.

### Modello dati modulo (Camila) {#form-data-model-camila}

**Questa sezione**: Camila passa alla pagina Origini dati per convalidare i dati replicati dal server all’interno del database Derby.

1. Una volta completata l’esperienza utente e completato l’invio da parte dell’utente, Camila passa alla scheda Origini dati in AEM Forms (**Forms** > **Integrazioni di dati**)

1. Camila seleziona quindi AEM Forms **We.gov FDM** e quindi modificare il **FDM iscrizione We.gov**.

1. Camila seleziona quindi il **Contatto** > **Servizio di lettura** da testare.

   ![Servizio di lettura contatti](assets/aftia-contact-read-service.jpg)

1. Camila fornisce quindi al servizio di test un ID contatto e fa clic sul pulsante Test. Ad esempio, 1 o 2, se il modulo è stato inviato. Se non hai inviato il modulo, non vengono restituiti dati.

   ![Servizio di lettura contatti](assets/aftia-test-service.jpg)

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

**Questa sezione:** Camila passa a una dashboard in cui può vedere attraverso i KPI dell’agenzia, ad esempio la percentuale di cittadini che iniziano a compilare e ad abbandonare un modulo di richiesta di assistenza, il periodo di tempo medio tra la presentazione della richiesta e la risposta di approvazione/rifiuto e le statistiche di coinvolgimento per i manuali sui benefit che ha inviato ai cittadini.

### Rapporti sui siti di Adobe Analytics (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Accedi a *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Seleziona la &quot;**Sito We.Gov di AEM Forms**&quot; per visualizzare le pagine del sito.
1. Seleziona una delle pagine del sito (ad esempio Home) e scegli &quot;**Analytics e Recommendations**&quot;.

   ![Analisi e consigli](/help/forms/using/assets/analytics_recommendation.jpg)

1. In questa pagina vengono visualizzate le informazioni recuperate da Adobe Analytics relative alla pagina di AEM Sites (NOTA: per progettazione queste informazioni vengono periodicamente aggiornate da Adobe Analytics e non vengono visualizzate in tempo reale).

   ![Metriche chiave di Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. Tornando alla pagina di visualizzazione della pagina (a cui si accede al punto 3), è possibile visualizzare le informazioni di visualizzazione della pagina modificando l’impostazione di visualizzazione in modo da visualizzare gli elementi nella sezione &quot;**Vista a elenco**&quot;.
1. Individua la &quot;**Visualizza**&quot; menu a discesa e selezionare &quot;**Vista a elenco**&quot;.

   ![Vista a elenco nel menu a discesa Vista](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Dallo stesso menu, seleziona &quot;**Visualizza impostazione**&quot; e seleziona le colonne da visualizzare dal &quot;**Analytics**&quot;.

   ![Configurare la visualizzazione delle colonne](/help/forms/using/assets/view_setting_analytics.jpg)

1. Fai clic su &quot;**Aggiorna**&quot; per rendere disponibili le nuove colonne.

   ![Rendi disponibili nuove colonne](/help/forms/using/assets/new_columns_available.jpg)

### Rapporti di Adobe Analytics Forms (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Accedi a

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Seleziona la &quot;**Domanda Di Iscrizione Per Benefici Sanitari**&quot;modulo adattivo e seleziona la&quot;**Rapporto di Analytics**&quot;.

   ![Richiesta di iscrizione per benefici per la salute](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Attendi che la pagina venga caricata e visualizza i dati del rapporto di Analytics.

   ![Dati dei rapporti di Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
