---
title: Procedura dettagliata sul sito di riferimento We.Gov
seo-title: Procedura dettagliata sul sito di riferimento We.Gov
description: Consulta la guida dettagliata del sito Web di riferimento We.Gov per capire in che modo  AEM Forms aiuta i governi a ricevere e inviare le informazioni richieste dagli individui ai sensi del Freedom of Information Act.
seo-description: Consulta la guida dettagliata del sito Web di riferimento We.Gov per capire in che modo  AEM Forms aiuta i governi a ricevere e inviare le informazioni richieste dagli individui ai sensi del Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# Sito di riferimento We.Gov FOIA Procedura dettagliata {#we-gov-reference-site-foia-walkthrough}

## Scenario di riferimento Freedom Information Act {#reference-site-freedom-of-information-act-scenario}

We.Gov è un&#39;organizzazione governativa che permette ai genitori adottivi di iscriversi al sostegno dei figli se adottano un figlio. We.Gov permette anche ai genitori di richiedere informazioni ai seguenti dipartimenti governativi sotto la legge sulla libertà di informazione:

* Agenzia per la logistica della difesa
* Dipartimento della Difesa dell&#39;Ispettore Generale
* Dipartimento di giustizia - Ufficio per la politica d&#39;informazione
* Dipartimento della Marina
* Agenzia per la protezione ambientale

Per ulteriori informazioni sulla legge sulla libertà di informazione, vedere [www.foia.gov](https://www.foia.gov).

Lo scenario coinvolge le seguenti persone:

* Sarah Rose, la persona che richiede informazioni in
* John Jacobs, la persona che gestisce la richiesta la inoltra al reparto appropriato
* Gloria Rios, dipendente del governo che fornisce le informazioni secondo la richiesta

## Sarah avvia la richiesta di informazioni in FOIA {#sarah-initiates-request-for-information-under-foia}

Secondo la legge sulla libertà d&#39;informazione, Sarah richiede una copia del registro di casi dell&#39;Amministrazione per bambini e famiglie per anni (anno fiscale 2013-2016). Sarah presenta questa richiesta al Dipartimento di giustizia e ufficio per la politica d&#39;informazione e indica che è disposta a pagare fino a 100 dollari per le spese di stampa e di spedizione.

### Come funziona {#how-it-works}

### Vedere da soli {#see-it-yourself}

Nel browser, aprite `https://<hostname>:<PublishPort>/wegov`. Nel sito We.Gov, toccate Applicazioni > Tutte le applicazioni. Nella pagina Tutte le applicazioni, toccate Applica in Applicazione per richiesta FOIA.

## Sarah avvia la sua applicazione per informazioni in FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah fa clic su **Applica** e nella pagina Modulo di richiesta Freedom of Information Act, Sarah inserisce informazioni tra cui:

* **Agenzia:** Sarah specifica l&#39;agenzia a cui la richiesta è stata indirizzata come Dipartimento di Giustizia - Ufficio della Politica di Informazione.

* **Pagherà Fino** A: Sarah specifica che è disposta a pagare fino a 100 dollari per la stampa e le spese postali.
* **Descrivete dettagliatamente** la richiesta: Sarah specifica &quot;Richiesta di copia dei casi di Amministrazione per bambini e famiglie per gli esercizi fiscali dal 2013 al 2016&quot;.

![Richiesta di copia del caso Amministrazione per bambini e famiglie per gli anni fiscali 2013-2016](assets/sarahfiosform.png)

Richiesta di copia del caso Amministrazione per bambini e famiglie per gli anni fiscali 2013-2016

In qualsiasi momento, Sarah può toccare Salva per salvare la bozza del modulo e tornare più tardi per compilare il modulo e inviarlo. Sarah invia il modulo.

>[!NOTE]
>
>Il flusso di lavoro di ripresa da e-mail funziona solo con gli utenti connessi. Nello scenario del sito di riferimento, accertatevi che l’utente Sarah Rose sia aggiunto. Le credenziali di accesso di Sarah sono `srose/password`.

## John Jacobs riceve e approva l&#39;applicazione {#john-jacobs-receives-and-approves-the-application}

John Jacobs riceve le richieste e le indirizza alla persona giusta. AEM Posta in arrivo consente di visualizzare tutte le applicazioni inviate in un&#39;unica posizione.

### Come funziona {#how-it-works-1}

Quando Sarah riempie e invia l&#39;applicazione FOIA, un record dell&#39;applicazione viene inviato alla inbox di John Jacobs. John Jacobs può visualizzare la domanda inviata e accettarla o rifiutarla.

### Vedere da soli {#see-it-yourself-1}

Potete accedere alla AEM inbox all&#39;indirizzo https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Accedete alla casella in entrata AEM utilizzando jjacobs/password come nome utente/password per John Jacobs, e vedete l&#39;applicazione FOIA. Per informazioni sull&#39;utilizzo di AEM Inbox per le attività relative ai flussi di lavoro incentrate sui moduli, vedere [Gestione di applicazioni e attività Forms in AEM Inbox](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs può visualizzare, approvare o rifiutare l’applicazione dal dashboard dell’applicazione. John Jacobs seleziona e apre i dettagli della richiesta e, dopo aver rivisto la richiesta, la approva.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah riceve un messaggio e-mail di conferma</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Dopo che John Jacobs ha approvato l&#39;applicazione, Sarah riceve un messaggio e-mail di conferma dal sito We.Gov. Sarah viene informata sulle tariffe e sui tempi necessari per l&#39;elaborazione della sua domanda. L&#39;e-mail include anche i dettagli email e telefono sarah può contattare per gli aggiornamenti sulla sua applicazione.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria riceve la richiesta FOIA di approvazione di secondo livello {#gloria-receives-the-foia-request-for-second-level-approval}

Dopo che John Jacobs ha compilato le informazioni richieste e approvato la richiesta di Sarah, le richieste vanno a Gloria Rios per l&#39;approvazione finale. Gloria rivede il documento di registrazione allegato e approva la richiesta.

![gloriariosinbox](assets/gloriariosinbox.png)

### Come funziona {#how-it-works-2}

Quando John Jacobs approva la richiesta FOIA, viene creato un PDF o un documento di registrazione dell&#39;applicazione e inviato alla inbox di Gloria Rios. Gloria può visualizzare la richiesta inviata e approvarla o rifiutarla.

### Vedere per se stessi {#see-for-yourself}

Potete accedere alla AEM inbox all&#39;indirizzo https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Accedete alla casella in entrata AEM utilizzando grios/password come nome utente/password per Gloria Rios e vedete la richiesta FOIS.

Gloria apre la richiesta ed esamina i dettagli della richiesta FOIA. Dopo aver esaminato i dettagli della richiesta e verificato la fattibilità dell&#39;invio dei documenti richiesti, Gloria approva la richiesta.

![gloriariosassoni](assets/gloriariosapproves.png)

## Sarah riceve la notifica che la sua richiesta è stata approvata {#sarah-receives-notification-that-her-request-is-approved}

Dopo che Gloria ha approvato la richiesta FOIA, Sarah riceve un&#39;e-mail di notifica della sua richiesta. L&#39;e-mail include anche informazioni sulla tempistica provvisoria per l&#39;invio del documento e i recapiti per il follow-up sulla richiesta.

![sarahroseemailApproval](assets/sarahroseemailapproval.png)

