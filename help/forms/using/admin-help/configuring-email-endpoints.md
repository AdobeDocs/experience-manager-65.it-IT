---
title: Configurazione degli endpoint e-mail
seo-title: Configuring email endpoints
description: Scopri come configurare gli endpoint e-mail.
seo-description: Learn how to configure email endpoints.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
exl-id: 33583a12-4f20-4146-baa4-c9854e454bbf
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3757'
ht-degree: 0%

---

# Configurazione degli endpoint e-mail {#configuring-email-endpoints}

Gli endpoint e-mail consentono agli utenti di richiamare un servizio inviando uno o più documenti (come allegati e-mail) a un account e-mail specifico. La casella in entrata e-mail funge da punto di raccolta per gli allegati. Il servizio controlla la casella in entrata ed elabora gli allegati. I risultati della conversione vengono inoltrati all’utente definito nell’endpoint.

Per un endpoint e-mail, gli utenti autorizzati possono richiamare un processo inviando file all’account appropriato. I risultati verranno restituiti all’utente che ha inviato il modulo (per impostazione predefinita) o all’utente definito nelle impostazioni dell’endpoint.

Prima di configurare un endpoint e-mail, crea un account e-mail POP3 o IMAP da utilizzare per l’endpoint. Imposta un account separato per ciascun tipo di conversione. Ad esempio, è possibile configurare un account per generare documenti PDF standard da allegati di file in entrata e un altro account per generare documenti PDF protetti.

>[!NOTE]
>
>Ogni indirizzo e-mail deve essere mappato su un solo endpoint e-mail. Non puoi configurare più endpoint e-mail in un unico indirizzo e-mail, anche se gli endpoint e-mail aggiuntivi sono disattivati.

Tutti gli endpoint e-mail sono configurati con un nome utente e una password autorizzati per la casella in entrata e-mail, necessari quando si richiama il servizio. L’account e-mail è protetto dal sistema del server di posta in cui è configurato.

Se gli utenti inviano documenti con caratteri di lingua occidentale europea nei nomi dei file e dei percorsi di conversione, devono utilizzare un&#39;applicazione e-mail che supporti i tipi di codifica richiesti (Latin1 [ISO-8859-1], Europa occidentale [Windows]o UTF-8). Per ulteriori informazioni, consulta la sezione *Installazione e distribuzione di moduli AEM* documento per il server applicazioni.

Prima di configurare un endpoint e-mail, configura il servizio e-mail. (Vedi [Configurare le impostazioni dell’endpoint e-mail predefinite](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) I parametri di configurazione del servizio e-mail hanno due finalità:

* Per configurare gli attributi comuni a tutti gli endpoint e-mail
* Per fornire valori predefiniti per tutti gli endpoint e-mail

## Configurare SSL per un endpoint e-mail {#configure-ssl-for-an-email-endpoint}

È possibile configurare POP3, IMAP o SMTP per utilizzare Secure Sockets Layer (SSL) per un endpoint e-mail.

1. Sul server di posta elettronica, abilita SSL per POP3, IMAP o SMTP, in base alla documentazione del produttore.
1. Esporta un certificato client dal server e-mail.
1. Utilizza il programma keytool per importare il file del certificato client nell’archivio certificati Java Virtual Machine (JVM) del server dell’applicazione. La procedura per questo passaggio dipenderà dai percorsi di installazione JVM e client.

   Ad esempio, se utilizzi un&#39;installazione predefinita di Oracle WebLogic Server con JDK 1.5.0 su Microsoft Windows Server® 2003, digitare il testo seguente nel prompt dei comandi:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Quando richiesto, immetti la password (per Java, la password predefinita è `changeit`). Riceverai un messaggio in cui viene indicato che il certificato è stato importato correttamente.
1. Utilizza la console di amministrazione per aggiungere l’endpoint e-mail al servizio.
1. Crea l’endpoint e-mail nella console di amministrazione. Durante la configurazione delle impostazioni dell’endpoint, selezionare SSL POP3/IMAP abilitato per i messaggi in arrivo e SSL SMTP abilitato per i messaggi in uscita e modificare di conseguenza le proprietà della porta.

>[!NOTE]
>
>Suggerimento: Se rilevi dei problemi durante l&#39;utilizzo di SSL, utilizza un client e-mail come Microsoft Outlook per verificare se può accedere al server e-mail utilizzando SSL. Se il client di posta elettronica non può accedere al server di posta elettronica, il problema è correlato alla configurazione del certificato o del server di posta elettronica.

## Configurare le impostazioni dell’endpoint e-mail predefinite {#configure-default-email-endpoint-settings}

Puoi utilizzare la pagina Gestione servizi per configurare gli attributi comuni a tutti gli endpoint e-mail e per fornire valori predefiniti per tutti gli endpoint e-mail.

Affinché il flusso di lavoro dei moduli possa ricevere e gestire i messaggi e-mail in arrivo dagli utenti, è necessario creare un endpoint e-mail per il servizio Attività completa. Questo endpoint e-mail richiede impostazioni aggiuntive, come descritto in [Creare un endpoint e-mail per il servizio Attività completa](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Modificare i valori predefiniti per gli endpoint e-mail {#change-the-default-values-for-email-endpoints}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione servizi, fai clic su E-mail: 1.0 (l&#39;ID componente è com.adobe.idp.dsc.provider.service.email.Email).
1. Nella scheda Configurazione, specifica le impostazioni dell’endpoint e-mail predefinito, quindi fai clic su Salva.

### Impostazioni dell’endpoint e-mail predefinito {#default-email-endpoint-settings}

**Espressione Cron:** L&#39;espressione cron utilizzata dal quarzo per pianificare il polling della directory di input.

**Intervallo di ripetizione:** Numero di volte in cui viene ripetuto il polling della directory. L&#39;intervallo di ripetizione predefinito è in secondi se questo valore non è specificato nella configurazione dell&#39;endpoint. Il valore predefinito è 10. Questo valore non può essere inferiore a 10.

**Conteggio ripetizioni:** Numero di volte in cui viene effettuato il polling della directory di input. Il conteggio di ripetizione predefinito da utilizzare se questo valore non è specificato nella configurazione dell’endpoint. Il valore -1 indica una scansione indefinita della directory. Il valore predefinito è -1.

**Ritardo all&#39;avvio del processo:** Il valore predefinito, in secondi, per il ritardo prima che il processo inizi la scansione dell&#39;endpoint. Il valore predefinito è 0.

**Dimensione batch:** Il numero di e-mail che il ricevitore elabora per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.

**Asincrono:** Identifica il tipo di chiamata come asincrono o sincrono. I processi transitori e sincroni possono essere richiamati solo in modo sincrono. Il valore predefinito è asincrono.

**Pattern di dominio:** Il pattern del nome di dominio utilizzato per filtrare le e-mail in arrivo. Ad esempio, se utilizzi adobe.com, verranno elaborati solo i messaggi e-mail provenienti da adobe.com; le e-mail provenienti da altri domini vengono ignorate.

**Pattern file:** I pattern di file allegato in ingresso accettati dal provider. Ciò include i file con estensioni specifiche (&amp;ast;.dat, &amp;ast;.xml), nomi specifici (dati) ed espressioni composite nel nome e nell&#39;estensione (.[dD][aA]&quot;port&quot;). Il valore predefinito è &amp;ast;.&amp;ast;.

**Destinatari del processo riuscito:** Uno o più indirizzi e-mail utilizzati per inviare e-mail per indicare processi riusciti. Per impostazione predefinita, al mittente del processo iniziale viene sempre inviato un messaggio di lavoro riuscito. Sono supportati fino a 100 destinatari. Per disattivare questa impostazione, lasciare vuoto questo campo.

**Destinatari del processo non riuscito:** Uno o più indirizzi e-mail utilizzati per inviare e-mail per indicare processi non riusciti. Per impostazione predefinita, al mittente che ha inviato il processo iniziale viene sempre inviato un messaggio di lavoro non riuscito. Sono supportati fino a 100 destinatari. Per disattivare questa impostazione, lasciare vuoto questo campo.

**Host casella in entrata:** Nome host della casella in entrata o indirizzo IP da analizzare dal provider di posta elettronica.

**Porta in entrata:** Numero della porta in entrata per il provider di posta elettronica da analizzare. Se il valore è 0, verrà utilizzata la porta IMAP o POP3 predefinita.

**Protocollo casella in entrata:** Il protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della casella in entrata. Le scelte sono IMAP o POP3. Il server di posta elettronica host della casella in entrata deve supportare questi protocolli.

**Timeout casella in entrata:** Specifica il tempo di attesa dell&#39;endpoint prima dell&#39;annullamento durante il tentativo di connessione alla casella in entrata. Se una connessione non viene acquisita prima del raggiungimento del valore di timeout, il polling della casella in entrata non viene eseguito.

**Utente casella in entrata:** Nome utente necessario per accedere all’account e-mail. A seconda del server e-mail e della configurazione, questo nome può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.

**Password casella in entrata:** Password per l&#39;utente in entrata.

**SSL POP3/IMAP abilitato:** Se selezionata, abilita SSL.

**Host SMTP:** Nome host del server di posta che il provider di posta elettronica utilizza per inviare i risultati e i messaggi di errore. Ad esempio, mail.example.com.

**Porta SMTP:** La porta utilizzata per la connessione al server di posta. Il valore predefinito è 25.

**Utente SMTP:** L’account utente del provider di posta elettronica da utilizzare quando invia e-mail per risultati ed errori.

**Password SMTP:** Password dell&#39;account SMTP. Alcuni server di posta non richiedono una password SMTP.

**Invia da:** L’indirizzo e-mail (ad esempio, user@company.com) utilizzato per inviare notifiche e-mail di risultati ed errori. Se non si specifica un valore Invia da, il server e-mail tenta di determinare l’indirizzo e-mail combinando il valore specificato nell’impostazione Utente SMTP con un dominio predefinito configurato sul server e-mail. Se il server di posta elettronica non dispone di un dominio predefinito e non si specifica un valore per Invia da, potrebbero verificarsi errori. Per garantire che l’indirizzo del messaggio e-mail sia corretto, specifica un valore per l’impostazione Invia da.

**SSL SMTP abilitato:** Se selezionata, abilita SSL su SMTP.

**Includi Il Corpo E-Mail Originale Come Allegato:** Per impostazione predefinita, quando si invia un’e-mail al server dei moduli, il testo originale del messaggio viene incluso nel corpo del messaggio. Per includere invece il testo come allegato, selezionare questa opzione.

**Utilizza La Riga Oggetto Originale Per Le E-Mail Di Risultato:** Per impostazione predefinita, il server Forms utilizza come oggetto i valori specificati nelle impostazioni Soggetto e-mail con esito positivo e Oggetto e-mail con errore durante l’invio dei messaggi e-mail con risultati. Per utilizzare invece la stessa riga dell’oggetto dell’e-mail originale inviata al server, seleziona questa opzione.

**Oggetto e-mail di successo:** Dopo aver inviato un’e-mail a un endpoint e-mail per avviare o continuare un processo, riceverai un messaggio e-mail di ritorno dal server dei moduli di AEM. Se l’e-mail ha esito positivo, riceverai un messaggio e-mail di successo. Se l’e-mail non riesce, riceverai un messaggio e-mail di errore per informarne il motivo dell’errore. Questa impostazione consente di specificare l’oggetto dei messaggi e-mail di successo inviati per l’endpoint.

**Corpo e-mail di successo:** Consente di specificare il corpo dei messaggi e-mail con esito positivo inviati per l’endpoint.

**Prefisso oggetto e-mail errore:** Consente di specificare il testo utilizzato all’inizio della riga dell’oggetto dei messaggi e-mail di errore inviati per l’endpoint.

**Oggetto e-mail errore:** Consente di specificare l’oggetto dei messaggi e-mail di errore inviati per l’endpoint. Questo testo viene visualizzato dopo il prefisso Oggetto e-mail di errore.

**Corpo e-mail errore:** Consente di specificare la prima riga nel testo del corpo dei messaggi e-mail di errore inviati per l’endpoint.

**Informazioni di riepilogo e-mail:** Ogni messaggio di errore o di successo include una sezione contenente il testo e-mail originale inviato al server dei moduli. Questa impostazione specifica il testo visualizzato sopra la sezione.

**Convalida La Casella In Entrata Prima Di Creare/Aggiornare Questo Endpoint:** Quando questa opzione è selezionata, il server dei moduli controlla se le impostazioni SMTP/POP3 sono corrette prima di creare l’endpoint. Quando fai clic su Aggiungi, viene visualizzato un messaggio che indica se l’account della casella in entrata è valido. Se questa opzione non è selezionata, il server dei moduli AEM crea l’endpoint senza convalidare la casella in entrata.

**Codifica set di caratteri:** Formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in un ambiente giapponese possono scegliere ISO2022-JP.

**Cartella inviata via e-mail non riuscita:** Specifica una directory in cui memorizzare i risultati se il server di posta SMTP non è operativo.

## Impostazioni dell’endpoint e-mail {#email-endpoint-settings}

Utilizza le seguenti impostazioni per configurare un endpoint e-mail.

**Nome:** Impostazione obbligatoria che identifica l’endpoint. Non includere un carattere &lt; perché tronca il nome visualizzato in Workspace. Se immetti un URL come nome dell’endpoint, accertati che sia conforme alle regole di sintassi specificate nella RFC1738.

**Descrizione:** Descrizione dell&#39;endpoint. Non includere un carattere &lt; perché tronca la descrizione visualizzata in Workspace.

**Espressione Cron:** Immetti un’espressione cron se l’e-mail deve essere pianificata utilizzando un’espressione cron.

**Conteggio ripetizioni:** Numero di volte in cui l’endpoint e-mail esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.

**Intervallo di ripetizione:** Frequenza di scansione utilizzata dal ricevitore per il controllo della posta in arrivo.

**Ritardo all&#39;avvio del processo:** Tempo di attesa per l&#39;analisi dopo l&#39;avvio della pianificazione.

**Dimensione batch:** Il numero di e-mail che il ricevitore elabora per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.

**Nome utente:** Un’impostazione obbligatoria, che è il nome utente utilizzato quando si richiama un servizio di destinazione da un’e-mail. Il valore predefinito è SuperAdmin.

**Nome di dominio:** Un’impostazione obbligatoria, che è il dominio dell’utente. Il valore predefinito è DefaultDom.

**Pattern di dominio:** Specifica i pattern di dominio delle e-mail in arrivo accettate dal provider. Ad esempio, se utilizzi adobe.com, viene elaborato solo l’e-mail da adobe.com; le e-mail provenienti da altri domini vengono ignorate.

**Pattern file:** Specifica i pattern di file allegato in ingresso accettati dal provider. Questo include i file che hanno estensioni specifiche (&amp;ast;.dat, &amp;ast;.xml), nomi specifici (dati) o espressioni composite nel nome e nell&#39;estensione (&amp;ast;.[dD][aA]&quot;port&quot;).

**Destinatari del processo riuscito:** Indirizzo e-mail a cui vengono inviati i messaggi per indicare l’esito positivo dei processi. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di lavoro riuscito. Se digiti il mittente, i risultati delle e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica altri destinatari con indirizzi e-mail, separati da virgole (,).

Per disattivare questa impostazione, lasciare vuota l&#39;impostazione. In alcuni casi, desideri attivare un processo e non desideri una notifica e-mail del risultato.

**Destinatari del processo non riuscito:** Indirizzo e-mail a cui vengono inviati i messaggi per indicare processi non riusciti. Per impostazione predefinita, al mittente viene sempre inviato un messaggio di lavoro non riuscito. Se digiti il mittente, i risultati delle e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica altri destinatari con indirizzi e-mail, separati da virgole (,).

Per disattivare questa impostazione, lasciare vuota l&#39;impostazione. In alcuni casi, desideri attivare un processo e non desideri una notifica e-mail del risultato.

**Host casella in entrata:** Nome host della casella in entrata o indirizzo IP da analizzare dal provider di posta elettronica.

**Porta in entrata:** La porta utilizzata dal server e-mail. Il valore predefinito per POP3 è 110 e il valore predefinito per IMAP è 143. Se SSL è abilitato, il valore predefinito per POP3 è 995 e il valore predefinito per IMAP è 993.

**Protocollo casella in entrata:** Il protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della casella in entrata. I valori sono IMAP o POP3. Il server di posta elettronica host della casella in entrata deve supportare questi protocolli.

**Timeout casella in entrata:** Timeout, in secondi, del provider di posta elettronica per attendere le risposte della casella in entrata.

**Utente casella in entrata:** Nome utente necessario per accedere all’account e-mail. A seconda del server e-mail e della configurazione, questo valore può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.

**Password casella in entrata:** Password per l’utente della inbox.

**SSL POP3/IMAP abilitato:** Seleziona questa impostazione per forzare il provider di posta elettronica a utilizzare SSL per la scansione della casella in entrata. Assicurati che il server di posta elettronica supporti SSL.

**Host SMTP:** Il nome host del server di posta elettronica utilizzato dal provider di posta elettronica per inviare i risultati e i messaggi di errore.

**Porta SMTP:** Il valore predefinito per la porta SMTP è 25.

**Utente SMTP:** L’account utente del provider di posta elettronica da utilizzare quando invia notifiche e-mail di risultati ed errori.

**Password SMTP:** Password dell&#39;account SMTP. Alcuni server di posta non richiedono una password SMTP.

**Invia da:** L’indirizzo e-mail (ad esempio, user@company.com) utilizzato per inviare notifiche e-mail di risultati ed errori. Se non si specifica un valore Invia da, il server e-mail tenta di determinare l’indirizzo e-mail combinando il valore specificato nell’impostazione Utente SMTP con un dominio predefinito configurato sul server e-mail. Se il server di posta elettronica non dispone di un dominio predefinito e non si specifica un valore per Invia da, potrebbero verificarsi errori. Per garantire che l’indirizzo del messaggio e-mail sia corretto, specifica un valore per l’impostazione Invia da.

**SSL SMTP abilitato:** Seleziona questa impostazione per forzare il provider di posta elettronica a utilizzare SSL per la scansione della casella in entrata. Assicurati che il server di posta elettronica supporti SSL.

**Cartella inviata via e-mail non riuscita:** Specifica una directory in cui memorizzare i risultati se il server di posta SMTP non è operativo.

**asincrono:** Se è impostato su sincrono, vengono elaborati tutti i documenti di input e viene restituita una sola risposta. Quando è impostato su asincrono, viene inviata una risposta per ogni documento elaborato.

Ad esempio, viene creato un endpoint e-mail per un servizio che prende un singolo documento Word e lo restituisce come file PDF. È possibile inviare un messaggio e-mail alla casella in entrata dell’endpoint contenente più (3) documenti Word. Quando vengono elaborati tutti e tre i documenti, se l’endpoint è configurato come sincrono, viene inviata un’e-mail di risposta singola con tutti e tre i documenti allegati. Se l’endpoint è asincrono, viene inviato un messaggio e-mail di risposta dopo la conversione in PDF di ogni documento Word. Il risultato sono tre e-mail, ciascuna con un singolo allegato PDF.

Il valore predefinito è asincrono.

**Includi il corpo dell’e-mail originale come allegato:** Per impostazione predefinita, quando si invia un’e-mail al server dei moduli, il testo originale del messaggio viene incluso nel corpo del messaggio. Per includere invece il testo come allegato, selezionare questa opzione.

**Utilizza l’oggetto originale per le e-mail dei risultati:** Per impostazione predefinita, il server Forms utilizza come oggetto i valori specificati nelle impostazioni Soggetto e-mail con esito positivo e Oggetto e-mail con errore durante l’invio dei messaggi e-mail con risultati. Per utilizzare invece la stessa riga dell’oggetto dell’e-mail originale inviata al server, seleziona questa opzione.

**Oggetto e-mail di successo:** Dopo aver inviato un’e-mail a un endpoint e-mail per avviare o continuare un processo, riceverai un messaggio e-mail di ritorno dal server dei moduli di AEM. Se l’e-mail ha esito positivo, riceverai un messaggio e-mail di successo. Se l’e-mail non riesce, riceverai un messaggio e-mail di errore per informarne il motivo dell’errore. Questa impostazione consente di specificare l’oggetto dei messaggi e-mail di successo inviati per l’endpoint.

**Corpo e-mail di successo:** Consente di specificare il corpo dei messaggi e-mail con esito positivo inviati per l’endpoint.

**Prefisso oggetto e-mail errore:** Consente di specificare il testo utilizzato all’inizio della riga dell’oggetto dei messaggi e-mail di errore inviati per l’endpoint.

**Oggetto e-mail errore:** Consente di specificare l’oggetto dei messaggi e-mail di errore inviati per l’endpoint. Questo testo viene visualizzato dopo il prefisso Oggetto e-mail di errore.

**Corpo e-mail errore:** Consente di specificare la prima riga nel testo del corpo dei messaggi e-mail di errore inviati per l’endpoint.

**Informazioni di riepilogo e-mail:** Ogni messaggio di errore o di successo include una sezione contenente il testo e-mail originale inviato al server dei moduli. Questa impostazione specifica il testo visualizzato sopra la sezione.

**Convalida la casella in entrata prima di creare/aggiornare questo endpoint:** Quando questa opzione è selezionata, il server dei moduli controlla se le impostazioni SMTP/POP3 sono corrette prima di creare l’endpoint. Quando fai clic su Aggiungi, viene visualizzato un messaggio che indica se l’account della casella in entrata è valido. Se questa opzione non è selezionata, il server dei moduli AEM crea l’endpoint senza convalidare la casella in entrata.

**Nome operazione:** Questa impostazione è obbligatoria. Elenco di operazioni che possono essere assegnate all’endpoint e-mail. L’operazione selezionata determina quali campi vengono visualizzati nelle sezioni Mappature parametri di input e Mappature parametri di output .

**Mappature dei parametri di input:** Utilizzato per configurare l&#39;input necessario per elaborare il servizio e l&#39;operazione. I due tipi di input sono letterali e variabili:

**Letterale:** L’e-mail utilizza il valore immesso nel campo così come viene visualizzato.

**Variabile:** Puoi mappare una stringa dall’oggetto dell’e-mail, dal corpo, dall’intestazione o dall’indirizzo e-mail del mittente. A questo scopo, utilizza una delle seguenti parole chiave: %SUBJECT%, %BODY%, %HEADER% o %SENDER%. Ad esempio, se utilizzi %SUBJECT%, il contenuto dell’oggetto dell’e-mail viene utilizzato come parametro di input. Per raccogliere gli allegati, immettere un pattern di file che l’endpoint e-mail può utilizzare per selezionare i documenti allegati. Ad esempio, l&#39;immissione di &amp;ast;.pdf seleziona qualsiasi documento allegato con estensione .pdf. Immissione &amp;ast; seleziona qualsiasi documento allegato. Se si immette example.pdf, verrà selezionato qualsiasi documento allegato denominato example.pdf.

**Mappature dei parametri di output:** Utilizzato per configurare l&#39;output del servizio e l&#39;operazione. I seguenti caratteri nei valori di mappatura dei parametri di output vengono espansi nel nome file allegato:

**%F** Rappresenta il nome del file di origine (senza un&#39;estensione ).

**%E** Rappresenta l&#39;estensione del file di origine.

Qualsiasi occorrenza della barra rovesciata (\) viene sostituita con %%.

***nota **: Se il messaggio di richiesta del servizio include più allegati di file, non è possibile utilizzare i parametri %F e %E per la proprietà Mapping parametri di output dell&#39;endpoint. Se la risposta dei servizi restituisce più allegati di file, non è possibile specificare lo stesso nome di file per più allegati. Se non si seguono queste raccomandazioni, il servizio richiamato crea i nomi dei file restituiti e i nomi non sono prevedibili.*

Sono disponibili i seguenti valori:

**Oggetto singolo:** Il provider di posta elettronica non ha la destinazione della cartella di origine; i risultati vengono restituiti come allegati. Il pattern è Result/%F.ps e restituisce Result%%sourcefilename.ps come allegato del nome file.

**Elenco:** Il pattern è Risultato/%F/ e restituisce Risultato%%sourcefilename%%file1 come allegato del nome file.

**Mappa:** Il pattern è Risultato/%F/ e la destinazione di origine è Risultato%%sourcefilename%%file1 e Risultato%%sourcefilename%%file2. Se la mappa contiene più di un oggetto e il pattern è Risultato/%F.ps, gli allegati del file di risposta sono Risultato%%sourcefilename1.ps (output 1) e Risultato%%sourcefilename2.ps (output 2).

## Creare un endpoint e-mail per il servizio Attività completa {#create-an-email-endpoint-for-the-complete-task-service}

Affinché il flusso di lavoro dei moduli possa ricevere e gestire i messaggi e-mail in arrivo dagli utenti, è necessario creare un endpoint e-mail per il servizio Attività completa.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione servizi fare clic sul servizio Attività completa.
1. Nella scheda Endpoint selezionare E-mail dall’elenco a discesa e fare clic su Aggiungi.
1. Nella casella Host casella in entrata digitare il nome host o l&#39;indirizzo IP del server di posta.
1. Nella casella Utente casella in entrata digitare il nome utente necessario per accedere all’account e-mail creato per gestire gli invii del modulo. A seconda del server e-mail e della configurazione, questo nome può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.
1. Nella casella Password casella in entrata digitare la password per l&#39;utente in entrata.
1. Nella casella Host SMTP digitare il nome host o l&#39;indirizzo IP del server di posta da cui il provider di posta elettronica invia i risultati e i messaggi di errore.
1. Nella casella Utente SMTP, digitare l’account utente da utilizzare per il provider di posta elettronica quando invia un’e-mail per individuare risultati ed errori. Questo account utente può essere lo stesso valore utilizzato per Posta in arrivo utente.
1. Nella casella Password SMTP, digitare la password per l&#39;account SMTP.
1. Nell&#39;elenco Nome operazione selezionare invoke.
1. Nell’elenco attachmentMap , seleziona Variabile e digita `*.*` nella casella adiacente. Questo invia tutti gli allegati dei messaggi di posta in entrata a una variabile di mappa per il processo Attività completa.
1. Nell&#39;elenco mailBody, selezionare variabile e digitare `%BODY%` nella casella adiacente.
1. Nell&#39;elenco mailFrom, selezionare Variabile e digitare `%SENDER%` nella casella adiacente. In questo modo l’indirizzo del mittente viene mappato sui dati del processo Attività completa.
1. Nella casella dei risultati, digita `results`. In questo modo l&#39;attività Completa o il processo di avvio restituirà una stringa di risultato.
1. Fate clic su Aggiungi.
