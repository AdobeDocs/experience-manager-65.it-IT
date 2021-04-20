---
title: Configurazione delle opzioni client e server
seo-title: Configurazione delle opzioni client e server
description: Scopri come configurare le varie opzioni client e server, ad esempio le impostazioni di configurazione del server, i ruoli di sicurezza dei documenti e il controllo degli eventi.
seo-description: Scopri come configurare le varie opzioni client e server, ad esempio le impostazioni di configurazione del server, i ruoli di sicurezza dei documenti e il controllo degli eventi.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '10275'
ht-degree: 0%

---


# Configurare il server di protezione dei documenti {#configure-the-document-security-server}

1. Nella console di amministrazione, fai clic su Servizi > sicurezza documento > Configurazione > Configurazione server.
1. Configura le impostazioni e fai clic su OK.

## Impostazioni di configurazione del server {#server-configuration-settings}

**URL di base:** l&#39;URL di protezione del documento di base, contenente il nome del server e la porta. Le informazioni aggiunte alla base creano gli URL di connessione. Ad esempio, /edc/Main.do viene aggiunto per accedere alle pagine web. Gli utenti rispondono anche agli inviti di registrazione degli utenti esterni tramite questo URL.

Se utilizzi IPv6, immetti l’URL di base come nome del computer o nome DNS. Se utilizzi un indirizzo IP numerico, Acrobat non riuscirà ad aprire i file protetti da criteri. Inoltre, utilizza l’URL protetto HTTP (HTTPS) per il tuo server.

>[!NOTE]
>
>L’URL di base è incorporato in file protetti da policy. Le applicazioni client utilizzano l&#39;URL di base per riconnettersi al server. I file protetti continueranno a contenere l’URL di base, anche se successivamente vengono modificati. Se modifichi l’URL di base, le informazioni di configurazione dovranno essere aggiornate per tutti i client che si connettono.

**Periodo di leasing offline predefinito:** il periodo di tempo predefinito per cui un utente può utilizzare un documento protetto offline. Questa impostazione determina il valore iniziale dell&#39;impostazione del periodo di lease offline automatica quando crei un criterio. (Vedere Creazione e modifica dei criteri.) Quando il periodo di leasing scade, il destinatario deve sincronizzare di nuovo il documento per continuare a utilizzarlo.

Per una discussione sul funzionamento del lease e della sincronizzazione offline, vedi [Primer sulla configurazione del lease e della sincronizzazione offline](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Periodo di sincronizzazione offline predefinito:** il tempo massimo di utilizzo offline di un documento da quando è inizialmente protetto.

**Timeout sessione client:** il periodo di tempo, in minuti, dopo il quale la sicurezza del documento viene disconnessa se un utente che ha effettuato l&#39;accesso tramite un&#39;applicazione client non interagisce con la sicurezza del documento.

**Consenti accesso utenti anonimi:** seleziona questa opzione per abilitare la possibilità di creare criteri condivisi e personali che consentano agli utenti anonimi di aprire documenti protetti da policy. (Gli utenti che non dispongono di account possono accedere al documento, ma non possono accedere alla protezione dei documenti o utilizzare altri documenti protetti da policy).

**Disattiva l&#39;accesso ai client della versione 7:** specifica se gli utenti possono utilizzare Acrobat o Reader 7.0 per connettersi al server. Quando questa opzione è selezionata, gli utenti devono utilizzare Acrobat o Reader 8.0 e versioni successive per completare le operazioni di protezione dei documenti sui documenti PDF. Se i criteri richiedono che Acrobat o Reader 8.0 e versioni successive vengano eseguiti in modalità certificata all&#39;apertura di documenti protetti da policy, è necessario disattivare l&#39;accesso ad Acrobat o al Reader 7. (Consultare Specificare le autorizzazioni del documento per utenti e gruppi.)

**Consenti accesso offline per** documentoSelezionare questa opzione per specificare l&#39;accesso offline per documento. Se questa impostazione è abilitata, l&#39;utente avrà accesso offline solo ai documenti che l&#39;utente ha aperto online almeno una volta.

**Consenti autenticazione password nome utente:** seleziona questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione nome utente/password quando si connettono al server.

**Consenti autenticazione Kerberos:** selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione Kerberos durante la connessione al server.

**Consenti autenticazione certificato client:** seleziona questa opzione per consentire alle applicazioni client di utilizzare l’autenticazione dei certificati durante la connessione al server.

**Consenti** autenticazione estesaSelezionare per abilitare l&#39;autenticazione estesa, quindi immettere l&#39;URL di destinazione per l&#39;autenticazione estesa.

Selezionando questa opzione le applicazioni client possono utilizzare l’autenticazione estesa. L’autenticazione estesa fornisce processi di autenticazione personalizzati e diverse opzioni di autenticazione configurate sul server dei moduli AEM. Ad esempio, ora gli utenti possono utilizzare l’autenticazione basata su SAML invece di AEM nome utente/password dei moduli, da Acrobat e Reader Client. Per impostazione predefinita, l&#39;URL di destinazione contiene *localhost* come nome del server. Sostituisci il nome del server con un nome host completo. Se l’autenticazione estesa non è ancora abilitata, il nome host nell’URL di destinazione viene popolato automaticamente dall’URL di base. Consulta [Aggiungi il provider di autenticazione esteso](configuring-client-server-options.md#add-the-extended-authentication-provider).

***nota **: L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.*

**Larghezza del controllo HTML preferita per l&#39;** autenticazione estesaSpecifica la larghezza della finestra di dialogo di autenticazione estesa che viene visualizzata in Acrobat per l&#39;immissione delle credenziali utente.

**Altezza di controllo HTML preferita per l&#39;** autenticazione estesaSpecifica l&#39;altezza della finestra di dialogo di autenticazione estesa che viene visualizzata in Acrobat per l&#39;immissione delle credenziali utente.

***nota **: I limiti di larghezza e altezza per questa finestra di dialogo sono i seguenti:*
Larghezza: Minimo = 400, massimo = 900

Altezza: Minimo = 450; massimo = 800

**Abilita memorizzazione in cache delle credenziali client:** seleziona questa opzione per consentire agli utenti di memorizzare in cache le proprie credenziali (nome utente e password). Quando le credenziali degli utenti vengono memorizzate nella cache, non devono immettere le credenziali ogni volta che aprono un documento o quando fanno clic sul pulsante Aggiorna nella pagina Gestisci criteri di sicurezza in Adobe Acrobat. È possibile specificare il numero di giorni prima che gli utenti debbano fornire nuovamente le proprie credenziali. Impostando il numero di giorni su 0, le credenziali possono essere memorizzate nella cache a tempo indeterminato.

## Configurazione di utenti e amministratori per la protezione dei documenti {#configuring-document-security-users-and-administrators}

### Assegnazione di ruoli di protezione dei documenti agli amministratori {#assigning-document-security-roles-to-administrators}

L’ambiente AEM forms contiene uno o più utenti amministratori con i privilegi appropriati per la creazione di utenti e gruppi. Se l’organizzazione utilizza la protezione dei documenti, è necessario assegnare ad almeno un amministratore il privilegio per gestire gli utenti invitati e locali.

Per accedere alla console di amministrazione, gli amministratori devono anche disporre del ruolo utente della console di amministrazione. (Consulta [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configurazione di utenti e gruppi visibili {#configuring-visible-users-and-groups}

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti dei criteri, un amministratore privilegiato o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati in Gestione utente) all&#39;elenco di utenti e gruppi visibili per ciascun set di criteri.

L&#39;elenco visibile di utenti e gruppi è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l&#39;utente finale può sfogliare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà utenti o gruppi da aggiungere al criterio. Può essere presente più di un coordinatore set di criteri per ogni set di criteri specificato.

1. Dopo aver installato e configurato l’ambiente dei moduli AEM con la protezione dei documenti, impostare tutti i domini appropriati in Gestione utente. <!-- Fix broken link (See Setting up and managing domains) -->

   ***nota **: È necessario creare i domini prima di creare qualsiasi criterio.*

1. Nella console di amministrazione, fai clic su Servizi > Gestione documenti > Criteri, quindi fai clic sulla scheda Set di criteri .
1. Seleziona Set di criteri globale, quindi fai clic sulla scheda Utenti e gruppi visibili .
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.
1. Passa a Servizi > Protezione documento > Configurazione > Criteri personali e fai clic sulla scheda Utenti e gruppi visibili .
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.

## Aggiungi il provider di autenticazione esteso {#add-the-extended-authentication-provider}

AEM forms offre una configurazione di esempio personalizzabile in base all’ambiente in uso. Esegui i seguenti passaggi:

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

1. Ottenere il file WAR di esempio distribuirlo. Vedere la guida all&#39;installazione appropriata per il server applicazioni.
1. Assicurati che il server dei moduli abbia un nome completo invece degli indirizzi IP come URL di base e che sia un URL HTTPS. Vedere [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).
1. Abilita l&#39;autenticazione estesa dalla pagina Configurazione server . Vedere [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).
1. Aggiungi gli URL di reindirizzamento SSO richiesti nel file di configurazione User Management. Consulta [Aggiungi URL di reindirizzamento SSO per l&#39;autenticazione estesa](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Aggiungi URL di reindirizzamento SSO per l&#39;autenticazione estesa {#add-sso-redirect-urls-for-extended-authentication}

Con l&#39;autenticazione estesa abilitata, gli utenti che aprono un documento protetto da policy in Acrobat XI o nel Reader XI ottengono una finestra di dialogo per l&#39;autenticazione. Questa finestra di dialogo carica la pagina HTML specificata come URL di destinazione per l’autenticazione estesa nelle impostazioni del server di protezione dei documenti. Vedere [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Esporta e salva il file di configurazione sul disco.
1. Apri il file in un editor e individua il nodo AllowedUrls .
1. Nel nodo `AllowedUrls`, aggiungi le seguenti righe: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Salvare il file e quindi importare il file aggiornato dalla pagina Configurazione manuale: Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.

## Configurazione della protezione offline {#configuring-offline-security}

la protezione dei documenti consente di utilizzare documenti protetti da policy offline senza connessione a Internet o di rete. Questa funzionalità richiede che il criterio consenta l&#39;accesso offline, come descritto in [Specificare le autorizzazioni del documento per utenti e gruppi](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Prima che un documento con tale criterio possa essere utilizzato offline, il destinatario deve aprire il documento online e abilitare l&#39;accesso offline facendo clic su Sì quando richiesto. Al destinatario può anche essere richiesto di autenticare la sua identità. Il destinatario può quindi utilizzare i documenti offline per la durata del periodo di lease offline specificato nel criterio.

Al termine del periodo di lease offline, il destinatario deve sincronizzarsi nuovamente con la sicurezza del documento aprendo un documento online o utilizzando un comando di menu Acrobat o Acrobat Reader DC extensions per eseguire la sincronizzazione. (Consulta la *Guida di Acrobat* o la *Guida delle estensioni Acrobat Reader DC* appropriata.)

Poiché i documenti che consentono l&#39;accesso offline richiedono la memorizzazione in cache del materiale chiave nel computer in cui i file vengono archiviati offline, il file può essere potenzialmente compromesso se un utente non autorizzato può ottenere il materiale chiave. Per compensare questa possibilità, vengono fornite opzioni di rollover programmate e manuali che è possibile configurare per impedire a una persona non autorizzata di utilizzare la chiave per accedere al documento.

### Imposta un periodo di leasing offline predefinito {#set-a-default-offline-lease-period}

I destinatari di documenti protetti da policy possono disconnettere i documenti per il numero di giorni specificato nel criterio. Dopo aver inizialmente sincronizzato il documento con la sicurezza del documento, il destinatario può utilizzarlo offline fino alla scadenza del periodo di lease offline. Quando il periodo di leasing scade, il destinatario deve portare il documento online ed effettuare l’accesso per eseguire la sincronizzazione con la sicurezza del documento per continuare a utilizzare il documento.

Puoi configurare un periodo di leasing offline predefinito. Il periodo di leasing può essere modificato da quello predefinito quando qualcuno crea o modifica un criterio.

1. Nella pagina di protezione del documento fare clic su Configurazione > Configurazione server.
1. Nella casella Periodo di leasing offline predefinito, digitare il numero di giorni per il periodo di leasing offline.
1. Fai clic su OK.

### Gestire i rollover delle chiavi {#manage-key-rollovers}

La sicurezza dei documenti utilizza algoritmi di crittografia e licenze per proteggere i documenti. Quando crittografa un documento, la protezione del documento genera e gestisce una chiave di decrittografia denominata *DocKey* che trasmette all&#39;applicazione client. Se il criterio di protezione di un documento consente l&#39;accesso offline, viene generata anche una chiave offline denominata *chiave principale* per ogni utente che ha accesso offline al documento.

>[!NOTE]
>
>Se una chiave principale non esiste, la sicurezza del documento ne genera una per proteggere un documento.

Per aprire un documento protetto da policy offline, il computer dell&#39;utente deve disporre della chiave principale appropriata. Il computer ottiene la chiave principale quando l&#39;utente si sincronizza con la sicurezza del documento (apre un documento protetto online). Se questa chiave principale viene compromessa, potrebbe essere compromesso anche qualsiasi documento a cui l&#39;utente ha accesso offline.

Un modo per ridurre la minaccia per i documenti offline è quello di evitare l&#39;accesso offline a documenti particolarmente sensibili. Un altro metodo consiste nel passare periodicamente il cursore sulle chiavi principali. Quando la protezione dei documenti esegue il rollover della chiave, tutte le chiavi esistenti non possono più accedere ai documenti protetti da policy. Ad esempio, se un autore ottiene una chiave principale da un computer portatile rubato, tale chiave non può essere utilizzata per accedere ai documenti protetti dopo il rollover. Se sospetti che una specifica chiave principale sia stata compromessa, puoi passare manualmente il cursore sulla chiave.

Tuttavia, è anche necessario tenere presente che un rollover di tasti interessa tutti i tasti principali, non solo uno. Riduce anche la scalabilità del sistema, perché i client devono memorizzare più chiavi per l&#39;accesso offline. La frequenza di rollover predefinita della chiave è 20 giorni. Si consiglia di non impostare questo valore su un valore inferiore a 14 giorni, poiché è possibile che agli utenti venga impedito di visualizzare documenti offline e che le prestazioni del sistema ne risentano.

Nell’esempio seguente, Key1 è la precedente delle due chiavi principali e Key2 è la più recente. Quando si fa clic sul pulsante Tasti rollover ora la prima volta, Key1 diventa non valido e viene generata una nuova chiave principale valida (Key3). Gli utenti otterranno Key3 quando si sincronizzano con la sicurezza dei documenti, in genere aprendo un documento protetto online. Tuttavia, gli utenti non sono costretti a eseguire la sincronizzazione con la sicurezza dei documenti fino a quando non raggiungono il periodo di lease offline massimo specificato in un criterio. Dopo il primo passaggio del tasto, gli utenti che rimangono offline possono comunque aprire i documenti offline, inclusi quelli protetti da Key3, fino a raggiungere il periodo massimo di lease offline. Quando si fa clic una seconda volta sul pulsante Rollover Keys Now, Key2 diventa non valido e viene creato Key4. Gli utenti che rimangono offline durante i due rollover chiave non possono aprire documenti protetti con Key3 o Key4 finché non si sincronizzano con la sicurezza dei documenti.

**Modificare la frequenza di rollover del tasto**

Per motivi di riservatezza, quando si utilizzano documenti offline, la sicurezza dei documenti fornisce un&#39;opzione di rollover automatico della chiave con un periodo di frequenza predefinito di 20 giorni. È possibile modificare la frequenza di rollover; tuttavia, evitare di impostare un valore inferiore a 14 giorni perché è possibile che agli utenti non sia consentito visualizzare documenti offline e che le prestazioni del sistema siano influenzate.

1. Nella pagina di protezione del documento fare clic su Configurazione > Gestione chiavi.
1. Nella casella Frequenza rollover chiave digitare il numero di giorni per il periodo di rollover.
1. Fai clic su OK.

**Esegui il roll over manuale delle chiavi principali**

Per mantenere la riservatezza dei documenti offline, puoi passare manualmente le chiavi principali. Potrebbe essere necessario passare manualmente su una chiave (ad esempio, se la chiave viene compromessa da un utente che la ottiene da un computer in cui è memorizzata nella cache per abilitare l&#39;accesso offline a un documento).

>[!NOTE]
>
>Evita di utilizzare frequentemente il rollover manuale perché fa sì che tutte le chiavi principali vengano sottoposte a roll over, non solo una, e può temporaneamente impedire agli utenti di visualizzare i nuovi documenti offline.

È necessario eseguire il rollback delle chiavi principali due volte prima che le chiavi esistenti nei computer client vengano invalidate. I computer client che hanno invalidato le chiavi principali devono eseguire nuovamente la sincronizzazione con il servizio di sicurezza dei documenti per acquisire le nuove chiavi principali.

1. Nella pagina di protezione del documento fare clic su Configurazione > Gestione chiavi.
1. Fare clic su Tasti rollover e quindi su OK.
1. Attendi circa 10 minuti. Nel registro server viene visualizzato il seguente messaggio di log: `Done RightsManagement key rollover for`*N* `principals`. Dove *N* è il numero di utenti nel sistema di sicurezza dei documenti.
1. Fare clic su Tasti rollover e quindi su OK.
1. Attendi circa 10 minuti.

## Configurazione del controllo degli eventi e delle impostazioni della privacy {#configuring-event-auditing-and-privacy-settings}

La sicurezza dei documenti consente di controllare e registrare le informazioni relative agli eventi correlati all&#39;interazione con documenti, criteri, amministratori e server protetti da policy. È possibile configurare il controllo degli eventi e specificare i tipi di eventi da controllare. Per verificare gli eventi di un documento specifico, è necessario abilitare anche l’opzione di controllo del criterio.

Quando il controllo è abilitato, è possibile visualizzare i dettagli degli eventi controllati nella pagina Eventi. gli utenti della sicurezza dei documenti possono inoltre visualizzare gli eventi correlati in modo specifico ai documenti protetti da policy che utilizzano o creano.

È possibile selezionare i seguenti tipi di eventi per il controllo:

* Eventi di documenti protetti da policy, ad esempio tentativi di apertura di documenti da parte di utenti autorizzati o non autorizzati
* Eventi di criteri quali creazione, modifica, eliminazione, abilitazione e disabilitazione di criteri
* Eventi utente quali inviti e registrazioni di utenti esterni, account utente attivati e disattivati, modifiche alle password utente e aggiornamenti del profilo
* Eventi AEM dei moduli, ad esempio mancata corrispondenza delle versioni, fornitori di autorizzazioni e server di directory non disponibili e modifiche alla configurazione del server

### Attiva o disattiva il controllo eventi {#enable-or-disable-event-auditing}

È possibile abilitare e disabilitare il controllo degli eventi relativi al server, ai documenti protetti da policy, ai criteri, ai set di criteri e agli utenti. Quando si abilita il controllo degli eventi, è possibile scegliere di controllare tutti gli eventi possibili o selezionare eventi specifici da controllare.

Quando si abilita il controllo del server, è possibile visualizzare gli eventi controllati nella pagina Eventi.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documento > Configurazione > Impostazioni di audit e privacy.
1. Per configurare il controllo del server, in Abilita controllo server selezionare Sì o No.
1. Se hai selezionato Sì, in ogni categoria di evento, esegui una delle seguenti azioni per selezionare le opzioni di controllo:

   * Per controllare tutti gli eventi della categoria, selezionare Tutto.
   * Per eseguire il controllo solo su alcuni eventi, deseleziona Tutti, quindi seleziona le caselle di controllo accanto agli eventi da controllare.

      (Vedere [Opzioni di controllo degli eventi](configuring-client-server-options.md#event-auditing-options).)

1. Fai clic su OK.

>[!NOTE]
>
>Quando lavori con le pagine web, evita di utilizzare i pulsanti del browser, ad esempio il pulsante Indietro, il pulsante di aggiornamento e la freccia indietro o avanti, perché questa azione può causare problemi indesiderati di acquisizione dati e visualizzazione dei dati.

### Attiva o disattiva la notifica sulla privacy {#enable-or-disable-privacy-notification}

Puoi abilitare e disabilitare un messaggio di notifica della privacy. Quando si abilita la notifica sulla privacy, viene visualizzato un messaggio quando un destinatario tenta di aprire un documento protetto da policy. L&#39;avviso informa l&#39;utente che l&#39;utilizzo del documento è in corso di verifica. Puoi inoltre specificare un URL che l’utente può utilizzare per visualizzare la pagina dell’informativa sulla privacy, se disponibile.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Configurazione > Impostazioni di audit e privacy.
1. Per configurare la notifica sulla privacy, in Abilita informativa sulla privacy selezionare Sì o No.

   Se i criteri allegati a un documento consentono l&#39;accesso anonimo dell&#39;utente e l&#39;opzione Abilita avviso privacy è impostata su No, all&#39;utente non viene richiesto di effettuare l&#39;accesso e il messaggio di notifica della privacy non viene visualizzato.

   Se i criteri allegati a un documento non consentono l&#39;accesso anonimo, l&#39;utente visualizza il messaggio di notifica della privacy.

1. Se applicabile, nella casella URL privacy , digita l’URL della pagina dell’informativa sulla privacy. Se la casella URL privacy è lasciata vuota, viene visualizzata la pagina privacy di adobe.com.
1. Fai clic su OK.

>[!NOTE]
>
>La disattivazione dell&#39;avviso sulla privacy non disattiva il controllo sull&#39;utilizzo dei documenti. Le azioni di controllo predefinite e le azioni personalizzate supportate tramite il tracciamento dell’uso esteso possono comunque raccogliere informazioni sul comportamento degli utenti.

### Importare un tipo di evento di controllo personalizzato {#import-a-custom-audit-event-type}

Se si utilizza un&#39;applicazione per la protezione dei documenti che supporta il controllo di eventi aggiuntivi, ad esempio eventi specifici per un determinato tipo di file, un partner di Adobe può fornire eventi di controllo personalizzati che è possibile importare nella protezione dei documenti. Utilizza questa funzione solo se un partner di Adobe ti ha fornito tipi di evento personalizzati.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Configurazione > Gestione eventi.
1. Fare clic su Sfoglia per passare al file XML da importare e fare clic su Importa.
1. L’importazione sovrascrive i tipi di evento di controllo personalizzati esistenti sul server se vengono trovate combinazioni identiche di codice evento e namespace.
1. Fai clic su OK.

### Eliminare un tipo di evento di controllo personalizzato {#delete-a-custom-audit-event-type}

1. Nella console di amministrazione, fai clic su Servizi > sicurezza documento > Configurazione > Gestione eventi.
1. Selezionare la casella di controllo accanto al tipo di evento di controllo personalizzato da eliminare e fare clic su Elimina.
1. Fai clic su OK.

### Esporta eventi di controllo {#export-audit-events}

È possibile esportare gli eventi di controllo in un file a scopo di archiviazione.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Configurazione > Gestione eventi.
1. Modifica le impostazioni in Esporta eventi di controllo come necessario. Puoi specificare:

   * l&#39;età minima degli eventi di audit da esportare
   * il numero massimo di eventi di controllo da includere in un singolo file. Il server genera uno o più file in base a questo valore.
   * la cartella in cui verrà creato il file. Questa cartella si trova sul server dei moduli. Se il percorso della cartella è relativo, è relativo alla directory principale del server dell&#39;applicazione.
   * il prefisso del file da utilizzare per i file degli eventi di controllo
   * il formato del file, un file CSV compatibile con Microsoft Excel o un file XML.

1. Fai clic su Esporta. Per annullare l’esportazione, fare clic su Annulla esportazione. Se un altro utente ha pianificato un’esportazione, il pulsante Annulla esportazione non è disponibile fino al completamento dell’esportazione. Il pulsante Annulla esportazione non è disponibile se un altro utente ha pianificato un’esportazione. Per verificare se un&#39;esportazione o un&#39;eliminazione pianificata è stata avviata o completata, fare clic su Aggiorna.

### Elimina eventi di controllo {#delete-audit-events}

È possibile eliminare gli eventi di controllo che superano un numero specificato di giorni.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Configurazione > Gestione eventi.
1. In Elimina eventi di controllo specificare il numero di giorni nella casella Elimina eventi di controllo precedenti a.
1. Fai clic su Elimina. Fai clic su Esporta. Per annullare l’eliminazione, fare clic su Annulla eliminazione. Se un altro utente ha pianificato un&#39;eliminazione, il pulsante Annulla eliminazione non è disponibile fino al completamento dell&#39;esportazione. Il pulsante Annulla eliminazione non è disponibile se un altro utente ha pianificato un’esportazione. Per verificare se un&#39;eliminazione pianificata è iniziata o terminata, fare clic su Aggiorna.

### Opzioni di controllo degli eventi {#event-auditing-options}

È possibile abilitare e disabilitare il controllo degli eventi e specificare i tipi di eventi da controllare.

**Eventi documento**

**Visualizza documento:** un destinatario visualizza un documento protetto da policy.

**Chiudi documento:** un destinatario chiude un documento protetto da policy.

**Stampa a bassa** risoluzioneUn destinatario stampa un documento protetto da policy con l&#39;opzione a bassa risoluzione specificata.

**Stampa ad alta risoluzione:** un destinatario stampa un documento protetto da policy con l&#39;opzione ad alta risoluzione specificata.

**Aggiungi annotazione a documento:** un destinatario aggiunge un’annotazione a un documento PDF.

**Revoca documento:** un utente o amministratore revoca l&#39;accesso a un documento protetto da policy.

**Annulla revoca documento:** un utente o amministratore ripristina l&#39;accesso a un documento protetto da policy.

**Compilazione del modulo:** un destinatario immette informazioni in un documento PDF che è un modulo compilabile.

**Criteri rimossi:** un editore rimuove un criterio da un documento per ritirare le protezioni di sicurezza.

**Modifica URL di revoca del documento:** una chiamata dal livello API modifica l&#39;URL di revoca specificato per accedere a un nuovo documento che sostituisce un documento revocato.

**Modifica documento:** un destinatario modifica il contenuto di un documento protetto da policy.

**Firma documento:** un destinatario firma un documento.

**Proteggere un nuovo documento:** un utente applica un criterio per proteggere un documento.

**Attiva criterio su documento:** un utente o un amministratore commuta il criterio associato a un documento.

**Pubblica documento come:** viene registrato sul server un nuovo documento il cui documentName e la cui licenza sono identici a un documento esistente e i cui documenti non hanno una relazione padre-figlio. Questo evento può essere attivato utilizzando l’SDK per moduli AEM.

**Documento iterato:** viene registrato sul server un nuovo documento il cui documentName e la cui licenza sono identici a un documento esistente e i documenti hanno una relazione padre-figlio. Questo evento può essere attivato utilizzando l’SDK per moduli AEM.

**Eventi dei criteri**

**Criterio creato:** un utente o amministratore crea un criterio.

**Criteri abilitati:** un amministratore rende disponibile un criterio.

**Criterio modificato:** un utente o amministratore modifica un criterio.

**Criteri disabilitati:** un amministratore rende i criteri non disponibili.

**Criterio eliminato:** un utente o amministratore elimina un criterio.

**Cambia proprietario criterio:** una chiamata dal livello API modifica il proprietario del criterio.

**Eventi utente**

**Utente eliminato:** un amministratore elimina un account utente.

**Registra utente invitato:** un utente esterno si registra con la sicurezza del documento.

**Accesso riuscito:** tentativi di accesso riusciti da parte di amministratori o utenti.

**Utenti invitati:** la sicurezza dei documenti invita un utente a registrarsi.

**Utenti attivati:** gli utenti esterni attivano i loro account utilizzando l’URL nel messaggio e-mail di attivazione, oppure un amministratore abilita un account.

**Modifica password:** gli utenti invitati cambiano le password o un amministratore reimposta una password per un utente locale.

**Accesso non riuscito:** tentativi di accesso non riusciti da parte di amministratori o utenti.

**Utenti disattivati:** un amministratore disabilita un account utente locale.

**Aggiornamento profilo:** gli utenti invitati cambiano nome, nome organizzazione e password.

**Account bloccato:** un amministratore blocca un account.

**Eventi set di criteri**

**Set di criteri creato:** un amministratore o un coordinatore di set di criteri crea un set di criteri.

**Set di criteri eliminato:** un amministratore o un coordinatore di set di criteri elimina un set di criteri.

**Set di criteri modificato:** un amministratore o un coordinatore di set di criteri modifica un set di criteri.

**Eventi di sistema**

**Sincronizzazione directory completata:** queste informazioni non sono disponibili nella pagina Eventi. Nella pagina Gestione dominio vengono visualizzate le informazioni correnti sulla sincronizzazione della directory, compreso lo stato e l’ora di sincronizzazione correnti dell’ultima sincronizzazione. Per accedere alla pagina Gestione domini nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

**Client Attiva accesso offline:** accesso offline abilitato dall&#39;utente ai documenti protetti dal server sul computer dell&#39;utente.

**L&#39;applicazione** ClientClient sincronizzata deve sincronizzare le informazioni con il server per consentire l&#39;accesso offline.

**Versione non corrispondente:** versione dell’SDK dei moduli AEM incompatibile con il server che ha tentato di connettersi al server.

**Informazioni sulla sincronizzazione della directory:** queste informazioni non sono disponibili nella pagina Eventi. Nella pagina Gestione dominio vengono visualizzate le informazioni correnti sulla sincronizzazione della directory, compreso lo stato e l’ora di sincronizzazione correnti dell’ultima sincronizzazione. Per accedere alla pagina Gestione domini nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

**Modifica alla configurazione del server:** modifiche alla configurazione del server che vengono effettuate tramite le pagine web o manualmente importando un file config.xml. Ciò include modifiche all&#39;URL di base, timeout sessione, blocchi di accesso, impostazioni della directory, rollover chiave, impostazioni del server SMTP per la registrazione esterna, configurazione della filigrana, opzioni di visualizzazione e così via.

## Configurazione del tracciamento esteso dell&#39;utilizzo {#configuring-extended-usage-tracking}

La sicurezza dei documenti può tenere traccia di vari eventi personalizzati che possono essere eseguiti su un documento protetto. È possibile abilitare il tracciamento degli eventi dal server di sicurezza dei documenti a livello globale o a livello di policy. È quindi possibile impostare un JavaScript per acquisire azioni specifiche eseguite all’interno del documento PDF protetto, ad esempio facendo clic su un pulsante o salvando il documento. Questi dati di utilizzo vengono inviati come file XML in coppie chiave-valore, che puoi utilizzare per ulteriori analisi. Gli utenti finali che accedono ai documenti protetti possono consentire o rifiutare tale tracciamento dall&#39;applicazione client.

Se il tracciamento è abilitato a livello globale, puoi ignorare questa impostazione a livello di criterio e disattivarla per un particolare criterio. L’override a livello di criterio non è possibile se il tracciamento è disabilitato a livello globale. L’elenco degli eventi tracciati viene inviato automaticamente al server quando il conteggio degli eventi raggiunge i 25 o quando il documento viene chiuso. È inoltre possibile configurare lo script in modo da inviare esplicitamente l’elenco di eventi in base alle proprie esigenze. È possibile personalizzare il tracciamento degli eventi accedendo alle proprietà e ai metodi dell&#39;oggetto di protezione del documento.

Dopo aver abilitato il tracciamento, per impostazione predefinita per tutti i criteri creati in seguito verrà attivato il tracciamento. I criteri creati prima che il tracciamento sia abilitato sul server dovranno essere aggiornati manualmente.

### Attiva o disattiva il tracciamento esteso dell&#39;uso {#enable-or-disable-extended-usage-tracking}

Prima di iniziare, assicurati che Server Auditing sia abilitato. Per ulteriori informazioni sul controllo, consulta [Configurazione del controllo degli eventi e delle impostazioni della privacy](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) .

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documento > Configurazione > Impostazioni di audit e privacy.
1. Per configurare il tracciamento dell&#39;uso esteso, in Abilita tracciamento selezionare Sì o No.
1. Per impostare la selezione della casella di controllo Consenti raccolta dati di utilizzo dettagliati nella pagina di accesso, in Abilita tracciamento predefinito, selezionare Sì o No.

Per visualizzare gli eventi tracciati è possibile utilizzare il filtro Eventi documenti nella pagina Eventi. Gli eventi tracciati utilizzando JavaScript sono etichettati come Tracciamento dettagliato dell’utilizzo. Per ulteriori informazioni sugli eventi, consulta [Monitoraggio eventi](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) .

## Configurare le impostazioni di visualizzazione della protezione dei documenti {#configure-document-security-display-settings}

1. Nella console di amministrazione, fai clic su Servizi > sicurezza documento > Configurazione > Opzioni di visualizzazione.
1. Configura le impostazioni e fai clic su OK.

### Impostazioni di visualizzazione {#display-settings}

**Righe da visualizzare per i risultati della ricerca:** Numero di righe che vengono visualizzate su una pagina quando vengono eseguite le ricerche.

**Personalizzazione della finestra di dialogo di accesso al client**

Queste impostazioni controllano il testo visualizzato nel prompt di accesso che viene visualizzato quando un utente accede alla sicurezza del documento tramite un&#39;applicazione client.

**Testo di benvenuto:** testo del messaggio di benvenuto, ad esempio &quot;Accedi con il tuo nome utente e la tua password&quot;. Il testo del messaggio di benvenuto deve contenere informazioni su come accedere alla sicurezza dei documenti e su come contattare un amministratore o un&#39;altra persona di supporto designata nella tua organizzazione per ricevere assistenza. Ad esempio, gli utenti esterni potrebbero dover contattare un amministratore se hanno dimenticato le password o necessitano di assistenza per la procedura di registrazione o di accesso. La lunghezza massima del testo di benvenuto è di 512 caratteri.

**Testo nome utente:** l’etichetta di testo per la casella del nome utente.

**Testo password:** l’etichetta di testo per la casella della password.

**Personalizzazione della finestra di dialogo di autenticazione dei certificati client**

Queste impostazioni controllano il testo visualizzato nella finestra di dialogo di autenticazione del certificato.

**Scegli Testo tipo di autenticazione:** il testo visualizzato per indirizzare un utente alla selezione di un tipo di autenticazione.

**Scegli testo certificato:** testo visualizzato per indirizzare l’utente alla selezione di un tipo di certificato.

**Certificati non disponibili Testo errore:** messaggio di massimo 512 caratteri da visualizzare quando il certificato selezionato non è disponibile.

**Personalizzazione della visualizzazione del certificato client**

**Visualizza solo gli emittenti di credenziali affidabili:** quando questa opzione è selezionata, l&#39;applicazione client presenta all&#39;utente solo i certificati degli emittenti di credenziali che AEM moduli è configurato per l&#39;attendibilità (vedere Gestione di certificati e credenziali). Quando questa opzione non è selezionata, all’utente viene presentato un elenco di tutti i certificati nel sistema dell’utente.

## Configurare le filigrane dinamiche {#configure-dynamic-watermarks}

Utilizzando la protezione dei documenti, è possibile configurare le impostazioni predefinite per l&#39;opzione di filigrana dinamica che è possibile applicare quando si creano i criteri. Una *filigrana* è un&#39;immagine sovrapposta al testo del documento. È utile per tenere traccia del contenuto di un documento e può aiutare a identificare l’uso illegale del contenuto.

Una filigrana dinamica può essere costituita da testo composto da variabili definite quali ID utente e data e testo personalizzato o da contenuti RTF all’interno di un PDF. È possibile configurare le filigrane con diversi elementi ciascuno con il proprio posizionamento e formattazione.

Le filigrane non sono modificabili e pertanto rappresentano un metodo più sicuro per garantire la riservatezza del contenuto del documento. Le filigrane dinamiche garantiscono inoltre che una filigrana mostri informazioni sufficienti per l’utente per fungere da deterrente all’ulteriore distribuzione del documento.

La filigrana specificata da un criterio viene visualizzata nel documento protetto dal criterio quando un destinatario visualizza o stampa il documento. A differenza dei watermark permanenti, nel documento non viene mai salvata una filigrana dinamica, che offre la flessibilità necessaria durante la distribuzione di un documento in un ambiente Intranet per garantire che l&#39;applicazione di visualizzazione visualizzi l&#39;identità dell&#39;utente specifico. Inoltre, se un documento ha più utenti, l&#39;utilizzo della filigrana dinamica consente di utilizzare un documento invece di più versioni, ciascuna con una filigrana diversa. La filigrana visualizzata riflette l’identità dell’utente corrente.

Le filigrane dinamiche sono diverse dalle filigrane che gli utenti possono aggiungere direttamente al documento in Acrobat. Il risultato è che è possibile avere due filigrane in un documento protetto da policy.

### Considerazioni durante la creazione di filigrane {#considerations-when-creating-watermarks}

È possibile creare filigrane dinamiche con diversi elementi di filigrana con ogni elemento specificato come testo o PDF. È possibile includere fino a cinque elementi in una filigrana.

Se scegliete una filigrana basata su testo, potete specificare diversi elementi all’interno della filigrana con più voci di testo e specificare il posizionamento di ciascun elemento. Assegna nomi significativi a questi elementi, ad esempio intestazione, piè di pagina e così via.

Ad esempio, se si desidera specificare come filigrana un testo diverso nell’intestazione, nel piè di pagina, nei margini e all’interno del documento, è necessario creare diversi elementi di filigrana e specificarne le posizioni. Se si desidera che l&#39;ID utente dell&#39;utente e la data corrente di accesso al documento vengano visualizzati nell&#39;intestazione, il nome del criterio a destra e il testo personalizzato &quot;CONFIDENTIAL&quot; vengano visualizzati diagonalmente nel documento, è necessario definire elementi di filigrana separati con testo come tipo e specificarne la formattazione e il posizionamento. Quando la filigrana viene applicata a un documento, tutti gli elementi della filigrana vengono applicati contemporaneamente al documento, nell&#39;ordine in cui vengono aggiunti alla filigrana.

In genere, i watermark basati su PDF vengono utilizzati per includere contenuti grafici quali loghi o simboli speciali come il copyright o il marchio registrato.

È possibile modificare i limiti relativi al numero di elementi di filigrana e alle dimensioni del file PDF modificando il file di configurazione della protezione del documento. Consulta [Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Quando configuri i watermark, tieni presente quanto segue:

* Non è possibile utilizzare un documento PDF protetto da password come elemento di filigrana. Tuttavia, se la filigrana creata contiene altri elementi non protetti da password, verrà applicata come parte della filigrana.
* È possibile modificare la dimensione massima del file PDF che si desidera utilizzare come elemento di filigrana. Tuttavia, i documenti PDF di grandi dimensioni utilizzati come filigrane peggiorano le prestazioni durante la sincronizzazione offline dei documenti applicati con tali filigrane. Consulta [Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Come filigrana viene utilizzata solo la prima pagina del PDF selezionato. Assicurati che le informazioni da visualizzare come filigrana siano disponibili nella prima pagina stessa.
* Anche se è possibile specificare la scala del documento PDF, tenere conto delle dimensioni e del layout della pagina se si intende utilizzarlo come filigrana nell’intestazione, nel piè di pagina o nei margini.
* Quando si specifica il nome del font, inserirlo correttamente. AEM forms sostituisce il font specificato se non è presente nel computer client in cui è aperto il documento.
* Se hai selezionato il testo come contenuto della filigrana, l’impostazione dell’opzione di ridimensionamento come Adatta a pagina non funziona per le pagine con larghezza diversa.
* Quando specifichi il posizionamento degli elementi della filigrana, accertati che non più di un elemento abbia lo stesso posizionamento. Se due elementi di filigrana hanno lo stesso posizionamento, ad esempio il centro, appaiono sovrapposti sul documento e nell&#39;ordine in cui sono stati aggiunti alla filigrana.
* Quando si specificano le dimensioni e il tipo di carattere, verificare che la lunghezza del testo sia completamente visibile all’interno della pagina. I contenuti di testo scorrono su nuove righe, in modo che il contenuto della filigrana che si intendeva presentare nei margini possa sovrapporsi alle aree contenuto delle pagine. Tuttavia, se il documento viene aperto in Acrobat 9, il testo oltre la riga singola viene troncato.

### Limitazioni delle filigrane dinamiche {#limitations-of-dynamic-watermarks}

Alcune applicazioni client potrebbero non supportare i watermark dinamici. Consulta la Guida appropriata per le estensioni Acrobat Reader DC . Inoltre, ricorda quanto segue sulle versioni di Acrobat che supportano i watermark dinamici:

* Non è possibile utilizzare un documento PDF protetto da password come elemento di filigrana.
* Le versioni Acrobat e Adobe Reader precedenti alla 10 non supportano le seguenti funzioni di filigrana:

   * Filigrane PDF
   * Elementi multipli nella filigrana (Testo/PDF)
   * Opzioni avanzate quali l’intervallo di pagine o le opzioni di visualizzazione
   * Opzioni di formattazione del testo quali il font, il nome del font e il colore specificati. Tuttavia, le versioni precedenti di Acrobat e Reader visualizzeranno il contenuto del testo con il font e il colore predefiniti.

* Acrobat 9.0 e versioni precedenti: Acrobat 9.0 e versioni precedenti non supporta i nomi dei criteri nelle filigrane dinamiche. Se Acrobat 9.0 apre un documento protetto da policy con una filigrana dinamica che include un nome di criterio e altri dati dinamici, la filigrana viene visualizzata senza il nome del criterio. Se la filigrana dinamica include solo il nome del criterio, Acrobat visualizza un messaggio di errore

### Aggiungi un modello di filigrana dinamica {#add-a-dynamic-watermark-template}

È possibile creare modelli di filigrana dinamici. Questi modelli rimangono disponibili come opzione di configurazione per i criteri creati dagli amministratori o dagli utenti.

>[!NOTE]
>
>Le informazioni di configurazione della filigrana dinamica non vengono acquisite con le altre informazioni di configurazione quando si esporta un file di configurazione.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Configurazione > Filigrane.
1. Fai clic su Nuovo.
1. Nella casella Nome digitare un nome per la nuova filigrana.

   ***nota **: Non è possibile utilizzare alcuni caratteri speciali nei nomi o nelle descrizioni di filigrane o elementi di filigrana. Consulta le restrizioni elencate in [Considerazioni sulla modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. Sotto Nome, accanto al segno più, immetti un nome significativo per l’elemento filigrana, ad esempio Intestazione, e aggiungi una descrizione ed espandi il segno più per visualizzare le opzioni.
1. In Origine, selezionare il tipo di filigrana come Testo o PDF.
1. Se hai selezionato Testo, procedi come segue:

   * Selezionare i tipi di filigrana da includere. Se si seleziona Testo personalizzato, nella casella adiacente digitare il testo da visualizzare per la filigrana. Tenere presente la lunghezza del testo che verrà visualizzata come filigrana.
   * Specificare le proprietà di formattazione del testo, ad esempio il nome del font, la dimensione del font, il colore in primo piano e il colore dello sfondo per il contenuto del testo della filigrana. Specifica il colore di primo piano e di sfondo come valori esadecimali.

      ***nota **: Se si seleziona l’opzione di ridimensionamento come Adatta alla pagina, la proprietà Dimensione font non è disponibile per la modifica.*

1. Se è stato selezionato PDF per le opzioni relative alle filigrane avanzate, fare clic su **Sfoglia** accanto a Seleziona PDF filigrana per selezionare il documento PDF che si desidera utilizzare come filigrana.

   ***nota **: Non utilizzare un documento PDF protetto da password. Se si specifica un PDF protetto da password come elemento della filigrana, la filigrana non viene applicata.*

1. In Usa come sfondo selezionare Sì o No.

   **nota**: Attualmente, la filigrana viene visualizzata in primo piano indipendentemente da questa impostazione.

1. Per controllare la posizione della filigrana sul documento, configurare le opzioni Allineamento verticale e Allineamento orizzontale.
1. Selezionare Adatta a pagina oppure selezionare % e digitare una percentuale nella casella. Il valore deve essere un numero intero, non una frazione. Per configurare la dimensione della filigrana, è possibile utilizzare un valore che corrisponde alla percentuale della pagina o impostare la filigrana in modo che si adatti alle dimensioni della pagina.
1. Nella casella Rotazione digitare i gradi in base ai quali ruotare la filigrana. L&#39;intervallo è compreso tra -180 e 180. Utilizzare un valore negativo per ruotare la filigrana in senso antiorario. Il valore deve essere un numero intero, non una frazione.
1. Nella casella Opacità digitare una percentuale. Utilizza un numero intero, non una frazione.
1. In Opzioni avanzate, imposta quanto segue:

   **Opzioni intervallo pagine**

   Imposta l&#39;intervallo di pagine in cui deve essere visualizzata la filigrana. Immetti la pagina iniziale come 1 e la pagina finale come -1 per avere tutte le pagine contrassegnate con la filigrana.

   **Opzioni di visualizzazione**

   Selezionare il punto in cui si desidera visualizzare la filigrana. Per impostazione predefinita, la filigrana viene visualizzata sia in copia soft (online) che in copia cartacea (stampata).

1. Fai clic su **Nuovo** in Elementi filigrana per aggiungere altri elementi di filigrana, se necessario.
1. Fai clic su OK.

### Modificare un modello di filigrana dinamica {#edit-a-dynamic-watermark-template}

1. Nella console di amministrazione, fai clic su Servizi > Protezione documento > Configurazione > Filigrane.
1. Fare clic sulla filigrana appropriata nell’elenco.
1. Nella pagina Modifica filigrane modificare le impostazioni in base alle esigenze.
1. Fai clic su OK.

### Eliminare un modello di filigrana dinamica {#delete-a-dynamic-watermark-template}

Quando elimini una filigrana dinamica, non è più disponibile per l’aggiunta a un nuovo criterio. Tuttavia, la filigrana rimane sui criteri esistenti che la utilizzano e i documenti attualmente protetti dal criterio continuano a mostrare la filigrana dinamica fino a quando non modifichi il criterio contenente la filigrana eliminata. Dopo la modifica del criterio, la filigrana non viene più applicata. Viene visualizzato un messaggio che indica che la filigrana esistente viene eliminata sul criterio e che l&#39;utente può selezionarne un&#39;altra per sostituirla.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Configurazione > Filigrane.
1. Selezionare la casella di controllo accanto alla filigrana appropriata e fare clic su Elimina.
1. Fai clic su OK.

## Configurazione della registrazione utente invitata {#configuring-invited-user-registration}

Gli utenti esterni all’organizzazione possono registrarsi con sicurezza dei documenti. Gli utenti invitati che registrano e attivano i propri account possono accedere alla sicurezza dei documenti utilizzando il proprio indirizzo e-mail e la password che creano al momento della registrazione. Gli utenti invitati registrati possono utilizzare documenti protetti da policy a cui dispongono delle autorizzazioni.

Quando gli utenti invitati vengono attivati, diventano utenti locali. Gli utenti locali possono essere configurati e gestiti utilizzando l’area Utenti invitati e locali. (Consulta [Gestione degli account utente invitati e locali](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

A seconda delle funzionalità abilitate per gli utenti invitati, possono utilizzare anche le seguenti funzioni di sicurezza dei documenti:

* Applicazione di criteri ai documenti
* Creare criteri
* Aggiungere utenti invitati ai criteri

La sicurezza dei documenti genera automaticamente un messaggio e-mail di invito alla registrazione quando si verificano i seguenti eventi, a meno che l&#39;utente non sia già nella directory LDAP di origine o sia stato precedentemente invitato a registrarsi:

* Un utente esistente aggiunge un utente invitato a un criterio
* Un amministratore aggiunge un account utente invitato nella pagina Registrazione utente invitata

Il messaggio e-mail di registrazione contiene un collegamento a una pagina Registrazione e informazioni su come registrarsi. Dopo che l’utente invitato si è registrato, la sicurezza dei documenti genera un messaggio e-mail di attivazione con un collegamento a una pagina Attivazione. Quando viene attivato, l’account rimane valido fino a quando non viene disattivato o eliminato.

Se si abilita la registrazione integrata, specificare il server SMTP, i dettagli dell&#39;e-mail di registrazione, le funzionalità di accesso e reimpostare le informazioni relative alla password solo una volta. Prima di abilitare la registrazione integrata, assicurati di aver creato un dominio locale in Gestione utente e aver assegnato il ruolo &quot;Utente invito sicurezza documento&quot; agli utenti e ai gruppi appropriati della tua organizzazione. (Consulta [Aggiungi un dominio locale](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) e [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Se non si utilizza la registrazione integrata, è necessario che sia creato un proprio sistema di registrazione utente utilizzando l’SDK per moduli AEM. Consultare la guida sullo sviluppo di SPI per moduli AEM in [Programmazione con moduli AEM](https://www.adobe.com/go/learn-aemforms-programming-63). Se non utilizzi l’opzione Registrazione incorporata, ti consigliamo di configurare un messaggio nell’e-mail di attivazione e nella schermata di accesso al client per informare gli utenti su come contattare l’amministratore per una nuova password o per altre informazioni.

**Abilita e configura la registrazione degli utenti invitati**

Per impostazione predefinita, il processo di registrazione dell’utente invitato è disabilitato. È possibile abilitare e disabilitare la registrazione utente invitata per la protezione dei documenti, in base alle esigenze.

1. Nella console di amministrazione, fai clic su Servizi > sicurezza documento > Configurazione > Registrazione utente invitata.
1. Selezionare Abilita registrazione utente invitata.
1. (Facoltativo) Aggiorna le impostazioni di registrazione dell&#39;utente invitato come richiesto:

   * [Escludere o includere un utente o un gruppo esterno](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parametri dell&#39;account server e di registrazione](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Impostazioni e-mail dell’invito per la registrazione](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Impostazioni e-mail di attivazione](configuring-client-server-options.md#activation-email-settings)
   * [Configurare un messaggio e-mail di ripristino della password](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Facoltativo) In Registrazione incorporata, selezionare Sì per abilitare questa opzione. Se non si abilita la registrazione integrata, è necessario configurare il proprio sistema di registrazione utente.
1. Fai clic su OK.

### Escludere o includere un utente o un gruppo esterno {#exclude-or-include-an-external-user-or-group}

È possibile limitare la registrazione con la protezione dei documenti per determinati utenti o gruppi di utenti esterni. Questa opzione è utile, ad esempio, per consentire l’accesso a un determinato gruppo di utenti, ma esclude singoli utenti specifici che fanno parte del gruppo.

Le seguenti impostazioni si trovano nell’area Filtro restrizioni e-mail della pagina Registrazione utente invitata .

**Esclusione:** digita l’indirizzo e-mail di un utente o gruppo da escludere. Per escludere più utenti o gruppi, digitare ogni indirizzo e-mail su una nuova riga. Per escludere tutti gli utenti che appartengono a un dominio specifico, immetti un carattere jolly e il nome del dominio. Ad esempio, per escludere tutti gli utenti nel dominio example.com, immetti &amp;ast;.example.com.

**Inclusione:** digita l’indirizzo e-mail di un utente o gruppo da includere. Per includere più utenti o gruppi, digitare ogni indirizzo e-mail su una nuova riga. Per includere tutti gli utenti che appartengono a un dominio specifico, immetti un carattere jolly e il nome del dominio. Ad esempio, per includere tutti gli utenti nel dominio example.com, immetti &amp;ast;.example.com.

### Parametri dell&#39;account server e registrazione {#server-and-registration-account-parameters}

Le seguenti impostazioni si trovano nell’area Impostazioni generali della pagina Registrazione utente invitata .

**Host SMTP:** il nome host del server SMTP. Il server SMTP gestisce gli avvisi e-mail in uscita per registrare e attivare gli account utente invitati.

Se richiesto dall&#39;host SMTP, digitare le informazioni richieste nelle caselle Nome account server SMTP e Password account server SMTP per connettersi al server SMTP. Alcune organizzazioni non applicano questo requisito. Per ulteriori informazioni, rivolgiti all’amministratore di sistema.

**Nome della classe socket del server SMTP:** Nome della classe Socket per il server SMTP. Ad esempio, javax.net.ssl.SSLSocketFactory.

**Tipo di contenuto e-mail:** tipo MIME accettato come text/plain o text/html.

**Codifica e-mail:** formato di codifica da utilizzare per l’invio di messaggi e-mail. È possibile specificare qualsiasi codifica, ad esempio UTF-8 per Unicode o ISO-8859-1 per Latin. Il valore predefinito è UTF-8.

**Indirizzo e-mail di reindirizzamento:** quando specifichi un indirizzo e-mail per questa impostazione, tutti i nuovi inviti vengono inviati all’indirizzo fornito. Questa impostazione può essere utile a scopo di test.

**Usa domini locali:** seleziona il dominio appropriato. In una nuova installazione, assicurati di aver creato il dominio utilizzando Gestione utente. Se si tratta di un aggiornamento, durante l’aggiornamento è stato creato un dominio utente esterno che può essere utilizzato.

**Usa SSL per il server SMTP:** seleziona questa opzione per abilitare SSL per il server SMTP.

**Visualizza il collegamento di accesso nella pagina di registrazione:** visualizza un collegamento di accesso nella pagina di registrazione visualizzata per gli utenti invitati.

**Per abilitare Transport Layer Security (TLS) per il server SMTP**

1. Apri la console di amministrazione.

   Il percorso predefinito della console di amministrazione è `https://<server>:<port>/adminui`.

1. Passa a Home > Servizi > Sicurezza documenti > Configurazione > Registrazione utente invitata.
1. In Registrazione utente invitata specificare tutte le impostazioni di configurazione e quindi fare clic su OK.

   >[!NOTE]
   >
   >Se si utilizza Microsoft Office 365 come server SMTP per l&#39;invio degli inviti per la registrazione utente, utilizzare le impostazioni seguenti:
   >
   >**Host SMTP:** smtp.office365.com
   >**Porta:** 587

1. Successivamente, devi aggiornare config.xml. Consulta [Configurazione per abilitare SMTP per Transport Layer Security (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Se apporti modifiche alle opzioni di Registrazione utente invitata , il file config.xml viene sovrascritto e TLS viene disattivato. Se sovrascrivi le modifiche, devi eseguire il passaggio precedente per riattivare il supporto TLS per la registrazione degli utenti invitati.

### Impostazioni e-mail dell&#39;invito per la registrazione {#registration-invitation-email-settings}

La sicurezza dei documenti invia automaticamente un messaggio e-mail di invito alla registrazione quando crei un nuovo account utente invitato o quando un utente esistente aggiunge un destinatario esterno che non si è precedentemente registrato o che è stato invitato a registrarsi a un criterio. L’e-mail contiene un collegamento che il destinatario può utilizzare per accedere alla pagina di registrazione e inserire le informazioni relative all’account personale, inclusi nome utente e password. La password può essere composta da una combinazione di otto caratteri.

Quando il destinatario attiva l’account, l’utente diventa un utente locale.

Le seguenti impostazioni si trovano nell’area Configurazione e-mail di invito della pagina Registrazione utente invitata .

**Da:** l’indirizzo e-mail da cui viene inviato l’e-mail di invito. Il formato predefinito dell&#39;indirizzo e-mail Da è postmaster@[your_installation_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di invito.

**Timeout:** il numero di giorni successivi alla scadenza dell’invito di registrazione se l’utente esterno non si registra. Il valore predefinito è 30 giorni.

**Messaggio:** testo visualizzato nel corpo del messaggio che invita l’utente a registrarsi.

### Impostazioni e-mail di attivazione {#activation-email-settings}

Dopo la registrazione degli utenti invitati, la sicurezza dei documenti invia un messaggio e-mail di attivazione. Il messaggio e-mail di attivazione contiene un collegamento alla pagina di attivazione dell’account, in cui gli utenti possono attivare il proprio account. Quando gli account vengono attivati, gli utenti possono accedere alla sicurezza dei documenti utilizzando il proprio indirizzo e-mail e la password che hanno creato al momento della registrazione.

Quando il destinatario attiva l’account utente, l’utente diventa un utente locale.

Le seguenti impostazioni si trovano nell’area Configurazione e-mail di attivazione della pagina Registrazione utente invitata .

>[!NOTE]
>
>È inoltre consigliabile configurare un messaggio nella schermata di accesso per consigliare agli utenti esterni come contattare il proprio amministratore per una nuova password o per altre informazioni.

**Da:** l’indirizzo e-mail da cui viene inviato il messaggio e-mail di attivazione. Questo indirizzo e-mail riceve avvisi di consegna non riusciti dall’host e-mail del dichiarante e anche tutti i messaggi che il destinatario invia in risposta all’e-mail di registrazione. Il formato predefinito dell&#39;indirizzo e-mail Da è postmaster@[your_installation_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di attivazione.

**Timeout:** il numero di giorni dopo la scadenza dell’invito di attivazione se l’utente non attiva l’account. Il valore predefinito è 30 giorni.

**Messaggio:** il testo che appare nel corpo del messaggio un messaggio che indica che l’account utente del destinatario deve essere attivato. È inoltre possibile includere informazioni quali la modalità di contatto con un amministratore per ottenere una nuova password.

### Configurare un messaggio e-mail per la reimpostazione della password {#configure-a-password-reset-email}

Se devi reimpostare la password di un utente invitato, viene generato un messaggio e-mail di conferma che invita l’utente a scegliere una nuova password. Impossibile determinare la password di un utente; se l&#39;utente lo dimentica, è necessario reimpostarlo.

Le seguenti impostazioni si trovano nell&#39;area Ripristina e-mail password della pagina Registrazione utente invitata .

**Da:** l’indirizzo e-mail da cui viene inviato il messaggio e-mail di reimpostazione della password. Il formato predefinito dell&#39;indirizzo e-mail Da è postmaster@[your_installation_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di reimpostazione.

**Messaggio:** il testo che appare nel corpo del messaggio un messaggio che indica che la password utente esterna del destinatario viene reimpostata.

## Abilitare utenti e gruppi a creare criteri {#enable-users-and-groups-to-create-policies}

Nella pagina Configurazione è disponibile un collegamento alla pagina Criteri personali, in cui è possibile specificare quali utenti finali possono creare i miei criteri e quali utenti e gruppi sono visibili nei risultati della ricerca. La pagina Criteri personali presenta due schede:

**Scheda Crea criteri:** consente di configurare le autorizzazioni utente per creare criteri personalizzati.

**Scheda Utenti e gruppi visibili:** consente di controllare quali utenti e gruppi sono visibili nei risultati della ricerca utente. L&#39;amministratore super utente o set di criteri è tenuto a selezionare e aggiungere i domini, creati in Gestione utente, all&#39;utente e al gruppo visibili per ciascun set di criteri. Questo elenco è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che il coordinatore del set di criteri può cercare quando sceglie gli utenti da aggiungere ai criteri.

Prima di concedere agli utenti l&#39;autorizzazione per creare criteri personalizzati, considera l&#39;accesso o il controllo che desideri che i singoli utenti dispongano. Inoltre, considera come desideri che gli utenti e i gruppi siano esposti quando li rendi visibili alle ricerche.

### Specificare utenti e gruppi che possono creare criteri {#specify-users-and-groups-who-can-create-policies}

In qualità di amministratore, specifica quali utenti e gruppi possono creare criteri personalizzati. Questa autorizzazione può essere impostata a livello di utente e gruppo. La funzionalità di ricerca cerca gli utenti e i gruppi nel database Gestione utente.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Configurazione > Criteri personali.
1. Nella pagina Criteri personali fare clic sulla scheda Crea criteri e quindi su Aggiungi utenti e gruppi.
1. Nella casella Trova digitare il nome utente o l&#39;indirizzo e-mail dell&#39;utente o del gruppo ricercato. Se non si dispone di queste informazioni, lasciare la casella vuota. È inoltre possibile digitare un nome parziale o un indirizzo e-mail, ad esempio se si conoscono solo le prime due lettere del nome utente.
1. Nell’elenco Utilizzo, seleziona i parametri di ricerca Nome o E-mail.
1. Nell’elenco Tipo, selezionare Gruppo o Utente per limitare la ricerca.
1. Nell’elenco In, selezionare il dominio da cercare. Se non conosci il dominio dell’utente o del gruppo, seleziona Tutti i domini.
1. Nell’elenco Visualizzazione specificare il numero di risultati di ricerca da visualizzare per pagina, quindi fare clic su Trova.
1. Per aggiungere utenti e gruppi Criteri personali, selezionare la casella di controllo relativa a ciascun utente e gruppo da aggiungere.
1. Fare clic su Aggiungi e quindi su OK.

Gli utenti e i gruppi selezionati ora dispongono delle autorizzazioni necessarie per creare criteri personalizzati.

### Rimuovere l&#39;autorizzazione per la creazione di criteri personalizzati da un utente o gruppo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Nella pagina di protezione del documento fare clic su Configurazione > Criteri personali.
1. Nella pagina Criteri personali fare clic sulla scheda Crea criteri . Vengono visualizzati gli utenti e i gruppi autorizzati a creare criteri personalizzati.
1. Seleziona la casella di controllo accanto agli utenti e ai gruppi da rimuovere da questa autorizzazione.
1. Fare clic su Elimina, quindi su OK.

### Specifica utenti e gruppi visibili nelle ricerche {#specify-users-and-groups-that-are-visible-in-searches}

Quando gli utenti gestiscono i propri criteri personalizzati, possono cercare utenti e gruppi da aggiungere ai propri criteri. Devi specificare i domini da cui gli utenti e i gruppi sono visibili in queste ricerche.

1. Nella pagina di protezione del documento fare clic su Configurazione > Criteri personali.
1. Nella pagina Criteri personali fare clic sulla scheda Utenti e gruppi visibili .
1. Per rendere visibili gli utenti e i gruppi di un dominio, fai clic su Aggiungi domini, seleziona i domini e fai clic su Aggiungi. Per rimuovere un dominio, seleziona la casella di controllo accanto al nome di dominio e fai clic su Elimina.

## Modifica manuale del file di configurazione della protezione del documento {#manually-editing-the-document-security-configuration-file}

È possibile importare ed esportare le informazioni di configurazione memorizzate nel database di protezione dei documenti. Ad esempio, è possibile creare una copia di backup delle informazioni di configurazione quando si passa da un ambiente di staging a un ambiente di produzione oppure modificare opzioni avanzate che possono essere configurate solo per la modifica di questo file.

Puoi apportare le seguenti modifiche utilizzando il file di configurazione:

[Visualizza le autorizzazioni CATIA durante la creazione e la modifica dei criteri](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Specifica un periodo di timeout per la sincronizzazione offline](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Negazione dei servizi di sicurezza dei documenti per applicazioni specifiche](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Disattivazione dei collegamenti esterni](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>L’importazione del file di configurazione riconfigura il sistema in base alle informazioni presenti nel file. Le eccezioni sono la configurazione della filigrana dinamica e le informazioni sugli eventi personalizzati, che non vengono salvate con il file di configurazione esportato. Devi configurare queste informazioni manualmente nel nuovo sistema. Solo un amministratore di sistema o un consulente di servizi professionali che abbia familiarità con la sicurezza dei documenti e con XML deve modificare il contenuto di un file di configurazione, ad esempio per riconfigurare un&#39;impostazione danneggiata o per ottimizzare i parametri di un particolare scenario di distribuzione aziendale.

**Esportare un file di configurazione**

1. Nella console di amministrazione, fare clic su Servizi > sicurezza documento 11 > Configurazione > Configurazione manuale.
1. Fai clic su Esporta e salva il file di configurazione in un altro percorso. Il nome file predefinito è config.xml.
1. Fai clic su OK.
1. Prima di modificare il file di configurazione, crea una copia di backup nel caso sia necessario ripristinarlo.

**Importare un file di configurazione**

1. Nella console di amministrazione, fare clic su Servizi > sicurezza documento 11 > Configurazione > Configurazione manuale.
1. Fare clic su Sfoglia per passare al file di configurazione e quindi su Importa. Non è possibile digitare il percorso direttamente nella casella Nome file.
1. Fai clic su OK.

### Specifica un periodo di timeout per la sincronizzazione offline {#specify-a-timeout-period-for-offline-synchronization}

La protezione dei documenti consente agli utenti di aprire e utilizzare documenti protetti quando non sono connessi al server di protezione dei documenti. L’applicazione client dell’utente deve sincronizzarsi regolarmente con il server per mantenere i documenti validi per l’uso offline. La prima volta che gli utenti aprono un documento protetto, viene chiesto loro se il loro computer deve essere autorizzato a eseguire la sincronizzazione client periodica.

Per impostazione predefinita, la sincronizzazione viene eseguita automaticamente ogni quattro ore e in base alle esigenze quando un utente è connesso al server di sicurezza dei documenti. Se il periodo offline di un documento scade mentre l&#39;utente è offline, è necessario riconnettersi al server per consentire all&#39;applicazione client di eseguire la sincronizzazione con il server.

Nel file di configurazione della protezione del documento è possibile specificare la frequenza predefinita della sincronizzazione automatica in background. Questa impostazione funge da applicazione client per il periodo di timeout predefinito, a meno che il client non imposti esplicitamente il proprio valore di timeout.

1. Esporta il file di configurazione della protezione del documento. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `PolicyServer` . Sotto quel nodo, individua il nodo `ServerSettings`.
1. Nel nodo `ServerSettings`, aggiungi la seguente voce e salva il file:

   `<entry key="BackgroundSyncFrequency" value="`*time* `"/>`

   dove *time* è il numero di secondi tra le sincronizzazioni in background automatiche. Se hai inviato questo valore a `0`, la sincronizzazione si verifica sempre. Il valore predefinito è `14400` secondi (ogni quattro ore).

1. Importa il file di configurazione. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Negazione dei servizi di sicurezza dei documenti per applicazioni specifiche {#denying-document-security-services-for-specific-applications}

È possibile configurare la protezione dei documenti per negare i servizi alle applicazioni che soddisfano criteri specifici. I criteri possono specificare un singolo attributo, ad esempio un nome di piattaforma, oppure più set di attributi. Questa funzione consente di controllare le richieste che la sicurezza del documento deve gestire. Di seguito sono elencate alcune applicazioni di questa funzione:

* **Protezione dei ricavi:** puoi negare l’accesso a qualsiasi applicazione client che non supporta le convenzioni sui ricavi.
* **Compatibilità dell’applicazione:** alcune applicazioni possono essere incompatibili con i criteri o il comportamento del server di sicurezza dei documenti.

Quando le applicazioni client tentano di stabilire un collegamento con la sicurezza dei documenti, forniscono informazioni su applicazione, versione e piattaforma. La protezione dei documenti confronta queste informazioni con le impostazioni di negazione ottenute dal file di configurazione della protezione dei documenti.

Le impostazioni Rifiuti possono contenere diversi set di condizioni di rifiuto. Se tutti gli attributi di un set corrispondono, all’applicazione richiedente viene negato l’accesso ai servizi di sicurezza dei documenti.

La funzione di negazione del servizio richiede che le applicazioni client utilizzino la versione 8.2 o successiva dell’SDK client C++ per la protezione dei documenti. I seguenti prodotti di Adobe forniscono informazioni sui prodotti durante la richiesta di servizi di sicurezza dei documenti:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard e versioni successive
* Adobe Reader 9.0 e versioni successive
* Estensioni Acrobat Reader DC per Microsoft Office 8.2 e versioni successive

Le applicazioni client utilizzano l’API client dall’SDK client per la protezione dei documenti C++ per richiedere i servizi dalla protezione dei documenti. Le richieste API client includono informazioni sulla versione di piattaforma e SDK (precompilate nell’API client) e informazioni sul prodotto ottenute dall’applicazione client.

Le applicazioni client o i plug-in forniscono informazioni di prodotto nella loro implementazione di una funzione di callback. L&#39;applicazione fornisce le seguenti informazioni:

* Nome integratore
* Versione integratore
* Famiglia di applicazioni
* Nome applicazione
* Versione applicazione

Se non sono disponibili informazioni, l&#39;applicazione client lascia vuoto il campo corrispondente.

Diverse applicazioni di Adobe includono informazioni sui prodotti durante la richiesta di servizi di sicurezza dei documenti, tra cui le estensioni Acrobat, Adobe Reader e Acrobat Reader DC per Microsoft Office.

**Acrobat e Adobe Reader**

Quando Acrobat o Adobe Reader richiedono un servizio da Document Security, fornisce le seguenti informazioni di prodotto:

* **Integratore:** Adobe Systems, Inc.
* **Versione integratore:** 1.0
* **Famiglia di applicazioni:** Acrobat
* **Nome applicazione:** Acrobat
* **Versione applicazione:** 9.0.0

**Estensioni Acrobat Reader DC per Microsoft Office**

Acrobat Reader DC extensions for Microsoft Office è un plug-in utilizzato con i prodotti Microsoft Office Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Quando richiede un servizio, fornisce le seguenti informazioni:

* **Integratore:** Adobe Systems Incorporated
* **Versione integratore:** 8.2
* **Famiglia di applicazioni:** estensioni Acrobat Reader DC per Microsoft Office
* **Nome applicazione:** Microsoft Word, Microsoft Excel o Microsoft PowerPoint
* **Versione applicazione:** 2003 o 2007

**Configurare la protezione dei documenti per negare i servizi per applicazioni specifiche**

1. Esporta il file di configurazione della protezione del documento. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `PolicyServer` . Aggiungi un nodo `ClientVersionRules` come figlio immediato del nodo `PolicyServer`, se non esiste:

   ```xml
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   dove:

   `SDKPlatforms` specifica la piattaforma che ospita l&#39;applicazione client. I valori possibili sono:

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` specifica la versione dell&#39;API client C++ di protezione del documento utilizzata dall&#39;applicazione client. Esempio, `"8.2"`.

   `APPFamilies` è definito dall’API client.

   `AppName`specifica il nome dell&#39;applicazione client. Le virgole vengono utilizzate come separatori di nome. Per includere una virgola in un nome, eseguine il escape con un carattere barra rovesciata (\). Ad esempio, *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` specifica la versione dell&#39;applicazione client.

   `Integrators` specifica il nome della società o del gruppo che ha sviluppato il plug-in o l&#39;applicazione integrata.

   `IntegratorVersions` è la versione del plug-in o dell’applicazione integrata.

1. Per ogni set aggiuntivo di dati non consentiti, aggiungi un altro elemento *MyEntryName*.
1. Salva il file di configurazione.
1. Importa il file di configurazione. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**Esempi**

In questo esempio, a tutti i client Windows viene negato l&#39;accesso.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

In questo esempio, l&#39;accesso a My Application versione 3.0 e My Other Application versione 2.0 è negato. Lo stesso URL di informazioni di rifiuto viene utilizzato indipendentemente dal motivo del rifiuto.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

In questo esempio, tutte le richieste provenienti da un&#39;installazione di Microsoft PowerPoint 2007 o Microsoft PowerPoint 2010 di estensioni Acrobat Reader DC per Microsoft Office sono negate.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### Modifica i parametri di configurazione della filigrana {#change-the-watermark-configuration-parameters}

Per impostazione predefinita, è possibile specificare un massimo di cinque elementi in una filigrana. Inoltre, la dimensione massima del file del documento PDF che si desidera utilizzare come filigrana è limitata a 100 KB. Puoi modificare questi parametri nel file config.xml.

***nota **: È necessario modificare questi parametri con cautela.*

1. Esporta il file di configurazione della protezione del documento. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `ServerSettings` .
1. Nel nodo `ServerSettings`, aggiungi le seguenti voci e salva il file: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   La prima voce, *dimensione massima del file* è la dimensione massima del file (in KB) consentita per un elemento filigrana PDF. Il valore predefinito è 100 KB.

   La seconda voce, *elementi massimi* è il numero massimo di elementi consentiti in una filigrana. Il valore predefinito è 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importa il file di configurazione. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Disabilitazione dei collegamenti esterni {#disabling-external-links}

Molti utenti della sicurezza dei documenti non hanno accesso a collegamenti esterni come **www.adobe.com** mentre utilizzano le interfacce utente di Gestione destra:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Le seguenti modifiche al file config.xml disattivano tutti i collegamenti esterni dalle interfacce utente di Right Management.

1. Esporta il file di configurazione della protezione del documento. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `DisplaySettings` .
1. Per disabilitare tutti i collegamenti esterni, nel nodo `DisplaySettings` aggiungi la seguente voce e salva il file: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importa il file di configurazione. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configurazione per abilitare SMTP per Transport Layer Security (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Le seguenti modifiche al file config.xml abilitano il supporto TLS per la funzione di registrazione degli utenti invitati .

1. Esporta il file di configurazione della protezione del documento. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `DisplaySettings` .
1. Individua il seguente nodo: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Imposta il valore della chiave `SmtpUseTls` nel nodo `ExternalUser` su **true**.
1. Imposta il valore della chiave `SmtpUseSsl` nel nodo `ExternalUser` su **false**.
1. Salva il `config.xml`.
1. Importa il file di configurazione. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Disattiva gli endpoint SOAP per i documenti di sicurezza dei documenti {#disable-soap-endpoints-for-document-security-documents}

Le seguenti modifiche al file config.xml per disabilitare gli endpoint SOAP per i documenti di sicurezza dei documenti.

1. Esporta il file di configurazione della protezione del documento. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il seguente nodo: `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. Nel nodo DRM, individua il nodo `entry`:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Per disabilitare gli endpoint SOAP per i documenti di sicurezza, impostare l&#39;attributo value su **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Salva il `config.xml`.
1. Importa il file di configurazione. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Maggiore scalabilità del server di sicurezza dei documenti {#increasingscalability}

Per impostazione predefinita, durante la sincronizzazione di un documento per l&#39;utilizzo offline, insieme alle informazioni relative al documento corrente, i client di protezione del documento recuperano le informazioni relative a criteri, filigrane, licenze e revoche per tutti gli altri documenti a cui l&#39;utente ha accesso. Se tali aggiornamenti e informazioni non vengono sincronizzati con il client, è possibile che un documento aperto in modalità offline si apra ancora con informazioni precedenti su criteri, filigrane e revoche.

È possibile aumentare la scalabilità del server di protezione dei documenti limitando le informazioni inviate al client. La riduzione della quantità di informazioni inviate al client comporta una maggiore scalabilità, una riduzione dei tempi di risposta e migliori prestazioni del server. Esegui i seguenti passaggi per aumentare la scalabilità:

1. Esporta il file di configurazione della protezione del documento. (Vedere [Modifica manuale del file di configurazione della protezione del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo ServerSettings .
1. Nel nodo ServerSettings, imposta il valore della proprietà `DisableGlobalOfflineSynchronizationData`su `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Se impostato su true, il server di protezione dei documenti invia informazioni solo per il documento corrente e le informazioni per il resto dei documenti (gli altri documenti a cui un utente ha accesso) non vengono inviate al client.

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore della chiave `DisableGlobalOfflineSynchronizationData`è impostato su `false`.

1. Salva e importa il file di configurazione. (Vedere [Modifica manuale del file di configurazione della protezione del documento](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

