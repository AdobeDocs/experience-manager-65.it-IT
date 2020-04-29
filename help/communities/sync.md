---
title: Sincronizzazione utenti community
seo-title: Sincronizzazione utenti community
description: Funzionamento della sincronizzazione degli utenti
seo-description: Funzionamento della sincronizzazione degli utenti
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
translation-type: tm+mt
source-git-commit: acc758b83486e8c623e31bb4a68f3c29dd4848ba

---


# Sincronizzazione utenti community {#communities-user-synchronization}

## Introduzione {#introduction}

In AEM Communities, dall’ambiente di pubblicazione (in base alle autorizzazioni configurate), i visitatori *del* sito possono diventare *membri*, creare gruppi *di* utenti e modificare il profilo *del* membro.

*I dati* utente sono termini utilizzati per fare riferimento a *utenti*, profili ** utente e gruppi *di* utenti.

*Membri* è un termine utilizzato per fare riferimento agli *utenti* registrati nell’ambiente di pubblicazione, anziché agli utenti registrati nell’ambiente di authoring.

Per ulteriori informazioni sui dati utente, visita [Gestione di utenti e gruppi](/help/communities/users.md)di utenti.

## Sincronizzazione degli utenti in una farm di pubblicazione {#synchronizing-users-across-a-publish-farm}

Per impostazione predefinita, i dati utente creati nell’ambiente di pubblicazione non vengono visualizzati nell’ambiente di authoring.

La maggior parte dei dati utente creati nell’ambiente di authoring deve rimanere nell’ambiente di authoring e non deve essere sincronizzata né replicata nelle istanze di pubblicazione.

Quando la [topologia](/help/communities/topologies.md) è una farm [di](/help/sites-deploying/recommended-deploys.md#tarmk-farm)pubblicazione, la registrazione e le modifiche apportate a un’istanza di pubblicazione devono essere sincronizzate con altre istanze di pubblicazione. I membri devono poter effettuare l’accesso e visualizzare i propri dati su qualsiasi nodo di pubblicazione.

Quando la sincronizzazione utente è abilitata, i dati utente vengono automaticamente sincronizzati tra le istanze di pubblicazione nella farm.

### Istruzioni per la configurazione della sincronizzazione degli utenti {#user-sync-setup-instructions}

Per istruzioni dettagliate e dettagliate su come abilitare la sincronizzazione in una farm di pubblicazione, consultate:

* [Sincronizzazione utente](/help/sites-administering/sync.md)

## Sincronizzazione utente in background {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **pacchetto VLT**

   Si tratta di un file zip contenente tutte le modifiche apportate a un editore, che devono essere distribuite tra gli editori. Le modifiche apportate a un editore generano eventi selezionati dal listener di eventi change. In questo modo viene creato un pacchetto di convalida contenente tutte le modifiche.

* **pacchetto di distribuzione**

   Contiene informazioni di distribuzione per Sling. Si tratta di informazioni su dove il contenuto deve essere distribuito e quando è stato distribuito per ultimo.

## Cosa Succede Quando ... {#what-happens-when}

### Pubblica sito dalla console Siti di Communities {#publish-site-from-communities-sites-console}

Per autore, quando un sito community viene pubblicato dalla console [Siti](/help/communities/sites-console.md)community, l&#39;effetto consiste nel [replicare](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) le pagine associate e Sling distribuisce i gruppi di utenti della community creati dinamicamente, inclusa la loro appartenenza.

### L&#39;utente viene creato o modifica il profilo in Pubblica {#user-is-created-or-edits-profile-on-publish}

Per impostazione predefinita, gli utenti e i profili creati nell’ambiente di pubblicazione (ad esempio mediante registrazione automatica, accesso mediante social network e autenticazione LDAP) non vengono visualizzati nell’ambiente di authoring.

Se la topologia è una farm [di](/help/communities/topologies.md) pubblicazione e la sincronizzazione utente è stata configurata correttamente, il profilo ** utente *e* utente viene sincronizzato nella farm di pubblicazione utilizzando la distribuzione Sling.

### Nuovo gruppo community creato in Pubblica {#new-community-group-is-created-on-publish}

Anche se avviata da un’istanza di pubblicazione, la creazione di gruppi di community, che genera nuove pagine di sito e un nuovo gruppo di utenti, viene in realtà creata nell’istanza di creazione.

Come parte del processo, le nuove pagine del sito vengono replicate in tutte le istanze di pubblicazione. Il gruppo di utenti della community creato dinamicamente e la relativa appartenenza sono Sling distribuiti a tutte le istanze di pubblicazione.

### Utenti o gruppi di utenti creati tramite la console di sicurezza {#users-or-user-groups-are-created-using-security-console}

Per impostazione predefinita, i dati utente creati nell’ambiente di pubblicazione non vengono visualizzati nell’ambiente di authoring e viceversa.

Quando la console Amministrazione [utente e sicurezza](/help/sites-administering/security.md) viene utilizzata per aggiungere nuovi utenti nell’ambiente di pubblicazione, la sincronizzazione utente sincronizza i nuovi utenti e i relativi membri del gruppo con altre istanze di pubblicazione, se necessario. La sincronizzazione utente sincronizza anche i gruppi di utenti creati tramite la console di protezione.

### Post utente Contenuto su Pubblica {#user-posts-content-on-publish}

Per il contenuto generato dall’utente (UGC), i dati immessi in un’istanza di pubblicazione sono accessibili tramite l’SRP [](/help/communities/srp-config.md)configurato.

## Best practices {#bestpractices}

Per impostazione predefinita, la sincronizzazione utente è **disattivata**. L&#39;abilitazione della sincronizzazione utente comporta la modifica delle configurazioni OSGi *esistenti* . Non è necessario aggiungere nuove configurazioni per abilitare la sincronizzazione degli utenti.

La sincronizzazione utente si basa sull’ambiente di authoring per gestire le distribuzioni dei dati utente, anche se i dati utente non vengono creati in fase di creazione.

**Prerequisiti**

1. Se utenti e gruppi di utenti sono già stati creati su un editore, si consiglia di sincronizzare [](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) manualmente i dati utente a tutti gli editori prima di configurare e abilitare la sincronizzazione utente.

   Una volta attivata la sincronizzazione degli utenti, vengono sincronizzati solo gli utenti e i gruppi appena creati.

1. Verifica che sia stato installato il codice più recente:

   * [Aggiornamenti della piattaforma AEM](https://helpx.adobe.com/it/experience-manager/kb/aem62-available-hotfixes.html)
   * [Aggiornamenti di AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Per abilitare la sincronizzazione degli utenti in AEM Communities, sono necessarie le seguenti configurazioni. Verificate che queste configurazioni siano corrette per evitare il malfunzionamento della distribuzione del contenuto.

### Apache Sling Distribution Agent - Sync Agent Factory {#apache-sling-distribution-agent-sync-agents-factory}

Questa configurazione recupera il contenuto da sincronizzare tra gli editori. La configurazione si trova nell’istanza Author. L&#39;autore deve tenere traccia di tutti gli editori presenti e di dove sincronizzare tutte le informazioni.

I valori predefiniti nella configurazione si riferiscono a una singola istanza di pubblicazione. Poiché la sincronizzazione degli utenti è utile per sincronizzare più istanze di pubblicazione, ad esempio per una farm di pubblicazione, è necessario aggiungere ulteriori istanze di pubblicazione alla configurazione.

**Come viene sincronizzato il contenuto?**

L’istanza Author esegue il ping dell’endpoint di esportazione degli editori. Ogni volta che un utente viene creato o aggiornato su editori specifici (n), l’autore riceve il contenuto dai punti finali dell’esportatore e [invia il contenuto](/help/communities/sync.md#main-pars-image-1413756164) ad altri editori (n-1, a parte gli editori da cui viene recuperato il contenuto).

Per configurare la configurazione degli agenti di sincronizzazione Apache Sling:

1. Accedete con privilegi di amministratore all’istanza di creazione di AEM.
1. Accedere alla console [](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)Web. Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Individuare **Apache Sling Distribution Agent - Sync Agent Factory**.

   * Selezionate la configurazione esistente da aprire per la modifica (icona matita).

      Nome verifica: **socialpubsync.**

   * Selezionare la casella di controllo **Abilitato** .
   * Selezionate **Usa più code.**
   * Specificate endpoint **** di esportazione e **endpoint** di importazione (potete aggiungere altri endpoint di esportazione e importazione).

      Questi endpoint definiscono dove si desidera ottenere il contenuto e dove si desidera inviare il contenuto push. L&#39;autore recupera il contenuto dall&#39;endpoint di esportazione specificato e invia il contenuto agli editori (diversi dall&#39;editore da cui ha recuperato il contenuto).
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Distribuzione di Adobe Granite - Provider Segreto di trasporto password crittografato {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Consente all’autore di identificare l’utente autorizzato, in quanto dispone dell’autorizzazione per sincronizzare i dati utente dall’autore alla pubblicazione.

L’utente [autorizzato creato](/help/sites-administering/sync.md#createauthuser) su tutte le istanze di pubblicazione consente agli editori di connettersi con l’autore e configurare la distribuzione Sling per l’autore. Questo utente autorizzato dispone di tutti gli [ACL](/help/sites-administering/sync.md#howtoaddacl)richiesti.

Ogni volta che i dati devono essere installati o recuperati dagli editori, l&#39;autore si connette con gli editori utilizzando le credenziali (nome utente e password) impostate in questa configurazione.

Per collegare l&#39;autore con gli editori utilizzando un utente autorizzato:

1. Accedete con privilegi di amministratore all’istanza di creazione di AEM.
1. Accedere alla console [](/help/sites-deploying/configuring-osgi.md)Web.

   Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Individua distribuzione **Adobe Granite - Provider Segreto Di Trasporto Password Crittografato.**
1. Selezionate la configurazione esistente da aprire per la modifica (icona matita).

   Verificare la proprietà **socialpubsync** - **publishUser.**

1. Impostate il nome utente e la password per l’utente [](/help/sites-administering/sync.md#createauthorizeduser)autorizzato.

   Ad esempio, **usersync - admin**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Coda Agenti Factory {#apache-sling-distribution-agent-queue-agents-factory}

Questa configurazione viene utilizzata per configurare i dati da sincronizzare tra gli editori. Quando i dati vengono creati/aggiornati nei percorsi specificati in **Consentite Roots**, &quot;var/community/distribution/diff&quot; viene attivato e il replicatore creato recupera i dati da un editore e li installa su altri editori.

Per configurare i dati (percorsi nodo) da sincronizzare:

1. Effettuate l’accesso con i privilegi di amministratore per l’istanza di creazione.
1. Accedere alla console [](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)Web.

   Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Individua agente di distribuzione **Apache Sling - Coda Agenti Factory**.
1. Selezionate la configurazione esistente da aprire per la modifica (icona matita).

   Nome verifica: **socialpubsync -reverse**

1. Selezionate la casella di controllo **Abilitato** e salvate.
1. Specificare i percorsi dei nodi da replicare nelle radici **** consentite.
1. Ripetete questa procedura per ogni istanza di **pubblicazione** .

   ![queue-agent-fact](assets/queue-agents-fact.png)

### Distribuzione Adobe Granite - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

Questa configurazione sincronizza l&#39;appartenenza al gruppo tra gli editori.
Se la modifica dell&#39;appartenenza di un gruppo in un editore non ne aggiorna l&#39;appartenenza ad altri editori, accertatevi che **ref:members** sia aggiunto ai nomi **delle proprietà** analizzate.

Per garantire la sincronizzazione dei membri:

1. Accedete con privilegi di amministratore all’istanza di creazione di AEM.
1. Accedere alla console [](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)Web.

   Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Individuare **Adobe Granite Distribution - Diff Observer Factory**.
1. Selezionate la configurazione esistente da aprire per la modifica (icona matita).

   Verifica nome **agente: socialpubsync -reverse**.

1. Selezionare la casella di controllo **Abilitato** .
1. Specificate **rep:members** come descrizione per propertyName nei nomi **delle proprietà** cercate e Save.

   ![diff-obs](assets/diff-obs.png)

### Trigger di distribuzione Apache Sling - Factory Triggers programmati {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Questa configurazione consente di configurare l’intervallo di polling (al termine del quale gli editori vengono sottoposti a ping e le modifiche vengono eseguite dall’autore) per sincronizzare le modifiche tra gli editori.

L’autore controlla gli editori ogni 30 secondi (impostazione predefinita). Se nella cartella sono presenti pacchetti `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, questi verranno recuperati e installati su altri editori.

Per modificare l’intervallo di polling:

1. Accedete con privilegi di amministratore all’istanza di creazione di AEM.
1. Accedere alla console [](/help/sites-deploying/configuring-osgi.md)Web, ad esempio [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Individua trigger di distribuzione **Apache Sling - Scheduled Triggers Factory**

   * Selezionate la configurazione esistente da aprire per la modifica (icona matita).

      Verifica **socialpubsync -Scheduled-trigger**

   * Impostate l&#39;intervallo in secondi sull&#39;intervallo desiderato e salvate.
   ![trigger programmato](assets/scheduled-trigger.png)

### Listener di sincronizzazione utenti di AEM Communities {#aem-communities-user-sync-listener}

Per problemi nella distribuzione Sling in cui vi è una discrepanza nelle iscrizioni e seguenti, controlla se le seguenti proprietà nelle configurazioni di **AEM Communities User Sync Listener** sono impostate:

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

Per sincronizzare iscrizioni, seguiti e notifiche

In ogni istanza di pubblicazione AEM:

1. Effettuate l&#39;accesso con privilegi di amministratore.
1. Accedere alla console [](/help/sites-deploying/configuring-osgi.md)Web. Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Individua listener **di sincronizzazione utenti di** AEM Communities.
1. Seleziona la configurazione esistente da aprire per la modifica (icona matita)

   Nome verifica: **socialpubsync - Scheduled-trigger**

1. Impostate i seguenti **NodeTypes**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   I tipi di nodo specificati in questa proprietà verranno sincronizzati e le informazioni sulle notifiche (blog e configurazioni seguite) vengono sincronizzate tra editori diversi.

1. Aggiungere tutte le cartelle da sincronizzare in **DistributedFolders**. Ad esempio,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Impostate i **nodi ignorablenodes** su:

   `.tokens`

   `system`

   `rep:cache` (poiché utilizziamo sessioni di tipo &quot;fisso&quot;, non è necessario sincronizzare questo nodo con editori diversi).

   ![user-sync-listner](assets/user-sync-listner.png)

### ID Sling univoco {#unique-sling-id}

L’istanza di creazione di AEM utilizza l’ID Sling per identificare da dove arrivano i dati e a quali editori deve (o non deve) inviare nuovamente il pacchetto.

Accertatevi che tutti gli editori di una farm di pubblicazione abbiano un ID Sling univoco. Se l’ID Sling è lo stesso per più istanze di pubblicazione in una farm di pubblicazione, la sincronizzazione degli utenti non riesce. Poiché l&#39;autore non sa da dove recuperare il pacchetto e dove installarlo.

Per garantire un ID Sling univoco degli editori nella farm di pubblicazione, in ogni istanza di pubblicazione:

1. Accedete a [https://_host:porta_/sistema/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Controllare il valore di **Sling ID**.

   ![singhiozzo](assets/slingid.png)

   Se l’ID Sling di un’istanza di pubblicazione corrisponde all’ID Sling di qualsiasi altra istanza di pubblicazione, effettuate le seguenti operazioni:

1. Interrompi una delle istanze di pubblicazione con un ID Sling corrispondente.
1. Nella `crx-quickstart/launchpad/felix` directory, cercare ed eliminare il file denominato *sling.id.file.*

   Ad esempio, su un sistema Linux:

   `rm -i $(find . -type f -name sling.id.file)`

   Ad esempio, in un sistema Windows:

   Utilizzare windows explorer e cercare `sling.id.file`

1. Avviate l’istanza di pubblicazione. All&#39;avvio, gli verrà assegnato un nuovo Sling ID.
1. Verifica che l’ID **** Sling sia ora univoco.

Ripetete questi passaggi finché tutte le istanze di pubblicazione non dispongono di un ID Sling univoco.

### Vault Package Builder Factory {#vault-package-builder-factory}

Affinché gli aggiornamenti possano essere sincronizzati correttamente, è necessario modificare il generatore di pacchetti vault per la sincronizzazione degli utenti.
In `/home/users`, viene creato un `*/rep:cache` nodo. È una cache che viene utilizzata per scoprire che se eseguiamo query sul nome principale di un nodo, allora questa cache può essere utilizzata direttamente.

La sincronizzazione degli utenti può interrompersi se `rep :cache` i nodi sono sincronizzati tra gli editori.

Per garantire la corretta sincronizzazione degli aggiornamenti tra gli editori, in ogni istanza di pubblicazione AEM:

1. Accesso alla console [Web](/help/sites-deploying/configuring-osgi.md)

   Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Individua il pacchetto di distribuzione **Apache Sling - Vault Package Builder Factory**

   Nome del generatore: socialpubsync-vlt.

1. Selezionate l’icona di modifica.
1. Aggiungete due filtri nodo pacchetto:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Gestione dei criteri
   * Per sovrascrivere i nodi rep:policy con i nuovi, aggiungete un terzo Filtro pacchetto: `/home/users|+.*/rep:policy`
   * Per evitare la distribuzione dei criteri, impostare: `Acl Handling: IGNORE`
   ![Fabbrica del generatore di pacchetti Vault](assets/vault-package-builder-factory.png)

## Risoluzione dei problemi di distribuzione Sling in AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Se la distribuzione Sling non riesce, provate i seguenti passaggi di debug:

1. **Verifica configurazioni aggiunte[in modo errato](/help/sites-administering/sync.md#improperconfig)**

   Assicuratevi che non vengano aggiunte o modificate più configurazioni, ma che le configurazioni predefinite esistenti vengano modificate.
1. **Controllare le configurazioni**

   Assicurati che tutte le [configurazioni](/help/communities/sync.md#bestpractices) siano impostate correttamente nell&#39;istanza di AEM Author, come indicato nelle [Best Practices](/help/communities/sync.md#main-pars-header-863110628).

1. **Verifica autorizzazioni utente autorizzate**

   Se i pacchetti non sono installati correttamente, verificate che l&#39;utente [](/help/sites-administering/sync.md#createauthuser) autorizzato creato nella prima istanza di pubblicazione abbia gli ACL corretti.

   Per convalidarlo, invece di [creare l&#39;utente](/help/sites-administering/sync.md#createauthuser) autorizzato, modificate la configurazione [Adobe Granite Distribution - Encrypted Password Transport Secret Provider (Fornitore](/help/sites-administering/sync.md#adobegraniteencpasswrd) segreto di trasporto password crittografato) nell&#39;istanza Author per utilizzare le credenziali utente Admin. Tentate nuovamente di installare i pacchetti. Se la sincronizzazione utente funziona correttamente con le credenziali dell&#39;amministratore, significa che l&#39;utente di pubblicazione creato non aveva ACL appropriati.

1. **Controllare la configurazione di Diff Observer Factory**

   Se solo nodi specifici non vengono sincronizzati nella farm di pubblicazione, ad esempio, i membri del gruppo non sono sincronizzati, accertatevi che la configurazione [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) sia abilitata e **rep: i membri** vengono impostati nei nomi delle proprietà **analizzate**.

1. **Verificate la configurazione del listener di sincronizzazione utenti di AEM Communities.** Se gli utenti creati sono sincronizzati ma le iscrizioni e i seguenti elementi non funzionano, assicurati che la configurazione del listener di sincronizzazione utenti di AEM Communities disponga di:

   * Tipi di nodo: impostati su **rep:User, nt:unstructure**, **nt:resource**, **rep:ACL**, **sling:Folder** e **sling:OrderedFolder**.
   * Nodi ignorabili: impostati su **.tokens**, **system** e **rep:cache**.
   * Cartelle distribuite: impostate le cartelle che desiderate distribuire.

1. **Controllate i registri generati durante la creazione dell’utente nell’istanza Pubblica**

   Se le configurazioni di cui sopra sono impostate correttamente ma la sincronizzazione utente non funziona, controllate i registri generati al momento della creazione dell&#39;utente.

   Verificare se l’ordine dei file di registro è lo stesso, come segue:

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
1. Nell’istanza di creazione di AEM, effettuate l’accesso con privilegi di amministratore.

   1. Accedere alla console [](/help/sites-deploying/configuring-osgi.md)Web. Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individuare la configurazione **Apache Sling Distribution Agent - Sync Agent Factory**.
   1. Deselezionare la casella di controllo **Abilitato** .

      Quando si disabilita la sincronizzazione utente nell’istanza di creazione, gli endpoint (esportatore e importatore) vengono disattivati e l’istanza di creazione è statica. I pacchetti **vlt** non vengono cerchiati o inseriti dall&#39;autore.

      Ora, se un utente viene creato nell’istanza di pubblicazione, il pacchetto **vlt** viene creato nel nodo */var/sling/distribution/packages/ socialpubsync - vlt /data* . E se questi pacchetti vengono inviati dall&#39;autore a un altro servizio. Puoi scaricare ed estrarre questi dati per verificare quali proprietà vengono inviate ad altri servizi.

1. Passate a un editore e create un utente sull&#39;editore. Di conseguenza, gli eventi vengono creati.
1. Controllate l’ [ordine dei registri](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)creati al momento della creazione dell’utente.
1. Verificate se un pacchetto **vlt** viene creato su **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Ora abilitate la sincronizzazione degli utenti nell’istanza di creazione di AEM.
1. Nell&#39;editore, modificate gli endpoint di esportazione o importazione in **Apache Sling Distribution Agent - Sync Agent Factory**.
Possiamo scaricare ed estrarre i dati del pacchetto per verificare quali proprietà vengono inviate ad altri editori e quali dati vengono persi.
