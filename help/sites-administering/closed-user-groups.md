---
title: Gruppi di utenti chiusi in AEM
description: Scopri i gruppi chiusi di utenti e i vantaggi che offrono in termini di scalabilità e sicurezza in AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '6654'
ht-degree: 0%

---

# Gruppi di utenti chiusi in AEM{#closed-user-groups-in-aem}

## Introduzione {#introduction}

A partire da AEM 6.3, esiste una nuova implementazione di Gruppo utenti chiuso destinata a risolvere i problemi di prestazioni, scalabilità e sicurezza presenti con l’implementazione esistente.

>[!NOTE]
>
>Per semplicità, in questa documentazione viene utilizzata l’abbreviazione CUG.

L’obiettivo della nuova implementazione è quello di coprire le funzionalità esistenti quando necessario, affrontando al contempo i problemi e le limitazioni di progettazione delle versioni precedenti. Il risultato è un nuovo design CUG con le seguenti caratteristiche:

* chiara separazione degli elementi di autenticazione e autorizzazione, che possono essere utilizzati singolarmente o in combinazione;
* Modello di autorizzazione dedicato per riflettere l’accesso in lettura limitato agli alberi del gruppo di utenti chiusi configurati senza interferire con altri requisiti di configurazione e autorizzazione del controllo degli accessi;
* Separazione tra l’impostazione di controllo degli accessi con accesso in lettura limitato, necessaria per le istanze di authoring, e la valutazione delle autorizzazioni, richiesta solo per la pubblicazione;
* Modifica dell&#39;accesso in lettura limitato senza escalation dei privilegi;
* Estensione del tipo di nodo dedicata per contrassegnare il requisito di autenticazione;
* Percorso di accesso facoltativo associato al requisito di autenticazione.

### Implementazione del nuovo gruppo utenti personalizzato {#the-new-custom-user-group-implementation}

Un CUG come è noto nel contesto di AEM è costituito dai seguenti passaggi:

* Limita l&#39;accesso in lettura alla struttura che deve essere protetta e consente la lettura solo per le entità principali elencate con una determinata istanza del gruppo utenti chiusi o escluse completamente dalla valutazione del gruppo utenti chiusi. Elemento denominato **authorization**.
* Applica l’autenticazione a una determinata struttura e, facoltativamente, specifica una pagina di accesso dedicata per la struttura da escludere. Elemento **authentication**.

La nuova implementazione è stata progettata per tracciare una linea tra gli elementi di autenticazione e di autorizzazione. A partire da AEM 6.3, è possibile limitare l’accesso in lettura senza aggiungere esplicitamente un requisito di autenticazione. Ad esempio, se una determinata istanza richiede completamente l’autenticazione oppure una determinata struttura già risiede in una sottostruttura che richiede già l’autenticazione.

Allo stesso modo, una determinata struttura può essere contrassegnata con un requisito di autenticazione senza modificare la configurazione delle autorizzazioni effettiva. Le combinazioni e i risultati sono elencati nella sezione [Combinazione di criteri CUG e requisiti di autenticazione](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement).

## Panoramica {#overview}

### Autorizzazione: limitazione dell’accesso in lettura {#authorization-restricting-read-access}

La funzione chiave di un gruppo utenti chiusi limita l’accesso in lettura a una determinata struttura nell’archivio dei contenuti per tutti gli utenti eccetto le entità selezionate. Invece di manipolare istantaneamente il contenuto di controllo di accesso predefinito, la nuova implementazione adotta un approccio diverso definendo un tipo dedicato di criteri di controllo di accesso che rappresenta un CUG.

#### Criterio di controllo accesso per CUG {#access-control-policy-for-cug}

Questo nuovo tipo di polizza presenta le seguenti caratteristiche:

* Criteri di controllo degli accessi di tipo org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (definito dall’API Apache Jackrabbit);
* PrincipalSetPolicy concede privilegi a un insieme modificabile di entità;
* I privilegi concessi e l’ambito del criterio sono un dettaglio di implementazione.

L’implementazione di PrincipalSetPolicy utilizzata per rappresentare i gruppi di utenti chiusi (CUG) definisce inoltre quanto segue:

* I criteri CUG concedono l’accesso in lettura solo agli elementi JCR regolari (ad esempio, il contenuto di controllo dell’accesso è escluso);
* L’ambito è definito dal nodo con controllo di accesso che detiene il criterio CUG;
* I criteri CUG possono essere nidificati, un CUG nidificato avvia un nuovo CUG senza ereditare il set principale del CUG &quot;padre&quot;;
* Se la valutazione è abilitata, l&#39;effetto del criterio viene ereditato dall&#39;intera sottostruttura fino al successivo CUG nidificato.

Questi criteri CUG vengono distribuiti in un’istanza AEM tramite un modulo di autorizzazione separato denominato oak-authorization-cug. Questo modulo include la propria gestione del controllo di accesso e la valutazione delle autorizzazioni. In altre parole, la configurazione predefinita di AEM prevede una configurazione dell’archivio dei contenuti di Oak che combina più meccanismi di autorizzazione. Per ulteriori informazioni, consulta [questa pagina nella documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

In questa configurazione composita, un nuovo CUG non sostituisce il contenuto di controllo di accesso esistente associato al nodo di destinazione. Si tratta invece di un supplemento che può essere rimosso in seguito senza influire sul controllo di accesso originale, che per impostazione predefinita in AEM sarebbe un elenco di controllo di accesso.

A differenza della precedente implementazione, i nuovi criteri CUG vengono sempre riconosciuti e trattati come contenuti di controllo dell’accesso. Ciò implica che vengono create e modificate utilizzando l’API di gestione del controllo di accesso JCR. Per ulteriori informazioni, consulta la sezione [Gestione dei criteri CUG](#managing-cug-policies).

#### Valutazione delle autorizzazioni dei criteri CUG {#permission-evaluation-of-cug-policies}

Oltre a una gestione dedicata del controllo degli accessi per i gruppi di utenti chiusi (CUG), il nuovo modello di autorizzazione consente di abilitare in modo condizionale la valutazione delle autorizzazioni per i relativi criteri. Questo consente di impostare i criteri per i gruppi utenti chiusi (CUG) in un ambiente di staging e di valutare solo le autorizzazioni valide una volta replicate nell’ambiente di produzione.

La valutazione delle autorizzazioni per i criteri CUG e l’interazione con il modello di autorizzazione predefinito o aggiuntivo segue il modello progettato per più meccanismi di autorizzazione in Apache Jackrabbit Oak. In altre parole, un determinato set di autorizzazioni viene concesso se e solo se tutti i modelli concedono l’accesso. Per ulteriori dettagli, consulta la [documentazione di Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Le seguenti caratteristiche si applicano alla valutazione delle autorizzazioni associata al modello di autorizzazione progettato per gestire e valutare i criteri CUG:

* Gestisce solo le autorizzazioni di lettura per i nodi e le proprietà normali, ma non il contenuto del controllo di accesso in lettura
* Non gestisce le autorizzazioni di scrittura né i tipi di autorizzazioni necessari per la modifica del contenuto JCR protetto (tra cui, controllo degli accessi, informazioni sul tipo di nodo, controllo delle versioni, blocco o gestione degli utenti). Queste autorizzazioni non sono influenzate da un criterio per gruppi utenti chiusi (CUG) e non verranno valutate dal modello di autorizzazione associato. La concessione di queste autorizzazioni dipende dagli altri modelli configurati nella configurazione della sicurezza.

L’effetto di un singolo criterio CUG sulla valutazione delle autorizzazioni può essere riassunto come segue:

* L’accesso in lettura è negato a tutti, ad eccezione dei soggetti che contengono i principali o i principali esclusi elencati nella policy;
* La politica ha effetto sul nodo controllato in cui si trova la politica e le relative proprietà;
* L’effetto viene ereditato anche nella gerarchia, ovvero nella struttura degli elementi definita dal nodo controllato dagli accessi;
* Tuttavia, non influisce né sui fratelli e le sorelle né sugli antenati del nodo controllato dagli accessi;
* L’ereditarietà di un determinato CUG si interrompe in corrispondenza di un CUG nidificato.

#### Best practice {#best-practices}

Le seguenti best practice devono tenere conto della definizione di accesso in lettura limitato tramite CUG:

* Decidere in modo consapevole se la necessità di un CUG riguarda la limitazione dell&#39;accesso in lettura o un requisito di autenticazione. Se è quest’ultimo, o se sono necessari entrambi, consulta la sezione sulle best practice per i dettagli relativi al requisito di autenticazione
* Crea un modello di minaccia per i dati o i contenuti che devono essere protetti per identificare i limiti della minaccia e ottenere un quadro chiaro della sensibilità dei dati e dei ruoli associati all’accesso autorizzato
* Modellare il contenuto dell’archivio e i gruppi di utenti chiusi (CUG) tenendo presenti gli aspetti generali relativi alle autorizzazioni e le best practice:

   * Ricorda che l’autorizzazione di lettura viene concessa solo se un determinato CUG e la valutazione di altri moduli distribuiti nella concessione dell’impostazione consentono a un determinato soggetto di leggere un determinato elemento dell’archivio
   * Evita la creazione di CUG ridondanti in cui l’accesso in lettura è già limitato da altri moduli di autorizzazione
   * L’eccessiva necessità di CUG nidificati potrebbe potenzialmente evidenziare problemi nella progettazione del contenuto
   * Un’eccessiva necessità di gruppi di utenti chiusi (ad esempio, su ogni pagina) può indicare la necessità di un modello di autorizzazione personalizzato potenzialmente più adatto alle esigenze di sicurezza specifiche dell’applicazione e del contenuto a portata di mano.

* Limita i percorsi supportati per i criteri CUG ad alcune strutture nell’archivio per ottimizzare le prestazioni. Ad esempio, consenti solo i CUG sotto il nodo /content come valore predefinito a partire da AEM 6.3.
* I criteri CUG sono progettati per consentire l&#39;accesso in lettura a un piccolo insieme di entità principali. La necessità di un numero elevato di utenti/gruppi/ruoli può evidenziare problemi nel contenuto o nella progettazione dell’applicazione e dovrebbe essere riconsiderata.

### Autenticazione: definizione del requisito di autenticazione {#authentication-defining-the-auth-requirement}

Le parti relative all’autenticazione della funzione del gruppo utenti chiusi (CUG) consentono di contrassegnare gli alberi che richiedono l’autenticazione e, facoltativamente, di specificare una pagina di accesso dedicata. In conformità alla versione precedente, la nuova implementazione consente di contrassegnare gli alberi che richiedono l’autenticazione nell’archivio dei contenuti. Consente inoltre la sincronizzazione in modo condizionale con `Sling org.apache.sling.api.auth.Authenticator` responsabile dell&#39;applicazione definitiva del requisito e del reindirizzamento a una risorsa di accesso.

Questi requisiti vengono registrati con Authenticator da un servizio OSGi che fornisce la proprietà di registrazione `sling.auth.requirements`. Queste proprietà vengono quindi utilizzate per estendere dinamicamente i requisiti di autenticazione. Per ulteriori dettagli, consulta la [documentazione di Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definizione del requisito di autenticazione con un tipo mixin dedicato {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Per motivi di sicurezza, la nuova implementazione sostituisce l&#39;utilizzo di una proprietà JCR residua con un tipo mixin dedicato denominato `granite:AuthenticationRequired`, che definisce una singola proprietà opzionale di tipo STRING per il percorso di accesso `granite:loginPath`. Solo le modifiche al contenuto relative a questo tipo di mixin determinano un aggiornamento dei requisiti registrati con Apache Sling Authenticator. Le modifiche vengono tracciate in caso di modifiche temporanee persistenti e richiedono quindi una chiamata `javax.jcr.Session.save()` per diventare effettiva.

Lo stesso vale per la proprietà `granite:loginPath`. Viene rispettato solo se è definito dal tipo mixin relativo al requisito di autenticazione. L’aggiunta di una proprietà residua con questo stesso nome in un nodo JCR non strutturato non mostra l’effetto desiderato e la proprietà viene ignorata dal gestore responsabile dell’aggiornamento della registrazione OSGi.

>[!NOTE]
>
>L&#39;impostazione della proprietà del percorso di accesso è facoltativa e necessaria solo se la struttura che richiede l&#39;autenticazione non può tornare alla pagina di accesso predefinita o altrimenti ereditata. Consulta la [Valutazione del percorso di accesso](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) di seguito.

#### Registrazione del requisito di autenticazione e del percorso di accesso con l’autenticatore Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Poiché si prevede che questo tipo di requisito di autenticazione sia limitato a determinate modalità di esecuzione e a un piccolo sottoinsieme di strutture all’interno dell’archivio dei contenuti, il tracciamento del tipo mixin dei requisiti e delle proprietà del percorso di accesso è condizionale. ed è associata a una configurazione corrispondente che definisce i percorsi supportati (vedi Opzioni di configurazione di seguito). Pertanto, solo le modifiche all’interno dell’ambito di questi percorsi supportati attivano un aggiornamento della registrazione OSGi, altrove vengono ignorati sia il tipo mixin che la proprietà.

La configurazione predefinita di AEM ora utilizza questa configurazione consentendo di impostare il mixin in modalità di esecuzione per l’authoring, ma solo per la replica nell’istanza di pubblicazione. Per informazioni dettagliate su come Sling applica il requisito di autenticazione, consulta la documentazione [Sling Authentication - Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html).

L&#39;aggiunta del tipo mixin `granite:AuthenticationRequired` nei percorsi configurati supportati causa l&#39;aggiornamento della registrazione OSGi del gestore responsabile contenente una nuova voce aggiuntiva con la proprietà `sling.auth.requirements`. Se un determinato requisito di autenticazione specifica la proprietà `granite:loginPath` facoltativa, il valore viene registrato anche con l&#39;autenticatore con il prefisso &#39;-&#39; da escludere dal requisito di autenticazione.

#### Valutazione ed ereditarietà del requisito di autenticazione {#evaluation-and-inheritance-of-the-authentication-requirement}

I requisiti di autenticazione di Apache Sling vengono ereditati tramite la gerarchia di pagine o nodi. I dettagli dell’ereditarietà e la valutazione dei requisiti di autenticazione, come ordine e precedenza, sono considerati un dettaglio di implementazione e non saranno documentati in questo articolo.

#### Valutazione del percorso di accesso {#evaluation-of-login-path}

La valutazione del percorso di accesso e del reindirizzamento alla risorsa corrispondente al momento dell&#39;autenticazione è un dettaglio di implementazione del gestore di autenticazione del selettore di accesso di Adobe Granite ( `com.day.cq.auth.impl.LoginSelectorHandler`), che è un Apache Sling AuthenticationHandler configurato con AEM per impostazione predefinita.

Quando si chiama `AuthenticationHandler.requestCredentials`, il gestore tenta di determinare la pagina di accesso di mapping a cui l&#39;utente viene reindirizzato. Ciò include i seguenti passaggi:

* distinguere tra password scaduta e necessità di accesso regolare come motivo del reindirizzamento;
* Se l’accesso è regolare, verifica se è possibile ottenere un percorso di accesso nell’ordine seguente:

   * dal LoginPathProvider implementato dal nuovo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * dalla precedente implementazione obsoleta di CUG,
   * dalle mappature pagina di accesso, come definite con `LoginSelectorHandler`,
   * e infine, tornare alla pagina di accesso predefinita, come definita con `LoginSelectorHandler`.

* Quando si ottiene un percorso di accesso valido tramite le chiamate elencate sopra, la richiesta dell’utente viene reindirizzata a tale pagina.

La destinazione di questa documentazione è la valutazione del percorso di accesso esposto dall&#39;interfaccia interna di `LoginPathProvider`. L’implementazione fornita da AEM 6.3 si comporta come segue:

* La registrazione dei percorsi di accesso dipende dalla distinzione tra password scaduta e necessità di accesso regolare come motivo del reindirizzamento
* Se l’accesso è regolare, verifica se è possibile ottenere un percorso di accesso nell’ordine seguente:

   * da `LoginPathProvider` come implementato dal nuovo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * dalla precedente implementazione obsoleta di CUG,
   * dalle mappature pagina di accesso definite con `LoginSelectorHandler`,
   * e infine tornare alla pagina di accesso predefinita come definita con `LoginSelectorHandler`.

* Quando si ottiene un percorso di accesso valido tramite le chiamate elencate sopra, la richiesta dell’utente viene reindirizzata a tale pagina.

L&#39;implementazione di `LoginPathProvider` da parte del nuovo supporto dei requisiti di autenticazione in Granite espone i percorsi di accesso come definiti dalle proprietà di `granite:loginPath`, che a loro volta sono definiti dal tipo mixin come descritto in precedenza. La mappatura del percorso della risorsa contenente il percorso di accesso e il valore della proprietà stessa vengono conservati in memoria e valutati per trovare un percorso di accesso appropriato per altri nodi nella gerarchia.

>[!NOTE]
>
>La valutazione viene eseguita solo per le richieste associate alle risorse che si trovano in nei percorsi supportati configurati. Per qualsiasi altra richiesta verranno valutati i modi alternativi per determinare il percorso di accesso.

#### Best practice {#best-practices-1}

Nel definire i requisiti di autenticazione è necessario tenere conto delle seguenti best practice:

* Evita di nidificare i requisiti di autenticazione: il posizionamento di un singolo marcatore di requisito di autenticazione all’inizio di una struttura deve essere sufficiente ed essere ereditato dall’intera sottostruttura definita dal nodo di destinazione. Requisiti di autenticazione aggiuntivi all’interno di tale struttura devono essere considerati ridondanti e possono causare problemi di prestazioni durante la valutazione dei requisiti di autenticazione in Apache Sling. Con la separazione delle aree CUG relative all&#39;autorizzazione e all&#39;autenticazione, è possibile limitare l&#39;accesso in lettura per CUG o altri tipi di criteri applicando l&#39;autenticazione per l&#39;intera struttura.
* Contenuto dell’archivio del modello tale che i requisiti di autenticazione si applichino all’intera struttura senza dover escludere nuovamente le sottostrutture nidificate dai requisiti.
* Per evitare di specificare e quindi registrare percorsi di accesso ridondanti:

   * affidarsi all’ereditarietà ed evitare di definire percorsi di accesso nidificati,
   * non impostare il percorso di accesso facoltativo su un valore corrispondente al valore predefinito o ereditato,
   * gli sviluppatori di applicazioni devono identificare i percorsi di accesso da configurare nelle configurazioni dei percorsi di accesso globali (sia predefiniti che mappati) associate a `LoginSelectorHandler`.

## Rappresentazione nel repository {#representation-in-the-repository}

### Rappresentazione dei criteri CUG nell’archivio {#cug-policy-representation-in-the-repository}

La documentazione di Oak illustra il modo in cui i nuovi criteri CUG si riflettono nel contenuto dell’archivio. Per ulteriori informazioni, consultare la [documentazione di Jackrabbit Oak sulla gestione dell&#39;accesso con i gruppi utenti chiusi](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Autenticazione richiesta nel repository {#authentication-requirement-in-the-repository}

La necessità di un requisito di autenticazione separato si riflette nel contenuto dell’archivio con un tipo di nodo mixin dedicato posizionato sul nodo di destinazione. Il tipo mixin definisce una proprietà opzionale per specificare una pagina di accesso dedicata per la struttura ad albero definita dal nodo di destinazione.

La pagina associata al percorso di accesso può trovarsi all’interno o all’esterno di tale struttura. È escluso dal requisito di autenticazione.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gestione dei criteri CUG e dei requisiti di autenticazione {#managing-cug-policies-and-authentication-requirement}

### Gestione dei criteri CUG {#managing-cug-policies}

Il nuovo tipo di criteri di controllo di accesso per limitare l&#39;accesso in lettura per un CUG viene gestito utilizzando l&#39;API di gestione del controllo di accesso JCR e segue i meccanismi descritti con la specifica [JCR 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Imposta un nuovo criterio per gruppi utenti chiusi {#set-a-new-cug-policy}

Codice per applicare un nuovo criterio CUG in un nodo in cui non è stato precedentemente impostato un CUG. `getApplicablePolicies` restituisce solo i nuovi criteri che non sono stati impostati in precedenza. Alla fine, il criterio deve essere riscritto e le modifiche devono essere mantenute.

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
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Modifica un criterio del gruppo utenti chiusi esistente {#edit-an-existing-cug-policy}

Per modificare un criterio CUG esistente sono necessari i seguenti passaggi. Il criterio modificato deve essere riscritto e le modifiche devono essere rese permanenti utilizzando `javax.jcr.Session.save()`.

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

La gestione del controllo degli accessi JCR definisce un metodo ottimale per recuperare i criteri che hanno effetto su un determinato percorso. Poiché la valutazione dei criteri del gruppo utenti chiusi è condizionale e dipende dalla configurazione corrispondente da abilitare, la chiamata a `getEffectivePolicies` è un modo pratico per verificare se un determinato criterio del gruppo utenti chiusi sta avendo effetto in una determinata installazione.

>[!NOTE]
>
>Differenza tra `getEffectivePolicies` e l&#39;esempio di codice successivo che procede nella gerarchia per verificare se un determinato percorso fa già parte di un CUG esistente.

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

Individuazione di tutti i CUG nidificati definiti in un determinato percorso, indipendentemente dal fatto che abbiano o meno effetto. Per ulteriori informazioni, vedere la sezione [Opzioni di configurazione](/help/sites-administering/closed-user-groups.md#configuration-options).

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

#### Gestione dei criteri CUG per entità {#managing-cug-policies-by-pincipal}

Le estensioni definite da `JackrabbitAccessControlManager` che consentono di modificare i criteri di controllo di accesso per entità non sono implementate con la gestione del controllo di accesso dei gruppi utenti chiusi (CUG), in quanto per definizione un criterio dei gruppi utenti chiusi (CUG) influisce sempre su tutte le entità: a quelle elencate con `PrincipalSetPolicy` viene concesso l&#39;accesso in lettura, mentre a tutte le altre entità verrà impedito di leggere il contenuto nella struttura definita dal nodo di destinazione.

I metodi corrispondenti restituiscono sempre un array di criteri vuoto, ma non generano eccezioni.

### Gestione dei requisiti di autenticazione {#managing-the-authentication-requirement}

La creazione, la modifica o la rimozione di un nuovo requisito di autenticazione si ottiene modificando il tipo di nodo effettivo del nodo di destinazione. La proprietà del percorso di accesso opzionale può quindi essere scritta utilizzando l’API JCR regolare.

>[!NOTE]
>
>Le modifiche apportate a uno specifico nodo di destinazione menzionato in precedenza verranno applicate ad Apache Sling Authenticator solo se `RequirementHandler` è stato configurato e la destinazione è contenuta nelle strutture definite dai percorsi supportati (vedere la sezione Opzioni di configurazione).
>
>Per ulteriori informazioni, vedere [Assegnazione di tipi di nodo mixin]&#x200B;(https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Assegnazione di tipi di nodo mixin) e [Aggiunta di nodi e impostazione di proprietà]&#x200B;(https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Aggiunta di nodi e impostazione di proprietà)

#### Aggiunta di un nuovo requisito di autenticazione {#adding-a-new-auth-requirement}

Di seguito sono riportati i passaggi per creare un requisito di autenticazione. Il requisito viene registrato con Apache Sling Authenticator solo se `RequirementHandler` è stato configurato per la struttura contenente il nodo di destinazione.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Aggiungi un nuovo requisito di autenticazione con percorso di accesso {#add-a-new-auth-requirement-with-login-path}

Passaggi per creare un requisito di autenticazione che include un percorso di accesso. Il requisito e l’esclusione per il percorso di accesso vengono registrati con Apache Sling Authenticator solo se `RequirementHandler` è stato configurato per la struttura contenente il nodo di destinazione.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificare un percorso di accesso esistente {#modify-an-existing-login-path}

Di seguito sono riportati i passaggi per modificare un percorso di accesso esistente. La modifica viene registrata con Apache Sling Authenticator solo se `RequirementHandler` è stato configurato per la struttura contenente il nodo di destinazione. Il valore del percorso di accesso precedente viene rimosso dalla registrazione. Questa modifica non influisce sul requisito di autenticazione associato al nodo di destinazione.

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

#### Rimuovi un percorso di accesso esistente {#remove-an-existing-login-path}

Passaggi per rimuovere un percorso di accesso esistente. La registrazione della voce del percorso di accesso verrà annullata dall&#39;autenticatore Apache Sling solo se `RequirementHandler` è stato configurato per la struttura contenente il nodo di destinazione. Il requisito di autenticazione associato al nodo di destinazione non è interessato.

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

In alternativa, puoi utilizzare il metodo seguente per ottenere lo stesso scopo:

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

Passaggi per rimuovere un requisito di autenticazione esistente. La registrazione del requisito verrà annullata da Apache Sling Authenticator solo se `RequirementHandler` è stato configurato per la struttura contenente il nodo di destinazione.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recupera requisiti di autenticazione effettivi {#retrieve-effective-auth-requirements}

Non esiste un’API pubblica dedicata per leggere tutti i requisiti di autenticazione effettivi registrati con Apache Sling Authenticator. Tuttavia, l&#39;elenco è esposto nella console di sistema in `https://<serveraddress>:<serverport>/system/console/slingauth` nella sezione &quot;**Configurazione dei requisiti di autenticazione**&quot;.

L’immagine seguente mostra i requisiti di autenticazione di un’istanza AEM Publish con contenuto demo. Il percorso evidenziato della pagina community illustra come un requisito aggiunto dall’implementazione descritta in questo documento viene riflesso in Apache Sling Authenticator.

>[!NOTE]
>
>In questo esempio la proprietà del percorso di accesso facoltativo non è stata impostata. Pertanto, non è stata registrata alcuna seconda voce con l’autenticatore.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Recuperare il percorso di accesso effettivo {#retrieve-the-effective-login-path}

Attualmente non esiste un’API pubblica per recuperare il percorso di accesso che viene applicato quando si accede in modo anonimo a una risorsa che richiede l’autenticazione. Consulta la sezione Valutazione del percorso di accesso per informazioni dettagliate sull’implementazione per il recupero del percorso di accesso.

Tuttavia, oltre ai percorsi di accesso definiti con questa funzione, esistono altri modi per specificare il reindirizzamento all’accesso, che deve essere tenuto in considerazione durante la progettazione del modello di contenuto e dei requisiti di autenticazione di una determinata installazione di AEM.

#### Recupera il requisito di autenticazione ereditato {#retrieve-the-inherited-auth-requirement}

Come per il percorso di accesso, non esiste un’API pubblica per recuperare i requisiti di autenticazione ereditati definiti nel contenuto. Nell&#39;esempio seguente viene illustrato come elencare tutti i requisiti di autenticazione definiti con una determinata gerarchia, indipendentemente dal fatto che abbiano effetto o meno. Per ulteriori informazioni, vedere [Opzioni di configurazione](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>Si consiglia di fare affidamento sul meccanismo di ereditarietà sia per i requisiti di autenticazione che per il percorso di accesso ed evitare la creazione di requisiti di autenticazione nidificati.
>
>Per ulteriori informazioni, vedere [Valutazione ed ereditarietà del requisito di autenticazione](#evaluation-and-inheritance-of-the-authentication-requirement), [Valutazione del percorso di accesso](#evaluation-of-login-path) e [Best practice](#best-practices).

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

### Combinazione di criteri CUG e requisiti di autenticazione {#combining-cug-policies-and-the-authentication-requirement}

Nella tabella seguente sono elencate le combinazioni valide di criteri CUG e i requisiti di autenticazione in un’istanza di AEM in cui entrambi i moduli sono abilitati tramite la configurazione.

| **Autenticazione richiesta** | **Percorso di accesso** | **Accesso in lettura limitato** | **Effetto previsto** |
|---|---|---|---|
| Sì | Sì | Sì | Un determinato utente potrà visualizzare il sottoalbero contrassegnato con il criterio CUG solo se la valutazione delle autorizzazioni effettiva concede l’accesso. Un utente non autenticato viene reindirizzato alla pagina di accesso specificata. |
| Sì | No | Sì | Un determinato utente potrà visualizzare il sottoalbero contrassegnato con il criterio CUG solo se la valutazione delle autorizzazioni effettiva concede l’accesso. Un utente non autenticato viene reindirizzato a una pagina di accesso predefinita ereditata. |
| Sì | Sì | No | Un utente non autenticato viene reindirizzato alla pagina di accesso specificata. La possibilità di visualizzare la struttura contrassegnata con il requisito di autorizzazione dipende dalle autorizzazioni effettive dei singoli elementi contenuti nella sottostruttura. Nessun CUG dedicato che limita l’accesso in lettura attivo. |
| Sì | No | No | Un utente non autenticato viene reindirizzato a una pagina di accesso predefinita ereditata. La possibilità di visualizzare la struttura contrassegnata con il requisito di autenticazione dipende dalle autorizzazioni effettive dei singoli elementi contenuti nella sottostruttura. Nessun CUG dedicato che limita l’accesso in lettura attivo. |
| No | No | Sì | Un determinato utente autenticato o non autenticato può visualizzare la sottostruttura contrassegnata con il criterio CUG solo se la valutazione delle autorizzazioni effettiva concede l’accesso. Un utente non autenticato viene trattato allo stesso modo e non viene reindirizzato per l’accesso. |

>[!NOTE]
>
>La combinazione di &quot;Autenticazione richiesta&quot; = No e &quot;Percorso di accesso&quot; = Sì non è elencata in precedenza in quanto &quot;Percorso di accesso&quot; è un attributo facoltativo associato a un requisito di autenticazione. La specifica di una proprietà JCR con tale nome senza l’aggiunta del tipo mixin di definizione non ha alcun effetto e viene ignorata dal gestore corrispondente.

## Componenti e configurazione OSGi {#osgi-components-and-configuration}

Questa sezione fornisce una panoramica dei componenti OSGi e delle singole opzioni di configurazione introdotte con la nuova implementazione CUG.

Consulta anche la documentazione sul mapping dei gruppi utenti chiusi (CUG) per una mappatura completa delle opzioni di configurazione tra la vecchia e la nuova implementazione.

### Autorizzazione: Configurazione e configurazione {#authorization-setup-and-configuration}

Le nuove parti correlate all&#39;autorizzazione sono contenute nel bundle **Autorizzazione CUG di Oak** ( `org.apache.jackrabbit.oak-authorization-cug`), che fa parte dell&#39;installazione predefinita di AEM. Il bundle definisce un modello di autorizzazione separato da distribuire come metodo aggiuntivo per gestire l’accesso in lettura.

#### Impostazione autorizzazione CUG {#setting-up-cug-authorization}

L&#39;impostazione dell&#39;autorizzazione CUG è descritta in dettaglio nella [documentazione Apache pertinente](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Per impostazione predefinita, in AEM l’autorizzazione per il gruppo utenti chiusi (CUG) è implementata in tutte le modalità di esecuzione. Le istruzioni dettagliate possono essere utilizzate anche per disabilitare l&#39;autorizzazione CUG negli impianti che richiedono una configurazione di autorizzazione diversa.

#### Configurazione del filtro Referrer {#configuring-the-referrer-filter}

Devi anche configurare il [filtro Sling Referrer](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) con tutti i nomi host che possono essere utilizzati per accedere ad AEM, ad esempio tramite CDN, Load Balancer ed altri.

Se il filtro del referente non è configurato, quando un utente tenta di accedere a un sito CUG vengono visualizzati errori simili ai seguenti:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Caratteristiche dei componenti OSGi {#characteristics-of-osgi-components}

Per definire i requisiti di autenticazione e specificare i percorsi di accesso dedicati, sono stati introdotti i due componenti OSGi seguenti:

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
   <td>Configurazione di autorizzazione dedicata alla configurazione e alla valutazione delle autorizzazioni CUG.</td>
  </tr>
  <tr>
   <td>Proprietà di configurazione</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Vedi anche <a href="#configuration-options">Opzioni di configurazione</a> di seguito.</p> </td>
  </tr>
  <tr>
   <td>Criteri di configurazione</td>
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
   <td>Elenco di esclusione CUG di Apache Jackrabbit Oak</td>
  </tr>
  <tr>
   <td>Descrizione</td>
   <td>Consente di escludere le entità con i nomi configurati dalla valutazione CUG.</td>
  </tr>
  <tr>
   <td>Proprietà di configurazione</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Vedi anche la sezione Opzioni di configurazione di seguito.</p> </td>
  </tr>
  <tr>
   <td>Criteri di configurazione</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Riferimenti</td>
   <td>ND</td>
  </tr>
 </tbody>
</table>

#### Opzioni di configurazione {#configuration-options}

Le opzioni di configurazione principali sono:

* `cugSupportedPaths`: specificare le sottostrutture che possono contenere gruppi utenti chiusi. Nessun valore predefinito impostato
* `cugEnabled`: opzione di configurazione per abilitare la valutazione delle autorizzazioni per i criteri CUG correnti.

Le opzioni di configurazione disponibili associate al modulo di autorizzazione CUG sono elencate e descritte più dettagliatamente nella [Documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Esclusione di entità dalla valutazione CUG {#excluding-principals-from-cug-evaluation}

L&#39;esenzione dei singoli mandanti dalla valutazione dei gruppi di utenti chiusi è stata adottata a partire dalla precedente attuazione. La nuova autorizzazione CUG copre questo problema con un’interfaccia dedicata denominata CugExclude. Apache Jackrabbit Oak 1.4 viene fornito con un’implementazione predefinita che esclude un set fisso di entità principali e un’implementazione estesa che consente di configurare i nomi delle singole entità. Quest’ultimo è configurato nelle istanze di pubblicazione di AEM.

Il valore predefinito, poiché AEM 6.3, impedisce che le seguenti entità principali siano interessate dai criteri CUG:

* entità amministrative principali (utente amministratore, gruppo amministratori)
* entità utente del servizio
* entità del sistema interno del repository

Per ulteriori informazioni, vedere la tabella nella sezione seguente [Configurazione predefinita a partire da AEM 6.3](#default-configuration-since-aem).

L&#39;esclusione del gruppo &#39;amministratori&#39; può essere modificata o espansa nella console di sistema nella sezione di configurazione di **Apache Jackrabbit Oak CUG Exclude List**.

In alternativa, è possibile fornire e distribuire un’implementazione personalizzata dell’interfaccia CugExclude per regolare il set di entità escluse in caso di esigenze speciali. Per informazioni dettagliate e un esempio di implementazione, consulta la documentazione sulla [collegabilità CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability).

### Autenticazione: configurazione {#authentication-setup-and-configuration}

Le nuove parti relative all&#39;autenticazione sono contenute nel bundle **Adobe Granite Authentication Handler** ( `com.adobe.granite.auth.authhandler` versione 5.6.48). Questo bundle fa parte dell’installazione predefinita di AEM.

Per impostare la sostituzione dei requisiti di autenticazione per il supporto CUG obsoleto, alcuni componenti OSGi devono essere presenti e attivi in una determinata installazione di AEM. Per ulteriori dettagli, consulta **Caratteristiche dei componenti OSGi** di seguito.

>[!NOTE]
>
>A causa dell’opzione di configurazione obbligatoria con RequirementHandler, le parti relative all’autenticazione saranno attive solo se la funzione è stata abilitata specificando un set di percorsi supportati. Con un’installazione standard di AEM, la funzione è disabilitata in modalità di esecuzione dell’autore e abilitata per /content in modalità di esecuzione della pubblicazione.

**Caratteristiche dei componenti OSGi**

Per definire i requisiti di autenticazione e specificare i percorsi di accesso dedicati, sono stati introdotti i due componenti OSGi seguenti:

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
   <td>Servizio OSGi dedicato per i requisiti di autenticazione che registra un osservatore per le modifiche al contenuto che influiscono sui requisiti di autenticazione (tramite il tipo mixin <code>granite:AuthenticationRequirement</code>) e i percorsi di accesso con sono esposti a <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Proprietà di configurazione</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Criteri di configurazione</td>
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

| Etichetta | Requisiti di autenticazione di Adobe Granite e gestore del percorso di accesso |
|---|---|
| Descrizione | Implementazione di `RequirementHandler` che aggiorna i requisiti di autenticazione di Apache Sling e la corrispondente esclusione per i percorsi di accesso associati. |
| Proprietà di configurazione | `supportedPaths` |
| Criteri di configurazione | `ConfigurationPolicy.REQUIRE` |
| Riferimenti | ND |

#### Opzioni di configurazione {#configuration-options-1}

Le parti relative all’autenticazione della riscrittura CUG sono disponibili con un’unica opzione di configurazione associata ai requisiti di autenticazione di Adobe Granite e al gestore del percorso di accesso:

**&quot;Requisiti di autenticazione e gestore del percorso di accesso&quot;**

<table>
 <tbody>
  <tr>
   <td>Proprietà</td>
   <td>Tipo</td>
   <td>Valore predefinito</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><p>Etichetta = percorsi supportati</p> <p>Nome = 'supportedPaths'</p> </td>
   <td>Set&lt;Stringa&gt;</td>
   <td>-</td>
   <td>Percorsi in cui i requisiti di autenticazione verranno rispettati da questo gestore. Lasciare questa configurazione non impostata se si desidera aggiungere il tipo mixin <code>granite:AuthenticationRequirement</code> ai nodi senza farli applicare (ad esempio, nelle istanze di authoring). Se manca, la funzione viene disabilitata. </td>
  </tr>
 </tbody>
</table>

## Configurazione predefinita da AEM 6.3 {#default-configuration-since-aem}

Per impostazione predefinita, le nuove installazioni di AEM utilizzeranno le nuove implementazioni sia per le parti relative all’autorizzazione che per quelle relative all’autenticazione della funzione CUG. La vecchia implementazione &quot;Supporto di Adobe Granite Closed User Group (CUG)&quot; è stata dichiarata obsoleta e verrà disabilitata per impostazione predefinita in tutte le installazioni di AEM. Le nuove implementazioni verranno invece abilitate come segue:

### Istanze autore {#author-instances}

| **&quot;Configurazione CUG di Apache Jackrabbit Oak&quot;** | **Spiegazione** |
|---|---|
| Percorsi supportati `/content` | La gestione del controllo di accesso per i criteri CUG è abilitata. |
| Valutazione CUG abilitata FALSE | La valutazione delle autorizzazioni è disabilitata. I criteri CUG non hanno effetto. |
| Classificazione \|200 | Consulta la documentazione di Oak. |

>[!NOTE]
>
>Nessuna configurazione per **Apache Jackrabbit Oak CUG Exclude List** e **Adobe Granite Authentication Requirement and Login Path Handler** è presente nelle istanze di authoring predefinite.

### Istanze di pubblicazione {#publish-instances}

| **&quot;Configurazione CUG di Apache Jackrabbit Oak&quot;** | **Spiegazione** |
|---|---|
| Percorsi supportati `/content` | La gestione del controllo degli accessi per i criteri del gruppo utenti chiusi (CUG) è abilitata sotto i percorsi configurati. |
| Valutazione CUG abilitata TRUE | La valutazione delle autorizzazioni è abilitata sotto i percorsi configurati. I criteri CUG diventano effettivi al `Session.save()`. |
| Classificazione \|200 | Consulta la documentazione di Oak. |

| **&quot;Elenco di esclusione CUG di Apache Jackrabbit Oak&quot;** | **Spiegazione** |
|---|---|
| Amministratori nomi principali | Esclude l&#39;entità di amministrazione dalla valutazione del gruppo utenti chiusi. |

| **&quot;Requisiti di autenticazione di Adobe Granite e gestore del percorso di accesso&quot;** | **Spiegazione** |
|---|---|
| Percorsi supportati `/content` | I requisiti di autenticazione definiti nel repository dal tipo mixin `granite:AuthenticationRequired` hanno effetto al di sotto di `/content` il `Session.save()`. Sling Authenticator viene aggiornato. L’aggiunta del tipo mixin all’esterno dei percorsi supportati viene ignorata. |

## Disabilitazione dei requisiti di autenticazione e autorizzazione per gruppi utenti chiusi (CUG) {#disabling-cug-authorization-and-authentication-requirement}

La nuova implementazione può essere disabilitata completamente nel caso in cui una determinata installazione non utilizzi CUG o utilizzi mezzi diversi per l’autenticazione e l’autorizzazione.

### Disattiva autorizzazione CUG {#disable-cug-authorization}

Per informazioni dettagliate su come rimuovere il modello di autorizzazione CUG dalla configurazione di autorizzazione composita, consultare la documentazione relativa alla [collegabilità CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability).

### Disattiva il requisito di autenticazione {#disable-the-authentication-requirement}

Per disabilitare il supporto per il requisito di autenticazione fornito dal modulo `granite.auth.authhandler`, è sufficiente rimuovere la configurazione associata a **Adobe Granite Authentication Requirement e Login Path Handler**.

>[!NOTE]
>
>Tuttavia, la rimozione della configurazione non annulla la registrazione del tipo mixin, che era ancora applicabile ai nodi senza avere effetto.

## Interazione con altri moduli {#interaction-with-other-modules}

### API Apache Jackrabbit {#apache-jackrabbit-api}

Per riflettere il nuovo tipo di criteri di controllo di accesso utilizzati dal modello di autorizzazione CUG, è stata estesa l’API definita da Apache Jackrabbit. A partire dalla versione 2.11.0 del modulo `jackrabbit-api`, viene definita una nuova interfaccia denominata `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, che si estende da `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Il meccanismo di importazione di Apache Jackrabbit FileVault è stato modificato per gestire i criteri di controllo di accesso di tipo `PrincipalSetPolicy`.

### Distribuzione dei contenuti Apache Sling {#apache-sling-content-distribution}

Consulta la sezione [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) precedente.

### Replica Adobe Granite {#adobe-granite-replication}

Il modulo di replica è stato leggermente modificato per consentire la replica dei criteri CUG tra diverse istanze di AEM:

* `DurboImportConfiguration.isImportAcl()` è interpretato letteralmente e influirà solo sui criteri di controllo di accesso che implementano `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` rispetterà questa configurazione solo per ACL veri
* Altri criteri come `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` istanze create dal modello di autorizzazione CUG verranno sempre replicati e l&#39;opzione di configurazione `DurboImportConfiguration.isImportAcl`() verrà ignorata.

Esiste un limite alla replica dei criteri CUG. Se un determinato criterio del gruppo utenti chiusi viene rimosso senza rimuovere il tipo di nodo mixin corrispondente `rep:CugMixin,`, la rimozione non verrà riflessa durante la replica. Questo problema è stato risolto rimuovendo sempre il mixin dopo la rimozione dei criteri. La limitazione può tuttavia essere visualizzata se il tipo di mixin viene aggiunto manualmente.

### Gestore autenticazione Adobe Granite {#adobe-granite-authentication-handler}

Il gestore di autenticazione **Adobe Granite HTTP Header Authentication Handler** fornito con il bundle `com.adobe.granite.auth.authhandler` contiene un riferimento all&#39;interfaccia `CugSupport` definita dallo stesso modulo. Viene utilizzato per calcolare il &#39;realm&#39; in determinate circostanze, ricadendo nel realm configurato con il gestore.

È stato modificato per rendere facoltativo il riferimento a `CugSupport` in modo da garantire la massima compatibilità con le versioni precedenti se una determinata configurazione decide di riabilitare l&#39;implementazione obsoleta. Le installazioni che utilizzano l&#39;implementazione non otterranno più il realm estratto dall&#39;implementazione CUG, ma visualizzeranno sempre il realm come definito con **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>Per impostazione predefinita, il **gestore di autenticazione dell&#39;intestazione HTTP Adobe Granite** è configurato solo in modalità di esecuzione di pubblicazione con l&#39;opzione &quot;Disabilita pagina di accesso&quot; ( `auth.http.nologin`) abilitata.

### AEM LiveCopy {#aem-livecopy}

La configurazione dei gruppi utenti chiusi (CUG) con Live Copy è rappresentata nell’archivio dall’aggiunta di un nodo e una proprietà aggiuntivi, come segue:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Entrambi gli elementi vengono creati in `cq:Page`. Con la progettazione corrente, MSM gestisce solo nodi e proprietà che si trovano sotto il nodo `cq:PageContent` (`jcr:content`).

Pertanto, non è possibile eseguire il rollout dei gruppi CUG in Live Copy da Blueprint. Pianifica tutto questo durante la configurazione della Live Copy.

## Modifiche con la nuova implementazione CUG {#changes-with-the-new-cug-implementation}

Lo scopo di questa sezione è quello di fornire una panoramica delle modifiche apportate alla funzione CUG e un confronto tra la vecchia e la nuova implementazione. Elenca le modifiche che influiscono sulla configurazione del supporto per i gruppi utenti chiusi (CUG) e descrive come e da chi vengono gestiti nel contenuto dell’archivio.

### Differenze nella configurazione e nella configurazione del gruppo utenti chiusi (CUG) {#differences-in-cug-setup-and-configuration}

Il componente OSGi obsoleto **Supporto per gruppo utenti chiuso (CUG) Adobe Granite** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) è stato sostituito da nuovi componenti per poter gestire separatamente le parti relative all&#39;autenticazione e all&#39;autorizzazione delle precedenti funzionalità CUG.

## Differenze nella gestione dei gruppi utenti chiusi (CUG) nel contenuto dell’archivio {#differences-in-managing-cugs-in-the-repository-content}

Le sezioni seguenti descrivono le differenze tra le vecchie e le nuove implementazioni dal punto di vista dell’implementazione e della sicurezza. Anche se la nuova implementazione mira a fornire la stessa funzionalità, ci sono sottili modifiche che sono importanti da sapere quando si utilizza il nuovo CUG.

### Differenze Per Quanto Riguarda L&#39;Autorizzazione {#differences-with-regards-to-authorization}

Le principali differenze dal punto di vista dell’autorizzazione sono riassunte nell’elenco seguente:

**Contenuto del controllo di accesso dedicato per i gruppi utenti chiusi**

Nella precedente implementazione veniva utilizzato il modello di autorizzazione predefinito per manipolare i criteri degli elenchi di controllo di accesso al momento della pubblicazione, sostituendo eventuali ACE esistenti con la configurazione richiesta dal CUG. Questo veniva attivato scrivendo proprietà JCR regolari e residue che venivano interpretate al momento della pubblicazione.

Con la nuova implementazione, l’impostazione del controllo di accesso del modello di autorizzazione predefinito non è influenzata dalla creazione, modifica o rimozione di eventuali gruppi di utenti chiusi (CUG). Viene invece applicato un nuovo tipo di criterio denominato `PrincipalSetPolicy` come contenuto di controllo di accesso aggiuntivo al nodo di destinazione. Questo criterio aggiuntivo si trova come elemento secondario del nodo di destinazione e, se presente, sarebbe di pari livello del nodo del criterio predefinito.

**Modifica dei criteri dei gruppi utenti chiusi (CUG) nella gestione del controllo di accesso**

Questo passaggio dalle proprietà JCR residue a un criterio di controllo degli accessi dedicato ha un impatto sull’autorizzazione necessaria per creare o modificare la parte di autorizzazione della funzione CUG. Poiché questa è considerata una modifica al contenuto di controllo dell&#39;accesso, richiede i privilegi `jcr:readAccessControl` e `jcr:modifyAccessControl` per essere scritti nell&#39;archivio. Pertanto, solo gli autori di contenuti autorizzati a modificare il contenuto di controllo di accesso di una pagina possono impostare o modificare tale contenuto. Questo è in contrasto con la vecchia implementazione in cui la capacità di scrivere proprietà JCR regolari era sufficiente, con conseguente escalation di privilegi.

**Nodo Di Destinazione Definito Dal Criterio**

Crea criteri CUG nel nodo JCR definendo la sottostruttura da assoggettare a restrizioni di accesso in lettura. È probabile che si tratti di una pagina AEM nel caso in cui si preveda che il gruppo utenti chiusi (CUG) influisca sull’intera struttura.

Il posizionamento del criterio CUG solo nel nodo jcr:content situato sotto una determinata pagina limita l&#39;accesso al contenuto s.str di una determinata pagina, ma non avrà effetto su pagine di pari livello o secondarie. Questo può essere un caso d’uso valido ed è possibile ottenerlo con un editor dell’archivio che consente di applicare contenuti ad accesso granulare. Tuttavia, contrasta con l&#39;implementazione precedente in cui il posizionamento di una proprietà cq:cugEnabled sul nodo jcr:content è stato rimappato internamente al nodo della pagina. Questa mappatura non viene più eseguita.

**Valutazione delle autorizzazioni con criteri per gruppi utenti chiusi (CUG)**

Passando dal vecchio supporto per gruppi utenti chiusi a un modello di autorizzazione aggiuntivo, cambia il modo in cui vengono valutate le autorizzazioni di lettura efficaci. Come descritto nella [documentazione di Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), a un determinato utente/gruppo/ruolo autorizzato a visualizzare `CUGcontent` verrà concesso l&#39;accesso in lettura solo se la valutazione delle autorizzazioni di tutti i modelli configurati nell&#39;archivio Oak concede l&#39;accesso in lettura.

In altre parole, per la valutazione delle autorizzazioni effettive, vengono prese in considerazione sia le voci di controllo di accesso `CUGPolicy` che le voci di controllo di accesso predefinite e l&#39;accesso in lettura al contenuto CUG viene concesso solo se concesso da entrambi i tipi di criteri. In un&#39;installazione AEM Publish predefinita in cui l&#39;accesso in lettura alla struttura `/content` completa è concesso a tutti, l&#39;effetto dei criteri CUG è lo stesso dell&#39;implementazione precedente.

**Valutazione su richiesta**

Il modello di autorizzazione CUG consente di attivare singolarmente la gestione del controllo degli accessi e la valutazione delle autorizzazioni:

* la gestione del controllo di accesso è abilitata se il modulo dispone di uno o più percorsi supportati in cui è possibile creare gruppi utenti chiusi (CUG)
* la valutazione delle autorizzazioni è abilitata solo se è selezionata anche l&#39;opzione **Valutazione CUG abilitata**.

Nella nuova valutazione predefinita dell’installazione di AEM dei criteri per gruppi utenti chiusi (CUG), è abilitata solo con la modalità di esecuzione &quot;pubblicazione&quot;. Per ulteriori dettagli, vedi i dettagli sulla configurazione predefinita [&#x200B; da AEM 6.3](#default-configuration-since-aem). Questo può essere verificato confrontando i criteri efficaci per un determinato percorso con i criteri memorizzati nel contenuto. I criteri effettivi verranno visualizzati solo se è abilitata la valutazione delle autorizzazioni per i gruppi di utenti chiusi (CUG).

Come spiegato in precedenza, i criteri di controllo dell&#39;accesso ai gruppi utenti chiusi (CUG) ora sono sempre memorizzati nel contenuto, ma la valutazione delle autorizzazioni effettive risultanti da tali criteri verrà applicata solo se **Valutazione gruppi utenti chiusi (CUG) abilitata** è attivata nella console di sistema in Apache Jackrabbit Oak **Configurazione gruppi utenti chiusi (CUG).** Per impostazione predefinita, è abilitato solo con la modalità di esecuzione &#39;pubblicazione&#39;.

### Differenze Di Autenticazione {#differences-with-regards-to-authentication}

Le differenze relative all’autenticazione sono descritte di seguito.

#### Tipo Di Mixin Dedicato Per Il Requisito Di Autenticazione {#dedicated-mixin-type-for-authentication-requirement}

Nell&#39;implementazione precedente, gli aspetti di autorizzazione e autenticazione di un CUG sono stati attivati da una singola proprietà JCR ( `cq:cugEnabled`). Per quanto riguarda l’autenticazione, ne è risultato un elenco aggiornato dei requisiti di autenticazione archiviati con l’implementazione Apache Sling Authenticator. Con la nuova implementazione, lo stesso risultato si ottiene contrassegnando il nodo di destinazione con un tipo mixin dedicato ( `granite:AuthenticationRequired`).

#### Proprietà Per Escludere Il Percorso Di Accesso {#property-for-excluding-login-path}

Il tipo mixin definisce una singola proprietà facoltativa denominata `granite:loginPath`, che corrisponde alla proprietà `cq:cugLoginPage`. A differenza dell’implementazione precedente, la proprietà del percorso di accesso viene rispettata solo se il relativo tipo di nodo dichiarante è il mixin menzionato. L’aggiunta di una proprietà con tale nome senza impostare il tipo mixin non ha alcun effetto e all’autenticatore non viene segnalato né un nuovo requisito né un’esclusione per il percorso di accesso.

#### Privilegio Per Il Requisito Di Autenticazione {#privilege-for-authentication-requirement}

Per aggiungere o rimuovere un tipo mixin è necessario concedere il privilegio `jcr:nodeTypeManagement`. Nell&#39;implementazione precedente, il privilegio `jcr:modifyProperties` viene utilizzato per modificare la proprietà residua.

Per quanto riguarda `granite:loginPath`, è necessario lo stesso privilegio per aggiungere, modificare o rimuovere la proprietà.

#### Nodo Di Destinazione Definito Dal Tipo Mixin {#target-node-defined-by-mixin-type}

Crea i requisiti di autenticazione nel nodo JCR che definisce la sottostruttura da sottoporre all’accesso forzato. È probabile che si tratti di una pagina AEM nel caso in cui si preveda che il gruppo utenti chiusi (CUG) influisca sull’intera struttura e l’interfaccia utente per la nuova implementazione aggiunge quindi il tipo mixin di requisito di autenticazione sul nodo della pagina.

Il posizionamento del criterio CUG solo nel nodo jcr:content situato sotto una determinata pagina limita l&#39;accesso solo al contenuto. Tuttavia, questo non influisce sul nodo della pagina stesso né su alcuna pagina figlia.

Questo potrebbe essere uno scenario valido ed è possibile con un editor di archivio che consente di posizionare il mixin in qualsiasi nodo. Tuttavia, il comportamento è in contrasto con l&#39;implementazione precedente, dove il posizionamento di una proprietà cq:cugEnabled o cq:cugLoginPage sul nodo jcr:content è stato rimappato internamente al nodo della pagina. Questa mappatura non viene più eseguita.

#### Percorsi supportati configurati {#configured-supported-paths}

Sia il tipo mixin `granite:AuthenticationRequired` che la proprietà granite:loginPath verranno rispettati solo all&#39;interno dell&#39;ambito definito dal set di **opzioni di configurazione percorsi supportati** presenti con il requisito di autenticazione **Adobe Granite e il gestore del percorso di accesso**. Se non viene specificato alcun percorso, la funzionalità dei requisiti di autenticazione viene disabilitata completamente. In questo caso, il tipo mixin e la proprietà diventano effettivi quando vengono aggiunti o impostati su un determinato nodo JCR.

### Mappatura di contenuti JCR, servizi OSGi e configurazioni {#mapping-of-jcr-content-osgi-services-and-configurations}

Il documento seguente fornisce una mappatura completa dei servizi OSGi, delle configurazioni e del contenuto dell’archivio tra la vecchia e la nuova implementazione.

Mappatura CUG a partire da AEM 6.3

[Ottieni il file](assets/cug-mapping.pdf)

## Aggiorna gruppo utenti chiusi {#upgrade-cug}

### Installazioni esistenti che utilizzano il gruppo utenti chiusi (CUG) obsoleto {#existing-installations-using-the-deprecated-cug}

L’implementazione del supporto per i gruppi utenti chiusi (CUG) precedente è stata dichiarata obsoleta e verrà rimossa per le versioni future. Si consiglia di passare alle nuove implementazioni durante l’aggiornamento da versioni precedenti a AEM 6.3.

Per l’installazione aggiornata di AEM, è importante assicurarsi che sia abilitata una sola implementazione CUG. La combinazione del nuovo e del vecchio supporto CUG obsoleto non viene testata ed è probabile che causi un comportamento indesiderato:

* conflitti nell’autenticatore Sling relativi ai requisiti di autenticazione
* accesso in lettura negato quando la configurazione ACL associata al vecchio CUG si scontra con un nuovo criterio CUG.

### Migrazione di contenuti CUG esistenti {#migrating-existing-cug-content}

Adobe fornisce uno strumento per la migrazione alla nuova implementazione CUG. Per utilizzarlo, effettua le seguenti operazioni:

1. Vai a `https://<serveraddress>:<serverport>/system/console/cug-migration` per accedere allo strumento.
1. Immettere il percorso radice per il quale si desidera verificare i gruppi utenti chiusi e premere il pulsante **Esegui esecuzione in prova**. Esegue la scansione dei gruppi utenti chiusi (CUG) idonei per la conversione nella posizione selezionata.
1. Dopo aver esaminato i risultati, premi il pulsante **Esegui migrazione** per migrare alla nuova implementazione.

>[!NOTE]
>
>In caso di problemi, è possibile impostare un logger specifico al livello **DEBUG** su `com.day.cq.auth.impl.cug` per ottenere l&#39;output dello strumento di migrazione. Per ulteriori informazioni su come eseguire questa operazione, vedere [Registrazione](/help/sites-deploying/configure-logging.md).
