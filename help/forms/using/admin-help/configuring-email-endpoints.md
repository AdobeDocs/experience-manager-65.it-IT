---
title: Configurazione degli endpoint e-mail
description: Scopri come configurare gli endpoint e-mail. Gli endpoint e-mail consentono di richiamare un servizio inviando uno o più documenti a un account e-mail specificato.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
exl-id: 33583a12-4f20-4146-baa4-c9854e454bbf
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3775'
ht-degree: 0%

---

# Configurazione degli endpoint e-mail {#configuring-email-endpoints}

Gli endpoint e-mail consentono agli utenti di richiamare un servizio inviando uno o più documenti (come allegati e-mail) a un account e-mail specificato. La posta in arrivo funge da punto di raccolta per gli allegati. Il servizio controlla la casella in entrata ed elabora gli allegati. I risultati della conversione vengono inoltrati all&#39;utente definito nell&#39;endpoint.

Per un endpoint e-mail, gli utenti autorizzati possono richiamare un processo inviando i file all’account appropriato. I risultati verranno restituiti all’utente che ha inviato il messaggio (per impostazione predefinita) o all’utente definito nelle impostazioni dell’endpoint.

Prima di configurare un endpoint e-mail, crea un account e-mail POP3 o IMAP da utilizzare per l’endpoint. Imposta un conto separato per ogni tipo di conversione. Ad esempio, un account può essere configurato per generare documenti PDF standard da allegati di file in arrivo e un altro account può essere configurato per generare documenti PDF protetti.

>[!NOTE]
>
>Ogni indirizzo e-mail deve essere mappato su un solo endpoint e-mail. Non puoi configurare più endpoint e-mail su un singolo indirizzo e-mail, anche se gli endpoint e-mail aggiuntivi sono disabilitati.

Tutti gli endpoint e-mail sono configurati con un nome utente e una password autorizzati per la casella in entrata e-mail, necessari quando si richiama il servizio. L’account e-mail è protetto dal sistema del server di posta in cui è configurato.

Se gli utenti inviano documenti con caratteri di lingua dell&#39;Europa occidentale nei nomi dei percorsi di file e conversione, devono utilizzare un&#39;applicazione e-mail che supporti i tipi di codifica richiesti (Latin1 [ISO-8859-1], Europa occidentale [Windows]o UTF-8). Per ulteriori informazioni, vedere *Installazione e distribuzione di moduli AEM* per il server applicazioni.

Prima di configurare un endpoint e-mail, configura il servizio e-mail. (vedere [Configurare le impostazioni predefinite dell’endpoint e-mail](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) I parametri di configurazione del servizio e-mail hanno due scopi:

* Per configurare gli attributi comuni a tutti gli endpoint e-mail
* Per fornire valori predefiniti per tutti gli endpoint e-mail

## Configurare SSL per un endpoint e-mail {#configure-ssl-for-an-email-endpoint}

È possibile configurare POP3, IMAP o SMTP per utilizzare Secure Sockets Layer (SSL) per un endpoint e-mail.

1. Sul server e-mail, abilita SSL per POP3, IMAP o SMTP in base alla documentazione del produttore.
1. Esporta un certificato client dal server e-mail.
1. Utilizzare il programma keytool per importare il file di certificato client nell&#39;archivio certificati Java Virtual Machine (JVM) del server applicazioni. La procedura per questo passaggio dipende dai percorsi di installazione JVM e client.

   Se ad esempio si utilizza un&#39;installazione predefinita di Oracle WebLogic Server con JDK 1.5.0 in Microsoft Windows Server® 2003, digitare il testo seguente al prompt dei comandi:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Quando richiesto, immettere la password (per Java, la password predefinita è `changeit`). Verrà visualizzato un messaggio che informa che il certificato è stato importato correttamente.
1. Utilizza la console di amministrazione per aggiungere l’endpoint e-mail al servizio.
1. Crea l’endpoint e-mail nella console di amministrazione. Durante la configurazione delle impostazioni dell&#39;endpoint, selezionare POP3/IMAP SSL Enabled per i messaggi in arrivo e SMTP SSL Enabled per i messaggi in uscita e modificare di conseguenza le proprietà della porta.

>[!NOTE]
>
>Suggerimento: se si verificano problemi durante l&#39;utilizzo di SSL, utilizzare un client di posta elettronica come Microsoft Outlook per verificare se è possibile accedere al server di posta elettronica utilizzando SSL. Se il client e-mail non è in grado di accedere al server e-mail, il problema è relativo alla configurazione del certificato o del server e-mail.

## Configurare le impostazioni predefinite dell’endpoint e-mail {#configure-default-email-endpoint-settings}

È possibile utilizzare la pagina Gestione del servizio per configurare attributi comuni a tutti gli endpoint e-mail e per fornire valori predefiniti per tutti gli endpoint e-mail.

Affinché il flusso di lavoro dei moduli riceva e gestisca i messaggi e-mail in arrivo dagli utenti, è necessario creare un endpoint e-mail per il servizio Completa attività. Questo endpoint e-mail richiede impostazioni aggiuntive, come descritto in [Creare un endpoint e-mail per il servizio Attività completa](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Modificare i valori predefiniti per gli endpoint e-mail {#change-the-default-values-for-email-endpoints}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizi, fai clic su E-mail: 1.0 (l’ID componente è com.adobe.idp.dsc.provider.service.email.Email).
1. Nella scheda Configurazione specifica le impostazioni predefinite dell’endpoint e-mail, quindi fai clic su Salva.

### Impostazioni endpoint e-mail predefinito {#default-email-endpoint-settings}

**Espressione Cron:** Espressione cron utilizzata da quartz per pianificare il polling della directory di input.

**Intervallo ripetizione:** Il numero di volte in cui il polling della directory viene ripetuto. L’intervallo di ripetizione predefinito è in secondi se questo valore non è specificato nella configurazione dell’endpoint. Il valore predefinito è 10. Questo valore non può essere inferiore a 10.

**Conteggio ripetizioni:** Il numero di volte in cui viene eseguito il polling della directory di input. Il conteggio di ripetizioni predefinito da utilizzare se questo valore non è specificato nella configurazione dell’endpoint. Il valore -1 indica l&#39;analisi indefinita della directory. Il valore predefinito è -1.

**Ritardo all&#39;avvio del processo:** Valore predefinito, in secondi, del ritardo prima che il processo inizi la scansione dell’endpoint. Il valore predefinito è 0.

**Dimensione batch:** Il numero di e-mail elaborate dal ricevitore per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.

**Asincrono:** Identifica il tipo di chiamata come asincrona o sincrona. I processi transitori e sincroni possono essere richiamati solo in modo sincrono. Il valore predefinito è asincrono.

**Pattern dominio:** Schema del nome di dominio utilizzato per filtrare le e-mail in arrivo. Ad esempio, se utilizzi adobe.com, verranno elaborate solo le e-mail da adobe.com; le e-mail da altri domini verranno ignorate.

**Pattern file:** I modelli di file allegati in ingresso accettati dal provider. Ciò include i file con estensioni specifiche (&amp;ast;.dat, &amp;ast;.xml), nomi specifici (dati) ed espressioni composite nel nome e nell&#39;estensione (.[dD][aA]&#39;porta&#39;). Il valore predefinito è &amp;ast;.&amp;ast;.

**Destinatari processo riusciti:** Uno o più indirizzi e-mail utilizzati per inviare e-mail per indicare processi riusciti. Per impostazione predefinita, un messaggio di processo riuscito viene sempre inviato al mittente del processo iniziale. Sono supportati fino a 100 destinatari. Per disattivare questa impostazione, lasciare vuoto il campo.

**Destinatari processo non riuscito:** Uno o più indirizzi e-mail utilizzati per inviare e-mail per indicare i processi non riusciti. Per impostazione predefinita, un messaggio di processo non riuscito viene sempre inviato al mittente che ha inviato il processo iniziale. Sono supportati fino a 100 destinatari. Per disattivare questa impostazione, lasciare vuoto il campo.

**Host casella in entrata:** Il nome host della casella in entrata o l’indirizzo IP che il provider e-mail deve analizzare.

**Porta casella in entrata:** Numero della porta della casella in entrata da analizzare per il provider e-mail. Se il valore è 0, viene utilizzata la porta IMAP o POP3 predefinita.

**Protocollo casella in entrata:** Il protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della casella in entrata. Le opzioni disponibili sono IMAP o POP3. Il server di posta host della casella in entrata deve supportare questi protocolli.

**Timeout casella in entrata:** Specifica il tempo di attesa dell&#39;endpoint prima dell&#39;annullamento quando si tenta di connettersi alla casella in entrata. Se una connessione non viene acquisita prima del raggiungimento del valore di timeout, la casella in entrata non verrà sottoposta a polling.

**Utente casella in entrata:** Il nome utente necessario per accedere all’account e-mail. A seconda del server e della configurazione di e-mail, questo nome può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.

**Password casella in entrata:** Password per l&#39;utente della casella in entrata.

**SSL POP3/IMAP abilitato:** Se questa opzione è selezionata, abilita SSL.

**Host SMTP:** Nome host del server di posta utilizzato dal provider di posta elettronica per inviare risultati e messaggi di errore. Ad esempio, mail.example.com.

**Porta SMTP:** Porta utilizzata per la connessione al server di posta. Il valore predefinito è 25.

**Utente SMTP:** Account utente del provider di posta elettronica da utilizzare per l&#39;invio di messaggi di posta elettronica per risultati ed errori.

**Password SMTP:** La password per l&#39;account SMTP. Alcuni server di posta non richiedono una password SMTP.

**Invia da:** L’indirizzo e-mail (ad esempio, user@company.com) utilizzato per inviare notifiche e-mail di risultati ed errori. Se non si specifica un valore Invia da, il server di posta elettronica tenta di determinare l&#39;indirizzo di posta elettronica combinando il valore specificato nell&#39;impostazione Utente SMTP con un dominio predefinito configurato sul server di posta elettronica. Se il server di posta elettronica non dispone di un dominio predefinito e non si specifica un valore per Invia da, potrebbero verificarsi degli errori. Per verificare che i messaggi e-mail abbiano l’indirizzo di origine corretto, specifica un valore per l’impostazione Invia da.

**SSL SMTP abilitato:** Se questa opzione è selezionata, abilita SSL su SMTP.

**Includi Il Corpo Dell’E-Mail Originale Come Allegato:** Per impostazione predefinita, quando si invia un messaggio di posta elettronica al server dei moduli, il testo originale del messaggio viene incluso nel corpo del messaggio. Per includere il testo come allegato, selezionare questa opzione.

**Utilizza La Riga Oggetto Originale Per Le E-Mail Dei Risultati:** Per impostazione predefinita, il server Forms utilizza i valori specificati nelle impostazioni Oggetto e-mail riuscito e Oggetto e-mail errore come riga dell’oggetto quando si inviano i messaggi e-mail dei risultati. Selezionare questa opzione per utilizzare invece la stessa riga dell&#39;oggetto dell&#39;e-mail originale inviata al server.

**Oggetto e-mail di successo:** Dopo aver inviato un messaggio e-mail a un endpoint e-mail per avviare o continuare un processo, si riceve un messaggio e-mail di ritorno dal server dei moduli AEM. Se l’e-mail ha esito positivo, riceverai un’e-mail di successo. Se l’e-mail non riesce, riceverai un’e-mail di errore con l’indicazione del motivo dell’errore. Questa impostazione consente di specificare l’oggetto dei messaggi e-mail di successo inviati per questo endpoint.

**Corpo e-mail di successo:** Consente di specificare il corpo del testo dei messaggi e-mail di successo inviati per questo endpoint.

**Errore Prefisso oggetto e-mail:** Consente di specificare il testo utilizzato all&#39;inizio della riga dell&#39;oggetto dei messaggi e-mail di errore inviati per questo endpoint.

**Oggetto e-mail errore:** Consente di specificare l’oggetto dei messaggi e-mail di errore inviati per questo endpoint. Questo testo viene visualizzato dopo il prefisso dell’oggetto e-mail di errore.

**Corpo e-mail errore:** Consente di specificare la prima riga nel corpo del testo dei messaggi e-mail di errore inviati per questo endpoint.

**Informazioni di riepilogo e-mail:** Ogni messaggio di operazione riuscita o non riuscita include una sezione contenente il testo dell&#39;e-mail originale inviato al server dei moduli. Questa impostazione specifica il testo visualizzato sopra la sezione.

**Convalida Casella In Entrata Prima Di Creare/Aggiornare Questo Endpoint:** Quando questa opzione è selezionata, il server Forms controlla se le impostazioni SMTP/POP3 sono corrette prima di creare l’endpoint. Quando fai clic su Aggiungi, viene visualizzato un messaggio che indica se l’account della casella in entrata è valido. Se questa opzione non è selezionata, il server AEM forms crea l&#39;endpoint senza convalidare la casella in entrata.

**Codifica set di caratteri:** Formato di codifica da utilizzare per il messaggio e-mail. Il valore predefinito è UTF-8, che verrà utilizzato dalla maggior parte degli utenti al di fuori del Giappone. Gli utenti in un ambiente giapponese possono scegliere ISO2022-JP.

**Cartella e-mail inviata non riuscita:** Specifica una directory in cui archiviare i risultati se il server di posta SMTP non è operativo.

## Impostazioni endpoint e-mail {#email-endpoint-settings}

Utilizza le seguenti impostazioni per configurare un endpoint e-mail.

**Nome:** Un’impostazione obbligatoria che identifica l’endpoint. Non includere un carattere &lt; perché tronca il nome visualizzato in Workspace. Se immetti un URL come nome dell’endpoint, accertati che sia conforme alle regole di sintassi specificate in RFC1738.

**Descrizione:** Descrizione dell&#39;endpoint. Non includere un carattere &lt; perché tronca la descrizione visualizzata in Workspace.

**Espressione Cron:** Inserisci un’espressione cron se l’e-mail deve essere pianificata utilizzando un’espressione cron.

**Conteggio ripetizioni:** Numero di volte in cui l’endpoint e-mail esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.

**Intervallo ripetizione:** Velocità di scansione utilizzata dal ricevitore per il controllo della posta in arrivo.

**Ritardo all&#39;avvio del processo:** Tempo di attesa per la scansione dopo l&#39;avvio della pianificazione.

**Dimensione batch:** Il numero di e-mail elaborate dal ricevitore per scansione per ottenere prestazioni ottimali. Il valore -1 indica tutte le e-mail. Il valore predefinito è 2.

**Nome utente:** Un’impostazione obbligatoria, che è il nome utente utilizzato quando si richiama un servizio target da e-mail. Il valore predefinito è SuperAdmin.

**Nome dominio:** Un’impostazione obbligatoria, che è il dominio dell’utente. Il valore predefinito è DefaultDom.

**Pattern dominio:** Specifica i pattern di dominio dei messaggi e-mail in arrivo accettati dal provider. Ad esempio, se utilizzi adobe.com, vengono elaborate solo le e-mail da adobe.com; le e-mail da altri domini vengono ignorate.

**Pattern file:** Specifica i modelli di file allegati in ingresso accettati dal provider. Ciò include i file con estensioni specifiche (&amp;ast;.dat, &amp;ast;.xml), nomi specifici (dati) o espressioni composite nel nome e nell&#39;estensione (&amp;ast;.[dD][aA]&#39;porta&#39;).

**Destinatari processo riusciti:** Un indirizzo e-mail a cui vengono inviati i messaggi per indicare i processi riusciti. Per impostazione predefinita, un messaggio di processo riuscito viene sempre inviato al mittente. Se si digita mittente, i risultati e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica destinatari aggiuntivi con indirizzi e-mail, separati da virgole (,).

Per disattivare questa impostazione, lasciare vuota l&#39;impostazione. In alcuni casi, si desidera attivare un processo e non inviare una notifica e-mail del risultato.

**Destinatari processo non riuscito:** Un indirizzo e-mail a cui vengono inviati i messaggi per indicare i processi non riusciti. Per impostazione predefinita, un messaggio di processo non riuscito viene sempre inviato al mittente. Se si digita mittente, i risultati e-mail vengono inviati al mittente. Sono supportati fino a 100 destinatari. Specifica destinatari aggiuntivi con indirizzi e-mail, separati da virgole (,).

Per disattivare questa impostazione, lasciare vuota l&#39;impostazione. In alcuni casi, si desidera attivare un processo e non inviare una notifica e-mail del risultato.

**Host casella in entrata:** Il nome host della casella in entrata o l’indirizzo IP che il provider e-mail deve analizzare.

**Porta casella in entrata:** La porta utilizzata dal server e-mail. Il valore predefinito per POP3 è 110 e quello per IMAP è 143. Se SSL è abilitato, il valore predefinito per POP3 è 995 e quello per IMAP è 993.

**Protocollo casella in entrata:** Il protocollo e-mail per l’endpoint e-mail da utilizzare per la scansione della casella in entrata. I valori sono IMAP o POP3. Il server di posta host della casella in entrata deve supportare questi protocolli.

**Timeout casella in entrata:** Timeout, in secondi, dell’attesa delle risposte della casella in entrata da parte del provider e-mail.

**Utente casella in entrata:** Il nome utente necessario per accedere all’account e-mail. A seconda del server e della configurazione di e-mail, questo valore può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.

**Password casella in entrata:** Password per l&#39;utente della casella in entrata.

**SSL POP3/IMAP abilitato:** Seleziona questa impostazione per forzare il provider di posta elettronica a utilizzare SSL per la scansione della casella in entrata. Assicurati che il server di posta supporti SSL.

**Host SMTP:** Il nome host del server di posta utilizzato dal provider di posta elettronica per inviare risultati e messaggi di errore.

**Porta SMTP:** Il valore predefinito per la porta SMTP è 25.

**Utente SMTP:** L’account utente che il provider di posta elettronica deve utilizzare per inviare notifiche e-mail di risultati ed errori.

**Password SMTP:** La password per l&#39;account SMTP. Alcuni server di posta non richiedono una password SMTP.

**Invia da:** L’indirizzo e-mail (ad esempio, user@company.com) utilizzato per inviare notifiche e-mail di risultati ed errori. Se non si specifica un valore Invia da, il server di posta elettronica tenta di determinare l&#39;indirizzo di posta elettronica combinando il valore specificato nell&#39;impostazione Utente SMTP con un dominio predefinito configurato sul server di posta elettronica. Se il server di posta elettronica non dispone di un dominio predefinito e non si specifica un valore per Invia da, potrebbero verificarsi degli errori. Per verificare che i messaggi e-mail abbiano l’indirizzo di origine corretto, specifica un valore per l’impostazione Invia da.

**SSL SMTP abilitato:** Seleziona questa impostazione per forzare il provider di posta elettronica a utilizzare SSL per la scansione della casella in entrata. Assicurati che il server di posta supporti SSL.

**Cartella e-mail inviata non riuscita:** Specifica una directory in cui archiviare i risultati se il server di posta SMTP non è operativo.

**asincrono:** Quando è impostato su synchronous, tutti i documenti di input vengono elaborati e viene restituita una singola risposta. Quando è impostato su asincrono, viene inviata una risposta per ogni documento elaborato.

Ad esempio, viene creato un endpoint e-mail per un servizio che accetta un singolo documento di Word e restituisce tale documento come file PDF. È possibile inviare un’e-mail alla casella in entrata dell’endpoint contenente più (3) documenti Word. Quando vengono elaborati tutti e tre i documenti, se l’endpoint è configurato come sincrono, viene inviata un’unica e-mail di risposta con tutti e tre i documenti allegati. Se l’endpoint è asincrono, viene inviata un’e-mail di risposta dopo che ogni documento di Word è stato convertito in PDF. Il risultato sono tre e-mail, ciascuna con un singolo allegato PDF.

Il valore predefinito è asincrono.

**Includi il corpo dell’e-mail originale come allegato:** Per impostazione predefinita, quando si invia un messaggio di posta elettronica al server dei moduli, il testo originale del messaggio viene incluso nel corpo del messaggio. Per includere il testo come allegato, selezionare questa opzione.

**Utilizza l’oggetto originale per le e-mail dei risultati:** Per impostazione predefinita, il server Forms utilizza i valori specificati nelle impostazioni Oggetto e-mail riuscito e Oggetto e-mail errore come riga dell’oggetto quando si inviano i messaggi e-mail dei risultati. Selezionare questa opzione per utilizzare invece la stessa riga dell&#39;oggetto dell&#39;e-mail originale inviata al server.

**Oggetto e-mail di successo:** Dopo aver inviato un messaggio e-mail a un endpoint e-mail per avviare o continuare un processo, si riceve un messaggio e-mail di ritorno dal server dei moduli AEM. Se l’e-mail ha esito positivo, riceverai un’e-mail di successo. Se l’e-mail non riesce, riceverai un’e-mail di errore con l’indicazione del motivo dell’errore. Questa impostazione consente di specificare l’oggetto dei messaggi e-mail di successo inviati per questo endpoint.

**Corpo e-mail di successo:** Consente di specificare il corpo del testo dei messaggi e-mail di successo inviati per questo endpoint.

**Errore Prefisso oggetto e-mail:** Consente di specificare il testo utilizzato all&#39;inizio della riga dell&#39;oggetto dei messaggi e-mail di errore inviati per questo endpoint.

**Oggetto e-mail errore:** Consente di specificare l’oggetto dei messaggi e-mail di errore inviati per questo endpoint. Questo testo viene visualizzato dopo il prefisso dell’oggetto e-mail di errore.

**Corpo e-mail errore:** Consente di specificare la prima riga nel corpo del testo dei messaggi e-mail di errore inviati per questo endpoint.

**Informazioni di riepilogo e-mail:** Ogni messaggio di operazione riuscita o non riuscita include una sezione contenente il testo dell&#39;e-mail originale inviato al server dei moduli. Questa impostazione specifica il testo visualizzato sopra la sezione.

**Convalida casella in entrata prima di creare/aggiornare questo endpoint:** Quando questa opzione è selezionata, il server Forms controlla se le impostazioni SMTP/POP3 sono corrette prima di creare l’endpoint. Quando fai clic su Aggiungi, viene visualizzato un messaggio che indica se l’account della casella in entrata è valido. Se questa opzione non è selezionata, il server AEM forms crea l&#39;endpoint senza convalidare la casella in entrata.

**Nome operazione:** Questa impostazione è obbligatoria. Elenco di operazioni che possono essere assegnate all’endpoint e-mail. L&#39;operazione selezionata determina i campi da visualizzare nelle sezioni Mapping parametri di input e Mapping parametri di output.

**Mappature parametri di input:** Utilizzato per configurare l’input necessario per elaborare il servizio e l’operazione. I due tipi di input sono letterali e variabili:

**Valore letterale:** L’e-mail utilizza il valore immesso nel campo così come viene visualizzato.

**Variabile:** Puoi mappare una stringa dall’oggetto dell’e-mail, dal corpo, dall’intestazione o dall’indirizzo e-mail del mittente. A tale scopo, utilizzare una delle seguenti parole chiave: %SUBJECT%, %BODY%, %HEADER% o %SENDER%. Se ad esempio si utilizza %SUBJECT%, il contenuto dell&#39;oggetto dell&#39;e-mail verrà utilizzato come parametro di input. Per prelevare gli allegati, immettere un modello di file che l&#39;endpoint e-mail può utilizzare per selezionare i documenti allegati. Se ad esempio si immette &amp;ast;.pdf, verranno selezionati tutti i documenti allegati con estensione pdf. Se si immette &amp;ast;, viene selezionato qualsiasi documento allegato. L&#39;immissione di example.pdf consente di selezionare qualsiasi documento allegato denominato example.pdf.

**Mappature parametri di output:** Utilizzato per configurare l’output del servizio e dell’operazione. I seguenti caratteri nei valori di mappatura dei parametri di output vengono espansi nel nome file allegato:

**%F** Rappresenta il nome del file di origine (senza estensione).

**%E** Rappresenta l’estensione del file sorgente.

Qualsiasi occorrenza della barra rovesciata (\) viene sostituita con %%.

***nota **: se il messaggio di richiesta del servizio include più file allegati, non è possibile utilizzare i parametri %F e %E per la proprietà Output Parameter Mappints dell&#39;endpoint. Se la risposta dei servizi restituisce più allegati, non è possibile specificare lo stesso nome per più allegati. Se non si seguono queste raccomandazioni, il servizio richiamato crea i nomi per i file restituiti e i nomi non sono prevedibili.*

Sono disponibili i seguenti valori:

**Oggetto singolo:** Il provider di posta elettronica non dispone della destinazione della cartella di origine. I risultati vengono restituiti come allegati. Il modello è Result/%F.ps e restituisce Result%%sourcefilename.ps come allegato del nome file.

**Elenco:** Il modello è Result/%F/ e restituisce Result%%sourcefilename%%file1 come allegato del nome file.

**Mappa:** Il modello è Result/%F/ e la destinazione di origine è Result%%sourcefilename%%file1 e Result%%sourcefilename%%file2. Se la mappa contiene più oggetti e il modello è Result/%F.ps, gli allegati del file di risposta sono Result%%sourcefilename1.ps (output 1) e Result%%sourcefilename2.ps (output 2).

## Creare un endpoint e-mail per il servizio Attività completa {#create-an-email-endpoint-for-the-complete-task-service}

Affinché il flusso di lavoro dei moduli riceva e gestisca i messaggi e-mail in arrivo dagli utenti, è necessario creare un endpoint e-mail per il servizio Completa attività.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fare clic sul servizio Completa attività.
1. Nella scheda Endpoint, seleziona E-mail dall’elenco a discesa, quindi fai clic su Aggiungi.
1. Nella casella Posta in arrivo host digitare il nome host o l&#39;indirizzo IP del server di posta.
1. Nella casella Utente casella in entrata digitare il nome utente necessario per accedere all&#39;account di posta elettronica creato per gestire l&#39;invio dei moduli. A seconda del server e della configurazione di e-mail, questo nome può essere solo la parte del nome utente dell’e-mail o l’indirizzo e-mail completo.
1. Nella casella Password casella in entrata digitare la password per l&#39;utente casella in entrata.
1. Nella casella Host SMTP digitare il nome host o l&#39;indirizzo IP del server di posta da cui il provider di posta elettronica invia risultati e messaggi di errore.
1. Nella casella Utente SMTP digitare l&#39;account utente che il provider di posta elettronica dovrà utilizzare per inviare l&#39;e-mail per i risultati e gli errori. Questo account utente può essere lo stesso valore utilizzato per l&#39;utente della casella in entrata.
1. Nella casella Password SMTP digitare la password per l&#39;account SMTP.
1. Nell&#39;elenco Nome operazione selezionare richiama.
1. Nell&#39;elenco attachmentMap, selezionare Variabile e digitare `*.*` nella casella adiacente. In questo modo tutti gli allegati dei messaggi di posta in arrivo vengono inviati a una variabile di mappa per il processo Completa attività.
1. Nell&#39;elenco mailBody, selezionare la variabile e digitare `%BODY%` nella casella adiacente.
1. Nell&#39;elenco mailFrom, selezionare Variabile e digitare `%SENDER%` nella casella adiacente. L&#39;indirizzo del mittente viene mappato sui dati del processo di completamento dell&#39;attività.
1. Nella casella dei risultati digitare `results`. In questo modo l&#39;attività completa o il processo di avvio restituirà una stringa di risultati.
1. Fai clic su Aggiungi.
