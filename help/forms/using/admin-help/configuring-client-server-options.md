---
title: Configurazione delle opzioni client e server
seo-title: Configurazione delle opzioni client e server
description: Scoprite come configurare le varie opzioni client e server, ad esempio le impostazioni di configurazione del server, i ruoli di protezione dei documenti e il controllo degli eventi.
seo-description: Scoprite come configurare le varie opzioni client e server, ad esempio le impostazioni di configurazione del server, i ruoli di protezione dei documenti e il controllo degli eventi.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '10273'
ht-degree: 0%

---


# Configurare il server di protezione dei documenti {#configure-the-document-security-server}

1. Nella console di amministrazione, fate clic su Servizi > Protezione documento > Configurazione > Configurazione server.
1. Configurare le impostazioni e fare clic su OK.

## Impostazioni di configurazione del server {#server-configuration-settings}

**URL di base:** L&#39;URL di protezione del documento di base, contenente il nome del server e la porta. Le informazioni aggiunte alla base creano gli URL di connessione. Ad esempio, /edc/Main.do viene aggiunto per accedere alle pagine Web. Gli utenti rispondono anche agli inviti di registrazione degli utenti esterni tramite questo URL.

Se si utilizza IPv6, immettere l&#39;URL di base come nome del computer o nome DNS. Se si utilizza un indirizzo IP numerico, Acrobat non riuscirà ad aprire i file protetti tramite criterio. Inoltre, utilizzate l&#39;URL HTTP sicuro (HTTPS) per il vostro server.

>[!NOTE]
>
>L&#39;URL di base è incorporato nei file protetti tramite criterio. Le applicazioni client utilizzano l&#39;URL di base per la connessione al server. I file protetti continueranno a contenere l&#39;URL di base, anche se successivamente verranno modificati. Se modificate l&#39;URL di base, le informazioni di configurazione dovranno essere aggiornate per tutti i client che si connettono.

**Periodo di leasing offline predefinito:** Il tempo predefinito entro il quale un utente può utilizzare un documento protetto offline. Questa impostazione determina il valore iniziale dell&#39;impostazione del periodo di tempo consentito per l&#39;utilizzo non in linea automatico quando si crea un criterio. Consultate Creazione e modifica dei criteri. Alla scadenza del periodo consentito, il destinatario deve sincronizzare di nuovo il documento per continuare a utilizzarlo.

Per informazioni sul funzionamento del lease e della sincronizzazione offline, consultate [Primer on configuring offline lease and sync](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html)(Introduzione alla configurazione del leasing e della sincronizzazione offline).

**Periodo di sincronizzazione offline predefinito:** La durata massima di utilizzo offline di un documento da parte di un&#39;applicazione di protezione iniziale.

**Timeout sessione client:** Il tempo, in minuti, al termine del quale la protezione dei documenti si disconnette se un utente che ha eseguito l&#39;accesso tramite un&#39;applicazione client non interagisce con la protezione dei documenti.

**Consenti accesso utenti anonimi:** Selezionate questa opzione per abilitare la possibilità di creare criteri condivisi e personali che consentano agli utenti anonimi di aprire documenti protetti tramite criterio. Gli utenti che non dispongono di account possono accedere al documento, ma non possono accedere a Document Security o utilizzare altri documenti protetti tramite criterio.

**Disattiva accesso ai client della versione 7:** Specifica se gli utenti possono utilizzare Acrobat o Reader 7.0 per connettersi al server. Quando questa opzione è selezionata, gli utenti devono utilizzare Acrobat o Reader 8.0 e versioni successive per completare le operazioni di protezione dei documenti sui documenti PDF. Se i criteri richiedono l&#39;esecuzione in modalità certificata di Acrobat o Reader 8.0 e versioni successive all&#39;apertura dei documenti protetti tramite criterio, è consigliabile disattivare l&#39;accesso ad Acrobat o Reader 7. Consultate Specificare le autorizzazioni del documento per utenti e gruppi.

**Consenti accesso offline per documento** Selezionate questa opzione per specificare l&#39;accesso offline per documento. Se questa impostazione è abilitata, l&#39;utente avrà accesso non in linea solo ai documenti che l&#39;utente ha aperto online almeno una volta.

**Consenti autenticazione password nome utente:** Selezionate questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione tramite nome utente/password durante la connessione al server.

**Consenti autenticazione Kerberos:** Selezionare questa opzione per abilitare l&#39;autenticazione Kerberos per le applicazioni client durante la connessione al server.

**Consenti autenticazione certificato client:** Selezionate questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione basata sui certificati durante la connessione al server.

**Consenti autenticazione** estesa Selezionate questa opzione per abilitare l&#39;autenticazione estesa e immettete l&#39;URL di destinazione autenticazione estesa.

Selezionando questa opzione, le applicazioni client possono utilizzare l&#39;autenticazione estesa. L&#39;autenticazione estesa fornisce processi di autenticazione personalizzati e diverse opzioni di autenticazione configurate sul server moduli AEM. Ad esempio, ora gli utenti possono utilizzare l&#39;autenticazione basata su SAML invece del nome utente/password dei moduli AEM, da Acrobat e Reader Client. Per impostazione predefinita, l’URL di destinazione contiene *localhost* come nome del server. Sostituite il nome del server con un nome host completo. Il nome host nell&#39;URL di destinazione viene popolato automaticamente dall&#39;URL di base, se l&#39;autenticazione estesa non è ancora abilitata. Consultate [Aggiunta del provider](configuring-client-server-options.md#add-the-extended-authentication-provider)di autenticazione estesa.

***nota **: L&#39;autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successiva.*

**Larghezza di controllo HTML preferita per l&#39;autenticazione** estesa Consente di specificare la larghezza della finestra di dialogo di autenticazione estesa che si apre in Acrobat per l&#39;immissione delle credenziali utente.

**Altezza di controllo HTML preferita per l&#39;autenticazione** estesa Consente di specificare l&#39;altezza della finestra di dialogo di autenticazione estesa che si apre in Acrobat per l&#39;immissione delle credenziali utente.

***nota **: I limiti di larghezza e altezza per questa finestra di dialogo sono i seguenti:*Larghezza: Minimo = 400, massimo = 900

Altezza: Minimo = 450; max = 800

**Abilita cache credenziali client:** Selezionate questa opzione per consentire agli utenti di memorizzare nella cache le credenziali (nome utente e password). Quando le credenziali degli utenti vengono memorizzate nella cache, non devono immettere le credenziali ogni volta che aprono un documento o quando fanno clic sul pulsante Aggiorna nella pagina Gestisci criteri di protezione di Adobe Acrobat. È possibile specificare il numero di giorni prima che gli utenti debbano nuovamente fornire le proprie credenziali. Impostando il numero di giorni su 0, le credenziali possono essere memorizzate nella cache a tempo indeterminato.

## Configurazione di utenti e amministratori per la protezione dei documenti {#configuring-document-security-users-and-administrators}

### Assegnazione di ruoli di protezione dei documenti agli amministratori {#assigning-document-security-roles-to-administrators}

L&#39;ambiente dei moduli AEM contiene uno o più utenti amministratori che dispongono dei privilegi appropriati per la creazione di utenti e gruppi. Se l&#39;organizzazione utilizza la protezione dei documenti, almeno un amministratore deve anche avere il privilegio di gestire gli utenti invitati e locali.

Per accedere alla console di amministrazione, gli amministratori devono anche avere il ruolo utente della console di amministrazione. Consultate [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).

### Configurazione di utenti e gruppi visibili {#configuring-visible-users-and-groups}

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti tramite criterio, un amministratore superiore o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati in Gestione utente) all&#39;elenco di utenti e gruppi visibile per ciascun set di criteri.

L&#39;elenco di utenti e gruppi visibile è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l&#39;utente finale può esplorare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà utenti o gruppi da aggiungere al criterio. Per ciascun set di criteri può essere presente più di un coordinatore set di criteri.

1. Dopo aver installato e configurato l&#39;ambiente dei moduli AEM con la protezione dei documenti, configura tutti i domini appropriati in Gestione utente. <!-- Fix broken link (See Setting up and managing domains) -->

   ***nota **: È necessario creare i domini prima di poter creare qualsiasi criterio.*

1. Nella console di amministrazione, fare clic su Servizi > Gestione documenti > Criteri, quindi fare clic sulla scheda Set criteri.
1. Selezionate Set di criteri globale, quindi fate clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come necessario.
1. Passa a Servizi > Protezione documento > Configurazione > Criteri personali e fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come necessario.

## Aggiunta del provider di autenticazione estesa {#add-the-extended-authentication-provider}

I moduli AEM forniscono un esempio di configurazione personalizzabile per il proprio ambiente. Effettuate le seguenti operazioni:

>[!NOTE]
>
>L&#39;autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successiva.

1. Ottenere il file WAR di esempio distribuirlo. Consultate la guida all’installazione appropriata per il server delle applicazioni.
1. Verificare che il server dei moduli disponga di un nome completo invece degli indirizzi IP come URL di base e che sia un URL HTTPS. Consultate Impostazioni [di configurazione del](configuring-client-server-options.md#server-configuration-settings)server.
1. Abilitare l&#39;autenticazione estesa dalla pagina Configurazione server. Consultate Impostazioni [di configurazione del](configuring-client-server-options.md#server-configuration-settings)server.
1. Aggiungete gli URL di reindirizzamento SSO richiesti nel file di configurazione Gestione utente. Consultate [Aggiungere URL di reindirizzamento SSO per l&#39;autenticazione](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication)estesa.

### Aggiunta di URL di reindirizzamento SSO per l&#39;autenticazione estesa {#add-sso-redirect-urls-for-extended-authentication}

Se l&#39;autenticazione estesa è abilitata, gli utenti che aprono un documento protetto tramite criterio in Acrobat XI o Reader XI ricevono una finestra di dialogo per l&#39;autenticazione. Questa finestra di dialogo carica la pagina HTML specificata come URL di destinazione dell&#39;autenticazione estesa nelle impostazioni del server di protezione del documento. Consultate Impostazioni [di configurazione del](configuring-client-server-options.md#server-configuration-settings)server.

>[!NOTE]
>
>L&#39;autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successiva.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Fate clic su Esporta e salvate il file di configurazione sul disco.
1. Aprite il file in un editor e individuate il nodo AllowedUrls.
1. Nel `AllowedUrls` nodo, aggiungere le seguenti righe: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Salvate il file, quindi importate il file aggiornato dalla pagina Configurazione manuale: Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.

## Configurazione della protezione offline {#configuring-offline-security}

la protezione dei documenti consente di utilizzare i documenti protetti tramite criterio offline senza una connessione di rete o Internet. Questa funzionalità richiede che il criterio consenta l&#39;accesso offline, come descritto in [Specificare le autorizzazioni del documento per utenti e gruppi](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Prima che un documento con tale criterio possa essere utilizzato offline, il destinatario deve aprire il documento mentre è in linea e abilitare l&#39;accesso offline, facendo clic su Sì quando richiesto. Il destinatario può anche essere invitato ad autenticare la propria identità. Il destinatario può quindi utilizzare i documenti offline per tutta la durata del periodo di tempo consentito per l&#39;utilizzo offline specificata nel criterio.

Al termine del periodo di tempo consentito per l’utilizzo non in linea, il destinatario deve sincronizzarsi nuovamente con la protezione del documento aprendo un documento in linea oppure utilizzando un comando di menu delle estensioni Acrobat o Acrobat Reader DC per la sincronizzazione. (Vedere la Guida *di* Acrobat o la Guida *delle estensioni di* Acrobat Reader DC appropriata.)

Poiché i documenti che consentono l&#39;accesso offline richiedono la memorizzazione nella cache del materiale chiave nel computer in cui i file vengono memorizzati offline, il file può essere potenzialmente compromesso se un utente non autorizzato può ottenere il materiale chiave. Per compensare questa possibilità, sono disponibili opzioni di rollover programmate e manuali che è possibile configurare per impedire a una persona non autorizzata di utilizzare la chiave per accedere al documento.

### Impostazione di un periodo di tempo consentito offline predefinito {#set-a-default-offline-lease-period}

I destinatari dei documenti protetti tramite criterio possono portare i documenti offline per il numero di giorni specificato nel criterio. Dopo aver inizialmente sincronizzato il documento con la protezione del documento, il destinatario può utilizzarlo offline fino alla scadenza del periodo consentito per la trasmissione offline. Alla scadenza del periodo consentito, il destinatario deve portare il documento online ed effettuare l&#39;accesso per sincronizzarsi con la protezione del documento per continuare a utilizzare il documento.

È possibile configurare un periodo di tempo consentito per l&#39;utilizzo offline predefinito. Il periodo di leasing può essere modificato dall&#39;impostazione predefinita quando qualcuno crea o modifica un criterio.

1. Nella pagina di protezione del documento, fare clic su Configurazione > Configurazione server.
1. Nella casella Periodo di leasing offline predefinito, specificare il numero di giorni per il periodo di leasing offline.
1. Fai clic su OK.

### Gestire i rollover delle chiavi {#manage-key-rollovers}

Document Security utilizza algoritmi di cifratura e licenze per proteggere i documenti. Quando esegue la cifratura di un documento, la protezione del documento genera e gestisce una chiave di decrittazione denominata *DocKey* che trasmette all&#39;applicazione client. Se il criterio di protezione di un documento consente l&#39;accesso offline, viene generata una chiave offline denominata chiave ** principale anche per ogni utente che ha accesso offline al documento.

>[!NOTE]
>
>Se non esiste una chiave principale, Document Security ne genera una per proteggere un documento.

Per aprire offline un documento protetto tramite criterio, il computer dell&#39;utente deve avere la chiave principale appropriata. Il computer ottiene la chiave principale quando l&#39;utente si sincronizza con Document Security (apre un documento protetto online). Se la chiave dell&#39;entità viene compromessa, potrebbe essere compromesso anche qualsiasi documento a cui l&#39;utente ha accesso offline.

Un modo per ridurre la minaccia per i documenti offline è evitare di consentire l&#39;accesso offline a documenti particolarmente sensibili. Un altro metodo consiste nel passare periodicamente i tasti principali. Quando Document Security sposta il tasto sopra, le chiavi esistenti non possono più accedere ai documenti protetti tramite criterio. Ad esempio, se un autore ottiene una chiave principale da un computer portatile rubato, tale chiave non può essere utilizzata per accedere ai documenti protetti dopo il rollover. Se sospettate che una specifica chiave dell&#39;entità sia stata compromessa, potete passare manualmente il mouse sulla chiave.

Tuttavia, dovete anche essere consapevoli del fatto che un rollover di tasti interessa tutte le chiavi principali, non solo una. Riduce inoltre la scalabilità del sistema, perché i client devono memorizzare più chiavi per l&#39;accesso offline. La frequenza di rollover predefinita della chiave è 20 giorni. Si consiglia di non impostare questo valore su un valore inferiore a 14 giorni, perché agli utenti potrebbe essere impedito di visualizzare documenti offline e le prestazioni del sistema potrebbero essere influenzate.

Nell&#39;esempio seguente, Key1 è la prima delle due chiavi principali e Key2 è la più recente. Quando si fa clic sul pulsante Rollover Tasti ora la prima volta, Key1 diventa non valido e viene generata una nuova chiave principale valida (Key3). Gli utenti otterranno Key3 quando si sincronizzano con la protezione dei documenti, in genere aprendo un documento protetto online. Tuttavia, gli utenti non sono obbligati a sincronizzarsi con la protezione dei documenti fino a raggiungere il periodo di tempo consentito massimo per l&#39;utilizzo non in linea specificato in un criterio. Dopo il primo passaggio del tasto, gli utenti che restano offline possono comunque aprire i documenti offline, inclusi quelli protetti da Key3, fino a raggiungere il periodo massimo di tempo consentito per l&#39;utilizzo non in linea. Quando si fa clic nuovamente sul pulsante Rollover Tasti ora, Key2 diventa non valido e Key4 viene creato. Gli utenti che restano offline durante i due rollover chiave non possono aprire documenti protetti con Key3 o Key4 finché non si sincronizzano con la protezione del documento.

**Modificare la frequenza di rollover chiave**

Per motivi di riservatezza, quando si utilizzano documenti offline, Document Security fornisce un&#39;opzione di rollover automatico delle chiavi con un periodo di frequenza predefinito di 20 giorni. Potete modificare la frequenza di rollover; tuttavia, evitare di impostare un valore inferiore a 14 giorni perché agli utenti potrebbe essere impedito di visualizzare documenti offline e le prestazioni del sistema potrebbero essere influenzate.

1. Nella pagina Protezione documento, fare clic su Configurazione > Gestione chiavi.
1. Nella casella Frequenza rollover chiave, digitate il numero di giorni per il periodo di rollover.
1. Fai clic su OK.

**Passate manualmente il puntatore del mouse sulle chiavi principali**

Per mantenere la riservatezza dei documenti offline, puoi passare manualmente le chiavi principali. È possibile che sia necessario passare manualmente su una chiave (ad esempio, se la chiave viene compromessa da un utente che la riceve da un computer in cui è memorizzata nella cache per consentire l&#39;accesso offline a un documento).

>[!NOTE]
>
>Evitate di utilizzare frequentemente il rollover manuale perché causa il rollover di tutte le chiavi principali, non solo di una, e potrebbe impedire temporaneamente agli utenti di visualizzare i nuovi documenti offline.

Per annullare la validità delle chiavi dei computer client, è necessario eseguire il rollback due volte. I computer client con chiavi principali invalidate devono essere sincronizzati nuovamente con il servizio di protezione del documento per acquisire le nuove chiavi principali.

1. Nella pagina Protezione documento, fare clic su Configurazione > Gestione chiavi.
1. Fate clic su Tasti di rollover e quindi su OK.
1. Aspetta circa 10 minuti. Nel registro del server viene visualizzato il seguente messaggio di registro: `Done RightsManagement key rollover for`*N *`principals`. Dove* N *è il numero di utenti nel sistema di protezione del documento.
1. Fate clic su Tasti di rollover e quindi su OK.
1. Aspetta circa 10 minuti.

## Configurazione del controllo degli eventi e delle impostazioni di privacy {#configuring-event-auditing-and-privacy-settings}

Document Security consente di controllare e registrare le informazioni relative agli eventi correlati all&#39;interazione con documenti, criteri, amministratori e server protetti tramite criterio. Potete configurare il controllo degli eventi e specificare i tipi di eventi da controllare. Per eseguire il controllo degli eventi per un particolare documento, è necessario abilitare anche l&#39;opzione di controllo del criterio.

Quando il controllo è abilitato, è possibile visualizzare i dettagli degli eventi sottoposti a controllo nella pagina Eventi. gli utenti di Document Security possono inoltre visualizzare gli eventi relativi specificamente ai documenti protetti tramite criterio che utilizzano o creano.

È possibile selezionare i seguenti tipi di eventi per il controllo:

* Eventi di documenti protetti tramite criterio, ad esempio tentativi di apertura di documenti da parte di utenti autorizzati o non autorizzati
* Eventi dei criteri, quali creazione, modifica, eliminazione, attivazione e disattivazione dei criteri
* Eventi utente, come inviti e registrazioni di utenti esterni, account utente attivati e disattivati, modifiche alle password utente e aggiornamenti dei profili
* Eventi dei moduli AEM, come mancata corrispondenza delle versioni, fornitori di autorizzazioni e server di directory non disponibili e modifiche alla configurazione del server

### Attivare o disattivare il controllo degli eventi {#enable-or-disable-event-auditing}

Potete abilitare e disabilitare il controllo degli eventi relativi al server, ai documenti protetti tramite criterio, ai criteri, ai set di criteri e agli utenti. Quando abilitate il controllo degli eventi, potete scegliere di controllare tutti gli eventi possibili o di selezionare eventi specifici da controllare.

Quando abilitate il controllo del server, potete visualizzare gli eventi sottoposti a controllo nella pagina Eventi.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration (Protezione documento) > Audit and Privacy Settings (Impostazioni controllo e privacy).
1. Per configurare il controllo del server, in Abilita controllo server selezionare Sì o No.
1. Se avete selezionato Sì, in ciascuna categoria di eventi, effettuate una delle seguenti operazioni per selezionare le opzioni da controllare:

   * Per controllare tutti gli eventi della categoria, selezionare Tutto.
   * Per controllare solo alcuni eventi, deselezionate Tutti, quindi selezionate le caselle di controllo accanto agli eventi da controllare.

      Consultate Opzioni [di controllo degli](configuring-client-server-options.md#event-auditing-options)eventi.

1. Fai clic su OK.

>[!NOTE]
>
>Quando lavorate con le pagine Web, evitate di utilizzare i pulsanti del browser, come il pulsante Indietro, il pulsante Aggiorna e la freccia indietro o avanti, perché questa azione può causare problemi indesiderati di acquisizione dei dati e visualizzazione dei dati.

### Attivare o disattivare la notifica sulla privacy {#enable-or-disable-privacy-notification}

Potete attivare e disattivare un messaggio di notifica sulla privacy. Quando abilitate la notifica sulla privacy, viene visualizzato un messaggio quando un destinatario tenta di aprire un documento protetto tramite criterio. L&#39;avviso informa l&#39;utente che l&#39;utilizzo del documento è sottoposto a controllo. Potete inoltre specificare un URL che l&#39;utente può utilizzare per visualizzare la pagina dell&#39;informativa sulla privacy, se disponibile.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration (Configurazione) > Audit and Privacy Settings (Impostazioni controllo e privacy).
1. Per configurare la notifica sulla privacy, in Abilita informativa sulla privacy selezionare Sì o No.

   Se il criterio allegato a un documento consente l&#39;accesso anonimo dell&#39;utente e l&#39;opzione Abilita informativa sulla privacy è impostata su No, all&#39;utente non viene richiesto di accedere e il messaggio di notifica sulla privacy non viene visualizzato.

   Se il criterio allegato a un documento non consente l&#39;accesso anonimo, l&#39;utente visualizzerà il messaggio di notifica della privacy.

1. Se applicabile, nella casella URL privacy digitare l&#39;URL della pagina dell&#39;informativa sulla privacy. Se la casella URL privacy viene lasciata vuota, viene visualizzata la pagina sulla privacy di adobe.com.
1. Fai clic su OK.

>[!NOTE]
>
>La disattivazione dell&#39;informativa sulla privacy non disattiva il controllo dell&#39;utilizzo del documento. Le azioni di controllo predefinite e le azioni personalizzate supportate tramite il tracciamento dell&#39;uso esteso possono comunque raccogliere informazioni sul comportamento degli utenti.

### Importare un tipo di evento di controllo personalizzato {#import-a-custom-audit-event-type}

Se si utilizza un&#39;applicazione abilitata per la protezione dei documenti che supporta il controllo di eventi aggiuntivi, ad esempio eventi specifici per un determinato tipo di file, un partner Adobe può fornire all&#39;utente eventi di controllo personalizzati che è possibile importare in Document Security. Utilizzate questa funzione solo se avete ricevuto tipi di evento personalizzati da un partner Adobe.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration > Gestione eventi.
1. Fate clic su Sfoglia per passare al file XML da importare e fate clic su Importa.
1. L&#39;importazione sovrascrive i tipi di evento di controllo personalizzato esistenti sul server se vengono trovate combinazioni identiche per il codice evento e lo spazio dei nomi.
1. Fai clic su OK.

### Eliminazione di un tipo di evento di controllo personalizzato {#delete-a-custom-audit-event-type}

1. Nella console di amministrazione, fate clic su Servizi > Protezione documento > Configurazione > Gestione eventi.
1. Selezionare la casella di controllo accanto al tipo di evento di controllo personalizzato da eliminare e fare clic su Elimina.
1. Fai clic su OK.

### Esportazione di eventi di controllo {#export-audit-events}

È possibile esportare gli eventi di controllo in un file a scopo di archiviazione.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration > Gestione eventi.
1. Modificate le impostazioni in Eventi di controllo esportazione come necessario. Potete specificare:

   * l&#39;età minima degli eventi di audit da esportare
   * il numero massimo di eventi di controllo da includere in un singolo file. Il server genera uno o più file in base a questo valore.
   * la cartella in cui verrà creato il file. Questa cartella si trova nel server dei moduli. Se il percorso della cartella è relativo, è relativo alla directory principale del server applicazione.
   * il prefisso del file da utilizzare per i file degli eventi di controllo
   * il formato del file, un file CSV compatibile con Microsoft Excel o un file XML.

1. Fate clic su Esporta. Per annullare l’esportazione, fate clic su Annulla esportazione. Se un altro utente ha pianificato un&#39;esportazione, il pulsante Annulla esportazione non è disponibile fino al completamento dell&#39;esportazione. Il pulsante Annulla esportazione non è disponibile se un altro utente ha pianificato un&#39;esportazione. Per verificare se un&#39;esportazione o un&#39;eliminazione pianificata è iniziata o terminata, fate clic su Aggiorna.

### Eliminazione degli eventi di controllo {#delete-audit-events}

È possibile eliminare gli eventi di controllo che sono precedenti a un numero specificato di giorni.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration > Gestione eventi.
1. In Elimina eventi controllo, specificare il numero di giorni nella casella Elimina eventi controllo precedenti a.
1. Fai clic su Elimina. Fate clic su Esporta. Per annullare l’eliminazione, fate clic su Annulla eliminazione. Se un altro utente ha pianificato l’eliminazione, il pulsante Annulla Elimina non è disponibile fino al completamento dell’esportazione. Il pulsante Annulla eliminazione non è disponibile se un altro utente ha pianificato un&#39;esportazione. Per verificare se un&#39;eliminazione pianificata è iniziata o terminata, fare clic su Aggiorna.

### Opzioni di controllo degli eventi {#event-auditing-options}

Potete abilitare e disabilitare il controllo degli eventi e specificare i tipi di eventi da sottoporre a controllo.

**Eventi dei documenti**

**Visualizza documento:** Un destinatario visualizza un documento protetto tramite criterio.

**Chiudi documento:** Un destinatario chiude un documento protetto tramite criterio.

**Stampa a bassa risoluzione** Un destinatario stampa un documento protetto tramite criterio con l&#39;opzione a bassa risoluzione specificata.

**Stampa ad alta risoluzione:** Un destinatario stampa un documento protetto tramite criterio con l&#39;opzione ad alta risoluzione specificata.

**Aggiungi annotazione al documento:** Un destinatario aggiunge un&#39;annotazione a un documento PDF.

**Revoca documento:** Un utente o un amministratore revoca l&#39;accesso a un documento protetto tramite criterio.

**Annulla revoca documento:** Un utente o un amministratore ripristina l&#39;accesso a un documento protetto tramite criterio.

**Compilazione modulo:** Un destinatario immette informazioni in un documento PDF che è un modulo compilabile.

**Criterio rimosso:** Un editore rimuove un criterio da un documento per ritirare le protezioni di protezione.

**Modifica URL revoca documento:** Una chiamata dal livello API modifica l&#39;URL di revoca specificato per accedere a un nuovo documento che sostituisce un documento revocato.

**Modifica documento:** Un destinatario modifica il contenuto di un documento protetto tramite criterio.

**Firma documento:** Un destinatario firma un documento.

**Proteggere un nuovo documento:** Un utente applica un criterio per proteggere un documento.

**Cambia criterio sul documento:** Un utente o un amministratore modifica il criterio associato a un documento.

**Pubblica documento come:** Un nuovo documento con documentName e licenza identici a un documento esistente viene registrato sul server e i documenti non hanno una relazione padre-figlio. Questo evento può essere attivato mediante l’SDK dei moduli AEM.

**Inserisci documento:** Un nuovo documento con documentName e licenza identici a un documento esistente viene registrato sul server e i documenti hanno una relazione padre-figlio. Questo evento può essere attivato mediante l’SDK dei moduli AEM.

**Eventi dei criteri**

**Criterio creato:** Un utente o un amministratore crea un criterio.

**Criterio attivato:** Un amministratore rende disponibile un criterio.

**Criterio modificato:** Un utente o un amministratore modifica un criterio.

**Criterio disabilitato:** Un amministratore rende un criterio non disponibile.

**Criterio eliminato:** Un utente o un amministratore elimina un criterio.

**Cambia proprietario criterio:** Una chiamata dal livello API modifica il proprietario del criterio.

**Eventi utente**

**Utente eliminato:** Un amministratore elimina un account utente.

**Registra utente invitato:** Un utente esterno si registra con Document Security.

**Login riuscito:** Tentativi di accesso riusciti da parte di amministratori o utenti.

**Utenti invitati:** Document Security invita un utente a registrarsi.

**Utenti attivati:** Gli utenti esterni attivano i propri account utilizzando l&#39;URL contenuto nel messaggio e-mail di attivazione, oppure un amministratore attiva un account.

**Cambia password:** Gli utenti invitati a cambiare la propria password o un amministratore reimposta una password per un utente locale.

**Login non riuscito:** Tentativi di login non riusciti da parte di amministratori o utenti.

**Utenti disattivati:** Un amministratore disabilita un account utente locale.

**Aggiornamento profilo:** Gli utenti invitati cambiano nome, nome organizzazione e password.

**Account bloccato:** Un amministratore blocca un account.

**Eventi set di criteri**

**Set di criteri creati:** Un amministratore o un coordinatore di set di criteri crea un set di criteri.

**Set di criteri eliminato:** Un amministratore o un coordinatore di set di criteri elimina un set di criteri.

**Set di criteri modificato:** Un amministratore o un coordinatore di set di criteri modifica un set di criteri.

**Eventi di sistema**

**Sincronizzazione directory completata:** Queste informazioni non sono disponibili nella pagina Eventi. Le informazioni sulla sincronizzazione della directory corrente, incluso lo stato e l&#39;ora della sincronizzazione correnti dell&#39;ultima sincronizzazione, vengono visualizzate nella pagina Gestione dominio. Per accedere alla pagina Gestione dominio nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

**Accesso offline client abilitato:** Un utente ha attivato l&#39;accesso offline ai documenti protetti rispetto al server nel computer dell&#39;utente.

**L&#39;applicazione client** client sincronizzata deve sincronizzare le informazioni con il server per consentire l&#39;accesso offline.

**Versione non corrispondente:** Versione dell’SDK dei moduli AEM incompatibile con il server che ha tentato di connettersi al server.

**Informazioni sulla sincronizzazione della directory:** Queste informazioni non sono disponibili nella pagina Eventi. Le informazioni sulla sincronizzazione della directory corrente, incluso lo stato e l&#39;ora della sincronizzazione correnti dell&#39;ultima sincronizzazione, vengono visualizzate nella pagina Gestione dominio. Per accedere alla pagina Gestione dominio nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

**Modifica configurazione server:** Modifiche alla configurazione del server che vengono effettuate tramite le pagine Web o manualmente importando un file config.xml. Ciò include modifiche all&#39;URL di base, timeout sessione, blocchi login, impostazioni directory, rollover chiave, impostazioni server SMTP per la registrazione esterna, configurazione delle filigrane, opzioni di visualizzazione e così via.

## Configurazione del tracciamento dell’utilizzo esteso {#configuring-extended-usage-tracking}

Document Security consente di tenere traccia di vari eventi personalizzati che possono essere eseguiti su un documento protetto. È possibile abilitare il tracciamento degli eventi dal server di protezione dei documenti a livello globale o a livello di criterio. È quindi possibile impostare un JavaScript per acquisire azioni specifiche eseguite all&#39;interno del documento PDF protetto, ad esempio fare clic su un pulsante o salvare il documento. Questi dati di utilizzo vengono inviati come file XML in coppie chiave-valore da utilizzare per ulteriori analisi. Gli utenti finali che accedono ai documenti protetti possono consentire o rifiutare tale tracciamento dall&#39;applicazione client.

Se il tracciamento è abilitato a livello globale, puoi ignorare questa impostazione a livello di criterio e disattivarla per un particolare criterio. La sostituzione a livello di criterio non è possibile se il tracciamento è disabilitato a livello globale. L&#39;elenco degli eventi tracciati viene inviato automaticamente al server quando il conteggio degli eventi raggiunge il 25 o quando il documento viene chiuso. Potete inoltre configurare lo script in modo che esegua il push dell&#39;elenco eventi in modo esplicito in base alle vostre esigenze. È possibile personalizzare il tracciamento dell&#39;evento accedendo alle proprietà e ai metodi dell&#39;oggetto Document Security.

Dopo aver attivato il tracciamento, per impostazione predefinita tutti i criteri creati successivamente avranno attivato il tracciamento. I criteri creati prima che il tracciamento venga attivato sul server necessiteranno di aggiornamenti manuali.

### Attiva o disattiva il tracciamento dell’uso esteso {#enable-or-disable-extended-usage-tracking}

Prima di iniziare, accertatevi che l&#39;audit del server sia attivato. Per ulteriori informazioni sul controllo, consultate [Configurazione del controllo degli eventi e delle impostazioni](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) di privacy.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration (Protezione documento) > Audit and Privacy Settings (Impostazioni controllo e privacy).
1. Per configurare il tracciamento dell’uso esteso, in Abilita tracciamento, selezionare Sì o No.
1. Per impostare la selezione della casella di controllo Consenti raccolta di dati di utilizzo dettagliati nella pagina di accesso, in Attiva tracciamento predefinito, selezionare Sì o No.

Per visualizzare gli eventi tracciati è possibile utilizzare il filtro Eventi documenti nella pagina Eventi. Gli eventi tracciati tramite JavaScript sono etichettati come Tracciamento dettagliato dell&#39;utilizzo. Per ulteriori informazioni sugli eventi, vedere Eventi [di](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) monitoraggio.

## Configurare le impostazioni di visualizzazione della protezione dei documenti {#configure-document-security-display-settings}

1. Nella console di amministrazione, fare clic su Servizi > Protezione documento > Configurazione > Opzioni di visualizzazione.
1. Configurare le impostazioni e fare clic su OK.

### Display settings {#display-settings}

**Righe da visualizzare per i risultati della ricerca:** Numero di righe che vengono visualizzate su una pagina quando vengono eseguite le ricerche.

**Finestra di dialogo Personalizzazione per accesso client**

Queste impostazioni controllano il testo visualizzato nel prompt di accesso che viene visualizzato quando un utente accede alla protezione del documento tramite un&#39;applicazione client.

**Testo di benvenuto:** Testo del messaggio di benvenuto, ad esempio &quot;Accedi con il tuo nome utente e la password&quot;. Il testo del messaggio di benvenuto deve contenere informazioni su come accedere a Document Security e su come contattare un amministratore o un&#39;altra persona di supporto designata nell&#39;organizzazione per ottenere assistenza. Ad esempio, gli utenti esterni potrebbero dover contattare un amministratore se dimenticano la password o necessitano di assistenza per il processo di registrazione o di accesso. La lunghezza massima del testo di benvenuto è di 512 caratteri.

**Testo nome utente:** Etichetta di testo per la casella del nome utente.

**Testo password:** Etichetta di testo per la casella della password.

**Personalizzazione per la finestra di dialogo di autenticazione client basata sui certificati**

Queste impostazioni controllano il testo visualizzato nella finestra di dialogo di autenticazione del certificato.

**Scegli tipo di autenticazione:** Testo visualizzato per indirizzare l&#39;utente alla selezione di un tipo di autenticazione.

**Scegli testo certificato:** Testo visualizzato per indirizzare l&#39;utente alla selezione di un tipo di certificato.

**Testo errore certificati non disponibili:** Messaggio con un massimo di 512 caratteri da visualizzare quando il certificato selezionato non è disponibile.

**Personalizzazione per visualizzazione certificato client**

**Visualizza solo emittenti di credenziali attendibili:** Quando questa opzione è selezionata, l&#39;applicazione client presenta all&#39;utente solo i certificati provenienti da emittenti di credenziali per i quali i moduli AEM sono configurati per essere affidabili (consultate Gestione di certificati e credenziali.) Se questa opzione non è selezionata, l&#39;utente riceve un elenco di tutti i certificati presenti nel sistema dell&#39;utente.

## Configurare le filigrane dinamiche {#configure-dynamic-watermarks}

La protezione dei documenti consente di configurare le impostazioni predefinite per l&#39;opzione filigrana dinamica che è possibile applicare al momento della creazione dei criteri. Per *filigrana* si intende un’immagine sovrapposta al testo del documento. È utile per tenere traccia del contenuto di un documento e può aiutare a identificare l’uso illegale del contenuto.

Una filigrana dinamica può essere costituita da testo composto da variabili definite come ID utente e data e testo personalizzato oppure da contenuto RTF all’interno di un PDF. È possibile configurare filigrane con diversi elementi ciascuno con il proprio posizionamento e formattazione.

Le filigrane non sono modificabili e pertanto rappresentano un metodo più sicuro per garantire la riservatezza del contenuto del documento. Le filigrane dinamiche garantiscono inoltre che una filigrana contenga un numero sufficiente di informazioni specifiche per l’utente, in modo da fungere da deterrente per l’ulteriore distribuzione del documento.

La filigrana specificata da un criterio viene visualizzata nel documento protetto tramite criterio quando il destinatario visualizza o stampa il documento. A differenza delle filigrane permanenti, nel documento non viene mai salvata una filigrana dinamica, il che offre la flessibilità necessaria per distribuire un documento in un ambiente Intranet in modo da garantire che l&#39;applicazione di visualizzazione visualizzi l&#39;identità dell&#39;utente specifico. Inoltre, se un documento ha più utenti, l&#39;uso della filigrana dinamica consente di utilizzare un documento invece di più versioni, ognuna con una filigrana diversa. La filigrana visualizzata riflette l&#39;identità dell&#39;utente corrente.

Le filigrane dinamiche sono diverse dalle filigrane che gli utenti possono aggiungere direttamente al documento in Acrobat. In un documento protetto tramite criterio è quindi possibile inserire due filigrane.

### Considerazioni per la creazione di filigrane {#considerations-when-creating-watermarks}

È possibile creare filigrane dinamiche con diversi elementi di filigrana con ciascun elemento specificato come testo o PDF. È possibile includere fino a cinque elementi in una filigrana.

Se scegliete una filigrana basata su testo, potete specificare diversi elementi all’interno della filigrana con più voci di testo e specificare il posizionamento di ciascun elemento. Assegnate nomi significativi a questi elementi, ad esempio intestazione, piè di pagina e così via.

Ad esempio, se si desidera specificare come filigrana un testo diverso nell&#39;intestazione, nel piè di pagina, nei margini e all&#39;interno del documento, è possibile creare diversi elementi di filigrana e specificarne le posizioni. Se si desidera che l&#39;ID utente dell&#39;utente e la data corrente di accesso al documento vengano visualizzati nell&#39;intestazione, il nome del criterio sul margine destro e un testo personalizzato &quot;CONFIDENTIAL&quot; venga visualizzato diagonalmente nel documento, è necessario definire elementi di filigrana separati con testo come tipo e specificarne la formattazione e il posizionamento. Quando la filigrana viene applicata a un documento, tutti gli elementi della filigrana vengono applicati contemporaneamente al documento, nell&#39;ordine in cui vengono aggiunti alla filigrana.

In genere, le filigrane basate su PDF vengono utilizzate per includere contenuti grafici quali logo o simboli speciali quali il copyright o il marchio registrato.

È possibile modificare i limiti relativi al numero di elementi della filigrana e alla dimensione del file PDF modificando il file di configurazione della protezione del documento. Consultate [Modificare i parametri](configuring-client-server-options.md#change-the-watermark-configuration-parameters)di configurazione delle filigrane.

Quando configurate le filigrane, tenete presente quanto segue:

* Non è possibile utilizzare un documento PDF protetto da password come elemento filigrana. Tuttavia, se la filigrana creata contiene altri elementi non protetti da password, verrà applicata come parte della filigrana.
* È possibile modificare la dimensione massima del file PDF che si desidera utilizzare come elemento filigrana. Tuttavia, i documenti PDF di grandi dimensioni utilizzati come filigrane compromettono le prestazioni durante la sincronizzazione offline dei documenti applicati con tali filigrane. Consultate [Modificare i parametri](configuring-client-server-options.md#change-the-watermark-configuration-parameters)di configurazione delle filigrane.
* Come filigrana viene usata solo la prima pagina del PDF selezionato. Verificate che le informazioni da visualizzare come filigrane siano disponibili sulla prima pagina stessa.
* Anche se è possibile specificare il ridimensionamento del documento PDF, tenere conto delle dimensioni e del layout della pagina del PDF se si intende utilizzarlo come filigrana nell&#39;intestazione, piè di pagina o margini.
* Quando specificate il nome del font, immettete correttamente il nome. I moduli AEM sostituiscono il font specificato se non è presente nel computer client in cui viene aperto il documento.
* Se il testo è stato selezionato come contenuto della filigrana, specificando l&#39;opzione di ridimensionamento Adatta alla pagina non sarà possibile utilizzare pagine con larghezza diversa.
* Quando specificate il posizionamento degli elementi della filigrana, accertatevi che non vi sia più di un elemento con lo stesso posizionamento. Se due elementi di filigrana hanno lo stesso posizionamento, ad esempio il centro, appaiono sovrapposti sul documento e nell&#39;ordine in cui sono stati aggiunti alla filigrana.
* Quando specificate la dimensione e il tipo di font, accertatevi che la lunghezza del testo sia completamente visibile all’interno della pagina. Il contenuto del testo viene disposto su nuove righe, pertanto il contenuto della filigrana che si intende presentare ai margini potrebbe sovrapporsi alle aree contenuto delle pagine. Tuttavia, se il documento viene aperto in Acrobat 9, il testo oltre la singola riga viene troncato.

### Limitazioni delle filigrane dinamiche {#limitations-of-dynamic-watermarks}

Alcune applicazioni client potrebbero non supportare filigrane dinamiche. Vedere la Guida alle estensioni Acrobat Reader DC appropriata. Inoltre, tenere presente quanto segue sulle versioni di Acrobat che supportano le filigrane dinamiche:

* Non è possibile utilizzare un documento PDF protetto da password come elemento filigrana.
* Le versioni di Acrobat e Adobe Reader precedenti alla 10 non supportano le seguenti funzionalità delle filigrane:

   * Filigrane PDF
   * Più elementi nella filigrana (Testo/PDF)
   * Opzioni avanzate, ad esempio una serie di pagine o opzioni di visualizzazione
   * Opzioni di formattazione del testo quali il font specificato, il nome e il colore del font specificati. Tuttavia, le versioni precedenti di Acrobat e Reader visualizzeranno il contenuto del testo con il font e il colore predefiniti.

* Acrobat 9.0 e versioni precedenti: Acrobat 9.0 e versioni precedenti non supporta i nomi dei criteri nelle filigrane dinamiche. Se Acrobat 9.0 apre un documento protetto tramite criterio con una filigrana dinamica che include un nome di criterio e altri dati dinamici, la filigrana viene visualizzata senza il nome del criterio. Se la filigrana dinamica include solo il nome del criterio, Acrobat visualizza un messaggio di errore

### Aggiungere un modello di filigrana dinamica {#add-a-dynamic-watermark-template}

Potete creare modelli di filigrane dinamiche. Tali modelli restano disponibili come opzione di configurazione per i criteri creati dagli amministratori o dagli utenti.

>[!NOTE]
>
>Le informazioni di configurazione delle filigrane dinamiche non vengono acquisite con le altre informazioni di configurazione al momento dell&#39;esportazione di un file di configurazione.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration > Watermarks.
1. Fai clic su Nuovo.
1. Nella casella Nome, digitare un nome per la nuova filigrana.

   ***nota **: Non è possibile utilizzare alcuni caratteri speciali nei nomi o nelle descrizioni di filigrane o elementi di filigrana. Consultate le limitazioni elencate in[Considerazioni per la modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. In Nome, accanto al segno più, immettete un nome significativo per l’elemento filigrana, ad esempio Intestazione, e aggiungete una descrizione, quindi espandete il segno più per visualizzare le opzioni.
1. In Sorgente, selezionate il tipo di filigrana come Testo o PDF.
1. Se avete selezionato Testo, effettuate le seguenti operazioni:

   * Selezionare i tipi di filigrana da includere. Se selezionate Testo personalizzato, digitate nella casella adiacente il testo da visualizzare per la filigrana. Tenere presente la lunghezza del testo che verrà visualizzata come filigrana.
   * Specificate le proprietà di formattazione del testo, quali il nome del font, la dimensione del font, il colore di primo piano e il colore di sfondo per il contenuto del testo della filigrana. Specificate il colore di primo piano e di sfondo come valori esadecimali.

      ***nota **: Se si seleziona l&#39;opzione di ridimensionamento Adatta alla pagina, la proprietà della dimensione del font non è disponibile per la modifica.*

1. Se è stato selezionato PDF per opzioni filigrana RTF, fare clic su **Sfoglia** accanto a Seleziona PDF filigrana per selezionare il documento PDF da utilizzare come filigrana.

   ***nota **: Non utilizzare un documento PDF protetto da password. Se specificate un PDF protetto da password come elemento filigrana, la filigrana non viene applicata.*

1. In Usa come sfondo, selezionare Sì o No.

   **nota**: Attualmente, la filigrana viene visualizzata in primo piano indipendentemente da questa impostazione.

1. Per controllare la posizione della filigrana sul documento, configurare le opzioni Allineamento verticale e Allineamento orizzontale.
1. Selezionare Adatta alla pagina oppure selezionare % e digitare una percentuale nella casella. Il valore deve essere un numero intero, non una frazione. Per configurare la dimensione della filigrana, è possibile utilizzare un valore pari alla percentuale della pagina oppure impostare la filigrana in modo che rientri nella dimensione della pagina.
1. Nella casella Rotazione, digitare i gradi in base ai quali ruotare la filigrana. L&#39;intervallo è compreso tra -180 e 180. Usate un valore negativo per ruotare la filigrana in senso antiorario. Il valore deve essere un numero intero, non una frazione.
1. Nella casella Opacità, digitare una percentuale. Utilizzate un numero intero, non una frazione.
1. In Opzioni avanzate, impostate quanto segue:

   **Opzioni intervallo pagine**

   Impostare l&#39;intervallo di pagine in cui deve essere visualizzata la filigrana. Immettete la pagina iniziale come 1 e la pagina finale come -1 in modo che tutte le pagine siano contrassegnate con la filigrana.

   **Opzioni di visualizzazione**

   Selezionare la posizione in cui si desidera visualizzare la filigrana. Per impostazione predefinita, la filigrana viene visualizzata sia in copia software (online) che in copia cartacea (stampa).

1. Fate clic su **Nuovo** in Elementi filigrana per aggiungere altri elementi di filigrana, se necessario.
1. Fai clic su OK.

### Modificare un modello di filigrana dinamica {#edit-a-dynamic-watermark-template}

1. Nella console di amministrazione, fate clic su Servizi > Protezione documento > Configurazione > Filigrane.
1. Fare clic sulla filigrana appropriata nell&#39;elenco.
1. Nella pagina Modifica filigrane, modificare le impostazioni in base alle esigenze.
1. Fai clic su OK.

### Eliminare un modello di filigrana dinamica {#delete-a-dynamic-watermark-template}

Quando si elimina una filigrana dinamica, non è più possibile aggiungerla a un nuovo criterio. Tuttavia, la filigrana rimane sui criteri esistenti che la utilizzano e i documenti attualmente protetti dal criterio continuano a mostrare la filigrana dinamica fino a quando l&#39;utente non modifichi il criterio che contiene la filigrana eliminata. Dopo la modifica del criterio, la filigrana non viene più applicata. Viene visualizzato un messaggio che indica che la filigrana esistente viene eliminata dal criterio e che l&#39;utente può selezionarne un&#39;altra per sostituirla.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configuration > Watermarks.
1. Selezionate la casella accanto alla filigrana appropriata e fate clic su Elimina.
1. Fai clic su OK.

## Configurazione della registrazione degli utenti invitati {#configuring-invited-user-registration}

Gli utenti esterni all&#39;organizzazione possono registrarsi con Document Security. Gli utenti invitati che si registrano e attivano i propri account possono accedere a Document Security utilizzando il proprio indirizzo e-mail e la password che creano al momento della registrazione. Gli utenti invitati registrati possono utilizzare documenti protetti tramite criterio per i quali dispongono delle autorizzazioni.

Quando gli utenti invitati vengono attivati, diventano utenti locali. Gli utenti locali possono essere configurati e gestiti utilizzando l&#39;area Utenti invitati e locali. Consultate [Gestione degli account](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)utente invitati e locali.

A seconda delle funzionalità abilitate per gli utenti invitati, questi possono utilizzare anche le seguenti funzioni di protezione dei documenti:

* Applicazione di criteri ai documenti
* Creare criteri
* Aggiunta di utenti invitati ai criteri

Document Security genera automaticamente un messaggio e-mail di invito alla registrazione quando si verificano gli eventi seguenti, a meno che l’utente non sia già nella directory LDAP di origine o sia stato invitato in precedenza a registrarsi:

* Un utente esistente aggiunge un utente invitato a un criterio
* Un amministratore aggiunge un account utente invitato nella pagina Registrazione utente invitata

Il messaggio e-mail di registrazione contiene un collegamento a una pagina di registrazione e informazioni su come registrarsi. Dopo che l&#39;utente invitato si è registrato, la protezione del documento genera un messaggio e-mail di attivazione con un collegamento a una pagina di attivazione. Quando è attivato, l&#39;account rimane valido fino a quando non viene disattivato o eliminato.

Se abilitate la registrazione integrata, specificate il vostro server SMTP, i dettagli e-mail di registrazione, le capacità di accesso e reimpostate le informazioni relative alla password solo una volta. Prima di abilitare la registrazione integrata, accertatevi di aver creato un dominio locale in Gestione utenti che abbia assegnato il ruolo &quot;Utente invito protezione documento&quot; agli utenti e ai gruppi appropriati dell&#39;organizzazione. Consultate [Aggiungere un dominio](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) locale e [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles). Se non utilizzate la registrazione integrata, è necessario che sia creato un sistema di registrazione utente personalizzato tramite l&#39;SDK dei moduli AEM. Consulta la guida sullo sviluppo di SPI per moduli AEM nella [programmazione con i moduli](https://www.adobe.com/go/learn-aemforms-programming-63)AEM. Se non utilizzate l&#39;opzione Registrazione incorporata, si consiglia di configurare un messaggio nel messaggio e-mail di attivazione e nella schermata di accesso del client per informare gli utenti su come contattare l&#39;amministratore per ottenere una nuova password o per altre informazioni.

**Abilitare e configurare la registrazione degli utenti invitati**

Per impostazione predefinita, il processo di registrazione degli utenti invitati è disabilitato. Potete attivare e disattivare la registrazione degli utenti invitati per la protezione del documento, a seconda delle necessità.

1. Nella console di amministrazione, fate clic su Servizi > Protezione documento > Configurazione > Registrazione utente invitata.
1. Selezionate Abilita registrazione utente invitata.
1. (Facoltativo) Aggiornate le impostazioni di registrazione degli utenti invitati come richiesto:

   * [Escludere o includere un utente o un gruppo esterno](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parametri del server e dell&#39;account di registrazione](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Impostazioni e-mail invito alla registrazione](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Impostazioni e-mail attivazione](configuring-client-server-options.md#activation-email-settings)
   * [Configurare un messaggio e-mail per la reimpostazione della password](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Facoltativo) In Registrazione incorporata, selezionate Sì per abilitare questa opzione. Se non abilitate la registrazione integrata, dovete configurare il vostro sistema di registrazione utente.
1. Fai clic su OK.

### Escludere o includere un utente o un gruppo esterno {#exclude-or-include-an-external-user-or-group}

È possibile limitare la registrazione con la protezione del documento a determinati utenti o gruppi di utenti esterni. Questa opzione è utile, ad esempio, per consentire l’accesso a un determinato gruppo di utenti, escludendo però individui specifici che fanno parte del gruppo.

Le seguenti impostazioni si trovano nell’area Filtro limitazioni e-mail della pagina Registrazione utente invitato.

**Esclusione:** Digitate l’indirizzo e-mail di un utente o gruppo da escludere. Per escludere più utenti o gruppi, digitate ogni indirizzo e-mail su una nuova riga. Per escludere tutti gli utenti che appartengono a un dominio particolare, immettete un carattere jolly e il nome del dominio. Ad esempio, per escludere tutti gli utenti nel dominio example.com, immetti &amp;ast;.example.com.

**Inclusione:** Digitate l’indirizzo e-mail di un utente o gruppo da includere. Per includere più utenti o gruppi, digitate ogni indirizzo e-mail su una nuova riga. Per includere tutti gli utenti che appartengono a un dominio particolare, immettete un carattere jolly e il nome del dominio. Ad esempio, per includere tutti gli utenti nel dominio example.com, immetti &amp;ast;.example.com.

### Parametri del server e dell&#39;account di registrazione {#server-and-registration-account-parameters}

Le seguenti impostazioni si trovano nell’area Impostazioni generali della pagina Registrazione degli utenti invitati.

**Host SMTP:** Il nome host del server SMTP. Il server SMTP gestisce le notifiche e-mail in uscita per registrare e attivare gli account utente invitati.

Se richiesto dall&#39;host SMTP, digitare le informazioni richieste nelle caselle Nome account server SMTP e Password account server SMTP per connettersi al server SMTP. Alcune organizzazioni non applicano questo requisito. Per ulteriori informazioni, rivolgetevi all’amministratore di sistema.

**Nome classe socket server SMTP:** Nome della classe Socket per il server SMTP. Ad esempio, javax.net.ssl.SSLSocketFactory.

**Tipo di contenuto e-mail:** Tipo MIME accettato come text/plain o text/html.

**Codifica e-mail:** Formato di codifica da utilizzare per l&#39;invio di messaggi e-mail. È possibile specificare qualsiasi codifica, ad esempio UTF-8 per Unicode o ISO-8859-1 per Latin. Il valore predefinito è UTF-8.

**Indirizzo e-mail di reindirizzamento:** Quando specificate un indirizzo e-mail per questa impostazione, tutti i nuovi inviti vengono inviati all&#39;indirizzo fornito. Questa impostazione può essere utile a scopo di test.

**Usa domini locali:** Selezionare il dominio appropriato. In una nuova installazione, accertati di aver creato il dominio utilizzando Gestione utente. Se si tratta di un aggiornamento, durante l&#39;aggiornamento è stato creato un dominio utente esterno che può essere utilizzato.

**Usa SSL per il server SMTP:** Selezionare questa opzione per abilitare SSL per il server SMTP.

**Visualizza il collegamento di accesso sulla pagina di registrazione:** Visualizza un collegamento di login nella pagina di registrazione visualizzata per gli utenti invitati.

**Per abilitare Transport Layer Security (TLS) per il server SMTP**

1. Aprite la console di amministrazione.

   Il percorso predefinito della console di amministrazione è `https://<server>:<port>/adminui`.

1. Andate a Home > Servizi > Document Security > Configuration (Protezione documento) > Invitated User Registration (Registrazione utente invitata).
1. In Registrazione utente invitata, specificate tutte le impostazioni di configurazione e fate clic su OK.

   >[!NOTE]
   >
   >Se utilizzate Microsoft Office 365 come server SMTP per inviare gli inviti per la registrazione degli utenti, utilizzate le seguenti impostazioni:
   >
   >**Host SMTP:** smtp.office365.com
   >**Porta:** 587

1. Quindi, è necessario aggiornare config.xml. Consultate [Configurazione per abilitare SMTP per Transport Layer Security (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Se apportate delle modifiche alle opzioni di registrazione degli utenti invitati, il file config.xml viene sovrascritto e TLS viene disattivato. Se sovrascrivete le modifiche, dovete eseguire il passaggio precedente per riattivare il supporto TLS per la registrazione degli utenti invitati.

### Impostazioni e-mail invito alla registrazione {#registration-invitation-email-settings}

Document Security invia automaticamente un messaggio e-mail di invito alla registrazione quando create un nuovo account utente invitato o quando un utente esistente aggiunge un destinatario esterno che non si è precedentemente registrato o che è stato invitato a registrarsi a un criterio. Il messaggio e-mail contiene un collegamento che il destinatario può utilizzare per accedere alla pagina di registrazione e immettere le informazioni relative all&#39;account personale, inclusi nome utente e password. La password può contenere una combinazione qualsiasi di otto caratteri.

Quando il destinatario attiva l&#39;account, l&#39;utente diventa un utente locale.

Le seguenti impostazioni si trovano nell’area Configurazione e-mail di invito della pagina Registrazione utente invitata.

**Da:** L’indirizzo e-mail dal quale viene inviato l’invito. Il formato predefinito dell&#39;indirizzo e-mail Da è postmaster@[your_install_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di invito.

**Timeout:** Il numero di giorni successivi alla scadenza dell’invito di registrazione se l’utente esterno non si registra. Il valore predefinito è 30 giorni.

**Messaggio:** Testo visualizzato nel corpo del messaggio che invita l’utente a registrarsi.

### Impostazioni e-mail attivazione {#activation-email-settings}

Dopo la registrazione degli utenti invitati, Document Security invia un messaggio e-mail di attivazione. Il messaggio e-mail di attivazione contiene un collegamento alla pagina di attivazione dell’account, in cui gli utenti possono attivare il proprio account. Quando gli account sono attivati, gli utenti possono accedere alla protezione dei documenti utilizzando il proprio indirizzo e-mail e la password che hanno creato al momento della registrazione.

Quando il destinatario attiva l&#39;account utente, l&#39;utente diventa un utente locale.

Le seguenti impostazioni si trovano nell’area Configurazione e-mail attivazione della pagina Registrazione utente invitata.

>[!NOTE]
>
>È inoltre consigliabile configurare un messaggio nella schermata di accesso per informare gli utenti esterni su come contattare l’amministratore per ottenere una nuova password o per altre informazioni.

**Da:** L’indirizzo e-mail dal quale viene inviato il messaggio e-mail di attivazione. Questo indirizzo e-mail riceve le notifiche di consegna non riuscite dall’ospitante dell’e-mail dell’utente registrato e tutti i messaggi inviati dal destinatario in risposta all’e-mail di registrazione. Il formato predefinito dell&#39;indirizzo e-mail Da è postmaster@[your_install_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di attivazione.

**Timeout:** Il numero di giorni successivi alla scadenza dell&#39;invito di attivazione se l&#39;utente non attiva l&#39;account. Il valore predefinito è 30 giorni.

**Messaggio:** Testo che appare nel corpo del messaggio un messaggio che indica che l&#39;account utente del destinatario deve essere attivato. È inoltre possibile includere informazioni come contattare un amministratore per ottenere una nuova password.

### Configurare un messaggio e-mail per la reimpostazione della password {#configure-a-password-reset-email}

Se dovete ripristinare la password di un utente invitato, viene generato un messaggio e-mail di conferma che invita l&#39;utente a scegliere una nuova password. Impossibile determinare la password di un utente; se l&#39;utente lo dimentica, è necessario reimpostarlo.

Le seguenti impostazioni si trovano nell’area Reimposta password e-mail della pagina Registrazione utente invitata.

**Da:** Indirizzo e-mail da cui viene inviato il messaggio e-mail di reimpostazione della password. Il formato predefinito dell&#39;indirizzo e-mail Da è postmaster@[your_install_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di ripristino.

**Messaggio:** Testo che appare nel corpo del messaggio un messaggio per indicare che la password utente esterna del destinatario viene reimpostata.

## Abilitare utenti e gruppi a creare criteri {#enable-users-and-groups-to-create-policies}

Nella pagina Configurazione è presente un collegamento alla pagina Criteri personali, in cui è possibile specificare quali utenti finali possono creare i miei criteri e quali utenti e gruppi sono visibili nei risultati della ricerca. La pagina Criteri personali presenta due schede:

**Scheda Crea criteri:** Utilizzate per configurare le autorizzazioni utente per creare criteri personalizzati.

**Scheda Utenti e gruppi visibili:** Consente di controllare quali utenti e gruppi sono visibili nei risultati della ricerca utente. L&#39;amministratore super utente o set di criteri deve selezionare e aggiungere i domini, creati in Gestione utente, all&#39;utente e al gruppo visibile per ciascun set di criteri. Questo elenco è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini a cui il coordinatore del set di criteri può accedere quando sceglie gli utenti da aggiungere ai criteri.

Prima di concedere agli utenti l&#39;autorizzazione per creare criteri personalizzati, considerate l&#39;accesso o il controllo che desiderate concedere ai singoli utenti. Inoltre, considerate come debbano essere esposti gli utenti e i gruppi quando li rendete visibili alle ricerche.

### Specificare utenti e gruppi che possono creare criteri {#specify-users-and-groups-who-can-create-policies}

In qualità di amministratore, specificate quali utenti e gruppi possono creare criteri personalizzati. Questa autorizzazione può essere impostata a livello di utente e gruppo. La funzionalità di ricerca cerca gli utenti e i gruppi nel database Gestione utente.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Configurazione > Criteri personali.
1. Nella pagina Criteri personali, fate clic sulla scheda Crea criteri e fate clic su Aggiungi utenti e gruppi.
1. Nella casella Trova, digitate il nome utente o l’indirizzo e-mail dell’utente o del gruppo che state cercando. Se non disponete di tali informazioni, lasciate vuota la casella. Potete anche digitare un nome parziale o un indirizzo e-mail, ad esempio se si conoscono solo le prime due lettere del nome utente.
1. Nell&#39;elenco Utilizzo, selezionare i parametri di ricerca Nome o E-mail.
1. Nell’elenco Tipo, selezionate Gruppo o Utente per limitare la ricerca.
1. Nell&#39;elenco In, selezionare il dominio da cercare. Se non conosci il dominio dell’utente o del gruppo, seleziona Tutti i domini.
1. Nell&#39;elenco Visualizza, specificare il numero di risultati di ricerca da visualizzare per pagina, quindi fare clic su Trova.
1. Per aggiungere utenti e gruppi Criteri personali, selezionate la casella di controllo per ciascun utente e gruppo da aggiungere.
1. Fate clic su Aggiungi, quindi su OK.

Gli utenti e i gruppi selezionati ora dispongono dell&#39;autorizzazione per creare criteri personalizzati.

### Rimuovere l&#39;autorizzazione per la creazione di criteri personalizzati da un utente o gruppo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Nella pagina Protezione documento, fare clic su Configurazione > Criteri personali.
1. Nella pagina Criteri personali fare clic sulla scheda Crea criteri. Vengono visualizzati utenti e gruppi con autorizzazioni per creare criteri personalizzati.
1. Selezionate la casella di controllo accanto agli utenti e ai gruppi da rimuovere da questa autorizzazione.
1. Fate clic su Elimina, quindi su OK.

### Specificare utenti e gruppi visibili nelle ricerche {#specify-users-and-groups-that-are-visible-in-searches}

Quando gli utenti gestiscono i propri criteri personalizzati, possono cercare utenti e gruppi da aggiungere ai propri criteri. È necessario specificare i domini da cui gli utenti e i gruppi sono visibili in queste ricerche.

1. Nella pagina Protezione documento, fare clic su Configurazione > Criteri personali.
1. Nella pagina Criteri personali, fai clic sulla scheda Utenti e gruppi visibili.
1. Per rendere visibili gli utenti e i gruppi di un dominio, fai clic su Aggiungi domini, seleziona i domini e fai clic su Aggiungi. Per rimuovere un dominio, selezionate la casella di controllo accanto al nome del dominio e fate clic su Elimina.

## Modifica manuale del file di configurazione della protezione del documento {#manually-editing-the-document-security-configuration-file}

È possibile importare ed esportare le informazioni di configurazione memorizzate nel database di protezione del documento. Ad esempio, potrebbe essere utile creare una copia di backup delle informazioni di configurazione quando si passa da un ambiente di produzione in fase di produzione, oppure si potrebbe desiderare di modificare le opzioni avanzate che possono essere configurate solo modificando questo file.

Utilizzando il file di configurazione potete effettuare le seguenti modifiche:

[Visualizzare le autorizzazioni CATIA durante la creazione e la modifica dei criteri](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Specificare un periodo di timeout per la sincronizzazione offline](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Rifiuto di Document Security Services per applicazioni specifiche](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Disattivazione di collegamenti esterni](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>L&#39;importazione del file di configurazione consente di riconfigurare il sistema in base alle informazioni contenute nel file. Le eccezioni sono la configurazione della filigrana dinamica e le informazioni sugli eventi personalizzati, che non vengono salvate con il file di configurazione esportato. È necessario configurare queste informazioni manualmente nel nuovo sistema. Solo un amministratore di sistema o un consulente di servizi professionali che abbia familiarità con Document Security e XML deve modificare il contenuto di un file di configurazione, ad esempio per riconfigurare un&#39;impostazione danneggiata o per sintonizzare i parametri di un particolare scenario di distribuzione aziendale.

**Esportare un file di configurazione**

1. Nella console di amministrazione, fare clic su Servizi > Protezione documento 11 > Configurazione > Configurazione manuale.
1. Fate clic su Esporta e salvate il file di configurazione in un’altra posizione. Il nome file predefinito è config.xml.
1. Fai clic su OK.
1. Prima di modificare il file di configurazione, effettuate una copia di backup nel caso sia necessario ripristinarlo.

**Importare un file di configurazione**

1. Nella console di amministrazione, fare clic su Servizi > Protezione documento 11 > Configurazione > Configurazione manuale.
1. Fate clic su Sfoglia per passare al file di configurazione e quindi su Importa. Non è possibile digitare il percorso direttamente nella casella Nome file.
1. Fai clic su OK.

### Specificare un periodo di timeout per la sincronizzazione offline {#specify-a-timeout-period-for-offline-synchronization}

Document Security consente agli utenti di aprire e utilizzare documenti protetti quando non sono connessi al server di protezione del documento. L&#39;applicazione client dell&#39;utente deve sincronizzarsi regolarmente con il server per mantenere i documenti validi per l&#39;uso offline. La prima volta che gli utenti aprono un documento protetto, viene chiesto loro se il computer deve essere autorizzato a eseguire la sincronizzazione periodica dei client.

Per impostazione predefinita, la sincronizzazione viene eseguita automaticamente ogni quattro ore e in base alle esigenze quando un utente è connesso al server di protezione del documento. Se il periodo offline di un documento scade mentre l&#39;utente è offline, l&#39;utente deve riconnettersi al server per consentire all&#39;applicazione client di sincronizzarsi con il server.

Nel file di configurazione della protezione del documento, potete specificare la frequenza predefinita della sincronizzazione automatica in background. Questa impostazione funge da applicazione client per il periodo di timeout predefinito, a meno che il client non imposti esplicitamente il proprio valore di timeout.

1. Esportare il file di configurazione della protezione del documento. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)
1. Apri il file di configurazione in un editor e individua il `PolicyServer` nodo. Sotto il nodo, individuare il `ServerSettings` nodo.
1. Nel `ServerSettings` nodo, aggiungere la seguente voce e salvare il file:

   `<entry key="BackgroundSyncFrequency" value="`*time *`"/>`

   dove *tempo* è il numero di secondi tra le sincronizzazioni in background automatiche. Se hai inviato questo valore a `0`, la sincronizzazione viene sempre eseguita. Il valore predefinito è `14400` secondi (ogni quattro ore).

1. Importa il file di configurazione. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)

### Rifiuto di Document Security Services per applicazioni specifiche {#denying-document-security-services-for-specific-applications}

È possibile configurare la protezione dei documenti per negare i servizi alle applicazioni che soddisfano criteri specifici. I criteri possono specificare un singolo attributo, ad esempio un nome di piattaforma, oppure più set di attributi. Questa funzione consente di controllare le richieste che la protezione del documento deve gestire. Di seguito sono riportate alcune applicazioni di questa funzione:

* **Protezione delle entrate:** È possibile negare l&#39;accesso a qualsiasi applicazione client che non supporta le convenzioni sulle entrate.
* **Compatibilità dell&#39;applicazione:** Alcune applicazioni potrebbero essere incompatibili con i criteri o il comportamento del server di protezione dei documenti.

Quando le applicazioni client tentano di stabilire un collegamento con la protezione dei documenti, forniscono informazioni su applicazione, versione e piattaforma. Document Security confronta queste informazioni con le impostazioni Rifiuti che ottengono dal file di configurazione Document Security.

Le impostazioni Rifiuti possono contenere diversi set di condizioni di rifiuto. Se tutti gli attributi di un set corrispondono, all&#39;applicazione richiedente viene negato l&#39;accesso ai servizi di protezione del documento.

La funzione di negazione del servizio richiede che le applicazioni client utilizzino la versione SDK client C++ versione 8.2 o successiva per la protezione del documento. I seguenti prodotti Adobe forniscono informazioni sui prodotti durante la richiesta di servizi di Document Security:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard e versioni successive
* Adobe Reader 9.0 e versioni successive
* Estensioni di Acrobat Reader DC per Microsoft Office 8.2 e versioni successive

Le applicazioni client utilizzano l&#39;API client dall&#39;SDK client per la protezione dei documenti C++ per richiedere i servizi dalla protezione dei documenti. Le richieste API client includono informazioni sulla piattaforma e sulla versione SDK (precompilate nell&#39;API client) e informazioni sui prodotti ottenute dall&#39;applicazione client.

Le applicazioni client o i plug-in forniscono informazioni sui prodotti nella loro implementazione di una funzione di callback. L&#39;applicazione fornisce le seguenti informazioni:

* Nome integratore
* Versione integratore
* Famiglia di applicazioni
* Nome applicazione
* Versione applicazione

Se non sono disponibili informazioni, l&#39;applicazione client lascia vuoto il campo corrispondente.

Diverse applicazioni Adobe includono informazioni sui prodotti durante la richiesta di servizi di protezione dei documenti, ad esempio le estensioni Acrobat, Adobe Reader e Acrobat Reader DC per Microsoft Office.

**Acrobat e Adobe Reader**

Quando Acrobat o Adobe Reader richiedono un servizio di protezione dei documenti, fornisce le seguenti informazioni sul prodotto:

* **Integratore:** Adobe Systems, Inc.
* **Versione integratore:** 1,0
* **Famiglia di applicazioni:** Acrobat
* **Nome applicazione:** Acrobat
* **Versione applicazione:** 9.0.0

**Estensioni di Acrobat Reader DC per Microsoft Office**

Le estensioni Acrobat Reader DC per Microsoft Office sono un plug-in utilizzato con i prodotti Microsoft Office Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Quando richiede un servizio, fornisce le seguenti informazioni:

* **Integratore:** Adobe Systems Incorporated
* **Versione integratore:** 8.2
* **Famiglia di applicazioni:** Estensioni di Acrobat Reader DC per Microsoft Office
* **Nome applicazione:** Microsoft Word, Microsoft Excel o Microsoft PowerPoint
* **Versione applicazione:** 2003 o 2007

**Configurare la protezione dei documenti per negare i servizi per applicazioni specifiche**

1. Esportare il file di configurazione della protezione del documento. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)
1. Apri il file di configurazione in un editor e individua il `PolicyServer` nodo. Aggiungi un `ClientVersionRules` nodo come figlio immediato del `PolicyServer` nodo, se non esiste:

   ```java
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

   `APPFamilies` è definita dall&#39;API client.

   `AppName`specifica il nome dell&#39;applicazione client. Le virgole vengono utilizzate come separatori di nomi. Per includere una virgola in un nome, eseguitene l&#39;escape con un carattere barra rovesciata (\). Ad esempio, *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` specifica la versione dell&#39;applicazione client.

   `Integrators` specifica il nome della società o del gruppo che ha sviluppato il plug-in o l&#39;applicazione integrata.

   `IntegratorVersions` è la versione del plug-in o dell&#39;applicazione integrata.

1. Per ogni ulteriore set di dati di rifiuto, aggiungere un altro elemento *MyEntryName* .
1. Salvate il file di configurazione.
1. Importa il file di configurazione. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)

**Esempi**

In questo esempio, a tutti i client Windows viene negato l&#39;accesso.

```java
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

In questo esempio, l&#39;accesso alla versione della mia applicazione 3.0 e alla versione della mia altra applicazione 2.0 non è consentito. Lo stesso URL negazioni informazioni viene utilizzato indipendentemente dal motivo del rifiuto.

```java
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

In questo esempio, tutte le richieste provenienti da un&#39;installazione di Microsoft PowerPoint 2007 o Microsoft PowerPoint 2010 di Acrobat Reader DC con estensioni per Microsoft Office vengono negate.

```java
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

### Modificare i parametri di configurazione della filigrana {#change-the-watermark-configuration-parameters}

Per impostazione predefinita, è possibile specificare fino a cinque elementi in una filigrana. Inoltre, la dimensione massima del file del documento PDF che si desidera utilizzare come filigrana è limitata a 100 KB. Potete modificare questi parametri nel file config.xml.

***nota **: È necessario modificare questi parametri con cautela.*

1. Esportare il file di configurazione della protezione del documento. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)
1. Apri il file di configurazione in un editor e individua il `ServerSettings` nodo.
1. Nel `ServerSettings` nodo, aggiungere le seguenti voci e salvare il file: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   La prima voce, *dimensione* massima del file, è la dimensione massima del file (in KB) consentita per un elemento filigrana PDF. Il valore predefinito è 100 KB.

   La seconda voce, *max elements* , è il numero massimo di elementi consentiti in una filigrana. Il valore predefinito è 5.

   ```java
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importa il file di configurazione. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)

### Disattivazione di collegamenti esterni {#disabling-external-links}

Molti utenti di Document Security non hanno accesso a collegamenti esterni, ad esempio **www.adobe.com** , mentre utilizzano le interfacce utente Right Management:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Le seguenti modifiche al file config.xml disattivano tutti i collegamenti esterni dalle interfacce utente Right Management.

1. Esportare il file di configurazione della protezione del documento. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)
1. Apri il file di configurazione in un editor e individua il `DisplaySettings` nodo.
1. Per disattivare tutti i collegamenti esterni, nel `DisplaySettings` nodo aggiungere la seguente voce e salvare il file: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```java
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importa il file di configurazione. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)

### Configurazione per abilitare SMTP per Transport Layer Security (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Le seguenti modifiche al file config.xml abilitano il supporto TLS per la funzione di registrazione degli utenti invitati.

1. Esportare il file di configurazione della protezione del documento. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)
1. Apri il file di configurazione in un editor e individua il `DisplaySettings` nodo.
1. Individua il nodo seguente: `<node name="ExternalUser">`

   ```java
   <node name="ExternalUser">
   ```

1. Impostate il valore della `SmtpUseTls` chiave nel `ExternalUser` nodo su **true**.
1. Impostate il valore della `SmtpUseSsl` chiave nel `ExternalUser` nodo su **false**.
1. Salva il `config.xml`.
1. Importa il file di configurazione. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)

### Disattivazione degli endpoint SOAP per i documenti di Document Security {#disable-soap-endpoints-for-document-security-documents}

Le seguenti modifiche al file config.xml per disabilitare gli endpoint SOAP per i documenti di protezione dei documenti.

1. Esportare il file di configurazione della protezione del documento. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)
1. Aprite il file di configurazione in un editor e individuate il seguente nodo: `<node name="DRM">`

   ```java
   <node name="DRM">
   ```

1. Nel nodo DRM, individuare il `entry` nodo:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Per disabilitare gli endpoint SOAP per i documenti di protezione, impostare l&#39;attributo value su **false**.

   ```java
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Salva il `config.xml`.
1. Importa il file di configurazione. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)

### Aumento della scalabilità del server di protezione dei documenti {#increasingscalability}

Per impostazione predefinita, durante la sincronizzazione di un documento per l&#39;uso offline, insieme alle informazioni per il documento corrente, i client di protezione dei documenti recuperano informazioni su criteri, filigrane, licenze e aggiornamenti di revoca per tutti gli altri documenti a cui l&#39;utente ha accesso. Se questi aggiornamenti e queste informazioni non vengono sincronizzati con il client, è possibile che un documento aperto in modalità offline si apra ancora con informazioni su criteri, filigrane e revoche meno recenti.

È possibile aumentare la scalabilità del server di protezione dei documenti limitando le informazioni inviate al client. La riduzione della quantità di informazioni inviate al client migliora la scalabilità, riduce i tempi di risposta e migliora le prestazioni del server. Per aumentare la scalabilità, effettuare le seguenti operazioni:

1. Esportare il file di configurazione della protezione del documento. (Vedere Modifica [manuale del file](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)
1. Aprite il file di configurazione in un editor e individuate il nodo ServerSettings.
1. Nel nodo ServerSettings, impostare il valore della `DisableGlobalOfflineSynchronizationData`proprietà su `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Se impostato su true, il server di protezione del documento invia informazioni solo per il documento corrente e le informazioni per il resto dei documenti (gli altri documenti a cui l&#39;utente ha accesso) non vengono inviate al client.

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore della `DisableGlobalOfflineSynchronizationData`chiave è impostato su `false`.

1. Salvate e importate il file di configurazione. (Vedere Modifica [manuale del file](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)di configurazione per la protezione dei documenti.)

