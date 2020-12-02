---
title: Sincronizzazione utente
seo-title: Sincronizzazione utente
description: Scopri la sincronizzazione degli utenti in AEM.
seo-description: Scopri la sincronizzazione degli utenti in AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
translation-type: tm+mt
source-git-commit: 8ed7409740cdd3e45fad006dc6e470a06acc60fe
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 3%

---


# Sincronizzazione utente{#user-synchronization}

## Introduzione {#introduction}

Quando la distribuzione è una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm), i membri devono essere in grado di accedere e visualizzare i propri dati su qualsiasi nodo di pubblicazione.

Gli utenti e i gruppi di utenti (dati utente) creati nell’ambiente di pubblicazione non sono necessari nell’ambiente di authoring.

La maggior parte dei dati utente creati nell’ambiente di authoring deve restare nell’ambiente di authoring e non deve essere copiata nelle istanze di pubblicazione.

Per poter accedere agli stessi dati utente, le registrazioni e le modifiche effettuate su un’istanza di pubblicazione devono essere sincronizzate con altre istanze di pubblicazione.

A partire AEM 6.1, quando la sincronizzazione degli utenti è abilitata, i dati utente vengono automaticamente sincronizzati tra le istanze di pubblicazione nella farm e non vengono creati in fase di creazione.

## Distribuzione Sling {#sling-distribution}

I dati utente, insieme ai rispettivi [ACL](/help/sites-administering/security.md), sono memorizzati in [Oak Core](/help/sites-deploying/platform.md), il livello sotto Oak JCR, e sono accessibili tramite l&#39;API Oak [API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Con aggiornamenti non frequenti, è ragionevole che i dati utente siano sincronizzati con altre istanze di pubblicazione utilizzando [Sling Content Distribution](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (distribuzione Sling).

Rispetto alla replica tradizionale, i vantaggi della sincronizzazione utente mediante la distribuzione Sling sono i seguenti:

* *gli utenti*, i  *profili* utente e i  *raggruppamenti di utenti* creati al momento della pubblicazione non vengono creati in fase di creazione

* La distribuzione Sling imposta le proprietà negli eventi jcr, consentendo di agire all&#39;interno dei listener di eventi lato pubblicazione senza preoccuparsi di cicli di replica infiniti
* La distribuzione Sling invia solo i dati utente alle istanze di pubblicazione non originarie, eliminando il traffico non necessario
* [ACLsset ](/help/sites-administering/security.md) nel nodo utente sono inclusi nella sincronizzazione

>[!NOTE]
>
>Se sono necessarie sessioni, si consiglia di utilizzare una soluzione SSO o una sessione fissa e di fare in modo che i clienti accedano se accedono a un altro editore.

>[!CAUTION]
>
>La sincronizzazione del gruppo ***Administrators*** non è supportata, anche quando la sincronizzazione utente è abilitata. Al contrario, un&#39;operazione di importazione delle diff verrà registrata nel registro degli errori.
>
>Pertanto, se la distribuzione è una farm di pubblicazione, se un utente viene aggiunto o rimosso dal gruppo ***Administrators**, la modifica deve essere eseguita manualmente su ogni istanza di pubblicazione.

## Abilita sincronizzazione utente {#enable-user-sync}

>[!NOTE]
>
>Per impostazione predefinita, la sincronizzazione utente è `disabled`.
>
>L&#39;abilitazione della sincronizzazione utente comporta la modifica delle configurazioni *OSGi* esistenti.
>
>Non è necessario aggiungere nuove configurazioni per abilitare la sincronizzazione degli utenti.

La sincronizzazione utente si basa sull’ambiente di authoring per gestire le distribuzioni dei dati utente, anche se i dati utente non vengono creati in fase di creazione. Gran parte, ma non tutti, della configurazione avviene nell’ambiente di authoring e ogni passaggio indica chiaramente se deve essere eseguita sull’autore o sulla pubblicazione.

Di seguito sono riportati i passaggi necessari per abilitare la sincronizzazione degli utenti, seguiti da una sezione [Risoluzione dei problemi](#troubleshooting):

### Prerequisiti {#prerequisites}

1. Se utenti e gruppi di utenti sono già stati creati su un editore, si consiglia di [sincronizzare manualmente](#manually-syncing-users-and-user-groups) i dati utente a tutti gli editori prima di configurare e abilitare la sincronizzazione utente.

Una volta attivata la sincronizzazione degli utenti, vengono sincronizzati solo gli utenti e i gruppi appena creati.

1. Verifica che sia stato installato il codice più recente:

* [Aggiornamenti AEM piattaforma](https://helpx.adobe.com/it/experience-manager/kb/aem62-available-hotfixes.html)
* [Aggiornamenti  AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent - Sync Agent Factory {#apache-sling-distribution-agent-sync-agents-factory}

**Abilita sincronizzazione utente**

* **sull&#39;autore**

   * accesso con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * individuare `Apache Sling Distribution Agent - Sync Agents Factory`

      * selezionate la configurazione esistente da aprire per la modifica (icona matita)
Verifica `name`: **`socialpubsync`**

      * selezionare la casella di controllo `Enabled`
      * select `Save`


![](assets/chlimage_1-20.png)

### 2. Crea utente autorizzato {#createauthuser}

**Configura**
autorizzazioni: questo utente autorizzato verrà utilizzato nel passaggio 3 per configurare la distribuzione Sling per l’autore.

* **in ogni istanza di pubblicazione**

   * accesso con privilegi di amministratore
   * accedere alla [console di sicurezza](/help/sites-administering/security.md)

      * ad esempio, [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * creare un nuovo utente

      * ad esempio, `usersync-admin`
   * aggiungi questo utente al gruppo di utenti **`administrators`**
   * [aggiungi ACL per questo utente a /home](#howtoaddacl)

      * `Allow jcr:all` con restrizione  `rep:glob=*/activities/*`



>[!CAUTION]
>
>È necessario creare un nuovo utente.
>
>* L&#39;utente predefinito assegnato è **`admin`**.
>* Non utilizzare `communities-user-admin user.`

>



#### Come aggiungere ACL {#addacls}

* crxde lite di accesso

   * ad esempio, [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* selezionare il nodo `/home`
* nel riquadro a destra, selezionare la scheda `Access Control`
* selezionare il pulsante `+` per aggiungere una voce ACL

   * **Principal**:  *cercare gli utenti creati per la sincronizzazione degli utenti*
   * **Tipo**: `Allow`
   * **Privilegi**:  `jcr:all`
   * **** Restrictionsrep:idspn:  `*/activities/*`
   * selezionare **OK**

* selezionare **Salva tutto**

![](assets/chlimage_1-21.png)

Consulta anche

* [Accesso a Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Sezione Risoluzione dei problemi [Modifica eccezione di operazione durante l&#39;elaborazione delle risposte](#modify-operation-exception-during-response-processing).

### 3. Distribuzione granite  Adobe - Provider segreto di trasporto password crittografata {#adobegraniteencpasswrd}

**Configurare le autorizzazioni**

Una volta creato un utente autorizzato, membro del gruppo di utenti **`administrators`**in tutte le istanze di pubblicazione, tale utente autorizzato deve essere identificato all&#39;autore come dotato dell&#39;autorizzazione per sincronizzare i dati utente dall&#39;autore alla pubblicazione.

* **sull&#39;autore**

   * accesso con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * individuare `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * selezionate la configurazione esistente da aprire per la modifica (icona matita)
Verifica `property name`: **`socialpubsync-publishUser`**

   * impostare nome utente e password per l&#39; [utente autorizzato](#createauthuser) creato al momento della pubblicazione nel passaggio 2

      * ad esempio, `usersync-admin`


![](assets/chlimage_1-22.png)

### 4. Agente di distribuzione Apache Sling - Coda Agenti Factory {#apache-sling-distribution-agent-queue-agents-factory}

**Abilita sincronizzazione utente**

* **al momento della pubblicazione**:

   * accesso con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * individuare `Apache Sling Distribution Agent - Queue Agents Factory`

      * selezionate la configurazione esistente da aprire per la modifica (icona matita)
Verifica `Name`: `socialpubsync-reverse`

      * selezionare la casella di controllo `Enabled`
      * select `Save`
   * **ripetizione **per ogni istanza di pubblicazione



![](assets/chlimage_1-23.png)

### 5.  Adobe Social Sync - Diff Observer Factory {#diffobserver}

**Abilita sincronizzazione gruppo**

* **in ogni istanza** di pubblicazione:

   * accesso con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * individuare **`Adobe Social Sync - Diff Observer Factory`**

      * selezionate la configurazione esistente da aprire per la modifica (icona matita)

         Verifica `agent name`: `socialpubsync-reverse`

      * selezionare la casella di controllo `Enabled`
      * select `Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6. Trigger di distribuzione Apache Sling - Pianificate Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Facoltativo) modificare l’intervallo di polling**

Per impostazione predefinita, l’autore effettua il sondaggio per le modifiche ogni 30 secondi. Per modificare questo intervallo:

* **sull&#39;autore**

   * accesso con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * individuare `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * selezionate la configurazione esistente da aprire per la modifica (icona matita)

         * Verifica `Name`: `socialpubsync-scheduled-trigger`
      * impostare la `Interval in Seconds` sull&#39;intervallo desiderato
      * select `Save`



![](assets/chlimage_1-24.png)

## Configurare per più istanze di pubblicazione {#configure-for-multiple-publish-instances}

La configurazione predefinita è per una singola istanza di pubblicazione. Poiché l’abilitazione della sincronizzazione degli utenti consente di sincronizzare più istanze di pubblicazione, ad esempio per una farm di pubblicazione, è necessario aggiungere ulteriori istanze di pubblicazione alla fabbrica di sincronizzazione degli agenti.

### 7. Apache Sling Distribution Agent - Sync Agent Factory {#apache-sling-distribution-agent-sync-agents-factory-1}

**Aggiungi istanze di pubblicazione:**

* **sull&#39;autore**

   * accesso con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * individuare `Apache Sling Distribution Agent - Sync Agents Factory`

      * selezionate la configurazione esistente da aprire per la modifica (icona matita)
Verifica `Name`: `socialpubsync`


![](assets/chlimage_1-25.png)

* **Exporter**
Endpoints: deve essere presente un endpoint di esportazione per ogni editore. Ad esempio, se ci sono 2 editori, localhost:4503 e 4504, dovrebbero essere 2 voci:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Endpoint importazione:**
deve essere presente un endpoint di importazione per ogni editore. Ad esempio, se ci sono 2 editori, localhost:4503 e 4504, dovrebbero essere 2 voci:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* select `Save`

### 8.  AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

**(Facoltativo) Sincronizzare nodi JCR aggiuntivi**

Se è necessario sincronizzare dati personalizzati tra più istanze di pubblicazione, effettuate le seguenti operazioni:

* **in ogni istanza** di pubblicazione:

   * accesso con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, `https://localhost:4503/system/console/configMgr`
   * individuare `AEM Communities User Sync Listener`
   * selezionate la configurazione esistente da aprire per la modifica (icona matita)
Verifica `Name`: `socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **Nodo**
TipiElenco dei tipi di nodi che verranno sincronizzati. È necessario elencare qui qualsiasi tipo di nodo diverso da sling:Folder (sling:folder viene gestito separatamente).
Elenco predefinito dei tipi di nodo da sincronizzare:

   * rep:Utente
   * nt:unstructured
   * nt:resource

* **Proprietà**
ignorabili: elenco di proprietà che verranno ignorate in caso di rilevamento di modifiche. Le modifiche apportate a queste proprietà potrebbero essere sincronizzate come effetto collaterale di altre modifiche (poiché la sincronizzazione è sempre a livello di nodo), ma le modifiche apportate a tali proprietà non attiveranno di per sé la sincronizzazione.
Proprietà predefinita da ignorare:

   * cq:lastModified

* **Nodi**
ignorabili: percorsi secondari che verranno ignorati completamente durante la sincronizzazione. Nessun elemento all&#39;interno di questi sottotracciati verrà sincronizzato in qualsiasi momento.
Nodi predefiniti da ignorare:

   * .token
   * system

* **Distributed**
FoldersLa maggior parte delle sling:Folders vengono ignorate perché la sincronizzazione non è necessaria. Le poche eccezioni sono elencate qui.
Cartelle predefinite da sincronizzare

   * segmenti/punteggio
   * social/relazioni
   * attività

### 9. ID Sling univoco {#unique-sling-id}

>[!CAUTION]
>
>Se l’ID Sling corrisponde a due o più istanze di pubblicazione, la sincronizzazione dei gruppi di utenti non riesce.

Se l’ID Sling è lo stesso per più istanze pubblicate in una farm di pubblicazione, i gruppi di utenti non verranno sincronizzati.

Per verificare che tutti i valori Sling ID siano diversi, per ogni istanza di pubblicazione:

1. individuare `http://<host>:<port>/system/console/status-slingsettings`
1. verificare il valore di **Sling ID**

![](assets/chlimage_1-27.png)

Se l’ID Sling di un’istanza di pubblicazione corrisponde all’ID Sling di qualsiasi altra istanza di pubblicazione, effettuate le seguenti operazioni:

1. arrestate una delle istanze di pubblicazione con un ID Sling corrispondente
1. nella directory crx-quickstart/launchpad/felix

   * cercare ed eliminare il file denominato *sling.id.file*

      * ad esempio, su un sistema Linux:
         `rm -i $(find . -type f -name sling.id.file)`

      * ad esempio, in un sistema Windows:
         `use windows explorer and search for *sling.id.file*`

1. avviare l’istanza di pubblicazione

   * all’avvio, gli verrà assegnato un nuovo ID Sling

1. verifica che l&#39; **Sling ID** sia ora univoco

Ripetete questi passaggi finché tutte le istanze di pubblicazione non dispongono di un ID Sling univoco.

## Vault Package Builder Factory {#vault-package-builder-factory}

Per sincronizzare correttamente gli aggiornamenti, è necessario modificare il generatore di pacchetti vault per la sincronizzazione utente:

* su ogni istanza di pubblicazione AEM
* accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

   * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* individuare la `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* seleziona l’icona di modifica
* aggiungere due `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* gestione dei criteri:

   * per sovrascrivere i nodi rep:policy esistenti con i nuovi, aggiungete un terzo filtro pacchetto:

      * `/home/users|+.*/rep:policy`
   * per impedire la distribuzione dei criteri, impostare

      * `Acl Handling:` `IGNORE`


![Vault Package Builder Factory](assets/vault-package-builder-factory.png)

## Cosa Succede Quando ... {#what-happens-when}

### Utente si registra o modifica il profilo in Pubblica {#user-self-registers-or-edits-profile-on-publish}

Per impostazione predefinita, gli utenti e i profili creati nell’ambiente di pubblicazione (registrazione automatica) non vengono visualizzati nell’ambiente di authoring.

Se la topologia è una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm) e la sincronizzazione utente è stata configurata correttamente, i profili *utente *e *utente* vengono sincronizzati nella farm di pubblicazione utilizzando la distribuzione Sling.

### Utenti o gruppi di utenti creati utilizzando la console di sicurezza {#users-or-user-groups-are-created-using-security-console}

Per impostazione predefinita, i dati utente creati nell’ambiente di pubblicazione non vengono visualizzati nell’ambiente di authoring e viceversa.

Quando si utilizza la console [Amministrazione utente e sicurezza](/help/sites-administering/security.md) per aggiungere nuovi utenti nell&#39;ambiente di pubblicazione, la sincronizzazione degli utenti sincronizzerà i nuovi utenti e i relativi membri del gruppo con altre istanze di pubblicazione, se necessario. La sincronizzazione utente sincronizza anche i gruppi di utenti creati tramite la console di protezione.

## Risoluzione dei problemi {#troubleshooting}

### Come attivare la sincronizzazione degli utenti offline {#how-to-take-user-sync-offline}

Per ottimizzare la sincronizzazione degli utenti, per [rimuovere un editore](#how-to-remove-a-publisher) o [sincronizzare manualmente i dati](#manually-syncing-users-and-user-groups), la coda di distribuzione deve essere vuota e silenziosa.

Per verificare lo stato della coda di distribuzione:

* autore:

   * utilizzando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * cercare le voci in `/var/sling/distribution/packages`

         * nodi di cartella denominati con il pattern `distrpackage_*`
   * utilizzo di [Gestione pacchetti](/help/sites-administering/package-manager.md)

      * cercare pacchetti in sospeso (non ancora installati)

         * denominato con il pattern `socialpubsync-vlt*`
         * creato da `communities-user-admin`


Quando la coda di distribuzione è vuota, disattivate la sincronizzazione utente:

* sull&#39;autore

   * *Deselezionare la casella di controllo `Enabled` per [agente di distribuzione Apache Sling - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)

Al termine delle attività, per riattivare la sincronizzazione utente:

* sull&#39;autore

   * selezionare la casella di controllo `Enabled` per [agente di distribuzione Apache Sling - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnostica sincronizzazione utenti {#user-sync-diagnostics}

Diagnostica sincronizzazione utenti è uno strumento che controlla la configurazione e tenta di identificare eventuali problemi.

Per l&#39;autore, è sufficiente spostarsi dalla console principale attraverso **Strumenti, Operazioni, Diagnosi, Diagnostica sincronizzazione utenti.**

I risultati verranno visualizzati semplicemente entrando nella console Diagnostica sincronizzazione utenti.

Questo è ciò che viene visualizzato quando la sincronizzazione utente non è stata abilitata:

![](assets/chlimage_1-28.png)

#### Come eseguire la diagnostica per gli editori {#how-to-run-diagnostics-for-publishers}

Quando la diagnostica viene eseguita dall&#39;ambiente di authoring, i risultati di esito positivo/negativo includeranno una sezione [INFO] che mostra l&#39;elenco delle istanze di pubblicazione configurate per la conferma.

Nell’elenco è incluso un URL per ogni istanza di pubblicazione che eseguirà la diagnostica per tale istanza. Il parametro url `syncUser` viene aggiunto all&#39;URL di diagnostica con il relativo valore impostato sull&#39; *utente di sincronizzazione autorizzato* creato in [Passaggio 2](#createauthuser).

**Nota**: prima di avviare l’URL, l’ *utente di sincronizzazione* autorizzato deve già essere connesso a tale istanza di pubblicazione.

![](assets/chlimage_1-29.png)

### Configurazione aggiunta errata {#configuration-improperly-added}

Quando la sincronizzazione degli utenti non funziona, il problema più comune è che sono state aggiunte *configurazioni aggiuntive*. Al contrario, la *configurazione esistente *predefinita dovrebbe essere stata modificata **.

Di seguito sono riportate le visualizzazioni di come dovrebbero essere visualizzate le configurazioni modificate e predefinite nella console Web. Se viene visualizzata più di un&#39;istanza, la configurazione aggiunta deve essere rimossa.

#### (autore) Un agente di distribuzione Apache Sling - Sync Agent Factory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### (autore) Credenziali di trasporto di distribuzione Apache Sling - Credenziali utente basate su DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### (pubblicare) Un agente di distribuzione Apache Sling - Coda agenti Factory {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### (pubblicare) Un  Adobe Social Sync - Diff Observer Factory {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### (autore) Un trigger di distribuzione Apache Sling - Pianificato Triggers Factory {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### Modifica eccezione operazione durante l&#39;elaborazione delle risposte {#modify-operation-exception-during-response-processing}

Se nel registro è visibile quanto segue:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

Quindi verificare che la sezione [2. Create Authorized User](#createauthuser) è stato seguito correttamente.

Questa sezione descrive come creare un utente autorizzato, che esiste su tutte le istanze di pubblicazione e identificarlo nella configurazione OSGi &#39;Provider segreto&#39; dell&#39;autore. Per impostazione predefinita, l&#39;utente è `admin`.

L&#39;utente autorizzato deve essere membro del gruppo di utenti **`administrators`** e le autorizzazioni per tale gruppo non devono essere modificate.

L’utente autorizzato deve avere esplicitamente i seguenti privilegi e restrizioni su tutte le istanze di pubblicazione:

| **path** | **jcr:all** | **rep:idspn** |
|---|---|---|
| /home | X | */attività/* |
| /home/users | X | */attività/* |
| /home/groups | X | */attività/* |

Come membro del gruppo `administrators`, l&#39;utente autorizzato deve disporre dei seguenti privilegi su tutte le istanze di pubblicazione:

| **path** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Sincronizzazione gruppo utenti non riuscita {#user-group-sync-failed}

Se l’ID Sling corrisponde a due o più istanze di pubblicazione, la sincronizzazione dei gruppi di utenti non riesce.

Vedere la sezione [9. ID Sling univoco](#unique-sling-id)

### Sincronizzazione manuale di utenti e gruppi di utenti {#manually-syncing-users-and-user-groups}

* sull’editore in cui sono presenti utenti e gruppi di utenti:

   * [se abilitata, disabilitate la sincronizzazione utente](#how-to-take-user-sync-offline)
   * [creare un ](/help/sites-administering/package-manager.md#creating-a-new-package) pacchetto di  `/home`

      * durante la modifica del pacchetto

         * Scheda Filtri: Aggiungi filtro: Percorso directory principale: `/home`
         * Scheda Avanzate: Gestione AC: `Overwrite`
   * [esportare il pacchetto](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* in altre istanze di pubblicazione:

   * [importare il pacchetto](/help/sites-administering/package-manager.md#installing-packages)

Per configurare o abilitare la sincronizzazione degli utenti, andate al punto 1: [Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)

### Quando un editore diventa non disponibile {#when-a-publisher-becomes-unavailable}

Quando un&#39;istanza di pubblicazione diventa non disponibile, non deve essere rimossa se torna in linea in futuro. Le modifiche verranno messe in coda per l&#39;editore e, una volta che l&#39;editore sarà nuovamente online, saranno elaborate.

Se l’istanza di pubblicazione non torna mai online, se è offline in modo permanente, deve essere rimossa perché la compilazione della coda comporterà un utilizzo notevole dello spazio su disco nell’ambiente di authoring.

Quando un editore non è attivo, nel registro dell’autore sono presenti eccezioni simili a:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Come rimuovere un editore {#how-to-remove-a-publisher}

Per rimuovere un editore dall&#39; [agente di distribuzione Apache Sling - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory), la coda di distribuzione deve essere vuota e silenziosa.

* autore:

   * [Sincronizzazione utenti offline](#how-to-take-user-sync-offline)
   * seguire il passaggio 7[ per rimuovere l&#39;editore da entrambi gli elenchi server:](#apache-sling-distribution-agent-sync-agents-factory)

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * riabilitare la sincronizzazione degli utenti

      * selezionare la casella di controllo `Enabled` per [agente di distribuzione Apache Sling - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)
