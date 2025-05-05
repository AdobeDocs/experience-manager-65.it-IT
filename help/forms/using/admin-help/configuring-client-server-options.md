---
title: Configurazione delle opzioni client e server
description: Scopri come configurare le varie opzioni client e server, ad esempio le impostazioni di configurazione del server, i ruoli di protezione dei documenti e il controllo degli eventi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '10278'
ht-degree: 0%

---

# Configurare il server di Document Security {#configure-the-document-security-server}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Configurazione server.
1. Configurare le impostazioni e fare clic su OK.

## Impostazioni di configurazione server {#server-configuration-settings}

**URL di base:** URL di base per la protezione dei documenti, contenente il nome del server e la porta. Le informazioni aggiunte alla base creano gli URL di connessione. Ad esempio, viene aggiunto /edc/Main.do per accedere alle pagine web. Gli utenti rispondono anche agli inviti di registrazione degli utenti esterni tramite questo URL.

Se si utilizza IPv6, immettere l&#39;URL di base come nome del computer o il nome DNS. Se utilizzi un indirizzo IP numerico, Acrobat non riuscirà ad aprire i file protetti tramite policy. Utilizza anche l’URL HTTP protetto (HTTPS) per il server.

>[!NOTE]
>
>L’URL di base è incorporato in file protetti tramite policy. Le applicazioni client utilizzano l&#39;URL di base per riconnettersi al server. I file protetti continueranno a contenere l’URL di base, anche se viene modificato in seguito. Se modifichi l’URL di base, le informazioni di configurazione devono essere aggiornate per tutti i client di connessione.

**Periodo di lease non in linea predefinito:** Periodo di tempo predefinito per cui un utente può utilizzare un documento protetto non in linea. Questa impostazione determina il valore iniziale dell&#39;impostazione del periodo di lease per l&#39;attivazione automatica della modalità offline quando si crea un criterio. Consulta Creazione e modifica di criteri. Alla scadenza del periodo di lease, il destinatario deve sincronizzare nuovamente il documento per continuare a utilizzarlo.

Per una discussione sul funzionamento del lease e della sincronizzazione offline, vedere [Introduzione alla configurazione del lease e della sincronizzazione offline](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Periodo di sincronizzazione offline predefinito:** il tempo massimo per l&#39;utilizzo non in linea di un documento dal momento in cui è inizialmente protetto.

**Timeout sessione client:** periodo di tempo, in minuti, trascorso il quale la protezione dei documenti si disconnette se un utente che ha eseguito l&#39;accesso tramite un&#39;applicazione client non interagisce con la protezione dei documenti.

**Consenti accesso utenti anonimi:** Selezionare questa opzione per consentire la creazione di criteri personali e condivisi che consentano agli utenti anonimi di aprire documenti protetti tramite policy. Gli utenti che non dispongono di account possono accedere al documento, ma non possono accedere alla protezione dei documenti o utilizzare altri documenti protetti tramite policy.

**Disabilita accesso ai client versione 7:** Specifica se gli utenti possono utilizzare Acrobat o Reader 7.0 per connettersi al server. Quando questa opzione è selezionata, gli utenti devono utilizzare Acrobat o Reader 8.0 e versioni successive per completare le operazioni di sicurezza dei documenti sui documenti PDF. Se i criteri richiedono che Acrobat o Reader 8.0 e versioni successive vengano eseguiti in modalità certificata all’apertura di documenti protetti tramite policy, disabilita l’accesso ad Acrobat o Reader 7. Consultate Specificare le autorizzazioni del documento per utenti e gruppi.

**Consenti accesso offline per documento** Selezionare questa opzione per specificare l&#39;accesso offline per documento. Se questa impostazione è abilitata, l&#39;utente avrà accesso offline solo ai documenti che ha aperto online almeno una volta.

**Consenti autenticazione password nome utente:** Selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione nome utente/password durante la connessione al server.

**Consenti autenticazione Kerberos:** Selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione Kerberos durante la connessione al server.

**Consenti autenticazione certificato client:** Selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione dei certificati durante la connessione al server.

**Consenti autenticazione estesa** Selezionare questa opzione per abilitare l&#39;autenticazione estesa, quindi immettere l&#39;URL di destinazione dell&#39;autenticazione estesa.

Se si seleziona questa opzione, le applicazioni client potranno utilizzare l&#39;autenticazione estesa. L’autenticazione estesa fornisce processi di autenticazione personalizzati e diverse opzioni di autenticazione configurate sul server AEM Forms. Ad esempio, ora gli utenti possono utilizzare l’autenticazione basata su SAML invece dei moduli AEM nome utente/password di Acrobat e client di Reader. Per impostazione predefinita, l&#39;URL di destinazione contiene *localhost* come nome del server. Sostituisci il nome del server con un nome host completo. Se l’autenticazione estesa non è ancora abilitata, il nome host nell’URL di destinazione viene popolato automaticamente dall’URL di base. Vedere [Aggiungere il provider di autenticazione estesa](configuring-client-server-options.md#add-the-extended-authentication-provider).

***nota &#x200B;**: l&#39;autenticazione estesa è supportata in Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.*

**Larghezza controllo HTML preferenziale per autenticazione estesa** Specificare la larghezza della finestra di dialogo di autenticazione estesa che si apre in Acrobat per l&#39;immissione delle credenziali utente.

**Altezza controllo HTML preferito per autenticazione estesa** Specificare l&#39;altezza della finestra di dialogo di autenticazione estesa che si apre in Acrobat per l&#39;immissione delle credenziali utente.

***nota &#x200B;**: i limiti di larghezza e altezza per questa finestra di dialogo sono i seguenti:*
Larghezza: minima = 400, massima = 900

Altezza: minima = 450; massima = 800

**Abilita caching credenziali client:** Selezionare questa opzione per consentire agli utenti di memorizzare le credenziali nella cache (nome utente e password). Quando le credenziali degli utenti vengono memorizzate nella cache, non è necessario immetterle ogni volta che aprono un documento o quando si fa clic sul pulsante Aggiorna nella pagina Gestisci criteri di sicurezza di Adobe Acrobat. È possibile specificare il numero di giorni prima che gli utenti debbano fornire nuovamente le credenziali. Se si imposta il numero di giorni su 0, le credenziali possono essere memorizzate nella cache a tempo indefinito.

## Configurazione di utenti e amministratori di Document Security {#configuring-document-security-users-and-administrators}

### Assegnazione di ruoli di protezione dei documenti agli amministratori {#assigning-document-security-roles-to-administrators}

L’ambiente dei moduli AEM contiene uno o più utenti amministratori che dispongono dei privilegi appropriati per la creazione di utenti e gruppi. Se la tua organizzazione utilizza la protezione dei documenti, è necessario assegnare ad almeno un amministratore il privilegio di gestire gli utenti invitati e locali.

Gli amministratori devono inoltre disporre del ruolo Utente della console di amministrazione per accedere alla console di amministrazione. (Vedi [Creazione e configurazione dei ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configurazione di utenti e gruppi visibili {#configuring-visible-users-and-groups}

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti dei criteri, un amministratore privilegiato o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati in Gestione utente) all&#39;elenco visibile di utenti e gruppi per ogni set di criteri.

L’elenco visibile di utenti e gruppi è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l’utente finale può sfogliare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà alcun utente o gruppo da aggiungere al criterio. Per ogni set di criteri può essere presente più di un coordinatore.

1. Dopo aver installato e configurato l’ambiente dei moduli AEM con la protezione dei documenti, imposta tutti i domini appropriati in Gestione utente. <!-- Fix broken link (See Setting up and managing domains) -->

   ***nota &#x200B;**: prima di creare i criteri è necessario creare i domini.*

1. Nella console di amministrazione, fai clic su Servizi > Gestione documenti > Criteri, quindi fai clic sulla scheda Set di criteri.
1. Selezionare Set di criteri globale, quindi fare clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.
1. Passa a Servizi > Document Security > Configurazione > I miei criteri e fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.

## Aggiungere il provider di autenticazione estesa {#add-the-extended-authentication-provider}

I moduli AEM forniscono una configurazione di esempio che puoi personalizzare per il tuo ambiente. Effettua le seguenti operazioni:

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

1. Ottieni il file WAR di esempio per distribuirlo. Vedere la guida all&#39;installazione appropriata per il server applicazioni.
1. Verificare che l&#39;URL di base del server Forms sia un URL completo e non un indirizzo IP e che si tratti di un URL HTTPS. Vedere [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).
1. Abilitare l&#39;autenticazione estesa dalla pagina Configurazione server. Vedere [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).
1. Aggiungi gli URL di reindirizzamento SSO richiesti nel file di configurazione di User Management. Consulta [Aggiungi URL di reindirizzamento SSO per l&#39;autenticazione estesa](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Aggiungere URL di reindirizzamento SSO per l’autenticazione estesa {#add-sso-redirect-urls-for-extended-authentication}

Se l’autenticazione estesa è abilitata, gli utenti che aprono un documento protetto tramite policy in Acrobat XI o nel Reader XI visualizzano una finestra di dialogo per l’autenticazione. Questa finestra di dialogo carica la pagina HTML specificata come URL di destinazione per l’autenticazione estesa nelle impostazioni del server di protezione dei documenti. Vedere [Impostazioni di configurazione del server](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Fare clic su Esporta e salvare il file di configurazione sul disco.
1. Apri il file in un editor e individua il nodo AllowedUrls.
1. Nel nodo `AllowedUrls` aggiungere le righe seguenti: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Salva il file e importa il file aggiornato dalla pagina Configurazione manuale: nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.

## Configurazione della sicurezza offline {#configuring-offline-security}

document security consente di utilizzare documenti protetti tramite policy in modalità non in linea senza una connessione Internet o di rete. Questa capacità richiede che i criteri consentano l&#39;accesso offline, come descritto in [Specificare le autorizzazioni del documento per utenti e gruppi](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Prima che un documento che dispone di tale criterio possa essere utilizzato in modalità non in linea, il destinatario deve aprire il documento in modalità in linea e attivare l&#39;accesso non in linea facendo clic su Sì quando richiesto. Al destinatario può anche essere richiesto di autenticare la sua identità. Il destinatario può quindi utilizzare i documenti offline per la durata del periodo di lease specificato nel criterio.

Al termine del periodo di lease offline, il destinatario deve sincronizzarsi nuovamente con document security aprendo un documento online o utilizzando un comando di menu delle estensioni di Acrobat o Acrobat Reader DC per eseguire la sincronizzazione. (Vedi *Guida di Acrobat* o la *Guida delle estensioni di Acrobat Reader DC* appropriata.)

Poiché i documenti che consentono l&#39;accesso offline richiedono la memorizzazione nella cache del materiale chiave nel computer in cui sono memorizzati i file offline, il file potrebbe essere compromesso se un utente non autorizzato può ottenere il materiale chiave. Per compensare questa possibilità, sono disponibili opzioni di rollover della chiave pianificate e manuali che è possibile configurare per impedire a persone non autorizzate di utilizzare la chiave per accedere al documento.

### Imposta un periodo di lease offline predefinito {#set-a-default-offline-lease-period}

I destinatari dei documenti protetti tramite policy possono disconnettere i documenti per il numero di giorni specificato nella policy. Dopo la sincronizzazione iniziale del documento con document security, il destinatario può utilizzarlo offline fino alla scadenza del periodo di lease offline. Alla scadenza del periodo di lease, il destinatario deve portare il documento online e accedere per sincronizzarsi con document security per continuare a utilizzare il documento.

Puoi configurare un periodo di lease offline predefinito. Il periodo di lease può essere modificato dal valore predefinito quando chiunque crea o modifica una policy.

1. Nella pagina di document security, fai clic su Configurazione > Configurazione server.
1. Nella casella Periodo lease non in linea predefinito digitare il numero di giorni per il periodo di lease non in linea.
1. Fare clic su OK.

### Gestire i rollover chiave {#manage-key-rollovers}

Document Security utilizza algoritmi di crittografia e licenze per proteggere i documenti. Quando crittografa un documento, Document Security genera e gestisce una chiave di decrittografia denominata *DocKey* che passa all&#39;applicazione client. Se il criterio che protegge un documento consente l&#39;accesso non in linea, viene generata anche una chiave non in linea denominata *chiave principale* per ogni utente che dispone dell&#39;accesso non in linea al documento.

>[!NOTE]
>
>Se non esiste una chiave principale, Document Security ne genera una per proteggere un documento.

Per aprire un documento protetto tramite policy in modalità non in linea, è necessario che il computer dell&#39;utente disponga della chiave principale appropriata. Il computer ottiene la chiave principale quando l’utente si sincronizza con document security (apre un documento protetto online). Se questa chiave principale è compromessa, anche qualsiasi documento a cui l&#39;utente ha accesso offline potrebbe essere compromesso.

Un modo per ridurre la minaccia per i documenti offline consiste nell&#39;evitare di consentire l&#39;accesso offline a documenti particolarmente sensibili. Un altro metodo consiste nel far scorrere periodicamente le chiavi principali. Quando Document Security passa il tasto, tutte le chiavi esistenti non possono più accedere ai documenti protetti tramite policy. Ad esempio, se un autore ottiene una chiave principale da un laptop rubato, tale chiave non può essere utilizzata per accedere ai documenti protetti dopo il rollover. Se si sospetta che una chiave principale specifica sia stata compromessa, è possibile eseguire manualmente il rollover della chiave.

Tuttavia, un rollover della chiave influisce su tutte le chiavi principali, non solo su una. Inoltre, riduce la scalabilità del sistema perché i client devono memorizzare più chiavi per l’accesso offline. La frequenza predefinita di rollover della chiave è di 20 giorni. Si consiglia di non impostare questo valore su un valore inferiore a 14 giorni, poiché potrebbe essere impedita la visualizzazione dei documenti offline agli utenti e le prestazioni del sistema potrebbero risentirne.

Nell&#39;esempio seguente, Chiave1 è la prima delle due chiavi principali e Chiave2 è la più recente. Quando si fa clic sul pulsante Rollover chiavi ora la prima volta, la chiave 1 non è più valida e viene generata una nuova chiave principale valida (chiave 3). Gli utenti otterranno Key3 quando eseguono la sincronizzazione con la protezione dei documenti, in genere aprendo un documento protetto online. Tuttavia, gli utenti non sono costretti a sincronizzarsi con la protezione dei documenti fino a quando non raggiungono il periodo di lease offline massimo specificato in una policy. Dopo il primo passaggio chiave, gli utenti che rimangono offline possono comunque aprire i documenti offline, inclusi quelli protetti da Key3, fino a raggiungere il periodo massimo di lease offline. Quando si fa nuovamente clic sul pulsante Rollover tasti ora, la chiave 2 non è più valida e viene creata la chiave 4. Gli utenti che rimangono offline durante i due rollover chiave non possono aprire i documenti protetti con Chiave3 o Chiave4 finché non si sincronizzano con la protezione dei documenti.

**Modifica la frequenza di rollover della chiave**

Per motivi di riservatezza, quando si utilizzano documenti offline, la protezione dei documenti fornisce un’opzione di rollover automatico della chiave con un periodo di frequenza predefinito di 20 giorni. È possibile modificare la frequenza di rollover; tuttavia, evitare di impostare un valore inferiore a 14 giorni, in quanto potrebbe essere impedita la visualizzazione dei documenti offline agli utenti e le prestazioni del sistema potrebbero risentirne.

1. Nella pagina Document Security, fai clic su Configurazione > Key Management (Gestione chiavi).
1. Nella casella Frequenza rollover chiave digitare il numero di giorni per il periodo di rollover.
1. Fare clic su OK.

**Eseguire manualmente il rollover delle chiavi principali**

Per mantenere la riservatezza dei documenti non in linea, è possibile eseguire manualmente il rollover delle chiavi principali. Potrebbe essere necessario eseguire manualmente il rollover di una chiave (ad esempio, se viene compromessa da un utente che la ottiene da un computer in cui è memorizzata nella cache per consentire l&#39;accesso offline a un documento).

>[!NOTE]
>
>Evitare di utilizzare frequentemente il rollover manuale, in quanto causa il rollover di tutte le chiavi principali, non solo di una, e può impedire temporaneamente agli utenti di visualizzare nuovi documenti offline.

È necessario eseguire il rollover delle chiavi principali due volte prima che le chiavi esistenti nei computer client vengano invalidate. I computer client che hanno invalidato le chiavi principali devono sincronizzarsi nuovamente con il servizio di sicurezza dei documenti per acquisire le nuove chiavi principali.

1. Nella pagina Document Security, fai clic su Configurazione > Key Management (Gestione chiavi).
1. Fare clic su Rollover tasti e quindi su OK.
1. Attendere circa 10 minuti. Nel registro del server viene visualizzato il seguente messaggio: `Done RightsManagement key rollover for`*N* `principals`. Dove *N* è il numero di utenti nel sistema di protezione dei documenti.
1. Fare clic su Rollover tasti e quindi su OK.
1. Attendere circa 10 minuti.

## Configurazione del controllo degli eventi e delle impostazioni della privacy {#configuring-event-auditing-and-privacy-settings}

Document Security consente di controllare e registrare informazioni su eventi correlati all’interazione con documenti, policy, amministratori e server protetti tramite policy. È possibile configurare il controllo degli eventi e specificare i tipi di eventi da controllare. Per controllare gli eventi di un determinato documento, è necessario abilitare anche l&#39;opzione di controllo relativa al criterio.

Quando il controllo è abilitato, è possibile visualizzare i dettagli degli eventi controllati nella pagina Eventi. gli utenti di document security possono anche visualizzare eventi correlati in modo specifico ai documenti protetti tramite policy che utilizzano o creano.

È possibile selezionare i seguenti tipi di eventi per il controllo:

* Eventi di documenti protetti tramite policy, ad esempio tentativi di apertura di documenti da parte di utenti autorizzati o non autorizzati
* Eventi relativi ai criteri, ad esempio creazione, modifica, eliminazione, abilitazione e disabilitazione dei criteri
* Eventi utente, ad esempio inviti e registrazioni di utenti esterni, account utente attivati e disattivati, modifiche alle password utente e aggiornamenti del profilo
* L’AEM forma eventi quali mancate corrispondenze tra le versioni, provider di autorizzazioni e server delle directory non disponibili e modifiche alla configurazione del server

### Attiva o disattiva il controllo degli eventi {#enable-or-disable-event-auditing}

È possibile abilitare e disabilitare il controllo degli eventi correlati al server, ai documenti protetti tramite policy, alle policy, ai set di policy e agli utenti. Quando abiliti il controllo degli eventi, puoi scegliere di controllare tutti i possibili eventi oppure selezionare eventi specifici da controllare.

Quando si abilita il controllo del server, è possibile visualizzare gli eventi controllati nella pagina Eventi.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Impostazioni controllo e privacy.
1. Per configurare il controllo del server, in Abilita controllo server selezionare Sì o No.
1. Se hai selezionato Sì, in ciascuna categoria di eventi, effettua una delle seguenti azioni per selezionare le opzioni da controllare:

   * Per controllare tutti gli eventi nella categoria, seleziona Tutto.
   * Per controllare solo alcuni eventi, deselezionare Tutti, quindi selezionare le caselle di controllo accanto agli eventi che si desidera controllare.

     (Vedi [Opzioni di controllo degli eventi](configuring-client-server-options.md#event-auditing-options).)

1. Fare clic su OK.

>[!NOTE]
>
>Quando si lavora con le pagine Web, evitare di utilizzare i pulsanti del browser, ad esempio il pulsante Indietro, il pulsante di aggiornamento e la freccia Indietro o Avanti perché questa azione può causare problemi indesiderati di acquisizione e visualizzazione dei dati.

### Abilita o disabilita le notifiche sulla privacy {#enable-or-disable-privacy-notification}

Puoi abilitare e disabilitare un messaggio di notifica della privacy. Quando si abilita la notifica della privacy, viene visualizzato un messaggio quando un destinatario tenta di aprire un documento protetto tramite policy. L&#39;avviso informa l&#39;utente che è in corso il controllo dell&#39;utilizzo del documento. Puoi anche specificare un URL che l’utente può utilizzare per visualizzare la pagina dell’informativa sulla privacy, se disponibile.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Impostazioni controllo e privacy.
1. Per configurare la notifica di accesso a dati personali, in Abilita notifica di accesso a dati personali selezionare Sì o No.

   Se la policy associata a un documento consente l’accesso anonimo e l’opzione Abilita informativa sulla privacy è impostata su No, all’utente non viene richiesto di effettuare l’accesso e il messaggio di notifica della privacy non viene visualizzato.

   Se la policy allegata a un documento non consente l’accesso anonimo, l’utente visualizzerà il messaggio di notifica della privacy.

1. Se applicabile, nella casella URL privacy, digita l’URL della pagina dell’informativa sulla privacy. Se la casella URL privacy viene lasciata vuota, viene visualizzata la pagina relativa alla privacy disponibile all’indirizzo adobe.com.
1. Fare clic su OK.

>[!NOTE]
>
>La disattivazione dell&#39;informativa sulla privacy non disattiva il controllo dell&#39;utilizzo dei documenti. Le azioni di controllo predefinite e le azioni personalizzate supportate tramite il tracciamento dell’utilizzo esteso possono comunque raccogliere informazioni sul comportamento dell’utente.

### Importare un tipo di evento di audit personalizzato {#import-a-custom-audit-event-type}

Se utilizzi un’applicazione abilitata per la protezione dei documenti che supporta il controllo di eventi aggiuntivi, ad esempio eventi specifici di un determinato tipo di file, un partner Adobe può fornirti eventi di controllo personalizzati che puoi importare in document security. Utilizza questa funzione solo se un partner Adobe ti ha fornito tipi di evento personalizzati.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Gestione eventi.
1. Fare clic su Sfoglia per passare al file XML da importare e fare clic su Importa.
1. L’importazione sovrascrive i tipi di evento di controllo personalizzati esistenti sul server se vengono trovate combinazioni identiche di codice evento e spazio dei nomi.
1. Fare clic su OK.

### Eliminare un tipo di evento di audit personalizzato {#delete-a-custom-audit-event-type}

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Gestione eventi.
1. Seleziona la casella di controllo accanto al tipo di evento di controllo personalizzato da eliminare e fai clic su Elimina.
1. Fare clic su OK.

### Esporta eventi di audit {#export-audit-events}

È possibile esportare gli eventi di controllo in un file a scopo di archiviazione.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Gestione eventi.
1. Modifica le impostazioni in Esporta eventi di controllo secondo necessità. Puoi specificare:

   * età minima degli eventi di audit da esportare
   * il numero massimo di eventi di controllo da includere in un singolo file. Il server genera uno o più file in base a questo valore.
   * la cartella in cui verrà creato il file. Questa cartella si trova sul server Forms. Se il percorso della cartella è relativo, è relativo alla directory principale del server applicazioni.
   * prefisso del file da utilizzare per i file degli eventi di controllo
   * il formato del file, un file con valori separati da virgole (CSV) compatibile con Microsoft Excel o un file XML.

1. Fai clic su Esporta. Se si desidera annullare l&#39;esportazione, fare clic su Annulla esportazione. Se un altro utente ha pianificato un’esportazione, il pulsante Annulla esportazione non è disponibile fino al completamento dell’esportazione. Il pulsante Annulla esportazione non è disponibile se un altro utente ha pianificato un’esportazione. Per verificare se è stata avviata o completata un&#39;esportazione o un&#39;eliminazione pianificata, fare clic su Aggiorna.

### Eliminare gli eventi di audit {#delete-audit-events}

È possibile eliminare gli eventi di audit precedenti a un numero specificato di giorni.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Gestione eventi.
1. In Elimina eventi di controllo specificare il numero di giorni nella casella Elimina eventi di controllo precedenti a.
1. Fai clic su Elimina. Fai clic su Esporta. Se si desidera annullare l&#39;eliminazione, fare clic su Annulla eliminazione. Se un altro utente ha pianificato un’eliminazione, il pulsante Annulla eliminazione non è disponibile fino al completamento dell’esportazione. Il pulsante Annulla eliminazione non è disponibile se un altro utente ha pianificato un’esportazione. Per verificare se è stata avviata o completata un&#39;eliminazione pianificata, fare clic su Aggiorna.

### Opzioni di controllo degli eventi {#event-auditing-options}

È possibile abilitare e disabilitare il controllo degli eventi e specificare i tipi di eventi da controllare.

**Eventi documento**

**Visualizza documento:** Un destinatario visualizza un documento protetto tramite policy.

**Chiudi documento:** Un destinatario chiude un documento protetto tramite policy.

**Stampa a bassa risoluzione** Un destinatario stampa un documento protetto tramite policy con l&#39;opzione a bassa risoluzione specificata.

**Stampa ad alta risoluzione:** Un destinatario stampa un documento protetto tramite policy con l&#39;opzione ad alta risoluzione specificata.

**Aggiungi annotazione al documento:** Un destinatario aggiunge un&#39;annotazione a un documento PDF.

**Revoca documento:** Un utente o un amministratore revoca l&#39;accesso a un documento protetto tramite policy.

**Annullamento della revoca del documento:** Un utente o un amministratore ripristina l&#39;accesso a un documento protetto tramite policy.

**Compilazione modulo:** un destinatario immette informazioni in un documento di PDF che è un modulo compilabile.

**Criterio rimosso:** Un editore rimuove un criterio da un documento per revocare le protezioni di protezione.

**Cambia URL revoca documento:** Una chiamata dal livello API modifica l&#39;URL di revoca specificato per accedere a un nuovo documento che sostituisce un documento revocato.

**Modifica documento:** Un destinatario modifica il contenuto di un documento protetto tramite policy.

**Firma documento:** Un destinatario firma un documento.

**Proteggere un nuovo documento:** Un utente applica una policy per proteggere un documento.

**Cambia criterio nel documento:** Un utente o un amministratore cambia il criterio associato a un documento.

**Documento Publish con nome:** Un nuovo documento con nome documento e licenza identici a quelli di un documento esistente è registrato nel server e i documenti non hanno una relazione padre-figlio. Questo evento può essere attivato utilizzando i moduli SDK dell’AEM.

**Itera documento:** Un nuovo documento con documentName e licenza identici a un documento esistente è registrato nel server e i documenti hanno una relazione padre-figlio. Questo evento può essere attivato utilizzando i moduli SDK dell’AEM.

**Eventi criteri**

**Criterio creato:** Un utente o un amministratore crea un criterio.

**Criterio abilitato:** Un amministratore rende disponibile un criterio.

**Criterio modificato:** Un utente o un amministratore modifica un criterio.

**Criterio disabilitato:** Un amministratore ha reso non disponibile un criterio.

**Criterio eliminato:** Un utente o un amministratore elimina un criterio.

**Modifica proprietario criterio:** Una chiamata dal livello API cambia il proprietario del criterio.

**Eventi utente**

**Utente eliminato:** Un amministratore elimina un account utente.

**Registra utente invitato:** un utente esterno si registra con Document Security.

**Accesso riuscito:** tentativi di accesso riusciti da parte di amministratori o utenti.

**Utenti invitati:** Document Security invita un utente a registrarsi.

**Utenti attivati:** Gli utenti esterni attivano i loro account utilizzando l&#39;URL nell&#39;e-mail di attivazione oppure un amministratore abilita un account.

**Modifica password:** Gli utenti invitati modificano le proprie password o un amministratore reimposta una password per un utente locale.

**Accesso non riuscito:** tentativi di accesso non riusciti da parte di amministratori o utenti.

**Utenti disattivati:** Un amministratore disabilita un account utente locale.

**Aggiornamento profilo:** gli utenti invitati modificano nome, nome organizzazione e password.

**Account bloccato:** Un amministratore blocca un account.

**Eventi set di criteri**

**creato
Set di criteri:** Un amministratore o un coordinatore di set di criteri crea un set di criteri.

**Set di criteri eliminato:** Un amministratore o un coordinatore di set di criteri elimina un set di criteri.

**Set di criteri modificato:** Un amministratore o un coordinatore di set di criteri modifica un set di criteri.

**Eventi di sistema**

Directory **Sincronizzazione completata:** Queste informazioni non sono disponibili nella pagina Eventi. Le informazioni sulla sincronizzazione della directory corrente, inclusi lo stato di sincronizzazione corrente e l&#39;ora dell&#39;ultima sincronizzazione, vengono visualizzate nella pagina Gestione dominio. Per accedere alla pagina Gestione dominio nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

**Accesso offline abilitato client:** Un utente ha abilitato l&#39;accesso offline ai documenti protetti dal server nel computer dell&#39;utente.

**Client sincronizzato** L&#39;applicazione client deve sincronizzare le informazioni con il server per consentire l&#39;accesso offline.

**Mancata corrispondenza versione:** Una versione di AEM form SDK non compatibile con il server ha tentato la connessione al server.

**Informazioni sulla sincronizzazione della directory:** Queste informazioni non sono disponibili nella pagina Eventi. Le informazioni sulla sincronizzazione della directory corrente, inclusi lo stato di sincronizzazione corrente e l&#39;ora dell&#39;ultima sincronizzazione, vengono visualizzate nella pagina Gestione dominio. Per accedere alla pagina Gestione dominio nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.

**Modifica configurazione server:** modifiche alla configurazione del server eseguite tramite pagine Web o manualmente importando un file config.xml. Ciò include modifiche all’URL di base, timeout della sessione, blocchi di accesso, impostazioni della directory, rollover delle chiavi, impostazioni del server SMTP per la registrazione esterna, configurazione delle filigrane, opzioni di visualizzazione e così via.

## Configurazione del tracciamento dell’utilizzo esteso {#configuring-extended-usage-tracking}

Document Security consente di tenere traccia di vari eventi personalizzati che possono essere eseguiti su un documento protetto. È possibile abilitare il tracciamento degli eventi dal server di Document Security a livello globale o a livello di policy. È quindi possibile impostare un JavaScript per acquisire azioni specifiche eseguite all’interno del documento protetto di PDF, ad esempio facendo clic su un pulsante o salvando il documento. Questi dati di utilizzo vengono inviati come file XML in coppie chiave-valore, che puoi utilizzare per ulteriori analisi. Gli utenti finali che accedono ai documenti protetti possono consentire o rifiutare tale tracciamento dall’applicazione client.

Se il tracciamento è abilitato a livello globale, è possibile ignorare questa impostazione a livello di criterio e disabilitarla per un criterio specifico. L’override a livello di criterio non è possibile se il tracciamento è disabilitato a livello globale. L&#39;elenco degli eventi tracciati viene inviato automaticamente al server quando il numero di eventi raggiunge i 25 o quando il documento viene chiuso. Puoi anche configurare lo script per inviare esplicitamente l’elenco degli eventi in base alle tue esigenze. È possibile personalizzare il tracciamento degli eventi accedendo alle proprietà e ai metodi dell&#39;oggetto di protezione del documento.

Dopo aver abilitato il tracciamento, per impostazione predefinita il tracciamento viene attivato per tutti i criteri creati successivamente. I criteri creati prima dell’abilitazione del tracciamento sul server avranno bisogno di aggiornamenti manuali.

### Abilita o disabilita il tracciamento dell&#39;utilizzo esteso {#enable-or-disable-extended-usage-tracking}

Prima di iniziare, verificare che Server Auditing sia abilitato. Per ulteriori informazioni sul controllo, vedere [Configurazione del controllo degli eventi e delle impostazioni di privacy](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Impostazioni controllo e privacy.
1. Per configurare il tracciamento dell&#39;utilizzo esteso, in Abilita tracciamento selezionare Sì o No.
1. Per impostare la selezione della casella di controllo Consenti raccolta di dati di utilizzo dettagliati nella pagina di accesso, in Attiva impostazione predefinita tracciamento selezionare Sì o No.

Per visualizzare gli eventi tracciati è possibile utilizzare il filtro Eventi documento nella pagina Eventi. Gli eventi tracciati con JavaScript sono etichettati come Tracciamento dettagliato dell’utilizzo. Per ulteriori informazioni sugli eventi, consultare [Eventi di monitoraggio](/help/forms/using/admin-help/monitoring-events.md#monitoring-events).

## Configurare le impostazioni di visualizzazione di Document Security {#configure-document-security-display-settings}

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Opzioni di visualizzazione.
1. Configurare le impostazioni e fare clic su OK.

### Impostazioni di visualizzazione {#display-settings}

**Righe da visualizzare per i risultati della ricerca:** Numero di righe visualizzate in una pagina durante l&#39;esecuzione delle ricerche.

**Finestra di dialogo Personalizzazione per accesso client**

Queste impostazioni controllano il testo visualizzato nel prompt di accesso visualizzato quando un utente accede a document security tramite un’applicazione client.

**Testo di benvenuto:** Il testo del messaggio di benvenuto, ad esempio &quot;Accedi con il nome utente e la password&quot;. Il testo del messaggio di benvenuto deve contenere informazioni su come accedere a document security e come contattare un amministratore o un’altra persona di supporto designata nella tua organizzazione per assistenza. Ad esempio, gli utenti esterni potrebbero dover contattare un amministratore se dimenticano le password o hanno bisogno di assistenza per la registrazione o il processo di accesso. La lunghezza massima del testo di benvenuto è di 512 caratteri.

**Testo nome utente:** Etichetta di testo per la casella del nome utente.

**Testo password:** Etichetta di testo per la casella della password.

**Finestra di dialogo Personalizzazione per autenticazione certificato client**

Queste impostazioni controllano il testo visualizzato nella finestra di dialogo Autenticazione certificato.

**Scegli
Testo tipo di autenticazione:** Testo visualizzato per indirizzare un utente alla selezione di un tipo di autenticazione.

**Scegli testo certificato:** Testo visualizzato per indirizzare un utente alla selezione di un tipo di certificato.

**Testo errore certificati non disponibili:** Messaggio contenente un massimo di 512 caratteri da visualizzare quando il certificato selezionato non è disponibile.

**Personalizzazione per la visualizzazione del certificato client**

**Visualizza solo emittenti di credenziali attendibili:** Quando questa opzione è selezionata, l&#39;applicazione client presenta all&#39;utente solo certificati di emittenti di credenziali configurati per l&#39;attendibilità dei moduli AEM (vedere Gestione di certificati e credenziali). Se questa opzione non è selezionata, all&#39;utente viene presentato un elenco di tutti i certificati presenti nel sistema dell&#39;utente.

## Configurare le filigrane dinamiche {#configure-dynamic-watermarks}

Document Security consente di configurare le impostazioni predefinite per l’opzione della filigrana dinamica che è possibile applicare durante la creazione dei criteri. Una *filigrana* è un&#39;immagine sovrapposta al testo nel documento. È utile per tenere traccia del contenuto di un documento e può aiutare a identificare l’utilizzo illegale del contenuto.

Una filigrana dinamica può essere costituita da testo costituito da variabili definite, ad esempio ID utente e data e testo personalizzato, oppure da contenuto RTF all’interno di un PDF. È possibile configurare filigrane con diversi elementi, ciascuno con il proprio posizionamento e formattazione.

Le filigrane non sono modificabili e pertanto rappresentano un metodo più sicuro per garantire la riservatezza del contenuto del documento. Le filigrane dinamiche garantiscono inoltre che una filigrana mostri un numero sufficiente di informazioni specifiche per l’utente da fungere da deterrente per l’ulteriore distribuzione del documento.

La filigrana specificata da una policy viene visualizzata nel documento protetto tramite policy quando un destinatario visualizza o stampa il documento. A differenza delle filigrane permanenti, una filigrana dinamica non viene mai salvata nel documento, il che offre la flessibilità necessaria durante la distribuzione di un documento in un ambiente Intranet per garantire che l’applicazione di visualizzazione visualizzi l’identità dell’utente specifico. Inoltre, se un documento ha più utenti, l&#39;utilizzo della filigrana dinamica consente di utilizzare un documento invece di più versioni, ciascuna con una filigrana diversa. La filigrana visualizzata riflette l&#39;identità dell&#39;utente corrente.

Le filigrane dinamiche sono diverse dalle filigrane che gli utenti possono aggiungere direttamente al documento in Acrobat. Il risultato è che in un documento protetto tramite policy è possibile avere due filigrane.

### Considerazioni durante la creazione di filigrane {#considerations-when-creating-watermarks}

È possibile creare filigrane dinamiche con più elementi filigrana, ognuno dei quali deve essere specificato come testo o PDF. È possibile includere fino a cinque elementi in una filigrana.

Se si sceglie una filigrana basata su testo, è possibile specificare diversi elementi all&#39;interno della filigrana con più voci di testo e specificare la posizione di ogni elemento. Assegna nomi significativi a questi elementi, ad esempio intestazione, piè di pagina e così via.

Se ad esempio si desidera specificare come filigrana un testo diverso nell&#39;intestazione, nel piè di pagina, nei margini e in tutto il documento, è possibile creare diversi elementi filigrana e specificarne la posizione. Se si desidera che l&#39;ID utente dell&#39;utente e la data corrente di accesso al documento vengano visualizzati nell&#39;intestazione, il nome della policy nel margine destro e un testo personalizzato &quot;CONFIDENTIAL&quot; vengano visualizzati in diagonale nel documento, è necessario definire elementi filigrana separati con testo come tipo e specificarne la formattazione e il posizionamento. Quando la filigrana viene applicata a un documento, tutti gli elementi della filigrana vengono applicati contemporaneamente al documento, nell&#39;ordine in cui vengono aggiunti alla filigrana.

In genere, le filigrane basate su PDF vengono utilizzate per includere contenuti grafici come loghi o simboli speciali come copyright o marchi registrati.

È possibile modificare i limiti relativi al numero di elementi della filigrana e alle dimensioni del file PDF modificando il file di configurazione per la protezione dei documenti. Consulta [Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Quando configurate le filigrane, tenete presente quanto segue:

* Non è possibile utilizzare un documento PDF protetto da password come elemento filigrana. Tuttavia, se la filigrana creata contiene altri elementi non protetti da password, questi verranno applicati come parte della filigrana.
* È possibile modificare la dimensione massima del file PDF da utilizzare come elemento filigrana. Tuttavia, i documenti PDF di grandi dimensioni utilizzati come filigrane compromettono le prestazioni durante la sincronizzazione offline dei documenti applicati con tali filigrane. Consulta [Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Come filigrana viene utilizzata solo la prima pagina del PDF selezionato. Verificare che le informazioni che si desidera vengano visualizzate come filigrana siano disponibili nella prima pagina.
* Anche se è possibile specificare il ridimensionamento del documento PDF, considerare le dimensioni e il layout della pagina del PDF se si intende utilizzarlo come filigrana nell&#39;intestazione, nel piè di pagina o nei margini.
* Quando specificate il nome del font, immettete il nome correttamente. I moduli AEM sostituiscono il tipo di carattere specificato se non è presente nel computer client in cui viene aperto il documento.
* Se come contenuto della filigrana è stato selezionato del testo, l&#39;impostazione dell&#39;opzione di ridimensionamento Adatta alla pagina non funziona per le pagine con larghezza diversa.
* Quando specificate il posizionamento degli elementi della filigrana, accertatevi che non vi siano più elementi con lo stesso posizionamento. Se due elementi della filigrana hanno lo stesso posizionamento, ad esempio il centro, essi appaiono sovrapposti sul documento e nell&#39;ordine in cui sono stati aggiunti alla filigrana.
* Quando specificate la dimensione e il tipo di carattere, accertatevi che la lunghezza del testo sia completamente visibile all&#39;interno della pagina. Il contenuto del testo viene riportato su nuove righe, in modo che il contenuto della filigrana che si intendeva presentare nei margini possa sovrapporsi alle aree di contenuto delle pagine. Tuttavia, se il documento viene aperto in Acrobat 9, il testo al di là della riga singola viene troncato.

### Limitazioni delle filigrane dinamiche {#limitations-of-dynamic-watermarks}

Alcune applicazioni client potrebbero non supportare le filigrane dinamiche. Consulta la Guida delle estensioni di Acrobat Reader DC appropriate. Inoltre, tieni presente quanto segue sulle versioni di Acrobat che supportano le filigrane dinamiche:

* Non è possibile utilizzare un documento PDF protetto da password come elemento filigrana.
* Le versioni di Acrobat e Adobe Reader precedenti alla 10 non supportano le seguenti funzioni per le filigrane:

   * Filigrane PDF
   * Più elementi nella filigrana (Testo/PDF)
   * Opzioni avanzate come intervallo di pagine o opzioni di visualizzazione
   * Opzioni di formattazione del testo, ad esempio il tipo di carattere, il nome e il colore specificati. Tuttavia, nelle versioni precedenti di Acrobat e Reader il contenuto di testo viene visualizzato con il carattere e il colore predefiniti.

* Acrobat 9.0 e versioni precedenti: Acrobat 9.0 e versioni precedenti non supportano i nomi dei criteri nelle filigrane dinamiche. Se Acrobat 9.0 apre un documento protetto tramite policy con una filigrana dinamica che include un nome di policy e altri dati dinamici, la filigrana viene visualizzata senza il nome della policy. Se la filigrana dinamica include solo il nome del criterio, Acrobat visualizza un messaggio di errore

### Aggiungere un modello di filigrana dinamico {#add-a-dynamic-watermark-template}

È possibile creare modelli di filigrana dinamici. Questi modelli rimangono disponibili come opzione di configurazione per i criteri creati da amministratori o utenti.

>[!NOTE]
>
>Le informazioni di configurazione delle filigrane dinamiche non vengono acquisite con le altre informazioni di configurazione quando esportate un file di configurazione.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Filigrane.
1. Fai clic su Nuovo.
1. Nella casella Nome digitare un nome per la nuova filigrana.

   ***nota &#x200B;**: non è possibile utilizzare caratteri speciali nei nomi o nelle descrizioni di filigrane o elementi filigrana. Vedi le restrizioni elencate in [Considerazioni per la modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. In Nome, accanto al segno più, immettere un nome significativo per l&#39;elemento della filigrana, ad esempio Intestazione, aggiungere una descrizione ed espandere il segno più per visualizzare le opzioni.
1. In Source, selezionare il tipo di filigrana come Testo o PDF.
1. Se è stata selezionata l&#39;opzione Testo, effettuare le seguenti operazioni:

   * Selezionare i tipi di filigrana da includere. Se si seleziona Testo personalizzato, nella casella adiacente digitare il testo da visualizzare per la filigrana. Tenere presente la lunghezza del testo che verrà visualizzato come filigrana.
   * Specificare le proprietà di formattazione del testo, ad esempio il nome, la dimensione, il colore di primo piano e il colore di sfondo del testo della filigrana. Specificate il colore di primo piano e di sfondo come valori esadecimali.

     ***nota &#x200B;**: se si seleziona l&#39;opzione di ridimensionamento Adatta alla pagina, la proprietà Dimensione carattere non sarà disponibile per la modifica.*

1. Se hai selezionato PDF per le opzioni della filigrana avanzata, fai clic su **Sfoglia** accanto a Seleziona PDF filigrana per selezionare il documento PDF che desideri utilizzare come filigrana.

   ***nota &#x200B;**: non utilizzare un documento PDF protetto da password. Se si specifica un PDF protetto da password come elemento filigrana, la filigrana non verrà applicata.*

1. In Usa come sfondo selezionare Sì o No.

   **nota**: attualmente la filigrana viene visualizzata in primo piano indipendentemente da questa impostazione.

1. Per controllare la posizione di visualizzazione della filigrana nel documento, configurare le opzioni Allineamento verticale e Allineamento orizzontale.
1. Selezionare Adatta alla pagina oppure % e digitare una percentuale nella casella. Il valore deve essere un numero intero, non una frazione. Per configurare le dimensioni della filigrana, è possibile utilizzare un valore corrispondente alla percentuale della pagina oppure impostare la filigrana in modo che corrisponda alle dimensioni della pagina.
1. Nella casella Rotazione digitare i gradi di rotazione della filigrana. L&#39;intervallo è compreso tra -180 e 180. Utilizzare un valore negativo per ruotare la filigrana in senso antiorario. Il valore deve essere un numero intero, non una frazione.
1. Nella casella Opacità digitare una percentuale. Utilizza un numero intero, non una frazione.
1. In Opzioni avanzate impostare quanto segue:

   **Opzioni intervallo pagine**

   Impostare l&#39;intervallo di pagine in cui visualizzare la filigrana. Immettere 1 come pagina iniziale e -1 come pagina finale per contrassegnare tutte le pagine con la filigrana.

   **Opzioni di visualizzazione**

   Selezionare il punto in cui si desidera visualizzare la filigrana. Per impostazione predefinita, la filigrana viene visualizzata sia in copia temporanea (online) che in copia cartacea (stampa).

1. Fai clic su **Nuovo** in Elementi filigrana per aggiungere altri elementi filigrana, se necessario.
1. Fare clic su OK.

### Modificare un modello di filigrana dinamica {#edit-a-dynamic-watermark-template}

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Filigrane.
1. Fare clic sulla filigrana appropriata nell&#39;elenco.
1. Nella pagina Modifica filigrane modificare le impostazioni in base alle esigenze.
1. Fare clic su OK.

### Eliminare un modello di filigrana dinamica {#delete-a-dynamic-watermark-template}

Quando si elimina una filigrana dinamica, questa non è più disponibile per l’aggiunta a un nuovo criterio. Tuttavia, la filigrana rimane nei criteri esistenti che la utilizzano attualmente e i documenti protetti dal criterio continuano a mostrare la filigrana dinamica fino a quando tu o un utente non modifichi il criterio che contiene la filigrana eliminata. Dopo la modifica del criterio, la filigrana non viene più applicata. Viene visualizzato un messaggio che indica che la filigrana esistente è stata eliminata dal criterio e che l’utente può selezionarne un’altra per sostituirla.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Filigrane.
1. Selezionare la casella di controllo accanto alla filigrana appropriata e fare clic su Elimina.
1. Fare clic su OK.

## Configurazione della registrazione degli utenti invitati {#configuring-invited-user-registration}

Gli utenti esterni all’organizzazione possono registrarsi in Document Security. Gli utenti invitati che registrano e attivano i propri account possono accedere a document security utilizzando il proprio indirizzo e-mail e la password create al momento della registrazione. Gli utenti invitati registrati possono utilizzare documenti protetti tramite policy per i quali dispongono di autorizzazioni.

Quando gli utenti invitati vengono attivati, diventano utenti locali. Gli utenti locali possono essere configurati e gestiti utilizzando l&#39;area Utenti invitati e Utenti locali. (Vedi [Gestione degli account utente invitati e locali](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

A seconda delle funzionalità abilitate per gli utenti invitati, è possibile utilizzare anche le seguenti funzionalità di protezione dei documenti:

* Applicare le policy ai documenti
* Creare criteri
* Aggiungere utenti invitati ai criteri

Document Security genera automaticamente un messaggio e-mail di invito alla registrazione quando si verificano gli eventi seguenti, a meno che l’utente non si trovi già nella directory LDAP di origine o sia stato precedentemente invitato a registrarsi:

* Un utente esistente aggiunge un utente invitato a un criterio
* Un amministratore aggiunge un account utente invitato nella pagina Registrazione utente invitato

L’e-mail di registrazione contiene un collegamento a una pagina di registrazione e informazioni su come registrarsi. Dopo che l’utente invitato si è registrato, Document Security invia un’e-mail di attivazione con un collegamento a una pagina di attivazione. Quando viene attivato, l’account rimane valido fino a quando non viene disattivato o eliminato.

Se si abilita la registrazione incorporata, specificare il server SMTP, i dettagli dell&#39;e-mail di registrazione, le funzionalità di accesso e reimpostare le informazioni dell&#39;e-mail della password una sola volta. Prima di abilitare la registrazione incorporata, accertati di aver creato un dominio locale in Gestione utenti e di aver assegnato il ruolo &quot;Invita utente&quot; di Document Security agli utenti e ai gruppi appropriati dell’organizzazione. (Vedi [Aggiungi un dominio locale](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) e [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Se non utilizzi la registrazione incorporata, devi creare un sistema di registrazione utenti personalizzato con i moduli AEM di SDK. Consulta la guida sullo sviluppo di SPI per i moduli AEM in [Programmazione con moduli AEM](/help/forms/developing/introducing-java-api-soap-quick.md). Se non utilizzi l’opzione di registrazione incorporata, ti consigliamo di configurare un messaggio nell’e-mail di attivazione e nella schermata di accesso del client per avvisare gli utenti di come contattare l’amministratore per una nuova password o per altre informazioni.

**Abilita e configura la registrazione degli utenti invitati**

Per impostazione predefinita, il processo di registrazione degli utenti invitati è disabilitato. Se necessario, puoi abilitare e disabilitare la registrazione degli utenti invitati per la sicurezza dei documenti.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > Registrazione utente invitato.
1. Selezionare Abilita registrazione utenti invitati.
1. (Facoltativo) Aggiorna le impostazioni di registrazione degli utenti invitati come richiesto:

   * [Escludere o includere un utente o un gruppo esterno](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parametri server e account di registrazione](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Impostazioni e-mail per invito alla registrazione](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Impostazioni e-mail di attivazione](configuring-client-server-options.md#activation-email-settings)
   * [Configurare un messaggio e-mail di reimpostazione della password](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Facoltativo) In Registrazione incorporata, seleziona Sì per abilitare questa opzione. Se non si abilita la registrazione incorporata, è necessario impostare un sistema di registrazione utente personalizzato.
1. Fare clic su OK.

### Escludere o includere un utente o un gruppo esterno {#exclude-or-include-an-external-user-or-group}

È possibile limitare la registrazione con Document Security per determinati utenti o gruppi di utenti esterni. Questa opzione è utile, ad esempio, per consentire l’accesso a un determinato gruppo di utenti, ma esclude persone specifiche che fanno parte del gruppo.

Le impostazioni seguenti si trovano nell&#39;area Filtro restrizioni e-mail della pagina Registrazione utente invitato.

**Esclusione:** Digitare l&#39;indirizzo di posta elettronica di un utente o di un gruppo da escludere. Per escludere più utenti o gruppi, digita ogni indirizzo e-mail su una nuova riga. Per escludere tutti gli utenti che appartengono a un dominio specifico, immettere un carattere jolly e il nome di dominio. Ad esempio, per escludere tutti gli utenti nel dominio example.com, immettere &ast;.example.com.

**Inclusione:** Digitare l&#39;indirizzo di posta elettronica di un utente o di un gruppo da includere. Per includere più utenti o gruppi, digita ogni indirizzo e-mail su una nuova riga. Per includere tutti gli utenti che appartengono a un determinato dominio, immettere un carattere jolly e il nome di dominio. Ad esempio, per includere tutti gli utenti nel dominio example.com, immettere &ast;.example.com.

### Parametri server e account di registrazione {#server-and-registration-account-parameters}

Le impostazioni seguenti si trovano nell&#39;area Impostazioni generali della pagina Registrazione utente invitato.

**Host SMTP:** Il nome host del server SMTP. Il server SMTP gestisce gli avvisi e-mail in uscita per registrare e attivare gli account utente invitati.

Se necessario, digitare le informazioni richieste nelle caselle Nome account server SMTP e Password account server SMTP per connettersi al server SMTP. Alcune organizzazioni non applicano questo requisito. Per ulteriori informazioni, rivolgersi all&#39;amministratore di sistema.

**Nome classe socket server SMTP:** Nome classe socket per il server SMTP. Ad esempio, javax.net.ssl.SSLSocketFactory.

**Tipo di contenuto e-mail:** Tipo MIME accettato come text/plain o text/html.

**Codifica e-mail:** Formato di codifica da utilizzare per l&#39;invio di messaggi e-mail. È possibile specificare qualsiasi codifica, ad esempio UTF-8 per Unicode o ISO-8859-1 per Latin. Il valore predefinito è UTF-8.

**Indirizzo e-mail di reindirizzamento:** Quando si specifica un indirizzo e-mail per questa impostazione, eventuali nuovi inviti vengono inviati all&#39;indirizzo fornito. Questa impostazione può essere utile a scopo di test.

**Usa domini locali:** Selezionare il dominio appropriato. In una nuova installazione, accertati di aver creato il dominio utilizzando Gestione utenti. Se si tratta di un aggiornamento, durante l’aggiornamento è stato creato un dominio utente esterno che può essere utilizzato.

**Usa SSL per il server SMTP:** Selezionare questa opzione per abilitare SSL per il server SMTP.

**Visualizza collegamento di accesso nella pagina di registrazione:** Visualizza un collegamento di accesso nella pagina di registrazione visualizzata per gli utenti invitati.

**Per abilitare Transport Layer Security (TLS) per il server SMTP**

1. Apri la console di amministrazione.

   Il percorso predefinito della console di amministrazione è `https://<server>:<port>/adminui`.

1. Passa a Home > Servizi > Document Security > Configurazione > Registrazione utente invitato.
1. In Registrazione utente invitato specificare tutte le impostazioni di configurazione e quindi fare clic su OK.

   >[!NOTE]
   >
   >Se si utilizza Microsoft Office 365 come server SMTP per l&#39;invio degli inviti per la registrazione degli utenti, utilizzare le impostazioni seguenti:
   >
   >**Host SMTP:** smtp.office365.com
   >**Porta:** 587

1. Successivamente, devi aggiornare config.xml. Vedere [Configurazione per abilitare SMTP per Transport Layer Security (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Se si apportano modifiche alle opzioni di Registrazione utente invitato, il file config.xml viene sovrascritto e TLS viene disattivato. Se sovrascrivi le modifiche, devi eseguire il passaggio precedente per riattivare il supporto TLS per la registrazione degli utenti invitati.

### Impostazioni e-mail per invito alla registrazione {#registration-invitation-email-settings}

Document Security invia automaticamente un messaggio e-mail di invito alla registrazione quando crei un account utente invitato o quando un utente esistente aggiunge un destinatario esterno che non si è registrato o che è stato invitato in precedenza a registrarsi a una policy. L’e-mail contiene un collegamento che il destinatario può utilizzare per accedere alla pagina di registrazione e immettere le informazioni sull’account personale, inclusi nome utente e password. La password può essere costituita da qualsiasi combinazione di otto caratteri.

Quando il destinatario attiva l’account, l’utente diventa un utente locale.

Le impostazioni seguenti si trovano nell&#39;area Configurazione e-mail di invito della pagina Registrazione utente invitato.

**Da:** L&#39;indirizzo di posta elettronica da cui viene inviato l&#39;invito. Il formato predefinito dell&#39;indirizzo di posta elettronica Da è postmaster@[your_installation_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di invito.

**Timeout:** il numero di giorni dopo i quali scade l&#39;invito di registrazione se l&#39;utente esterno non si registra. Il valore predefinito è 30 giorni.

**Messaggio:** il testo visualizzato nel corpo del messaggio che invita l&#39;utente a registrarsi.

### Impostazioni e-mail di attivazione {#activation-email-settings}

Dopo che gli utenti sono stati invitati a registrarsi, document security invia un’e-mail di attivazione. L’e-mail di attivazione contiene un collegamento alla pagina di attivazione dell’account in cui gli utenti possono attivare l’account. Quando gli account vengono attivati, gli utenti possono accedere a document security utilizzando il proprio indirizzo e-mail e la password creati al momento della registrazione.

Quando il destinatario attiva l’account utente, l’utente diventa un utente locale.

Le impostazioni seguenti si trovano nell&#39;area Configurazione e-mail di attivazione della pagina Registrazione utente invitato.

>[!NOTE]
>
>È inoltre consigliabile configurare un messaggio nella schermata di accesso per indicare agli utenti esterni come contattare il proprio amministratore per ottenere una nuova password o altre informazioni.

**Da:** l&#39;indirizzo e-mail da cui viene inviata l&#39;e-mail di attivazione. Questo indirizzo e-mail riceve gli avvisi di recapito non riusciti dall&#39;host e-mail del registrante e tutti i messaggi inviati dal destinatario in risposta all&#39;e-mail di registrazione. Il formato predefinito dell&#39;indirizzo di posta elettronica Da è postmaster@[your_installation_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio di posta elettronica di attivazione.

**Timeout:** il numero di giorni dopo i quali l&#39;invito di attivazione scade se l&#39;utente non attiva l&#39;account. Il valore predefinito è 30 giorni.

**Messaggio:** Il testo visualizzato nel corpo del messaggio indica che l&#39;account utente del destinatario deve essere attivato. È inoltre possibile includere informazioni su come contattare un amministratore per ottenere una nuova password.

### Configurare un messaggio e-mail di reimpostazione della password {#configure-a-password-reset-email}

Se devi reimpostare la password di un utente invitato, viene generato un messaggio e-mail di conferma che invita l’utente a scegliere una nuova password. Impossibile determinare la password di un utente. Se l&#39;utente la dimentica, è necessario reimpostarla.

Le impostazioni seguenti si trovano nell&#39;area E-mail reimpostazione password della pagina Registrazione utente invitato.

**Da:** l&#39;indirizzo e-mail da cui viene inviata l&#39;e-mail di reimpostazione della password. Il formato predefinito dell&#39;indirizzo di posta elettronica Da è postmaster@[your_installation_domain].com.

**Oggetto:** Oggetto predefinito per il messaggio e-mail di reimpostazione.

**Messaggio:** Il testo visualizzato nel corpo del messaggio indica che la password utente esterna del destinatario è stata reimpostata.

## Consenti a utenti e gruppi di creare criteri {#enable-users-and-groups-to-create-policies}

La pagina Configurazione contiene un collegamento alla pagina Criteri personali, in cui è possibile specificare gli utenti finali autorizzati a creare i criteri e quali utenti e gruppi sono visibili nei risultati della ricerca. La pagina I miei criteri dispone di due schede:

**Scheda Crea criteri:** Utilizzare per configurare le autorizzazioni utente per la creazione di criteri personalizzati.

**Scheda Utenti e gruppi visibili:** Utilizzare per controllare quali utenti e gruppi sono visibili nei risultati della ricerca utente. L&#39;amministratore di utenti con privilegi avanzati o set di criteri deve selezionare e aggiungere i domini, creati in Gestione utente, all&#39;utente e al gruppo visibili per ogni set di criteri. Questo elenco è visibile al coordinatore del set di criteri e viene utilizzato per definire i limiti sui domini che il coordinatore può esplorare quando sceglie gli utenti da aggiungere ai criteri.

Prima di concedere agli utenti l&#39;autorizzazione per la creazione di criteri personalizzati, è opportuno considerare il livello di accesso o di controllo che si desidera assegnare ai singoli utenti. Inoltre, considera la modalità di esposizione desiderata per utenti e gruppi quando li rendi visibili alle ricerche.

### Specificare gli utenti e i gruppi che possono creare i criteri {#specify-users-and-groups-who-can-create-policies}

In qualità di amministratore, specifica quali utenti e gruppi possono creare criteri personalizzati. Questa autorizzazione può essere impostata a livello di utente e di gruppo. La funzionalità di ricerca consente di cercare utenti e gruppi nel database di User Management.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Configurazione > I miei criteri.
1. Nella pagina Criteri personali fare clic sulla scheda Crea criteri e quindi su Aggiungi utenti e gruppi.
1. Nella casella Trova digitare il nome utente o l&#39;indirizzo di posta elettronica dell&#39;utente o del gruppo che si sta cercando. Se non disponi di queste informazioni, lascia vuota la casella. Puoi anche digitare un nome parziale o un indirizzo e-mail, ad esempio quando conosci solo le prime due lettere di un nome utente.
1. Nell’elenco Utilizzo, seleziona i parametri di ricerca Nome o E-mail.
1. Nell&#39;elenco Tipo selezionare Gruppo o Utente per restringere la ricerca.
1. Nell&#39;elenco In selezionare il dominio in cui eseguire la ricerca. Se non conosci il dominio dell’utente o del gruppo, seleziona Tutti i domini.
1. Nell&#39;elenco Visualizza specificare il numero di risultati di ricerca da visualizzare per pagina e quindi fare clic su Trova.
1. Per aggiungere utenti e gruppi di criteri personali, selezionare la casella di controllo relativa a ogni utente e gruppo da aggiungere.
1. Fare clic su Aggiungi e quindi su OK.

Gli utenti e i gruppi selezionati ora dispongono delle autorizzazioni per creare criteri personalizzati.

### Rimuovere l’autorizzazione per creare criteri personalizzati da un utente o un gruppo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Nella pagina di Document Security, fai clic su Configurazione > I miei criteri.
1. Nella pagina Criteri personali fare clic sulla scheda Crea criteri. Vengono visualizzati gli utenti e i gruppi con le autorizzazioni per creare criteri personalizzati.
1. Selezionare la casella di controllo accanto agli utenti e ai gruppi da rimuovere da questa autorizzazione.
1. Fare clic su Elimina e quindi su OK.

### Specificare utenti e gruppi visibili nelle ricerche {#specify-users-and-groups-that-are-visible-in-searches}

Quando gli utenti gestiscono i propri criteri personalizzati, possono cercare utenti e gruppi da aggiungere ai propri criteri. Specificare i domini dai quali utenti e gruppi sono visibili in queste ricerche.

1. Nella pagina di Document Security, fai clic su Configurazione > I miei criteri.
1. Nella pagina Criteri personali fare clic sulla scheda Utenti e gruppi visibili.
1. Per rendere visibili gli utenti e i gruppi di un dominio, fai clic su Aggiungi domini, seleziona i domini e fai clic su Aggiungi. Per rimuovere un dominio, seleziona la casella di controllo accanto al nome di dominio e fai clic su Elimina.

## Modifica manuale del file di configurazione per la protezione dei documenti {#manually-editing-the-document-security-configuration-file}

È possibile importare ed esportare le informazioni di configurazione memorizzate nel database di Document Security. Ad esempio, potrebbe essere utile creare una copia di backup delle informazioni di configurazione quando si passa da un ambiente di staging a un ambiente di produzione, oppure modificare le opzioni avanzate che possono essere configurate solo per la modifica di questo file.

Puoi apportare le seguenti modifiche utilizzando il file di configurazione:

[Visualizzare le autorizzazioni CATIA durante la creazione e la modifica dei criteri](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Specificare un periodo di timeout per la sincronizzazione offline](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Negazione dei servizi di protezione dei documenti per applicazioni specifiche](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Modificare i parametri di configurazione della filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Disabilitazione dei collegamenti esterni](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>L&#39;importazione del file di configurazione riconfigura il sistema in base alle informazioni contenute nel file. Le eccezioni sono la configurazione della filigrana dinamica e le informazioni sugli eventi personalizzati, che non vengono salvate con il file di configurazione esportato. Configura queste informazioni manualmente nel nuovo sistema. Solo un amministratore di sistema o un consulente di servizi professionali che ha familiarità con document security e XML può modificare il contenuto di un file di configurazione, ad esempio per riconfigurare un&#39;impostazione danneggiata o per sottoporre a tuning i parametri di un particolare scenario di distribuzione aziendale.

**Esporta un file di configurazione**

1. Nella console di amministrazione, fai clic su Servizi > Document Security 11 > Configurazione > Configurazione manuale.
1. Fare clic su Esporta e salvare il file di configurazione in un&#39;altra posizione. Il nome file predefinito è config.xml.
1. Fare clic su OK.
1. Prima di modificare il file di configurazione, esegui una copia di backup nel caso sia necessario ripristinarlo.

**Importa un file di configurazione**

1. Nella console di amministrazione, fai clic su Servizi > Document Security 11 > Configurazione > Configurazione manuale.
1. Fare clic su Sfoglia per passare al file di configurazione e quindi su Importa. Non è possibile digitare il percorso direttamente nella casella Nome file.
1. Fare clic su OK.

### Specificare un periodo di timeout per la sincronizzazione offline {#specify-a-timeout-period-for-offline-synchronization}

Document Security consente agli utenti di aprire e utilizzare un documento protetto quando non sono connessi al server di Document Security. L&#39;applicazione client dell&#39;utente deve sincronizzarsi regolarmente con il server per mantenere i documenti validi per l&#39;utilizzo offline. La prima volta che si apre un documento protetto, viene richiesto se il computer deve essere autorizzato a eseguire la sincronizzazione periodica del client.

Per impostazione predefinita, la sincronizzazione viene eseguita automaticamente ogni quattro ore e in base alle esigenze quando un utente è connesso al server di Document Security. Se il periodo non in linea di un documento scade mentre l&#39;utente non è in linea, è necessario riconnettersi al server per consentire all&#39;applicazione client di eseguire la sincronizzazione con il server.

Nel file di configurazione di document security è possibile specificare la frequenza predefinita della sincronizzazione automatica in background. Questa impostazione funge da periodo di timeout predefinito per le applicazioni client, a meno che il client non imposti esplicitamente il proprio valore di timeout.

1. Esporta il file di configurazione di document security. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Aprire il file di configurazione in un editor e individuare il nodo `PolicyServer`. Sotto tale nodo, individuare il nodo `ServerSettings`.
1. Nel nodo `ServerSettings`, aggiungere la seguente voce, quindi salvare il file:

   `<entry key="BackgroundSyncFrequency" value="`*ora* `"/>`

   dove *time* è il numero di secondi tra le sincronizzazioni in background automatiche. Se hai inviato questo valore a `0`, la sincronizzazione si verifica sempre. Il valore predefinito è `14400` secondi (ogni quattro ore).

1. Importa il file di configurazione. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Negazione dei servizi di protezione dei documenti per applicazioni specifiche {#denying-document-security-services-for-specific-applications}

È possibile configurare document security in modo da negare i servizi alle applicazioni che soddisfano criteri specifici. I criteri possono specificare un singolo attributo, ad esempio il nome di una piattaforma, oppure più insiemi di attributi. Questa funzione consente di controllare le richieste che Document Security deve gestire. Di seguito sono elencate alcune applicazioni di questa funzione:

* **Protezione dei ricavi:** È possibile negare l&#39;accesso a qualsiasi applicazione client che non supporta le convenzioni dei ricavi.
* **Compatibilità dell&#39;applicazione:** Alcune applicazioni potrebbero non essere compatibili con i criteri o il comportamento del server di Document Security.

Quando le applicazioni client tentano di stabilire un collegamento con la sicurezza dei documenti, forniscono informazioni su applicazione, versione e piattaforma. Document Security confronta queste informazioni con le impostazioni di rifiuto ottenute dal file di configurazione di Document Security.

Le impostazioni Rifiuti possono contenere diversi set di condizioni di rifiuto. Se tutti gli attributi di un set corrispondono, all’applicazione richiedente viene negato l’accesso ai servizi di protezione dei documenti.

La funzione di negazione del servizio richiede che le applicazioni client utilizzino la versione 8.2 o successiva di Document Security C++ Client SDK. I seguenti Adobe forniscono informazioni sul prodotto quando si richiedono i servizi di sicurezza dei documenti:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard e versioni successive
* Adobe Reader 9.0 e versioni successive
* Estensioni Acrobat Reader DC per Microsoft Office 8.2 e versioni successive

Le applicazioni client utilizzano l’API client di Document Security C++ Client SDK per richiedere servizi di Document Security. Le richieste API client includono informazioni sulla piattaforma e sulla versione di SDK (precompilate nell’API client) e informazioni sul prodotto ottenute dall’applicazione client.

Le applicazioni client o i plug-in forniscono informazioni sui prodotti nell’implementazione di una funzione di callback. L&#39;applicazione fornisce le seguenti informazioni:

* Nome integratore
* Versione integratore
* Famiglia di applicazioni
* Nome applicazione
* Versione applicazione

Se non sono applicabili informazioni, l’applicazione client lascia vuoto il campo corrispondente.

Diverse applicazioni di Adobe includono informazioni sul prodotto quando si richiedono servizi di sicurezza dei documenti, tra cui Acrobat, Adobe Reader e le estensioni Acrobat Reader DC per Microsoft Office.

**Acrobat e Adobe Reader**

Quando Acrobat o Adobe Reader richiedono un servizio da document security, forniscono le seguenti informazioni di prodotto:

* **Integratore:** Adobe Systems, Inc.
* **Versione integratore:** 1.0
* **Famiglia di applicazioni:** Acrobat
* **Nome applicazione:** Acrobat
* **Versione applicazione:** 9.0.0

**Estensioni Acrobat Reader DC per Microsoft Office**

Le estensioni Acrobat Reader DC per Microsoft Office sono un plug-in utilizzato con i prodotti Microsoft Office Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Quando richiede un servizio, fornisce le seguenti informazioni:

* **Integratore:** Adobe Systems Incorporated
* **Versione integratore:** 8.2
* **Famiglia di applicazioni:** estensioni Acrobat Reader DC per Microsoft Office
* **Nome applicazione:** Microsoft Word, Microsoft Excel o Microsoft PowerPoint
* **Versione applicazione:** 2003 o 2007

**Configura la protezione dei documenti per negare i servizi per applicazioni specifiche**

1. Esporta il file di configurazione di document security. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Aprire il file di configurazione in un editor e individuare il nodo `PolicyServer`. Aggiungere un nodo `ClientVersionRules` come figlio immediato del nodo `PolicyServer`, se non ne esiste uno:

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

   Dove:

   `SDKPlatforms` specifica la piattaforma che ospita l&#39;applicazione client. I valori possibili sono:

   * Microsoft Windows
   * APPLE OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` specifica la versione dell&#39;API client C++ di Document Security utilizzata dall&#39;applicazione client. Esempio: `"8.2"`.

   `APPFamilies` è definito dall&#39;API client.

   `AppName`specifica il nome dell&#39;applicazione client. Le virgole vengono utilizzate come separatori dei nomi. Per includere una virgola in un nome, esegui l’escape con una barra rovesciata (\). *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` specifica la versione dell&#39;applicazione client.

   `Integrators` specifica il nome della società o del gruppo che ha sviluppato il plug-in o l&#39;applicazione integrata.

   `IntegratorVersions` è la versione del plug-in o dell&#39;applicazione integrata.

1. Per ogni set aggiuntivo di dati non consentiti, aggiungere un altro elemento *MyEntryName*.
1. Salva il file di configurazione.
1. Importa il file di configurazione. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

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

In questo esempio, a Applicazione personale versione 3.0 e Altra applicazione personale versione 2.0 viene negato l&#39;accesso. Lo stesso URL di informazioni sui rifiuti viene utilizzato indipendentemente dal motivo del rifiuto.

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

In questo esempio, tutte le richieste provenienti da un&#39;installazione di Microsoft PowerPoint 2007 o Microsoft PowerPoint 2010 di estensioni Acrobat Reader DC per Microsoft Office vengono rifiutate.

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

Per impostazione predefinita, è possibile specificare un massimo di cinque elementi in una filigrana. Inoltre, la dimensione massima del file del documento PDF che si desidera utilizzare come filigrana è limitata a 100 KB. È possibile modificare questi parametri nel file config.xml.

***nota &#x200B;**: è necessario modificare questi parametri con cautela.*

1. Esporta il file di configurazione di document security. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Aprire il file di configurazione in un editor e individuare il nodo `ServerSettings`.
1. Nel nodo `ServerSettings` aggiungere le voci seguenti e quindi salvare il file: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   La prima voce, *dimensione massima file*, corrisponde alla dimensione massima del file (in KB) consentita per un elemento filigrana PDF. Il valore predefinito è 100 KB.

   La seconda voce, *max elementi*, rappresenta il numero massimo di elementi consentito in una filigrana. Il valore predefinito è 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importa il file di configurazione. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Disabilitazione dei collegamenti esterni {#disabling-external-links}

Molti utenti di Document Security non hanno accesso a collegamenti esterni come **www.adobe.com** mentre utilizzano le interfacce utente di Right Management:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Le seguenti modifiche apportate al file config.xml disattivano tutti i collegamenti esterni dalle interfacce utente di Right Management.

1. Esporta il file di configurazione di document security. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Aprire il file di configurazione in un editor e individuare il nodo `DisplaySettings`.
1. Per disabilitare tutti i collegamenti esterni, nel nodo `DisplaySettings` aggiungere la voce seguente e quindi salvare il file: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importa il file di configurazione. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configurazione per abilitare SMTP per TLS (Transport Layer Security) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Le seguenti modifiche apportate al file config.xml abilitano il supporto per TLS per la funzione di registrazione degli utenti invitati.

1. Esporta il file di configurazione di document security. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Aprire il file di configurazione in un editor e individuare il nodo `DisplaySettings`.
1. Individuare il seguente nodo: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Impostare il valore della chiave `SmtpUseTls` nel nodo `ExternalUser` su **true**.
1. Impostare il valore della chiave `SmtpUseSsl` nel nodo `ExternalUser` su **false**.
1. Salva `config.xml`.
1. Importa il file di configurazione. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Disattivazione degli endpoint SOAP per i documenti di Document Security {#disable-soap-endpoints-for-document-security-documents}

Di seguito sono riportate le modifiche apportate al file config.xml per disabilitare gli endpoint SOAP per i documenti relativi alla protezione dei documenti.

1. Esporta il file di configurazione di document security. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Aprire il file di configurazione in un editor e individuare il nodo seguente: `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. Nel nodo DRM, individuare il nodo `entry`:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Per disabilitare gli endpoint SOAP per i documenti di Document Security, impostare l&#39;attributo value su **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Salva `config.xml`.
1. Importa il file di configurazione. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Maggiore scalabilità del server di Document Security {#increasingscalability}

Per impostazione predefinita, durante la sincronizzazione di un documento per l’utilizzo offline, insieme alle informazioni per il documento corrente, i client di protezione dei documenti recuperano le informazioni relative a criteri, filigrane, licenze e aggiornamenti di revoca per tutti gli altri documenti a cui l’utente ha accesso. Se questi aggiornamenti e informazioni non vengono sincronizzati con il client, è possibile che un documento aperto in modalità offline venga comunque aperto con informazioni precedenti relative a criteri, filigrana e revoche.

È possibile aumentare la scalabilità del server di Document Security limitando le informazioni inviate al client. La riduzione della quantità di informazioni inviate al client consente di migliorare la scalabilità, ridurre i tempi di risposta e migliorare le prestazioni del server. Per aumentare la scalabilità, effettua le seguenti operazioni:

1. Esporta il file di configurazione di document security. (Vedi [Modifica manuale del file di configurazione di document security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Apri il file di configurazione in un editor e individua il nodo ServerSettings.
1. Nel nodo ServerSettings, impostare il valore della proprietà `DisableGlobalOfflineSynchronizationData` su `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Se impostato su true, il server di Document Security invia informazioni solo per il documento corrente e le informazioni per gli altri documenti (gli altri documenti a cui un utente ha accesso) non vengono inviate al client.

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore della chiave `DisableGlobalOfflineSynchronizationData` è impostato su `false`.

1. Salva e importa il file di configurazione. (Vedi [Modifica manuale del file di configurazione di document security](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
