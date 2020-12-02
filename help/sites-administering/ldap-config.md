---
title: Configurazione di LDAP con AEM 6
seo-title: Configurazione di LDAP con AEM 6
description: Scoprite come configurare LDAP con AEM.
seo-description: Scoprite come configurare LDAP con AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---


# Configurazione di LDAP con AEM 6 {#configuring-ldap-with-aem}

LDAP (il **L** protocollo **D** directory **A** Access **P** Access) viene utilizzato per accedere ai servizi di directory centralizzate. In questo modo si riducono gli sforzi necessari per gestire gli account utente a cui possono accedere più applicazioni. Uno di questi server LDAP è Active Directory. LDAP viene spesso utilizzato per ottenere Single Sign On, che consente all’utente di accedere a più applicazioni dopo l’accesso.

Gli account utente possono essere sincronizzati tra il server LDAP e l’archivio, e i dettagli dell’account LDAP vengono salvati nell’archivio. Questo consente di assegnare gli account ai gruppi di repository per l&#39;allocazione delle autorizzazioni e dei privilegi richiesti.

L’archivio utilizza l’autenticazione LDAP per autenticare tali utenti, con le credenziali trasmesse al server LDAP per la convalida, necessaria prima di consentire l’accesso all’archivio. Per migliorare le prestazioni, le credenziali convalidate correttamente possono essere memorizzate nella cache dall&#39;archivio, con un timeout di scadenza per garantire che il ripristino si verifichi dopo un periodo appropriato.

Quando un account viene rimosso dalla convalida del server LDAP non viene più concesso e viene negato l’accesso all’archivio. È inoltre possibile eliminare i dettagli degli account LDAP salvati nell’archivio.

L’utilizzo di tali account è trasparente per gli utenti, che non vedono alcuna differenza tra gli account utente e di gruppo creati da LDAP e quelli creati esclusivamente nell’archivio.

In AEM 6, il supporto LDAP viene fornito con una nuova implementazione che richiede un tipo di configurazione diverso rispetto alle versioni precedenti.

Tutte le configurazioni LDAP sono ora disponibili come configurazioni OSGi. Possono essere configurati tramite la console Gestione Web all&#39;indirizzo:
`https://serveraddress:4502/system/console/configMgr`

Affinché LDAP funzioni con AEM, è necessario creare tre configurazioni OSGi:

1. Un provider di identità LDAP (IDP).
1. Un Gestore Di Sincronizzazione.
1. Un Modulo Di Login Esterno.

>[!NOTE]
>
>Guardate il modulo di login esterno di [Oak - Autenticazione con LDAP e oltre](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) per acquisire i moduli di login esterni.
>
>Per leggere un esempio di configurazione  Experience Manager con Apache DS, vedere [Configurazione di Adobe Experience Manager 6.5 per l&#39;utilizzo di Apache Directory Service.](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## Configurazione del provider di identità LDAP {#configuring-the-ldap-identity-provider}

Il provider di identità LDAP viene utilizzato per definire il modo in cui gli utenti vengono recuperati dal server LDAP.

È disponibile nella console di gestione sotto il nome **Apache Jackrabbit Oak LDAP Identity Provider**.

Per il provider di identità LDAP sono disponibili le seguenti opzioni di configurazione:

<table>
 <tbody>
  <tr>
   <td><strong>Nome provider LDAP</strong></td>
   <td>Nome della configurazione del provider LDAP.</td>
  </tr>
  <tr>
   <td><strong>Nome host server LDAP</strong><br /> </td>
   <td>Nome host del server LDAP</td>
  </tr>
  <tr>
   <td><strong>Porta server LDAP</strong></td>
   <td>Porta del server LDAP</td>
  </tr>
  <tr>
   <td><strong>Usa SSL</strong></td>
   <td>Indica se utilizzare una connessione SSL (LDAP).</td>
  </tr>
  <tr>
   <td><strong>Usa TLS</strong></td>
   <td>Indica se TLS deve essere avviato sulle connessioni.</td>
  </tr>
  <tr>
   <td><strong>Disattiva controllo certificati</strong></td>
   <td>Indica se la convalida del certificato del server deve essere disabilitata.</td>
  </tr>
  <tr>
   <td><strong>DN di binding</strong></td>
   <td>DN dell’utente per l’autenticazione. Se questo campo viene lasciato vuoto, verrà eseguito un binding anonimo.</td>
  </tr>
  <tr>
   <td><strong>Password di binding</strong></td>
   <td>Password dell'utente per l'autenticazione</td>
  </tr>
  <tr>
   <td><strong>Timeout ricerca</strong></td>
   <td>Tempo fino al termine della ricerca</td>
  </tr>
  <tr>
   <td><strong>Massimo pool amministratore attivo</strong></td>
   <td>La dimensione massima attiva del pool di connessioni di amministrazione.</td>
  </tr>
  <tr>
   <td><strong>Massimo pool di utenti attivo</strong></td>
   <td>Dimensione massima attiva del pool di connessioni utente.</td>
  </tr>
  <tr>
   <td><strong>DN base utente</strong></td>
   <td>DN per ricerche utente</td>
  </tr>
  <tr>
   <td><strong>Classi degli oggetti utente</strong></td>
   <td>L'elenco delle classi di oggetti che una voce utente deve contenere.</td>
  </tr>
  <tr>
   <td><strong>Attributo ID utente</strong></td>
   <td>Nome dell’attributo che contiene l’ID utente.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra utente</strong></td>
   <td>Filtro LDAP aggiuntivo da usare per la ricerca di utenti. Il filtro finale è formattato come: '(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Percorsi DN utente</strong></td>
   <td>Controlla se il DN deve essere utilizzato per calcolare una parte del percorso intermedio.</td>
  </tr>
  <tr>
   <td><strong>DN base gruppo</strong></td>
   <td>DN di base per le ricerche di gruppi.</td>
  </tr>
  <tr>
   <td><strong>Classi degli oggetti gruppo</strong></td>
   <td>L'elenco delle classi di oggetti che una voce di gruppo deve contenere.</td>
  </tr>
  <tr>
   <td><strong>Attributo nome gruppo</strong></td>
   <td>Nome dell’attributo che contiene il nome del gruppo.</td>
  </tr>
  <tr>
   <td><strong>Raggruppa filtro aggiuntivo</strong></td>
   <td>Filtro LDAP aggiuntivo da usare per la ricerca di gruppi. Il filtro finale è formattato come: '(&amp;(&lt;nomeAttr&gt;=&lt;nomeGruppo&gt;)(objectclass=&lt;classeOggetto&gt;)&lt;filtroExtra&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Percorsi DN gruppo</strong></td>
   <td>Controlla se il DN deve essere utilizzato per calcolare una parte del percorso intermedio.</td>
  </tr>
  <tr>
   <td><strong>Attributo membro del gruppo</strong></td>
   <td>Attributo del gruppo che contiene i membri di un gruppo.</td>
  </tr>
 </tbody>
</table>

## Configurazione del gestore di sincronizzazione {#configuring-the-synchronization-handler}

Il gestore di sincronizzazione definirà il modo in cui gli utenti e i gruppi del provider di identità verranno sincronizzati con il repository.

Si trova sotto il nome **Apache Jackrabbit Oak Default Sync Handler** nella console di gestione.

Per il gestore sincronizzazione sono disponibili le seguenti opzioni di configurazione:

<table>
 <tbody>
  <tr>
   <td><strong>Nome gestore sincronizzazione</strong></td>
   <td>Nome della configurazione di sincronizzazione.</td>
  </tr>
  <tr>
   <td><strong>Ora di scadenza utente</strong></td>
   <td>Durata fino alla scadenza di un utente sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>iscrizione automatica utente</strong></td>
   <td>Elenco di gruppi a cui viene aggiunto automaticamente un utente sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>Mappatura proprietà utente</strong></td>
   <td>Definizione di mappatura elenco delle proprietà locali da quelle esterne.</td>
  </tr>
  <tr>
   <td><strong>Prefisso percorso utente</strong></td>
   <td>Il prefisso del percorso utilizzato per la creazione di nuovi utenti.</td>
  </tr>
  <tr>
   <td><strong>Scadenza iscrizione utente</strong></td>
   <td>Tempo di scadenza dell'iscrizione.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profondità di nidificazione appartenenza utente</strong></td>
   <td>Restituisce la profondità massima di nidificazione del gruppo durante la sincronizzazione delle relazioni di appartenenza. Un valore pari a 0 disabilita efficacemente la ricerca di appartenenza al gruppo. Il valore 1 aggiunge solo i gruppi diretti di un utente. Questo valore non ha alcun effetto quando si sincronizzano singoli gruppi solo quando si sincronizza un antenato di appartenenza a un utente.</td>
  </tr>
  <tr>
   <td><strong>Ora di scadenza gruppo</strong></td>
   <td>Durata fino alla scadenza di un gruppo sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>iscrizione automatica al gruppo</strong></td>
   <td>Elenco di gruppi a cui viene aggiunto automaticamente un gruppo sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>Mappatura delle proprietà del gruppo</strong></td>
   <td>Definizione di mappatura elenco delle proprietà locali da quelle esterne.</td>
  </tr>
  <tr>
   <td><strong>Prefisso percorso gruppo</strong></td>
   <td>Prefisso percorso utilizzato per la creazione di nuovi gruppi.</td>
  </tr>
 </tbody>
</table>

## Il modulo di login esterno {#the-external-login-module}

Il modulo di login esterno si trova nella sezione **Apache Jackrabbit Oak External Login Module** nella console di gestione.

>[!NOTE]
>
>Il modulo di login esterno Apache Jackrabbit Oak implementa le specifiche Java Authentication and Authorization Servi (JAAS). Per ulteriori informazioni, vedere la [guida ufficiale  Oracle Java Security Reference Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html).

Il suo compito è definire il provider di identità e il gestore di sincronizzazione da utilizzare, con l&#39;effettivo binding dei due moduli.

Sono disponibili le seguenti opzioni di configurazione:

| **Classificazione JAAS** | Specifica della classificazione (cioè l’ordine di ordinamento) di questa voce del modulo di login. Le voci vengono ordinate in ordine decrescente (ad esempio, le configurazioni con un valore più elevato vengono visualizzate per prime). |
|---|---|
| **Flag di controllo JAAS** | Proprietà che specifica se un LoginModule è OBBLIGATORIO, OBBLIGATORIO, SUFFICIENTE o FACOLTATIVO. Per ulteriori informazioni sul significato di questi flag, fare riferimento alla documentazione di configurazione JAAS. |
| **JAAS Realm** | Nome dell&#39;area di autenticazione (o nome dell&#39;applicazione) rispetto al quale viene registrato il Modulo di accesso. Se non viene fornito alcun nome di realm, LoginModule viene registrato con un realm predefinito come configurato nella configurazione Felix JAAS. |
| **Nome provider identità** | Nome del provider di identità. |
| **Nome gestore sincronizzazione** | Nome del gestore di sincronizzazione. |

>[!NOTE]
>
>Se intendete disporre di più configurazioni LDAP con l’istanza AEM, dovete creare provider di identità e gestori sincronizzazione separati per ogni configurazione.

## Configurare LDAP su SSL {#configure-ldap-over-ssl}

AEM 6 può essere configurato per l’autenticazione con LDAP tramite SSL seguendo la procedura seguente:

1. Selezionare le caselle di controllo **Usa SSL** o **Usa TLS** durante la configurazione del [provider di identità LDAP](#configuring-the-ldap-identity-provider).
1. Configurate il gestore di sincronizzazione e il modulo di login esterno in base alla configurazione.
1. Se necessario, installate i certificati SSL nella macchina virtuale Java. A tale scopo, è possibile utilizzare lo strumento keytool:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Verificate la connessione al server LDAP.

### Creazione di certificati SSL {#creating-ssl-certificates}

I certificati autofirmati possono essere utilizzati per configurare AEM per l’autenticazione con LDAP tramite SSL. Di seguito è riportato un esempio di procedura di lavoro per la generazione di certificati da utilizzare con AEM.

1. Accertatevi che sia installata e funzionante una libreria SSL. Questa procedura utilizza OpenSSL come esempio.

1. Create un file di configurazione OpenSSL personalizzato (cnf). Questo può essere fatto copiando il file di configurazione **openssl.cnf **predefinito e personalizzandolo. Sui sistemi UNIX, in genere si trova in `/usr/lib/ssl/openssl.cnf`

1. Per creare la chiave radice CA, esegui il comando seguente in un terminale:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Create quindi un nuovo certificato autofirmato:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1.  Inspect il certificato appena generato per essere sicuri che tutto sia in ordine:

   `openssl x509 -noout -text -in root-ca.crt`

1. Verificate che tutte le cartelle specificate nel file di configurazione del certificato (.cnf) esistano. In caso contrario, createli.
1. Create un seme casuale, eseguendo, ad esempio:

   `openssl rand -out private/.rand 8192`

1. Spostate i file .pem creati nelle posizioni configurate nel file .cnf.

1. Infine, aggiungete il certificato all&#39;archivio chiavi Java.

## Abilitazione della registrazione di debug {#enabling-debug-logging}

La registrazione del debug può essere abilitata sia per il provider di identità LDAP che per il modulo di login esterno, al fine di risolvere i problemi di connessione.

Per abilitare la registrazione di debug, è necessario:

1. Passate alla console di gestione Web.
1. Trovate &quot;Apache Sling Logging Logger Configuration&quot; e create due logger con le seguenti opzioni:

* Livello di registro: Debug
* File di registro logs/ldap.log
* Pattern messaggio: {0,data,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.security.authentication.ldap

* Livello di registro: Debug
* File di registro: logs/external.log
* Pattern messaggio: {0,data,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.spi.security.authentication.external

## Una parola sull&#39;affiliazione del gruppo {#a-word-on-group-affiliation}

Gli utenti sincronizzati tramite LDAP possono appartenere a diversi gruppi di AEM. Questi gruppi possono essere gruppi LDAP esterni che verranno aggiunti a AEM come parte del processo di sincronizzazione, ma possono anche essere gruppi che vengono aggiunti separatamente e non fanno parte dello schema di affiliazione del gruppo LDAP originale.

Nella maggior parte dei casi, questi possono essere gruppi aggiunti da un amministratore AEM locale o da qualsiasi altro provider di identità.

Se un utente viene rimosso da un gruppo sul server LDAP, la modifica verrà riflessa anche sul lato AEM al momento della sincronizzazione. Tuttavia, tutte le altre affiliazioni di gruppo dell’utente che non sono state aggiunte da LDAP rimarranno in vigore.

AEM rileva e gestisce l&#39;eliminazione degli utenti da gruppi esterni utilizzando la proprietà `rep:externalId`. Questa proprietà viene aggiunta automaticamente a qualsiasi utente o gruppo sincronizzato dal Gestore sincronizzazione e contiene informazioni sul provider di identità di origine.

Per ulteriori informazioni, consultate la documentazione Apache Oak in [Sincronizzazione utente e gruppo](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemi noti {#known-issues}

Se intendete utilizzare LDAP su SSL, accertatevi che i certificati utilizzati siano creati senza l’opzione commento Netscape. Se questa opzione è abilitata, l&#39;autenticazione non riuscirà con un errore di Handshake SSL.

