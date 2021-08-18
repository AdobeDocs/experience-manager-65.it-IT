---
title: Sincronizzazione utente community
seo-title: Sincronizzazione utente community
description: Funzionamento della sincronizzazione utente
seo-description: Funzionamento della sincronizzazione utente
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: f4f4be3d9885723953b1306ff25a52d27799aa93
workflow-type: tm+mt
source-wordcount: '2508'
ht-degree: 1%

---

# Sincronizzazione utente community {#communities-user-synchronization}

## Introduzione {#introduction}

In AEM Communities, dall&#39;ambiente di pubblicazione (a seconda delle autorizzazioni configurate), i *visitatori del sito* possono diventare *membri*, creare *gruppi di utenti* e modificare il loro *profilo membro* .

*I* dati utente sono termini utilizzati per fare riferimento a  *utenti*,  *profili* utente e gruppi di  *utenti*.

** Iscrizione è un termine utilizzato per fare riferimento agli  ** utenti registrati nell’ambiente di pubblicazione, rispetto agli utenti registrati nell’ambiente di authoring.

Per ulteriori informazioni sui dati utente, visita [Gestione di utenti e gruppi di utenti](/help/communities/users.md).

## Sincronizzazione degli utenti in una farm di pubblicazione {#synchronizing-users-across-a-publish-farm}

Per progettazione, i dati utente creati nell’ambiente di pubblicazione non vengono visualizzati nell’ambiente di authoring.

La maggior parte dei dati utente creati nell’ambiente di authoring ha lo scopo di rimanere nell’ambiente di authoring e non viene sincronizzata né replicata nelle istanze di pubblicazione.

Quando la [topologia](/help/communities/topologies.md) è una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm), la registrazione e le modifiche effettuate su un&#39;istanza di pubblicazione devono essere sincronizzate con altre istanze di pubblicazione. I membri devono essere in grado di accedere e visualizzare i propri dati su qualsiasi nodo di pubblicazione.

Quando la sincronizzazione utente è abilitata, i dati utente vengono sincronizzati automaticamente tra le istanze di pubblicazione nella farm.

### Istruzioni per l&#39;installazione della sincronizzazione utente {#user-sync-setup-instructions}

Per istruzioni dettagliate e dettagliate su come abilitare la sincronizzazione in una farm di pubblicazione, vedi:

* [Sincronizzazione utente](/help/sites-administering/sync.md)

## Sincronizzazione utente in background  {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **pacchetto vlt**

   Si tratta di un file zip di tutte le modifiche apportate a un editore, che deve essere distribuito tra gli editori. Le modifiche apportate a un editore generano eventi selezionati dal listener di eventi change. Questo crea un pacchetto vlt contenente tutte le modifiche.

* **pacchetto di distribuzione**

   Contiene informazioni di distribuzione per Sling. Queste sono informazioni su dove il contenuto deve essere distribuito e quando è stato distribuito per ultimo.

## Cosa Succede Quando ... {#what-happens-when}

### Pubblica sito dalla console Sites di Communities {#publish-site-from-communities-sites-console}

Su autore, quando un sito community viene pubblicato dalla [console Sites di Communities](/help/communities/sites-console.md), l&#39;effetto è quello di [replicare](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) le pagine associate e Sling distribuisce i gruppi di utenti della community creati dinamicamente, inclusa la loro appartenenza.

### L’utente viene creato o modifica il profilo in Pubblica {#user-is-created-or-edits-profile-on-publish}

Per progettazione, gli utenti e i profili creati nell’ambiente di pubblicazione (ad esempio mediante registrazione automatica, accesso social network, autenticazione LDAP) non vengono visualizzati nell’ambiente di authoring.

Quando la topologia è una [farm di pubblicazione](/help/communities/topologies.md) e la sincronizzazione utente è stata configurata correttamente, i *utenti* e *profili utente* vengono sincronizzati nella farm di pubblicazione utilizzando la distribuzione Sling.

### Viene creato un nuovo gruppo community su Pubblica {#new-community-group-is-created-on-publish}

Anche se avviata da un&#39;istanza di pubblicazione, la creazione del gruppo community, che si traduce in nuove pagine del sito e in un nuovo gruppo di utenti, in realtà avviene nell&#39;istanza di authoring.

Come parte del processo, le nuove pagine del sito vengono replicate in tutte le istanze di pubblicazione. Il gruppo di utenti della community creato dinamicamente e la relativa iscrizione sono Sling distribuiti a tutte le istanze di pubblicazione.

### Utenti o gruppi di utenti creati tramite la console di sicurezza {#users-or-user-groups-are-created-using-security-console}

Per progettazione, i dati utente creati nell’ambiente di pubblicazione non vengono visualizzati nell’ambiente di authoring e viceversa.

Quando la console [Amministrazione utente e sicurezza](/help/sites-administering/security.md) viene utilizzata per aggiungere nuovi utenti nell’ambiente di pubblicazione, la sincronizzazione utente sincronizza i nuovi utenti e la loro appartenenza al gruppo con altre istanze di pubblicazione, se necessario. La sincronizzazione utente sincronizza anche i gruppi di utenti creati tramite la console di sicurezza.

### Pubblicazioni utente Contenuto su Pubblica {#user-posts-content-on-publish}

Per il contenuto generato dall’utente (UGC), i dati immessi in un’istanza di pubblicazione sono accessibili tramite l’ [SRP](/help/communities/srp-config.md) configurato.

## Best practice {#bestpractices}

Per impostazione predefinita, la sincronizzazione utente è **disabilitata**. L&#39;abilitazione della sincronizzazione utente comporta la modifica delle configurazioni *esistenti* OSGi. Non è necessario aggiungere nuove configurazioni per abilitare la sincronizzazione utente.

La sincronizzazione utente si basa sull’ambiente di authoring per gestire le distribuzioni di dati utente, anche se i dati utente non vengono creati sull’autore .

**Prerequisiti**

1. Se utenti e gruppi di utenti sono già stati creati su un editore, si consiglia di [sincronizzare manualmente](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) i dati utente a tutti gli editori prima di configurare e abilitare la sincronizzazione utente.

   Una volta abilitata la sincronizzazione utente, vengono sincronizzati solo gli utenti e i gruppi appena creati .

1. Verifica che sia stato installato il codice più recente:

   * [Aggiornamenti AEM piattaforma](https://helpx.adobe.com/it/experience-manager/kb/aem62-available-hotfixes.html)
   * [Aggiornamenti AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Le seguenti configurazioni sono necessarie per abilitare la sincronizzazione utente su AEM Communities. Assicurati che queste configurazioni siano corrette per evitare errori nella distribuzione del contenuto sling.

### Agente di distribuzione Apache Sling - Sync Agent Factory {#apache-sling-distribution-agent-sync-agents-factory}

Questa configurazione recupera il contenuto da sincronizzare tra gli editori. La configurazione si trova nell’istanza Author. L&#39;autore deve tenere traccia di tutti gli editori presenti e di dove sincronizzare tutte le informazioni.

I valori predefiniti nella configurazione sono per una singola istanza di pubblicazione. Poiché la sincronizzazione utente è utile per sincronizzare più istanze di pubblicazione, ad esempio per una farm di pubblicazione, è necessario aggiungere ulteriori istanze di pubblicazione alla configurazione.

**Come viene sincronizzato il contenuto?**

L&#39;istanza dell&#39;autore esegue il ping dell&#39;endpoint dell&#39;esportatore degli editori. Ogni volta che un utente viene creato o aggiornato su editori specifici (n), l&#39;autore ottiene il contenuto dai propri endpoint di esportazione e [invia il contenuto](/help/communities/sync.md#main-pars-image-1413756164) ad altri editori (n-1, a parte gli editori da cui viene recuperato il contenuto).

Per configurare la configurazione degli agenti di sincronizzazione Apache Sling:

1. Accedi con privilegi di amministratore all’istanza di authoring AEM.
1. Accedi alla [Console web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html). Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Individua **Apache Sling Distribution Agent - Sync Agents Factory**.

   * Seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita).

      Nome verifica: **socialpubsync.**

   * Selezionare la casella di controllo **Attivato**.
   * Seleziona **Usa più code.**
   * Specifica **Endpoint esportazione** e **Endpoint importazione** (puoi aggiungere altri endpoint di esportazione e importazione).

      Questi endpoint definiscono la posizione da cui desideri ottenere il contenuto e la posizione in cui desideri inviarlo. L’autore recupera il contenuto dall’endpoint di esportazione specificato e lo invia agli editori (diversi dall’editore da cui ha recuperato il contenuto).
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Distribuzione Granite Adobe - Provider segreto di trasporto password crittografata {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Consente all’autore di identificare l’utente autorizzato, in quanto dispone dell’autorizzazione per sincronizzare i dati utente dall’autore alla pubblicazione.

L’ [utente autorizzato creato](/help/sites-administering/sync.md#createauthuser) su tutte le istanze di pubblicazione aiuta gli editori a connettersi con l’autore e configurare la distribuzione Sling sull’autore. Questo utente autorizzato ha tutti i [ACLs](/help/sites-administering/sync.md#howtoaddacl) richiesti.

Ogni volta che i dati devono essere installati o recuperati dagli editori, l’autore si connette con gli editori utilizzando le credenziali (nome utente e password) impostate in questa configurazione.

Per collegare l&#39;autore agli editori utilizzando un utente autorizzato:

1. Accedi con privilegi di amministratore all’istanza di authoring AEM.
1. Accedi alla [Console web](/help/sites-deploying/configuring-osgi.md).

   Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Individua **Distribuzione Granite Adobe - Provider segreto di trasporto password crittografata.**
1. Seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita).

   Verifica la proprietà **socialpubsync** - **publishUser.**

1. Imposta il nome utente e la password sull&#39; [utente autorizzato](/help/sites-administering/sync.md#createauthorizeduser).

   Ad esempio, **user sync - admin**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Agente di distribuzione Apache Sling - Queue Agent Factory {#apache-sling-distribution-agent-queue-agents-factory}

Questa configurazione viene utilizzata per configurare i dati da sincronizzare tra gli editori. Quando i dati vengono creati/aggiornati nei percorsi specificati in **Radici consentite**, viene attivato &quot;var/community/distribution/diff&quot; e il replicatore creato recupera i dati da un editore e li installa su altri editori.

Per configurare i dati (percorsi dei nodi) da sincronizzare:

1. Accedi con privilegi di amministratore all’istanza di pubblicazione.
1. Accedi alla [Console web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Individua **Apache Sling Distribution Agent - Queue Agent Factory**.
1. Seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita).

   Nome verifica: **socialpubsync -reverse**

1. Selezionare la casella di controllo **Abilitato** e salvare.
1. Specifica i percorsi dei nodi da replicare in **Radici consentite**.
1. Ripeti la procedura per ogni istanza **pubblica**.

   ![queue-agent-fact](assets/queue-agents-fact.png)

### Distribuzione Granite Adobe - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

Questa configurazione sincronizza l&#39;appartenenza al gruppo tra gli editori.
Se la modifica dell&#39;appartenenza di un gruppo in un editore non ne aggiorna l&#39;appartenenza ad altri editori, assicurati che **ref:Members** venga aggiunto a **nomi di proprietà analizzate**.

Per garantire la sincronizzazione dei membri:

1. Accedi con privilegi di amministratore all’istanza di pubblicazione.
1. Accedi alla [Console web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Individua **Distribuzione granite Adobe - Diff Observer Factory**.
1. Seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita).

   Verifica **nome agente: socialpubsync -reverse**.

1. Selezionare la casella di controllo **Attivato**.
1. Specificare **rep:Members** come descrizione per propertyName in **nome proprietà cercato** e salvare.

   ![diff-obs](assets/diff-obs.png)

### Trigger di distribuzione Apache Sling - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Questa configurazione ti consente di configurare l’intervallo di polling (dopo il quale gli editori vengono inseriti nel ping e le modifiche vengono richiamate dall’autore) per sincronizzare le modifiche tra gli editori.

L’autore controlla gli editori ogni 30 secondi (impostazione predefinita). Se nella cartella `/var/sling/distribution/packages/  socialpubsync -  vlt /shared` sono presenti pacchetti, questi verranno recuperati e installati su altri editori.

Per modificare l’intervallo di polling:

1. Accedi con privilegi di amministratore all’istanza di authoring AEM.
1. Accedi alla [Console web](/help/sites-deploying/configuring-osgi.md), ad esempio [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Individua **Trigger di distribuzione Apache Sling - Scheduled Triggers Factory**

   * Seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita).

      Verifica **socialpubsync -scheduled-trigger**

   * Imposta l&#39;intervallo in secondi sull&#39;intervallo desiderato e salva.

   ![innesco programmato](assets/scheduled-trigger.png)

### Listener di sincronizzazione utenti di AEM Communities {#aem-communities-user-sync-listener}

Per i problemi nella distribuzione Sling in cui vi è una discrepanza nelle sottoscrizioni e seguenti, controlla se sono impostate le seguenti proprietà in **AEM Communities User Sync Listener** configurazioni:

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* Cartelle distribuite

Per sincronizzare abbonamenti, seguiti e notifiche

Su ogni istanza di pubblicazione AEM:

1. Accedi con privilegi di amministratore.
1. Accedi alla [Console web](/help/sites-deploying/configuring-osgi.md). Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Individua **AEM Communities User Sync Listener**.
1. Seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita)

   Nome verifica: **socialpubsync -scheduled-trigger**

1. Imposta i seguenti **NodeTypes**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   I tipi di nodo specificati in questa proprietà verranno sincronizzati e le informazioni sulle notifiche (blog e configurazioni seguite) vengono sincronizzate tra diversi editori.

1. Aggiungi tutte le cartelle da sincronizzare in **DistributedFolders**. Esempio,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Imposta **ignorablenodes** su:

   `.tokens`

   `system`

   `rep:cache` (poiché utilizziamo sessioni permanenti, non è necessario sincronizzare questo nodo con editori diversi).

   ![user-sync-listner](assets/user-sync-listner.png)

### ID Sling univoco {#unique-sling-id}

AEM’istanza di authoring utilizza l’ID Sling per identificare da dove vengono i dati e a quali editori deve (o non deve) restituire il pacchetto.

Assicurati che tutti gli editori in una farm di pubblicazione abbiano un ID Sling univoco. Se l’ID Sling è lo stesso per più istanze di pubblicazione in una farm di pubblicazione, la sincronizzazione utente avrà esito negativo. Poiché l’autore non saprà da dove recuperare il pacchetto e dove installarlo.

Per garantire un ID Sling univoco degli editori nella farm di pubblicazione, per ogni istanza di pubblicazione:

1. Vai a [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Controlla il valore di **Sling ID**.

   ![singhiozzo](assets/slingid.png)

   Se l’ID Sling di un’istanza di pubblicazione corrisponde all’ID Sling di qualsiasi altra istanza di pubblicazione, allora:

1. Interrompi una delle istanze di pubblicazione con un ID Sling corrispondente.
1. Nella directory `crx-quickstart/launchpad/felix`, cerca ed elimina il file denominato *sling.id.file.*

   Ad esempio, su un sistema Linux:

   `rm -i $(find . -type f -name sling.id.file)`

   Ad esempio, in un sistema Windows:

   Utilizzare windows explorer e cercare `sling.id.file`

1. Avvia l&#39;istanza di pubblicazione. All&#39;avvio gli verrà assegnato un nuovo ID Sling.
1. Convalida che l&#39; **Sling ID** sia ora univoco.

Ripeti questi passaggi fino a quando tutte le istanze di pubblicazione hanno un ID Sling univoco.

### Vault Package Builder Factory {#vault-package-builder-factory}

Affinché gli aggiornamenti si sincronizzino correttamente, è necessario modificare il generatore di pacchetti vault per la sincronizzazione utente.
In `/home/users` viene creato un nodo `*/rep:cache`. È una cache che viene utilizzata per scoprire che se eseguiamo query sul nome principale di un nodo allora questa cache può essere utilizzata direttamente.

La sincronizzazione utente può interrompersi se i nodi `rep :cache` sono sincronizzati tra gli editori.

Per garantire che gli aggiornamenti siano sincronizzati correttamente tra gli editori, in ogni istanza di pubblicazione AEM:

1. Accedi alla [Console web](/help/sites-deploying/configuring-osgi.md)

   Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Individua il **Pacchetto di distribuzione Apache Sling - Vault Package Builder Factory**

   Nome del generatore: socialpubsync-vlt.

1. Seleziona l’icona di modifica.
1. Aggiungi due filtri del nodo del pacchetto:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Gestione dei criteri
   * Per sovrascrivere i nodi rep:policy esistenti con quelli nuovi, aggiungi un terzo filtro pacchetti: `/home/users|+.*/rep:policy`
   * Per evitare la distribuzione dei criteri, imposta: `Acl Handling: IGNORE`

   ![Fabbrica del generatore di pacchetti di Vault](assets/vault-package-builder-factory.png)

## Risolvere i problemi relativi alla distribuzione Sling in AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Se la distribuzione Sling non riesce, prova i seguenti passaggi di debug:

1. **Verifica configurazioni aggiunte  [in modo errato](/help/sites-administering/sync.md#improperconfig)**

   Assicurati che non vengano aggiunte o modificate più configurazioni, ma devi modificare le configurazioni predefinite esistenti.
1. **Controllare le configurazioni**

   Assicurati che tutte le [configurazioni](/help/communities/sync.md#bestpractices) siano impostate correttamente nell&#39;istanza di AEM Author, come indicato in [Best practice](/help/communities/sync.md#main-pars-header-863110628).

1. **Verifica autorizzazioni utente autorizzate**

   Se i pacchetti non sono installati correttamente, controlla che l&#39; [utente autorizzato](/help/sites-administering/sync.md#createauthuser) creato nella prima istanza di pubblicazione abbia le ACL corrette.

   Per convalidarlo, invece della configurazione [utente autorizzato creato](/help/sites-administering/sync.md#createauthuser) modifica la [Distribuzione granite di Adobe - Provider segreto di trasporto password crittografata](/help/sites-administering/sync.md#adobegraniteencpasswrd) nell&#39;istanza Autore per utilizzare le credenziali utente amministratore. Ora prova di nuovo a installare i pacchetti. Se la sincronizzazione utente funziona correttamente con le credenziali di amministratore, significa che l&#39;utente di pubblicazione creato non aveva ACL appropriati.

1. **Controllare la configurazione di Diff Observer Factory**

   Se solo nodi specifici non sono sincronizzati nella farm di pubblicazione, ad esempio, i membri del gruppo non sono sincronizzati, assicurati che la configurazione [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) sia abilitata e **rep: i membri** sono impostati in **nomi delle proprietà analizzate**.

1. **Controlla la configurazione del listener di sincronizzazione utente di AEM Communities.** Se gli utenti creati sono sincronizzati ma le sottoscrizioni e i seguenti non funzionano, assicurati che la configurazione del listener di sincronizzazione utenti di AEM Communities abbia:

   * Tipi di nodo: impostato su **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder** e **sling:OrderedFolder**.
   * Nodi ignorabili: impostati su **.tokens**, **system** e **rep:cache**.
   * Cartelle distribuite: impostate le cartelle da distribuire.

1. **Controlla i registri generati durante la creazione dell’utente nell’istanza Publish**

   Se le configurazioni di cui sopra sono impostate in modo appropriato ma la sincronizzazione utente non funziona, controlla i registri generati al momento della creazione dell’utente.

   Verifica se l’ordine dei registri è lo stesso, come segue:

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

Per eseguire il debug:

1. Disattiva la sincronizzazione utente:
1. Su AEM’istanza di authoring, accedi con privilegi di amministratore.

   1. Accedi alla [Console web](/help/sites-deploying/configuring-osgi.md). Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individua la configurazione **Apache Sling Distribution Agent - Sync Agents Factory**.
   1. Deseleziona la casella di controllo **Abilitato** .

      Quando si disabilita la sincronizzazione utente nell’istanza di authoring, gli endpoint (esportazione e importazione) sono disabilitati e l’istanza di authoring è statica. I pacchetti **vlt** non vengono inseriti o recuperati dall’autore.

      Ora, se un utente viene creato sull&#39;istanza di pubblicazione, il pacchetto **vlt** viene creato nel nodo */var/sling/distribution/packages/ socialpubsync - vlt /data* . E se questi pacchetti vengono inviati dall&#39;autore a un altro servizio. Puoi scaricare ed estrarre questi dati per controllare quali proprietà vengono inviate ad altri servizi.

1. Passa a un editore e crea un utente sull&#39;editore. Di conseguenza, vengono creati degli eventi.
1. Controlla l&#39; [ordine dei log](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities) creati al momento della creazione dell&#39;utente.
1. Controlla se un pacchetto **vlt** viene creato su **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Ora, abilita la sincronizzazione utente sull&#39;istanza AEM autore.
1. Sull&#39;editore, modifica gli endpoint dell&#39;esportatore o dell&#39;importatore in **Apache Sling Distribution Agent - Sync Agents Factory**.
Possiamo scaricare ed estrarre i dati del pacchetto per verificare quali proprietà vengono inviate ad altri editori e quali dati vengono persi.
