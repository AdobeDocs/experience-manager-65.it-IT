---
title: Configurazione degli endpoint e-mail
seo-title: Configurazione degli endpoint e-mail
description: Scoprite come configurare gli endpoint e-mail.
seo-description: Scoprite come configurare gli endpoint e-mail.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '3766'
ht-degree: 0%

---


# Configurazione degli endpoint e-mail {#configuring-email-endpoints}

Gli endpoint e-mail consentono agli utenti di richiamare un servizio inviando uno o più documenti (come allegati e-mail) a un account e-mail specificato. La casella in entrata dell’e-mail funge da punto di raccolta per gli allegati. Il servizio controlla la inbox ed elabora gli allegati. I risultati della conversione vengono inoltrati all&#39;utente definito nell&#39;endpoint.

Per un endpoint e-mail, gli utenti autorizzati possono richiamare un processo inviando i file all&#39;account appropriato. I risultati verranno restituiti all&#39;utente che ha inviato l&#39;invio (per impostazione predefinita) o all&#39;utente definito nelle impostazioni dell&#39;endpoint.

Prima di configurare un endpoint e-mail, create un account e-mail POP3 o IMAP da utilizzare per l&#39;endpoint. Configurate un account separato per ciascun tipo di conversione. Ad esempio, un account può essere configurato per generare documenti PDF standard da allegati di file in entrata e un altro account può essere configurato per generare documenti PDF protetti.

>[!NOTE]
>
>Ogni indirizzo e-mail deve essere mappato su un solo endpoint e-mail. Non potete configurare più endpoint e-mail su un unico indirizzo e-mail, anche se gli endpoint e-mail aggiuntivi sono disattivati.

Tutti gli endpoint e-mail sono configurati con un nome utente e una password autorizzati per la inbox e-mail, necessari quando si richiama il servizio. L&#39;account e-mail è protetto dal sistema del server di posta in cui è configurato.

Se gli utenti inviano documenti con caratteri di lingua occidentale europea nei nomi di file e percorsi di conversione, devono utilizzare un&#39;applicazione e-mail che supporti i tipi di codifica richiesti (Latin1 [ISO-8859-1], Western European [Windows] o UTF-8). Per ulteriori informazioni, vedere il documento *Installazione e distribuzione di moduli AEM* per il server delle applicazioni.

Prima di configurare un endpoint e-mail, configurate il servizio e-mail. (Vedere [Configurare le impostazioni dell&#39;endpoint e-mail predefinito](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) I parametri di configurazione del servizio e-mail hanno due scopi:

* Per configurare gli attributi comuni a tutti gli endpoint e-mail
* Per fornire valori predefiniti per tutti gli endpoint e-mail

## Configurare SSL per un endpoint e-mail {#configure-ssl-for-an-email-endpoint}

È possibile configurare POP3, IMAP o SMTP per utilizzare Secure Sockets Layer (SSL) per un endpoint e-mail.

1. Nel server e-mail, abilitate SSL per POP3, IMAP o SMTP in base alla documentazione del produttore.
1. Esportate un certificato client dal server e-mail.
1. Utilizzare il programma keytool per importare il file del certificato client nell&#39;archivio certificati Java Virtual Machine (JVM) del server applicazioni. La procedura per questo passaggio dipenderà dai percorsi di installazione JVM e client.

   Ad esempio, se si utilizza un&#39;installazione predefinita  Oracle WebLogic Server con JDK 1.5.0 in Microsoft Windows Server® 2003, digitare il testo seguente in un prompt dei comandi:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Quando richiesto, immettete la password (per Java, la password predefinita è `changeit`). Riceverete un messaggio in cui si informa che il certificato è stato importato correttamente.
1. Utilizzate la console di amministrazione per aggiungere l&#39;endpoint e-mail al servizio.
1. Create l’endpoint e-mail nella console di amministrazione. Durante la configurazione delle impostazioni dell&#39;endpoint, selezionare l&#39;SSL POP3/IMAP abilitato per i messaggi in arrivo e l&#39;SSL SMTP abilitato per i messaggi in uscita, quindi modificare di conseguenza le proprietà della porta.

>[!NOTE]
>
>Suggerimento: Se si verificano dei problemi durante l’utilizzo di SSL, utilizzate un client e-mail come Microsoft Outlook per verificare se può accedere al server e-mail utilizzando SSL. Se il client di posta elettronica non è in grado di accedere al server di posta elettronica, il problema è correlato alla configurazione del certificato o del server di posta elettronica.

## Configurare le impostazioni predefinite dell&#39;endpoint e-mail {#configure-default-email-endpoint-settings}

Potete utilizzare la pagina Gestione servizi per configurare gli attributi comuni a tutti gli endpoint e-mail e per fornire valori predefiniti per tutti gli endpoint e-mail.

Per consentire al flusso di lavoro dei moduli di ricevere e gestire i messaggi e-mail in arrivo dagli utenti, è necessario creare un endpoint e-mail per il servizio Attività completa. Questo endpoint e-mail richiede impostazioni aggiuntive, come descritto in [Creare un endpoint e-mail per il servizio Attività completa](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Modificare i valori predefiniti per gli endpoint e-mail {#change-the-default-values-for-email-endpoints}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione dei servizi, fai clic su E-mail: 1.0 (l&#39;ID componente è com.adobe.idp.dsc.provider.service.email.Email).
1. Nella scheda Configurazione, specificate le impostazioni dell&#39;endpoint e-mail predefinito, quindi fate clic su Salva.

### Impostazioni endpoint e-mail predefinite {#default-email-endpoint-settings}

**Espressione cron:** l&#39;espressione cron utilizzata dal quarzo per pianificare il polling della directory di input.

**Intervallo ripetizione:** il numero di volte in cui il polling della directory viene ripetuto. L&#39;intervallo di ripetizione predefinito è espresso in secondi se questo valore non è specificato nella configurazione dell&#39;endpoint. Il valore predefinito è 10. Questo valore non può essere minore di 10.

**Ripeti conteggio:** il numero di volte in cui viene effettuato il polling della directory di input. Conteggio ripetizioni predefinito da utilizzare se questo valore non è specificato nella configurazione dell&#39;endpoint. Il valore -1 indica la scansione indefinita della directory. Il valore predefinito è -1.

**Ritardo all’avvio del processo:** il valore predefinito, in secondi, per il ritardo prima che il processo inizi la scansione dell’endpoint. Il valore predefinito è 0.

**Dimensione batch:** il numero di e-mail che il ricevitore elabora per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.

**Asincrono:** identifica il tipo di chiamata come asincrono o sincrono. I processi transitori e sincroni possono essere invocati solo in modo sincrono. Il valore predefinito è asincrono.

**Pattern di dominio:** il pattern del nome di dominio utilizzato per filtrare le e-mail in arrivo. Ad esempio, se si utilizza adobe.com, verranno elaborati solo i messaggi e-mail inviati da adobe.com; le e-mail provenienti da altri domini vengono ignorate.

**Pattern file:** i pattern di allegati che il provider accetta. Questo include file con estensioni specifiche (&amp;ast;.dat, &amp;ast;.xml), nomi specifici (dati) ed espressioni composite nel nome e nell&#39;estensione (.[dD][aA]&#39;port&#39;). Il valore predefinito è &amp;ast;.&amp;ast;.

**Destinatari del processo di successo:** Uno o più indirizzi e-mail utilizzati per inviare e-mail per indicare processi riusciti. Per impostazione predefinita, un messaggio di processo riuscito viene sempre inviato al mittente del processo iniziale. Sono supportati fino a 100 destinatari. Per disattivare questa impostazione, lasciare vuoto questo campo.

**Destinatari del processo non riuscito:** Uno o più indirizzi e-mail utilizzati per inviare e-mail per indicare processi non riusciti. Per impostazione predefinita, al mittente che ha inviato il processo iniziale viene sempre inviato un messaggio di processo non riuscito. Sono supportati fino a 100 destinatari. Per disattivare questa impostazione, lasciare vuoto questo campo.

**Host Posta in arrivo:** nome host della inbox o indirizzo IP per il provider di posta elettronica da analizzare.

**Porta inbox:** il numero della porta della inbox che il provider di posta elettronica deve analizzare. Se il valore è 0, verrà utilizzata la porta IMAP o POP3 predefinita.

**Protocollo Inbox:** protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della inbox. Le opzioni disponibili sono IMAP o POP3. Il server di posta elettronica dell&#39;host della inbox deve supportare questi protocolli.

**Tempo inbox:** specifica la quantità di tempo che l&#39;endpoint attenderà prima dell&#39;annullamento quando si tenta di connettersi alla inbox. Se una connessione non viene acquisita prima del raggiungimento del valore di timeout, il polling della inbox non viene eseguito.

**Utente Casella in entrata:** nome utente necessario per accedere all’account e-mail. A seconda del server e-mail e della configurazione, questo nome può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.

**Password casella in entrata:** la password per l&#39;utente della casella in entrata.

**SSL POP3/IMAP abilitato:** se selezionato, abilita SSL.

**Host SMTP:** Il nome host del server di posta elettronica utilizzato dal provider di posta elettronica per inviare i risultati e i messaggi di errore. Ad esempio, mail.corp.example.com.

**Porta SMTP:** La porta utilizzata per connettersi al server di posta. Il valore predefinito è 25.

**Utente SMTP:** L&#39;account utente del provider di posta elettronica da utilizzare per l&#39;invio di e-mail in caso di risultati ed errori.

**Password SMTP:** La password per l&#39;account SMTP. Alcuni server di posta elettronica non richiedono una password SMTP.

**Invia da:** l&#39;indirizzo e-mail (ad esempio, user@company.com) utilizzato per inviare le notifiche e-mail di risultati ed errori. Se non si specifica un valore Invia da, il server e-mail tenta di determinare l&#39;indirizzo e-mail combinando il valore specificato nell&#39;impostazione Utente SMTP con un dominio predefinito configurato sul server e-mail. Se il server e-mail non dispone di un dominio predefinito e non si specifica un valore per Invia da, potrebbero verificarsi degli errori. Per fare in modo che i messaggi e-mail abbiano l&#39;indirizzo da corretto, specificate un valore per l&#39;impostazione Invia da.

**SSL SMTP abilitato:** se selezionato, abilita SSL su SMTP.

**Includi il corpo dell’e-mail originale come allegato:** per impostazione predefinita, quando si invia un messaggio e-mail al server dei moduli, il testo originale del messaggio viene incluso nel corpo del messaggio. Per includere il testo come allegato, selezionare questa opzione.

**Usa la riga oggetto originale per le e-mail dei risultati:** per impostazione predefinita, il server Forms utilizza i valori specificati nelle impostazioni Oggetto e-mail di successo e Oggetto e-mail di errore come oggetto per l’invio dei messaggi e-mail dei risultati. Per utilizzare la stessa riga dell&#39;oggetto del messaggio e-mail originale inviato al server, selezionare questa opzione.

**Oggetto e-mail di successo:** Dopo aver inviato un messaggio e-mail a un endpoint e-mail per avviare o continuare un processo, si riceverà un messaggio e-mail di ritorno dal server dei moduli di AEM. Se l’e-mail ha esito positivo, riceverete un messaggio e-mail di successo. Se l’e-mail non riesce, riceverete un messaggio e-mail di errore in cui viene indicato il motivo dell’errore. Questa impostazione consente di specificare l&#39;oggetto dei messaggi e-mail di successo inviati per l&#39;endpoint.

**Corpo e-mail di successo:** consente di specificare il corpo dei messaggi e-mail di successo inviati per questo endpoint.

**Prefisso oggetto e-mail errore:** consente di specificare il testo utilizzato all&#39;inizio della riga dell&#39;oggetto dei messaggi e-mail di errore inviati per l&#39;endpoint.

**Oggetto e-mail errore:** consente di specificare l&#39;oggetto dei messaggi e-mail di errore inviati per l&#39;endpoint. Questo testo viene visualizzato dopo il prefisso Oggetto e-mail di errore.

**Corpo e-mail errore:** consente di specificare la prima riga nel testo corpo dei messaggi e-mail di errore inviati per l&#39;endpoint.

**Informazioni riepilogo e-mail:** ogni messaggio di riuscita o di errore include una sezione contenente il testo e-mail originale inviato al server dei moduli. Questa impostazione specifica il testo visualizzato sopra la sezione.

**Convalida della casella in entrata prima di creare/aggiornare questo endpoint:** quando questa opzione è selezionata, il server moduli verifica se le impostazioni SMTP/POP3 sono corrette prima di creare l&#39;endpoint. Quando fate clic su Aggiungi, viene visualizzato un messaggio in cui viene indicato se l’account della inbox è valido. Se questa opzione non è selezionata, il server moduli AEM crea l&#39;endpoint senza convalidare la inbox.

**Codifica set di caratteri:** il formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in un ambiente giapponese possono scegliere lo standard ISO2022-JP.

**Cartella inviata per e-mail non riuscita:** specifica una directory in cui memorizzare i risultati se il server di posta SMTP non è operativo.

## Impostazioni endpoint e-mail {#email-endpoint-settings}

Utilizzate le seguenti impostazioni per configurare un endpoint e-mail.

**Nome:** Un&#39;impostazione obbligatoria che identifica l&#39;endpoint. Non includete un carattere &lt; perché tronca il nome visualizzato in Workspace. Se immettete un URL come nome dell’endpoint, accertatevi che sia conforme alle regole di sintassi specificate in RFC1738.

**Descrizione:** una descrizione dell’endpoint. Non includere un carattere &lt; perché tronca la descrizione visualizzata in Workspace.

**Espressione cron:** immettere un&#39;espressione cron se l&#39;e-mail deve essere pianificata utilizzando un&#39;espressione cron.

**Conteggio ripetizioni:** numero di volte in cui l’endpoint e-mail esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.

**Intervallo di ripetizione:** la frequenza di scansione utilizzata dal ricevitore per controllare la posta in arrivo.

**Ritardo all&#39;avvio del processo:** tempo di attesa per l&#39;analisi dopo l&#39;avvio del pianificatore.

**Dimensione batch:** il numero di e-mail che il ricevitore elabora per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.

**Nome utente:** un&#39;impostazione obbligatoria, ovvero il nome utente utilizzato per richiamare un servizio di destinazione dall&#39;e-mail. Il valore predefinito è SuperAdmin.

**Nome dominio:** un&#39;impostazione obbligatoria, ossia il dominio dell&#39;utente. Il valore predefinito è DefaultDom.

**Pattern di dominio:** specifica i pattern di dominio dell&#39;e-mail in arrivo che il provider accetta. Ad esempio, se viene utilizzato adobe.com, viene elaborato solo il messaggio e-mail inviato da adobe.com; le e-mail provenienti da altri domini vengono ignorate.

**Pattern file:** specifica i pattern di allegati che il provider accetta. Questo include file con estensioni specifiche (&amp;ast;.dat, &amp;ast;.xml), nomi specifici (dati) o espressioni composite nel nome e nell&#39;estensione (&amp;ast;.[dD][aA]&#39;port&#39;).

**Destinatari del processo di successo:** un indirizzo e-mail cui vengono inviati messaggi per indicare l’esito positivo dei processi. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di processo riuscito. Se digitate il mittente, i risultati dell&#39;e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specificate altri destinatari con indirizzi e-mail, separati da virgole (,).

Per disattivare questa impostazione, lasciare vuota l&#39;impostazione. In alcuni casi, si desidera attivare un processo e non si desidera inviare una notifica via e-mail del risultato.

**Destinatari del processo non riuscito:** un indirizzo e-mail a cui vengono inviati messaggi per indicare processi non riusciti. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di processo non riuscito. Se digitate il mittente, i risultati dell&#39;e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specificate altri destinatari con indirizzi e-mail, separati da virgole (,).

Per disattivare questa impostazione, lasciare vuota l&#39;impostazione. In alcuni casi, si desidera attivare un processo e non si desidera inviare una notifica via e-mail del risultato.

**Host Posta in arrivo:** nome host della inbox o indirizzo IP per il provider di posta elettronica da analizzare.

**Porta inbox:** la porta utilizzata dal server e-mail. Il valore predefinito per POP3 è 110 e il valore predefinito per IMAP è 143. Se SSL è abilitato, il valore predefinito per POP3 è 995 e il valore predefinito per IMAP è 993.

**Protocollo Inbox:** protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della inbox. I valori sono IMAP o POP3. Il server di posta elettronica dell&#39;host della inbox deve supportare questi protocolli.

**Tempo inbox in uscita:** il timeout, in secondi, per il provider di posta elettronica di attendere le risposte della inbox.

**Utente Casella in entrata:** nome utente necessario per accedere all’account e-mail. A seconda del server e-mail e della configurazione, questo valore può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.

**Password casella in entrata:** la password per l’utente della inbox.

**SSL POP3/IMAP abilitato:** selezionare questa impostazione per obbligare il provider di posta elettronica a utilizzare SSL per la scansione della inbox. Verificate che il server di posta elettronica supporti SSL.

**Host SMTP:** Il nome host del server di posta elettronica utilizzato dal provider di posta elettronica per inviare i risultati e i messaggi di errore.

**Porta SMTP:** Il valore predefinito per la porta SMTP è 25.

**Utente SMTP:** L&#39;account utente del provider di posta elettronica da utilizzare per l&#39;invio tramite e-mail di notifiche di risultati ed errori.

**Password SMTP:** La password per l&#39;account SMTP. Alcuni server di posta elettronica non richiedono una password SMTP.

**Invia da:** l&#39;indirizzo e-mail (ad esempio, user@company.com) utilizzato per inviare le notifiche e-mail di risultati ed errori. Se non si specifica un valore Invia da, il server e-mail tenta di determinare l&#39;indirizzo e-mail combinando il valore specificato nell&#39;impostazione Utente SMTP con un dominio predefinito configurato sul server e-mail. Se il server e-mail non dispone di un dominio predefinito e non si specifica un valore per Invia da, potrebbero verificarsi degli errori. Per fare in modo che i messaggi e-mail abbiano l&#39;indirizzo da corretto, specificate un valore per l&#39;impostazione Invia da.

**SSL SMTP abilitato:** selezionate questa impostazione per obbligare il provider di posta elettronica a utilizzare SSL per eseguire la scansione della inbox. Verificate che il server di posta elettronica supporti SSL.

**Cartella inviata per e-mail non riuscita:** specifica una directory in cui memorizzare i risultati se il server di posta SMTP non è operativo.

**asincrono:** quando è impostato su sincrono, tutti i documenti di input vengono elaborati e viene restituita una sola risposta. Quando è impostata su asincrona, viene inviata una risposta per ogni documento elaborato.

Ad esempio, viene creato un endpoint e-mail per un servizio che prende un singolo documento Word e lo restituisce come file PDF. È possibile inviare un messaggio e-mail alla inbox dell&#39;endpoint contenente più (3) documenti Word. Quando tutti e tre i documenti vengono elaborati, se l&#39;endpoint è configurato come sincrono, viene inviato un unico messaggio e-mail di risposta con tutti e tre i documenti allegati. Se l&#39;endpoint è asincrono, viene inviato un messaggio e-mail di risposta dopo che ogni documento di Word è stato convertito in PDF. Il risultato è tre e-mail, ciascuna con un singolo allegato PDF.

Il valore predefinito è asincrono.

**Includere il corpo del messaggio e-mail originale come allegato:** per impostazione predefinita, quando si invia un messaggio e-mail al server dei moduli, il testo originale del messaggio viene incluso nel corpo del messaggio. Per includere il testo come allegato, selezionare questa opzione.

**Utilizzate la riga dell&#39;oggetto originale per le e-mail dei risultati:** per impostazione predefinita, il server Forms utilizza i valori specificati nelle impostazioni Oggetto e-mail di successo e Oggetto e-mail di errore come oggetto per l&#39;invio dei messaggi e-mail dei risultati. Per utilizzare la stessa riga dell&#39;oggetto del messaggio e-mail originale inviato al server, selezionare questa opzione.

**Oggetto e-mail di successo:** Dopo aver inviato un messaggio e-mail a un endpoint e-mail per avviare o continuare un processo, si riceverà un messaggio e-mail di ritorno dal server dei moduli di AEM. Se l’e-mail ha esito positivo, riceverete un messaggio e-mail di successo. Se l’e-mail non riesce, riceverete un messaggio e-mail di errore in cui viene indicato il motivo dell’errore. Questa impostazione consente di specificare l&#39;oggetto dei messaggi e-mail di successo inviati per l&#39;endpoint.

**Corpo e-mail di successo:** consente di specificare il corpo dei messaggi e-mail di successo inviati per questo endpoint.

**Prefisso oggetto e-mail errore:** consente di specificare il testo utilizzato all&#39;inizio della riga dell&#39;oggetto dei messaggi e-mail di errore inviati per l&#39;endpoint.

**Oggetto e-mail errore:** consente di specificare l&#39;oggetto dei messaggi e-mail di errore inviati per l&#39;endpoint. Questo testo viene visualizzato dopo il prefisso Oggetto e-mail di errore.

**Corpo e-mail errore:** consente di specificare la prima riga nel testo corpo dei messaggi e-mail di errore inviati per l&#39;endpoint.

**Informazioni riepilogo e-mail:** ogni messaggio di riuscita o di errore include una sezione contenente il testo e-mail originale inviato al server dei moduli. Questa impostazione specifica il testo visualizzato sopra la sezione.

**Convalidare la casella in entrata prima di creare/aggiornare l&#39;endpoint:** Quando questa opzione è selezionata, il server moduli verifica se le impostazioni SMTP/POP3 sono corrette prima di creare l&#39;endpoint. Quando fate clic su Aggiungi, viene visualizzato un messaggio in cui viene indicato se l’account della inbox è valido. Se questa opzione non è selezionata, il server moduli AEM crea l&#39;endpoint senza convalidare la inbox.

**Nome operazione:** questa impostazione è obbligatoria. Elenco di operazioni che possono essere assegnate all’endpoint e-mail. L&#39;operazione selezionata qui determina quali campi vengono visualizzati nelle sezioni Mappature parametri di input e Mappature parametri di output.

**Mappature parametri di input:** utilizzato per configurare l&#39;input richiesto per l&#39;elaborazione del servizio e dell&#39;operazione. I due tipi di input sono letterali e variabili:

**Letterale:** Il messaggio e-mail utilizza il valore immesso nel campo così come viene visualizzato.

**Variabile:** potete mappare una stringa dall’oggetto dell’e-mail, dal corpo, dall’intestazione o dall’indirizzo e-mail del mittente. A questo scopo, utilizzare una delle seguenti parole chiave: %SUBJECT%, %BODY%, %HEADER% o %SENDER%. Ad esempio, se si utilizza %SUBJECT%, il contenuto dell&#39;oggetto dell&#39;e-mail viene utilizzato come parametro di input. Per raccogliere gli allegati, immettere un pattern di file che l&#39;endpoint e-mail può utilizzare per selezionare i documenti allegati. Ad esempio, immettendo &amp;ast;.pdf si seleziona qualsiasi documento allegato con estensione .pdf. Immissione di &amp;ast; seleziona qualsiasi documento allegato. Immettendo example.pdf si seleziona qualsiasi documento allegato denominato example.pdf.

**Mappature parametri di output:** utilizzato per configurare l&#39;output del servizio e dell&#39;operazione. I seguenti caratteri nei valori di mappatura dei parametri di output sono espansi nel nome del file allegato:

**%** FRrappresenta il nome del file di origine (senza estensione).

**%** ERrappresenta l&#39;estensione del file di origine.

Qualsiasi occorrenza della barra rovesciata (\) viene sostituita con %%.

***nota **: Se il messaggio di richiesta del servizio include più allegati di file, non è possibile utilizzare i parametri %F e %E per la proprietà Mappature parametri di output dell&#39;endpoint. Se la risposta dei servizi restituisce più allegati, non è possibile specificare lo stesso nome file per più allegati. Se non si seguono queste raccomandazioni, il servizio richiamato crea i nomi dei file restituiti e i nomi non sono prevedibili.*

Sono disponibili i seguenti valori:

**Oggetto singolo:** il provider di posta elettronica non ha la destinazione della cartella di origine; i risultati vengono restituiti come allegati. Il pattern è Result/%F.ps e restituisce Result%%sourcefilename.ps come allegato del nome del file.

**Elenco:** Il pattern è Result/%F/ e restituisce Result%%sourcefilename%%file1 come allegato del nome file.

**Mappa:** Il pattern è Result/%F/ e la destinazione di origine è Result%%sourcefilename%%file1 e Result%%sourcefilename%%file2. Se la mappa contiene più oggetti e il pattern è Result/%F.ps, gli allegati del file di risposta sono Result%%sourcefilename1.ps (output 1) e Result%%sourcefilename2.ps (output 2).

## Creare un endpoint e-mail per il servizio Attività completa {#create-an-email-endpoint-for-the-complete-task-service}

Per consentire al flusso di lavoro dei moduli di ricevere e gestire i messaggi e-mail in arrivo dagli utenti, è necessario creare un endpoint e-mail per il servizio Attività completa.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione dei servizi, fate clic sul servizio Attività completa.
1. Nella scheda Endpoint, selezionare E-mail dall&#39;elenco a discesa, quindi fare clic su Aggiungi.
1. Nella casella Host inbox digitare il nome host o l&#39;indirizzo IP del server di posta.
1. Nella casella Utente inbox, digitare il nome utente necessario per accedere all&#39;account e-mail creato per gestire l&#39;invio del modulo. A seconda del server e-mail e della configurazione, questo nome potrebbe essere solo la parte del nome utente dell’e-mail oppure l’indirizzo e-mail completo.
1. Nella casella Password inbox, digitare la password per l&#39;utente della inbox.
1. Nella casella Host SMTP, digitare il nome host o l&#39;indirizzo IP del server di posta elettronica dal quale il provider di posta elettronica invia i risultati e i messaggi di errore.
1. Nella casella Utente SMTP, digitare l&#39;account utente del provider di posta elettronica da utilizzare per l&#39;invio di messaggi e-mail in caso di risultati ed errori. Questo account utente può essere lo stesso valore utilizzato per Posta in arrivo.
1. Nella casella Password SMTP, digitare la password per l&#39;account SMTP.
1. Nell&#39;elenco Nome operazione, selezionare chiama.
1. Nell&#39;elenco attachmentMap, selezionare Variabile e digitare `*.*` nella casella adiacente. Questo invia tutti gli allegati dai messaggi di posta elettronica in entrata a una variabile di mappa per il processo Attività completa.
1. Nell&#39;elenco mailBody, selezionare la variabile e digitare `%BODY%` nella casella adiacente.
1. Nell&#39;elenco mailFrom, selezionare Variabile e digitare `%SENDER%` nella casella adiacente. In questo modo l&#39;indirizzo del mittente viene mappato sui dati del processo Attività completa.
1. Nella casella dei risultati, digitare `results`. Ciò fa sì che l&#39;attività Completa o il processo di avvio restituiscano una stringa di risultato.
1. Fate clic su Aggiungi.

