---
title: Procedura dettagliata sul sito di riferimento We.Gov FOIA
seo-title: We.Gov reference site FOIA walkthrough
description: Consulta la procedura dettagliata sul sito di riferimento We.Gov per comprendere in che modo AEM Forms aiuta i governi a ricevere e inviare le informazioni richieste dalle persone ai sensi del Freedom of Information Act.
seo-description: See the We.Gov reference site walkthrough to understand how AEM Forms helps governments receive and impart information requested by individuals under the Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Procedura dettagliata sul sito di riferimento We.Gov FOIA {#we-gov-reference-site-foia-walkthrough}

## Scenario di riferimento Freedom Information Act {#reference-site-freedom-of-information-act-scenario}

We.Gov è un&#39;organizzazione statale che permette ai genitori adottivi di iscriversi al supporto dei figli se hanno adottato un bambino. We.Gov consente inoltre ai genitori di richiedere informazioni ai seguenti dipartimenti governativi in base alla legge sulla libertà di informazione:

* Agenzia per la logistica della difesa
* Ufficio di controllo generale del ministero della difesa
* Dipartimento di Giustizia - Ufficio per la politica dell&#39;informazione
* Dipartimento della Marina Militare
* Agenzia per la protezione ambientale

Per maggiori informazioni sulla legge sulla libertà di informazione, vedi [www.foia.gov](https://www.foia.gov).

Lo scenario include i seguenti utenti tipo:

* Sarah Rose, la persona che richiede informazioni in
* John Jacobs, la persona che gestisce la richiesta la inoltra al reparto competente
* Gloria Rios, dipendente governativo che fornisce le informazioni secondo la richiesta

## Sarah avvia la richiesta di informazioni in base all&#39;UFFICIO {#sarah-initiates-request-for-information-under-foia}

Secondo la legge sulla libertà di informazione, Sarah richiede una copia del caso di registro dell&#39;Amministrazione per bambini e famiglie per anni (FY) dal 2013 al 2016. Sarah presenta questa richiesta al Dipartimento di Giustizia - Ufficio per la Politica d&#39;Informazione e indica anche che è disposta a pagare fino a 100 dollari per le spese di stampa e postali.

### Come funziona {#how-it-works}

### Vedi di persona {#see-it-yourself}

Nel browser, apri `https://<hostname>:<PublishPort>/wegov`. Nel sito We.Gov, tocca Applicazioni > Tutte le applicazioni. Nella pagina Tutte le applicazioni, toccare Applica in Applicazione per Richiesta FOIA.

## Sarah avvia la sua domanda di informazioni sotto FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah clicca **Applica** e nella pagina Modulo di richiesta della legge sulla libertà di informazione, Sarah inserisce informazioni tra cui:

* **Agenzia:** Sarah specifica l&#39;agenzia a cui la richiesta è stata indirizzata come Dipartimento di Giustizia - Ufficio per la Politica d&#39;Informazione.

* **Paga fino a**: Sarah specifica che è disposta a pagare fino a 100 dollari per le spese di stampa e postali.
* **Descrivi dettagliatamente la richiesta**: Sarah specifica &quot;Richiesta di copia dei casi di amministrazione per bambini e famiglie per gli anni fiscali dal 2013 al 2016&quot;.

![Richiesta di copia del caso di registro dell&#39;Amministrazione per bambini e famiglie per gli esercizi fiscali dal 2013 al 2016](assets/sarahfiosform.png)

Richiesta di copia del caso di registro dell&#39;Amministrazione per bambini e famiglie per gli esercizi fiscali dal 2013 al 2016

In qualsiasi momento, Sarah può toccare Salva per salvare la bozza del modulo e tornare più tardi per compilare il modulo e inviarlo. Sarah invia il modulo.

>[!NOTE]
>
>Il flusso di lavoro di ripresa da e-mail funziona solo con gli utenti registrati. Nello scenario relativo al sito di riferimento, assicurati che l’utente Sarah Rose sia aggiunto. Le credenziali di accesso di Sarah sono `srose/password`.

## John Jacobs riceve e approva l&#39;applicazione {#john-jacobs-receives-and-approves-the-application}

John Jacobs riceve le richieste e le indirizza alla persona giusta. AEM casella in entrata consente di visualizzare tutte le applicazioni inviate in un’unica posizione.

### Come funziona {#how-it-works-1}

Quando Sarah compila e invia l&#39;applicazione FOIA, un record dell&#39;applicazione viene inviato alla casella in entrata di John Jacobs. John Jacobs può visualizzare la domanda inviata e accettarla o rifiutarla.

### Vedi di persona {#see-it-yourself-1}

Puoi accedere alla casella in entrata AEM all’indirizzo https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Accedi alla casella in entrata AEM utilizzando jjacobs/password come nome utente/password per John Jacobs e vedi l&#39;applicazione FOIA. Per informazioni sull’utilizzo della casella in entrata AEM per le attività del flusso di lavoro incentrate sui moduli, vedere [Gestione di applicazioni e attività Forms nella casella in entrata AEM](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs può visualizzare, approvare o rifiutare l&#39;applicazione dal dashboard dell&#39;applicazione. John Jacobs seleziona e apre i dettagli della richiesta e dopo aver rivisto la richiesta, la approva.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah riceve un&#39;e-mail di riconoscimento</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Dopo che John Jacobs approva l&#39;applicazione, Sarah riceve un messaggio e-mail di riconoscimento dal sito We.Gov. Sarah viene informata delle tariffe e del tempo necessario per l&#39;elaborazione della sua domanda. L&#39;e-mail include anche le email e i numeri di telefono che sarah può contattare per gli aggiornamenti sulla sua applicazione.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria riceve la richiesta FOIA di approvazione di secondo livello {#gloria-receives-the-foia-request-for-second-level-approval}

Dopo che John Jacobs ha compilato le informazioni richieste e approvato la richiesta di Sarah, le richieste vanno a Gloria Rios per l&#39;approvazione finale. Gloria rivede il documento di registrazione allegato e approva la richiesta.

![gloriariosinbox](assets/gloriariosinbox.png)

### Come funziona {#how-it-works-2}

Quando John Jacobs approva la richiesta FOIA, viene creato un PDF o un documento di registrazione dell&#39;applicazione e inviato alla casella in entrata di Gloria Rios. Gloria può visualizzare la richiesta inviata e approvarla o rifiutarla.

### Vedi te stesso {#see-for-yourself}

Puoi accedere alla casella in entrata AEM all’indirizzo https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Accedi alla casella in entrata AEM utilizzando grios/password come nome utente/password per Gloria Rios e vedi la richiesta FOIS.

Gloria apre la richiesta ed esamina i dettagli della richiesta FOIA. Dopo aver esaminato i dettagli della richiesta e verificato la fattibilità dell&#39;arredamento dei documenti richiesti, Gloria approva la richiesta.

![gloriariosapproves](assets/gloriariosapproves.png)

## Sarah riceve la notifica che la sua richiesta è stata approvata {#sarah-receives-notification-that-her-request-is-approved}

Dopo che Gloria ha approvato la richiesta FOIA, Sarah riceve un&#39;e-mail di notifica che la sua richiesta è stata approvata. L&#39;e-mail include anche le informazioni sul calendario provvisorio per l&#39;invio del documento e i dettagli di contatto per il follow-up sulla richiesta.

![sarahroseemailoapprovazione](assets/sarahroseemailapproval.png)
