---
title: Configurazione delle opzioni client e server
description: Scopri come configurare le varie opzioni client e server, come le impostazioni di configurazione del server, i ruoli di protezione dei documenti e l’auditing degli eventi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '10278'
ht-degree: 100%

---

# Configura il server della protezione dei documenti {#configure-the-document-security-server}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Configurazione server.
1. Configura le impostazioni e fai clic su OK.

## Impostazioni della configurazione dei canali {#server-configuration-settings}

**URL di base:** URL di base per la protezione dei documenti, contenente il nome e la porta del server. Le informazioni associate alla base creano gli URL di connessione. Ad esempio, viene associato /edc/Main.do per accedere alle pagine web. Gli utenti rispondono anche agli inviti di registrazione degli utenti esterni tramite questo URL.

Se utilizzi IPv6, immetti l’URL di base come nome del computer o nome DNS. Se utilizzi un indirizzo IP numerico, Acrobat non riuscirà ad aprire i file protetti tramite policy. Utilizza anche l’URL HTTP protetto (HTTPS) per il server.

>[!NOTE]
>
>L’URL di base è incorporato in file protetti tramite policy. Le applicazioni client utilizzano l’URL di base per riconnettersi al server. I file protetti continueranno a contenere l’URL di base, anche se viene modificato in seguito. Se modifichi l’URL di base, le informazioni di configurazione devono essere aggiornate per tutti i client connessi.

**Periodo di lease offline predefinito:** periodo di tempo predefinito durante il quale un utente può utilizzare un documento protetto offline. Questa impostazione determina il valore iniziale dell’impostazione del periodo di lease per l’attivazione automatica della modalità offline durante la creazione di un criterio. Consulta Creazione e modifica dei criteri. Alla scadenza del periodo di lease, il destinatario deve sincronizzare nuovamente il documento per continuare a utilizzarlo.

Per una discussione sul funzionamento del lease e della sincronizzazione offline, consulta [Introduzione alla configurazione del lease e della sincronizzazione offline](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Periodo di sincronizzazione offline predefinito:** il tempo massimo per l’utilizzo non in linea di un documento dal momento in cui è inizialmente protetto.

**Timeout sessione client:** periodo di tempo, in minuti, dopo il quale la protezione dei documenti si disconnette se un utente che ha eseguito l’accesso tramite un’applicazione client non interagisce con la protezione dei documenti.

**Consenti accesso a utenti anonimi:** seleziona questa opzione per consentire la creazione di criteri personali e condivisi che consentano agli utenti anonimi di aprire documenti protetti da criteri. Gli utenti che non dispongono di account possono visualizzare il documento, ma non possono accedere alla protezione dei documenti o utilizzare altri documenti protetti da criteri.

**Disabilita accesso ai client versione 7:** specifica se gli utenti possono utilizzare Acrobat o Reader 7.0 per connettersi al server. Quando questa opzione è selezionata, gli utenti devono utilizzare Acrobat o Reader 8.0 e versioni successive per completare le operazioni di protezione dei documenti sui documenti in PDF. Se i criteri richiedono che Acrobat o Reader 8.0 e versioni successive vengano eseguiti in modalità certificata all’apertura di documenti protetti da criteri, disabilita l’accesso a Acrobat o Reader 7. Consulta Specificare le autorizzazioni del documento per utenti e gruppi.

**Consenti accesso offline per documento:** seleziona questa opzione per specificare l’accesso offline per documento. Se questa impostazione è abilitata, l’utente avrà accesso offline solo ai documenti che ha aperto online almeno una volta.

**Consenti autenticazione con password e nome utente:** seleziona questa opzione per consentire alle applicazioni client di utilizzare l’autenticazione con nome utente/password durante la connessione al server.

**Consenti autenticazione Kerberos:** seleziona questa opzione per consentire alle applicazioni client di utilizzare l’autenticazione Kerberos durante la connessione al server.

**Consenti autenticazione tramite certificato client:** seleziona questa opzione per consentire alle applicazioni client di utilizzare l’autenticazione tramite certificato durante la connessione al server.

**Consenti autenticazione estesa:** seleziona questa opzione per abilitare l’autenticazione estesa, quindi immettere l’URL di destinazione per l’autenticazione estesa.

Se selezioni questa opzione, le applicazioni client potranno utilizzare l’autenticazione estesa. L’autenticazione estesa fornisce processi di autenticazione personalizzati e diverse opzioni di autenticazione configurate sul server AEM Forms. Ad esempio, ora gli utenti possono utilizzare l’autenticazione basata su SAML invece del nome utente/password di AEM Forms da Acrobat e Reader Client. Per impostazione predefinita, l’URL di destinazione contiene *localhost* come nome del server. Sostituisci il nome del server con un nome host completo. Se l’autenticazione estesa non è ancora abilitata, il nome host nell’URL di destinazione viene completato automaticamente dall’URL di base. Consulta [Aggiungere il provider di autenticazione estesa](configuring-client-server-options.md#add-the-extended-authentication-provider).

***nota **: l’autenticazione estesa è supportata da Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.*

**Larghezza controllo HTML preferita per l’autenticazione estesa:** specifica la larghezza della finestra di dialogo di autenticazione estesa che si apre in Acrobat per l’immissione delle credenziali utente.

**Altezza controllo HTML preferita per l’autenticazione estesa:** specifica l’altezza della finestra di dialogo di autenticazione estesa che si apre in Acrobat per l’immissione delle credenziali utente.

***nota **: i limiti di larghezza e altezza per questa finestra di dialogo sono i seguenti:*
Larghezza: minima = 400, massima = 900

Altezza: minima = 450; massima = 800

**Abilita memorizzazione cache di credenziali client:** seleziona questa opzione per consentire agli utenti di memorizzare le credenziali nella cache (nome utente e password). Quando le credenziali degli utenti vengono memorizzate nella cache, non è necessario immetterle ogni volta che viene aperto un documento o quando viene fatto clic sul pulsante Aggiorna nella pagina Gestisci criteri di sicurezza di Adobe Acrobat. Puoi specificare il numero di giorni prima che gli utenti debbano fornire nuovamente le credenziali. Se imposti il numero di giorni su 0, le credenziali possono essere memorizzate nella cache per un tempo indeterminato.

## Configurazione di utenti e amministratori della protezione dei documenti {#configuring-document-security-users-and-administrators}

### Assegnazione di ruoli di protezione dei documenti agli amministratori {#assigning-document-security-roles-to-administrators}

L’ambiente AEM Forms contiene uno o più utenti amministratori che dispongono dei privilegi appropriati per la creazione di utenti e gruppi. Se la tua organizzazione utilizza la protezione dei documenti, è necessario assegnare il diritto di gestire gli utenti invitati e locali ad almeno un amministratore.

Gli amministratori devono inoltre disporre del ruolo di utente della console di amministrazione per accedere alla console di amministrazione. (Consulta [Creazione e configurazione dei ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configurazione di utenti e gruppi visibili {#configuring-visible-users-and-groups}

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti dei criteri, un amministratore principale o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati nella Gestione utenti) all’elenco visibile di utenti e gruppi per ogni set di criteri.

L’elenco visibile di utenti e gruppi è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l’utente finale può sfogliare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà alcun utente o gruppo da aggiungere al criterio. Per ogni set di criteri può essere presente più di un coordinatore.

1. Dopo aver installato e configurato l’ambiente AEM Forms con la protezione dei documenti, imposta tutti i domini appropriati nella Gestione utenti. <!-- Fix broken link (See Setting up and managing domains) -->

   ***Nota **: prima di creare i criteri è necessario creare i domini.*

1. Nella console di amministrazione, fai clic su Servizi > Gestione documenti > Criteri, quindi fai clic sulla scheda Set di criteri.
1. Seleziona Set di criteri globale, quindi fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.
1. Passa a Servizi > Protezione dei documenti > Configurazione > Criteri personali e fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.

## Aggiungere il provider di autenticazione estesa {#add-the-extended-authentication-provider}

AEM Forms fornisce una configurazione di esempio che puoi personalizzare per il tuo ambiente. Esegui i passaggi seguenti:

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

1. Ottieni il file WAR di esempio per distribuirlo. Consulta la guida all’installazione appropriata per il server applicazioni.
1. Assicurati che il server Forms disponga di un nome completo invece di un indirizzo IP come URL di base e che l’URL sia in HTTPS. Consulta [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).
1. Abilita l’autenticazione estesa dalla pagina di configurazione del server. Consulta [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).
1. Aggiungi gli URL di reindirizzamento SSO richiesti nel file di configurazione della Gestione utenti. Consulta [Aggiungi URL di reindirizzamento SSO per l’autenticazione estesa](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Aggiungere URL di reindirizzamento SSO per l’autenticazione estesa {#add-sso-redirect-urls-for-extended-authentication}

Se l’autenticazione estesa è abilitata, gli utenti che aprono un documento protetto da criteri in Acrobat XI o Reader XI visualizzano una finestra di dialogo per l’autenticazione. Questa finestra di dialogo carica la pagina HTML specificata come URL di destinazione per l’autenticazione estesa nelle impostazioni del server per la protezione dei documenti. Consulta [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Esporta e salva il file di configurazione sul disco.
1. Apri il file in un editor e individua il nodo AllowedUrls.
1. Nel nodo `AllowedUrls` aggiungi le righe seguenti: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Salva il file e importa il file aggiornato dalla pagina di configurazione del manuale: nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione.

## Configurazione della sicurezza offline {#configuring-offline-security}

La protezione dei documenti consente di utilizzare documenti protetti da criteri in modalità non in linea senza una connessione Internet o di rete. Questa capacità richiede che i criteri consentano l’accesso offline, come descritto in [Specificare le autorizzazioni del documento per utenti e gruppi](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Prima che un documento che dispone di tale criterio possa essere utilizzato in modalità offline, il destinatario deve aprire il documento in modalità online e abilitare l’accesso offline facendo clic su Sì quando richiesto. Al destinatario può anche essere richiesto di autenticare la sua identità. Il destinatario può quindi utilizzare i documenti offline per la durata del periodo di lease specificato nel criterio.

Al termine del periodo di lease offline, il destinatario deve sincronizzarsi nuovamente con la protezione dei documenti aprendo un documento online o utilizzando un comando di menu delle estensioni di Acrobat o Acrobat Reader DC extensions per eseguire la sincronizzazione. Consulta la *Guida di Acrobat* o la *Guida delle estensioni di Adobe Reader DC* appropriata.

Poiché i documenti che consentono l’accesso offline richiedono la memorizzazione nella cache del materiale chiave nel computer in cui sono memorizzati i file offline, il file potrebbe essere compromesso se un utente non autorizzato può ottenere il materiale chiave. Per compensare questa possibilità, sono disponibili opzioni di rollover della chiave, pianificate e manuali, che puoi configurare per impedire a persone non autorizzate di utilizzarla per accedere al documento.

### Impostare un periodo di lease offline predefinito {#set-a-default-offline-lease-period}

I destinatari dei documenti protetti da criteri possono tenerli offline per il numero di giorni specificato nel criterio. Dopo la sincronizzazione iniziale con la protezione documenti, il destinatario può utilizzare il documento offline fino alla scadenza del periodo di lease offline. Alla scadenza del periodo di lease, il destinatario deve caricare il documento online e accedere per sincronizzare la protezione documenti per continuare a utilizzarlo.

Puoi configurare un periodo di lease offline predefinito. Il valore predefinito del periodo di lease può essere cambiato da chiunque crea o modifica un criterio.

1. Nella pagina di Protezione documenti, fai clic su Configurazione > Configurazione server.
1. Nella casella Periodo di lease offline predefinito digita il numero di giorni consentiti per il lease offline.
1. Fai clic su OK.

### Gestire i rollover chiave {#manage-key-rollovers}

Protezione documenti utilizza algoritmi di crittografia e licenze per proteggere i documenti. Quando crittografa un documento, Protezione documenti genera e gestisce una chiave di decrittografia denominata *DocKey* che passa all’applicazione client. Se il criterio che protegge un documento consente l’accesso offline, viene generata anche una chiave offline denominata *Chiave principale* per ogni utente che dispone dell’accesso offline al documento.

>[!NOTE]
>
>Se non esiste una chiave principale, Protezione documenti ne genera una per la sicurezza di un documento.

Per aprire offline un documento protetto da criteri, è necessario che il computer dell’utente disponga della chiave principale appropriata. Il computer ottiene la chiave principale quando l’utente sincronizza Protezione documenti (apre un documento protetto online). Se questa chiave principale è compromessa, potrebbe essere compromesso anche qualsiasi documento a cui l’utente ha accesso offline.

Un modo per ridurre la minaccia per i documenti offline consiste nell’evitare di consentire l’accesso offline a documenti particolarmente sensibili. Un altro metodo consiste nell’effettuare periodicamente il rollover delle chiavi principali. Quando Protezione documenti esegue il rollover, tutte le chiavi esistenti non possono più accedere ai documenti protetti da criteri. Ad esempio, se una persona disonesta ottiene una chiave principale da un laptop rubato, tale chiave non può essere utilizzata per accedere ai documenti protetti dopo il rollover. Se sospetti che una chiave principale specifica sia stata compromessa, puoi eseguirne manualmente il rollover.

Tuttavia, un rollover della chiave influisce su tutte le chiavi principali, non solo su una. Inoltre, riduce la scalabilità del sistema perché i client devono memorizzare più chiavi per l’accesso offline. La frequenza predefinita di rollover della chiave è di 20 giorni. Si consiglia di non impostare questo valore sotto i 14 giorni, poiché potrebbe essere impedita la visualizzazione dei documenti offline agli utenti e le prestazioni del sistema potrebbero risentirne.

Nell’esempio seguente, Chiave1 è la prima delle due chiavi principali e Chiave2 è la più recente. Quando fai clic sul pulsante Rollover chiavi ora la prima volta, la Chiave1 non è più valida e viene generata una nuova chiave principale valida (Chiave3). Gli utenti otterranno la Chiave3 quando eseguono la sincronizzazione con Protezione documenti, in genere aprendo un documento protetto online. Tuttavia, gli utenti non sono costretti a sincronizzare Protezione documenti fino a quando non raggiungono il periodo massimo di lease offline specificato in un criterio. Dopo il primo rollover della chiave, gli utenti che rimangono offline possono comunque aprire i documenti offline, inclusi quelli protetti da Chiave3, fino a raggiungere il periodo massimo di lease. Quando fai nuovamente clic sul pulsante Rollover chiavi ora, la Chiave2 non è più valida e viene creata la Chiave4. Gli utenti che rimangono offline durante i due rollover della chiave non possono aprire i documenti protetti con Chiave3 o Chiave4 finché non sincronizzano Protezione documenti.

**Modificare la frequenza di rollover della chiave**

Per motivi di riservatezza, quando utilizzi documenti offline, Protezione documenti fornisce un’opzione di rollover automatico della chiave con un periodo di frequenza predefinito di 20 giorni. Puoi modificare la frequenza di rollover; tuttavia, evita di impostare un valore inferiore a 14 giorni, in quanto potrebbe essere impedita la visualizzazione dei documenti offline agli utenti e le prestazioni del sistema potrebbero risentirne.

1. Nella pagina Protezione documenti, fai clic su Configurazione > Key Management (Gestione chiavi).
1. Nella casella Frequenza rollover chiave digita il numero di giorni per il periodo di rollover.
1. Fai clic su OK.

**Eseguire manualmente il rollover delle chiavi principali**

Per mantenere la riservatezza dei documenti offline, è possibile eseguire manualmente il rollover delle chiavi principali. Potrebbe essere necessario eseguire manualmente il rollover di una chiave (ad esempio, se viene compromessa da un utente che la ottiene da un computer in cui è memorizzata nella cache per consentire l’accesso offline a un documento).

>[!NOTE]
>
>Evita di utilizzare frequentemente il rollover manuale, in quanto causa il rollover di tutte le chiavi principali, non solo di una, e può impedire temporaneamente agli utenti di visualizzare nuovi documenti offline.

È necessario eseguire il rollover delle chiavi principali due volte prima che le chiavi esistenti nei computer client vengano invalidate. I computer client che hanno chiavi principali invalidate devono sincronizzarsi nuovamente con il servizio Protezione documenti per acquisire le nuove chiavi principali.

1. Nella pagina Protezione documenti, fai clic su Configurazione > Key Management (Gestione chiavi).
1. Fai clic sui tasti di rollover, quindi su OK.
1. Attendi circa 10 minuti. Nel registro del server viene visualizzato il seguente messaggio: `Done RightsManagement key rollover for`*N* `principals`. Dove *N* è il numero di utenti presenti nel sistema di protezione dei documenti.
1. Fai clic sui tasti di rollover, quindi su OK.
1. Attendi circa 10 minuti.

## Configurare l’auditing degli eventi e le impostazioni di privacy {#configuring-event-auditing-and-privacy-settings}

La funzione Protezione dei documenti consente di controllare e registrare le informazioni su eventi correlati all’interazione con documenti protetti da criteri, criteri, amministratori e server. Puoi configurare l’auditing degli eventi e specificare i tipi di eventi da controllare. Per effettuare l’auditing degli eventi di un determinato documento, è necessario abilitare anche l’opzione di auditing relativa al criterio.

Quando l’auditing è abilitato, puoi visualizzare i dettagli degli eventi controllati nella pagina Eventi. Gli utenti di Protezione dei documenti possono anche visualizzare gli eventi correlati specificamente ai documenti protetti da criteri che utilizzano o creano.

È possibile selezionare i seguenti tipi di eventi per l’auditing:

* Eventi di documenti protetti da criteri, ad esempio tentativi di apertura di documenti da parte di utenti autorizzati o non autorizzati
* Eventi relativi ai criteri, ad esempio creazione, modifica, eliminazione, abilitazione e disabilitazione dei criteri
* Eventi dell’utente, ad esempio inviti e registrazioni di utenti esterni, account utente attivati e disattivati, modifiche alle password dell’utente e aggiornamenti del profilo
* Eventi di AEM Forms, ad esempio mancata corrispondenza delle versioni, provider di autorizzazioni e server delle directory non disponibili e modifiche alla configurazione del server

### Abilitare o disabilitare l’auditing degli eventi {#enable-or-disable-event-auditing}

Puoi abilitare e disabilitare l’auditing degli eventi correlati al server, ai documenti protetti da criteri, ai criteri, ai set di criteri e agli utenti. Quando abiliti l’auditing degli eventi, puoi scegliere di controllare tutti i possibili eventi oppure selezionare eventi specifici.

Quando abiliti l’auditing del server, puoi visualizzare gli eventi controllati nella pagina Eventi.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Impostazioni auditing e privacy.
1. Per configurare l’auditing del server, seleziona Sì o No in Abilita auditing del server.
1. Se hai selezionato Sì, in ciascuna categoria di eventi, procedi con una delle seguenti azioni per selezionare le opzioni da controllare:

   * Per controllare tutti gli eventi nella categoria, seleziona Tutti.
   * Per controllare solo alcuni eventi, deseleziona Tutti, quindi seleziona le caselle di controllo accanto agli eventi che desideri controllare.

     (Consulta [Opzioni di auditing degli eventi](configuring-client-server-options.md#event-auditing-options).)

1. Fai clic su OK.

>[!NOTE]
>
>Quando lavori con le pagine web, evita di utilizzare i pulsanti del browser, come ad esempio il pulsante Indietro, il pulsante di aggiornamento e la freccia Indietro o Avanti perché questa azione può causare problemi indesiderati durante l’acquisizione e la visualizzazione dei dati.

### Abilitare o disabilitare le notifiche sulla privacy {#enable-or-disable-privacy-notification}

Puoi abilitare e disabilitare un messaggio di notifica sulla privacy. Quando abiliti la notifica sulla privacy, viene visualizzato un messaggio non appena un destinatario tenta di aprire un documento protetto da criteri. La notifica informa l’utente che è in corso il controllo dell’utilizzo del documento. È anche possibile specificare un URL che l’utente può utilizzare per visualizzare la pagina dell’informativa sulla privacy, se disponibile.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Impostazioni auditing e privacy.
1. Per configurare la notifica sulla privacy, seleziona Sì o No in Abilita notifica sulla privacy.

   Se il criterio associato a un documento consente l’accesso anonimo dell’utente e l’opzione Abilita notifica sulla privacy è impostata su No, all’utente non verrà richiesto di effettuare l’accesso e il messaggio di notifica della privacy non verrà visualizzato.

   Se il criterio associato a un documento non consente l’accesso anonimo, l’utente visualizzerà il messaggio di notifica della privacy.

1. Se pertinente, digita l’URL della pagina dell’informativa sulla privacy nella casella URL privacy. Se lasci vuota la casella URL privacy, viene visualizzata la pagina relativa alla privacy disponibile all’indirizzo adobe.com.
1. Fai clic su OK.

>[!NOTE]
>
>La disabilitazione dell’informativa sulla privacy non disabilita il controllo dell’utilizzo dei documenti. Le azioni di controllo pronte all’uso e le azioni personalizzate supportate tramite il tracciamento sull’utilizzo esteso possono comunque raccogliere informazioni sul comportamento dell’utente.

### Importare un tipo di evento di audit personalizzato {#import-a-custom-audit-event-type}

Se utilizzi un’applicazione abilitata per la sicurezza dei documenti che supporta l’auditing di eventi aggiuntivi, ad esempio eventi specifici di un determinato tipo di file, un partner Adobe può fornirti eventi di auditing personalizzati che puoi importare in Protezione dei documenti. Utilizza questa funzione solo se un partner Adobe ti ha fornito tipi di evento personalizzati.

1. Nella Console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Gestione eventi.
1. Fai clic su Sfoglia per passare al file XML da importare, quindi fai clic su Importa.
1. Con l’importazione vengono sovrascritti i tipi di evento di auditing personalizzati esistenti sul server se vengono trovate combinazioni identiche di codice evento e spazio dei nomi.
1. Fai clic su OK.

### Eliminare un tipo di evento di auditing personalizzato {#delete-a-custom-audit-event-type}

1. Nella Console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Gestione eventi.
1. Seleziona la casella di controllo accanto al tipo di evento di audit personalizzato da eliminare e fai clic su Elimina.
1. Fai clic su OK.

### Esportare eventi di audit {#export-audit-events}

Puoi esportare gli eventi di audit in un file, per scopi di archiviazione.

1. Nella Console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Gestione eventi.
1. Modifica le impostazioni in Esporta eventi di audit secondo le tue esigenze. Puoi specificare:

   * l’età minima degli eventi di audit da esportare
   * Il numero massimo di eventi di audit da includere in un singolo file. Il server genera uno o più file in base a questo valore.
   * La cartella in cui verrà creato il file Questa cartella si trova nel server Forms. Se il percorso della cartella è relativo, è relativo alla directory principale del server applicazioni.
   * Il prefisso da utilizzare per i file degli eventi di audit
   * Il formato del file: un file con valori separati da virgole (CSV) compatibile con Microsoft Excel oppure un file XML.

1. Fai clic su Esporta. Per annullare l’esportazione, fai clic su Annulla esportazione. Se un altro utente ha pianificato un’esportazione, il pulsante Annulla esportazione non è disponibile fino al completamento di tale esportazione. Il pulsante Annulla esportazione non è disponibile se un altro utente ha pianificato un’esportazione. Per verificare se un’esportazione o un’eliminazione pianificata è stata avviata o completata, fai clic su Aggiorna.

### Eliminare gli eventi di audit {#delete-audit-events}

Puoi eliminare gli eventi di audit con data precedente a un numero di giorni specificato.

1. Nella Console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Gestione eventi.
1. In Elimina eventi di audit, specifica il numero di giorni nella casella Elimina eventi di audit precedenti a.
1. Fai clic su Elimina. Fai clic su Esporta. Per annullare l’eliminazione, fai clic su Annulla eliminazione. Se un altro utente ha pianificato un’eliminazione, il pulsante Annulla eliminazione non è disponibile fino al completamento dell’esportazione. Il pulsante Annulla eliminazione non è disponibile se un altro utente ha pianificato un’esportazione. Per verificare se un’eliminazione pianificata è stata avviata o completata, fai clic su Aggiorna.

### Opzioni di auditing degli eventi {#event-auditing-options}

Puoi abilitare e disabilitare l’auditing degli eventi e specificare i tipi di eventi per i quali eseguire l’auditing.

**Eventi dei documenti**

**Visualizza documento:** un destinatario visualizza un documento protetto tramite criteri.

**Chiudi documento:** un destinatario chiude un documento protetto tramite criteri.

**Stampa a bassa risoluzione:** un destinatario stampa un documento protetto tramite criteri con l’opzione a bassa risoluzione specificata.

**Stampa ad alta risoluzione:** un destinatario stampa un documento protetto tramite criteri con l’opzione ad alta risoluzione specificata.

**Aggiungi annotazione al documento:** un destinatario aggiunge un’annotazione a un documento PDF.

**Revoca documento:** un utente o un amministratore revoca l’accesso a un documento protetto tramite criteri.

**Annulla revoca del documento:** un utente o un amministratore ripristina l’accesso a un documento protetto tramite criteri.

**Compilazione modulo:** un destinatario immette informazioni in un documento PDF che è un modulo compilabile.

**Criterio rimosso:** un editore rimuove un criterio da un documento per revocare le protezioni di sicurezza.

**Cambia URL di revoca del documento:** una chiamata dal livello API modifica l’URL di revoca specificato per l’accesso a un nuovo documento che sostituisce un documento revocato.

**Modifica documento:** un destinatario modifica il contenuto di un documento protetto tramite criteri.

**Firma documento:** un destinatario firma un documento.

**Proteggi un nuovo documento:** un utente applica un criterio per proteggere un documento.

**Cambia criterio del documento:** un utente o un amministratore cambia il criterio associato a un documento.

**Pubblica documento come:** un nuovo documento con nome e licenza identici a un documento esistente è registrato nel server e i documenti non hanno una relazione padre-figlio. Questo evento può essere attivato utilizzando l’SDK AEM Forms.

**Itera documento:** un nuovo documento con nome e licenza identici a un documento esistente è registrato nel server e i documenti hanno una relazione principale-secondario. Questo evento può essere attivato utilizzando l’SDK AEM Forms.

**Eventi dei criteri**

**Criterio creato:** un utente o un amministratore crea un criterio.

**Criterio abilitato:** un amministratore rende disponibile un criterio.

**Criterio modificato:** un utente o un amministratore modifica un criterio.

**Criterio disabilitato:** un amministratore ha reso non disponibile un criterio.

**Criterio eliminato:** un utente o un amministratore elimina un criterio.

**Modifica proprietario criterio:** una chiamata dal livello API cambia il proprietario del criterio.

**Eventi utente**

**Utente eliminato:** un amministratore elimina un account utente.

**Registra utente invitato:** un utente esterno si registra tramite protezione documenti.

**Accesso riuscito:** tentativi di accesso riusciti da parte di amministratori o utenti.

**Utenti invitati:** la funzione protezione documenti invita un utente a registrarsi.

**Utenti attivati:** gli utenti esterni attivano i loro account utilizzando l’URL nell’e-mail di attivazione oppure un amministratore abilita un account.

**Modifica password:** gli utenti invitati modificano le proprie password o un amministratore reimposta una password per un utente locale.

**Accesso non riuscito:** tentativi di accesso non riusciti da parte di amministratori o utenti.

**Utenti disattivati:** un amministratore disabilita un account utente locale.

**Aggiornamento profilo:** gli utenti invitati modificano nome, nome organizzazione e password.

**Account bloccato:** un amministratore blocca un account.

**Eventi set di criteri**

**Set di criteri
creati:** un amministratore o un coordinatore di set di criteri crea un set di criteri.

**Set di criteri eliminato:** un amministratore o un coordinatore di set di criteri elimina un set di criteri.

**Set di criteri modificato:** un amministratore o un coordinatore di set di criteri modifica un set di criteri.

**Eventi di sistema**

**Sincronizzazione
directory completata:** queste informazioni non sono disponibili nella pagina Eventi. Le informazioni sulla sincronizzazione della directory corrente tra cui lo stato di sincronizzazione corrente e l’ora dell’ultima sincronizzazione, vengono visualizzate nella pagina Gestione dominio. Per accedere alla pagina Gestione dominio nella console di amministrazione, fare clic su Impostazioni > Gestione utente > Gestione dominio.

**Accesso offline abilitato client:** un utente ha abilitato l’accesso offline ai documenti protetti dal server nel computer dell’utente.

**Client sincronizzato** L’applicazione client deve sincronizzare le informazioni con il server per consentire l’accesso offline.

**Versione non corrispondente:** una versione dell’SDK AEM Forms non compatibile con il server ha tentato la connessione al server.

**Informazioni sulla sincronizzazione della directory:** Queste informazioni non sono disponibili nella pagina Eventi. Le informazioni sulla sincronizzazione della directory corrente tra cui lo stato di sincronizzazione corrente e l’ora dell’ultima sincronizzazione, vengono visualizzate nella pagina Gestione dominio. Per accedere alla pagina Gestione dominio nella console di amministrazione, fare clic su Impostazioni > Gestione utente > Gestione dominio.

**Modifica configurazione server:** modifiche alla configurazione del server eseguite tramite pagine Web o manualmente importando un file config.xml. Ciò include modifiche all’URL di base, timeout della sessione, blocchi di accesso, impostazioni della directory, cumulabilità delle chiavi, impostazioni del server SMTP per la registrazione esterna, configurazione delle filigrane, opzioni di visualizzazione e così via.

## Configurazione del tracciamento dell’utilizzo esteso {#configuring-extended-usage-tracking}

Protezione documenti consente di tenere traccia di vari eventi personalizzati che possono essere eseguiti su un documento protetto. È possibile abilitare il tracciamento degli eventi dal server di protezione documenti a livello globale o a livello di criterio In seguito, è possibile impostare un JavaScript per acquisire azioni specifiche eseguite all’interno del documento PDF protetto, ad fare clic su un pulsante o salvare il documento. Questi dati di utilizzo vengono inviati come file XML in coppie chiave-valore da utilizzare per ulteriori analisi. Gli utenti finali che accedono ai documenti protetti possono consentire o rifiutare tale tracciamento dall’applicazione client.

Se il tracciamento è abilitato a livello globale, è possibile sostituire questa impostazione a livello di criterio e disabilitarla per un criterio specifico. La sostituzione a livello di criterio non è possibile se il tracciamento è disabilitato a livello globale. L’elenco degli eventi tracciati viene inviato automaticamente al server quando il numero di eventi raggiunge i 25 o quando il documento viene chiuso. È anche possibile configurare lo script per inviare esplicitamente l’elenco degli eventi in base alle proprie esigenze. È possibile personalizzare il tracciamento degli eventi accedendo alle proprietà e ai metodi dell’oggetto di protezione documento.

Dopo aver abilitato il tracciamento, il tracciamento viene attivato per tutti i criteri creati successivamente come impostazione predefinita. I criteri creati prima dell’abilitazione del tracciamento sul server necessitano di aggiornamenti manuali.

### Abilitazione o disabilitazione del tracciamento di utilizzo esteso {#enable-or-disable-extended-usage-tracking}

Prima di iniziare, assicurati che l’auditing del server sia abilitato. Per ulteriori informazioni sull’auditing, consulta [Configurazione delle impostazioni dell’auditing e della privacy degli eventi](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Impostazioni auditing e privacy.
1. Per configurare il tracciamento dell’utilizzo esteso, in Abilita tracciamento seleziona Sì o No.
1. Per impostare la selezione della casella di controllo Consenti raccolta di dati di utilizzo dettagliati nella pagina di accesso, in Abilita tracciamento predefinito, seleziona Sì o No.

Per visualizzare gli eventi tracciati, puoi utilizzare il filtro Eventi documento nella pagina Eventi. Gli eventi tracciati con JavaScript sono etichettati come Tracciamento dettagliato dell’utilizzo. Per ulteriori informazioni sugli eventi, fai riferimento a [Eventi di monitoraggio](/help/forms/using/admin-help/monitoring-events.md#monitoring-events).

## Configurare le impostazioni di visualizzazione di protezione dei documenti {#configure-document-security-display-settings}

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Opzioni di visualizzazione.
1. Configura le impostazioni e fai clic su OK.

### Impostazioni di visualizzazione {#display-settings}

**Righe da visualizzare per i risultati della ricerca:** numero di righe visualizzate in una pagina durante l’esecuzione delle ricerche.

**Finestra di dialogo Personalizzazione per accesso client**

Queste impostazioni controllano il testo visualizzato nel prompt di accesso visualizzato quando un utente accede alla protezione dei documenti tramite un’applicazione client.

**Testo di benvenuto:** testo del messaggio di benvenuto, ad esempio “Accedi con il nome utente e la password”. Il testo del messaggio di benvenuto deve contenere informazioni su come accedere alla protezione dei documenti e come contattare un amministratore o un’altra persona di supporto designata nella tua organizzazione per ricevere assistenza. Ad esempio, gli utenti esterni potrebbero dover contattare un amministratore se dimenticano le password o hanno bisogno di assistenza per la registrazione o il processo di accesso. La lunghezza massima del testo di benvenuto è di 512 caratteri.

**Testo nome utente:** etichetta di testo per la casella del nome utente.

**Testo password:** etichetta di testo per la casella della password.

**Finestra di dialogo Personalizzazione per autenticazione certificato client**

Queste impostazioni controllano il testo visualizzato nella finestra di dialogo Autenticazione certificato.

**Scegli
Testo per tipo di autenticazione:** testo visualizzato per indirizzare un utente alla selezione di un tipo di autenticazione.

**Scegli testo per certificato:** testo visualizzato per indirizzare un utente alla selezione di un tipo di certificato.

**Testo di errore Certificati non disponibili:** messaggio contenente un massimo di 512 caratteri da visualizzare quando il certificato selezionato non è disponibile.

**Personalizzazione per la visualizzazione del certificato client**

**Visualizza solo emittenti di credenziali attendibili:** quando questa opzione è selezionata, l’applicazione client presenta all’utente solo i certificati di emittenti di credenziali configurati per l’attendibilità di AEM forms (consulta Gestione di certificati e credenziali). Se questa opzione non è selezionata, all’utente viene presentato un elenco di tutti i certificati presenti nel sistema dell’utente.

## Configurare le filigrane dinamiche {#configure-dynamic-watermarks}

L’utilizzo della protezione dei documenti consente di configurare le impostazioni predefinite per l’opzione della filigrana dinamica che è possibile applicare durante la creazione dei criteri. Una *filigrana* è un’immagine sovrapposta al testo nel documento. È utile per tenere traccia del contenuto di un documento e può aiutare a identificare l’utilizzo illegale del contenuto.

Una filigrana dinamica può essere costituita da testo composto da variabili definite, come ID utente e data e testo personalizzato, o da contenuti dinamici all’interno di un PDF. Puoi configurare filigrane con diversi elementi, ciascuno con il proprio posizionamento e la propria formattazione.

Le filigrane non sono modificabili e pertanto rappresentano un metodo più sicuro per garantire la riservatezza del contenuto del documento. Le filigrane dinamiche garantiscono inoltre che una filigrana mostri un numero sufficiente di informazioni specifiche per l’utente, in modo tale da fungere da deterrente per l’ulteriore distribuzione del documento.

La filigrana specificata da un criterio viene visualizzata nel documento protetto da criteri quando un destinatario visualizza o stampa il documento. A differenza delle filigrane permanenti, una filigrana dinamica non viene mai salvata nel documento, il che offre la flessibilità necessaria durante la distribuzione di un documento in un ambiente Intranet per garantire che l’applicazione di visualizzazione mostri l’identità dell’utente specifico. Inoltre, se un documento ha più utenti, l’utilizzo della filigrana dinamica consente di utilizzare un documento invece di più versioni, ciascuna con una filigrana diversa. La filigrana visualizzata riflette l’identità dell’utente corrente.

Le filigrane dinamiche sono diverse dalle filigrane che gli utenti possono aggiungere direttamente al documento in Acrobat. Il risultato è che un documento protetto da criteri può avere due filigrane.

### Considerazioni sulla creazione di filigrane {#considerations-when-creating-watermarks}

Puoi creare filigrane dinamiche con più elementi filigrana, ognuno dei quali è specificato come testo o PDF. Puoi includere fino a cinque elementi in una filigrana.

Se scegli una filigrana basata su testo, puoi specificare diversi elementi all’interno della filigrana con più voci di testo e specificare la posizione di ogni elemento. Assegna nomi significativi a questi elementi, ad esempio intestazione, piè di pagina e così via.

Se, ad esempio, desideri specificare come filigrana un testo diverso nell’intestazione, nel piè di pagina, nei margini e in tutto il documento, puoi creare diversi elementi filigrana e specificarne la posizione. Se desideri che l’ID utente dell’utente e la data corrente di accesso al documento vengano visualizzati nell’intestazione, il nome del criterio nel margine destro e un testo personalizzato “CONFIDENTIAL” in diagonale nel documento, è necessario definire elementi filigrana separati con testo come tipo e specificarne la formattazione e il posizionamento. Quando la filigrana viene applicata a un documento, tutti gli elementi della filigrana vengono applicati contemporaneamente al documento, nell’ordine in cui vengono aggiunti alla filigrana.

In genere, le filigrane basate su PDF vengono utilizzate per includere contenuti grafici come i logo o simboli speciali come il copyright o i marchi registrati.

È possibile modificare i limiti relativi al numero di elementi filigrana e alle dimensioni del file PDF modificando il file di configurazione della protezione dei documenti. Consulta [Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Quando configuri le filigrane, tieni presente quanto segue:

* Impossibile utilizzare un documento PDF protetto da password come elemento filigrana. Tuttavia, se la filigrana creata contiene altri elementi non protetti da password, questi verranno applicati come parte della filigrana.
* Puoi modificare la dimensione massima del file PDF da utilizzare come elemento filigrana. Tuttavia, i documenti PDF di grandi dimensioni utilizzati come filigrane compromettono le prestazioni durante la sincronizzazione offline dei documenti a cui sono applicate tali filigrane. Consulta [Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Come filigrana viene utilizzata solo la prima pagina del PDF selezionato. Verifica che le informazioni che desideri vengano visualizzate come filigrana siano disponibili nella prima pagina.
* Anche se puoi specificare il ridimensionamento del documento PDF, considera le dimensioni e il layout della pagina del file PDF se intendi utilizzarlo come filigrana nell’intestazione, nel piè di pagina o nei margini.
* Quando specifichi il nome del font, digitalo correttamente. AEM Forms sostituisce il tipo di carattere specificato qualora non fosse presente nel computer client in cui viene aperto il documento.
* Se come contenuto della filigrana è stato selezionato del testo, l’impostazione dell’opzione di ridimensionamento Adatta alla pagina non funziona per le pagine con larghezza diversa.
* Quando specifichi il posizionamento degli elementi della filigrana, accertati che non vi siano più elementi con lo stesso posizionamento. Se due elementi della filigrana hanno lo stesso posizionamento, ad esempio in centro, sul documento appariranno sovrapposti e nell’ordine in cui sono stati aggiunti alla filigrana.
* Quando specifichi la dimensione e il tipo di font, accertati che la lunghezza del testo sia completamente visibile all’interno della pagina. I contenuti di testo vengono riportati su nuove righe, in modo che il contenuto della filigrana che intendevi inserire nei margini possa sovrapporsi alle aree di contenuti delle pagine. Tuttavia, se il documento viene aperto in Acrobat 9, il testo al di là della riga singola viene troncato.

### Limitazioni delle filigrane dinamiche {#limitations-of-dynamic-watermarks}

Alcune applicazioni client potrebbero non supportare le filigrane dinamiche. Consulta la relativa Guida alle estensioni di Adobe Reader DC. Inoltre, tieni presente quanto segue sulle versioni di Acrobat che supportano le filigrane dinamiche:

* Impossibile utilizzare un documento PDF protetto da password come elemento filigrana.
* Le versioni di Acrobat e Adobe Reader precedenti alla 10 non supportano le seguenti funzioni per filigrane:

   * Filigrane in PDF
   * Più elementi nella filigrana (testo/PDF)
   * Opzioni avanzate come intervallo di pagine oppure opzioni di visualizzazione
   * Opzioni di formattazione del testo, come ad esempio il tipo di font, il nome del font e il colore specificato. Tuttavia, nelle versioni precedenti di Acrobat e Adobe Reader il contenuto di testo viene visualizzato con il carattere e il colore predefiniti.

* Acrobat 9.0 e versioni precedenti: Acrobat 9.0 e versioni precedenti non supportano i nomi dei criteri nelle filigrane dinamiche. Se Acrobat 9.0 apre un documento protetto da criteri con una filigrana dinamica che include il nome di un criterio e altri dati dinamici, la filigrana viene visualizzata senza il nome del criterio. Se la filigrana dinamica include solo il nome del criterio, Acrobat visualizza un messaggio di errore

### Aggiungere un modello di filigrana dinamico {#add-a-dynamic-watermark-template}

Puoi creare modelli di filigrana dinamici. Questi modelli rimangono disponibili come opzione di configurazione per i criteri creati da amministratori o utenti.

>[!NOTE]
>
>Le informazioni di configurazione delle filigrane dinamiche non vengono acquisite con le altre informazioni di configurazione quando esporti un file di configurazione.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Filigrane.
1. Fai clic su Nuovo.
1. Nel campo Nome, immetti un nome per la nuova filigrana.

   ***Nota **: non puoi utilizzare caratteri speciali nei nomi o nelle descrizioni di filigrane o elementi filigrana. Vedi le restrizioni elencate in [Considerazioni per la modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. Alla voce Nome, accanto al segno più, immetti un nome significativo per l’elemento della filigrana, ad esempio Intestazione, aggiungi una descrizione ed espandi il segno più per visualizzare le opzioni.
1. In Origine, seleziona il tipo di filigrana come testo o PDF.
1. Se hai selezionato l’opzione Testo, procedi come segue:

   * Seleziona i tipi di filigrana da includere. Selezionando Testo personalizzato, digita il testo da visualizzare per la filigrana nella casella adiacente. Tieni presente la lunghezza del testo che verrà visualizzato come filigrana.
   * Specifica le proprietà di formattazione del testo, come ad esempio il nome, la dimensione del font, il colore di primo piano e il colore di sfondo del testo della filigrana. Specifica il colore di primo piano e di sfondo come valori esadecimali.

     ***Nota **: se selezioni l’opzione di ridimensionamento Adatta alla pagina, la proprietà Dimensione font non sarà disponibile per la modifica.*

1. Se hai selezionato PDF per le opzioni relative alle filigrane avanzate, fai clic su **Sfoglia** accanto a Seleziona filigrana PDF per selezionare il documento PDF che desideri utilizzare come filigrana.

   ***Nota **: non utilizzare un documento PDF protetto da password. Se specifichi un PDF protetto da password come elemento filigrana, la filigrana non verrà applicata.*

1. In Usa come sfondo, seleziona Sì o No.

   **Nota**: attualmente la filigrana viene visualizzata in primo piano indipendentemente da questa impostazione.

1. Per controllare la posizione di visualizzazione della filigrana nel documento, configura le opzioni Allineamento verticale e Allineamento orizzontale.
1. Seleziona Adatta alla pagina oppure % e digita una percentuale nella casella. Il valore deve essere un numero intero, non una frazione. Per configurare le dimensioni della filigrana, puoi utilizzare un valore corrispondente alla percentuale della pagina oppure impostare la filigrana in modo che si adatti alle dimensioni della pagina.
1. Nella casella Rotazione digita i gradi di rotazione della filigrana. L’intervallo è compreso tra -180 e 180. Utilizza un valore negativo per ruotare la filigrana in senso antiorario. Il valore deve essere un numero intero, non una frazione.
1. Nella casella Opacità digita una percentuale. Utilizza un numero intero, non una frazione.
1. In Opzioni avanzate imposta quanto segue:

   **Opzioni intervallo pagine**

   Imposta l’intervallo di pagine in cui visualizzare la filigrana. Immetti 1 come pagina iniziale e -1 come pagina finale per contrassegnare tutte le pagine con la filigrana.

   **Opzioni di visualizzazione**

   Seleziona il punto in cui desideri visualizzare la filigrana. Per impostazione predefinita, la filigrana viene visualizzata sia nella copia digitale (online) che nella copia cartacea (stampa).

1. Fai clic su **Nuovo** in Elementi filigrana per aggiungere altri elementi filigrana, se necessario.
1. Fai clic su OK.

### Modificare un modello di filigrana dinamica {#edit-a-dynamic-watermark-template}

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Filigrane.
1. Fai clic sulla filigrana appropriata nell’elenco.
1. Nella pagina Modifica filigrane, modifica le impostazioni in base alle esigenze.
1. Fai clic su OK.

### Eliminare un modello di filigrana dinamica {#delete-a-dynamic-watermark-template}

Quando elimini una filigrana dinamica, questa non è più disponibile per essere aggiunta a un nuovo criterio. Tuttavia, la filigrana rimane nei criteri esistenti che la utilizzano attualmente e i documenti protetti dal criterio continuano a mostrare la filigrana dinamica fino a quando tu o un utente non modifichi il criterio che contiene la filigrana eliminata. Dopo la modifica del criterio, la filigrana non viene più applicata. Viene visualizzato un messaggio che indica che la filigrana esistente è stata eliminata dal criterio e che l’utente può selezionarne un’altra per sostituirla.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Filigrane.
1. Seleziona la casella di controllo accanto alla filigrana appropriata e fai clic su Elimina.
1. Fai clic su OK.

## Configurazione della registrazione degli utenti invitati {#configuring-invited-user-registration}

Gli utenti esterni all’organizzazione possono registrarsi con protezione dei documenti. Gli utenti invitati che si registrano e attivano i propri account possono accedere in protezione dei documenti utilizzando il proprio indirizzo e-mail e la password creata al momento della registrazione. Gli utenti invitati registrati possono utilizzare documenti protetti tramite criteri per i quali dispongono di autorizzazioni.

Quando gli utenti invitati vengono attivati, diventano utenti locali. Gli utenti locali possono essere configurati e gestiti utilizzando l’area Utenti invitati e locali. (Consulta [Gestione degli account utenti invitati e locali](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

A seconda delle funzionalità abilitate per gli utenti invitati, questi possono utilizzare anche le seguenti funzionalità di protezione dei documenti:

* Applicare i criteri ai documenti
* Creare i criteri
* Aggiungere utenti invitati ai criteri

La funzione Sicurezza dei documenti genera automaticamente un messaggio e-mail di invito alla registrazione quando si verificano gli eventi seguenti, salvo quando l’utente si trova già nella directory LDAP di origine o è stato invitato in precedenza alla registrazione:

* Un utente esistente aggiunge un utente invitato a un criterio
* Un amministratore aggiunge un account utente invitato nella pagina Registrazione utente invitato

L’e-mail di registrazione contiene un collegamento a una pagina di registrazione e informazioni su come registrarsi. Una volta che l’utente invitato si è registrato, la protezione dei documenti invia un’e-mail di attivazione con un collegamento a una pagina di attivazione. Dopo l’attivazione, l’account rimane valido fino a quando non lo disattivi o lo elimini.

Se abiliti la registrazione incorporata, dovrai specificare il server SMTP, i dettagli dell’e-mail di registrazione, le funzionalità di accesso e le informazioni dell’e-mail di reimpostazione della password una sola volta. Prima di abilitare la registrazione incorporata, accertati di aver creato un dominio locale in Gestione utenti e di aver assegnato il ruolo Invita utente di Sicurezza documenti agli utenti e ai gruppi appropriati dell’organizzazione. Consulta [Aggiungere un dominio locale](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) e [Creare e configurare ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles). Se non utilizzi la registrazione incorporata, devi disporre di un sistema di registrazione utenti personalizzato creato con l’SDK AEM Forms. Consulta la guida allo sviluppo di interfacce del provider di servizi (SPI) per AEM Forms in [Programmare con AEM Forms](/help/forms/developing/introducing-java-api-soap-quick.md). Se non utilizzi l’opzione di registrazione incorporata, ti consigliamo di configurare nell’e-mail di attivazione e nella schermata di accesso del client un messaggio che indica agli utenti come contattare l’amministratore per ottenere una nuova password o per altre informazioni.

**Abilitare e configurare la registrazione dell’utente invitato**

Per impostazione predefinita, il processo di registrazione dell’utente invitato è disabilitato. Per la protezione dei documenti, puoi abilitare e disabilitare la registrazione dell’utente invitato in base alle esigenze.

1. Nella Console di amministrazione, fai clic su Servizi > Protezione dei documenti > Configurazione > Registrazione dell’utente invitato.
1. Seleziona Abilita registrazione dell’utente invitato.
1. (Facoltativo) Aggiorna le impostazioni di registrazione dell’utente invitato come richiesto:

   * [Escludere o includere un utente o un gruppo esterno](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parametri del server e dell’account di registrazione](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Impostazioni e-mail di invito alla registrazione](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Impostazioni e-mail di attivazione](configuring-client-server-options.md#activation-email-settings)
   * [Configurare un messaggio e-mail di reimpostazione della password](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Facoltativo) In Registrazione incorporata, seleziona Sì per abilitare questa opzione. Se non abiliti la registrazione incorporata, dovrai impostare un sistema di registrazione utente personalizzato.
1. Fai clic su OK.

### Escludere o includere un utente o un gruppo esterno {#exclude-or-include-an-external-user-or-group}

Puoi limitare la registrazione con la protezione dei documenti per determinati utenti o gruppi di utenti esterni. Questa opzione è ad esempio utile per consentire l’accesso a un determinato gruppo di utenti, ma escludendo persone specifiche appartenenti al gruppo.

Le impostazioni seguenti si trovano nell’area Filtro di restrizione e-mail della pagina Registrazione utente invitato.

**Esclusione:** digita l’indirizzo e-mail di un utente o un gruppo da escludere. Per escludere più utenti o gruppi, digita ciascun indirizzo e-mail su una nuova riga. Per escludere tutti gli utenti che appartengono a un dominio specifico, digita un carattere jolly e il nome del dominio. Ad esempio, per escludere tutti gli utenti del dominio esempio.com, digita &amp;ast;.esempio.com.

**Inclusione:** digita l’indirizzo e-mail di un utente o un gruppo da includere. Per includere più utenti o gruppi, digita ogni indirizzo e-mail su una nuova riga. Per includere tutti gli utenti che appartengono a un dominio, specifico, digita un carattere jolly e il nome del dominio. Ad esempio, per includere tutti gli utenti del dominio esempio.com, digita &amp;ast;.esempio.com.

### Parametri del server e dell’account di registrazione {#server-and-registration-account-parameters}

Le impostazioni seguenti si trovano nell’area Impostazioni generali della pagina Registrazione dell’utente invitato.

**Host SMTP:** nome host del server SMTP. Il server SMTP gestisce gli avvisi e-mail in uscita per la registrazione e l’attivazione degli account utente invitato.

Se richiesto dall’host SMTP, digita le informazioni necessarie nelle caselle Nome account del server SMTP e Password dell’account del server SMTP per la connessione al server SMTP. Alcune organizzazioni non applicano questo requisito. Per ulteriori informazioni, contatta l’amministratore di sistema.

**Nome della classe socket del server SMTP:** nome della classe socket per il server SMTP. Ad esempio, javax.net.ssl.SSLSocketFactory.

**Tipo di contenuto e-mail:** tipo MIME accettato, ad esempio text/plain o text/html.

**Codifica e-mail:** formato di codifica da utilizzare per l’invio di messaggi e-mail. Puoi specificare qualsiasi codifica, ad esempio UTF-8 per Unicode o ISO-8859-1 per Latin. L’impostazione predefinita è UTF-8.

**Indirizzo e-mail di reindirizzamento:** quando specifichi un indirizzo e-mail per questa impostazione, eventuali nuovi inviti vengono inviati all’indirizzo fornito. Questa impostazione può essere utile a scopo di test.

**Usa domini locali:** seleziona il dominio appropriato. In una nuova installazione, assicurati di aver creato il dominio utilizzando Gestione utenti. Se si tratta di un aggiornamento, durante l’aggiornamento è stato creato un dominio utente esterno che può essere utilizzato.

**Usa SSL per il server SMTP:** seleziona questa opzione per abilitare le funzioni SSL per il server SMTP.

**Visualizza collegamento di accesso nella pagina di registrazione:** visualizza un collegamento di accesso nella pagina di registrazione visualizzata per gli utenti invitati.

**Per abilitare Transport Layer Security (TLS) per il server SMTP**

1. Apri la console di amministrazione.

   Il percorso predefinito della console di amministrazione è `https://<server>:<port>/adminui`.

1. Passa a Home > Servizi > Protezione dei documenti > Configurazione > Registrazione utente invitato.
1. In Registrazione utente invitato specifica tutte le impostazioni di configurazione e quindi fai clic su OK.

   >[!NOTE]
   >
   >Se utilizzi Microsoft Office 365 come server SMTP per l’invio degli inviti per la registrazione degli utenti, utilizza le impostazioni seguenti:
   >
   >**Host SMTP:** smtp.office365.com
   >**Porta:** 587

1. Successivamente, devi aggiornare config.xml. Consulta [Configurazione per abilitare SMTP per Transport Layer Security (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Se apporti modifiche alle opzioni di Registrazione utente invitato, il file config.xml viene sovrascritto e TLS viene disattivato. Se sovrascrivi le modifiche, devi eseguire il passaggio precedente per riattivare il supporto TLS per la Registrazione utente invitato.

### Impostazioni e-mail di invito alla registrazione {#registration-invitation-email-settings}

Protezione documenti invia automaticamente un messaggio e-mail di invito alla registrazione quando crei un account utente invitato o quando un utente esistente aggiunge un destinatario esterno che non si è registrato o che è stato invitato in precedenza a registrarsi a un criterio. L’e-mail include un collegamento che il destinatario può utilizzare per accedere alla pagina di registrazione e inserire le informazioni dell’account personale, inclusi nome utente e password. La password può essere costituita da una qualsiasi combinazione di otto caratteri.

Quando il destinatario attiva l’account, l’utente diventa un utente locale.

Le impostazioni seguenti si trovano nell’area Configurazione e-mail di invito della pagina Registrazione utente invitato.

**Da:** l’indirizzo e-mail da cui viene inviato l’invito. Il formato predefinito dell’indirizzo e-mail Da è postmaster@[your_installation_domain].com.

**Oggetto:** oggetto predefinito per il messaggio e-mail di invito.

**Timeout:** il numero di giorni dopo i quali scade l’invito di registrazione se l’utente esterno non si registra. Il valore predefinito è 30 giorni.

**Messaggio:** il testo visualizzato nel corpo del messaggio che invita l’utente a registrarsi.

### Impostazioni e-mail di attivazione {#activation-email-settings}

Dopo aver invitato gli utenti a registrarsi, la protezione dei documenti invia un’e-mail di attivazione.  L’e-mail di attivazione include un collegamento alla pagina di attivazione dell’account in cui gli utenti possono attivare il proprio account. Quando gli account vengono attivati, gli utenti possono accedere alla protezione dei documenti utilizzando il proprio indirizzo e-mail e la password creati al momento della registrazione.

Quando il destinatario attiva l’account utente, l’utente diventa un utente locale.

Le impostazioni seguenti si trovano nell’area Configurazione e-mail di attivazione della pagina Registrazione utente invitato.

>[!NOTE]
>
>Si consiglia inoltre di configurare un messaggio nella schermata di accesso per indicare agli utenti esterni come contattare il proprio amministratore per ottenere una nuova password o altre informazioni.

**Da:** l’indirizzo e-mail da cui viene inviata l’e-mail di attivazione. Questo indirizzo e-mail riceve le notifiche di errore di consegna dall’host di posta elettronica dell’utente che effettua la registrazione, nonché eventuali messaggi inviati dal destinatario in risposta all’e-mail di registrazione. Il formato predefinito dell’indirizzo di posta elettronica Da è postmaster@[your_installation_domain].com.

**Oggetto:** oggetto predefinito per il messaggio e-mail di attivazione.

**Timeout:** il numero di giorni dopo i quali l’invito di attivazione scade se l’utente non attiva l’account. Il valore predefinito è 30 giorni.

**Messaggio:** il testo visualizzato nel corpo del messaggio indica che l’account utente del destinatario deve essere attivato. È inoltre possibile includere informazioni su come contattare un amministratore per ottenere una nuova password.

### Configurare un messaggio e-mail di reimpostazione della password {#configure-a-password-reset-email}

Se occorre reimpostare la password di un utente invitato, viene generata un’e-mail di conferma che invita l’utente a scegliere una nuova password. Non è possibile individuare la password di un utente; se l’utente la dimentica, è necessario reimpostarla.

Le impostazioni seguenti si trovano nell’area E-mail reimpostazione password della pagina Registrazione utente invitato.

**Da:** l’indirizzo e-mail da cui viene inviata l’e-mail per reimpostare la password. Il formato predefinito dell’indirizzo e-mail Da è postmaster@[your_installation_domain].com.

**Oggetto:** oggetto predefinito per il messaggio e-mail di reimpostazione.

**Messaggio:** testo visualizzato nel corpo del messaggio che indica che la password utente esterna del destinatario è stata reimpostata.

## Consentire a utenti e gruppi di creare criteri {#enable-users-and-groups-to-create-policies}

Nella pagina Configurazione è presente un collegamento alla pagina Criteri personali in cui puoi specificare quali utenti finali possono creare i criteri e quali utenti e gruppi sono visibili nei risultati della ricerca. Nella pagina Criteri personali sono presenti due schede:

**Scheda Crea criteri:** utilizzala per configurare le autorizzazioni utente per la creazione di criteri personalizzati.

**Scheda Utenti e gruppi visibili:** utilizzala per controllare quali utenti e gruppi sono visibili nei risultati della ricerca utente. Il super utente o l’amministratore del set di criteri deve selezionare e aggiungere i domini, creati in Gestione utenti, all’utente e al gruppo visibili per ogni set di criteri. Questo elenco è visibile al coordinatore del set di criteri e viene utilizzato per definire i limiti sui domini che il coordinatore del set di criteri può esplorare quando sceglie gli utenti da aggiungere ai criteri.

Prima di concedere agli utenti l’autorizzazione per la creazione di criteri personalizzati, è opportuno considerare il livello di accesso o di controllo che desideri assegnare ai singoli utenti. Inoltre, considera il livello di esposizione desiderato per utenti e gruppi quando li rendi visibili nelle ricerche.

### Specificare gli utenti e i gruppi che possono creare criteri {#specify-users-and-groups-who-can-create-policies}

In qualità di amministratore, specifica quali utenti e gruppi possono creare criteri personalizzati. Questa autorizzazione può essere impostata a livello di utente e di gruppo. La funzionalità di ricerca consente di cercare utenti e gruppi nel database della Gestione utenti.

1. Nella console di amministrazione fai clic su Servizi > Protezione dei documenti > Configurazione > Criteri personali.
1. Nella pagina Criteri personali fai clic sulla scheda Crea criteri, quindi su Aggiungi utenti e gruppi.
1. Nella casella Trova digita il nome utente o l’indirizzo e-mail dell’utente o del gruppo che stai cercando. Se non disponi di queste informazioni, lascia vuota la casella. Puoi anche digitare un nome o un indirizzo e-mail parziale, ad esempio se conosci solo le prime due lettere di un nome utente.
1. Nell’elenco Utilizzo seleziona i parametri di ricerca Nome o E-mail.
1. Nell’elenco Tipo seleziona Gruppo o Utente per restringere la ricerca.
1. Nell’elenco In seleziona il dominio da cercare. Se non conosci il dominio dell’utente o del gruppo, seleziona Tutti i domini.
1. Nell’elenco Visualizza specifica il numero di risultati di ricerca da visualizzare per pagina, quindi fai clic su Trova.
1. Per aggiungere utenti e gruppi a Criteri personali, seleziona la casella di controllo relativa a ogni utente e gruppo da aggiungere.
1. Fai clic su Aggiungi, quindi su OK.

Gli utenti e i gruppi selezionati ora dispongono delle autorizzazioni per creare criteri personalizzati.

### Rimuovere l’autorizzazione per creare criteri personalizzati da un utente o un gruppo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Nella pagina di Protezione dei documenti, fai clic su Configurazione > Criteri personali.
1. Nella pagina Criteri personali fai clic sulla scheda Crea criteri. Vengono visualizzati gli utenti e i gruppi con le autorizzazioni per creare criteri personalizzati.
1. Seleziona la casella di controllo accanto agli utenti e ai gruppi a cui rimuovere questa autorizzazione.
1. Fai clic su Elimina, quindi su OK.

### Specificare utenti e gruppi visibili nelle ricerche {#specify-users-and-groups-that-are-visible-in-searches}

Quando gli utenti gestiscono i propri criteri personalizzati, possono cercare utenti e gruppi da aggiungere ai propri criteri. Specifica i domini dai quali utenti e gruppi sono visibili in queste ricerche.

1. Nella pagina di Protezione dei documenti, fai clic su Configurazione > Criteri personali.
1. Nella pagina Criteri personali fai clic sulla scheda Utenti e gruppi visibili.
1. Per rendere visibili gli utenti e i gruppi di un dominio, fai clic su Aggiungi domini, seleziona i domini e fai clic su Aggiungi. Per rimuovere un dominio, seleziona la casella di controllo accanto al nome del dominio e fai clic su Elimina.

## Modifica manuale del file di configurazione per la protezione dei documenti {#manually-editing-the-document-security-configuration-file}

Puoi importare ed esportare le informazioni di configurazione memorizzate nel database della protezione dei documenti. Ad esempio, potresti voler creare una copia di backup delle informazioni di configurazione quando passi da un ambiente di staging a uno di produzione oppure modificare le opzioni avanzate che possono essere configurate solo per la modifica di questo file.

Utilizzando il file di configurazione, puoi apportare le seguenti modifiche:

[Visualizzare le autorizzazioni CATIA durante la creazione e la modifica dei criteri](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Specificare un periodo di timeout per la sincronizzazione offline](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Rifiuto dei servizi di protezione dei documenti per applicazioni specifiche](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Disabilitazione dei collegamenti esterni](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>L’importazione del file di configurazione riconfigura il sistema in base alle informazioni contenute nel file. Le eccezioni sono la configurazione della filigrana dinamica e le informazioni sugli eventi personalizzati, che non vengono salvate con il file di configurazione esportato. Configura queste informazioni manualmente nel nuovo sistema. Solo un amministratore di sistema o un consulente di servizi professionali che ha familiarità con la protezione dei documenti e con XML può modificare il contenuto di un file di configurazione, ad esempio per riconfigurare un’impostazione danneggiata o per ottimizzare i parametri per un particolare scenario di distribuzione aziendale.

**Esportare un file di configurazione**

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti 11 > Configurazione > Configurazione manuale.
1. Fai clic su Esporta e salva il file di configurazione in un’altra posizione. Il nome file predefinito è config.xml.
1. Fai clic su OK.
1. Prima di modificare il file di configurazione, esegui una copia di backup nel caso sia necessario ripristinarlo.

**Importare un file di configurazione**

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti 11 > Configurazione > Configurazione manuale.
1. Fai clic su Sfoglia per passare al file di configurazione e quindi fai clic su Importa. Non puoi digitare il percorso direttamente nella casella Nome file.
1. Fai clic su OK.

### Specificare un periodo di timeout per la sincronizzazione offline {#specify-a-timeout-period-for-offline-synchronization}

La protezione dei documenti consente agli utenti di aprire e utilizzare un documento protetto quando non sono connessi al server della protezione dei documenti. L’applicazione client dell’utente deve sincronizzarsi regolarmente con il server per mantenere i documenti validi per l’utilizzo offline. La prima volta che gli utenti aprono un documento protetto, viene richiesto loro se il computer deve essere autorizzato a eseguire la sincronizzazione periodica del client.

Per impostazione predefinita, la sincronizzazione viene eseguita automaticamente ogni quattro ore e in base alle esigenze quando un utente è connesso al server di protezione dei documenti. Se il periodo offline di un documento scade mentre l’utente è offline, l’utente deve riconnettersi al server per consentire all’applicazione client di eseguire la sincronizzazione con il server.

Nel file di configurazione di protezione dei documenti, puoi specificare la frequenza predefinita della sincronizzazione automatica in background. Questa impostazione funge da periodo di timeout predefinito per le applicazioni client, a meno che il client non imposti esplicitamente il proprio valore di timeout.

1. Esporta il file di configurazione di protezione documenti. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `PolicyServer`. Sotto tale nodo, individua il nodo `ServerSettings`.
1. Nel nodo `ServerSettings`, aggiungi la voce seguente, quindi salva il file:

   `<entry key="BackgroundSyncFrequency" value="`*tempo* `"/>`

   dove *tempo* è il numero di secondi tra le sincronizzazioni in background automatiche. Se hai inviato questo valore a `0`, la sincronizzazione si verifica sempre. Il valore predefinito è `14400` secondi (ogni quattro ore).

1. Importa file di configurazione. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Rifiuto dei servizi di protezione dei documenti per applicazioni specifiche {#denying-document-security-services-for-specific-applications}

Puoi configurare la protezione dei documenti in modo da rifiutare i servizi alle applicazioni che soddisfano criteri specifici. I criteri possono specificare un singolo attributo, ad esempio il nome di una piattaforma, oppure più insiemi di attributi. Questa funzione consente di controllare le richieste che la protezione dei documenti deve gestire. Di seguito sono elencate alcune applicazioni di questa funzione:

* **Protezione dei ricavi:** puoi rifiutare l’accesso a qualsiasi applicazione client che non supporta le convenzioni dei ricavi.
* **Compatibilità dell’applicazione:** alcune applicazioni potrebbero non essere compatibili con i criteri o il comportamento del server di protezione dei documenti.

Quando le applicazioni client tentano di stabilire un collegamento con la protezione dei documenti, forniscono informazioni su applicazione, versione e piattaforma. La protezione dei documenti confronta queste informazioni con le impostazioni di rifiuto ottenute dal file di configurazione della protezione dei documenti.

Le impostazioni di Rifiuto possono contenere diversi set di condizioni di rifiuto. Se tutti gli attributi di un qualunque set corrispondono, all’applicazione richiedente viene negato l’accesso ai servizi di protezione dei documenti.

La funzione di rifiuto del servizio richiede che le applicazioni client utilizzino la versione 8.2 o successiva di C++ Client SDK per la protezione dei documenti. I seguenti prodotti Adobe forniscono informazioni sul prodotto quando si richiedono i servizi di protezione dei documenti:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard e versioni successive
* Adobe Reader 9.0 e versioni successive
* Estensioni Acrobat Reader DC per Microsoft Office 8.2 e versioni successive

Le applicazioni client utilizzano il client API di SDK C++ Client di Protezione documenti per richiedere tali servizi. Le richieste del client API includono informazioni sulla piattaforma e sulla versione di SDK (precompilate nel client API) e informazioni sul prodotto ottenute dall’applicazione client.

Le applicazioni client o i plug-in forniscono informazioni sui prodotti nell’implementazione di una funzione di callback. L’applicazione fornisce le seguenti informazioni:

* Nome integratore
* Versione integratore
* Famiglia applicazione
* Nome applicazione
* Versione applicazione

Se non ci sono informazioni applicabili, l’applicazione client lascia vuoto il campo corrispondente.

Diverse applicazioni Adobe includono informazioni sul prodotto quando richiedono servizi di protezione dei documenti, tra cui le estensioni Acrobat, Adobe Reader e Estensioni di Adobe Reader DC per Microsoft Office.

**Acrobat e Adobe Reader**

Quando Acrobat o Adobe Reader richiedono un servizio di protezione dei documenti, fornisce le seguenti informazioni di prodotto:

* **Integratore:** Adobe Systems, Inc.
* **Versione integratore:** 1.0
* **Famiglia di applicazioni:** Acrobat
* **Nome applicazione:** Acrobat
* **Versione applicazione:** 9.0.0

**Estensioni di Adobe Reader DC per Microsoft Office**

Estensioni di Adobe Reader DC per Microsoft Office è un plug-in utilizzato con i prodotti Microsoft Office: Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Quando richiede un servizio, fornisce le seguenti informazioni:

* **Integratore:** Adobe Systems Incorporated
* **Versione integratore:** 8.2
* **Famiglia di applicazioni:** estensioni di Adobe Reader DC per Microsoft Office
* **Nome applicazione:** Microsoft Word, Microsoft Excel o Microsoft PowerPoint
* **Versione applicazione:** 2003 o 2007

**Configura la protezione dei documenti per negare i servizi ad applicazioni specifiche**

1. Esporta il file di configurazione di protezione documenti. (Consulta [Modifica manuale del file di configurazione di Protezione documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Aprire il file di configurazione in un editor e individua il nodo `PolicyServer`. Aggiungi un nodo `ClientVersionRules` come dipendente immediato del nodo `PolicyServer`, se non ne esiste uno:

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

   `SDKPlatforms` specifica la piattaforma che ospita l’applicazione client. I valori possibili sono:

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` specifica la versione del client API C++ di Protezione documenti utilizzata dall’applicazione client. Ad esempio, `"8.2"`.

   `APPFamilies` è definito dal client API.

   `AppName` specifica il nome dell’applicazione client. Le virgole vengono utilizzate come separatori dei nomi. Per includere una virgola in un nome, aggiungi un carattere di escape con una barra rovesciata (\). Per esempio: *“Adobe Systems\, Inc.”*.

   `AppVersions` specifica la versione dell’applicazione client.

   `Integrators` specifica il nome della società o del gruppo che ha sviluppato il plug-in o l’applicazione integrata.

   `IntegratorVersions` è la versione del plug-in o dell’applicazione integrata.

1. Per ogni set aggiuntivo di dati non consentiti, aggiungi un altro elemento *MyEntryName*.
1. Salva il file di configurazione.
1. Importa file di configurazione. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**Esempi**

In questo esempio, a tutti i client Windows viene negato l’accesso.

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

In questo esempio, a Applicazione personale versione 3.0 e Altra applicazione personale versione 2.0 viene negato l’accesso. Lo stesso URL di informazioni sui rifiuti viene utilizzato indipendentemente dal motivo del rifiuto.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
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

In questo esempio, tutte le richieste provenienti da un’installazione di Microsoft PowerPoint 2007 o Microsoft PowerPoint 2010 di estensioni Acrobat Reader DC per Microsoft Office vengono rifiutate.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
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

### Modificare i parametri di configurazione della filigrana {#change-the-watermark-configuration-parameters}

Per impostazione predefinita, puoi specificare un massimo di cinque elementi in una filigrana. Inoltre, la dimensione massima del file del documento PDF che desideri utilizzare come filigrana è limitata a 100 KB. Puoi modificare questi parametri nel file config.xml.

***Nota **: devi modificare questi parametri con cautela.*

1. Esporta il file di configurazione di protezione documenti. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `ServerSettings`.
1. Nel nodo `ServerSettings` aggiungi le voci seguenti e quindi salva il file: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   La prima voce, *dimensione masisma del file*, corrisponde alla dimensione massima del file (in KB) consentita per un elemento filigrana del PDF. Il valore predefinito è 100 KB.

   La seconda voce, *numero massimo di elementi*, rappresenta il numero massimo di elementi consentito in una filigrana. Il valore predefinito è 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importa file di configurazione. (Consulta [Modifica manuale del file di configurazione di protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Disabilitazione dei collegamenti esterni {#disabling-external-links}

Molti utenti della protezione dei documenti non hanno accesso a collegamenti esterni come **www.adobe.com** mentre utilizzano le interfacce utente delle gestione dei diritti:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Le seguenti modifiche apportate al file config.xml disabilitano tutti i collegamenti esterni dalle interfacce utente della gestione dei diritti.

1. Esporta il file di configurazione di protezione documenti. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `DisplaySettings`.
1. Per disabilitare tutti i collegamenti esterni, nel nodo `DisplaySettings` aggiungi la voce seguente e quindi salva il file: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importa file di configurazione. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configurazione per abilitare SMTP per Transport Layer Security (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Le seguenti modifiche apportate al file config.xml abilitano il supporto per TLS per la funzione di registrazione degli utenti invitati.

1. Esporta il file di configurazione di protezione documenti. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo `DisplaySettings`.
1. Individua il seguente codice: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Imposta il valore della chiave `SmtpUseTls` nel nodo `ExternalUser` su **vero**.
1. Imposta il valore della chiave `SmtpUseSsl` nel nodo `ExternalUser` su **falso**.
1. Salva `config.xml`.
1. Importa file di configurazione. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Disabilitare gli endpoint di SOAP per documenti della funzione di protezione dei documenti {#disable-soap-endpoints-for-document-security-documents}

Di seguito sono riportate le modifiche apportate al file config.xml per disabilitare gli endpoint di SOAP per i documenti della funzione di protezione dei documenti.

1. Esporta il file di configurazione di protezione documenti. (Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo seguente: `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. Nel nodo DRM, individua il nodo `entry`:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Per disabilitare gli endpoint SOAP per i documenti di Protezione dei documenti, imposta l’attributo del valore su **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Salva `config.xml`.
1. Importa file di configurazione. Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).

### Maggiore scalabilità del server di protezione dei documenti {#increasingscalability}

Per impostazione predefinita, durante la sincronizzazione di un documento per l’utilizzo offline, insieme alle informazioni per il documento corrente, i client di protezione dei documenti recuperano le informazioni relative a criteri, filigrane, licenze e aggiornamenti di revoca per tutti gli altri documenti a cui l’utente ha accesso. Se questi aggiornamenti e informazioni non vengono sincronizzati con il client, è possibile che un documento aperto in modalità offline venga comunque aperto con informazioni precedenti relative a criteri, filigrana e revoche.

Puoi aumentare la scalabilità del server di protezione dei documenti limitando le informazioni inviate al client. La riduzione della quantità di informazioni inviate al client consente di migliorare la scalabilità, ridurre i tempi di risposta e migliorare le prestazioni del server. Per migliorare la scalabilità, esegui i passaggi seguenti:

1. Esporta il file di configurazione di protezione documenti. Consulta [Modifica manuale del file di configurazione della protezione dei documenti](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).
1. Apri il file di configurazione in un editor e individua il nodo ServerSettings.
1. Nel nodo ServerSettings, imposta il valore della proprietà `DisableGlobalOfflineSynchronizationData` su `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Se impostato su true, il server della protezione dei documenti invia informazioni solo per il documento corrente e le informazioni per gli altri documenti (gli altri documenti a cui un utente ha accesso) non vengono inviate al client.

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore della chiave `DisableGlobalOfflineSynchronizationData` è impostato su `false`.

1. Salva e importa il file di configurazione. Consulta [Modifica manuale del file di configurazione della protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).
