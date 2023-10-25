---
title: Configurazione di LDAP con AEM 6
description: Scopri come utilizzare e configurare i servizi LDAP con AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 0%

---

# Configurazione di LDAP con AEM 6 {#configuring-ldap-with-aem}

LDAP (il **L** leggero **D** directory **A** accesso **P** protocollo) viene utilizzato per accedere ai servizi di directory centralizzati. Consente di ridurre lo sforzo necessario per gestire gli account utente in quanto sono accessibili da più applicazioni. Uno di questi server LDAP è Active Directory. LDAP viene spesso utilizzato per ottenere Single Sign-On che consente a un utente di accedere a più applicazioni dopo l&#39;accesso una sola volta.

Gli account utente possono essere sincronizzati tra il server LDAP e il repository, con i dettagli dell&#39;account LDAP salvati nel repository. Questa funzionalità consente di assegnare gli account ai gruppi del repository per l&#39;allocazione delle autorizzazioni e dei privilegi richiesti.

Il repository utilizza l&#39;autenticazione LDAP per autenticare tali utenti, con le credenziali passate al server LDAP per la convalida, necessaria prima di consentire l&#39;accesso al repository. Per migliorare le prestazioni, le credenziali convalidate correttamente possono essere memorizzate nella cache dall’archivio, con un timeout di scadenza per garantire che la riconvalida avvenga dopo un periodo di tempo appropriato.

Quando un account viene rimosso dal server LDAP, la convalida non viene più concessa e l’accesso all’archivio viene negato. È inoltre possibile eliminare i dettagli degli account LDAP salvati nell’archivio.

L’utilizzo di tali account è trasparente per i tuoi utenti. In altre parole, non vedono alcuna differenza tra gli account utente e di gruppo creati da LDAP e gli account creati esclusivamente nell’archivio.

In AEM 6, il supporto LDAP viene fornito con una nuova implementazione che richiede un tipo di configurazione diverso rispetto alle versioni precedenti.

Tutte le configurazioni LDAP sono ora disponibili come configurazioni OSGi. Possono essere configurati tramite la console Gestione web all’indirizzo:
`https://serveraddress:4502/system/console/configMgr`

Affinché LDAP funzioni con AEM, devi creare tre configurazioni OSGi:

1. Provider di identità LDAP (IDP).
1. Gestore di sincronizzazione.
1. Un Modulo Di Accesso Esterno.

>[!NOTE]
>
>Osserva [Modulo di accesso esterno Oak - Autenticazione con LDAP e oltre](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=en) per approfondire i moduli di accesso esterno.
>
>Per un Experience Manager sulla configurazione di Apache DS, consulta [Configurazione di Adobe Experience Manager 6.5 per l’utilizzo del servizio directory Apache.](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805)

## Configurazione Del Provider Di Identità LDAP {#configuring-the-ldap-identity-provider}

Il provider di identità LDAP viene utilizzato per definire la modalità di recupero degli utenti dal server LDAP.

Si trova nella console di gestione sotto al **Provider di identità LDAP Apache Jackrabbit Oak** nome.

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
   <td>Indica se deve essere utilizzata una connessione SSL (LDAP).</td>
  </tr>
  <tr>
   <td><strong>Usa TLS</strong></td>
   <td>Indica se TLS deve essere avviato sulle connessioni.</td>
  </tr>
  <tr>
   <td><strong>Disattiva verifica certificati</strong></td>
   <td>Indica se la convalida del certificato del server deve essere disabilitata.</td>
  </tr>
  <tr>
   <td><strong>Associa DN</strong></td>
   <td>DN dell'utente per l'autenticazione. Se questo campo viene lasciato vuoto, viene eseguito un binding anonimo.</td>
  </tr>
  <tr>
   <td><strong>Password binding</strong></td>
   <td>Password dell’utente per l’autenticazione</td>
  </tr>
  <tr>
   <td><strong>Timeout ricerca</strong></td>
   <td>Tempo fino al timeout di una ricerca</td>
  </tr>
  <tr>
   <td><strong>Massimo pool di amministrazione attivo</strong></td>
   <td>Dimensione massima attiva del pool di connessioni amministratore.</td>
  </tr>
  <tr>
   <td><strong>Max. pool utenti attivo</strong></td>
   <td>Dimensione massima attiva del pool di connessioni utente.</td>
  </tr>
  <tr>
   <td><strong>DN base utente</strong></td>
   <td>DN per le ricerche utente</td>
  </tr>
  <tr>
   <td><strong>Classi oggetto utente</strong></td>
   <td>L'elenco delle classi oggetto che una voce utente deve contenere.</td>
  </tr>
  <tr>
   <td><strong>Attributo ID utente</strong></td>
   <td>Nome dell’attributo che contiene l’ID utente.</td>
  </tr>
  <tr>
   <td><strong>Filtro aggiuntivo utente</strong></td>
   <td>Filtro LDAP aggiuntivo da utilizzare per la ricerca di utenti. Il filtro finale è formattato come: '(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Percorsi DN utente</strong></td>
   <td>Controlla se il DN deve essere utilizzato per calcolare una porzione del percorso intermedio.</td>
  </tr>
  <tr>
   <td><strong>DN base gruppo</strong></td>
   <td>DN di base per le ricerche di gruppi.</td>
  </tr>
  <tr>
   <td><strong>Raggruppa classi oggetto</strong></td>
   <td>L'elenco delle classi oggetto che una voce del gruppo deve contenere.</td>
  </tr>
  <tr>
   <td><strong>Attributo nome gruppo</strong></td>
   <td>Nome dell'attributo che contiene il nome del gruppo.</td>
  </tr>
  <tr>
   <td><strong>Filtro aggiuntivo gruppo</strong></td>
   <td>Filtro LDAP aggiuntivo da utilizzare per la ricerca di gruppi. Il filtro finale è formattato come: '(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Raggruppa percorsi DN</strong></td>
   <td>Controlla se il DN deve essere utilizzato per calcolare una porzione del percorso intermedio.</td>
  </tr>
  <tr>
   <td><strong>Attributo membro gruppo</strong></td>
   <td>Attributo gruppo contenente uno o più membri di un gruppo.</td>
  </tr>
 </tbody>
</table>

## Configurazione Del Gestore Di Sincronizzazione {#configuring-the-synchronization-handler}

Il gestore di sincronizzazione definisce il modo in cui gli utenti e i gruppi del provider di identità vengono sincronizzati con il repository.

Si trova sotto il **Gestore di sincronizzazione predefinito Apache Jackrabbit Oak** nome nella console di gestione.

Per il gestore di sincronizzazione sono disponibili le seguenti opzioni di configurazione:

<table>
 <tbody>
  <tr>
   <td><strong>Nome gestore di sincronizzazione</strong></td>
   <td>Nome della configurazione di sincronizzazione.</td>
  </tr>
  <tr>
   <td><strong>Tempo di scadenza utente</strong></td>
   <td>Durata della scadenza di un utente sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>Iscrizione automatica utente</strong></td>
   <td>Elenco di gruppi a cui viene aggiunto automaticamente un utente sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>Mappatura proprietà utente</strong></td>
   <td>Definizione di mapping elenco di proprietà locali da quelle esterne.</td>
  </tr>
  <tr>
   <td><strong>Prefisso percorso utente</strong></td>
   <td>Prefisso del percorso utilizzato per la creazione degli utenti.</td>
  </tr>
  <tr>
   <td><strong>Scadenza appartenenza utente</strong></td>
   <td>Tempo dopo il quale scade l’iscrizione.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profondità di nidificazione appartenenza utente</strong></td>
   <td>Restituisce la profondità massima della nidificazione dei gruppi quando le relazioni di appartenenza vengono sincronizzate. Un valore pari a 0 disattiva efficacemente la ricerca di appartenenza al gruppo. Il valore 1 aggiunge solo i gruppi diretti di un utente. Questo valore non ha alcun effetto quando si sincronizzano singoli gruppi solo durante la sincronizzazione di un elemento precedente di appartenenza degli utenti.</td>
  </tr>
  <tr>
   <td><strong>Ora scadenza gruppo</strong></td>
   <td>Durata fino alla scadenza di un gruppo sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>Iscrizione automatica gruppo</strong></td>
   <td>Elenco di gruppi a cui viene aggiunto automaticamente un gruppo sincronizzato.</td>
  </tr>
  <tr>
   <td><strong>Mappatura proprietà gruppo</strong></td>
   <td>Definizione di mapping elenco di proprietà locali da quelle esterne.</td>
  </tr>
  <tr>
   <td><strong>Prefisso percorso gruppo</strong></td>
   <td>Prefisso del percorso utilizzato per la creazione di gruppi.</td>
  </tr>
 </tbody>
</table>

## Modulo di accesso esterno {#the-external-login-module}

Il modulo di accesso esterno si trova sotto **Modulo di accesso esterno Apache Jackrabbit Oak** nella console di gestione.

>[!NOTE]
>
>Il modulo di accesso esterno Apache Jackrabbit Oak implementa le specifiche Java™ Authentication and Authorization Servi (JAAS). Consulta la [Guida di riferimento ufficiale per la sicurezza Java™ Oracle](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) per ulteriori informazioni.

Il suo lavoro consiste nel definire quale provider di identità e gestore di sincronizzazione utilizzare, associando in modo efficace i due moduli.

Sono disponibili le seguenti opzioni di configurazione:

| **Classifica JAAS** | Specifica la classificazione (ovvero l’ordinamento) di questa voce del modulo di accesso. Le voci sono ordinate in ordine decrescente (ovvero, le configurazioni con classificazione di valori più elevati vengono per prime). |
|---|---|
| **Flag di controllo JAAS** | Proprietà che specifica se LoginModule è REQUIRED, REQUIITE, SUFFICIENT o OPTIONAL. Per ulteriori informazioni sul significato di questi flag, consulta la documentazione sulla configurazione JAAS. |
| **Realm JAAS** | Il nome dell&#39;area di autenticazione (o nome dell&#39;applicazione) con cui è registrato LoginModule. Se non viene fornito alcun nome di area di autenticazione, LoginModule viene registrato con un&#39;area di autenticazione predefinita come configurato nella configurazione Felix JAAS. |
| **Nome provider di identità** | Nome del provider di identità. |
| **Nome gestore di sincronizzazione** | Nome del gestore di sincronizzazione. |

>[!NOTE]
>
Se si prevede di avere più configurazioni LDAP con l&#39;istanza AEM, è necessario creare provider di identità e gestori di sincronizzazione separati per ogni configurazione.

## Configurare LDAP su SSL {#configure-ldap-over-ssl}

AEM 6 può essere configurato per l’autenticazione con LDAP tramite SSL seguendo la procedura seguente:

1. Controlla la **Usa SSL** o **Usa TLS** caselle di controllo durante la configurazione di [Provider identità LDAP](#configuring-the-ldap-identity-provider).
1. Configura il gestore di sincronizzazione e il modulo di accesso esterno in base alla configurazione.
1. Se necessario, installa i certificati SSL nella tua Java™ VM. Questa installazione può essere eseguita utilizzando lo strumento chiave:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Verificare la connessione al server LDAP.

### Creazione di certificati SSL {#creating-ssl-certificates}

I certificati autofirmati possono essere utilizzati durante la configurazione dell’AEM per l’autenticazione con LDAP tramite SSL. Di seguito è riportato un esempio di procedura operativa per la generazione di certificati da utilizzare con l’AEM.

1. Assicurati di avere una libreria SSL installata e funzionante. Questa procedura utilizza OpenSSL come esempio.

1. Crea un file di configurazione OpenSSL (cnf) personalizzato. Questa configurazione può essere eseguita copiando il file di configurazione **openssl.cnf **predefinito e personalizzandolo. Nei sistemi UNIX®, è disponibile `/usr/lib/ssl/openssl.cnf`

1. Procedi alla creazione della chiave radice CA eseguendo il comando seguente in un terminale:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Quindi, crea un certificato autofirmato:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Per verificare che tutto sia a posto, controlla il certificato appena generato:

   `openssl x509 -noout -text -in root-ca.crt`

1. Verifica che siano presenti tutte le cartelle specificate nel file di configurazione del certificato (con estensione cnf). In caso contrario, creale.
1. Crea un valore di inizializzazione casuale eseguendo, ad esempio:

   `openssl rand -out private/.rand 8192`

1. Spostare i file con estensione pem creati nelle posizioni configurate nel file con estensione cnf.

1. Aggiungi infine il certificato al keystore Java™.

## Abilitazione registrazione debug {#enabling-debug-logging}

Per risolvere i problemi di connessione, è possibile abilitare la registrazione di debug sia per il provider di identità LDAP che per il modulo di accesso esterno.

Per abilitare la registrazione di debug, è necessario effettuare le seguenti operazioni:

1. Passa a Web Management Console.
1. Trova &quot;Apache Sling Logging Logger Configuration&quot; e crea due logger con le seguenti opzioni:

* Livello registro: debug
* File di registro logs/ldap.log
* Pattern messaggio: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.security.authentication.ldap

* Livello registro: debug
* File di registro: logs/external.log
* Pattern messaggio: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.spi.security.authentication.external

## Una parola sull&#39;affiliazione di gruppo {#a-word-on-group-affiliation}

Gli utenti sincronizzati tramite LDAP possono far parte di diversi gruppi in AEM. Questi gruppi possono essere gruppi LDAP esterni che vengono aggiunti all&#39;AEM come parte del processo di sincronizzazione. Tuttavia, possono anche essere gruppi aggiunti separatamente e non fanno parte dello schema di affiliazione al gruppo LDAP originale.

Di solito, questi gruppi vengono aggiunti da un amministratore AEM locale o da qualsiasi altro provider di identità.

Se un utente viene rimosso da un gruppo sul server LDAP, la modifica si riflette sul lato AEM durante la sincronizzazione. Tuttavia, tutte le altre affiliazioni di gruppo dell’utente che non sono state aggiunte da LDAP rimangono attive.

L’AEM rileva e gestisce l’eliminazione di utenti da gruppi esterni utilizzando `rep:externalId` proprietà. Questa proprietà viene aggiunta automaticamente a qualsiasi utente o gruppo sincronizzato dal gestore di sincronizzazione e contiene informazioni sul provider di identità di origine.

Consulta la documentazione di Apache Oak su [Sincronizzazione utenti e gruppi](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemi noti {#known-issues}

Se si prevede di utilizzare LDAP su SSL, assicurarsi che i certificati utilizzati vengano creati senza l&#39;opzione di commento Netscape. Se questa opzione è abilitata, l’autenticazione non riesce e viene restituito un errore di handshake SSL.
