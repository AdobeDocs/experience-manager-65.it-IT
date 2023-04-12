---
title: Tracciamento e-mail rimbalzate
seo-title: Tracking Bounced Emails
description: Quando invii una newsletter a molti utenti, in genere ci sono alcuni indirizzi e-mail non validi nell’elenco. L'invio di newsletter a tali indirizzi non viene recapitato. AEM gestire questi messaggi non recapitati e può interrompere l'invio di newsletter a tali indirizzi dopo il superamento del contatore non recapitato configurato.
seo-description: When you send a newsletter to many users, there are usually some invalid emails addresses in the list. Sending newsletters to those addresses bounce back. AEM is capable of managing those bounces and can stop sending newsletters to those addresses after the configured bounce counter is exceeded.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Tracciamento e-mail rimbalzate{#tracking-bounced-emails}

>[!NOTE]
>
>L’Adobe non prevede di migliorare ulteriormente il tracciamento delle e-mail aperte/rimbalzate inviate dal servizio SMTP AEM.
>
>La raccomandazione è di [utilizzare Adobe Campaign e la relativa integrazione AEM](/help/sites-administering/campaign.md).

Quando invii una newsletter a molti utenti, in genere ci sono alcuni indirizzi e-mail non validi nell’elenco. L&#39;invio di newsletter a tali indirizzi non viene recapitato. AEM gestire questi messaggi non recapitati e può interrompere l&#39;invio di newsletter a tali indirizzi dopo il superamento del contatore non recapitato configurato. Per impostazione predefinita, la frequenza di rimbalzo è impostata su 3 ma è configurabile.

Per impostare AEM per il tracciamento delle e-mail rimbalzate, imposta AEM per eseguire il polling di una cassetta postale esistente in cui vengono ricevute le e-mail rimbalzate. Di solito, si tratta dell’indirizzo e-mail &quot;Da&quot; specificato per l’invio della newsletter. AEM controlla questa casella in entrata e importa tutti i messaggi e-mail che si trovano nel percorso specificato nella configurazione di polling. Viene quindi attivato un flusso di lavoro per cercare gli indirizzi e-mail rimbalzati all’interno degli utenti e aggiorna di conseguenza il valore della proprietà bounceCounter dell’utente. Una volta superati i limiti massimi configurati, l’utente viene rimosso dall’elenco della newsletter.

## Configurazione di Feed Importer {#configuring-the-feed-importer}

Importazione feed consente di importare ripetutamente contenuti da fonti esterne nell’archivio. Con questa configurazione di Importazione feed, AEM controlla la casella del mittente per le e-mail rimbalzate.

Per configurare Importazione feed per il tracciamento delle e-mail rimbalzate, procedi come segue:

1. In **Strumenti**, seleziona Importazione feed.

1. Fai clic su **Aggiungi** per creare una configurazione.

   ![chlimage_1](assets/chlimage_1a.png)

1. Aggiungi una configurazione selezionando il tipo e aggiungendo informazioni all’URL di polling in modo da poter configurare l’host e la porta. Inoltre, aggiungi alcuni parametri di posta e di protocollo specifici alla query URL. Imposta la configurazione per il polling almeno una volta al giorno.

   Tutte le configurazioni richiedono informazioni su quanto segue nell’URL di polling:

   `username`: Nome utente utilizzato per la connessione

   `password`: Password utilizzata per la connessione

   Inoltre, a seconda del protocollo, puoi configurare alcune impostazioni.

   **Proprietà di configurazione POP3:**

   `pop3.leave.on.server`: Definisce se lasciare o meno i messaggi sul server. Imposta su true per lasciare i messaggi sul server, su false in caso contrario. Predefinito su true.

   **Esempi POP3:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | Utilizzo di pop3 su SSL per connettersi a Gmail sulla porta 995 con utente/segreto, lasciando i messaggi sul server per impostazione predefinita |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **Proprietà di configurazione IMAP:**

   Consente di impostare i flag da cercare.

   `imap.flag.SEEN`:Imposta false per i messaggi nuovi/non visualizzati, true per i messaggi già letti

   Vedi [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) per l&#39;elenco completo dei flag.

   **Esempi IMAP:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | Utilizzo di IMAP su SSL per connettersi a Gmail sulla porta 993 con utente/segreto. Per impostazione predefinita, è possibile ricevere solo i nuovi messaggi. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | Usare IMAP su SSL per connettersi a GMail 993 con utente/segreto, ricevendo solo messaggi già visti. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | Utilizzo di IMAP su SSL per connettersi a Gmail 993 con utente/segreto, ricezione di messaggi già letti O nuovi. |

1. Salva la configurazione.

## Configurazione del componente del servizio newsletter {#configuring-the-newsletter-service-component}

Dopo aver configurato Importazione feed, configura l’indirizzo Da e il contatore di rimbalzo.

Per configurare il servizio newsletter:

1. Nella console OSGi, in `<host>:<port>/system/console/configMgr`, passa a **Newsletter MCM**.

1. Configura il servizio e salva le modifiche al termine.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   È possibile impostare le seguenti configurazioni per regolare il comportamento:

   | Massimo contatore rimbalzi (max.bounce.count) | Definisce il numero di rimbalzi fino a quando un utente non viene omesso quando invia una newsletter. Impostando questo valore su 0, il controllo non recapitato viene disattivato completamente. |
   |---|---|
   | Attività senza cache (sent.activity.nocache) | Definisce l’impostazione della cache da utilizzare per l’attività newsletter inviata |

   Una volta salvato, il servizio MCM per newsletter effettua le seguenti operazioni:

   * Scrive un’attività al flusso nascosto degli utenti dopo l’invio di una newsletter.
   * Scrive un&#39;attività se viene rilevato un rimbalzo e il contatore di rimbalzi degli utenti viene modificato.
