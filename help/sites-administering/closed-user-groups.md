---
title: Gruppi di utenti chiusi in AEM
seo-title: Gruppi di utenti chiusi in AEM
description: Scopri i gruppi di utenti chiusi in AEM.
seo-description: Scopri i gruppi di utenti chiusi in AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Sicurezza
translation-type: tm+mt
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '6886'
ht-degree: 0%

---

# Gruppi di utenti chiusi in AEM{#closed-user-groups-in-aem}

## Introduzione {#introduction}

A partire dalla versione 6.3 di AEM, esiste una nuova implementazione di Gruppo utenti chiuso destinata a risolvere i problemi di prestazioni, scalabilità e sicurezza presenti con l’implementazione esistente.

>[!NOTE]
>
>Per semplicità, l&#39;abbreviazione CUG sarà utilizzata in tutta la presente documentazione.

L&#39;obiettivo della nuova implementazione è quello di coprire le funzionalità esistenti laddove necessario, affrontando al tempo stesso i problemi e le limitazioni di progettazione rispetto alle versioni precedenti. Il risultato è un nuovo progetto CUG con le seguenti caratteristiche:

* chiara separazione degli elementi di autenticazione e autorizzazione, che possono essere utilizzati singolarmente o in combinazione;
* modello di autorizzazione dedicato per riflettere l&#39;accesso in lettura limitato agli alberi CUG configurati senza interferire con altri requisiti di configurazione e autorizzazione del controllo degli accessi;
* separazione tra la configurazione del controllo di accesso dell&#39;accesso in lettura limitato, solitamente necessaria per le istanze di authoring, e la valutazione delle autorizzazioni, che in genere è desiderata solo al momento della pubblicazione;
* Modifica dell&#39;accesso in lettura limitato senza escalation dei privilegi;
* estensione dedicata del tipo di nodo per contrassegnare il requisito di autenticazione;
* Percorso di accesso facoltativo associato al requisito di autenticazione.

### Implementazione del nuovo gruppo di utenti personalizzato {#the-new-custom-user-group-implementation}

Un CUG come noto nel contesto di AEM è costituito dai seguenti passaggi:

* Limita l’accesso in lettura all’albero che deve essere protetto e consente la lettura solo delle entità elencate con una determinata istanza CUG o escluse dalla valutazione CUG. Questo si chiama elemento **authorization** .
* Applica l&#39;autenticazione su un albero specifico e, facoltativamente, specifica una pagina di accesso dedicata per tale albero che viene successivamente esclusa. Questo si chiama elemento **authentication** .

La nuova implementazione è stata progettata per tracciare una linea tra gli elementi di autenticazione e di autorizzazione. A partire dalla AEM 6.3, è possibile limitare l&#39;accesso in lettura senza aggiungere esplicitamente un requisito di autenticazione. Ad esempio, se una determinata istanza richiede completamente l’autenticazione o una determinata struttura risiede già in una sottostruttura che richiede già l’autenticazione.

Allo stesso modo, un determinato albero può essere contrassegnato con un requisito di autenticazione senza modificare l&#39;impostazione effettiva delle autorizzazioni. Le combinazioni e i risultati sono elencati nella sezione [Combining CUG Policies (Criteri per gruppi di utenti) e nella sezione Authentication Requirements](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) (Requisito di autenticazione).

## Panoramica {#overview}

### Autorizzazione: Limitazione dell&#39;accesso in lettura {#authorization-restricting-read-access}

La funzione chiave di un gruppo di utenti chiuso limita l’accesso in lettura su una determinata struttura nell’archivio dei contenuti per tutti, eccetto i gruppi selezionati. Invece di manipolare al volo il contenuto predefinito del controllo di accesso, la nuova implementazione adotta un approccio diverso definendo un tipo dedicato di policy di controllo di accesso che rappresenta un CUG.

#### Criteri di controllo accessi per CUG {#access-control-policy-for-cug}

Questo nuovo tipo di criterio presenta le seguenti caratteristiche:

* Accedi alla policy di controllo del tipo org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (definita dall’API Jackrabbit di Apache);
* PrincipalSetPolicy concede privilegi a un set modificabile di entità principali;
* I privilegi concessi e l&#39;ambito di applicazione della politica sono un dettaglio di implementazione.

L&#39;implementazione di PrincipalSetPolicy utilizzata per rappresentare i CUG definisce inoltre che:

* I criteri CUG consentono l’accesso in lettura solo agli articoli JCR regolari (ad esempio, il contenuto del controllo di accesso è escluso);
* L’ambito è definito dal nodo controllato dall’accesso che detiene la politica CUG;
* I criteri CUG possono essere nidificati, un CUG nidificato avvia un nuovo CUG senza ereditare il set principale del CUG &#39;parent&#39;;
* L’effetto del criterio, se la valutazione è abilitata, viene ereditato dall’intera sottostruttura fino al successivo CUG nidificato.

Questi criteri CUG vengono distribuiti in un&#39;istanza AEM tramite un modulo di autorizzazione separato denominato oak-authorization-cug. Questo modulo viene fornito con la propria gestione del controllo degli accessi e la valutazione delle autorizzazioni. In altre parole, la configurazione AEM predefinita fornisce una configurazione dell’archivio di contenuti Oak che combina più meccanismi di autorizzazione. Per ulteriori informazioni, consulta [questa pagina nella documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

In questa configurazione composita un nuovo CUG non sostituisce il contenuto del controllo di accesso esistente collegato al nodo di destinazione, ma è progettato per essere un supplemento che può anche essere rimosso successivamente senza influire sul controllo di accesso originale, che per impostazione predefinita in AEM sarebbe un elenco di controllo di accesso.

A differenza della precedente implementazione, le nuove politiche CUG vengono sempre riconosciute e trattate come contenuti di controllo degli accessi. Ciò significa che vengono create e modificate utilizzando l’API di gestione del controllo accessi JCR. Per ulteriori informazioni, consulta la sezione [Gestione dei criteri CUG](#managing-cug-policies) .

#### Autorizzazione per la valutazione dei criteri CUG {#permission-evaluation-of-cug-policies}

Oltre a una gestione dedicata del controllo degli accessi per i CUG, il nuovo modello di autorizzazione consente di consentire condizionalmente la valutazione delle autorizzazioni per le sue politiche. Questo consente di configurare i criteri CUG in un ambiente di staging e di abilitare la valutazione delle autorizzazioni effettive solo una volta replicate nell&#39;ambiente di produzione.

La valutazione delle autorizzazioni per i criteri CUG e l&#39;interazione con il modello di autorizzazione predefinito o aggiuntivo segue il modello progettato per meccanismi di autorizzazione multipli in Apache Jackrabbit Oak: viene concesso un set specifico di autorizzazioni se e solo se tutti i modelli concedono l’accesso. Per ulteriori informazioni, consulta [questa pagina](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) .

Per la valutazione delle autorizzazioni associata al modello di autorizzazione destinato a gestire e valutare le politiche CUG si applicano le seguenti caratteristiche:

* Gestisce solo le autorizzazioni di lettura per nodi e proprietà regolari, ma non la lettura del contenuto del controllo di accesso
* non gestisce le autorizzazioni di scrittura né alcun tipo di autorizzazioni necessarie per la modifica del contenuto JCR protetto (tra cui il controllo degli accessi, le informazioni sul tipo di nodo, il controllo delle versioni, il blocco o la gestione degli utenti); Queste autorizzazioni non sono influenzate da un criterio CUG e non verranno valutate dal modello di autorizzazione associato. Il fatto che queste autorizzazioni siano concesse o meno dipende dagli altri modelli configurati nella configurazione di protezione.

L&#39;effetto di un&#39;unica politica CUG sulla valutazione delle autorizzazioni può essere riassunto come segue:

* Accesso in lettura negato per tutti tranne per soggetti contenenti entità o entità principali esclusi elencati nel criterio;
* La politica ha effetto sul nodo controllato di accesso che detiene la politica e le sue proprietà;
* L&#39;effetto viene inoltre ereditato sotto la gerarchia, ovvero la struttura degli elementi definita dal nodo controllato dall&#39;accesso;
* Tuttavia, non influisce sui fratelli o antenati del nodo controllato di accesso;
* L’ereditarietà di un determinato CUG si arresta in un CUG nidificato.

#### Best practice   {#best-practices}

Per definire l’accesso in lettura limitato tramite CUG è necessario tenere conto delle seguenti best practice:

* Decidi in modo consapevole se la tua necessità di un CUG riguarda la limitazione dell’accesso in lettura o un requisito di autenticazione. In caso di quest&#39;ultimo o se vi è la necessità di entrambi, consultare la sezione sulle migliori pratiche per informazioni dettagliate in merito all&#39;obbligo di autenticazione
* Creare un modello di minaccia per i dati o i contenuti che devono essere protetti al fine di identificare i limiti della minaccia e ottenere un quadro chiaro sulla sensibilità dei dati e dei ruoli associati all&#39;accesso autorizzato
* Modellare il contenuto dell’archivio e i CUG tenendo presenti gli aspetti e le best practice relativi all’autorizzazione generale:

   * Ricorda che l&#39;autorizzazione di lettura sarà concessa solo se un CUG dato e la valutazione di altri moduli implementati nella sovvenzione di installazione consentono a un determinato soggetto di leggere un dato elemento dell&#39;archivio
   * Evitare la creazione di CUG ridondanti in cui l’accesso in lettura è già limitato da altri moduli di autorizzazione
   * L’eccessiva necessità di gruppi di utenti chiusi nidificati può potenzialmente evidenziare problemi nella progettazione dei contenuti
   * L’eccessiva necessità di CUG (ad esempio, su ogni singola pagina) può indicare la necessità di un modello di autorizzazione personalizzato potenzialmente più adatto a soddisfare le specifiche esigenze di sicurezza dell’applicazione e del contenuto in questione.

* Limita i percorsi supportati per i criteri CUG ad alcuni alberi nell’archivio per consentire prestazioni ottimizzate. Ad esempio, consenti solo CUG sotto il nodo /content come valore predefinito a partire da AEM 6.3.
* I criteri CUG sono progettati per garantire l&#39;accesso in lettura a un piccolo insieme di entità. La necessità di un gran numero di entità principali può evidenziare problemi nella progettazione del contenuto o dell&#39;applicazione e dovrebbe essere riconsiderata.

### Autenticazione: Definizione del requisito di autenticazione {#authentication-defining-the-auth-requirement}

Le parti correlate all’autenticazione della funzione CUG consentono di contrassegnare gli alberi che richiedono l’autenticazione e facoltativamente specificare una pagina di accesso dedicata. In conformità alla versione precedente, la nuova implementazione consente di contrassegnare gli alberi che richiedono l’autenticazione nell’archivio dei contenuti e di abilitare la sincronizzazione con `Sling org.apache.sling.api.auth.Authenticator`responsabile in ultima analisi dell’applicazione del requisito e del reindirizzamento a una risorsa di accesso.

Questi requisiti vengono registrati con Authenticator tramite un servizio OSGi che fornisce la proprietà di registrazione `sling.auth.requirements`. Queste proprietà vengono quindi utilizzate per estendere dinamicamente i requisiti di autenticazione. Per ulteriori informazioni, consulta la [documentazione Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definizione del requisito di autenticazione con un tipo di mixin dedicato {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Per motivi di sicurezza, la nuova implementazione sostituisce l’utilizzo di una proprietà JCR residua con un tipo mixin dedicato chiamato `granite:AuthenticationRequired`, che definisce una singola proprietà opzionale di tipo STRING per il percorso di accesso `granite:loginPath`. Solo le modifiche al contenuto relative a questo tipo di mixin porteranno all’aggiornamento dei requisiti registrati con Apache Sling Authenticator. Le modifiche vengono tracciate in seguito alla persistenza di eventuali modifiche transitorie e richiedono quindi una chiamata `javax.jcr.Session.save()` per diventare effettiva.

Lo stesso vale per la proprietà `granite:loginPath` . Sarà rispettato solo se è definito dal tipo di mixin relativo al requisito di autorizzazione. L&#39;aggiunta di una proprietà residua con questo stesso nome a un nodo JCR non strutturato non mostrerà l&#39;effetto desiderato e la proprietà verrà ignorata dal gestore responsabile dell&#39;aggiornamento della registrazione OSGi.

>[!NOTE]
>
>L’impostazione della proprietà del percorso di accesso è facoltativa e necessaria solo se la struttura che richiede l’autenticazione non può tornare alla pagina di accesso predefinita o ereditata in altro modo. Vedi la [Valutazione del percorso di accesso](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) di seguito.

#### Registrazione del requisito di autenticazione e del percorso di accesso con l&#39;autenticatore Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Poiché questo tipo di requisito di autenticazione deve essere limitato a determinate modalità di esecuzione e a un piccolo sottoinsieme di alberi all’interno dell’archivio dei contenuti, il tracciamento del tipo di mixin dei requisiti e delle proprietà del percorso di accesso è condizionale e associato a una configurazione corrispondente che definisce i percorsi supportati (vedi Opzioni di configurazione di seguito). Di conseguenza, solo le modifiche nell&#39;ambito di questi percorsi supportati attiveranno un aggiornamento della registrazione OSGi, altrove sia il tipo mixin che la proprietà verranno ignorati.

La configurazione di AEM predefinita ora utilizza questa configurazione consentendo di impostare il mixin in modalità di esecuzione dell’autore, ma di farlo avere effetto solo sulla replica nell’istanza di pubblicazione. Consulta [questa pagina](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) per i dettagli su come Sling applica il requisito di autenticazione.

Aggiungendo il tipo di mixin `granite:AuthenticationRequired` all&#39;interno dei percorsi supportati configurati, la registrazione OSGi del gestore responsabile verrà aggiornata con una nuova voce aggiuntiva con la proprietà `sling.auth.requirements` . Se un determinato requisito di autenticazione specifica la proprietà opzionale `granite:loginPath` , il valore viene registrato anche con l&#39;Autenticatore con il prefisso &quot;-&quot; per essere escluso dal requisito di autenticazione.

#### Valutazione e ereditarietà del requisito di autenticazione {#evaluation-and-inheritance-of-the-authentication-requirement}

I requisiti di autenticazione Apache Sling devono essere ereditati attraverso la gerarchia di pagine o nodi. I dettagli specifici dell’ereditarietà e della valutazione dei requisiti di autenticazione come l’ordine e la precedenza sono considerati dettagli di implementazione e non saranno documentati nel presente articolo.

#### Valutazione del percorso di accesso {#evaluation-of-login-path}

La valutazione del percorso di accesso e il reindirizzamento alla risorsa corrispondente al momento dell’autenticazione è attualmente un dettaglio di implementazione dell’Adobe Granite Login Selector Authentication Handler ( `com.day.cq.auth.impl.LoginSelectorHandler`), che è un Apache Sling AuthenticationHandler configurato con AEM per impostazione predefinita.

Quando si chiama `AuthenticationHandler.requestCredentials` questo gestore tenta di determinare la pagina di accesso per la mappatura a cui verrà reindirizzato l&#39;utente. Ciò include i seguenti passaggi:

* Distinguere tra la password scaduta e la necessità di un accesso regolare come motivo del reindirizzamento;
* In caso di accesso regolare, verifica se un percorso di accesso può essere ottenuto nel seguente ordine:

   * da LoginPathProvider come implementato dal nuovo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * dalla vecchia implementazione di CUG obsoleta,
   * dalle mappature di pagina di accesso, come definito con `LoginSelectorHandler`,
   * e infine, fallback alla pagina di accesso predefinita, come definita con `LoginSelectorHandler`.

* Non appena è stato ottenuto un percorso di accesso valido attraverso le chiamate elencate qui sopra, la richiesta dell&#39;utente verrà reindirizzata a quella pagina.

L&#39;obiettivo di questa documentazione è la valutazione del percorso di accesso come esposto dall&#39;interfaccia interna `LoginPathProvider`. L’implementazione fornita a partire da AEM 6.3 si comporta come segue:

* La registrazione dei percorsi di accesso dipende dalla distinzione tra password scaduta e la necessità di un accesso regolare come motivo del reindirizzamento
* In caso di accesso regolare, verifica se un percorso di accesso può essere ottenuto nel seguente ordine:

   * dal `LoginPathProvider` come implementato dal nuovo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * dalla vecchia implementazione di CUG obsoleta,
   * dalle mappature di pagina di accesso come definito con `LoginSelectorHandler`,
   * e infine fallback alla pagina di accesso predefinita come definita con il `LoginSelectorHandler`.

* Non appena è stato ottenuto un percorso di accesso valido attraverso le chiamate elencate qui sopra, la richiesta dell&#39;utente verrà reindirizzata a quella pagina.

Il `LoginPathProvider` implementato dal nuovo supporto per i requisiti di autenticazione in Granite espone i percorsi di accesso definiti dalle proprietà `granite:loginPath` , che a loro volta sono definiti dal tipo di mixin come descritto sopra. La mappatura del percorso della risorsa contenente il percorso di accesso e il valore della proprietà stesso viene mantenuta in memoria e viene valutata per trovare un percorso di accesso adatto per altri nodi della gerarchia.

>[!NOTE]
>
>La valutazione viene eseguita solo per le richieste associate alle risorse che si trovano nei percorsi supportati configurati. Per qualsiasi altra richiesta verranno valutati i modi alternativi per determinare il percorso di accesso.

#### Best practice    {#best-practices-1}

Quando definisci i requisiti di autenticazione, è necessario tenere conto delle seguenti best practice:

* Evita di nidificare i requisiti di autenticazione: l’inserimento di un singolo marcatore del requisito di autenticazione all’inizio di una struttura ad albero deve essere sufficiente ed è ereditato dall’intera sottostruttura definita dal nodo di destinazione. Ulteriori requisiti di autenticazione all’interno di tale albero dovrebbero essere considerati ridondanti e possono causare problemi di prestazioni durante la valutazione del requisito di autenticazione all’interno di Apache Sling. Con la separazione delle aree di CUG relative all&#39;autorizzazione e all&#39;autenticazione è possibile limitare l&#39;accesso in lettura tramite CUG o altri tipi di criteri, applicando al tempo stesso l&#39;autenticazione per l&#39;intero albero.
* Modellare il contenuto dell’archivio in modo che i requisiti di autenticazione si applichino all’intero albero senza la necessità di escludere nuovamente i sottoalberi nidificati dai requisiti.
* Per evitare di specificare e successivamente registrare percorsi di accesso ridondanti:

   * basarsi sull’ereditarietà ed evitare di definire percorsi di login nidificati,
   * non impostare il percorso di accesso facoltativo su un valore corrispondente al valore predefinito o ereditato,
   * gli sviluppatori di applicazioni devono identificare quali percorsi di accesso devono essere configurati nelle configurazioni del percorso di accesso globale (sia predefiniti che mappature) associate al `LoginSelectorHandler`.

## Rappresentazione nel repository {#representation-in-the-repository}

### Rappresentazione dei criteri CUG nell&#39;archivio {#cug-policy-representation-in-the-repository}

La documentazione Oak illustra come i nuovi criteri CUG si riflettono nel contenuto dell’archivio. Per ulteriori informazioni, consulta [questa pagina](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Autenticazione richiesta nell&#39;archivio {#authentication-requirement-in-the-repository}

La necessità di un requisito di autenticazione separato si riflette nel contenuto del repository con un tipo di nodo mixin dedicato posizionato sul nodo target. Il tipo di mixin definisce una proprietà opzionale per specificare una pagina di accesso dedicata per la struttura definita dal nodo di destinazione.

La pagina associata al percorso di accesso può trovarsi all’interno o all’esterno di tale struttura. Sarà escluso dal requisito di autenticazione.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gestione dei criteri e dei requisiti di autenticazione del gruppo utenti chiuso {#managing-cug-policies-and-authentication-requirement}

### Gestione dei criteri CUG {#managing-cug-policies}

Il nuovo tipo di criteri di controllo accessi per limitare l’accesso in lettura per un CUG viene gestito utilizzando l’API di gestione del controllo accessi JCR e segue i meccanismi descritti con la [specifica JCR 2.0](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html).

#### Imposta un nuovo criterio CUG {#set-a-new-cug-policy}

Codice per applicare un nuovo criterio CUG in un nodo in cui non è stato impostato un CUG in precedenza. Tieni presente che `getApplicablePolicies` restituirà solo i nuovi criteri non impostati in precedenza. Alla fine la politica deve essere riscritta e le modifiche devono essere mantenute.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Modificare un criterio CUG esistente {#edit-an-existing-cug-policy}

I passaggi seguenti sono necessari per modificare un criterio CUG esistente. Tieni presente che il criterio modificato deve essere riscritto e che le modifiche devono essere mantenute utilizzando `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### Recupera criteri CUG effettivi {#retrieve-effective-cug-policies}

La gestione del controllo di accesso JCR definisce un metodo di sforzo migliore per recuperare i criteri che hanno effetto in un determinato percorso. Poiché la valutazione dei criteri CUG è condizionale e dipende dalla configurazione corrispondente da abilitare, chiamare `getEffectivePolicies` è un modo conveniente per verificare se una determinata policy CUG sta avendo effetto in una determinata installazione.

>[!NOTE]
>
>Tieni presente la differenza tra `getEffectivePolicies` e l’esempio di codice successivo che attraversa la gerarchia per scoprire se un determinato percorso fa già parte di un CUG esistente.

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### Recupera criteri CUG ereditati {#retrieve-inherited-cug-policies}

Ricerca di tutti i CUG nidificati definiti in un determinato percorso indipendentemente dal fatto che abbiano o meno effetto. Per ulteriori informazioni, consulta la sezione [Opzioni di configurazione](/help/sites-administering/closed-user-groups.md#configuration-options) .

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### Gestione dei criteri per i gruppi di utenti chiusi (CUG) da parte di Principal {#managing-cug-policies-by-pincipal}

Le estensioni definite da `JackrabbitAccessControlManager` che consentono di modificare i criteri di controllo accessi in base all’entità non vengono implementate con la gestione del controllo accessi CUG, in quanto, per definizione, una policy CUG influisce sempre su tutte le entità: a quelli elencati con `PrincipalSetPolicy` viene concesso l&#39;accesso in lettura, mentre a tutte le altre entità principali verrà impedito di leggere il contenuto nella struttura definita dal nodo di destinazione.

I metodi corrispondenti restituiscono sempre una matrice di criteri vuota ma non generano eccezioni.

### Gestione del requisito di autenticazione {#managing-the-authentication-requirement}

La creazione, la modifica o la rimozione di nuovi requisiti di autenticazione si ottiene modificando il tipo di nodo effettivo del nodo di destinazione. La proprietà del percorso di accesso opzionale può quindi essere scritta utilizzando l’API JCR normale.

>[!NOTE]
>
>Le modifiche apportate a un dato nodo di destinazione menzionato sopra verranno applicate all’autenticazione Apache Sling solo se il `RequirementHandler` è stato configurato e il target è contenuto nelle strutture definite dai percorsi supportati (consulta la sezione Opzioni di configurazione ).
>
>Per ulteriori informazioni, consulta [Assegnazione di tipi di nodo misti](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Assegnazione di tipi di nodo misti) e [Aggiunta di nodi e impostazione di proprietà](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Aggiunta di nodi e impostazione di proprietà)

#### Aggiunta di un nuovo requisito di autenticazione {#adding-a-new-auth-requirement}

I passaggi per creare un nuovo requisito di autenticazione sono descritti di seguito. Tieni presente che il requisito verrà registrato con Apache Sling Authenticator solo se è stato configurato il `RequirementHandler` per la struttura ad albero contenente il nodo di destinazione.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Aggiungi un nuovo requisito di autenticazione con il percorso di accesso {#add-a-new-auth-requirement-with-login-path}

Passaggi per creare un nuovo requisito di autenticazione, incluso un percorso di accesso. Tieni presente che il requisito e l’esclusione per il percorso di accesso saranno registrati con l’autenticazione Apache Sling solo se è stato configurato il `RequirementHandler` per la struttura ad albero contenente il nodo di destinazione.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificare un percorso di accesso esistente {#modify-an-existing-login-path}

I passaggi per modificare un percorso di accesso esistente sono descritti di seguito. La modifica verrà registrata con Apache Sling Authenticator solo se è stato configurato il `RequirementHandler` per la struttura ad albero contenente il nodo di destinazione. Il valore del percorso di accesso precedente verrà rimosso dalla registrazione. Questa modifica non influisce sul requisito di autenticazione associato al nodo di destinazione.

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### Rimuovere un percorso di accesso esistente {#remove-an-existing-login-path}

Passaggi per rimuovere un percorso di accesso esistente. La voce del percorso di accesso verrà annullata dalla funzione di autenticazione Apache Sling solo se è stato configurato `RequirementHandler` per la struttura contenente il nodo di destinazione. Il requisito di autenticazione associato al nodo di destinazione non è interessato.

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

Oppure, puoi utilizzare il metodo seguente per raggiungere lo stesso scopo:

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### Rimuovere un requisito di autenticazione {#remove-an-auth-requirement}

Passaggi per rimuovere un requisito di autenticazione esistente. Il requisito verrà rimosso dalla registrazione dall&#39;Autenticatore Apache Sling solo se è stato configurato il `RequirementHandler` per la struttura ad albero contenente il nodo di destinazione.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recupera requisiti di autenticazione effettivi {#retrieve-effective-auth-requirements}

Non esiste un’API pubblica dedicata per leggere tutti i requisiti di autenticazione efficaci come registrati con Apache Sling Authenticator. Tuttavia, l&#39;elenco è esposto nella console di sistema in `https://<serveraddress>:<serverport>/system/console/slingauth` nella sezione &quot;**Configurazione del requisito di autenticazione**&quot;.

L’immagine seguente mostra i requisiti di autenticazione di un’istanza di pubblicazione AEM con contenuto demo. Il percorso evidenziato della pagina della community illustra come un requisito aggiunto dall’implementazione descritta in questo documento si riflette nell’Autenticatore Apache Sling.

>[!NOTE]
>
>In questo esempio la proprietà del percorso di accesso facoltativo non è stata impostata. Di conseguenza, non è stata registrata alcuna seconda voce presso l&#39;autenticatore.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Recupera il percorso di accesso effettivo {#retrieve-the-effective-login-path}

Al momento non è disponibile alcuna API pubblica per recuperare il percorso di accesso che entrerà in vigore quando si accede in modo anonimo a una risorsa che richiede l’autenticazione. Consulta la sezione Valutazione del percorso di accesso per i dettagli di implementazione sul modo in cui viene recuperato il percorso di accesso.

Tuttavia, oltre ai percorsi di accesso definiti con questa funzione, esistono modi alternativi per specificare il reindirizzamento all’accesso, che devono essere presi in considerazione durante la progettazione del modello di contenuto e i requisiti di autenticazione di una determinata installazione AEM.

#### Recupera il requisito di autenticazione ereditato {#retrieve-the-inherited-auth-requirement}

Come per il percorso di accesso, non esiste un’API pubblica per recuperare i requisiti di autenticazione ereditati definiti nel contenuto. L&#39;esempio seguente illustra come elencare tutti i requisiti di autenticazione definiti con una determinata gerarchia indipendentemente dal fatto che abbiano o meno effetto. Per ulteriori informazioni, consulta [Opzioni di configurazione](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>Si consiglia di basarsi sul meccanismo di ereditarietà sia per i requisiti di autenticazione che per il percorso di accesso ed evitare la creazione di requisiti di autenticazione nidificati.
>
>Per ulteriori informazioni, consulta [Valutazione e ereditarietà dei requisiti di autenticazione](#evaluation-and-inheritance-of-the-authentication-requirement), [Valutazione del percorso di accesso](#evaluation-of-login-path) e [Best practice](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### Combinazione di criteri per il gruppo utenti chiuso e dei requisiti di autenticazione {#combining-cug-policies-and-the-authentication-requirement}

Nella tabella seguente sono elencate le combinazioni valide di criteri CUG e i requisiti di autenticazione in un’istanza AEM che ha entrambi i moduli abilitati tramite la configurazione.

| **Autenticazione richiesta** | **Percorso di accesso** | **Accesso in lettura limitato** | **Effetto previsto** |
|---|---|---|---|
| Sì | Sì | Sì | Un determinato utente può visualizzare la struttura secondaria contrassegnata con i criteri CUG solo se una valutazione efficace delle autorizzazioni consente l’accesso. Un utente non autenticato verrà reindirizzato alla pagina di accesso specificata. |
| Sì | No | Sì | Un determinato utente può visualizzare la struttura secondaria contrassegnata con i criteri CUG solo se una valutazione efficace delle autorizzazioni consente l’accesso. Un utente non autenticato verrà reindirizzato a una pagina di accesso predefinita ereditata. |
| Sì | Sì | No | Un utente non autenticato verrà reindirizzato alla pagina di accesso specificata. Il fatto che sia consentito o meno visualizzare la struttura contrassegnata con il requisito di autorizzazione dipende dalle autorizzazioni effettive dei singoli elementi contenuti nella sottostruttura. Nessun CUG dedicato che limita l&#39;accesso in lettura. |
| Sì | No | No | Un utente non autenticato verrà reindirizzato a una pagina di accesso predefinita ereditata. Il fatto che sia consentito o meno visualizzare la struttura contrassegnata con il requisito di autorizzazione dipende dalle autorizzazioni effettive dei singoli elementi contenuti nella sottostruttura. Nessun CUG dedicato che limita l&#39;accesso in lettura. |
| No | No | Sì | Un utente autenticato o non autenticato può visualizzare la struttura secondaria contrassegnata con i criteri CUG solo se una valutazione efficace delle autorizzazioni consente l&#39;accesso. Un utente non autenticato verrà trattato allo stesso modo e non verrà reindirizzato all&#39;accesso. |

>[!NOTE]
>
>La combinazione di &quot;Autenticazione richiesta&quot; = No e &quot;Percorso di accesso&quot; = Sì non è elencata sopra, in quanto il &quot;Percorso di accesso&quot; è un attributo facoltativo associato a un requisito di autenticazione. La specifica di una proprietà JCR con quel nome senza aggiungere il tipo di mixin di definizione non avrà alcun effetto e verrà ignorata dal gestore corrispondente.

## Componenti e configurazione OSGi {#osgi-components-and-configuration}

Questa sezione fornisce una panoramica dei componenti OSGi e delle singole opzioni di configurazione introdotte con la nuova implementazione CUG.

Vedi anche la documentazione sulla mappatura CUG per una mappatura completa delle opzioni di configurazione tra la vecchia e la nuova implementazione.

### Autorizzazione: Configurazione e configurazione {#authorization-setup-and-configuration}

Le nuove parti relative all&#39;autorizzazione sono contenute nel bundle **Oak CUG Authorization** ( `org.apache.jackrabbit.oak-authorization-cug`), che fa parte dell&#39;installazione predefinita AEM. Il bundle definisce un modello di autorizzazione separato che deve essere distribuito come modo aggiuntivo per gestire l&#39;accesso in lettura.

#### Impostazione dell&#39;autorizzazione CUG {#setting-up-cug-authorization}

L&#39;impostazione dell&#39;autorizzazione CUG è descritta in dettaglio nella [documentazione Apache pertinente](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Per impostazione predefinita, AEM l’autorizzazione CUG è distribuita in tutte le modalità di esecuzione. Le istruzioni dettagliate possono essere utilizzate anche per disabilitare l’autorizzazione CUG nelle installazioni che richiedono un’autorizzazione diversa.

#### Configurazione del filtro di riferimento {#configuring-the-referrer-filter}

È inoltre necessario configurare il [filtro referente Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) con tutti i nomi host che possono essere utilizzati per accedere a AEM; ad esempio, tramite CDN, Load Balancer e altri.

Se il filtro di riferimento non è configurato, quando un utente tenta di accedere a un sito CUG vengono visualizzati errori simili a quelli seguenti:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Caratteristiche dei componenti OSGi {#characteristics-of-osgi-components}

Sono stati introdotti i due componenti OSGi seguenti per definire i requisiti di autenticazione e specificare percorsi di accesso dedicati:

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Etichetta</td>
   <td>Configurazione CUG Apache Jackrabbit Oak</td>
  </tr>
  <tr>
   <td>Descrizione</td>
   <td>Configurazione dell’autorizzazione dedicata alla configurazione e alla valutazione delle autorizzazioni CUG.</td>
  </tr>
  <tr>
   <td>Proprietà di configurazione</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Inoltre, vedi <a href="#configuration-options">Opzioni di configurazione</a> di seguito.</p> </td>
  </tr>
  <tr>
   <td>Criterio di configurazione</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Riferimenti</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>Etichetta</td>
   <td>Elenco di esclusione di Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descrizione</td>
   <td>Consente di escludere entità principali con i nomi configurati dalla valutazione CUG.</td>
  </tr>
  <tr>
   <td>Proprietà di configurazione</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Consulta anche la sezione Opzioni di configurazione di seguito.</p> </td>
  </tr>
  <tr>
   <td>Criterio di configurazione</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Riferimenti</td>
   <td>ND</td>
  </tr>
 </tbody>
</table>

#### Opzioni di configurazione {#configuration-options}

Le opzioni di configurazione chiave sono:

* `cugSupportedPaths`: specificare le sottostrutture che possono contenere CUG. Nessun valore predefinito impostato
* `cugEnabled`: opzione di configurazione per abilitare la valutazione delle autorizzazioni per i criteri CUG correnti.

Le opzioni di configurazione disponibili associate al modulo di autorizzazione CUG sono elencate e descritte più dettagliatamente nella [Documentazione Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Esclusione di entità dalla valutazione del gruppo utenti chiuso {#excluding-principals-from-cug-evaluation}

L&#39;esenzione dei singoli principi dalla valutazione del CUG è stata adottata dalla prima attuazione. La nuova autorizzazione CUG lo copre con un’interfaccia dedicata denominata CugExclude. Apache Jackrabbit Oak 1.4 viene fornito con un&#39;implementazione predefinita che esclude un set fisso di entità e un&#39;implementazione estesa che consente di configurare i singoli nomi principali. Quest’ultimo è configurato in AEM istanze di pubblicazione.

L’impostazione predefinita a partire da AEM 6.3 impedisce che i seguenti principi siano influenzati dai criteri CUG:

* entità amministrative (utente amministratore, gruppo amministratori)
* entità utente del servizio
* repository interno system principal

Per ulteriori informazioni, consulta la tabella nella sezione [Configurazione predefinita dal AEM 6.3](#default-configuration-since-aem) di seguito.

L&#39;esclusione del gruppo &quot;amministratori&quot; può essere modificata o espansa nella console di sistema nella sezione di configurazione di **Apache Jackrabbit Oak CUG Exclude List**.

In alternativa, è possibile fornire e distribuire un&#39;implementazione personalizzata dell&#39;interfaccia CugExclude per regolare il set di entità escluse in caso di esigenze speciali. Per informazioni dettagliate e un esempio di implementazione, consulta la documentazione sulla [plug-in CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) .

### Autenticazione: Configurazione e configurazione {#authentication-setup-and-configuration}

Le nuove parti correlate all&#39;autenticazione sono contenute nel bundle **Adobe Granite Authentication Handler** ( `com.adobe.granite.auth.authhandler` versione 5.6.48). Questo bundle fa parte dell&#39;installazione predefinita AEM.

Per impostare la sostituzione del requisito di autenticazione per il supporto CUG obsoleto, alcuni componenti OSGi devono essere presenti e attivi in una determinata installazione AEM. Per ulteriori dettagli, consulta **Caratteristiche dei componenti OSGi** di seguito.

>[!NOTE]
>
>A causa dell&#39;opzione di configurazione obbligatoria con RequirementHandler, le parti relative all&#39;autenticazione saranno attive solo se la funzione è stata abilitata specificando un set di percorsi supportati. Con un’installazione AEM standard, la funzione è disabilitata in modalità di esecuzione dell’autore e abilitata per /content in modalità di esecuzione della pubblicazione.

**Caratteristiche dei componenti OSGi**

Sono stati introdotti i seguenti 2 componenti OSGi per definire i requisiti di autenticazione e specificare percorsi di login dedicati:

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirements.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>Etichetta</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Descrizione</td>
   <td>Servizio OSGi dedicato per i requisiti di autenticazione che registra un osservatore per le modifiche dei contenuti che influiscono sui requisiti di autenticazione (attraverso il tipo di mixin <code>granite:AuthenticationRequirement</code>) e i percorsi di accesso con sono esposti al <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Proprietà di configurazione</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Criterio di configurazione</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>Riferimenti</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler**

| Etichetta | Adobe Granite Authentication Requirements e Login Path Handler |
|---|---|
| Descrizione | `RequirementHandler` implementazione che aggiorna i requisiti di autenticazione Apache Sling e la corrispondente esclusione per i percorsi di accesso associati. |
| Proprietà di configurazione | `supportedPaths` |
| Criterio di configurazione | `ConfigurationPolicy.REQUIRE` |
| Riferimenti | ND |

#### Opzioni di configurazione {#configuration-options-1}

Le parti correlate all’autenticazione della riscrittura CUG sono associate solo a una singola opzione di configurazione associata all’Adobe Requisiti di autenticazione Granite e Gestore del percorso di accesso:

**&quot;Autenticazione richiesta e gestore del percorso di accesso&quot;**

<table>
 <tbody>
  <tr>
   <td>Proprietà</td>
   <td>Tipo</td>
   <td>Valore predefinito</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><p>Etichetta = Percorsi supportati</p> <p>Name = 'supportedPaths'</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>Percorsi in cui i requisiti di autenticazione saranno rispettati da questo gestore. Lascia disattivata questa configurazione se desideri aggiungere il tipo di mixin <code>granite:AuthenticationRequirement</code> ai nodi senza farli applicare (ad esempio, sulle istanze dell’autore). Se mancante, la funzione è disabilitata. </td>
  </tr>
 </tbody>
</table>

## Configurazione predefinita a partire da AEM 6.3 {#default-configuration-since-aem}

Per impostazione predefinita, le nuove installazioni di AEM utilizzeranno le nuove implementazioni sia per le parti relative all’autorizzazione che per l’autenticazione della funzione CUG. La vecchia implementazione &quot;Adobe Granite Closed User Group (CUG) Support&quot; è stata deprecata e verrà disabilitata per impostazione predefinita in tutte le installazioni AEM. Le nuove implementazioni verranno invece abilitate come segue:

### Istanze autore {#author-instances}

| **&quot;Configurazione CUG Apache Jackrabbit Oak&quot;** | **Spiegazione** |
|---|---|
| Percorsi supportati `/content` | La gestione del controllo degli accessi per i criteri CUG è abilitata. |
| Valutazione CUG abilitata FALSE | La valutazione delle autorizzazioni è disabilitata. Le politiche CUG non hanno alcun effetto. |
| Classificazione | 200 | Consulta la documentazione Oak. |

>[!NOTE]
>
>Nelle istanze di authoring predefinite non è presente alcuna configurazione per **Apache Jackrabbit Oak CUG Exclude List** e **Adobe Granite Authentication Requirements and Login Path Handler**.

### Pubblica istanze {#publish-instances}

| **&quot;Configurazione CUG Apache Jackrabbit Oak&quot;** | **Spiegazione** |
|---|---|
| Percorsi supportati `/content` | La gestione del controllo degli accessi per i criteri CUG è abilitata nei percorsi configurati. |
| Valutazione CUG abilitata TRUE | La valutazione delle autorizzazioni è abilitata nei percorsi configurati. I criteri CUG hanno effetto a partire da `Session.save()`. |
| Classificazione | 200 | Consulta la documentazione Oak. |

| **&quot;Elenco di esclusione di Apache Jackrabbit Oak CUG&quot;** | **Spiegazione** |
|---|---|
| Amministratori dei nomi principali | Esclude l’entità amministratore dalla valutazione CUG. |

| **&quot;Adobe Granite Authentication Requirements and Login Path Handler&quot;** | **Spiegazione** |
|---|---|
| Percorsi supportati `/content` | I requisiti di autenticazione definiti nell’archivio tramite il tipo di mixin `granite:AuthenticationRequired` hanno effetto al di sotto di `/content` in data `Session.save()`. Sling Authenticator viene aggiornato. L’aggiunta del tipo di mixin all’esterno dei percorsi supportati viene ignorata. |

## Disabilitazione del requisito di autorizzazione e autenticazione CUG {#disabling-cug-authorization-and-authentication-requirement}

La nuova implementazione può essere completamente disattivata nel caso in cui una determinata installazione non utilizzi CUG o utilizzi mezzi diversi per l’autenticazione e l’autorizzazione.

### Disattiva autorizzazione CUG {#disable-cug-authorization}

Per informazioni dettagliate su come rimuovere il modello di autorizzazione CUG dalla configurazione dell&#39;autorizzazione composita, consultare la documentazione relativa alla [pluggability CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) .

### Disattiva il requisito di autenticazione {#disable-the-authentication-requirement}

Per disabilitare il supporto per i requisiti di autenticazione forniti dal modulo `granite.auth.authhandler` è sufficiente rimuovere la configurazione associata a **Adobe Granite Authentication Requirements and Login Path Handler**.

>[!NOTE]
>
>Tuttavia, la rimozione della configurazione non annullerà la registrazione del tipo di mixin, che era ancora applicabile ai nodi senza prendere effetto.

## Interazione con altri moduli {#interaction-with-other-modules}

### API Jackrabbit di Apache {#apache-jackrabbit-api}

Al fine di rispettare il nuovo tipo di politica di controllo degli accessi utilizzata dal modello di autorizzazione CUG, l’API definita da Apache Jackrabbit è stata estesa. A partire dalla versione 2.11.0 del modulo `jackrabbit-api`, definisce una nuova interfaccia denominata `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` che si estende da `javax.jcr.security.AccessControlPolicy`.

### FileVault Apache Jackrabbit {#apache-jackrabbit-filevault}

Il meccanismo di importazione di Apache Jackrabbit FileVault è stato modificato per gestire le politiche di controllo degli accessi di tipo `PrincipalSetPolicy`.

### Distribuzione dei contenuti Sling Apache {#apache-sling-content-distribution}

Vedi la sezione [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) precedente.

### Replica Granite Adobe {#adobe-granite-replication}

Il modulo di replica è stato leggermente modificato per poter replicare i criteri CUG tra diverse istanze AEM:

* `DurboImportConfiguration.isImportAcl()` viene interpretato letteralmente e influenzerà solo le politiche di controllo degli accessi che si implementano  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` rispetterà questa configurazione solo per le ACL vere
* Altri criteri come le istanze `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` create dal modello di autorizzazione CUG verranno sempre replicati e l&#39;opzione di configurazione `DurboImportConfiguration.isImportAcl`() verrà ignorata.

C&#39;è un limite di replicare le politiche CUG. Se un determinato criterio CUG viene rimosso senza rimuovere il corrispondente tipo di nodo mixin `rep:CugMixin,`, la rimozione non verrà riflessa in fase di replica. Questo problema è stato affrontato rimuovendo sempre il mixin al momento della rimozione delle politiche. La limitazione può tuttavia apparire se il tipo di mixin viene aggiunto manualmente.

### Adobe gestore di autenticazione Granite {#adobe-granite-authentication-handler}

Il gestore di autenticazione **Adobe Granite HTTP Header Authentication Handler** fornito con il bundle `com.adobe.granite.auth.authhandler` contiene un riferimento all&#39;interfaccia `CugSupport` definita dallo stesso modulo. Viene utilizzato per calcolare il &quot;realm&quot; in alcune circostanze, rientrando nel realm configurato con il gestore.

È stato modificato per rendere facoltativo il riferimento a `CugSupport` al fine di garantire la massima compatibilità con le versioni precedenti se una determinata configurazione decide di riabilitare l’implementazione obsoleta. Le installazioni che utilizzano l&#39;implementazione non otterranno più il realm estratto dall&#39;implementazione CUG, ma visualizzeranno sempre il realm come definito con **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>Per impostazione predefinita, il **gestore di autenticazione delle intestazioni HTTP Granite** di Adobe è configurato solo in modalità di esecuzione di pubblicazione con l&#39;opzione &quot;Disattiva pagina di accesso&quot; ( `auth.http.nologin`) abilitata.

### AEM Live Copy {#aem-livecopy}

La configurazione dei CUG in combinazione con LiveCopy è rappresentata nell’archivio dall’aggiunta di un nodo aggiuntivo e di una proprietà aggiuntiva come segue:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Entrambi questi elementi vengono creati sotto `cq:Page`. Con la progettazione corrente, MSM gestisce solo i nodi e le proprietà che si trovano sotto il nodo `cq:PageContent` (`jcr:content`).

Pertanto, i gruppi CUG non possono essere implementati in Live Copy da Blueprint. Pianifica tutto questo durante la configurazione di Live Copy.

## Modifiche all’implementazione del nuovo CUG {#changes-with-the-new-cug-implementation}

Lo scopo di questa sezione è quello di fornire una panoramica delle modifiche apportate alla funzione CUG e un confronto tra la vecchia e la nuova implementazione. Elenca le modifiche che influiscono sulla configurazione del supporto CUG e descrive come e da chi vengono gestiti i CUG nel contenuto dell’archivio.

### Differenze di configurazione e configurazione del gruppo utenti chiuso {#differences-in-cug-setup-and-configuration}

Il componente OSGi **Adobe Granite Closed User Group (CUG) Support** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) è stato sostituito da nuovi componenti per poter gestire separatamente le parti relative all&#39;autorizzazione e all&#39;autenticazione della precedente funzionalità CUG.

## Differenze nella gestione dei gruppi di utenti chiusi nel contenuto dell’archivio {#differences-in-managing-cugs-in-the-repository-content}

Le sezioni seguenti descrivono le differenze tra le vecchie e le nuove implementazioni dal punto di vista dell&#39;implementazione e della sicurezza. Anche se la nuova implementazione ha lo scopo di fornire la stessa funzionalità, ci sono sottili modifiche che è importante sapere quando si utilizza il nuovo CUG.

### Differenze Relative All&#39;Autorizzazione {#differences-with-regards-to-authorization}

Le principali differenze dal punto di vista dell&#39;autorizzazione sono riassunte nell&#39;elenco seguente:

**Contenuto del controllo di accesso dedicato per i gruppi di utenti chiusi**

Nella vecchia implementazione, il modello di autorizzazione predefinito è stato utilizzato per manipolare i criteri dell’elenco di controllo accessi in fase di pubblicazione, sostituendo gli ACE esistenti con la configurazione richiesta dal gruppo di lavoro utenti chiuso. Questo è stato attivato scrivendo proprietà JCR regolari e residue interpretate al momento della pubblicazione.

Con la nuova implementazione, la configurazione del controllo di accesso del modello di autorizzazione predefinito non viene influenzata da alcun CUG creato, modificato o rimosso. Al contrario, un nuovo tipo di criterio denominato `PrincipalSetPolicy` viene applicato come contenuto aggiuntivo per il controllo accessi al nodo di destinazione. Questo criterio aggiuntivo si trova come secondario del nodo di destinazione e, se presente, sarà di pari livello del nodo di criterio predefinito.

**Modifica dei criteri CUG in Gestione controllo accessi**

Questo passaggio dalle proprietà JCR residue a una politica di controllo degli accessi dedicata ha un impatto sull&#39;autorizzazione necessaria per creare o modificare la parte di autorizzazione della funzione CUG. Poiché questa operazione è considerata una modifica per accedere ai contenuti di controllo, per poter essere scritti nell’archivio sono necessari i privilegi `jcr:readAccessControl` e `jcr:modifyAccessControl` . Pertanto, solo gli autori di contenuti autorizzati a modificare il contenuto del controllo di accesso di una pagina possono impostare o modificare tale contenuto. Ciò contrasta con la vecchia implementazione in cui la capacità di scrivere proprietà JCR regolari era sufficiente, dando luogo a un&#39;escalation dei privilegi.

**Nodo Di Target Definito Dal Criterio**

I criteri CUG devono essere creati nel nodo JCR che definisce la sottostruttura soggetta a restrizioni di accesso in lettura. È probabile che si tratti di una pagina AEM nel caso in cui il CUG si verifichi un impatto sull’intero albero.

Tieni presente che il posizionamento del criterio CUG solo sul nodo jcr:content situato sotto una determinata pagina limiterà l’accesso al contenuto s.str di una data pagina, ma non avrà effetto su alcuna pagina di pari livello o secondaria. Questo può essere un caso d’uso valido ed è possibile ottenere con un editor di repository che consente di applicare contenuti di accesso a grana fine. Tuttavia, contrasta la precedente implementazione in cui il posizionamento di una proprietà cq:cugEnabled sul nodo jcr:content è stato ricapitato internamente al nodo della pagina. Questa mappatura non viene più eseguita.

**Valutazione delle autorizzazioni con i criteri CUG**

Spostandosi dal vecchio supporto CUG a un modello di autorizzazione aggiuntivo, cambia il modo in cui vengono valutate le autorizzazioni di lettura efficaci. Come descritto nella [documentazione Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), a un determinato entità autorizzato a visualizzare il `CUGcontent` sarà concesso l&#39;accesso in lettura solo se la valutazione delle autorizzazioni di tutti i modelli configurati nell&#39;archivio Oak concede l&#39;accesso in lettura.

In altre parole, per la valutazione delle autorizzazioni effettive, verranno prese in considerazione sia le voci `CUGPolicy` che le voci predefinite per il controllo degli accessi e l’accesso in lettura al contenuto CUG sarà concesso solo se concesso da entrambi i tipi di criteri. In un’installazione di pubblicazione AEM predefinita in cui l’accesso in lettura all’albero completo `/content` è concesso a tutti, l’effetto dei criteri CUG sarà lo stesso della vecchia implementazione.

**Valutazione su richiesta**

Il modello di autorizzazione CUG consente di attivare singolarmente la gestione del controllo degli accessi e la valutazione delle autorizzazioni:

* la gestione del controllo degli accessi è abilitata se il modulo dispone di uno o più percorsi supportati in cui è possibile creare CUG
* la valutazione delle autorizzazioni è abilitata solo se l&#39;opzione **Valutazione CUG abilitata** è selezionata.

Nella nuova valutazione di impostazione predefinita AEM dei criteri CUG è abilitata solo con la modalità di esecuzione &quot;pubblica&quot;. Per ulteriori informazioni, consulta i dettagli sulla [configurazione predefinita a partire da AEM 6.3](#default-configuration-since-aem) . Questo può essere verificato confrontando i criteri effettivi per un determinato percorso con i criteri memorizzati nel contenuto. Le politiche efficaci saranno visualizzate solo se è abilitata la valutazione delle autorizzazioni per i CUG.

Come spiegato in precedenza, i criteri di controllo accessi CUG ora sono sempre memorizzati nel contenuto, ma la valutazione delle autorizzazioni effettive risultanti da tali criteri verrà applicata solo se **CUG Evaluation Enabled** è attivata nella console del sistema in Apache Jackrabbit Oak **CUG Configuration.** Per impostazione predefinita, è attivato solo con la modalità di esecuzione &quot;pubblica&quot;.

### Differenze Relative All&#39;Autenticazione {#differences-with-regards-to-authentication}

Di seguito sono descritte le differenze relative all&#39;autenticazione.

#### Tipo Mixin Dedicato Per Il Requisito Di Autenticazione {#dedicated-mixin-type-for-authentication-requirement}

Nella prima implementazione, sia gli aspetti di autorizzazione che di autenticazione di un CUG sono stati attivati da una singola proprietà JCR ( `cq:cugEnabled`). Per quanto riguarda l’autenticazione, ciò ha portato a un elenco aggiornato dei requisiti di autenticazione memorizzati con l’implementazione Apache Sling Authenticator. Con la nuova implementazione lo stesso risultato si ottiene contrassegnando il nodo target con un tipo di mixin dedicato ( `granite:AuthenticationRequired`).

#### Proprietà Per Escludere Il Percorso Di Accesso {#property-for-excluding-login-path}

Il tipo di mixin definisce una singola proprietà facoltativa denominata `granite:loginPath`, che corrisponde fondamentalmente alla proprietà `cq:cugLoginPage` . A differenza dell&#39;implementazione precedente, la proprietà del percorso di accesso verrà rispettata solo se il tipo di nodo dichiarante è il mixin menzionato. L&#39;aggiunta di una proprietà con quel nome senza impostare il tipo di mixin non avrà alcun effetto e né un nuovo requisito né un&#39;esclusione per il percorso di accesso saranno segnalati all&#39;autenticatore.

#### Privilegio per il requisito di autenticazione {#privilege-for-authentication-requirement}

Per aggiungere o rimuovere un tipo di mixin è necessario concedere il privilegio `jcr:nodeTypeManagement` . Nell’implementazione precedente, il privilegio `jcr:modifyProperties` viene utilizzato per modificare la proprietà residua.

Per quanto riguarda `granite:loginPath`, lo stesso privilegio è necessario per aggiungere, modificare o rimuovere la proprietà.

#### Nodo di destinazione definito dal tipo di mixin {#target-node-defined-by-mixin-type}

I requisiti di autenticazione devono essere creati nel nodo JCR che definisce la sottostruttura soggetta all’accesso imposto. È probabile che si tratti di una pagina AEM nel caso in cui il CUG influisca sull’intero albero e l’interfaccia utente per la nuova implementazione aggiungerà di conseguenza il tipo di mixin per requisiti di autenticazione sul nodo della pagina.

Posizionare il criterio CUG solo sul nodo jcr:content situato sotto una determinata pagina limiterà l’accesso ai contenuti, ma non avrà effetto né sul nodo della pagina stesso né su alcuna pagina figlia.

Questo può essere uno scenario valido ed è possibile con un editor di repository che consente di inserire il mixin a qualsiasi nodo. Tuttavia, il comportamento contrasta con l’implementazione precedente, in cui il posizionamento di una proprietà cq:cugEnabled o cq:cugLoginPage sul nodo jcr:content veniva ricollegato internamente in ultima istanza al nodo della pagina. Questa mappatura non viene più eseguita.

#### Percorsi supportati configurati {#configured-supported-paths}

Sia il tipo mixin `granite:AuthenticationRequired` che la proprietà granite:loginPath verranno rispettati solo nell&#39;ambito definito dall&#39;insieme di **Paths** supportati disponibili con l&#39;opzione di configurazione **Adobe Granite Authentication Requirements and Login Path Handler**. Se non è stato specificato alcun percorso, la funzione dei requisiti di autenticazione è disabilitata completamente. In questo caso il tipo di mixin o la proprietà hanno effetto quando vengono aggiunti o impostati su un dato nodo JCR.

### Mappatura del contenuto JCR, dei servizi OSGi e delle configurazioni {#mapping-of-jcr-content-osgi-services-and-configurations}

Il documento seguente fornisce una mappatura completa dei servizi, delle configurazioni e del contenuto del repository OSGi tra la vecchia e la nuova implementazione.

Mappatura CUG a partire da AEM 6.3

[Ottieni file](assets/cug-mapping.pdf)

## Aggiorna CUG {#upgrade-cug}

### Installazioni esistenti tramite CUG obsoleto {#existing-installations-using-the-deprecated-cug}

L’implementazione del supporto per CUG precedente è stata dichiarata obsoleta e verrà rimossa per nelle versioni future. Si consiglia di passare alle nuove implementazioni quando si esegue l&#39;aggiornamento da versioni precedenti alla versione 6.3 di AEM.

Per l’installazione AEM aggiornata, è importante assicurarsi che sia abilitata una sola implementazione CUG. La combinazione del nuovo e del vecchio supporto per CUG obsoleto non viene testata ed è probabile che causi un comportamento indesiderato:

* conflitti in Sling Authenticator per quanto riguarda i requisiti di autenticazione
* accesso in lettura negato quando l&#39;impostazione ACL associata al vecchio CUG si scontra con un nuovo criterio CUG.

### Migrazione di contenuti CUG esistenti {#migrating-existing-cug-content}

Adobe fornisce uno strumento per la migrazione alla nuova implementazione CUG. Per utilizzarlo, effettua le seguenti operazioni:

1. Vai a `https://<serveraddress>:<serverport>/system/console/cug-migration` per accedere allo strumento.
1. Immettere il percorso principale per il quale si desidera controllare i CUG e premere il pulsante **Esegui esecuzione a secco**. Verranno analizzati i gruppi di utenti chiusi idonei alla conversione nella posizione selezionata.
1. Dopo aver esaminato i risultati, premi il pulsante **Esegui migrazione** per eseguire la migrazione alla nuova implementazione.

>[!NOTE]
>
>In caso di problemi, è possibile impostare un logger specifico a livello **DEBUG** su `com.day.cq.auth.impl.cug` per ottenere l&#39;output dello strumento di migrazione. Per ulteriori informazioni su come eseguire questa operazione, consulta [Logging](/help/sites-deploying/configure-logging.md) .
