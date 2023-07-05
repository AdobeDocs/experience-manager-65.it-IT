---
title: Sincronizzazione utente
seo-title: User Synchronization
description: Scopri come sincronizzare gli utenti in AEM.
seo-description: Learn about user synchronization in AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
source-git-commit: f0acb130e1c68b927356c4e0ea625bbd88a6fc19
workflow-type: tm+mt
source-wordcount: '2527'
ht-degree: 5%

---


# Sincronizzazione utente{#user-synchronization}

## Introduzione {#introduction}

Quando la distribuzione è un [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm), i membri devono essere in grado di accedere e visualizzare i propri dati su qualsiasi nodo di pubblicazione.

Gli utenti e i gruppi di utenti (dati utente) creati nell’ambiente di pubblicazione non sono necessari nell’ambiente di authoring.

La maggior parte dei dati utente creati nell’ambiente di authoring deve rimanere in tale ambiente e non deve essere copiata nelle istanze di pubblicazione.

La registrazione e le modifiche effettuate su un’istanza Publish devono essere sincronizzate con altre istanze Publish affinché possano accedere agli stessi dati utente.

A partire da AEM 6.1, quando la sincronizzazione utente è abilitata, i dati utente vengono sincronizzati automaticamente tra le istanze di pubblicazione nella farm e non vengono creati durante l’authoring.

## Distribuzione Sling {#sling-distribution}

I dati utente, insieme ai relativi [ACL](/help/sites-administering/security.md), sono archiviati in [Oak Core](/help/sites-deploying/platform.md), il livello sotto Oak JCR e sono accessibili utilizzando [API Oak](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Con aggiornamenti non frequenti, è ragionevole sincronizzare i dati utente con altre istanze di pubblicazione utilizzando [Distribuzione dei contenuti Sling](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (distribuzione Sling).

Rispetto alla replica tradizionale, la sincronizzazione degli utenti con la distribuzione Sling offre i seguenti vantaggi:

* *utenti*, *profili utente* e *gruppi di utenti* create al momento della pubblicazione non vengono create nell’ambiente di authoring

* La distribuzione Sling imposta le proprietà negli eventi JCR, consentendo di agire all’interno dei listener di eventi lato pubblicazione senza preoccuparsi di cicli di replica infiniti
* La distribuzione Sling invia solo i dati utente alle istanze di pubblicazione non originarie, eliminando il traffico non necessario
* [ACL](/help/sites-administering/security.md) impostati nel nodo utente sono inclusi nella sincronizzazione

>[!NOTE]
>
>Se sono necessarie sessioni, è consigliabile utilizzare una soluzione SSO o utilizzare una sessione fissa e chiedere ai clienti di accedere se passano a un’altra istanza di pubblicazione.

>[!CAUTION]
>
>Sincronizzazione del **amministratori** il gruppo non è supportato, anche quando la sincronizzazione utente è abilitata. Al contrario, l’errore &quot;importa la diff&quot; verrà registrato nel registro degli errori.
>
>Pertanto, quando la distribuzione è una farm di pubblicazione, se un utente viene aggiunto o rimosso dalla **amministratori** gruppo, la modifica deve essere eseguita manualmente su ogni istanza Publish.

## Abilita sincronizzazione utenti {#enable-user-sync}

>[!NOTE]
>
>Per impostazione predefinita, la sincronizzazione utente è `disabled`.
>
>Per abilitare la sincronizzazione degli utenti è necessario modificare *esistente* Configurazioni OSGi.
>
>Non è possibile aggiungere nuove configurazioni abilitando la sincronizzazione degli utenti.

La sincronizzazione degli utenti si basa sull’ambiente di authoring per gestire le distribuzioni dei dati utente, anche se i dati utente non vengono creati sull’ambiente di authoring. Gran parte della configurazione, ma non tutte, si svolge nell’ambiente di authoring e ogni passaggio identifica chiaramente se deve essere eseguita all’autore o alla pubblicazione.

Di seguito sono riportati i passaggi necessari per abilitare la sincronizzazione utente, seguiti da [Risoluzione dei problemi](#troubleshooting) sezione:

### Prerequisiti {#prerequisites}

1. Se utenti e gruppi di utenti sono già stati creati in un’istanza Publish, si consiglia di: [sincronizzazione manuale](#manually-syncing-users-and-user-groups) i dati utente a tutte le istanze di pubblicazione prima di configurare e abilitare la sincronizzazione utente.

Una volta abilitata la sincronizzazione degli utenti, vengono sincronizzati solo gli utenti e i gruppi appena creati.

1. Verifica che sia stato installato il codice più recente:

* [Aggiornamenti della piattaforma AEM](https://helpx.adobe.com/it/experience-manager/kb/aem62-available-hotfixes.html)
* [Aggiornamenti di AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione {#apache-sling-distribution-agent-sync-agents-factory}

**Abilita sincronizzazione utenti**

* **all’autore**

   * accedi con privilegi di amministratore
   * accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individuare `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita) Verifica `name`: **`socialpubsync`**

      * seleziona la `Enabled` casella di controllo
      * seleziona `Save`

![Agente di distribuzione Apache Sling](assets/chlimage_1-20.png)

### 2. Crea utente autorizzato {#createauthuser}

**Configurare le autorizzazioni**
Questo utente autorizzato verrà utilizzato nel passaggio 3 per configurare la distribuzione Sling durante l’authoring.

* **su ogni istanza di pubblicazione**

   * accedi con privilegi di amministratore
   * accedere a [Console di sicurezza](/help/sites-administering/security.md)

      * ad esempio: [https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * crea un nuovo utente

      * ad esempio, `usersync-admin`

   * aggiungi questo utente a **`administrators`** gruppo utenti
   * [aggiungi ACL per questo utente a /home](#howtoaddacl)

      * `Allow jcr:all` con restrizione `rep:glob=*/activities/*`

>[!CAUTION]
>
>Creare un nuovo utente.
>
>* L&#39;utente predefinito assegnato è **`admin`**.
>* Non usi `communities-user-admin user.`
>

#### Come aggiungere ACL {#addacls}

* access CRXDE Lite

   * ad esempio: [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* seleziona `/home` nodo
* nel riquadro a destra, selezionare `Access Control` scheda
* seleziona la `+` per aggiungere una voce ACL

   * **Entità**: *cerca l&#39;utente creato per la sincronizzazione utente*
   * **Tipo**: `Allow`
   * **Privilegi**: `jcr:all`
   * **Restrizioni** rep:glob: `*/activities/*`
   * seleziona **OK**

* seleziona **Salva tutto**

![Finestra Aggiungi ACL](assets/chlimage_1-21.png)

Consulta anche

* [Gestione diritti di accesso](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Sezione Risoluzione dei problemi [Modifica eccezione operazione durante l&#39;elaborazione della risposta](#modify-operation-exception-during-response-processing).

### 3. Adobe Granite Distribution - Provider segreto di trasporto con password crittografata {#adobegraniteencpasswrd}

**Configurare le autorizzazioni**

Una volta che un utente autorizzato, un membro di **`administrators`** Il gruppo di utenti, è stato creato in tutte le istanze di pubblicazione e l’utente autorizzato deve essere identificato nell’autore come autorizzato a sincronizzare i dati utente dall’autore alla pubblicazione.

* **all’autore**

   * accedi con privilegi di amministratore
   * accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individuare `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita) Verifica `property name`: **`socialpubsync-publishUser`**

   * imposta il nome utente e la password su [utente autorizzato](#createauthuser) creato al momento della pubblicazione nel passaggio 2

      * ad esempio, `usersync-admin`

![Provider segreto di trasporto per password crittografata](assets/chlimage_1-22.png)

### 4. Agente di distribuzione Apache Sling - Factory agenti coda {#apache-sling-distribution-agent-queue-agents-factory}

**Abilita sincronizzazione utenti**

* **su ogni istanza di pubblicazione**:

   * accedi con privilegi di amministratore
   * accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * individuare `Apache Sling Distribution Agent - Queue Agents Factory`

      * seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita) Verifica `Name`: `socialpubsync-reverse`

      * seleziona la `Enabled` casella di controllo
      * seleziona `Save`

   * **repeat** per ogni istanza di pubblicazione

![Factory agenti coda](assets/chlimage_1-23.png)

### 5. Sincronizzazione Adobe Social - Diff Observer Factory {#diffobserver}

**Abilita sincronizzazione gruppi**

* **su ogni istanza di pubblicazione**:

   * accedi con privilegi di amministratore
   * accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * individuare **`Adobe Social Sync - Diff Observer Factory`**

      * seleziona la configurazione esistente da aprire per la modifica (icona matita)

        Verifica `agent name`: `socialpubsync-reverse`

      * seleziona la `Enabled` casella di controllo
      * seleziona `Save`

![Diff Observer Factory](assets/screen-shot_2019-05-24at090809.png)

### 6. Trigger di distribuzione Apache Sling - Fabbrica dei trigger pianificati {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Facoltativo) modifica intervallo di polling**

Per impostazione predefinita, l’autore esegue il polling delle modifiche ogni 30 secondi. Per modificare questo intervallo:

* **all’autore**

   * accedi con privilegi di amministratore
   * accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individuare `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * seleziona la configurazione esistente da aprire per la modifica (icona matita)

         * Verifica `Name`: `socialpubsync-scheduled-trigger`

      * imposta `Interval in Seconds` all&#39;intervallo desiderato
      * seleziona `Save`

![Fabbrica attivatori pianificati](assets/chlimage_1-24.png)

## Configurazione per più istanze di pubblicazione {#configure-for-multiple-publish-instances}

La configurazione predefinita è per una singola istanza di pubblicazione. Poiché il motivo per abilitare la sincronizzazione degli utenti è quello di sincronizzare più istanze di pubblicazione, ad esempio per una farm di pubblicazione, sarà necessario aggiungere le istanze di pubblicazione aggiuntive alla factory degli agenti di sincronizzazione.

### 7. Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione {#apache-sling-distribution-agent-sync-agents-factory-1}

**Aggiungi istanze di pubblicazione:**

* **all’autore**

   * accedi con privilegi di amministratore
   * accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individuare `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita) Verifica `Name`: `socialpubsync`

![Factory agenti di sincronizzazione](assets/chlimage_1-25.png)

* **Endpoint esportazione**
Deve essere presente un endpoint di esportazione per ogni istanza di pubblicazione. Ad esempio, se sono presenti 2 istanze Publish, localhost:4503 e 4504, devono essere presenti 2 voci:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Endpoint importazione**
Deve essere presente un endpoint di importazione per ogni istanza di pubblicazione. Ad esempio, se sono presenti 2 istanze Publish, localhost:4503 e 4504, devono essere presenti 2 voci:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* seleziona `Save`

### 8. Listener di sincronizzazione utenti di AEM Communities {#aem-communities-user-sync-listener}

**(Facoltativo) Sincronizza nodi JCR aggiuntivi**

Se sono presenti dati personalizzati che devono essere sincronizzati tra più istanze di pubblicazione:

* **su ogni istanza di pubblicazione**:

   * accedi con privilegi di amministratore
   * accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, `https://localhost:4503/system/console/configMgr`

   * individuare `AEM Communities User Sync Listener`
   * seleziona la configurazione esistente da aprire per la modifica (icona a forma di matita) Verifica `Name`: `socialpubsync-scheduled-trigger`

![Listener di sincronizzazione utenti AEM Communities](assets/chlimage_1-26.png)

* **Tipi di nodo**
Elenco dei tipi di nodo che verranno sincronizzati. Qualsiasi tipo di nodo diverso da sling:Folder deve essere elencato qui (sling:folder viene gestito separatamente).
Elenco predefinito di tipi di nodo da sincronizzare:

   * rep:Utente
   * nt:unstructured
   * nt:resource

* **Proprietà ignorabili**
Questo è l&#39;elenco delle proprietà che verranno ignorate se viene rilevata una modifica. Le modifiche a queste proprietà potrebbero essere sincronizzate come effetto collaterale di altre modifiche (poiché la sincronizzazione è sempre a livello di nodo), ma le modifiche a queste proprietà non attiveranno di per sé la sincronizzazione.
Proprietà predefinita da ignorare:

   * cq:lastModified

* **Nodi ignorabili**
Sottopercorsi che verranno completamente ignorati durante la sincronizzazione. In questi percorsi secondari non verrà sincronizzato in alcun momento.
Nodi predefiniti da ignorare:

   * .token
   * system

* **Cartelle distribuite**
La maggior parte di sling:Folders viene ignorata perché la sincronizzazione non è necessaria. Le poche eccezioni sono elencate qui.
Cartelle predefinite da sincronizzare

   * segmenti/punteggio
   * social/relazioni
   * attività

### 9. ID Sling univoco {#unique-sling-id}

>[!CAUTION]
>
>Se l’ID Sling corrisponde tra due o più istanze di pubblicazione, la sincronizzazione dei gruppi di utenti non riuscirà.

Se l’ID Sling è lo stesso per più istanze di pubblicazione in una farm di pubblicazione, i gruppi di utenti non verranno sincronizzati.

Per verificare che tutti i valori degli ID Sling siano diversi, per ogni istanza di pubblicazione:

1. sfoglia per `http://<host>:<port>/system/console/status-slingsettings`
1. controlla il valore di **ID Sling**

![Controllo del valore di Sling ID](assets/chlimage_1-27.png)

Se l’ID Sling di un’istanza Publish corrisponde all’ID Sling di qualsiasi altra istanza Publish:

1. arresta una delle istanze di pubblicazione con un ID Sling corrispondente
1. nella directory crx-quickstart/launchpad/felix

   * cerca ed elimina il file denominato *sling.id.file*

      * ad esempio, su un sistema Linux:
        `rm -i $(find . -type f -name sling.id.file)`

      * ad esempio, in un sistema Windows:
        `use windows explorer and search for *sling.id.file*`

1. avvia l’istanza Publish

   * all’avvio gli verrà assegnato un nuovo ID Sling

1. verificare che **ID Sling** è ora univoco

Ripeti questi passaggi fino a quando tutte le istanze di pubblicazione non avranno un ID Sling univoco.

## Generatore pacchetti Vault - Fabbrica {#vault-package-builder-factory}

Per consentire la corretta sincronizzazione degli aggiornamenti, è necessario modificare il generatore di pacchetti di Vault per la sincronizzazione utente:

* su ogni istanza di pubblicazione AEM
* accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

   * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* individuare `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* seleziona l’icona modifica
* aggiungi due `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* gestione delle policy:

   * per sovrascrivere i nodi rep:policy esistenti con quelli nuovi, aggiungete un terzo filtro pacchetto:

      * `/home/users|+.*/rep:policy`

   * per impedire la distribuzione dei criteri, impostare

      * `Acl Handling:` `IGNORE`

![Generatore pacchetti Vault - Fabbrica](assets/vault-package-builder-factory.png)

## Cosa Succede Quando... {#what-happens-when}

### Autoregistrazione utente o modifica profilo durante la pubblicazione {#user-self-registers-or-edits-profile-on-publish}

Per progettazione, gli utenti e i profili creati nell’ambiente di pubblicazione (registrazione autonoma) non vengono visualizzati nell’ambiente di authoring.

Quando la topologia è [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm) e la sincronizzazione utente è stata configurata correttamente, il *utente* e *profilo utente* viene sincronizzato nella farm di pubblicazione utilizzando la distribuzione Sling.

### Gli utenti o i gruppi di utenti vengono creati utilizzando la console Sicurezza {#users-or-user-groups-are-created-using-security-console}

Per progettazione, i dati utente creati nell’ambiente di pubblicazione non vengono visualizzati nell’ambiente di authoring e viceversa.

Quando [Amministrazione utenti e sicurezza](/help/sites-administering/security.md) viene utilizzata per aggiungere nuovi utenti nell’ambiente di pubblicazione; se necessario, la sincronizzazione utenti sincronizzerà i nuovi utenti e la loro appartenenza al gruppo con altre istanze di pubblicazione. La sincronizzazione degli utenti sincronizzerà anche i gruppi di utenti creati tramite la console di sicurezza.

## Risoluzione dei problemi {#troubleshooting}

### Come portare offline User Sync {#how-to-take-user-sync-offline}

Per portare offline la sincronizzazione degli utenti, per [rimuovere un’istanza Publish](#how-to-remove-a-publish-instance) o [sincronizzare manualmente i dati](#manually-syncing-users-and-user-groups), la coda di distribuzione deve essere vuota e silenziosa.

Per verificare lo stato della coda di distribuzione:

* sull’autore:

   * utilizzo [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * cerca voci in `/var/sling/distribution/packages`

         * nodi di cartelle denominati con il modello `distrpackage_*`

   * utilizzo [Gestione pacchetti](/help/sites-administering/package-manager.md)

      * cerca pacchetti in sospeso (non ancora installati)

         * denominato con il pattern `socialpubsync-vlt*`
         * creato da `communities-user-admin`

Quando la coda di distribuzione è vuota, disabilita la sincronizzazione utente:

* all’autore

   * *deselezionare *il `Enabled` casella di controllo per [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory)

Una volta completate le attività, per riattivare la sincronizzazione utente:

* all’autore

   * controlla la `Enabled` casella di controllo per [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnostica sincronizzazione utenti {#user-sync-diagnostics}

Diagnostica sincronizzazione utenti è uno strumento che controlla la configurazione e tenta di identificare eventuali problemi.

Durante l’authoring, passa semplicemente dalla console principale alle **Strumenti, operazioni, diagnostica, diagnostica sincronizzazione utenti.**

I risultati vengono visualizzati semplicemente inserendo la console di diagnostica Sincronizzazione utenti.

Questo viene visualizzato quando Sincronizzazione utente non è stata abilitata:

![Avviso di mancato funzionamento di Diagnostica sincronizzazione utenti](assets/chlimage_1-28.png)

#### Eseguire la diagnostica per le istanze di pubblicazione {#how-to-run-diagnostics-for-publish-instances}

Quando la diagnostica viene eseguita dall’ambiente di authoring, i risultati superati/non superati includeranno [INFO] sezione in cui viene visualizzato l’elenco delle istanze di pubblicazione configurate per la conferma.

Nell’elenco è incluso un URL per ogni istanza di pubblicazione che eseguirà la diagnostica per tale istanza. Parametro URL `syncUser` viene aggiunto all&#39;URL di diagnostica con il relativo valore impostato su *utente di sincronizzazione autorizzato* creato in [Passaggio 2](#createauthuser).

**Nota**: prima di avviare l’URL, il *utente di sincronizzazione autorizzato* deve già essere connesso a tale istanza di pubblicazione.

![Diagnostica per le istanze di pubblicazione](assets/chlimage_1-29.png)

### Configurazione aggiunta in modo errato {#configuration-improperly-added}

Quando la sincronizzazione utente non funziona, il problema più comune è che configurazioni aggiuntive erano *aggiunto*. Invece, la configurazione *predefinita esistente* avrebbe dovuto essere *modificato*.

Di seguito sono riportate le visualizzazioni delle configurazioni predefinite modificate da visualizzare nella console Web. Se compaiono più istanze, la configurazione aggiunta deve essere rimossa.

#### (author) Un agente di distribuzione Apache Sling - Sync Agents Factory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![Visualizzazione Configurazioni predefinite modificate nella console Web](assets/chlimage_1-30.png)

#### (author) Una credenziale trasporto distribuzione Apache Sling - Credenziali utente basate su DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![Visualizzazione Configurazioni predefinite modificate nella console Web](assets/chlimage_1-31.png)

#### (pubblicazione) Un agente di distribuzione Apache Sling - Queue Agents Factory {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![Visualizzazione Configurazioni predefinite modificate nella console Web](assets/chlimage_1-32.png)

#### (pubblicazione) One Adobe Social Sync - Diff Observer Factory {#publish-one-adobe-social-sync-diff-observer-factory}

![Visualizzazione Configurazioni predefinite modificate nella console Web](assets/chlimage_1-33.png)

#### (author) Un trigger di distribuzione Apache Sling - Factory di trigger pianificati {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![Visualizzazione Configurazioni predefinite modificate nella console Web](assets/chlimage_1-34.png)

### Modifica eccezione operazione durante l&#39;elaborazione della risposta {#modify-operation-exception-during-response-processing}

Se nel registro è visibile quanto segue:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

Verifica quindi che la sezione [2. Crea utente autorizzato](#createauthuser) è stato seguito correttamente.

Questa sezione descrive come creare un utente autorizzato, presente in tutte le istanze di pubblicazione, e come identificarlo nella configurazione OSGi &quot;Provider segreto&quot; nell’ambiente di authoring. Per impostazione predefinita, l’utente è `admin`.

L’utente autorizzato deve diventare membro del **`administrators`** Il gruppo utenti e le autorizzazioni per tale gruppo non devono essere modificati.

L’utente autorizzato deve disporre esplicitamente dei seguenti privilegi e restrizioni su tutte le istanze di pubblicazione:

| **percorso** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | &#42;/attività/&#42; |
| /home/users | X | &#42;/attività/&#42; |
| /home/groups | X | &#42;/attività/&#42; |

In qualità di membro del `administrators` l’utente autorizzato deve disporre dei seguenti privilegi su tutte le istanze di pubblicazione:

| **percorso** | **jcr:all** | **jcr:read** | **rep:scrittura** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Sincronizzazione gruppo utenti non riuscita {#user-group-sync-failed}

Se l’ID Sling corrisponde tra due o più istanze di pubblicazione, la sincronizzazione dei gruppi di utenti non riuscirà.

Vedere la sezione [9. ID Sling univoco](#unique-sling-id)

### Sincronizzazione manuale di utenti e gruppi di utenti {#manually-syncing-users-and-user-groups}

* nelle istanze di pubblicazione in cui esistono utenti e gruppi di utenti:

   * [se abilitata, disabilita la sincronizzazione utenti](#how-to-take-user-sync-offline)
   * [creare un pacchetto](/help/sites-administering/package-manager.md#creating-a-new-package) di `/home`

      * durante la modifica del pacchetto

         * Scheda Filtri: Aggiungi filtro: Percorso directory principale: `/home`
         * Scheda Avanzate: Gestione AC: `Overwrite`

   * [esportare il pacchetto](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* in altre istanze di pubblicazione:

   * [importare il pacchetto](/help/sites-administering/package-manager.md#installing-packages)

Per configurare o abilitare la sincronizzazione utente, andare al passaggio 1: [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory)

### Quando un’istanza Publish non è più disponibile {#when-a-publish-instance-becomes-unavailable}

Quando un’istanza pubblicata non è più disponibile, non deve essere rimossa se tornerà online in futuro. Le modifiche verranno messe in coda per l’istanza di pubblicazione e, una volta tornata online, verranno elaborate.

Se l’istanza Publish non sarà mai più online o è offline in modo permanente, deve essere rimossa perché l’accumulo della coda determinerà un notevole utilizzo di spazio su disco nell’ambiente di authoring.

Quando un’istanza Publish è inattiva, il registro di authoring presenta eccezioni simili alle seguenti:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Come rimuovere un’istanza di pubblicazione {#how-to-remove-a-publish-instance}

Per rimuovere un&#39;istanza Publish da [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory), la coda di distribuzione deve essere vuota e silenziosa.

* sull’autore:

   * [Disconnetti sincronizzazione utenti](#how-to-take-user-sync-offline)
   * seguire [passaggio 7](#apache-sling-distribution-agent-sync-agents-factory) per rimuovere l’istanza Publish da entrambi gli elenchi di server:

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * riabilita sincronizzazione utenti

      * controlla la `Enabled` casella di controllo per [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory)
